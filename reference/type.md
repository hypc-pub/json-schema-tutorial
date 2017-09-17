# Type定义

Type关键字是`JSON Schema`的基础。它用来指定schema的数据格式。

* [string](string.md)
* [numeric types](numeric.md)
* [object](object.md)
* [array](array.md)
* [boolean](boolean.md)
* [null](null.md)

关键字type的值可以是string，也可以是array：

* 如果是string，那么值必须是以上基本类型；
* 如果是array，则值必须是string array，并且每个string都是一个基本类型，array中的值必须唯一不能重复。
    这种情况下，JSON代码段与任何给定的类型匹配，则认为该段代码是有效的。

这是一个简单的例子：

```json
{ "type": "number" }        // a schema
```

```json
42          // success
```

```json
42.1        // success
```

```json
"42"        // failure
```

这是一个以数组作为type的值的例子：

```json
{ "type": ["number", "string"] }        // a schema
```

```json
42          // success
```

```json
"This is a string."     // success
```

```json
["this", "is", "a", "array"]        // failure
```
