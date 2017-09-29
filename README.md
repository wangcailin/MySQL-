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

#### 导出整个数据库中的所有数据
```mysql
1、在linux命令行下输入:
`mysqldump -u userName -p  dabaseName  > fileName.sql`
fileName.sql最好加上路径名

导出数据库中的某个表的数据
`mysqldump -u userName -p  dabaseName tableName > fileName.sql`
导出整个数据库中的所有的表结构

在linux命令行下输入：
`mysqldump -u userName -p -d dabaseName  > fileName.sql`
注意：是加了-d 

导出整个数据库中某个表的表结构

在linux命令行下输入：
`mysqldump -u userName -p -d dabaseName tableName > fileName.sql`
注意：是加了-d

导入mysql方法1

进入linux命令命令行下：
mysql -uroot -p 回车  输入密码
`source fileName.sql`
注意fileName.sql要有路径名，例如：source /home/user/data/fileName.sql
导入mysql方法2

进入linux命令命令行下：
`mysql -uroot -p database < fileName.sql`
注意fileName.sql要有路径名
```

### 字段处理
```mysql
1：删除列
ALTER TABLE 【表名字】 DROP 【列名称】
2：增加列
ALTER TABLE 【表名字】 ADD 【列名称】 INT NOT NULL  COMMENT '注释说明'
3：修改列的类型信息
ALTER TABLE 【表名字】 CHANGE 【列名称】【新列名称（这里可以用和原来列同名即可）】 BIGINT NOT NULL  COMMENT '注释说明'
4：重命名列
ALTER TABLE 【表名字】 CHANGE 【列名称】【新列名称】 BIGINT NOT NULL  COMMENT '注释说明'
5：重命名表
ALTER TABLE 【表名字】 RENAME 【表新名字】
6：删除表中主键
Alter TABLE 【表名字】 drop primary key
7：添加主键
ALTER TABLE sj_resource_charges ADD CONSTRAINT PK_SJ_RESOURCE_CHARGES PRIMARY KEY (resid,resfromid)
8：添加索引
ALTER TABLE sj_resource_charges add index INDEX_NAME (name);
9: 添加唯一限制条件索引
ALTER TABLE sj_resource_charges add unique emp_name2(cardnumber);
10: 删除索引
alter table tablename drop index emp_name;
11: 在指定字段之前添加一个字段
ALTER TABLE 【表名字】 ADD 【列名称】 INT NOT NULL  COMMENT '注释说明' AFTER 【在字段之后】;
```

