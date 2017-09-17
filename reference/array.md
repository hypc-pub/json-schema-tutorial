# array

在JSON中，数组中每个元素的类型都可能不一样。

```json
// a schema
{ "type": "array" }
```

```json
// success
[1, 2, 3, 4, 5]
```

```json
// success
[3, "different", { "types" : "of values" }]
```

```json
// failure
{"Not": "an array"}
```

## Items

默认情况下，数组元素可以是任何类型。但是，通常，我们需要限制数组元素的类型，这时候，可以使用`items`和`additionalItems`关键字。

在JSON中，有两种方式来校验数组元素：

* **List validation**: 任意长度的数组，每一个元素都匹配同一类型。
* **Tuple validation**: 固定长度的数组，每一个元素都可能有不同的类型，在这种方式中，每个元素的类型与索引项有关。

### List validation

任意长度的数组，每一个元素都匹配同一类型。可以使用单个`items`关键字进行校验。

另外，这种情况下，`additionalItems`关键字没有意义，它也不能被使用。

```json
// a schema
{
    "type": "array",
    "items": {
        "type": "number"
    }
}
```

```json
// success
[1, 2, 3, 4, 5]
```

```json
// faliure
[1, 2, "3", 4, 5]
```

```json
// success
[]
```

### Tuple validation

当数组中每一项具有不同的意义，而且它们的类型又不相同时，可以使用Tuple validation。

例如街道地址：

```
1600 Pennsylvania Avenue NW
```

它们的意思是：

```
[number, street_name, street_type, direction]
```

为此，我们需要校验这个数组，则需要按顺序校验每个元素的类型。

```json
// a schema
{
    "type": "array",
    "items": [{
        "type": "number"
    }, {
        "type": "string"
    }, {
        "type": "string",
        "enum": ["Street", "Avenue", "Boulevard"]
    }, {
        "type": "string",
        "enum": ["NW", "NE", "SW", "SE"]
    }]
}
```

```json
// success
[1600, "Pennsylvania", "Avenue", "NW"]
```

```json
// failure
[24, "Sussex", "Drive"]
```

```json
// failure
["Palais de l'Élysée"]
```

```json
// success
[10, "Downing", "Street"]
```

```json
// success
[1600, "Pennsylvania", "Avenue", "NW", "Washington"]
```

`additionalItems`关键字用于控制是否允许有额外的元素。
当`additionalItems`关键字的值为false时，表示不允许有额外的元素。

```json
// a schema
{
    "type": "array",
    "items": [{
        "type": "number"
    }, {
        "type": "string"
    }, {
        "type": "string",
        "enum": ["Street", "Avenue", "Boulevard"]
    }, {
        "type": "string",
        "enum": ["NW", "NE", "SW", "SE"]
    }],
    "additionalItems": false
}
```

```json
// success
[1600, "Pennsylvania", "Avenue", "NW"]
```

```json
// success
[1600, "Pennsylvania", "Avenue"]
```

```json
// failure
[1600, "Pennsylvania", "Avenue", "NW", "Washington"]
```

## Length

可以使用`minItems`和`maxItems`来限制数组元素的个数。

```json
// a schema
{
    "type": "array",
    "minItems": 2,
    "maxItems": 3
}
```

```json
// failure
[]
```

```json
// failure
[1]
```

```json
// success
[1, 2]
```

```json
// success
[1, 2, 3]
```

```json
// failure
[1, 2, 3, 4]
```

## Uniqueness

当需要保证数组中每个元素都是唯一时，可以使用关键字`uniqueItems`，并将值设为true。

```json
// a schema
{
    "type": "array",
    "uniqueItems": true
}
```

```json
// success
[1, 2, 3, 4, 5]
```

```json
// failure
[1, 2, 3, 3, 4]
```

```json
// success
[]
```
