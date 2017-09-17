# allOf

`allOf`关键字意思是对给定所有的schema进行校验。

```json
// a schema
{
    "allOf": [
        { "type": "string" },
        { "maxLength": 5 }
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

当然，写出满足所有逻辑的schema不是一件容易的事，有时也会出现冲突的逻辑存在。

```json
// a schema
{
    "allOf": [
        { "type": "string" },
        { "type": "number" }
    ]
}
```

```json
// failure
"No way"
```

```json
// failure
1
```
