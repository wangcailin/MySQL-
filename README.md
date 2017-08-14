# MySQL-
MySQL日常使用命令  增删改查 权限分配 导入导出等

### 连接MySQL
格式： `mysql -h(host) -u(user) －p(password)`

### 修改密码
格式：`mysqladmin -u用户名 -p旧密码 password 新密码`
```shell
# 给root加个密码ab12
mysqladmin -u root -password ab12

# 再将root的密码改为djg345
mysqladmin -u root -p ab12 password djg345
```

### 增加新用户
格式：`grant all on 数据库.* to 用户名@登录主机 identified by “密码”`

### 创建数据库
命令：create database <数据库名>
#### 创建数据库并分配用户
 - CREATE DATABASE 数据库名;
 - GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON 数据库名.* TO 数据库名@localhost IDENTIFIED BY '密码';
 - SET PASSWORD FOR '数据库名'@'localhost' = OLD_PASSWORD('密码');

