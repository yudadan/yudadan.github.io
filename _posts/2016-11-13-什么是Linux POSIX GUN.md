---
layout: post
category : lessons
tagline: ""
tags : [linux]
---
{% include JB/setup %}

## GUN 工程 

- GNU 软件 是自由的软件，GNU 系统可以包括非 GNU 软件程序。
- GNU 软件 强调 Free，而非价格，GNU 软件可以自由下载，当不代表它不能售卖，出售也是自由软件发展筹集资金的重要方法。
- GNU 的目标是给用户自由，而不是仅仅成为流行。使用 copyleft 来规定 GUN 软件被转变为私有软件。Copyleft 利用著作权法，它成为一种保持软件自由的手段。
- 大多数 GNU 软件使用的 copyleft 的明确实现是 GNU （一般公众许可证），或简称 GNU GPL 。
- 自由软件基金会，为了寻求资金，一个免税的为自由软件发展的慈善团体成立了，FSF 接受捐款，但是其大部分收入常常来自销售。
-  自由软件基金会维护的 GNU 软件包，比较重要的是 C 库和外壳(shell)。GNU C 库是每个运行於 GNU/Linux 系统的程序使用来与 Linux 通信的。被大多数 GNU/Linux 系统使用的外壳程序是 BASH。
-  自由软件哲学抵制一种特定的分布广泛的商业实践，但是它不是反商业的。许多公司尽管将它们自己与「open source」发生联系，实际上它们的生意基於与自由软件合作的非自由软件。它们是私有软件公司而不是自由软件公司，其产品诱惑用户远离自由。它们称此为「增值」，反映了它们希望我们采用的价值观念：便利在自由之上。
-  GNU C 库使用一个称做 GNU 较少一般公众许可证（LGPL）的特殊种类的 copyleft，它允许私有软件可以链接到该库。对 C 库或任何库使用 LGPL，是一个策略上的事情。C 库做的是原生工作；每个私有系统或编译器都带有 C 库。因此，只将我们的 C 库给自由软件用并不会给自由软件带来任何好处 -- 这将只会阻止使用我们的库。
- GNU/Linux,表达它是 GNU 系统和以 Linux 作为内核的组合。
- 估计当今有数千万的用户使用诸如 Debian GNU/Linux 和 Red Hat Linux 的 GNU/Linux 系统。自由软件已经发展到了这样实用的优势，使得用户纯粹为了实用原因而聚集到它身边。

GUN 工程面临的挑战：
- 秘密的硬件，硬件厂商非常注意硬件规范保密，所以对于操作系统来说编写驱动将非常困难，解决的办法就是反向工程。
- 非自由库，私有软件库的程序假如流行起来，会让使用者陷入使用陷阱，比较典型的是：非自由GUI 工具箱库（Qt），另外一个是 KDE 桌面（使用了 Qt，且该桌面包含了大量自由软件）。由于 KDE 是非自由软件，GNU/Linux 系统无法使用，所以开发了 GNOME 和 Harmony。
- 软件专利，最大的威胁来自专利，比如 GUN 一直无法使用 LZW 压缩算法。
- 自由文档，自由文档和自由软件一样，需要被广泛宣传。

## Linux 和 GNU 工程

我们提到的 Linux 实际上是一个内核，内核只有作为整个系统的一个部分才有用处，Linux 是和 GNU 操作系统结合在一起使用，所以我们一般应该称为 GUN/Linux。

大部分用户没有理解 Linux内核和被称作“Linux”的整个系统的区别。

GUN 工程在开始的时候就勾画了原始提纲，GNU 是一个系统而不是一些实用程序的组合（GNU 工程的最初目标就是做一个完整系统），GUN 的创建时间远早于 Linux。

除了 GNU，还有一个独立进行的工程开发了一个自由的类似 Unix 的操作系统。这个系统被称为 BSD。它们是两套独立开发的不同的系统。今天一个免费的操作系统几乎都是采用 GNU 或 BSD 系统的一个派生版本。

今天我们的绝大多数的工作都在基于 Linux 的 GNU 系统上完成的，你在讨论到这个组合系统时，请使用 “GNU/Linux”。

## POSIX 

POSIX 是各大操作系统之间的一个接口，是一组标准，这个表示有 IEEE Computer Society 来维护器兼容性的。 POSIX 定义了应用程序接口 (API)、命令行 shellsh和工具接口。符合 POSIX 标准的软件能兼容 Unix和其他的一些操作系统

POSIX 比较流行的标准包含：

- C API
- CLI utilities：比如cd, ls, echo
- Shell language
- Environment variables
- Program exit status
- Regular expression
- Directory struture
- Filenames
- Command line utility API conventions

GUN 工程其实也有一些标准，但是他们开发的软件是被 Linux 操作系统使用的，而 POSIX 是标准，是和系统无关的。

## 什么是Linux

Linux 是一个类 Unix ，并兼容 POSIX 标准的一个操作系统模型，是一个自由软件，Linux 的主要部分是 Linux内核，The Free Software Foundation 用 GNU/Linux 去定义操作系统。

## Linux Standard Base 

LSB 是有几个 Linux 发行版组织创建的，这些组织属于the Linux Foundation to standardize the software system structure。定义的标准有标准化的文件系统等。LSB 是基于 POSIX及其他的一些标准

## Linux distribution 

Linux 发行包是一个操作系统，基于 Linux内核，另外包含大量的包管理系统。

A typical Linux distribution comprises a Linux kernel, GNU tools and libraries, additional software, documentation, a window system (the most common being the X Window System), a window manager, and a desktop environment.

参考：

- [The GNU Project](https://www.gnu.org/gnu/the-gnu-project.html)
- [Linux and the GNU System](https://www.gnu.org/gnu/linux-and-gnu.html)
- [POSIX wikipedia](https://en.wikipedia.org/wiki/POSIX)
- [What exactly is POSIX?](http://unix.stackexchange.com/questions/11983/what-exactly-is-posix)
- [什么是Linux](https://zh.wikipedia.org/wiki/Linux)
- [Linux Standard Base](https://en.wikipedia.org/wiki/Linux_Standard_Base)
- [Linux distribution](https://en.wikipedia.org/wiki/Linux_distribution)