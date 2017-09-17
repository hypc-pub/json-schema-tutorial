# oneOf

`oneOf`意思是，对于给定的多个schema，只能有一个有效。

```json
// a schema
{
    "oneOf": [
        { "type": "number", "multipleOf": 5 },
        { "type": "number", "multipleOf": 3 }
    ]
}
```

```json
// success
10
```

```json
// success
9
```

```json
// failure
15
```

上面schema也可以写成下面这样：

```json
// a schema
{
    "type": "number",
    "oneOf": [
        { "multipleOf": 5 },
        { "multipleOf": 3 }
    ]
}
```
