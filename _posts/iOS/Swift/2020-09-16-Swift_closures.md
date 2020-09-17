---
layout: post
title: "Swift closures"
author: "yuruj"
catelog: true
header-style: text
tags:
  - Swift
  - iOS
  - 学习笔记
---

# Swift

## Closures

闭包是独立的函数块，可以在代码中传递和使用。Swift中的闭包类似于C和Objective-C中的`block`以及其他编程语言中的`lambdas(匿名函数)`。闭包可以捕获和`存储`上下文中定义的任何常量和变量的引用。 全局函数和嵌套函数实际上是闭包的特例。闭包采用以下三种形式之一：

- 全局函数是具有名称但不捕获任何值的闭包。
- 嵌套函数是具有名称并且可以从其封闭函数中捕获值的闭包。
- Closure表达式是一种未命名的可以从周围的上下文中捕获值的闭包，用轻量级语法编写。

Swift的闭包表达式鼓励简洁，因此闭包具备：

- 从上下文中推断参数和返回值类型
- 单表达式闭包的隐式返回
- 简洁的参数名称
- 尾随闭包语法

### 闭包表达式

对于内联闭包表达式，参数和返回类型写在花括号内，而不是在花括号外。闭包的方法体的开头由`in`关键字引入。这个关键字表示闭包的参数和返回类型的定义已经完成，闭包的方法体即将开始

### 尾随闭包

如果需要将闭包表达式作为函数的最终参数传递给函数，并且闭包表达式很长，则可以将其写为尾随闭包。写法：尾随闭包写在函数调用的圆括号之后，即它是函数的最终参数。如果尾随闭包作为函数的最终参数，并且定义了相应的参数标签，在使用尾随闭包语法时，不能将闭包的参数标签写为函数调用的一部分。

```swift
//定义一个闭包表达式为函数最终参数的函数
func trailingClosures(parameter:String,block:(_:String)->Void) -> Void {
    block(parameter + " 期待下：trailingClosures")
}
//可以有非尾随闭包的调用形式
func blockFunction(_ paramter:String)->Void {
    print(paramter)
}
trailingClosures(parameter: "不是尾随闭包写法1", block: blockFunction)
trailingClosures(parameter: "不是尾随闭包写法2", block: {(parameter:String)->Void in print(parameter)})
trailingClosures(parameter: "不是尾随闭包写法3", block: {(parameter)in print(parameter)})//!< 参数类型和返回值可以根据函数类型得知，故可以省略
//尾随闭包写法的调用形式，block函数标签不能出现在圆括号内
trailingClosures(parameter: "尾随闭包的写法") { (parameter) in
 print(parameter)
}
```

若闭包表达式是函数的唯一参数，在调用该函数时，若采用尾随闭包的写法，则不需要再函数名称之后写一对圆括号`()`

### 值的捕获

闭包可以从定义它的周围上下文中捕获常量和变量。闭包可以在其方法体中引用并修改常量和变量的值，即使定义常量和变量的原始作用域不存在。 在Swift中，一个闭包可以捕获值的最简单形式就是嵌套函数。一个嵌套函数可以捕获任何它外围函数的参数也可以捕获定义在外围函数里的常量和变量。

```swift
//阐述闭包捕获值的函数方法。
func createIncrementer(forIncrese amount:Int) -> ()->Int {
    //定义嵌套函数外部的变量
    var total = 0
    //定义一个嵌套函数
    func increase()->Int {
        total += amount
        return total
    }
    //返回此嵌套函数
    return increase
}
let increaseByTen = createIncrementer(forIncrese: 10)//increaseByTen其实是内部的嵌套函数（闭包的一种），捕获了`createIncrementer`方法的参数`amount`与方法体中定义的`total`变量。
print(increaseByTen())//!< log:10
print(increaseByTen())//!< log:20
print(increaseByTen())//!< log:30 综上述`increaseByTen`函数捕获了捕获了`createIncrementer`方法的参数`amount`与方法体中定义的`total`变量，并在其内部持有了外部变量`total`和外部方法参数`amount`的副本。以至于`increaseByTen`可以每次调用都能基于`amount`的值，对变量`total`进行递增，并且返回结果。
let increaseBySix = createIncrementer(forIncrese: 6)
print(increaseBySix())//!< log:6
print(increaseBySix())//!< log:12
print(increaseBySix())//!< log:18 综上述：`increaseBySix`是调用了`createIncrementer`生成的一个`()->Int`类型的常量。在生成的过程中，内部的闭包（嵌套函数）`increase`重新捕获了外部变量`total`和外部方法参数`amount`，并返回此方法赋值给了`increaseBySix`，以至于`increaseBySix`和`increaseByTen`具备不同的递增系数。本质上这是两个不同的函数类型的常量。
```

上述示例中，`increaseByTen`其实是内部的嵌套函数（闭包的一种）`increase`。`increaseByTen`函数捕获了`createIncrementer`方法的参数`amount`与方法体中定义的`total`变量，并在其内部持有了`increaseByTen`函数捕获的值的副本。以至于`increaseByTen`可以每次调用都能基于`amount`的值，对变量`total`进行递增，并且返回结果。`increaseBySix`是调用了`createIncrementer`生成的另一个`()->Void`类型的常量。在生成的过程中，内部的闭包（嵌套函数）`increase`重新捕获了外部变量`total`和外部方法参数`amount`，并返回此方法赋值给了`increaseBySix`，以至于`increaseBySix`和`increaseByTen`具备不同的递增系数，并且分别进行多次调用。本质上这是两个不同的函数类型的常量。

如果值不会被闭包改变，并且闭包创建以后值也不会被改变。Swift可以代替闭包捕获和存储值的一个副本。Swift也会参与处理所有不再需要的变量的内存管理

### 闭包是引用类型

函数和闭包是引用类型。无论何时将函数或闭包赋值给常量或变量，实际上都是将该常量或变量设置为对函数或闭包的引用。意味着如果为两个不同的常量或变量分配同一个闭包，那么这两个常量或变量都将引用的是相同的闭包。

### 逃逸闭包?

闭包作为函数参数进行传递，但是该闭包并未在函数返回前调用，而是在函数返回后才被调用，则这个闭包被称为逃逸了。当我们声明一个以闭包作为参数之一的函数时，我们可以在该闭包参数的类型之前书写`@escaping`来表示该闭包允许逃逸。即：允许该闭包在函数结束后仍然可以被调用。 当一个函数需要用到异步操作回调的时候需要使用逃逸闭包。 实现闭包逃逸的一种途径是通过将该闭包存储到定义在函数外面的变量中，稍后再去调用

```swift
class escapeClosure: NSObject {
    //声明一个闭包类型的数组
    var closureArray : [(String)->Void] = []
    override init() {
        super.init()
        
    }
    //模仿闭包逃逸:写完 closureArray.append编译器检测到时逃逸闭包提示添加@escaping
    func escapeClosures(title:String,handle:@escaping (String)->Void){
        closureArray.append(handle)
    }
    //类方法
    static func startEscape(){
       let escapeObject = escapeClosure()
       escapeObject.escapeClosures(title: "场景1") { (s1) in
            print("场景1"+s1)//!< 场景1逃逸闭包1被调用了
        }
        escapeObject.escapeClosures(title: "场景2") { (s1) in
            print("场景2"+s1)//!< 场景2逃逸闭包2被调用了
        }
        //使用迭代器进行下标和元素的同时遍历
        for (index,obj) in  escapeObject.closureArray.enumerated() {
            obj("逃逸闭包\(index+1)被调用了")
        }
    }
}
//调用
escapeClosure.startEscape()//!< 场景1逃逸闭包1被调用了 场景2逃逸闭包2被调用了
```

### 自动闭包?
