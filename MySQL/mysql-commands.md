# Mysql Commands

## 查看配置文件的读取顺序

```MySQL
mysql --help|grep my.cnf
```

## 备份

```MySQL
mysqldump -h localhost -P 3306 -u root -p databasename > bak.sql;
password
```

## 远程连接

### tcp

```MySQL
mysql -h 127.0.0.1 -u root -p -P 3306
password
```

### socket

```MySQL
SHOW VARIABLES LIKE 'socket'; -- 查看socket文件
mysql -u root -S /var/lib/mysql/mysql.sock
```

## 查看版本

```MySQL
SHOW version();
SHOW VARIABLES LIKE 'innodb_version';
```

## 修改动态参数

```MySQL
SET@@[global|session].system_var_name=expr;
```

## 查看线程

```MySQL
SHOW VARIABLES LIKE 'innodb_%io_threads'; -- io线程
SHOW VARIABLES LIKE 'innodb_purge_threads'; -- purge线程
```

## 查看数据引擎

```MySQL
SHOW ENGINES;  //查看支持的数据引擎
SHOW ENGINE INNODB STATUS; //查看每个缓冲池实例对象运行的状态
```

## InnoDB 缓冲池相关配置

### 查看缓冲池大小

```MySQL
SHOW VARIABLES LIKE 'innodb_buffer_pool_size';
```

### 缓冲池实例个数

```MySQL
SHOW VARIABLES LIKE 'innodb_buffer_pool_instances';
```

### 查看各个缓冲池的使用状态

```MySQL
USE information_schema;
SELECT POOL_ID,POOL_SIZE,FREE_BUFFERS,DATABASE_PAGES FROM INNODB_BUFFER_POOL_STATS;
```

### 查看 midpoint 位置

```MySQL
SHOW VARIABLES LIKE 'innodb_old_blocks_pct';
```

### 页读取到 mid 位置后需要等待多久才会被加入到 LRU 列表的热端

```MySQL
SHOW VARIABLES LIKE 'innodb_old_blocks_time';
```

### 重做日志缓冲大小

```MySQL
SHOW VARIABLES LIKE 'innodb_log_buffer_size';
```

### LRU 列表中可用页的数量

```MySQL
SHOW VARIABLES LIKE 'innodb_lru_scan_depth';
```

### 最大脏页百分比

超过会强制执行 checkpoint

```MySQL
SHOW VARIABLES LIKE 'innodb_max_dirty_pages_pct';
```

### 每次 purge 清理的 undo 页数

```MySQL
SHOW VARIABLES LIKE 'innodb_purge_batch_size';
```

### 开启和关闭各种 Buffer 的选项

```MySQL
SHOW VARIABLES LIKE 'innodb_change_buffering';
```

### Change Buffer 的最大使用内存数量

默认 25（即 1/4 的缓冲池内存空间），最大有效值为 50

```MySQL
SHOW VARIABLES LIKE 'innodb_change_buffer_max_size';
```

### 查看 unzip_LRU 中的页

```MySQL
USE information_schema;
SELECT TABLE_NAME,SPACE,PAGE_NUMBER,COMPRESSED_SIZE FROM INNODB_BUFFER_PAGE_LRU WHERE COMPRESSED_SIZE <> 0;
```

### 查看 LRU 列表中脏页数量

```MySQL
USE information_schema;
SELECT TABLE_NAME,SPACE,PAGE_NUMBER,PAGE_TYPE FROM INNODB_BUFFER_PAGE_LRU WHERE OLDEST_MODIFICATION > 0;
```

## InnoDB 的一些开关参数

### 查看自适应哈希索引（AHI）是否开启

```MySQL
SHOW VARIABLES LIKE 'innodb_adaptive_hash_index';
```

### 查看是否启用 Native AIO

```MySQL
SHOW VARIABLES LIKE 'innodb_use_native_aio';
```

### 查看是否启用刷新邻接页

```MySQL
SHOW VARIABLES LIKE 'innodb_flush_neighbors';
```

### 数据库关闭时 InnoDB 的行为

参数 [0 merge 全部；1 merge 部分；2 不 merge]

```MySQL
SHOW VARIABLES LIKE 'innodb_fast_shutdown';
```

## 查看 doublewrite 运行情况

```MySQL
SHOW GLOBAL STATUS LIKE 'innodb_dblwr%';

> Innodb_dblwr_page_number
> Innodb_dblwr_writes
```

## 错误日志

```MySQL
SHOW VARIABLES LIKE 'log_error';
```

## 二进制日志

### 开启 binlog

修改 my.conf，去掉 log_bin 的注释

### 文件路径在数据库所在目录（datadir）

```MySQL
SHOW VARIABLES LIKE 'datadir';
```

### 单个二进制文件的最大值

默认 1G

```MySQL
show variables like 'max_binlog_size';
```

### 缓冲中的二进制文件大小

默认 32k

```MySQL
show variables like 'binlog_cache_size';
```

### 使用二进制日志缓存的事务数量

使用临时文件写二进制日志的次数: Binlog_cache_disk_use
使用缓冲写二进制日志的次数: Binlog_cache_use

```MySQL
show global status like 'binlog_cache%';
```

### 是否开启同步写磁盘

```MySQL
show variables like 'sync_binlog';
```

### 二进制日志的格式

STATEMENT | ROW | MIXED

```MySQL
show variables like 'binlog_format';
```

## InnoDB 重做日志

### 每个文件大小

<=512G

```MySQL
SHOW VARIABLES LIKE 'innodb_log_file_size';
```

### 每个组的文件个数

默认 2

```MySQL
SHOW VARIABLES LIKE 'innodb_log_files_in_group';
```

### 日志镜像文件组的数量

默认 1，表示只有一个文件组，没有镜像

```MySQL
SHOW VARIABLES LIKE 'innodb_mirrored_log_groups';
```

### 日志文件组所在路径

默认./，表示在 MySQL 数据库的数据目录下

```MySQL
SHOW VARIABLES LIKE 'innodb_log_group_home_dir';
```

### 在 commit 操作时，处理重做日志的方式

0 提交时不写磁盘;
1 提交时同步写磁盘;
2 异步写磁盘

```MySQL
SHOW VARIABLES LIKE 'innodb_flush_log_at_trx_commit';
```
