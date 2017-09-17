# 数字类型

在`JSON Schema`中有两种数字类型：`integer`和`number`。

## integer

`integer`类型用来校验整数。

```json
{ "type": "integer" }       // a schema
```

```json
42          // success
```

```json
-12         // success
```

```json
3.1415      // failure
```

```json
"42"        // failure
```

## number

`number`类型能用于任何数字，包括整数以及浮点数。

```json
{ "type": "number" }        // a schema
```

```json
42          // success
```

```json
-12         // success
```

```json
3.1415      // success
```

```json
"42"        // failure
```

## Multiples

可以使用`multipleOf`关键字将数字限制为给定数字的倍数。它可以设置为任何正数。

```json
// a schema
{
    "type": "number",
    "multipleOf": 10
}
```

```json
0           // success
```

```json
10          // success
```

```json
30          // success
```

```json
23          // failure，不是10的倍数
```

## Range

可以使用以下关键字限制数字的范围：

* **minimum**: 最小值。
* **exclusiveMinimum**: 是一个boolean值，当值为true时，表示数字必须大于最小值，`x > min`。
    当值为false（或者没有该属性）时，数字可以等于最小值，`x >= min`。
* **maximum**: 最大值。
* **exclusiveMaximum**: 是一个boolean值，当值为true时，表示数字必须小于最大值，`x < max`。
    当值为false（或者没有该属性）时，数字可以等于最大值，`x <= max`。

```json
// a schema，值应该是 0 <= x < 100
{
  "type": "number",
  "minimum": 0,
  "maximum": 100,
  "exclusiveMaximum": true
}
```

```json
-1          // failure，值小于0
```

```json
0           // success
```

```json
1           // success
```

```json
10          // success
```

```json
99          // success
```

```json
100         // failure，值必须小于100
```

```json
101         // failure，值必须小于100
```
