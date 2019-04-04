### composer开发文档

#### 简介
composer相关介绍可参考:
1. [月报:指尖上的交响乐 - PHP包管理使用](http://wiki.skyunion.net/index.php/%E6%9C%88%E6%8A%A5:%E6%8C%87%E5%B0%96%E4%B8%8A%E7%9A%84%E4%BA%A4%E5%93%8D%E4%B9%90_-_PHP%E5%8C%85%E7%AE%A1%E7%90%86%E4%BD%BF%E7%94%A8#.E5.88.B6.E4.BD.9C.E4.BE.9D.E8.B5.96.2F.E5.8C.85.EF.BC.88library.EF.BC.89)
2. [composer中文学习](https://docs.phpcomposer.com/00-intro.html)

#### 开发示例流程

##### 创建目录名称

```
mkdir composer-dev-demo
cd composer-dev-demo
```
#### 初始化扩展包
```
composer init

---

This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>) [brightwang/composer-dev-demo]: igg/composer-dev-demo
Description []: 测试
Author [brightwang <brightwang1984@gmail.com>, n to skip]: n
Minimum Stability []:
Package Type (e.g. library, project, metapackage, composer-plugin) []: library
License []:

Define your dependencies.

Would you like to define your dev dependencies (require-dev) interactively [yes]? no

{
    "name": "igg/composer-dev-demo",
    "description": "测试",
    "type": "library",
    "require": {}
}

Do you confirm generation [yes]? yes

```
经过上述命令生成composer.json文件

##### 修改composer.json增加自动加载规范(命名空间和目录映射关系)和环境要求

加入autoload

```
{
    "name": "igg/composer-dev-demo",
    "description": "测试",
    "type": "library",
    "autoload": {
        "psr-4": {
            "Tools\\": "src/"
        }
    },
    "require": {}
}
```
autoload:包的加载方式，具体加载方式可以参考composer中文网说明。这里使用的是psr-4标准加载方式。composer会在src目录下根据命名空间执行自动加载。


##### 新建src目录。添加Add.php文件


```
namespace Tools;

Class Add
{
    public function sum($a,$b)
    {
        return $a + $b;
    }
}
```


文件目录

```
├── composer.json
└── src
    └── Add.php
```
##### 提交至https://packagist.skyunion.net
1. 执行后可以提交入git中
2. 在packagist中提交包文件
![image](http://wiki.skyunion.net/images/thumb/e/ef/Packagist%E6%B7%BB%E5%8A%A0%402x.png/800px-Packagist%E6%B7%BB%E5%8A%A0%402x.png)
3. 提交后信息显示
![image](http://wiki.skyunion.net/images/thumb/6/67/%E6%B7%BB%E5%8A%A0%E5%8C%85%402x.png/800px-%E6%B7%BB%E5%8A%A0%E5%8C%85%402x.png)

##### tag相关操作

```
git tag v1.0
git push origin --tags
```
更新packagist查看
![image](http://wiki.skyunion.net/images/thumb/a/ab/Tag%402x.png/800px-Tag%402x.png)

##### 安装使用测试

```
composer require igg/composer-dev-demo
```

```
require 'vendor/autoload.php';
use Tools\Add;

$add=new Add();
var_dump($add->sum(1,2));
```







