# Mysql Commands

<!-- TOC -->
  - [查看配置文件的读取顺序](#查看配置文件的读取顺序)
  - [远程连接](#远程连接)
    - [tcp](#tcp)
    - [socket](#socket)
  - [查看版本](#查看版本)
  - [修改动态参数](#修改动态参数)
  - [查看线程](#查看线程)
  - [查看数据引擎](#查看数据引擎)
  - [InnoDB缓冲池相关配置](#innodb缓冲池相关配置)
    - [查看缓冲池大小](#查看缓冲池大小)
    - [缓冲池实例个数](#缓冲池实例个数)
    - [查看各个缓冲池的使用状态](#查看各个缓冲池的使用状态)
    - [查看midpoint位置](#查看midpoint位置)
    - [页读取到mid位置后需要等待多久才会被加入到LRU列表的热端](#页读取到mid位置后需要等待多久才会被加入到lru列表的热端)
    - [重做日志缓冲大小](#重做日志缓冲大小)
    - [LRU列表中可用页的数量](#lru列表中可用页的数量)
    - [最大脏页百分比](#最大脏页百分比)
    - [每次purge清理的undo页数](#每次purge清理的undo页数)
    - [开启和关闭各种Buffer的选项](#开启和关闭各种buffer的选项)
    - [Change Buffer的最大使用内存数量](#change-buffer的最大使用内存数量)
    - [查看unzip_LRU中的页](#查看unzip_lru中的页)
    - [查看LRU列表中脏页数量](#查看lru列表中脏页数量)
  - [InnoDB的一些开关参数](#innodb的一些开关参数)
    - [查看自适应哈希索引（AHI）是否开启](#查看自适应哈希索引ahi是否开启)
    - [查看是否启用Native AIO](#查看是否启用native-aio)
    - [查看是否启用刷新邻接页](#查看是否启用刷新邻接页)
    - [数据库关闭时InnoDB的行为](#数据库关闭时innodb的行为)
  - [查看doublewrite运行情况](#查看doublewrite运行情况)
  - [错误日志](#错误日志)
  - [慢查询日志](#慢查询日志)
    - [是否开启](#是否开启)
    - [文件位置](#文件位置)
    - [慢查询时间设置](#慢查询时间设置)
    - [如果运行的SQL语句没有使用索引，则会记录到慢查询日志文件](#如果运行的sql语句没有使用索引则会记录到慢查询日志文件)
    - [表示没分钟允许记录到slow log的且未使用索引的SQL语句的限制](#表示没分钟允许记录到slow-log的且未使用索引的sql语句的限制)
    - [查看慢查询日志](#查看慢查询日志)
    - [查看执行时间最长的10条SQL语句](#查看执行时间最长的10条sql语句)
    - [慢查询输出格式](#慢查询输出格式)
    - [表存储时查看慢查询日志](#表存储时查看慢查询日志)
    - [查看slow_log表结构](#查看slow_log表结构)
  - [二进制日志](#二进制日志)
    - [开启binlog：](#开启binlog)
    - [文件路径在数据库所在目录（datadir）](#文件路径在数据库所在目录datadir)
    - [单个二进制文件的最大值](#单个二进制文件的最大值)
    - [缓冲中的二进制文件大小](#缓冲中的二进制文件大小)
    - [使用二进制日志缓存的事务数量](#使用二进制日志缓存的事务数量)
    - [是否开启同步写磁盘](#是否开启同步写磁盘)
    - [二进制日志的格式](#二进制日志的格式)
  - [InnoDB重做日志](#innodb重做日志)
    - [每个文件大小](#每个文件大小)
    - [每个组的文件个数](#每个组的文件个数)
    - [日志镜像文件组的数量](#日志镜像文件组的数量)
    - [日志文件组所在路径](#日志文件组所在路径)
    - [在commit操作时，处理重做日志的方式](#在commit操作时处理重做日志的方式)


## 查看配置文件的读取顺序
```
mysql --help|grep my.cnf 
```

## 远程连接

### tcp
```
mysql -h 120.24.101.110 -u public_yk -p -P 4040
gh7gh5esazds63
```
### socket
```
SHOW VARIABLES LIKE 'socket'; //查看socket文件
mysql -u root -S /var/lib/mysql/mysql.sock
```

## 查看版本
```
SHOW version();
SHOW VARIABLES LIKE 'innodb_version';
```

## 修改动态参数
```
SET@@[global|session].system_var_name=expr;
```

## 查看线程
```
SHOW VARIABLES LIKE 'innodb_%io_threads'; //io线程
SHOW VARIABLES LIKE 'innodb_purge_threads'; //purge线程
```

## 查看数据引擎
```
SHOW ENGINES;  //查看支持的数据引擎
SHOW ENGINE INNODB STATUS; //查看每个缓冲池实例对象运行的状态
```

## InnoDB缓冲池相关配置

### 查看缓冲池大小
```
SHOW VARIABLES LIKE 'innodb_buffer_pool_size'; 
```

### 缓冲池实例个数
```
SHOW VARIABLES LIKE 'innodb_buffer_pool_instances'; 
```

### 查看各个缓冲池的使用状态
```
USE information_schema;
SELECT POOL_ID,POOL_SIZE,FREE_BUFFERS,DATABASE_PAGES FROM INNODB_BUFFER_POOL_STATS; 
```

### 查看midpoint位置
```
SHOW VARIABLES LIKE 'innodb_old_blocks_pct'; 
```

### 页读取到mid位置后需要等待多久才会被加入到LRU列表的热端
```
SHOW VARIABLES LIKE 'innodb_old_blocks_time'; 
```

### 重做日志缓冲大小
```
SHOW VARIABLES LIKE 'innodb_log_buffer_size'; 
```

### LRU列表中可用页的数量
```
SHOW VARIABLES LIKE 'innodb_lru_scan_depth'; 
```

### 最大脏页百分比
超过会强制执行checkpoint
```
SHOW VARIABLES LIKE 'innodb_max_dirty_pages_pct'; 
```
 
### 每次purge清理的undo页数
```
SHOW VARIABLES LIKE 'innodb_purge_batch_size'; 
```

### 开启和关闭各种Buffer的选项
```
SHOW VARIABLES LIKE 'innodb_change_buffering'; 
```

### Change Buffer的最大使用内存数量 
默认25（即1/4的缓冲池内存空间），最大有效值为50
```
SHOW VARIABLES LIKE 'innodb_change_buffer_max_size'; 
```

### 查看unzip_LRU中的页
```
USE information_schema;
SELECT TABLE_NAME,SPACE,PAGE_NUMBER,COMPRESSED_SIZE FROM INNODB_BUFFER_PAGE_LRU WHERE COMPRESSED_SIZE <> 0;  
```

### 查看LRU列表中脏页数量
```
USE information_schema;
SELECT TABLE_NAME,SPACE,PAGE_NUMBER,PAGE_TYPE FROM INNODB_BUFFER_PAGE_LRU WHERE OLDEST_MODIFICATION > 0; 
```

## InnoDB的一些开关参数

### 查看自适应哈希索引（AHI）是否开启
```
SHOW VARIABLES LIKE 'innodb_adaptive_hash_index';
```

### 查看是否启用Native AIO
```
SHOW VARIABLES LIKE 'innodb_use_native_aio';
```

### 查看是否启用刷新邻接页
```
SHOW VARIABLES LIKE 'innodb_flush_neighbors';
```

### 数据库关闭时InnoDB的行为
参数 [0 merge全部；1 merge部分；2不merge]
```
SHOW VARIABLES LIKE 'innodb_fast_shutdown';
```

## 查看doublewrite运行情况
```
SHOW GLOBAL STATUS LIKE 'innodb_dblwr%';

> Innodb_dblwr_page_number
> Innodb_dblwr_writes
```

## 错误日志
```
SHOW VARIABLES LIKE 'log_error';
```

## 慢查询日志

### 是否开启
```
SHOW VARIABLES LIKE 'slow_query_log';
```

### 文件位置
```
SHOW VARIABLES LIKE 'slow_query_log_file';
```

### 慢查询时间设置
```
SHOW VARIABLES LIKE 'long_query_time';
```

### 如果运行的SQL语句没有使用索引，则会记录到慢查询日志文件
```
SHOW VARIABLES LIKE' log_queries_not_using_indexes';
```
### 表示没分钟允许记录到slow log的且未使用索引的SQL语句的限制
默认0，不限制
```
SHOW VARIABLES LIKE' log_queries_not_using_indexes'; 
```

### 查看慢查询日志
```
mysqldumpslow localhost-slow.log
```

### 查看执行时间最长的10条SQL语句
```
mysqldumpslow -s at -t 1 localhost-slow.log 
```

### 慢查询输出格式
默认FILE（文件），设为TABLE则使用 *slow_log* 表存储
```
SHOW VARIABLES LIKE 'log_output';
```

### 表存储时查看慢查询日志
```
SELECT * FROM mysql.slow_log;
```

### 查看slow_log表结构
默认csv引擎
```
SHOW CREATE TABLE mysql.slow_log;
```
## 二进制日志

### 开启binlog：
修改my.conf，去掉log_bin的注释

### 文件路径在数据库所在目录（datadir）
```
SHOW VARIABLES LIKE 'datadir';
```

### 单个二进制文件的最大值
默认1G
```
show variables like 'max_binlog_size'; 
```

### 缓冲中的二进制文件大小
默认32k
```
show variables like 'binlog_cache_size'; 
```

### 使用二进制日志缓存的事务数量
使用临时文件写二进制日志的次数: Binlog_cache_disk_use <br>
使用缓冲写二进制日志的次数: Binlog_cache_use
```
show global status like 'binlog_cache%';
```

### 是否开启同步写磁盘
```
show variables like 'sync_binlog'; 
```

### 二进制日志的格式 
STATEMENT | ROW | MIXED 
```
show variables like 'binlog_format'; 
```

## InnoDB重做日志

### 每个文件大小
<=512G
```
SHOW VARIABLES LIKE 'innodb_log_file_size';
```

### 每个组的文件个数
默认2
```
SHOW VARIABLES LIKE 'innodb_log_files_in_group';
```

### 日志镜像文件组的数量
默认1，表示只有一个文件组，没有镜像
```
SHOW VARIABLES LIKE 'innodb_mirrored_log_groups';
```

### 日志文件组所在路径
默认./，表示在MySQL数据库的数据目录下
```
SHOW VARIABLES LIKE 'innodb_log_group_home_dir';
```

### 在commit操作时，处理重做日志的方式
0 提交时不写磁盘; 
1 提交时同步写磁盘; 
2 异步写磁盘
```
SHOW VARIABLES LIKE 'innodb_flush_log_at_trx_commit';
```