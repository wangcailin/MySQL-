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
### 创建新用户
格式:`CREATE USER 'username'@'host' IDENTIFIED BY 'password'`
### 给用户分配表
格式：`grant all on 数据库.* to 用户名@登录主机 identified by “密码”`

### 创建数据库
命令：create database <数据库名>
#### 创建数据库并分配用户
 - CREATE DATABASE 数据库名;
 - GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON 数据库名.* TO 数据库名@localhost IDENTIFIED BY '密码';
 - SET PASSWORD FOR '数据库名'@'localhost' = OLD_PASSWORD('密码');
 
`--skip-lock-tables` 备份有表锁的数据库

### windows开启MySQL general log日志
```shell
mysql@localhost.(none)>show global variables like "%genera%";
mysql@localhost.(none)>set global general_log=on;
```
### 导出数据库结构
```shell
mysqldump --opt -d 数据库名 -u root -p > xxx.sql
```

### 连接字段
```
function statistics_list($where = '', $start = 0, $end = 15, $start_time, $end_time){
    $sql = "SELECT statistics.*,store.* FROM ecs_touch_sale_statistics statistics, ecs_touch_store store 
WHERE statistics.store_id = store.id AND 
UNIX_TIMESTAMP(CONCAT('-',statistics.`year`,statistics.`month`,statistics.`day`)) > ".$start_time." AND 
UNIX_TIMESTAMP(CONCAT('-',statistics.`year`,statistics.`month`,statistics.`day`)) < ".$end_time.$where."  LIMIT ".$start.",".$end;
    return $GLOBALS['db']->getAll($sql);
}
```
### 
```
UPDATE ecs_touch_sale_statistics SET add_time = UNIX_TIMESTAMP(CONCAT(`year`,`month`,`day`))
```
