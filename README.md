[English](./README-EN.md) | 中文

<p align="center"><img src="https://laravel.com/assets/img/components/logo-laravel.svg"><span align="center">Plus</span> </p>

![php-badge](https://img.shields.io/badge/php-%3E%3D%207.1-8892BF.svg)
![laravel-badge](https://img.shields.io/badge/Laravel%20-%3E%3D5.8-red.svg)
[![Build Status](https://api.travis-ci.org/ElapseAnnals/LaravelPlus.svg)](https://travis-ci.org/ElapseAnnals/LaravelPlus)
<img class="latest_stable_version_img" src="https://poser.pugx.org/elapse-annals/laravel-plus/v/stable">
<img class="total_img" src="https://poser.pugx.org/elapse-annals/laravel-plus/downloads">
<img class="latest_unstable_version_img" src="https://poser.pugx.org/elapse-annals/laravel-plus/v/unstable">
[![License](https://poser.pugx.org/elapse-annals/laravel-plus/license)](LICENSE)
[![composer.lock](https://poser.pugx.org/elapse-annals/laravel-plus/composerlock)](https://packagist.org/packages/elapse-annals/laravel-plus)
<a href="https://beerpay.io/ElapseAnnals/LaravelPlus"><img src="https://beerpay.io/ElapseAnnals/LaravelPlus/make-wish.svg?style=flat" /></a>

## 介绍
[LaravelPlus](https://github.com/ElapseAnnals/LaravelPlus) 基于 [Laravel](https://github.com/laravel/laravel) 增加一部分软件包初始安装和进行实际业务使用功能调整



## 版本基础
待完成 Todo List 后自身文档版本考虑于 Laravel 版本一致

当前版本基于 

| PHP     | Laravel |
|:-------:|:-------:|
| >=7.1.3 | >=5.8    |

## 文档

Please see [Wiki](https://github.com/ElapseAnnals/LaravelPlus.wiki.git) 

## 项目使用

```php
// 下载项目
git clone https://github.com/ElapseAnnals/LaravelPlus.git   
或
composer create-project elapse-annals/laravel-plus
mv laravel-plus  LaravelPlus

复制项目方案：
    1.当前目录运行复制脚本(推荐)
    php LaravelPlus/create YourProject
    
    2.复制项目至自身项目
        cd LaravelPlus
        rm composer.lock
        rsync -av --exclude  . --exclude  .. --exclude  .git/ --exclude  vendor/ --exclude  .github/ LaravelPlus/* YourProject               // */         
        cd YourProject
        rm composer.lock .env .travis
        cp .env.example .env   

cd YourProject //  进入 YourProject 项目中
composer install   // 更新软件包 （请先已安装 composer ）
php artisan key:generate    // 更新 key

php artisan storage:link // 图片资源软连接映射【非必须】
```
Tips:
1. 兼容 laravel-plus 目录名

<hr>

## 功能使用说明

##### 创建分层脚本
```
 php artisan make:framework Test  // 创建分层结构
 php artisan make:framework Test --basis  // 创建系统分层和主要分层结构（Controller, Service, Repository）
 php artisan make:framework Test --D // 删除分层结构 
```

##### 热切换配置使用（config/dynamic/）
```php
config('dynamic.env')

```
dynamic 目录文件说明
   -  production 生产环境 (必须配置)
 -  develop 开发环境 (必须配置，以下配置继承 develop 配置)
    -  test 测试环境
    -  local 本地环境
    -  simulation 仿真环境
    
Tips：
  
1. .env 配置 DYNAMIC_IS_STRICT 控制热配是否严格模式（默认 false 关闭）
    - 严格模式下不会继承 production/develop，完全采用当前环境配置
2. 默认在继承基础上有重复属性，会覆盖继承项 
3. 继承基础特有属性会被携带至当前配置 
4. config/dynamic.php 为 IDEA 提示文件，使用空 key 即可

优化默认路由中闭包
- 路由中禁止使用闭包，如有需要请在 ClosureController 中注册

##### 缓存清理
- php artisan optimize:clear     // (慎用）
    - php artisan view:clear
    - php artisan cache:clear    // 应用程序缓存清理(慎用- 会清理 config.cache 中启用缓存)
    - php artisan route:cache
    - php artisan config:clear
    - php artisan clear-compiled    // 清理编译
 php artisan debug:clear

##### 性能优化（只建议生产环境使用）
- php artisan optimize
    - php artisan config:cache
    - php artisan route:cache
- php artisan view:cache
- composer dumpautoload


##### 前端样式构建

 ```php
npm run dev    // 本地开发,开启 debug 模式

npm run prod    // 线上部署,进行压缩

npm run watch   // 监视编译（开发时启用）
```

##### 本地服务开启
```php
php artisan serve
```

<hr />

### [改动内容](https://github.com/ElapseAnnals/LaravelPlus/wiki/3.-%E6%94%B9%E5%8A%A8%E5%86%85%E5%AE%B9)
- 设置日志打印默认按天执行（.env::LOG_CHANNEL）
- 增加默认加载软件包
    - production  生产环境
        - [respect/validation](https://github.com/Respect/Validation) 验证包
        - [react/react](https://github.com/reactphp/react) ReactPHP 多进程异步扩展（可以移除）
        - 引入 ElasticSearch For scout
            - [laravel/scout](https://github.com/laravel/scout) 
            - [tamayo/laravel-scout-elastic](https://github.com/ErickTamayo/laravel-scout-elastic)
        - [elastic/elasticsearch-php](https://github.com/elastic/elasticsearch-php) 原生 ElasticSearch (可选)
        - [rap2hpoutre/laravel-log-viewer](https://github.com/rap2hpoutre/laravel-log-viewer) 日志展示 [访问 host/logs] 
        - [predis/predis](https://github.com/nrk/predis) Redis 插件（建议使用 php-redis 扩展）
    - develop     开发环境
      - [reliese/laravel](https://github.com/reliese/laravel)         模型 code 代码生成包
      - [barryvdh/laravel-debugbar](https://github.com/barryvdh/laravel-debugbar)   debuger 工具包
      - [barryvdh/laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper)   ide 帮助包    
      - [overtrue/laravel-query-logger](https://github.com/overtrue/laravel-query-logger)       日志包
      - [nunomaduro/phpinsights](https://github.com/nunomaduro/phpinsights)          统计检测项目问题（类似 PHPCS,需求版本 php 7.2.* ，请手动安装 composer require nunomaduro/phpinsights --dev）
      - [infyomlabs/laravel-generator](https://github.com/InfyOmLabs/laravel-generator)     代码生成工具（可移除）
  
-  增加前端资源
    - element-ui 样式框架（可选方案 iview）
  
 - 增加热切换配置（config/dynamic）
   -  production 生产环境
   -  develop 开发环境 
        -  local 本地环境
        -  test 测试环境
        -  simulation 仿真环境
   
   
 - 增加默认图片存储目录（storage/app/public/images)
 - 扩展结构分层 [想法来源](https://learnku.com/articles/19452?order_by=created_at&)
    - 系统分层
        - Controller 控制器层
    - 主要分层
        - Service 业务服务层
        - Repository 数据仓库层
    - 扩展分层
        - Presenter 固定业务中控层
        - Transformer 转化层/筛选层（筛选后在选择输出）
        - Formatter 格式化层（对于输出数据进行格式化，服务于 view 层），便于前端模版渲染与展示


## Todo

增加 controller 资源类型处理



扩展  php-redis 配置



增加 redis 集群查询接口（/ demo 中可满足

增加 mq 扩展



简化介绍，完善 wiki



        
