 

这是在github page上的第一篇博客,记录了三个点:

- 了解markdown
- 了解Sublime Text上的Markdown插件
- 使用Jekyll生成文章并发布到github page上.


### 了解markdown
 

[github官方出品的Markdown guide](https://guides.github.com/features/mastering-markdown)详细介绍了Markdown,另外标准的Markdown和GitHub Flavored Markdown是有一定区别的.

假如要了解Markdown的``语法``,参考[Markdown Here Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet),需要的时候查阅即可.

### 了解Sublime Text上的Markdown插件
 
自己使用ST3作为日常的编辑器,Markdown Preview和MarkdownEditing是两个不错的插件.

[Markdown Preview](https://github.com/revolunet/sublimetext-markdown-preview)

常用的配置:
 
```
{   
    "browser": "C:\\Google\\Chrome\\Application\\chrome.exe",
    "parser": "markdown",
    "build_action": "browser",  
}
```
可以选择各类markdown解析器
通过`CTRL+B`构建HTML文件,并在浏览器中查看.


**[MarkdownEditing](https://github.com/ttscoff/MarkdownEditing)**

这个插件提供了多套颜色主题,另外支持很多快捷键,可以方便的编辑,支持Standard Markdown, GitHub flavored Markdown, MultiMarkdown,默认是GFM,可以通过View > Syntax >MarkdownEditing进行修改.

快捷键不要死记硬背,查看`key`配置,`windows`常用的包括`ctrl+super+v`(插入连接),
`super+shift+k`(插入图像),`ctrl+n`(插入Headers),

### 使用Jekyll生成文章并发布到github page上


#### [GitHub Pages](https://guides.github.com/features/pages)
GitHub Pages相当于一个静态网页的托管网站,支持自定义域名,创建很简单,只要创建名为**用户名.github.io**的仓库,然后就可访问.


#### Jekyll
Jekyll is an open source tool that builds a static web site from dynamic components like templates, liquid code, markdown, etc.

Jekyll包含二部分:

- 解析器:通过Lquid,YAML,模版解析为HTML文件,相当于解析引擎.GitHub Pages就相当于一个Jekyll解析引擎.
- 构建工具:可以通过解析器生成HTML文件.

在Linxu上没有安装成功Jekyll,所以对于一些命令行没有试验,**另外Jekyll应该包含了一些模版的CSS定义**.
考虑到GitHub Pages也能解析Jekyll,所以只要手动配置并上传到GitHub Pages,就能够浏览自己的博客了.

注意点:

- Jekyll 本身只是HTML构建,HTML的呈现需要CSS的渲染,假如对HTML和CSS不精通,可才采用Bootstrap.
- Jekyll的语法设计很精巧,不过要完全精通还是需要掌握其规则.
- GitHub Pages 目前支持[Jekyll 3.1](https://github.com/blog/2172-github-pages-now-runs-jekyll-3-1),采用**kramdown** Markdown engine
- 后期还是需要在Linux上安装Jekyll,了解在本地的构建和发布.
- ST3 MarkdownEditing的解析引擎可能和GitHub Pages的kramdown引擎不一样,所以在ST3上看到的效果也许和GitHub Page不一样


#### [Jekyll Bootstrap](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)
Jekyll Bootstrap是一个基于Bootstrap的Jekyll风格的模版,我的
[GitHub Pages](http://github.newyingyong.cn)就是基于该模版创建而来的,稍微修改下就能浏览.
