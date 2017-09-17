# 构建一个复杂的模式

## Reuse

> 这部分内容是草案4新增内容，而草案3没有。

你可以使用关键字`definitions`预先定义部分schema。

```json
// a schema
{
    "type": "object",
    "properties": {
        "street_address": { "type": "string" },
        "city": { "type": "string" },
        "state": { "type": "string" }
    },
    "required": ["street_address", "city", "state"]
}
```

也可以写成：

```json
// a schema
{
    "definitions": {
        "address": {
            "type": "object",
            "properties": {
                "street_address": { "type": "string" },
                "city": { "type": "string" },
                "state": { "type": "string" }
            },
            "required": ["street_address", "city", "state"]
        }
    }
}
```

当使用时，我们用`$ref`关键字进行引用，`$ref`值时一个[JSON Pointer][rfc6901]。

```json
{ "$ref": "#/definitions/address" }
```

如下示例：

```json
// a schema
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "definitions": {
        "address": {
            "type": "object",
            "properties": {
                "street_address": { "type": "string" },
                "city": { "type": "string" },
                "state": { "type": "string" }
            },
            "required": ["street_address", "city", "state"]
        }
    },
    "type": "object",
    "properties": {
        "billing_address": { "$ref": "#/definitions/address" },
        "shipping_address": { "$ref": "#/definitions/address" }
    }
}
```

```json
// success
{
    "shipping_address": {
        "street_address": "1600 Pennsylvania Avenue NW",
        "city": "Washington",
        "state": "DC"
    },
    "billing_address": {
        "street_address": "1st Street SE",
        "city": "Washington",
        "state": "DC"
    }
}
```

## The id property

`id`关键字有两个用途：

* 被声明用来唯一标识一个schema。
* 用来作为`$ref`的base url被解析。

例如，如果有以下声明：

```json
{ "id": "http://foo.bar/schemas/address.json" }
```

那么：

```json
{ "$ref": "person.json" }
```

此时，`person.json`的url为`http://foo.bar/schemas/person.json`。

## Extending

`$ref`的强大之处在于它同组合模式一起使用。

```json
// a schema
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "definitions": {
        "address": {
            "type": "object",
            "properties": {
                "street_address": { "type": "string" },
                "city": { "type": "string" },
                "state": { "type": "string" }
            },
            "required": ["street_address", "city", "state"]
        }
    },
    "type": "object",
    "properties": {
        "billing_address": { "$ref": "#/definitions/address" },
        "shipping_address": {
            "allOf": [{
                "$ref": "#/definitions/address"
            }, {
                "properties": { "type": { "enum": [ "residential", "business" ] } },
                "required": ["type"]
            }]
        }
    }
}
```

```json
// failure
{
    "shipping_address": {
        "street_address": "1600 Pennsylvania Avenue NW",
        "city": "Washington",
        "state": "DC"
    }
}
```

```json
// success
{
    "shipping_address": {
        "street_address": "1600 Pennsylvania Avenue NW",
        "city": "Washington",
        "state": "DC",
        "type": "business"
    }
}
```


[rfc6901]: https://tools.ietf.org/html/rfc6901
