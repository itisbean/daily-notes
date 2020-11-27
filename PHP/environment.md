# Environment Problem

## Centos升級php

1. 移除舊版本 
```
yum remove php*
```
2. 安裝新版本 
```
yum install -y php72w php72w-opcache php72w-xml php72w-mcrypt php72w-gd php72w-devel php72w-mysqlnd php72w-intl php72w-mbstring  
```
3. 安裝php-fpm
```sh
yum install php72w-fpm
# 啟動
systemctl start php-fpm.service
# 開機啟動
systemctl enable php-fpm.service
```
4. 安装redis扩展
```sh
# phpredis库
git clone  https://github.com/phpredis/phpredis.git
cd phpredis
# 切换到一个稳定版本的分支
git checkout issue.1214-session-failover
# 安装
phpize
./configure 
make && sudo make install
# 修改php配置 （註：不要在php.ini直接加，會報錯`php_json_decode_ex`，原因是和json擴展加載先後順序衝突）
vim /etc/php.d/redis.ini
`extension=/usr/lib64/php/modules/redis.so`
# 重啟php-fpm
systemctl restart php-fpm
```
5. 其他問題
- 報錯 `PHP Warning: PHP Startup: Unable to load dynamic library undefined symbol: php_json_decode_ex`
    解決：見上。

- 報錯 `the requested PHP extension bcmath is missing from your system`
    ```
    yum install php72w-bcmath
    ```

- 代碼報錯 `Redis::delete() is deprecated`
    原因：php-redis 5版本以上弃用了 Redis::delete()
    查看版本 `php --ri redis`
    解決：将 `delete($key)` 改成 `del($key)`