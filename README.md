CodeWater
=========

面向后台与客户端接口,基于CI HMVC的PHP敏捷开发框架


#1 关于HMVC

目前的扩展方式是在 application 目录下增加 modules 目录，每个模块有自己的目录，并且模块可以有一级子目录，比如 application/modules/目录/模块名/....；
每个模块都有自己的 MVC 结构，像这样 application/modules/模块名/controllers; application/modules/模块名/models; application/modules/模块名/views

在视图中装载模块：

$this->load->module('模块名/控制器/方法');

这里也可以使用 URL 路由中的默认控制器，默认的方法是 index() 方法，和普通控制器保持一致。
如果要传递参数：

$this->load->module('模块名/控制器/方法', array('参数1', '参数2', ...));

如果需要返回模块的结果而不想输出到屏幕，可以把第 3 个参数设置为 TRUE：

$this->load->module('模块名', array('参数1', '参数2', ...), TRUE);

如果需要从 URL 访问某个模块的某个方法，URL 规则是这样的：
http://domain/index.php/module/模块名/控制器/方法

实际上 /module 后面的内容和前面传入 $this->load->module() 中的参数一致。
如果要通过 URL 传递参数，则直接加在 URL 后面：
http://domain/index.php/module/模块名/控制器/方法/参数1/参数2/..../参数n

另外，这里的 URI 可以使用路由规则，也就是说什么样的 URL 都可以，只要最后路由成符合上面的规则即可，比如要使用这样的 URL：
http://domain/index.php/m/模块名/控制器/方法

可以在 routers.php 里添加一个路由规则：

$route['m/(:any)'] = 'module/$1';

如果要在某个模块的视图里生成访问当前模块当前控制器的某方法的 URL，可以在视图里这样写：

<?php echo $this->module_url('要访问的方法名/参数1/..../参数n'); ?>

如果要生成当前模块其他控制器的方法的 URL，可以这样：

<?php echo $this->module_url('要访问的方法名/参数1/..../参数n', '控制器名'); ?>