# 简介

`JSON Schema`是验证`JSON`数据结构的强大工具。
然而，通过阅读它的说明书来学习如何使用它，就像通过设计蓝图来学习驾驶汽车一样。
如果你想开箱即用，那么你不需要知道内燃机是如何组合在一起的。
因此，这本书的目的旨在帮助大家更好的学习`JSON Schema`。
它是为那些想写它，理解它，但并不想建设自己的汽车的人所写，只是写`JSON Schema`验证器。

## 从哪里开始

* 如果您不确定`Schema`是什么，请查看[什么是`Schema`][about]。
* [基础][basics]这一章旨在能帮助你更好的理解[`JSON Scheme`核心][reference]。
* 当您开始使用多个嵌套和重复的部分开发大型模式时，请学习如何[构建一个复杂的模式][structuring]

## 目录

* [什么是模式][about]
* [基础][basics]
* [JSON Schema手册][reference]
    - [Type定义][type]
        + [string][]
        + [numeric types][numeric]
        + [object][]
        + [array][]
        + [boolean][]
        + [null][]
    - [通用关键字][generic]
    - [组合模式][combining]
        + [allOf][]
        + [anyOf][]
        + [oneOf][]
        + [not][]
    - [$schema关键字][schema]
    - [正则表达式][regular_expressions]
* [构建一个复杂的模式][structuring]


[about]: about/about.md
[basics]: basics/basics.md
[reference]: reference/reference.md
[type]: reference/type.md
[string]: reference/string.md
[numeric]: reference/numeric.md
[object]: reference/object.md
[array]: reference/array.md
[boolean]: reference/boolean.md
[null]: reference/null.md
[generic]: reference/generic.md
[combining]: reference/combining.md
[allOf]: reference/allOf.md
[anyOf]: reference/anyOf.md
[oneOf]: reference/oneOf.md
[not]: reference/not.md
[schema]: reference/schema.md
[regular_expressions]: reference/regular_expressions.md
[structuring]: structuring/structuring.md
