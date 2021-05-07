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

[back](../../)
