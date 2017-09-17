# $schema关键字

`$schema`关键字用来声明当前schema属于哪种schema规范。

```json
{ "$schema": "http://json-schema.org/schema#" }         // schema声明
```

如果你schema是根据某个`JSON Schema`规范编写的，而不仅仅是最新版，你可以使用以下预设值。

* **http://json-schema.org/schema#**: 当前版本的`JSON Schema`。
* **http://json-schema.org/hyper-schema#**: 当前版本的`JSON Schema hyperschema`。
* **http://json-schema.org/draft-04/schema#**: 符合_draft v4_的`JSON Schema`。
* **http://json-schema.org/draft-04/hyper-schema#**: 符合_draft v4_的`JSON Schema hyperschema`。
* **http://json-schema.org/draft-03/schema#**: 符合_draft v3_的`JSON Schema`。
* **http://json-schema.org/draft-03/hyper-schema#**: 符合_draft v3_的`JSON Schema hyperschema`。

如果你扩展了`JSON Schema`用于校验自定义的关键字，那么`$schema`可以使用你自定义的uri，它不能是上面预设值之一。
