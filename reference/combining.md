# 组合模式

`JSON Schema`允许将几个schema组合在一起使用。但是，注意，这并意味着可以将多个`JSON Schema`文件
或`JSON Schema`结构组合在一起使用。组合模式很简单，就像允许一个值同时对多个标准进行校验一样。

* [allOf](allOf.md)
* [anyOf](anyOf.md)
* [oneOf](oneOf.md)
* [not](not.md)

```json
// a schema
{
    "anyOf": [
        { "type": "string", "maxLength": 5 },
        { "type": "number", "minimum": 0 }
    ]
}
```

```json
// success
"short"
```

```json
// failure
"too long"
```

```json
// success
12
```

```json
// failure
-5
```
