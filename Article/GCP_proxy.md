# Google Cloud Platform 搭建http/https Proxy

1. 安装squid3 

`sudo apt-get install squid3`

2. 修改配置 `sudo vim /etc/squid/squid.conf`

```conf
# 端口默认3128，可自定义
http_port 3128 

# 设置允许的ip
acl allcomputers src 0.0.0.0/0.0.0.0
# 设置可验证的用户名密码
auth_param basic program /usr/lib/squid3/basic_ncsa_auth /etc/squid/passwords
auth_param basic realm proxy
acl authenticated proxy_auth REQUIRED
# 允许经过验证的请求
http_access allow authenticated allcomputers
```

3. 设置用户名密码

    (1) 安装apache2-utils
    ```ssh
    sudo apt-get install apache2-utils
    ```
    (2) 设置用户名密码
    ```ssh
    sudo htpasswd -c -d /etc/squid3/passwords <自定义用户名>
    `> 设置密码，连输两次 <`
    ```
    (3) 给读+可执行权限
    ```ssh
    sudo chmod o+r /etc/squid3/passwords
    ```

4. 启动squid3 `sudo service squid3 start`

5. GCP [添加防火墙规则](https://console.cloud.google.com/networking/firewalls/list?project=planar-airship-286116)

![image](https://dony-1257037510.cos.ap-chengdu.myqcloud.com/markdown/ipproxyfirewall.png)

6. 在本地验证proxy是否可用
```ssh
export http_proxy="http://用户名:密码@代理IP:代理端口"
```
访问Google
```ssh
curl -l "http://www.google.com"
```
