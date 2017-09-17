# anyOf

`anyOf`用于匹配给定schema中的一个或多个。

```json
// a schema
{
    "anyOf": [
        { "type": "string" },
        { "type": "number" }
    ]
}
```

```json
// success
"Yes"
```

```json
// success
42
```

```json
// failure
{ "Not a": "string or number" }
```
