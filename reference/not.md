# not

`not`表示json数据不允许匹配某种schema。

```json
// a schema
{ "not": { "type": "string" } }
```

```json
// success
42
```

```json
// success
{ "key": "value" }
```

```json
// failure
"I am a string"
```
