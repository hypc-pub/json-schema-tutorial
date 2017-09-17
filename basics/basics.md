# 基础

在[什么是`JSON Schema`][about]中，介绍了什么是`JSON Schema`，并且说明了为什么需要`JSON Schema`。
这一章我们继续学习怎么编写一个简单的`JSON Schema`。

## Hello World

学习一门新的语言，通常从简单的开始。学习`JSON Schema`亦是如此，一个空的对象可以用来校验任何`JSON`。

```json
{}
```

它能校验任何东西：

```json
42      // success
```

```json
"This is a string."     // success
```

```json
{ "a": "string", "b": ["first", 4] }        // success
```

## Type关键字

当然，大多数情况下，我们只允许我们定义好的类型通过校验，这时候需要用到`type`关键字。

如下，值允许string通过校验：

```json
{ "type": "string" }        // a schema
```

```json
"This is a string."     // success
```

```json
42          // failure
```

```json
{ "a": "string" }       // failure
```

更多的`type`定义详见[Type定义][type]。

## 声明`JSON Schema`

因为`JSON Schema`本身就是`JSON`，所以一个`JSON`数据并不能很好区分出来它是一个`JSON Schema`还是一个`JSON`数据。
`$schema`关键字用来声明当前数据到底是一个`JSON Schema`还是一个`JSON`，当然，它并不是必须的。

```json
{ "$schema": "http://json-schema.org/schema#" }
```

还可以使用此关键字来声明架构所写入的`JSON Schema`的规范属于哪个版本。
更多内容参见[$schema关键字][schema]。

## 声明一个唯一标识

当然，一般情况下会使用id属性为是为每一个`JSON Schema`添加一个唯一标识。
一般会使用你拥有的url作为唯一标识：

```json
{ "id": "http://yourdomain.com/schemas/myschema.json" }
```

从[构建一个复杂的模式][structuring]中，你可以学习有关[id][]属性的知识。


[about]: ../about/about.md
[type]: ../reference/type.md
[schema]: ../reference/schema.md
[structuring]: ../structuring/structuring.md
[id]: ../structuring/structuring.md#the-id-property
