# 运行环境

这一章节将会讲解如何在你的 GNU/Linux 系统中如何搭建 AWK 的运行环境

## 使用包管理器安装 AWK

一般情况下，绝大多数 GNU/Linux 发行版中都默认安装了 AWK。 使用 **which** 命令可以判断你当前的系统上是否安装了 AWK。 如果没有安装，在Debian GNU/Linux 系统中你可以使用 apt 包管理工具安装 AWK。如下所示：  

```  
[jeryy]$ sudo apt-get update  
[jeryy]$ sudo apt-get install gawk  
```
  
同样地，在基于RPM的 GNU/Linux 的系统上安装 AWK 时，你可以使用 yum 包管理工具安装：  

```
[root]# yum install gawk
```  

安装过后，使用命令行命令确认 AWK 已成安装成功： 
 
```
[jerry]$ which awk
```  

执行上面的代码，如果得到如下的结果，则说明你已经成功安装 awk：  

```
/usr/bin/awk
```  

## 由源码安装

因为 GNU AWK 是 GNU 项目的一部分，所以它的源代码也是可以自由下载的。在前面我们已经看到了如何使用包管理器安装 AWK。接下来，我们将讲解如何通过源代码安装 AWK。  
下面的安装方法适用于所有的 GNU/Linux 软件，同时也适用于大部分其它自由应用程序。下面是安装的步骤：  
**step 1**——从可信的源下载源代码。可以在命令行使用 **wget** 命令下载。  

```
[jerry]$ wget http://ftp.gnu.org/gnu/gawk/gawk-4.1.1.tar.xz
```
  
**step 2**——解压并提取下载的源代码。
  
```
[jerry]$ tar xvf gawk-4.1.1.tar.xz
```  

**step 3**——切换至解压后的目录并运行 configure 命令 
 
```
[jerry]$ ./configure
```  

**step 4**——**configure** 命令成功执行后会生成一个 Makefile 文件。 接下来使用 **make** 命令编译源代码。  

```
[jerry]$ make
```  

**step 5**——你可以运行测试工具保证 build 是干净的。 这一步是可选的。  

```
[jerry]$ make check
```  

**step 6**——最后一步，安装 AWK。 安装前请确认你有超级用户的权限。  

```
[jerry]$ sudo make install
```  

通过以上六个步骤，你就成功地编译并安装了 AWK。 你可以通过如下的命令来确认 **awk** 安装成功： 
 
```
[jerry]$ which awk
```  

执行上面的命令，你将会得到如下的结果： 
 
```
/usr/bin/awk
```  
