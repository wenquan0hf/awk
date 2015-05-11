# 基本语法  

AWK 使用起来非常方便。我们可以直接通过命令行的方式为 AWK 程序提供 AWK 命令，也可以使用包括 AWK 命令的脚本文件。这篇教程将使用合适的例子分别介绍这两种使用 AWK 的方法:    

## AWK 命令行

如下所示，在命令行中，我们可以使用如下的格式调用 AWK 命令，其中 AWK 命令由单引号括起来：  

```
awk [options] file ...
```  

### 例子  

假设我们有一个名为**marks.txt**的文件需要处理，文件中的内容如下：  
  
```
1)    Amit     Physics    80
2)    Rahul    Maths      90
3)    Shyam    Biology    87
4)    Kedar    English    85
5)    Hari     History    89
```  

我们可以按如下方式使用 AWK 命令输出整个文件中的内容：  

```
[jerry]$ awk '{print}' marks.txt 
```  

执行上面的命令可以得到如下的结果： 
 
```
1)    Amit     Physics    80   
2)    Rahul    Maths      90
3)    Shyam    Biology    87
4)    Kedar    English    85
5)    Hari     History    89  
```  

## AWK 程序文件  

接下来讲解的是另外一种提供 AWK 命令的方式——通过脚本文件提供： 
 
```
awk [option] -f file ....
```

首先，创建一个文本文件 **command.awk**，在文件中输入如下 AWK 命令：  

```
{print}
```  

现在，我们可以调用 AWK 从文本文件中读入命令并执行。这里，我们实现了与上面例子相同的效果：  

```
[jerry]$ awk -f command.awk marks.txt
```  

执行上面的命令可以得到如下的结果：  
 
```
1)    Amit     Physics    80
2)    Rahul    Maths      90
3)    Shyam    Biology    87
4)    Kedar    English    85
5)    Hari     History    89
```  

## AWK 标准选项

在命令行环境下，AWK 支持如下的标准选项： 
 
### -v 选项

这个选项可以为变量赋值。它允许在程序执行之前为变量赋值。下面是一个 -v 选项使用的示例程序：
  
```
[jerry]$ awk -v name=Jerry 'BEGIN{printf "Name = %s\n", name}'
```  

执行上面的命令可以得到如下的结果：   

```
Name = Jerry
```  

### --dump-variables[=file] 选项  

此选项会将全局变量及相应值按序输出到指定文件中。默认的输出文件名是 **awkvars.out**。  

```
[jerry]$ awk --dump-variables ''
[jerry]$ cat awkvars.out 
```  

执行上面的命令可以得到如下的结果：   

```
ARGC: 1
ARGIND: 0
ARGV: array, 1 elements
BINMODE: 0
CONVFMT: "%.6g"
ERRNO: ""
FIELDWIDTHS: ""
FILENAME: ""
FNR: 0
FPAT: "[^[:space:]]+"
FS: " "
IGNORECASE: 0
LINT: 0
NF: 0
NR: 0
OFMT: "%.6g"
OFS: " "
ORS: "\n"
RLENGTH: 0
RS: "\n"
RSTART: 0
RT: ""
SUBSEP: "\034"
TEXTDOMAIN: "messages"
```  

### --help 选项  

此选项将帮助消息转出到标准输出中。 
 
```
[jerry]$ awk --help
```  

执行上面的命令可以得到如下的结果：  

```
Usage: awk [POSIX or GNU style options] -f progfile [--] file ...
Usage: awk [POSIX or GNU style options] [--] 'program' file ...
POSIX options:		GNU long options: (standard)
	-f progfile		--file=progfile
	-F fs			--field-separator=fs
	-v var=val		--assign=var=val
Short options:		GNU long options: (extensions)
	-b			--characters-as-bytes
	-c			--traditional
	-C			--copyright
	-d[file]		--dump-variables[=file]
	-e 'program-text'	--source='program-text'
	-E file			--exec=file
	-g			--gen-pot
	-h			--help
	-L [fatal]		--lint[=fatal]
	-n			--non-decimal-data
	-N			--use-lc-numeric
	-O			--optimize
	-p[file]		--profile[=file]
	-P			--posix
	-r			--re-interval
	-S			--sandbox
	-t			--lint-old
	-V			--version
```  

### --lint[=fatal] 选项  

这个选项用于检查程序的可移植情况以及代码中的可疑部分。如果提供了参数 **fatal**，AWK 会将所有的警告信息当作错误信息处理。下面这个简单的示例说明了 lint 选项的用法：  

```
[jerry]$ awk --lint '' /bin/ls
```  

执行上面的命令可以得到如下的结果：  

```
awk: cmd. line:1: warning: empty program text on command line
awk: cmd. line:1: warning: source file does not end in newline
awk: warning: no program text at all!
```  

### --posix 选项  

这个选项会打开严格 POSIX 兼容性审查。 如此，所有共同的以及 GAWK 特定的扩展将被设置为无效。  

### --profile[=file] 选项  

这个选项会将程序文件以一种很优美的方式输出（译注：用于格式化 awk 脚本文件）。默认输出文件是 **awkprof.out**。示例如下：  

```
[jerry]$ awk --profile 'BEGIN{printf"---|Header|--\n"} {print} END{printf"---|Footer|---\n"}' marks.txt > /dev/null 
[jerry]$ cat awkprof.out
``` 

执行上面的命令可以得到如下的结果：  

```

\# gawk profile, created Sun Oct 26 19:50:48 2014

	# BEGIN block(s)

	BEGIN {
		printf "---|Header|--\n"
	}

	# Rule(s)

	{
		print $0
	}

	# END block(s)

	END {
		printf "---|Footer|---\n"
	}
``` 

### --traditional 选项  

此选项用于禁止 GAWK 相关的扩展。 
 
### --version 选项  

此选项显示 AWK 程序的版本信息。  

```
[jerry]$ awk --version
```  

上面的代码执行后，将产生下面的输出结果(译注：与具体的 AWK 版本相关)：  
 
```
GNU Awk 4.0.1
Copyright (C) 1989, 1991-2012 Free Software Foundation.
```




