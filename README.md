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
#添加表字段
alter table table1 add transactor varchar(10) not Null;
alter table   table1 add id int unsigned not Null auto_increment primary key
#修改某个表的字段类型及指定为空或非空
>alter table 表名称 change 字段名称 字段名称 字段类型 [是否允许非空];
>alter table 表名称 modify 字段名称 字段类型 [是否允许非空];
>alter table 表名称 modify 字段名称 字段类型 [是否允许非空];
#修改某个表的字段名称及指定为空或非空
>alter table 表名称 change 字段原名称 字段新名称 字段类型 [是否允许非空
#如果要删除某一字段，可用命令：ALTER TABLE mytable DROP 字段 名;
```

### 站点管理 自定义变量 增加备案等字段
```php
打开\phpcms\languages\zh-cn\admin.lang.php 
PHPCMS的中文语言定义文件。
查找“site_management”大概在505行，在上面新建一行。
加入新建字段的名称
$LANG['contacts'] = 'Contacts'; //联系方式
$LANG['contacts_address'] = 'Address';//地址
$LANG['contacts_phone'] = 'Phone';//电话
$LANG['contacts_mobile'] = 'Mobile';//手机
$LANG['contacts_email'] = 'Email';//邮箱
$LANG['contacts_qq'] = 'QQ';//QQ
$LANG['contacts_beian'] = 'Beian';//备案
同样打开\phpcms\languages\en\admin.lang.php 
加入英文名称。

修改后台模板文件
打开\phpcms\modules\admin\templates\site_add.tpl.php
搜索“seo_configuration”在“<div class="bk15"></div>”下面新建一行
复制以下内容
<div class="bk15"></div>
<fieldset>
<legend><?php echo L('contacts')?></legend>
<table width="100%"  class="table_form">
  <tr>
    <th width="80"><?php echo L('contacts_address')?>：</th>
    <td class="y-bg"><input type="text" class="input-text" name="contacts_address" id="contacts_address" size="30" /></td>
  </tr>
  <tr>
    <th><?php echo L('contacts_phone')?>：</th>
    <td class="y-bg"><input type="text" class="input-text" name="contacts_phone" id="contacts_phone" size="30" /></td>
  </tr>
    <tr>
    <th><?php echo L('contacts_mobile')?>：</th>
    <td class="y-bg"><input type="text" class="input-text" name="contacts_mobile" id="contacts_mobile" size="30" /></td>
  </tr>
<tr>
    <th><?php echo L('contacts_email')?>：</th>
    <td class="y-bg"><input type="text" class="input-text" name="contacts_email" id="contacts_email" size="30" /></td>
  </tr>
<tr>
    <th><?php echo L('contacts_qq')?>：</th>
    <td class="y-bg"><input type="text" class="input-text" name="contacts_qq" id="contacts_qq" size="30" /></td>
  </tr>
<tr>
    <th><?php echo L('contacts_beian')?>：</th>
    <td class="y-bg"><input type="text" class="input-text" name="contacts_beian" id="contacts_beian" size="30" /></td>
  </tr>
</table>
</fieldset>
3
同样打开 站点信息修改页面\phpcms\modules\admin\templates\site_edit.tpl.php
加入上一步添加的字段。

打开后台站点信息修改文件
\phpcms\modules\admin\site.php
查找“add()”
查找“$default_style”
在下面新建一行，加入字段获取代码：
$contacts_address = isset($_POST['contacts_address']) && trim($_POST['contacts_address']) ? trim($_POST['contacts_address']) : '';
$contacts_phone = isset($_POST['contacts_phone']) && trim($_POST['contacts_phone']) ? trim($_POST['contacts_phone']) : '';
$contacts_mobile = isset($_POST['contacts_mobile']) && trim($_POST['contacts_mobile']) ? trim($_POST['contacts_mobile']) : '';
$contacts_email = isset($_POST['contacts_email']) && trim($_POST['contacts_email']) ? trim($_POST['contacts_email']) : '';
$contacts_qq = isset($_POST['contacts_qq']) && trim($_POST['contacts_qq']) ? trim($_POST['contacts_qq']) : '';
$contacts_beian = isset($_POST['contacts_beian']) && trim($_POST['contacts_beian']) ? trim($_POST['contacts_beian']) : '';
查找“=>$default_style”在后面加入',contacts_address'=>$contacts_address,'contacts_phone'=>$contacts_phone,'contacts_mobile'=>$contacts_mobile,'contacts_email'=>$contacts_email,'contacts_qq'=>$contacts_qq,'contacts_beian'=>$contacts_beian)
同样的在"edit()”函数里面
加入更新字段的代码
然后在修改数据库
打开数据表
v9_site
在数据表结构新建以下字段
contacts_address varchar(100)
contacts_phone varchar(30)
contacts_mobile varchar(30)
contacts_email varchar(30)
contacts_qq varchar(30)
contacts_qq varchar(30)
contacts_beian varchar(30)
然后保存
```
