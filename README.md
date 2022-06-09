# Fast-Hyperf
[![Latest Stable Version](http://poser.pugx.org/yogcloud/framework/v)](https://packagist.org/packages/yogcloud/framework) [![Total Downloads](http://poser.pugx.org/yogcloud/framework/downloads)](https://packagist.org/packages/yogcloud/framework) [![Latest Unstable Version](http://poser.pugx.org/yogcloud/framework/v/unstable)](https://packagist.org/packages/yogcloud/framework) [![License](http://poser.pugx.org/yogcloud/framework/license)](https://packagist.org/packages/yogcloud/framework) [![PHP Version Require](http://poser.pugx.org/yogcloud/framework/require/php)](https://packagist.org/packages/yogcloud/framework)

[中文](README.md) | [English](README-en.md)

Hyperf 的一把梭组件


```php
composer require yogcloud/framework
```


# 功能
提供从 `Controller` `Request` `Model` `Service` `Interface` 一整套生成命令
```php
$ php bin/hyperf 
fs
    fs:controller        生成 controller, 默认生成于 app/Controller 目录下
    fs:model             生成 Model, 默认生成于 app/Model 目录下 自动生成 Service,Interface
    fs:plugin            plugin of hyperf install
    fs:request           生成 request, 默认生成于 app/Request 目录下
    fs:service           生成 service, 默认生成于 app/Service 目录下
    fs:serviceInterface  生成 service Interface, 默认生成于 app/Service 目录下
server
    server:restart       Restart hyperf servers.
    server:start         Start hyperf servers.
    server:stop          Stop hyperf servers.
```


一键生成代码 快速CRUD
```php
php bin/hyperf.php fs:model test

Model App\Model\Test was created.
success:[/demo/app/Rpc/TestServiceInterface.php]
success:[/demo/app/Service/TestService.php]
```

## 多应用
在 主项目外生成

设计之初就是为了多应用多功能模块

因为`Hyperf/Utils/CodeGen`需要读取`composer-psr4`所以需要添加生成的路径
```json
"autoload": {
    "psr-4": {
        "App\\": "src/", // 默认情况
        "Demo\\Plugin\\Test": "plugin/demo/test/src/" // 自定义插件/组件
    }
}
```
添加之后需要更新一下`composer`缓存
```php
composer dump-autoload -o
```
生成
```php
php bin/hyperf fs:model test --path plugin/demo/test/src
```

生成的TestService可方便操作数据免去大部分CRUD时间

> 生成Service时 `--cache false` 可不启用缓存(默认启用)

缓存会请求后生成, 更新/删除 删除缓存(默认9000TTL,不会一直占用资源)

## 技巧
期待你们发现其他小技巧欢迎Pr

1. `SelectRaw`
```php
'selectRaw' => 'sum(`id`) as sum'
```
2. `闭包Where查询`
```php
[function ($q) {
    $q->where('id','=',1)->orWhere('id','=',2);
}]
```
# License
Apache License Version 2.0, http://www.apache.org/licenses/