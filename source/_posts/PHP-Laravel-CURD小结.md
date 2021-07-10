---
title: Laravel-CURD小结
toc: true
date: 2020-03-02 21:35:37
tags: PHP 框架 Laravel
categories:
- [PHP,框架,Laravel]
---

### Laravel-CURD小结

## 1.curd思路设计表格式
	文章列表  id  标题， 内容，类型（类型i的）， 简介， 作者
	文章类型：1新闻，2科技，3社会，4自然，5教育

## 2.建立 模型，
	php artisan make:model Models\Article -a    -a 创建所有 模型 迁移表 控制器

## 3.设计数据表并迁移到数据库
	 在database/migrate   文件夹    php artisan migrate(在数据库生成一个数据表)

## 4.设计数据表的模拟数据格式，生成模拟数据
    方法一
        factory =》faker
        命令  php artisan tinker   factory助手函数factory(App\Models\Article::class, 5)->make();
    factory(App\Models\Article::class, 5)->create();

    方法二
    seeder  php artisan make:seeder ArtTypesTableSeeder 生成类  --->查询构造器填数据
    --->填充 php artisan db:seed(执行DatabaseSeeder.php)(手动执行   php artisan db:seed --class=*** 具体执行某一个填充类)
        

## 5.设置模型属性，  
	详情见模型  1.定义主键 表名称 可填充数据的字段
		protected $primaryKey='id';
   		 protected $table='articles';
   		 protected $fillable = ['title','content','category_id','introduction', 'author'];
  	2 .定义表的关联关系
		 	两个关联表要同时定义关联关系， 可在php artisan tinker 里面做验证【类似sql语句， 程序里能写的都可以在这里做验证，相当于一个交互式的环境】

## 6.设置资源路由
	

## 7.控制器 视图编写相关代码
create----store
edit--------update


![](01.png)
![](02.png)
![](03.png)


