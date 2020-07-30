# JSON空值问题

1. 代码中使用json被忽略
```go
var buf bytes.Buffer
err := (&jsonpb.Marshaler{
        EmitDefaults: true,
}).Marshal(&buf, msg)
if err != nil {
    return nil, err
}
content := string(buf.Bytes())
```

2. http响应json被忽略，需要修改网关层
```go
// 公司框架不能直接修改网关参数，要在注册时传入该option
runtime.WithMarshalerOption(runtime.MIMEWildcard, &runtime.JSONPb{OrigName: true, EmitDefaults: true})(gateway)
```