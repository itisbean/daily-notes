# Generate SSH key

## 生成密钥对
```
ssh-keygen -t rsa -b 4096 -C "iamdonydou@gmail.com"
```

## 私钥生成公钥
```
ssh-keygen -y -f [private-key-path] > [output-path]
```

## 测试
```
ssh -T git@github.com
```

## 常用参数
- `-t` 指定生成密钥的类型，默认 RSA 
- `-f` 指定生成密钥的路径，默认 ~/.ssh/id_rsa（私钥 id_rsa，公钥 id_rsa.pub）
- `-P` 提供旧密码，空表示不需要密码（-P ''）
- `-N` 提供新密码，空表示不需要密码 (-N '')
- `-b` 指定密钥长度（bits），默认是 2048 位
- `-C` 提供一个新注释，比如邮箱
- `-y` 读取 OpenSSH 格式私钥文件并将 OpenSSH 公钥输出到 std­out
- `-q` 安静模式

## 问题：

### 权限问题
> Permissions 0777 for '/root/.ssh/id_rsa' are too open...

```
chmod 600 /root/.ssh/id_rsa
```