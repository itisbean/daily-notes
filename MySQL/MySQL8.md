# MySQL 8.0 新特性

## Performance Schema

- *系统和状态变量* 信息不再保存在 **INFORMATION_SCHEMA** 中，以下表已转到 **Performance Schema**（MySQL 5.7.6引入）：
  `GLOBAL_VARIABLES`
  `SESSION_VARIABLES`
  `GLOBAL_STATUS`
  `SESSION_STATUS`

- 在MySQL 8.0 `SHOW`语句全部基于基础的Performance Schema表

参考：[Migrating to Performance Schema System and Status Variable Tables](https://dev.mysql.com/doc/refman/5.7/en/performance-schema-variable-table-migration.html)

---

## GRANT

- 不能直接 `GRANT ALL PRIVILEGES ON *.* TO 'root'@'127.0.0.1' IDENTIFIED BY 'password' WITH GRANT OPTION;` 隐式创建用户。必须先create用户再分配权限。
  
```MySQL
CREATE USER 'root'@'localhost' IDENTIFIED BY '密码';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
```

- 可以使用`role`批量分配权限

```MySQL
CREATE ROLE ‘developer_user’;
GRANT 'developer_user' TO '用户';

# 在当前对话生效
SET DEFAULT ROLE 'developer_user' TO '用户';
SELECT CURRENT_ROLE();

# 创建新用户使用默认角色
CREATE USER '用户1' IDENTIFIED BY '密码' DEFAULT ROLE 'developer_user';
```

---

