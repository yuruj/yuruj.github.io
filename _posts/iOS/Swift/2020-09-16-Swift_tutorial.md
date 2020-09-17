---
layout: post
title: "Swift tutorial"
author: "yuruj"
catelog: true
header-style: text
tags:
  - Swift
  - iOS
  - 学习笔记
---

# Swift

## Swift闭包

闭包是自包含的功能代码块，可以在代码中使用或者用来作为参数传值

闭包的形式：

1、全局函数：有名字但不能捕获任何的值

2、嵌套函数：有名字，也能捕获封闭函数内的值

3、闭包表达式：无名闭包，使用轻量级语法，可以根据上下文环境捕获值

Swift的几点优化：

1、根据上下文推断参数和返回值类型

2、从单行表达式闭包中隐式返回

3、可以使用简化参数名，如$0，$1

4、提供了尾随闭包语法

```swift
{(parameters) -> return type in
	statements
}
```

Swift的String类型定义了关于>的字符串实现，其作为一个函数接受两个String类型的参数并返回Bool类型的值。而这正好与sort(_:)方法的第二个参数需要的函数类型相符合

### 尾随闭包

尾随闭包是一个书写在函数括号之后的闭包表达式，函数支持将其作为最后一个参数调用

```swift
func someFunctionThatTakesAClosure(closure: () -> Void){
  //函数部分
}

someFunctionThatTakesAClouse({
  //闭包主体部分
})

someFuncionThatTakesAClouse(){
  //闭包主体部分
}
```

如果函数只需要闭包表达式一个参数，当您使用尾随闭包时，您甚至可以把()省略掉

### 捕获值

闭包可以在其定义的上下文捕获常量或变量

即使定义这些变量和常量的原域已经不存在了，闭包仍然可以在闭包函数体内引用和修改这些值

嵌套函数可以捕获其外部函数所有的参数以及定义的常量和变量

### 闭包是引用类型

## Swift结构体

与C和Objective C不同的是：

* 结构体不需要包含实现文件和接口
* 结构体允许我们创建一个单一文件，且系统会自动生成面向其他代码的外部接口

### 结构体是值类型

结构体实例化

## Swift类

与其他编程语言所不同的是，Swift并不要求你为自定义类去创建独立的接口和实现文件。你所要做的是在一个单一的文件中定义一个类，系统会自动生成面向其他代码的外部接口

与结构体相比，类的附加功能：

* 继承允许一个类继承另一个类的特征
* 类型转换允许在运行时检查和解释一个类实例的类型
* 结构起允许一个类实例释放其任何所被分配的资源
* 引用计数允许对一个类的多次饮用

类实例化

因为类是引用类型，有可能有多个常量和变量在后台同时引用某一个类实例

为了能够判断两个常量或者变量是否引用同一个类实例，Swift内建了恒等运算符===、!==

## Swift属性

属性可分为存储属性和计算属性

存储属性：存储常量或变量作为实例的一部分，用于类和结构体

计算属性：计算（而不是）存储一个值，用于类、结构体和枚举

### 存储属性

* 可以在定义存储属性的时候制定默认值
* 也可以在构造过程中设置或修改存储属性的值，甚至修改常量存储属性的值

### 延迟存储属性

当第一次被调用时才会计算其初始值的属性

关键字lazy

必须将延迟存储属性声明成变量（使用var关键字），因为属性的值在实例构造完成之前可能无法得到。而常量属性在构造过程完成之前必须要有初始值，因此无法声明成延迟属性

延迟存储属性一般用于：

* 延迟对象的创建
* 当属性的值依赖于其他未知类

```swift
import Cocoa

class sample {
  lazy var no = number()
}

class number {
  var name = "xixi"
}

var firstsample = sample()
print(firtsample.no.name)
```

### 实例化变量

如果您有过 Objective-C 经验，应该知道Objective-C 为类实例存储值和引用提供两种方法。对于属性来说，也可以使用实例变量作为属性值的后端存储

Swift 编程语言中把这些理论统一用属性来实现。Swift 中的属性没有对应的实例变量，属性的后端存储也无法直接访问。这就避免了不同场景下访问方式的困扰，同时也将属性的定义简化成一个语句。一个类型中属性的全部信息——包括命名、类型和内存管理特征——都在唯一一个地方（类型定义中）定义

### 计算属性

计算属性不直接存储值，而是通过一个getter来获取值，一个可选的setter来间接设置其他属性或变量的值

如果计算属性的setter没有定义新值的参数名，则可以使用默认名称newValue

```swift
import Cocoa

class sample {
    var no1 = 0.0, no2 = 0.0
    var length = 300.0, breadth = 150.0
    
    var middle: (Double, Double) {
        get{
            return (length / 2, breadth / 2)
        }
        set(axis){
            no1 = axis.0 - (length / 2)
            no2 = axis.1 - (breadth / 2)
        }
    }
}

var result = sample()
print(result.middle) //(150.0, 75.0)
result.middle = (0.0, 10.0)

print(result.no1) //-150.0
print(result.no2) //-65.0
```

### 只读计算属性

只有getter没有setter的属性就是只读属性

只读属性总是返回一个值，可以通过点运算符访问，不能设置新的值

```swift
import Cocoa

class film {
    var head = ""
    var duration = 0.0
    var metaInfo: [String:String] {
        return [
            "head": self.head,
            "duration":"\(self.duration)"
        ]
    }
}

var movie = film()
movie.head = "Swift 属性"
movie.duration = 3.09

print(movie.metaInfo["head"]!)
print(movie.metaInfo["duration"]!)
```

必须使用var关键字定义计算属性，包括只读属性，因为他们的值不是固定的

### 属性观察器

属性观察器监控和响应属性的值的变化，每次属性被设置值的时候都会调用属性观察器，甚至新的值和现在的值相同的时候也不例外

可以为除了延迟存储属性之外的其他存储属性添加属性观察器，也可以通过属性重载的方式为继承的属性（包括存储属性和计算属性）添加属性观察期

不需要为无法重载的计算属性添加属性观察器，因为可以通过setter直接监控和响应值的变化

可以为属性添加如下的一个或全部观察器：

* willSet在设置新的值之前调用
* didSet在新的值被设置之后调用
* willSet和didSet观察器在属性初始化过程中不会被调用

```swift
import Cocoa

class Samplepgm {
    var counter: Int = 0{
        willSet(newTotal){
            print("计数器: \(newTotal)")
        }
        didSet{
            if counter > oldValue {
                print("新增数 \(counter - oldValue)")
            }
        }
    }
}
let NewCounter = Samplepgm()
NewCounter.counter = 100
NewCounter.counter = 800
```

### 全局变量和局部变量

计算属性和属性观察器所描述的模式也可以用于全局变量和局部变量

### 类型属性

类型属性是作为类型定义的一部分写在类型最外层的花括号内

使用关键字static来定义值类型的类型属性，关键字class来为类定义类型属性

```swift
struct Structname {
  static var storedTypeProperty = ""
  static var computedTypeProperty: Int {
    //这里返回一个Int值
  }
}

enum Enumname {
  static var storedTypeProperty = ""
  static var computedTypeProperty: Int {
    //这里返回一个Int值
  }
}

class Classname {
  class var computedTypeProperty: Int {
    //这里返回一个Int值
  }
}
```

例子中的计算型类型属性是只读的，但也可以定义可读可写的计算型类型属性，跟实例计算属性的语法类似

### 获取和设置类型属性的值

类似于实例的属性，类型属性的访问也是通过点运算符来进行。但是，类型属性是通过类型本身来获取和设置，而不是通过实例

```swift
import Cocoa

struct StudMarks {
  static let markCount = 97
  static var totalCount = 0
  var InternalMarks: Int = 0 {
    didSet {
      if InternalMarks > StudMarks.markCount {
        InternalMarks = StudMarks.markCount
      }
      if InternalMarks > StudMarks.totalCount {
        StudMarks.totalCount = InternalMarks
      }
    }
  }
}

var stud1Mark1 = StudMarks()
var stud1Mark2 = StudMarks()

stud1Mark1.InternalMarks = 98
print(stud1Mark1.InternalMarks) //97

stud1Mark2.InternalMarks = 87
print(stud1Mark2.InternalMarks) //87
```

## Swift方法

在OC中，类是唯一能定义方法的类型。但在Swift中，你不仅能选择是否要定义一个类/结构体/枚举，还能灵活的在你创建的类型上定义方法

### 实例方法

在Swift语言中，实例方法是属于某个特定类、结构体或者枚举类型实例的方法

* 可以访问和修改实例属性
* 提供与实例目的相关的功能

实例方法要写在它所属的类型的前后大括号之间

实例方法能够隐式访问它所属类型的所有其他实例方法和属性

实例方法只能被他所属的类的某个特定的实例所调用

实例方法不能脱离于现存的实例而被调用

```swift
func funcname(Parameters) -> returntype
{
  Statement1
  Statement2
  ......
  StatementN
  return parameters
}
```

### 方法的局部参数名称和外部参数名称

Swift默认仅给方法的第一个参数名称一个局部参数名称，默认同时给第二个和后续的参数名称为全局参数名称

### self属性

类型的每一个实例都有一个隐含属性叫做self，self完全等同于该实例本身

你可以在一个实例的实例方法中使用这个隐含的self属性来引用当前实例

### 在实例方法中修改值类型

Swift语言中结构体和枚举是值类型。一般情况下，值类型的属性不能在他的实例方法中被修改

但是，如果你确定需要在某个具体的方法中修改结构体或者枚举的属性，你可以选择变异mutating这个方法，然后方法就可以从方法内部改变他的属性，并且他做的任何改变在方法结束时还会保留在原始结构中

方法还可以给他隐含的self属性赋值一个全新的实例，这个新实例在方法结束后将替换原来的实例

```swift
import Cocoa

struct area {
    var length = 1
    var breadth = 1
    
    func area() -> Int {
        return length * breadth
    }
    
    mutating func scaleBy(res: Int) {
        length *= res
        breadth *= res
        
        print(length)
        print(breadth)
    }
}

var val = area(length: 3, breadth: 5)
val.scaleBy(res: 3)
val.scaleBy(res: 30)
val.scaleBy(res: 300)
```

### 在可变方法中给self赋值

可变方法能够赋给隐含属性self一个全新的实例

```swift
import Cocoa

struct area {
    var length = 1
    var breadth = 1
    
    func area() -> Int {
        return length * breadth
    }
    
    mutating func scaleBy(res: Int) {
        self.length *= res
        self.breadth *= res
        print(length)
        print(breadth)
    }
}
var val = area(length: 3, breadth: 5)
val.scaleBy(res: 13)

39
65
```

### 类型方法

生命结构体和枚举的类型方法，在方法的func关键字之前加上关键字static。类可能会用关键字class来允许子类重写父类的实现方法

类型方法和实例方法一样用点语法调用

```swift
import Cocoa

class Math
{
    class func abs(number: Int) -> Int
    {
        if number < 0
        {
            return (-number)
        }
        else
        {
            return number
        }
    }
}

struct absno
{
    static func abs(number: Int) -> Int
    {
        if number < 0
        {
            return (-number)
        }
        else
        {
            return number
        }
    }
}

let no = Math.abs(number: -35)
let num = absno.abs(number: -5)

print(no)
print(num)

35
5
```

## Swift下标脚本

## Swift继承

## Swfit可选链

## Swfit自动引用计数

## Swfit类型转换

## Swift访问控制

## Swift扩展

扩展就是向一个已有的类、结构体或枚举类型添加新功能

扩展可以对一个类型添加新的功能，但是不能重写已有的功能

Swift中的扩展可以：

* 添加计算型属性和计算型静态属性
* 定义实例方法和类型方法
* 提供新的构造器
* 定义下标
* 定义和使用新的嵌套类型
* 使一个已有类型符合某个协议

```swift
extension SomeType {
  //加到SomeType的新功能写到这里
}

extension SomeType: SomeProtocol, AnotherProtocol {
  //协议实现写到这里
}
```

### 计算型属性

扩展可以向已有类型添加计算型实例属性和计算型类型属性

```swift
extension Int {
   var add: Int {return self + 100 }
   var sub: Int { return self - 10 }
   var mul: Int { return self * 10 }
   var div: Int { return self / 5 }
}
    
let addition = 3.add
print("加法运算后的值：\(addition)")
    
let subtraction = 120.sub
print("减法运算后的值：\(subtraction)")
    
let multiplication = 39.mul
print("乘法运算后的值：\(multiplication)")
    
let division = 55.div
print("除法运算后的值: \(division)")

let mix = 30.add + 34.sub
print("混合运算结果：\(mix)")
```

### 构造器

这可以让你扩展其他类型，将你自己的定制类型作为构造器参数，或者提供该类型的原始实现中没有包含的额外初始化选项

### 方法

拓展可以向已有类型添加新的实例方法和类型方法

```swift
extension Int {
   func topics(summation: () -> ()) {
      for _ in 0..<self {
         summation() 
      }
   }
}  

4.topics({
   print("扩展模块内")       
})    
    
3.topics({
   print("内型转换模块内")       
})  
```

### 可变实例方法

通过拓展添加的实例方法也可以修改该实例本身

结构体和枚举类型中修改self或其属性的方法必须将该实例方法标注为mutating，正如来自原始实现的修改方法一样

```swift
extension Double {
  mutating func square() {
    let pi = 3.1415
    self = pi * self * self
  }
}

var trial = 3.3
trial.square()
print(trial)
```

### 下标

扩展可以向一个已有类型添加新下标

## Swift协议

协议规定了用来实现某一特定功能所必需的方法和属性

任意能够满足协议要求的类型被称为遵循这个协议

类、结构体或枚举类型都可以遵循协议，并提供具体实现方法来完成协议定义的方法和功能

```swift
protocol SomeProtocol {
  //协议内容
}

struct SomeStructure: FirstProtocol, AnotherProtocol {
  //结构体内容
}

class SomeClass: SomeSuperClass, FirstProtocol, AnotherProtocol {
  //类的内容
}
```

如果类在遵循协议的同时拥有父类，应该将父类名放在协议名之前，以逗号分隔

### 对属性的规定

协议用于指定的实例类型或类属性，而不用指定是存储类型或计算型属性。此外还必须指明是只读的还是可读可写的

协议中的通常用var来声明变量属性，在类型声明后加上{set get}来表示属性是可读可写的，只读属性则用{get}来表示

```swift
protocol classa {
    
    var marks: Int { get set }
    var result: Bool { get }
    
    func attendance() -> String
    func markssecured() -> String
    
}

protocol classb: classa {
    
    var present: Bool { get set }
    var subject: String { get set }
    var stname: String { get set }
    
}

class classc: classb {
    var marks = 96
    let result = true
    var present = false
    var subject = "Swift 协议"
    var stname = "Protocols"
    
    func attendance() -> String {
        return "The \(stname) has secured 99% attendance"
    }
    
    func markssecured() -> String {
        return "\(stname) has scored \(marks)"
    }
}
```

### 对Mutating方法的规定

```swift
protocol daysofaweek {
    mutating func show()
}

enum days: daysofaweek {
    case sun, mon, tue, wed, thurs, fri, sat
    mutating func show() {
        switch self {
        case .sun:
            self = .sun
            print("Sunday")
        case .mon:
            self = .mon
            print("Monday")
        case .tue:
            self = .tue
            print("Tuesday")
        case .wed:
            self = .wed
            print("Wednesday")
        case .thurs:
            self = .thurs
            print("Wednesday")
        case .fri:
            self = .fri
            print("Wednesday")
        case .sat:
            self = .sat
            print("Saturday")
        default:
            print("NO Such Day")
        }
    }
}

var res = days.wed
res.show()
```

### 对构造器的规定

协议可以要求他的遵循者实现指定的构造器

```swift
protocol SomeProtocol {
   init(someParameter: Int)
}
```

### 协议构造器规定在类中的实现

```swift
class SomeClass: SomeProtocol {
   required init(someParameter: Int) {
      // 构造器实现
   }
}

protocol tcpprotocol {
   init(aprot: Int)
}

class tcpClass: tcpprotocol {
   required init(aprot: Int) {
   }
}
```

使用required修饰符可以保证：所有的遵循该协议的子类，同样能为构造器规定提供一个显式的实现或继承实现

```swift
protocol tcpprotocol {
    init(no1: Int)
}

class mainClass {
    var no1: Int // 局部变量
    init(no1: Int) {
        self.no1 = no1 // 初始化
    }
}

class subClass: mainClass, tcpprotocol {
    var no2: Int
    init(no1: Int, no2 : Int) {
        self.no2 = no2
        super.init(no1:no1)
    }
    // 因为遵循协议，需要加上"required"; 因为继承自父类，需要加上"override"
    required override convenience init(no1: Int)  {
        self.init(no1:no1, no2:0)
    }
}
let res = mainClass(no1: 20)
let show = subClass(no1: 30, no2: 50)

print("res is: \(res.no1)")
print("res is: \(show.no1)")
print("res is: \(show.no2)")
```

### 协议类型

尽管协议本身不实现任何功能，但是协议可以被当作类型来使用

协议可以像其他普通类型一样。使用场景：

* 作为函数、方法或构造器中的参数类型或返回值类型
* 作为常量、变量或属性的类型
* 作为数组、字典或其他容器中的元素类型

### 在拓展中添加协议成员

### 协议的继承

协议的继承语法与类的继承相似，多个被继承的协议间用逗号分隔

### 类专属协议

通过添加class关键字，限制协议只能适配到类类型

class关键字必须是第一个

```swift
protocol SomeClassOnlyProtocol: class, SomeInheritedProtocol {
  //协议定义
}
```

### 协议合成

Swift支持合成多个协议，这在我们需要同时遵循多个协议时非常有用

### 检验协议的一致性

使用is和as操作符来检查是否遵循某一协议或强制转化为某一类型

## Swift泛型

Swift提供了泛型让你写出灵活且可重用的函数和类型

Swift标准库是通过泛型代码构建出来的

Swift的数组和字典类型都是泛型集

功能代码是相同的，只是类型上不一样，这是我们可以使用泛型，从而避免重复编写代码

泛型使用了占位类型名（在这里用字母T来表示）来代替实际类型名

```swift
func swapTwoStrings(_ a: inout String, _ b: inout String) {
    let temporaryA = a
    a = b
    b = temporaryA
}
 
func swapTwoDoubles(_ a: inout Double, _ b: inout Double) {
    let temporaryA = a
    a = b
    b = temporaryA
}

// 定义一个交换两个变量的函数
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
 
var numb1 = 100
var numb2 = 200
 
print("交换前数据:  \(numb1) 和 \(numb2)")
swapTwoValues(&numb1, &numb2)
print("交换后数据: \(numb1) 和 \(numb2)")
 
var str1 = "A"
var str2 = "B"
 
print("交换前数据:  \(str1) 和 \(str2)")
swapTwoValues(&str1, &str2)
print("交换后数据: \(str1) 和 \(str2)")
```

swapTwoValues后面跟着占位类型名，并用尖括号括起来。这个尖括号告诉Swift那个T是swapTwoValues()函数定义内的一个占位类型名，因此Swift不会去查找名为T的实际类型

### 泛型类型

Swift允许你定义你自己的泛型类型

自定义类、结构体和枚举作用于任何类型，如同Array和Dictionary的用法

```swift
// Int型的栈
struct IntStack {
  var items = [Int]()
  mutating func push(_ item: Int) {
    items.append(item)
  }
  mutating func pop() -> Int {
    return items.removeLast()
  }
}

// 泛型的栈
struct Stack<Element> {
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}

var stackOfStrings = Stack<String>()
stackOfStrings.push("google")
```

### 拓展泛型类型

```swift
struct Stack<Element> {
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
 
extension Stack {
    var topItem: Element? {
       return items.isEmpty ? nil : items[items.count - 1]
    }
}
 
var stackOfStrings = Stack<String>()
print("字符串元素入栈: ")
stackOfStrings.push("google")
stackOfStrings.push("runoob")
 
if let topItem = stackOfStrings.topItem {
    print("栈中的顶部元素是：\(topItem).")
}
 
print(stackOfStrings.items)
```

```swift
extension Array: Container {}
```

### 类型约束

类型约束制定了一个必须继承自指定类的类型参数名或者遵循一个特定的协议或协议构成

```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
  //这里是泛型函数的函数体部分
}
```

```swift
// 非泛型函数，查找指定字符串在数组中的索引
func findIndex(ofString valueToFind: String, in array: [String]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            // 找到返回索引值
            return index
        }
    }
    return nil
}
 
 
let strings = ["google", "weibo", "taobao", "runoob", "facebook"]
if let foundIndex = findIndex(ofString: "runoob", in: strings) {
    print("runoob 的索引为 \(foundIndex)")
}
```
