---
layout: post
category : lessons
tagline: ""
tags : [php,memcached]
---
{% include JB/setup %}

前一段时间在 Apache 想安装 Memcached PHP 扩展，用 `pecl install memcached`
命令安装总提示错误：
```
checking for libmemcached location... configure: error: Unable to find memcached.h under /usr/include/libmemcached
ERROR: `/var/tmp/memcached/configure --with-libmemcached-dir=/usr/include/libmemcached' failed
```

搜索了下，还是决定使用源码自己编译，具体的方法就是：

- libmemcached [release 1.0.16](https://launchpad.net/libmemcached/1.0/1.0.16) - installed from source
- php-memcached release [2.1.0](https://github.com/php-memcached-dev/php-memcached/releases/tag/r2.1.0) - installed from source

具体方法：

```
wget https://launchpad.net/libmemcached/1.0/1.0.16/+download/libmemcach
ed-1.0.16.tar.gz
tar xzvf libmemcached-1.0.16.tar.gz 
cd libmemcached-1.0.16
./configure
make
make install

wget https://github.com/php-memcached-dev/php-memcached/archive/r2.1.0.
tar.gz
tar xvf r2.1.0.tar.gz
cd php-memcached-r2.1.0/
/usr/bin/phpize
./configure
make
make install

ll /usr/lib64/php/modules/memcached.so
cat /etc/php.ini | grep php.d 
echo "extension=memcached.so" >>  /etc/php.d/memcached.ini
```
