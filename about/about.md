# 什么是Schema

如果你用过`XML Schema`、`RelaxNG`或者`ASN.1`，你可能也已经知道了什么是Schema，那么你可以跳过该章节。
在开始学习`JSON Schema`之前，你需要先学习`JSON`。

`JSON`（`JavaScript`对象标记），是一种轻量级的数据交换格式。它最开始应用于万维网。
现在由于`JavaScript`存在于大多数web浏览器中，并且`JSON`基于`JavaScript`，所以使用它变得非常容易。
然而，它足够简单并且可以应用到任何地方，而不仅仅是用web页面中。

`JSON`可以用来构建以下数据结构：

* 对象

    ```json
    { "key1": "value1", "key2": "value2" }
    ```

* 数组

    ```json
    [ "first", "second", "third" ]
    ```

* 数字

    ```json
    42
    3.141592653589793
    ```

* 字符串

    ```json
    "This is a string"
    ```

* 布尔值

    ```json
    true
    false
    ```

* null

    ```json
    null
    ```

这些类型在其他语言中也存在，以下是与其他语言的对比：

JavaScript  |Python     |Java               |Ruby
------------|-----------|-------------------|----------------------
string      |string     |String             |String
number      |int/float  |int/float/double   |Integer/Float
object      |dict       |Map                |Hash
array       |list/tuple |Array              |Array
boolean     |bool       |boolean            |TrueClass/FalseClass
null        |None       |null               |NilClass

使用这些简单的数据类型，可以表示各种结构化数据。
然而，这种巨大的灵活性带来了巨大的责任，因为同样的概念可以用无数的方式来表示。
例如，您可以使用不同的方式来表示一个人的信息：

```json
{
    "name": "George Washington",
    "birthday": "February 22, 1992",
    "address": "Mount Vernon, Virginia, United States"
}

{
    "first_name": "George",
    "last_name": "Washington",
    "birthday": "1992-02-22",
    "address": {
        "street_address": "3200 Mount Vernon Memorial Highway",
        "city": "Mount Vernon",
        "state": "Virginia",
        "country": "United States"
    }
}
```

这两种描述都是有效的，但明显能看出其中一种比另外一种更为正式。
数据格式的设计很大程度上取决于在应用程序中的用途，在这里没有正确或错误的答案。
但是，当需要交互时，知道数据是怎么组织的是很重要的一件事。这时候我们需要`JSON Schema`。

```json
{
    "type": "object",
    "properties": {
        "first_name": { "type": "string" },
        "last_name": { "type": "string" },
        "birthday": { "type": "string", "format": "date-time" },
        "address": {
            "type": "object",
            "properties": {
                "street_address": { "type": "string" },
                "city": { "type": "string" },
                "state": { "type": "string" },
                "country": { "type" : "string" }
            }
        }
    }
}
```

然后你会发现第一个数据校验失败，而第二个数据校验成功。
