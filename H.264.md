#### SPS
Sequence Parameter Set.SPS信息在整个视频编码序列中是不变的

#### PPS
Picture Parameter Set.PPS信息在一幅编码图像之内是不变的.


#### 闭包表达式
```
{
  (parameters) -> return type in
    statements
}
reversedNames = names.sorted(by: { (s1:String, s2:String) -> Bool in
  return s1 > s2
})
```

### Swift 字符串
#### 值类型
+ 字符串是值类型, 没一次复制和传递, 现存的 String 值都会被复制一次.

#### 字符串插值
```
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier)*2.5)"
```
#### 字符串和字符相等性
字符串和字符相等使用那个运算符( ==  != )



#### 操作
```
for character in "Dog!".characters {
  print(character)
}

var emptyString = ""
if emptyString.isEmpty {
    print("empty string")
}

let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
```

### Swift 函数
####函数的形式形式参数
#####无形式参数的函数
```
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())
```
##### 多形式参数的函数
```
func greet(person: String, alreadyGreeted: Bool) -> String {
    if alreadyGreeted {
        return greetAgain(person: person)
    } else {
        return greet(person: person)
    }
}
print(greet(person: "Tim", alreadyGreeted: true))
```
##### 无返回值的函数
```
func greet(person: String) {
    print("Hello, \(person)!")
}
greet(person: "Dave")
```
##### 多返回值的函数
```
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

##### 函数实际参数标签和形式参数名

##### 函数类型
函数类型由形式参数类型,返回类型组成.


#### 闭包
##### 逃逸闭包?
##### 自动闭包

### 类和结构体
不像其他的程序语言，Swift不需要你为自定义类和结构体创建独立的接口和实现文件。在 Swift 中，你在一个文件中定义一个类或者结构体， 则系统将会自动生成面向其他代码的外部接口.


#### 结构体类型的成员初始化器
所有的结构体都有一个自动生成的成员初始化器，你可以使用它来初始化新结构体实例的成员属性.
```
let vga = Resolution(width: 640, height: 480)
```
与结构体不同，类实例不会接收默认的成员初始化器.
#### 结构体和枚举是值类型
类型是一种当它被指定到常量或者变量，或者被传递给函数时会被拷贝的类型.

实际上，Swift 中所有的基本类型——整数，浮点数，布尔量，字符串，数组和字典——都是值类型，并且都以结构体的形式在后台实现.

#### 类是引用类型
有时候找出两个常量或者变量是否引用自同一个类实例非常有用,为了允许这样，Swift提供了两个特点运算符：
+ 相同于( === )
+ 不相同于( !== )

#### 字符串，数组和字典的赋值与拷贝行为
Swift 的 String , Array 和 Dictionary类型是作为结构体来实现的，这意味着字符串，数组和字典在它们被赋值到一个新的常量或者变量，亦或者它们本身被传递到一个函数或方法中的时候，其实是传递了拷贝。

这种行为不同于基础库中的 NSString, NSArray和 NSDictionary，它们是作为类来实现的，而不是结构体。 NSString , NSArray 和 NSDictionary实例总是作为一个已存在实例的引用而不是拷贝来赋值和传递。


#### 属性
##### 常量结构体实例的存储属性
```
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}
let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
rangeOfFourItems.firstValue = 6
// this will report an error, even though firstValue is a variable property
```
结构体是值类型.当一个值类型的实例被标记为常量时，该实例的其他属性也均为常量.


##### 延迟存储属性
延迟存储属性的初始值在其第一次使用时才进行计算.你可以通过在其声明前标注 lazy 修饰语来表示一个延迟存储属性.

你必须把延迟存储属性声明为变量（使用 var 关键字），因为它的初始值可能在实例初始化完成之前无法取得.常量属性则必须在初始化完成之前有值，因此不能声明为延迟.

##### 存储属性与实例变量
Swift 属性没有与之相对应的实例变量，并且属性的后备存储不能被直接访问.

##### 类型属性

#### 方法
##### self 熟悉
每一个类的实例都隐含一个叫做 self的属性，它完完全全与实例本身相等.你可以使用 self属性来在当前实例当中调用它自身的方法.


### 可选链

### 类型检测
使用类型检查操作符 （ is ）来检查一个实例是否属于一个特定的子类.

由于向下类型转换能失败，类型转换操作符就有了两个不同形式。条件形式， as? ，返回了一个你将要向下类型转换的值的可选项. 失败返回 nil .

强制形式， as! ，则将向下类型转换和强制展开结合为一个步骤。

### 关键字
'convenience'

### Queues
+ Dispatch queues are thread-safe which means that you can access them from multiple threads simultaneously.
+ In Swift, any variable declared with the let keyword is considered a constant and is read-only and thread-safe. Declare the variable with the var keyword however, and it becomes mutable and not thread-safe unless the data type is designed to be so. The Swift collection types like Array and Dictionary are not thread-safe when declared mutable.
+

### Enums
Enums　can extend them, create custom initializer methods, provide namespaces and encapsulate related operations
