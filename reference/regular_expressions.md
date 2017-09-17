# 正则表达式

[`pattern`][pattern]和[`patternProperties`][patternProperties]关键字都可以使用正则表达式。
正则表达式的语法是从JavaScript语法（[Ecma 262][Ecma262]）演变过来。当然，并没有完整的支持所有语法。

* 一个简单的unicode字符用来匹配它自己。
* `^`: 
* `$`: 
* `(...)`: 
* `|`: 
* `[abc]`: 
* `[a-z]`: 
* `[^abc]`: 
* `[^a-z]`: 
* `+`: 
* `*`: 
* `?`: 
* `+?`、`*?`、`??`: 
* `{x}`: 
* `{x,y}`: 
* `{x,}`: 
* `{x}?`、`{x,y}?`、`{x,}?`: 

```json
// a schema
{
   "type": "string",
   "pattern": "^(\+?86)?1(3|5|7|8)\D{9}$"
}
```

```json
"13512341234"       // success
```

```json
"+8617012341234"    // success
```

```json
"010-12341234"      // failure
```


[pattern]: string.md#pattern
[patternProperties]: object.md#pattern-properties
[Ecma262]: http://www.ecma-international.org/publications/standards/Ecma-262.htm
