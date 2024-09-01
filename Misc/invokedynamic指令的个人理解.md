---
title: invokedynamic指令的个人理解
date: false
keywords: JVM, invokedynamic, ASM, 使用, 理解, lovexyn0827
desc: 试着在3000字以内讲清自己对Java 7中引入的`invokedynamic`的理解。这篇文章主要是省去了一些对Java API与JVM规范的引述，并侧重于该指令本身的使用的基本思路。如有缺漏错误之处，欢迎反馈。
id: understanding_invokedynamic:0
draft: false
---

# `invokedynamic`指令的个人理解

## 前言

试着在3000字以内讲清自己对Java 7中引入的`invokedynamic`的理解。这篇文章主要是省去了一些对Java API与JVM规范的引述，并侧重于该指令本身的使用的基本思路。如有缺漏错误之处，欢迎反馈。

此处假定读者掌握以下知识：

- Java语言
- JVM的基本运行模型
- 基本的字节码指令
- ASM的基本结构与简单使用

---

## 概述

`invokedynamic`这一指令由两个词语组成，即invoke（v., 调用）与dynamic（adv. & adj., 动态的），顾名思义，这条指令可以访问一个在运行时动态地确定而非硬编码于类文件中的目标。

简单来说，这条指令的执行包括以下几个步骤：

1. 如果是第一次执行，调用指令附加参数中给出的一个方法（`BootstrapMethod`）来确定该指令的行为，如调用哪一个方法或者是访问哪一个字段。
2. 按照第一次执行时确定的行为执行具体操作。

---

## 方法句柄`MethodHandle`

方法句柄代表了一个对类成员的基本操作，包括读写字段（等价于getter或setter）和调用方法等。可以认为，一个方法句柄包含了一个具体成员的位置与其执行的具体操作两个属性。

可以通过由`java.invoke.MethodHandles.lookup()`方法获取的`MethodHandles.Lookup`实例中提供的工厂方法获取`MethodHandle`实例。那些工厂方法大致可以分为两类，一类是名称类似`findXXX()`的方法，支持使用类似于反射的方式获取方法句柄；另一类工厂方法的名称类似于`unflectXXX()`，支持为已有的`Field`或`Method`对象指定具体操作以将其转换为方法句柄。

第一类工厂方法的形式大多类似于`findXXX(class, name, type)`，三个参数分别为定义目标成员的类相应的`Class`实例、目标成员的名称与目标成员的确切类型（或方法签名）。唯一的例外是`findConstructor`方法，因为它不需要显式地指明名称。在获取操作方法的方法句柄时，需要使用一个`MethodType`实例来表示方法签名，这个实例可以通过工厂方法`MethodType.methodType()`获取。

第二类工厂方法的形式比较简单，只接受一个`Field`或`Method`实例，此处不再细说。

另外，这些工厂方法在执行时通常会检查曾获取所用的`Lookup`实例的类是否能访问目标成员，如果失败则抛出一个`IllegalAccessException`。在Java 9及以后的版本中，我们可以使用`privateLookupIn()`工厂方法获取可以访问调用类以外的其他类的私有成员的`Lookup`实例。对于第二类工厂方法，我们可以预先在用到的反射对象上调用`setAccessible(true)`来禁用这一访问检查，或许这也是Java 8中唯一可以获取任意私有方法句柄的方案。

`MethodHandles`类中也提供了多个工厂方法以获取或变换一些方法句柄，此处不再赘述。

---

## 调用站点`CallSite`

调用站点是一个方法句柄的容器，可以在需要时提供一个`MethodHandle`实例。方法句柄只有被包含在调用站点中时才可以在`invokedynamic`指令中使用。

调用站点可以是可变的（`MutableCallSite`，`VolatileCallSite`），也可以是不可变的（`ConstantCallSite`）。不可变的调用站点可能会更高效，因为JVM可以对其进行一些优化。

也可以创建自己的`CallSite`子类以实现一些自定义逻辑，如在调用次数超过一定值的前后提供不同的方法句柄。

---

## `BootstrapMethod`

`BootstrapMethod`，简称“BSM”，是一个用于在运行时确定`invokedynamic`指令的具体行为的方法。当然，Java 11中引入的动态常量也使用了相同的技术，但是这超出了本文的范围，此处不再详述。

一个`BootstrapMethod`通常是一个静态方法，前三个参数的类型必须依次为：

1. `MethodHandles.Lookup`
2. `String`
3. `MethodType`

这些参数后面还可以附加几个参数用于传递一些附加信息。Java 10及之前的版本中，附加的参数类型可以为`int`、`float`、`long`、`double`、`String`、`MethodType`或`MethodHandle`。同时，该方法必须返回一个`CallSite`实例。下方是一个简单的`BootstrapMethod`的定义：

````java
protected static CallSite methodBSM(MethodHandles.Lookup lookup, String name, MethodType type)
````

Java 11中也允许借助动态常量技术使用其他类型的附加参数，此处不再赘述。
在执行该方法时，传入的参数依次是：

- 由`invokedynamic`所在类通过`MethodHandles.lookup()`工厂方法获取的`MethodHandles.Lookup`实例；
- 为`invokedynamic`指令指定的名称；
- 描述该`invokedynamic`行为的方法描述符
- 附加的零至多个参数
  JVM标准中规定，也可以使用构造器作为`BootstrapMethod`，只要那个构造器能够构造出一个CallSite类型的对象。具体实现与使用静态方法类似，此处不再赘述。
  有必要说明，通过附加参数给出的`MethodHandle`不可以访问`invokedynamic`指令所在类不可访问的成员，否则在类的解析阶段会因为访问检查出错而抛出`IllegalAccessError`。

---

## `invokedynamic`指令的格式

JVM字节码中`invokedynamic`指令的格式非常简单:

```asm
invokedynamic index_1 index_2 0 0
```


其中，两个`index`字节共同组成了一个指向常量池中一个`CONSTANT_InvokeDynamic_info`结构的索引，该结构直接或间接地提供了以下信息：

- `invokedynamic`的名称与对应的方法描述符；
- `BootstrapMethod`方法信息，可以指定一个静态方法或构造器；
- `BootstrapMethod`方法的附加参数。

某种意义上也就是说，这三项信息是`invokedynamic`方法的固定参数。

---

## 在ASM中使用`invokedynamic`指令

### Core API

可以由`visitInvokeDynamicInsn()`方法获取或创建`invokedynamic`指令，其定义如下：

````java
public void visitInvokeDynamicInsn(String name, String descriptor, 
		Handle bootstrapMethodHandle, Object... bootstrapMethodArguments)
````

- `name`：该`invokedynmaic`指令的名称，只是传入`BootstrapMethod`一个常量，可以按需要（随便）设定；

- `descriptor`：描述`invokedynmaic`指令行为方法一个方法描述符，应与`BootstrapMethod`返回的`CallSite`实际相应的方法签名相符；

- `bootstrapMethodHandle`：一个`Handle`实例，提供的信息与`MethodHandle`相似，指定了`BootstrapMethod`具体实现的位置；

- `bootstrapMethodArguments`：传入`BootstrapMethod`的附加参数，可以为`Integer`、`Float`、`Long`、`Double`、`String`、`org.objectweb.asm.Type`和`org.objectweb.asm.Handle`几种类型。真正传入`BootstrapMethod`时基本类型的封装类会被拆箱为基本类型，而ASM提供的`Type`与`Handle`类分别会被转换为包含同样信息的`MethodType`与`MethodHandle`实例。Java 11和ASM 7.0之后也可以传入`org.objectweb.asm.ConstantDynamic`来指定一个在运行时动态获取的常量，

  其中`Handle`类是ASM提供的用于记录`MethodHandle`实例属性的一个类，可以通过以下构造器获取：

````java
public Handle(int tag, String owner, String name, String descriptor, 
              boolean isInterface)
````

- `tag`：用于描述该`Handle`类型的一个数字，决定了其对应的`MethodHandle`的行为，可以将ASM库中`Opcodes`接口中名为的`H_XXX`字段（如`Opcodes.H_GETFIELD`）传入，在对JVM有所了解的前提下从名称分析其含义还是比较简单的。
- `owner`：包含目标成员的类的内部名称。
- `name`：目标成员的名称。
- `descriptor`：描述该`invokedynamic`指令行为的方法描述符。
- `isInterface`：包含目标成员的类是否是接口。

### Tree API

Tree API中的`InvokeDynamicInsnNode`对应一个`invokedynamic`指令，使用方法与Core API相似，此处不再赘述。

---

## `invokedynamic`指令的应用

在Java语言中`invokedynamic`指令两个最常见个用途是实现Lambda表达式与方法引用，具体的实现方式超出了本文的范围，本文中不再详述。

此处我们真正要探讨的是`invokedynamic`这个指令自身的用法。
举个例子，假设一个应用程序需要从一个配置文件中获取真正的`Main`类，那么这个应用的入口类可以用反射这样实现:

````java
public Class EntryPoint {
    public static void main(String[] args) throws Throwable ​{
        String main = getMainFromConfig(2023);
        Class.forName(main)
                .getMethod("main", String[].class)
                .invoke(null, args);
    }

    private static String getMainFromConfig(int addr) {
        // ...
    }
}
````

如果不使用反射呢？我们也可以生成一个使用`invokedynamic`的入口类！
可以使用以下代码生成`main()`方法的字节码：

````java
Handle bsmH = new Handle(Opcodes.H_INVOKESTATIC, 
		"EntryPoint", "bootstrap", 
		"(Ljava/lang/invoke/MethodHandles$Lookup;Ljava/lang/String;Ljava/lang/invoke/MethodType;)Ljava/lang/invoke/CallSite;I");
mv.visitInvokeDynamicInsn("inDy_boot", 
		"([Ljava/lang/String;)V", 
		bsmH, 
		2023);
mv.visitInsn(Opcodes.RETURN);
````

这时，可以这样实现`BootstrapMethod`：

````java
private static CallSite bootstrap(Lookup l, String name, MethodType type, int line) throws Throwable {
    String mainCl = getMainFromConfig(line):
    MethodHandle mh = l.findStatic(Class.forName(mainCl), 
            "main", 
            MethodType.methodType(void.class, String[].class);
    return new ConstantCallSite(mh);
}
````

或许这个例子有些牵强，但这确实在一个简单的情景下为我们展示了`invokedynamic`指令的基本用法。

另一个比较接近实际的例子是自己在上个月做的AccessingPath编译器中实现的使用字节码访问私有成员的功能。因为直接使用反射的性能较低，那里使用了`invokedynamic`来访问私有字段与方法。具体实现可以在[链接](https://github.com/lovexyn0827/MessMod/tree/master/src/main/java/lovexyn0827/mess/util/access)中`CompiledPath`与`BytecodeHelper.addInvoker()`下找到。
