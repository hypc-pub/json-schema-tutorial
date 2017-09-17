# string

string类型用于字符串，它当然也包含unicode字符。

```json
{ "type": "string" }        // a schema
```

```json
"This is a string"          // success
```

```json
"中文"                    // success
```

```json
""              // success
```

```json
"42"            // success
```

```json
31.15           // failure
```

## length

在使用string类型的时候，也可以使用`minlength`、`maxlength`属性来限制字符串的长度：

```json
// a schema
{
  "type": "string",
  "minLength": 2,
  "maxLength": 3
}
```

```json
"A"         // failure
```

```json
"AB"        // success
```

```json
"ABC"       // success
```

```json
"ABCD"      // failure
```

## pattern

当然也可以使用`pattern`属性用来检查是否匹配一个正则表达式。正则表达式的语法参见[Ecma 262][Ecma262]。
更多正则表达式的内容参见[正则表达式][regular_expressions]这一章。

以下是一个验证手机号码的例子：

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

## format

format关键字能对一些常用的类型进行校验，当然这些值也可以使用[正则表达式][regular_expressions]进行校验。

`JSON Schema`能理解一些常用类型，当能不能理解的将会忽略。

### 内建formats

* **date-time**: 日期时间格式化，详见[RFC3339, 5.6章][rfc3339]。
* **email**: 电子邮箱地址，详见[RFC5322, 3.4.1章][rfc5322]。
* **hostname**: 互联网主机名，详见[RFC1034，3.1章][rfc1034]。
* **ipv4**: IPv4地址，详见[RFC2673，3.2章][rfc2673]。
* **ipv6**: IPv6地址，详见[RFC2373，2.2章][rfc2373]。
* **uri**: 通用资源标识符，详见[RFC3986][rfc3986]。


[Ecma262]: http://www.ecma-international.org/publications/standards/Ecma-262.htm
[regular_expressions]: regular_expressions.md
[rfc3339]: http://tools.ietf.org/html/rfc3339
[rfc5322]: http://tools.ietf.org/html/rfc5322
[rfc1034]: http://tools.ietf.org/html/rfc1034
[rfc2673]: http://tools.ietf.org/html/rfc2673
[rfc2373]: http://tools.ietf.org/html/rfc2373
[rfc3986]: http://tools.ietf.org/html/rfc3986
