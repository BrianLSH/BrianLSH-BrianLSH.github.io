---
title: Mysql远程连接失败解决方案
toc: true
date: 2019-08-02 16:58:34
tags: mysql基础 远程连接
categories:
- [mysql, 基础]
---

### 今天编译安装mysql, Navicate远程连接失败,整理以下解决方案

```php
1.安全组 开放端口
2.防火墙 开放端口
3. mysql 配置  bind 0000
4.开放权限 修改mysql user表中 root 远程连接权限
```

### 在8.0以前，我们习惯使用以下命令授权远程连接操作：
```php
grant all privileges on *.* to 'root'@'%';
但在8.0以后，使用以上命令会报错
ERROR 1410 (42000): You are not allowed to create a user with GRANT
```

 
### 使用以下命令可以成功，但无法远程登陆：
```php
grant all on *.* to 'root'@'%';

此时，可以使用以下2种方式，实现远程：
-- 1. 使用alter user
alter user set user.host='%' where user.user='root';
-- 2. 使用create user
create user 'userName'@'%' identified 'your_password';
```
### 重要 flushprivileges 别忘记
