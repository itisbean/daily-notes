# Vscode Debug

## 1. 安装dlv

`Cmd` + `p`, **Go:Install/Update Tools** *dlv*

## 2. 修改 *launch.josn* 配置

``` json
{
    "name": "Launch remote",
    "type": "go",
    "request": "attach",
    "mode": "remote",
    "remotePath": "${workspaceFolder}",
    "port": 2345,
    "showLog": true,
    "trace": "verbose"
}
```

## 3. dlv 

```
dlv debug --headless --listen=:2345 --api-version=2 --log -- -saas_mysql_proxy=10.10.8.33:30696
```

## 4. Vscode启动调试模式
`f5`


> 文档 <br>
> vscode-go https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code <br>
> dlv https://github.com/go-delve/delve/tree/master/Documentation/cli 