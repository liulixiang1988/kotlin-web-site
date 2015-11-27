---
type: doc
layout: reference
category: "基础"
title: "基本语法"
---

# 基本语法

## 定义包

报的定义应该在源码文件的顶部：

``` kotlin
package my.demo

import java.util.*

// ...
```

并不要求文件夹和包匹配：源文件可以放在文件系统的任何位置。

参见 [包](packages.html).

## 定义函数

有两个`Int`参数和一个`Int`返回类型的函数：

``` kotlin
fun sum(a: Int, b: Int): Int {
  return a + b
}
```

有表达式主体和推测返回类型的函数：

``` kotlin
fun sum(a: Int, b: Int) = a + b
```

返回无意义值得函数：

``` kotlin
fun printSum(a: Int, b: Int): Unit {
  print(a + b)
}
```

`Unit`返回类型可以省略:

``` kotlin
public fun printSum(a: Int, b: Int) {
  print(a + b)
}
```

参见 [函数](functions.html).

## 定义局部变量

单次赋值（只读）局部变量：

``` kotlin
val a: Int = 1
val b = 1   // `Int` 类型可以被推断出来
val c: Int  // 没有初始化时需要声明类型
c = 1       // 确定赋值
```

可变变量:

``` kotlin
var x = 5 // `Int` 类型可以被推断出来
x += 1
```

参见 [属性 和 字段](properties.html).

## 使用字符串模板

``` kotlin
fun main(args: Array<String>) {
  if (args.size == 0) return

  print("First argument: ${args[0]}")
}
```

参见 [String templates](basic-types.html#string-templates).

## 使用条件表达式

``` kotlin
fun max(a: Int, b: Int): Int {
  if (a > b)
    return a
  else
    return b
}
```

使用 *if*{: .keyword } 作为表达式

``` kotlin
fun max(a: Int, b: Int) = if (a > b) a else b
```

参见 [*if*{: .keyword }-表达式](control-flow.html#if-expression).

## 使用可空值，并且检查是否为*null*{: .keyword }

当引用可能为*null*{: .keyword }值时，需要显式标明是可空的。

如果`str`不包含整数，返回 *null*{: .keyword }：

``` kotlin
fun parseInt(str: String): Int? {
  // ...
}
```

使用返回可空值的函数：

``` kotlin
fun main(args: Array<String>) {
  if (args.size < 2) {
    print("Two integers expected")
    return
  }

  val x = parseInt(args[0])
  val y = parseInt(args[1])

  // 使用`x * y`可能会产生错误，应为它们可能含有空值
  if (x != null && y != null) {
    // null检查后，x和y自动会转换为非空类型
    print(x * y)
  }
}
```

或者

``` kotlin
  // ...
  if (x == null) {
    print("Wrong number format in '${args[0]}'")
    return
  }
  if (y == null) {
    print("Wrong number format in '${args[1]}'")
    return
  }

  // x和y在空检查后自动转换为非空类型
  print(x * y)
```

参见 [Null-安全](null-safety.html).

## 使用类型检查并且自动转换

*is*{: .keyword }操作符检查表达式是否是某一类型的实例。
如果对一个不可变局部变量或者属性检查是否是某一特定类型，就不需要显式的强制转换了:

``` kotlin
fun getStringLength(obj: Any): Int? {
  if (obj is String) {
    // `obj` 在这个分支自动转换为`String`
    return obj.length
  }

  // 在分支外，`obj`依旧是`Any`类型
  return null
}
```

或者

``` kotlin
fun getStringLength(obj: Any): Int? {
  if (obj !is String)
    return null

  // `obj`在这个分支自动转换为`String`
  return obj.length
}
```

or even

``` kotlin
fun getStringLength(obj: Any): Int? {
  // `obj`在`&&`右侧自动转换为`String`
  if (obj is String && obj.length > 0)
    return obj.length

  return null
}
```

参见 [类](classes.html) and [类型转换](typecasts.html).

## 使用 `for` 循环

``` kotlin
fun main(args: Array<String>) {
  for (arg in args)
    print(arg)
}
```

或者

``` kotlin
for (i in args.indices)
  print(args[i])
```

参见 [for 循环](control-flow.html#for-loops).

## 使用`while`循环

``` kotlin
fun main(args: Array<String>) {
  var i = 0
  while (i < args.size)
    print(args[i++])
}
```

参加 [while 循环](control-flow.html#while-loops).

## 使用 `when` 表达式

``` kotlin
fun cases(obj: Any) {
  when (obj) {
    1          -> print("One")
    "Hello"    -> print("Greeting")
    is Long    -> print("Long")
    !is String -> print("Not a string")
    else       -> print("Unknown")
  }
}
```

参见 [when 表达式](control-flow.html#when-expression).

## 使用 ranges

使用*in*{: .keyword }操作符，检查一个数是否在一个范围之内:

``` kotlin
if (x in 1..y-1)
  print("OK")
```

检查一个数是否在范围之外：

``` kotlin
if (x !in 0..array.lastIndex)
  print("Out")
```

遍历一个范围：

``` kotlin
for (x in 1..5)
  print(x)
```

参见 [Ranges](ranges.html).

## 使用集合

遍历一个集合：

``` kotlin
for (name in names)
  println(name)
```

使用*in*{: .keyword }操作符，检查一个集合是否含有某个对象：

``` kotlin
if (text in names) // names.contains(text) is called
  print("Yes")
```

使用函数字面量来过滤(filter)和映射(map)集合：

``` kotlin
names
    .filter { it.startsWith("A") }
    .sortedBy { it }
    .map { it.toUpperCase() }
    .forEach { print(it) }
```

参见 [高阶函数 和 Lambdas](lambdas.html).

