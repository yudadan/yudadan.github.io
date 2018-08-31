---
layout: post
category : lessons
tagline: ""
tags : [php,codeigniter]
---
{% include JB/setup %}

## 辅助函数 

辅助函数主要是完成特定任务的小函数，是函数的集合，在 Codeigniter 中辅助函数没有使用 OOP 的方式编写，而是使用过程式的方式编写，辅助函数保存在 helpers 目录下，加载好后辅助函数后，可以直接使用函数进行使用。

辅助函数一般以_helper.php（比如email_helper.php）结尾，调用形式`$this->load->helper("email")`，假如辅助函数有多级子目录可以这样调用`$this->load->helper("my/email")`

扩展辅助函数很简单（或者原生的），只要文件以MY_开头即可。

## 加载器类

在 CodeIgniter 中，加载器类主要用于加载元素的，包括库（libraries），视图（view），辅助函数（helpers），文件（configs），模型（models），语言包（lang）。

举个例子，要加载 library 下的 email库，可以调用`$this->load->library('email');`，后续 email 类就可以通过 $this->email调用了。

假如一个开发者开发了一个独立的程序，则可以将所有的包拷贝到自己的目录下，比如 /application/third_party/dsf 目录下。 然后调用`$this->load->add_package_path()`函数设置第三方包目录。

## Cookie 和 Session

Cookie 和 Session 是 WEB 开发中比较常规的两个知识点:

```
$this->input->cookie(array('c1', 'c2')); //获取 Cookie

$this->load->helper("cookie");
set_cookie("ck","value",3600,"","","",false,true);

$this->load->library('session');
$array = array('ka' => 'va');
print_r($this->session->get_userdata($array));
$this->unset_userdata($array);
```

### 多环境开发

用户可以配置开发环境和测试环境，在不同的环境下，使用的配置信息可能是不一样的。
可以在 application/config/production 和 application/config/production/development 目录下添加系统的配置文件（参数可以不一致）。