---
layout: default
title: Swift
description: Study Notes
---

## Swift Logo
![Swift](https://developer.apple.com/swift/images/swift-logo.svg)

## Preparation
MacOS installed Xcode (the easiest way)
If you use other OS (Linux/Windows), refer to [this](https://swift.org/getting-started/).

## Playground
You can write down codes and see the results there.

## Grammar
It is better to have C++ or Java programming experience, so that you can quickly get started with Swift.

| Language Guide | Tour |
| :-: | :- |
| 1 | [The Basics](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html) |
| 2 | [Basic Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html) |
| 3 | [Strings and Characters](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html) |
| 4 | [Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html) |
| ... | ... |

**Swift**
```swift
func greetAgain(person: String) -> String {
    return "Hello again, " + person + "!"
}
print(greetAgain(person: "Anna"))
// Prints "Hello again, Anna!"
```
**C**
```C
/* function returning the max between two numbers */
int max(int num1, int num2) {

   /* local variable declaration */
   int result;
 
   if (num1 > num2)
      result = num1;
   else
      result = num2;
 
   return result; 
}
```

*extension.swift*
```swift
//: Playground - noun: a place where people can play

import UIKit

class Student{
    var name:String
    var id:Int
    var sex:String
    init() {
        name = "jack"
        id = 1001
        sex = "male"
    }
    init(name:String,id:Int,sex:String){
        self.name=name
        self.id=id
        self.sex=sex
    }
}
var student1=Student()
var student2=Student(name:"mike", id: 2001, sex: "male")

class Aclass{
    var num:Int
    init(num:Int) {
        self.num=num
    }
    convenience init(num:Int,str:String){
        if num>100{
            self.init(num: 100)
        }else{
            self.init(num: num)
        }
    }
}

protocol ExamProtocol{
    var simpleDescription:String{get}
    mutating func adjust()
}

class SimpleClass:ExamProtocol{
    var simpleDescription: String
    func adjust() {
        simpleDescription+=" 100% adjusted"
    }
    init(simpleDescription:String) {
        self.simpleDescription = simpleDescription
    }
}

struct SimpleStruct:ExamProtocol{
    var simpleDescription: String
    mutating func adjust() {
        simpleDescription+=" 100% adjusted"
    }
}

enum SimpleEnum:ExamProtocol{
    case off
    case low
    case high
    mutating func adjust() {
        switch self {
        case .high:
            self = .low
        case .low:
            self = .off
        default:
            self = .high
        }
    }
    var simpleDescription: String{
        switch self {
        case .off:
            return "off"
        case .high:
            return "high"
        case .low:
            return "low"
        }
    }
    init(){
        self = .high
    }
}
let state = SimpleEnum()

protocol BaseProtocol {
    var a:Int {get set}
    static func function1()
}
protocol SubProtocol:BaseProtocol {
    var b:String {get}
    func function2()
}
class MyClass:SubProtocol {
    var b:String
    var a:Int
    func function2() {
        print("From SubProtocol")
    }
    static func function1() {
        print("static function From BaseProtocol")
    }
    init(a:Int,b:String) {
        self.a = a
        self.b = b
    }
}
var myClass1:BaseProtocol = MyClass(a: 10, b: "abc")
myClass1.a = 100
var myClass2:SubProtocol = MyClass(a: 20, b: "def")
myClass2.function2()

protocol Test {
    var a:Int {get}
    var b:Int {get}
    func aa()
    static func bb()
}
protocol SubTest:Test {
    var c:Int {get}
    init(a:Int,b:Int,c:Int,d:Int,name:String)
}
class BaseClass {
    var name:String
    init(name:String) {
        self.name = name
    }
}
class SubClass:BaseClass,SubTest {
    var a:Int
    var b:Int
    var c:Int
    var d:Int
    required init(a:Int,b:Int,c:Int,d:Int,name:String) {
        self.a = a
        self.b = b
        self.c = c
        self.d = d
        super.init(name: name)
    }
    func aa() {
        print("aaa")
    }
    static func bb() {
        print("bbbb")
    }
}
protocol AAA {
    var name:String {get}
}
class BBB:AAA {
    var name:String
    init(name:String) {
        self.name = name
    }
}
class CCC:BBB {
    var id:Int
    init(name:String,id:Int) {
        self.id = id
        super.init(name: name)
    }
}
var ccc:AAA = CCC(name: "jack", id: 1001)
print(ccc.name)

extension Double {
    func abs()->Double {
        return self>=0 ? self : -self
    }
    var int:Int {
        get {
            return Int(self)
        }
    }
}

struct Size{
    var width:Int
    var length:Int
}
class Button{
    var name:String
    var size:Size
    var text:String
    func loadImage(imageName:String) {
        print("image \(imageName) has load")
    }
    init(name:String,size:Size,text:String) {
        self.name=name
        self.size=size
        self.text=text
    }
}
extension Button{
    convenience
    init(name:String,size:Size,text:String,imageName:String){
        self.init(name: name, size: size, text: text)
        loadImage(imageName: imageName)
    }
}

extension UInt{
    func power(n:UInt) -> UInt {
        var ret:UInt = 1
        for _ in 1...n{
            ret=ret*self
        }
        return ret
    }
}
var x:UInt = 5
print(x.power(n: 2))

extension Double{
    var km:Double{
        get{
            return self*1000.0
        }
    }
}
var y:Double = 10.0
print("\(y)km = \(y.km)m")

extension Int{
    func changeToChinessNum() -> String {
        var ret:String=""
        var tmp=self
        repeat{
            switch tmp%10 {
            case 0:
                ret="零"+ret
            case 1:
                ret="一"+ret
            case 2:
                ret="二"+ret
            case 3:
                ret="三"+ret
            case 4:
                ret="四"+ret
            case 5:
                ret="五"+ret
            case 6:
                ret="六"+ret
            case 7:
                ret="七"+ret
            case 8:
                ret="八"+ret
            default:
                ret="九"+ret
            }
            tmp/=10
        }while tmp>0
        return ret
    }
}
print("\(1234567890.changeToChinessNum())")

extension String{
    subscript(index:Int)->Character?{
        if index<0||index>=self.count{
            return nil
        }
        else{
            return self[self.index(self.startIndex, offsetBy:index)]
        }
    }
}
var str:String="asdfgh"
print("\(String(describing: str[4]))")
```

*generic.swift*
```swift
//: Playground - noun: a place where people can play

import Cocoa

func appendIntToArray(src:[Int], dest:inout [Int]) {
    for element in src {
        dest.append(element)
    }
}
func appendStringToArray(src:[String], dest:inout [String]) {
    for element in src {
        dest.append(element)
    }
}
// 泛型 T
func appendToArray<T>(src:[T], dest:inout [T]) {
    for element in src {
        dest.append(element)
    }
}
let srcInt = [5,2,1]
var destInt = [0,2,5]
appendToArray(src: srcInt, dest: &destInt)
print(destInt)
let srcString = ["I","Love","you"]
var destString = ["Do","wanna","be","my","girlfriend"]
appendToArray(src: srcString, dest: &destString)
print(destString)
let srcArray = [[1,1],[2,2],[3,3]]
var destArray = [[4,4],[5,5],[6,6]]
appendToArray(src: srcArray, dest: &destArray)
print(destArray)

// 泛型函数 泛型协议
func swapTwo<X>(one:inout X, two:inout X) {
    let temp = one
    one = two
    two = temp
}
var oneInt = 100, twoInt = 200
swapTwo(one: &oneInt, two: &twoInt)
print("Now one=\(oneInt), two=\(twoInt)")
// 泛型类型
class AAAA<S> {
    var id:S
    var name:String
    init(id:S, name:String) {
        self.id = id
        self.name = name
    }
}
var aaaa = AAAA<String>(id: "sn1001", name: "1号零件")
var bbbb = AAAA(id: 1001, name: "1001号零件")
// 泛型 栈
struct Stack<T> {
    var items = [T]()  // 空数组
    mutating func push(item: T) {
        items.append(item)
    }
    mutating func pop() -> T {
        return items.removeLast()
    }
}
var stackOne = Stack<String>()  // 创建一个栈
stackOne.push(item: "SingleDog")
stackOne.push(item: "AllTheDay")
print(stackOne.items.count)  // 栈内数据的个数
print("弹出数据\(stackOne.pop())")
var stackTwo = Stack<[Int]>()  // 栈内存放整型数组
stackTwo.push(item: [8,8])
stackTwo.push(item: [9,9])
// 泛型约束: 继承约束 条件约束
class Animal {
    func run() {
        print("Animal run")
    }
}
class Dog:Animal {
    override func run() {
        print("Dog run")
    }
}
class Cat:Animal {
    override func run() {
        print("Cat run")
    }
}
class Flower {
    func showColor() {
        print("A red Flower")
    }
}
func animalRun<T:Animal>(animal:T) {  // T这个类型必须继承自Animal类(也包括Animal)才可调用run方法
    animal.run()
}
animalRun(animal: Dog())
animalRun(animal: Cat())
animalRun(animal: Animal())
// animalRun(animal: Flower()) ERROR

// 协议约束 Equatable == !=
func findIndex<T:Equatable>(array:[T], valueToFind:T) -> Int? {
    var index = 0
    for value in array {
        if value==valueToFind {
            return index
        } else {
            index += 1
        }
    }
    return nil
}
var arrayString = ["🍎","Zoy","🦁","panda","♥️","pumpkin"]
if let index = findIndex(array: arrayString, valueToFind: "❤️") {
    print("Find it at index=\(index)")
}
var arrayInt = [5,4,3,2,1,-7,-2,0,9,99,3]
if let index = findIndex(array: arrayInt, valueToFind: 1) {
    print("Find it at index=\(index)")
} else {
    print("Not Fund in Array")
}

func getMax<T:Comparable>(array:inout [T]) -> T {
    var max = array[0]
    for i in array {
        if max<i {
            max = i
        }
    }
    return max
}
print("\(arrayInt)'s maximum is \(getMax(array: &arrayInt))")
print("\(arrayString)'s maximum is \(getMax(array: &arrayString))")
func arraySort<T:Comparable>(array:inout [T],flag:Bool) -> [T] {
    array.sort()
    if flag==false {
        array.reverse()
    }
    return array
}
var sortedDES = arraySort(array:&arrayInt,flag:true)
print(sortedDES)
var sortedAES = arraySort(array:&arrayString,flag:false)
print(sortedAES)

func printElements<T>(inputs:[T]){
    for element in inputs{
        print(element,terminator:"\n")
    }
}
printElements(inputs:arrayString)

//MARK:- 初始化注释说明
//TODO: balabala
//FIXME: next

```

(Last updated at 16:08 on May 21th UTC+8)

[back](../../)
