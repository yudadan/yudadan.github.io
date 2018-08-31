---
layout: post
category : lessons
tagline: ""
tags : [php]
---
{% include JB/setup %}

Codeigniter 框架没有强化异常的概念，比如 Codeigniter 框架核心的数据库操作不会返回异常的，对于数据库的查询和更新函数会通过返回 TRUE 和 FALSE 来表达操作是否成功（db_debug 这个参数假如设置为 TRUE，数据库操作遇到错误会直接返回 500 错误，现实当中不建议这样操作）。

虽然 Codeigniter 不强调异常概念，但是用户可以在二个层面使用异常，分别是在控制器和模型中进行定义，举个例子：

```
//在模型中抛出异常
public function testerror() {
    if (!$this->load->database("test")) {
        throw new Exception('db connect error');
    }
    if (!$this->db->query("select * from blog limit 1"))
        $error = $this->db->error();
        throw new Exception($error['code'] . "_" . $error['message']);
    }
}

//在控制器中捕获异常
public function testerror() {
    $this->load->model('blog_module');
    try {
        $this->blog_module->testerror();
    } catch (Exception $e) {
        echo $e->getMessage();
    }
}
```

那么有了异常，假如代码没有捕获异常，Codeigniter 会如何做？在 Codeigniter 内部，异常和错误是以同样的机制去处理的。Codeigniter 会用`set_error_handler()`和`set_exception_handler()`函数自定义异常和错误处理函数。

在自定义的函数中：
对于异常都会记录一个“error”类型的日志，同时返回一个 500 HTTP状态吗， 错误状态吗为 EXIT_ERROR；
对于错误会根据`error_reporting()`配置和当前的错误类型决定是否记录日志（假如记录也是一个“error”类型的日志）。

有兴趣的可以研究下 `system/core/Exceptions.php` 这个代码。


