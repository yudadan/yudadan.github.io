---
layout: post
category : lessons
tagline: ""
tags : [php]
---
{% include JB/setup %}

前几天想通过程序发送 HTML 格式的邮件，使用了[nette/mail](https://packagist.org/packages/nette/mail) 库。

其中使用的代码：

```
$mail->setHTMLBody('<b>Sample HTML</b> <img src="background.gif">');
```

文档中如此说：

>Embedded images can be inserted using $mail->addEmbeddedFile('background.gif'), but it is not necessary. Why? Because Nette Framework finds and inserts all files referenced in the HTML code automatically. This behavior can be supressed by adding FALSE as a second parameter of the setHtmlBody() method.

当时思考这 background.gif 图片类库是从哪儿读取的呢？参考了源代码，才发现 setHTMLBody 函数有第二个参数，这个参数代表 background.gif 存放的绝对路径，代码修改如下解决：

```
$mail->setHTMLBody('<b>Sample HTML</b> <img src="background.gif">','/data1/');
```