# 通用关键字

这一章列出了所有可以用于其他JSON类型的属性。

## Metadata

`JSON Schema`包含一个属性：`title`、`description`、`default`，它们不是用来校验数据，而是用来描述schema。

`title`和`description`必须是字符串。`title`可以用来做简要说明，
而`description`可以用来完整的说明json数据的意义。

`default`关键字用来指定默认值。一些`JSON Schema`处理工具可以根据这个来添加缺省的默认值，
当然，有些`JSON Schema`工具只是忽略`default`关键字。

```json
// a schema
{
    "title" : "Match anything",
    "description" : "This is a schema that matches anything.",
    "default" : "Default value"
}
```

## Enumerated values

`enum`关键字给定一组固定的值，而json数据的值只能在`enum`给定的范围内，当然`enum`值的每一项必须是唯一的。

```json
// a schema
{
    "type": "string",
    "enum": ["red", "amber", "green"]
}
```

```json
// success
"red"
```

```json
// failure
"blue"
```

当不使用`type`关键字的时候，`enum`可以使用不同的类型。

```json
// a schema
{
    "enum": ["red", "amber", "green", null, 42]
}
```

```json
// success
"red"
```

```json
// success
null
```

```json
// success
42
```

```json
// failure
12
```

当然，正常情况下，json数据的值必须匹配`enum`和`type`关键字的值。

```json
// a schema
{
    "type": "string",
    "enum": ["red", "amber", "green", null]
}
```

```json
// success
"red"
```

```json
// failure
null
```
