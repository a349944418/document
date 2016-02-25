# OpenCart二次开发

### 目录结构

* system 系统核心目录
* catalog 前台目录
    * model 数据库操作文件夹（M 层）
    * controller 控制器文件夹（C 层）
    * language 语言包文件夹（L 层）
    * view 模板文件夹（V 层）
* admin 后台目录（同上）
* image 系统图片资源目录

### 加载流程
在网页加载过程中，入口文件中首先引用了startup.php
``` php
    require_once(DIR_SYSTEM . 'startup.php');
```

打开此文件**（startup.php）**查看其内容：

1. 对系统环境进行检测
2. 注册自动加载函数(library, vender函数)
3. 引用核心的类库(controller, action, event, loader, registry....)

回到**根目录index.php** 文件

1. 实例化startup.php文件中引入的核心类（包括autoload），放入全局对象registry中
2. 根据当前请求的url，分析router参数，实例化对应前台目录控制器（catalog／controller）中的对应类，执行对应方法
    * 如不存在router参数，进入首页
    * 如该类或方法不存在，执行error/not_found
    
3. 进入C层，进入处理，生成返回内容，并输出
