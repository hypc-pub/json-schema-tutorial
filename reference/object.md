# object

在JSON中，对象是一种映射类型，它用来映射`keys`和`values`。在`JSON`中，`keys`必须是字符串。

```json
// a schema
{ "type": "object" }
```

```json
// success
{
   "key": "value",
   "another_key": "another_value"
}
```

```json
// success
{
    "Sun": 1.9891e30,
    "Jupiter": 1.8986e27,
    "Saturn": 5.6846e26,
    "Neptune": 10.243e25,
    "Uranus": 8.6810e25,
    "Earth": 5.9736e24,
    "Venus": 4.8685e24,
    "Mars": 6.4185e23,
    "Mercury": 3.3022e23,
    "Moon": 7.349e22,
    "Pluto": 1.25e22
}
```

```json
// failure
"Not an object"
```

```json
// failure
["An", "array", "not", "an", "object"]
```

## Properties

使用`properties`属性来定义对象上的属性。`properties`的值是一个对象，它的每一个`key`对应`JSON`对象的每一个属性。

```json
// a schema
{
    "type": "object",
    "properties": {
        "number": { "type": "number" },
        "street_name": { "type": "string" },
        "street_type": {
            "type": "string",
            "enum": ["Street", "Avenue", "Boulevard"]
        }
    }
}
```

```json
// success
{ "number": 1600, "street_name": "Pennsylvania", "street_type": "Avenue" }
```

```json
// failure，number属性的值必须是数字
{ "number": "1600", "street_name": "Pennsylvania", "street_type": "Avenue" }
```

```json
// success
{ "number": 1600, "street_name": "Pennsylvania" }
```

```json
// success
{ }
```

```json
// success
{
    "number": 1600,
    "street_name": "Pennsylvania",
    "street_type": "Avenue",
    "direction": "NW"
}
```

`additionalProperties`关键字用于控制额外的属性，那些不在`properties`里面的属性。
当然，默认是允许额外的属性。

`additionalProperties`关键字的值为boolean或object，当`additionalProperties`值设为boolean值且为false时，表示不允许任何额外的属性。

下面是一个`additionalProperties`值为false的例子：

```json
// a schema
{
    "type": "object",
    "properties": {
        "number": { "type": "number" },
        "street_name": { "type": "string" },
        "street_type": {
            "type": "string",
            "enum": ["Street", "Avenue", "Boulevard"]
        }
    },
    "additionalProperties": false
}
```

```json
// success
{ "number": 1600, "street_name": "Pennsylvania", "street_type": "Avenue" }
```

```json
// failure，多了direction属性
{
    "number": 1600,
    "street_name": "Pennsylvania",
    "street_type": "Avenue",
    "direction": "NW"
}
```

如果`additionalProperties`值是一个对象，那么这个对象也是一个`schema`，用来校验不在`properties`列表中的属性。

```json
// a schema
{
    "type": "object",
    "properties": {
        "number": { "type": "number" },
        "street_name": { "type": "string" },
        "street_type": {
            "type": "string",
            "enum": ["Street", "Avenue", "Boulevard"]
        }
    },
    "additionalProperties": { "type": "string" }
}
```

```json
// success
{ "number": 1600, "street_name": "Pennsylvania", "street_type": "Avenue" }
```

```json
// success
{
    "number": 1600,
    "street_name": "Pennsylvania",
    "street_type": "Avenue",
    "direction": "NW"
}
```

```json
// failure，属性office_number值不是字符串类型
{
    "number": 1600,
    "street_name": "Pennsylvania",
    "street_type": "Avenue",
    "office_number": 210
}
```

## Required Properties

默认情况下，`properties`列表中的属性都不是必须的。当某些属性必须时，可以使用`required`关键字。

`required`值是一个长度大于1的数组，而且数组中的每个值都是唯一的。

```json
// a schema
{
    "type": "object",
    "properties": {
        "name": { "type": "string" },
        "email": { "type": "string" },
        "address": { "type": "string" },
        "telephone": { "type": "string" }
    },
    "required": ["name", "email"]
}
```

```json
// success
{
    "name": "William Shakespeare",
    "email": "bill@stratford-upon-avon.co.uk"
}
```

```json
// success
{
    "name": "William Shakespeare",
    "email": "bill@stratford-upon-avon.co.uk",
    "address": "Henley Street, Stratford-upon-Avon, Warwickshire, England",
    "authorship": "in question"
}
```

```json
// failure，缺少属性email
{
    "name": "William Shakespeare",
    "address": "Henley Street, Stratford-upon-Avon, Warwickshire, England",
}
```

## Size

可以使用`minProperties`和`maxProperties`关键字限制属性的个数。

```json
// a schema
{
    "type": "object",
    "minProperties": 2,
    "maxProperties": 3
}
```

```json
// failure
{}
```

```json
// failure
{ "a": 0 }
```

```json
// success
{ "a": 0, "b": 1 }
```

```json
// success
{ "a": 0, "b": 1, "c": 2 }
```

```json
// failure
{ "a": 0, "b": 1, "c": 2, "d": 3 }
```

## Dependencies

`dependencies`允许schema根据某些特殊的属性存在而发生改变。

`JSON Schema`中存在两种形式的依赖关系：

* **Property dependencies**: 声明如果给定属性存在，则某些属性必须存在。
* **Schema dependencies**: 声明如果给定属性存在，则schema发生变化。

### Property dependencies

我们从简单的属性依赖关系开始。
例如，假设你有一个客户的schema，如果你有他们的信用卡号码，你也确保有他们的账单地址。
如果你没有他们的信用卡号码，你也不需要他们的账单地址。
我们使用`dependencies`关键字来定义属性之间的依赖关系，`dependencies`关键字的值是一个对象。

```json
// a schema，其中如果存在credit_card属性，那么billing_address属性也必须存在
{
    "type": "object",
    "properties": {
        "name": { "type": "string" },
        "credit_card": { "type": "number" },
        "billing_address": { "type": "string" }
    },
    "required": ["name"],
    "dependencies": {
        "credit_card": ["billing_address"]
    }
}
```

```json
// success
{
    "name": "John Doe",
    "credit_card": 5555555555555555,
    "billing_address": "555 Debtor's Lane"
}
```

```json
// failure
{
    "name": "John Doe",
    "credit_card": 5555555555555555
}
```

```json
// success
{
    "name": "John Doe"
}
```

```json
// success，没有credit_card属性时，billing_address属性可以存在
{
    "name": "John Doe",
    "billing_address": "555 Debtor's Lane"
}
```

当然，如果想让`credit_card`属性和`billing_address`属性都存在时，可以定义相互依赖关系：

```json
// a schema
{
    "type": "object",
    "properties": {
        "name": { "type": "string" },
        "credit_card": { "type": "number" },
        "billing_address": { "type": "string" }
    },
    "required": ["name"],
    "dependencies": {
        "credit_card": ["billing_address"],
        "billing_address": ["credit_card"]
    }
}
```

```json
// failure
{
    "name": "John Doe",
    "credit_card": 5555555555555555
}
```

```json
// failure
{
    "name": "John Doe",
    "billing_address": "555 Debtor's Lane"
}
```

```json
// success
{
    "name": "John Doe",
    "credit_card": 5555555555555555,
    "billing_address": "555 Debtor's Lane"
}
```

### Schema dependencies

**Schema dependencies**与**Property dependencies**相似，但它不是指定必须的属性，而是扩展让它拥有其他约束。

```json
// a schema，当属性credit_card存在时，它需要额外定义属性billing_address
{
    "type": "object",
    "properties": {
        "name": { "type": "string" },
        "credit_card": { "type": "number" }
    },
    "required": ["name"],
    "dependencies": {
        "credit_card": {
            "properties": {
                "billing_address": { "type": "string" }
            },
            "required": ["billing_address"]
        }
    }
}
```

```json
// success
{
    "name": "John Doe",
    "credit_card": 5555555555555555,
    "billing_address": "555 Debtor's Lane"
}
```

```json
// failure，失败，因为属性credit_card存在时，扩展了属性billing_address，而billing_address是必选属性
{
    "name": "John Doe",
    "credit_card": 5555555555555555
}
```

```json
// success，默认情况下，没有additionalProperties关键字时，可随意添加额外的属性
{
    "name": "John Doe",
    "billing_address": "555 Debtor's Lane"
}
```

## Pattern Properties

正如前面所描述的，`additionalProperties`关键字可以限制对象，使它可以不显示的指定其他属性，也可以显示的指定属性的schema结构。
而这些，有时候还不够，你可能需要指定某些属性，属性名符合某种规则。而这时候就需要用到`patternProperties`。
它从正则表达式映射过来，如果附加的属性符合给定的正则表达式，那么必须对该属性进行校验。

```json
// a schema，以S_开头的属性必须时字符串类型，以I_开头的属性必须时整数类型
{
    "type": "object",
    "patternProperties": {
        "^S_": { "type": "string" },
        "^I_": { "type": "integer" }
    },
    "additionalProperties": false
}
```

```json
// success
{ "S_25": "This is a string" }
```

```json
// success
{ "I_0": 42 }
```

```json
// faliure
{ "S_0": 42 }
```

```json
// faliure
{ "I_42": "This is a string" }
```

```json
// faliure，additionalProperties为false
{ "keyword": "value" }
```

`patternProperties`可以和`additionalProperties`结合使用。在这种情况下，
`additionalProperties`将引用properties中未列出的任何属性，并且不匹配`patternProperties`。

```json
// a schema
{
    "type": "object",
    "properties": {
        "builtin": { "type": "number" }
    },
    "patternProperties": {
        "^S_": { "type": "string" },
        "^I_": { "type": "integer" }
    },
    "additionalProperties": { "type": "string" }
}
```

```json
// success
{ "builtin": 42 }
```

```json
// success
{ "keyword": "value" }
```

```json
// failure
{ "keyword": 42 }
```
