# boolean

布尔值只有两个值`true`和`false`，其他值（如1、0）都不属于布尔值。

```json
{ "type": "boolean" }       // a schema
```

```json
true            // success
```

```json
false           // success
```

```json
"true"          // failure
```

```json
0               // failure
```
