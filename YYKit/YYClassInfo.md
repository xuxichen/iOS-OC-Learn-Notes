YYClassIvarInfo
=======

YYClassInfo类是YYModel的一个工具类。里面有继承自NSObject的四个子类。分别是
* YYClassInfo
* YYClassIvarInfo
* YYClassMethodInfo
* YYClassPropertyInfo

我们可以通过类名大概知道这四个类的作用；

Objective-C运行时定义了几种重要的类型。

** 我们在这个类的.h文件中我们能看到这些类型都是用assign修饰的，我们点进这些类型进去看就能明白为什么了，因为它们的实质都是结构体.所以用assign修饰 **
* `Class`：定义Objective-C类。
* `Ivar`：定义对象的实例变量，包括类型和名字。
* `Protocol`：定义正式协议。
* `Method`：定义对象方法或类方法。这个类型提供了方法的名字（就是**选择器**）、参数数量和类型，以及返回值（这些信息合起来称为方法的**签名**），还有一个指向代码的函数指针（也就是方法的**实现**）。
* `SEL`：定义选择器。选择器是方法名的唯一标识符。
* `IMP`：定义方法实现。这只是一个指向某个函数的指针，该函数接受一个对象、一个选择器和一个可变长参数列表（varargs），返回一个对象

首先看下`YYClassIvarInfo` 这个类
这个类中有一个不常见的属性：**ptrdiff_t offset**
* `ptrdiff_t`是C/C++标准库中定义的一个与机器相关的数据类型。ptrdiff_t类型变量通常用来保存两个指针减法操作的结果。ptrdiff_t定义在stddef.h（cstddef）这个文件内。ptrdiff_t通常被定义为long int类型。
ptrdiff_t定义在C99标准中。
`ptrdiff_t`
标准库类型(library type)ptrdiff_t 与 size_t 类型一样,ptrdiff_t 也是一种与机器相关的类型,在 cstddef 头文件中定义。size_t 是unsigned 类型,而 ptrdiff_t 则是 signed 整型[1]。  
`size_t`
这两种类型的差别体现了它们各自的用途：size_t 类型用于指明数组长度,它必须是一个正数;ptrdiff_t 类型则应保证足以存放同一数组中两个指针之间的差距,它有可能是负数[1]  。  
目前我猜测这个属性的作用，类似与引用计数吧。  

* 一个初始化方法：`- (instancetype)initWithIvar:(Ivar)ivar;`我们可以看下它在这个方法中做了什么操作：
