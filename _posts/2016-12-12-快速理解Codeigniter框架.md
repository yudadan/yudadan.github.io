---
layout: post
category : lessons
tagline: ""
tags : [php,codeigniter]
---
{% include JB/setup %}
Codeigniter 框架是一个比较轻型的 PHP 框架，没有太多的约束，可以灵活的使用它，所以个人比较喜欢这个框架，只要简单遵循 MVC 规则，就可以进行开发，下面是我学习过程中的一些总结，当将来遗忘相关知识后，通过这个笔记就能快速想起。根据 20/80 原则，Codeigniter 中的应用类库建议使用其他开源的类库替代。

这个笔记分为两部分，第一部分掌握了就能快速掌握 Codeigniter 的使用，就是使用 Codeigniter 的核心即可，第二部分是 Codeigniter 的扩展部分，主要是使用它的类包，包括扩展 Codeigniter 。

## Codeigniter的MVC模型

模型-视图-控制器模型，了解这三部分和 CodeIgniter URL 基本上就可以开发了。

控制器是一个中间层，处理 HTTP 请求，连接模型和视图，处理具体的逻辑。
视图，代表网页模版。
模型，相当于数据结构，比如进行数据库的操作。

## CodeIgniter URL

CodeIgniter URL使用基于段的方法，入口文件是/index.php，该文件可以重命名为其他的名称。

`/index.php/class/function/ID`
其中class代表控制器类,function是控制器类中的方法或者函数,后面的参数是传递给控制器的参数

假如控制器包含子目录，比如访问`/index.php/blog/user/getuser/10`，则控制器目录是`application/controllers/blog/User.php`。对于大型项目来说，给控制器创建子目录比较合适。

**为了 url 友好**,可以在 url中 移除 index.php，在 apache 中可以在`.htaccess`文件中配置

```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [L]
```
 
## 控制器

A Controller is simply a class file that is named in a way that can be associated with a URI.

类文件名首字母和类定义首字母必须是大写的，定义标识符且要一一对应。

控制器必须继承之 CI_Controller 类。

The second segment of the URI determines which method in the controller gets called.

If your URI contains more than two segments they will be passed to your method as parameters.

假如在控制器中定义构造函数，必须重载父类的构造函数 `parent::__construct();`

*假如控制器有子目录，那么如何定义默认的控制器呢？该问题我没有解决方案。*

## 模型

模型被设计为和数据库操作的一个类。

模型的类文件名首字母和类定义首字母必须是大写的，定义标识符且要一一对应。

模型必须继承之 CI_Model 基类。模型保存在  application/models 目录下，也支持子目录的创建。

加载模型并使用：

```
$this->load->model('model_name');
//通过一个和类同名的对象访问模型中的方法
$this->model_name->method(); 

//可以为加载的模型赋予一个不同名字的对象
$this->load->model('blog/model_name',"alias_model");
$this->alias_model->method(); 
```

## 视图

Codeigniter 中的视图并不是模版引擎，提倡简单。视图必须由控制器调用。

视图可以存储在子目录中（application/view）。视图默认处理是将数据发送到浏览器，当然也可以将视图渲染的结果赋值给变量。

可以加载多个视图，Codeigniter 会按照加载顺序合并页面。

可以通过数组和对象像视图传递数据（在视图中，对象会转换为数组元素）。

在视图中，可以通过 PHP 的替代语法来进行循环、判断等相关逻辑的处理。

## 规划你的应用程序

假如你开放一个项目，该项目有前台(user.codeigniter.com)和后台(admin.codeigniter.com)，代码的逻辑大体是相同的，那么如何组织代码结构呢。可以采取以下的两种设计方式。

#### 第一种
根据不同的虚拟主机 rewrite 到不同的入口文件（比如分别是 user.php ，admin.php），application 下分别有二个控制器 （user.php,admin.php）。
那么如何在两个不同的入口文件中分别定义自己默认的控制器呢？
由于本质上还是同一个 application ，无法做到。
不过可以通过一个 Hack 解决该问题，修改 application/config/route.php 代码

```
if ($_SERVER['host'] == "user.codeigniter.com") {
	$route['default_controller'] = 'admin';
} else {
	$route['default_controller'] = 'admin';
}
```

#### 第二种
根据不同的虚拟主机 rewrite 到不同的入口文件（比如分别是 user.php ，admin.php），定义两个子 applcation 文件夹，目录结构如下：

```
admin.php
user.php
application_user
		config
		controllers
application_admin
		config
		controllers
```

在 user.php ，admin.php中分别通过 $application_folder 参数指定不同的  applcation 文件夹。

通过目录结构也看出，applcation 两个子文件夹是完全独立的（控制器，视图，模型代码是不一样的），代码显得非常的冗余（如何解决该问题呢？）。当然第三方类库可以放到 system目录下 。

## URI Routing

一般情况下，一个 URL 字符串和它对应的控制器中类和方法是一一对应的关系，不过可以通过 URI Routing 重写。

在`application/config/routes.php`文件配置路由规则：

```
$route['route/(:num)'] = 'blog/route/route/$1';
$route['products/([a-z]+)/(\d+)'] = 'blog/$1/regroute/id_$2';
```

## 日志处理

CodeIgniter 通过 log_message() 函数提供日志记录功能，日志类型包含“error”,"debug","info"三种类型。CodeIgniter 可以通过 log_threshold 参数是否启用日志，启用什么类型的日志。

```
$config['log_path'] = 'C:\\code\\';
$config['log_file_extension'] = 'txt';
$config['log_threshold'] = 4;  
```

**说明：** CodeIgniter 框架的日志，PHP 本身处理的日志底层使用的也是 log_message() 函数，所以记录的信息会混杂在一块。建议日志处理类使用第三方的库。

## show_error()

当程序员处理逻辑的时候遇到一个错误，程序无法正确运行，这时候可以调用该函数返回友好的页面（HTTP 状态码）或者命令行退出状态码。

该函数输出使用的错误模版是 `application/views/errors/html/error_general.php` 或者 `application/views/errors/cli/error_general.php`。

调用函数：`show_error($message, $status_code, $heading);`

假如 $status_code 小于 100，HTTP 状态码将被置为 500 。退出状态码将被置为 $status_code + EXIT__AUTO_MIN 。
如果 $status_code 大于等于 100 ，退出状态码将被置为 EXIT_ERROR 。

**注意：**调用该函数将会生成一条“error”类型的信息存储到 log_message() 定义的日志系统中。

## show_404()

假如控制器找不到，或者控制器代码显示的调用该函数，则会返回一个 404 页面。

该函数的第二个函数可以控制是否输出一条“error”类型的信息存储到 log_message() 定义的日志系统中。

同时退出状态码将设置为 EXIT_UNKNOWN_FILE 。

## 错误处理机制

CodeIgniter 中的日志处理是和“”错误“”，“异常”机制紧密关联的。具体的相关信息可以参考《Codeigniter是如何处理异常的 》这篇博文，[地址如下](http://notes.newyingyong.cn/2016/12/09/Codeigniter%E6%98%AF%E5%A6%82%E4%BD%95%E5%A4%84%E7%90%86%E5%BC%82%E5%B8%B8%E7%9A%84.html)

## WEB 输入处理

WEB 开发中，对于 GET ，POST 的使用是非常频繁的。

CodeIgniter 提供二种基本的方式保证 HTTP 输入的安全性：
- $config['allow_get_array'] 设置为 TRUE ，则会销毁全局的 GET 数组。
- 会过滤 GET/POST/COOKIE 数据的键值，只允许字母和部分数字字符。

`$something = $this->input->post('something');` （等同于 `$something = isset($_POST['something']) ? $_POST['something'] : NULL;`），假如传递的 POST 健值不存在则返回 NULL，注意和传递健对应的值为空的区别。

CodeIgniter 提供四种方法（$this->input->post()）分别获取 POST，GET，COOKIE，SERVER 数据。

通过 `$this->input->raw_input_stream;` 可以使用  php://input 流。

`$this->security->xss_clean($file, TRUE);` 进行 xss 过滤，注意开发者不建议在输入的时候进行 xss 过滤，而是在输出的时候进行 xss 过滤 （后面学习下 xss_clean 的源代码）。

## 关于国语化

语言类提供了一些方法用于获取语言文件和不同语言的文本来实现国际化。但并不是完整的国际化，只是代码中的一些常量和变量支持国家化，而视图目前是不支持国际化的（可以自己实现）。

CodeIgniter 框架自带了一套 "英语" 语言文件，保存在 system/language/english 目录下。

可以在 applcation/language 目录下创建程序需要用到的语言文件（语言文件必须以_lang.php 结尾），然后加载语言文件，最后获取相关常量和变量。

```
$this->lang->load('zdy',  "english");
echo $this->lang->line('zdy_a_ok');
```

## 自动加载

CodeIgniter 中的“Packages、Libraries、Drivers、Helper files、Config files、Language files、Models” 可以实现自动加载资源。

以语言类自动加载作为例子：

`application/config/config.php` 文件可以配置默认语言`$config['language']	= 'english';`。
然后在`application/config/autoload.php`文件中配置自动加载的具体语言文件（zdy_lang.php）`$autoload['language'] = array("zdy");` 

## 关于数据库

CodeIgniter 提供的数据库类库比较“重”，这里简单描述常用的数据库操作。

数据库的 db_debug 配置，假如该值等于 TRUE，那么数据库操作（连接，查询）一旦失败，则代码直接返回 500 HTTP 状态码错误。

由于 CodeIgniter 中的数据库操作没有“异常”的概念，所以建议在模型中判断数据库操作是否成功，假如失败则主动抛出异常。另外 error() 函数返回最近一条数据库操作的错误代码和具体信息（数据库连接错误该函数不能返回）。

数据库配置参数可以在 application/config/database.php 文件在定义，参数 $db 数组代表数据库连接信息（数组的健值代表数据库组），默认使用的数据库组定义在 $active_group 参数中。

```
$this->load->database("test");
数据库连接可以自动加载，也可以手动加载
$db = $this->load->database("test",TRUE);//假如第二个参数为 TRUE 表示返回数据库操作句柄
$db->reconnect();//可以优雅的重新连接
if (!$db->query($sql)) {
	$db->error();
}
$db->close(); 
```

## 


## 加载器类

在 CodeIgniter 中，加载器类主要用于加载元素的，包括库（libraries），视图（view），辅助函数（helpers），文件（configs），模型（models），语言包（lang）。

举个例子，要加载 library 下的 email库，可以调用`$this->load->library('email');`，后续 email 类就可以通过 $this->email调用了。

假如需要第三方库，
