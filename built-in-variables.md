# 内置变量 

AWK 提供了一些内置变量。 它们在你写 AWK 脚本的时候起着很重要的作用。 这一章节中将会展示如何使用这些内置变量。 

## 标准 AWK 变量 

下面将介绍标准 AWK 变量：  

### ARGC  

ARGC 表示在命令行提供的参数的个数。  

```
[jerry]$ awk 'BEGIN {print "Arguments =", ARGC}' One Two Three Four
```  
  
执行上面的命令可以得到如下的结果：  

```
Arguments = 5
```  

程序哪儿出毛病了吗？为什么只输入四个参数而 AWK 却显示输入的参数个数的五呢？ 看完下面这个例子，你就会明白的。 

### ARGV  

这个变量表示存储命令行输入参数的数组。数组的有效索引是从 0 到 ARGC-1。  

```
[jerry]$ awk 'BEGIN { for (i = 0; i < ARGC - 1; ++i)
      { printf "ARGV[%d] = %s\n", i, ARGV[i] } 
                    }' one two three four
```  

执行上面的命令可以得到如下的结果：  

```
ARGV[0] = awk
ARGV[1] = one
ARGV[2] = two
ARGV[3] = three
```  

### CONVFMT  

此变量表示数据转换为字符串的格式，其默认值为 %.6g。  

```
[jerry]$ awk 'BEGIN { print "Conversion Format =", CONVFMT }'
```  

执行上面的命令可以得到如下的结果：   

``` 
Conversion Format = %.6g 
```  

### ENVIRON  

此变量是与环境变量相关的关联数组变量。  

```
[jerry]$ awk 'BEGIN { print ENVIRON["USER"] }'
```  

执行上面的命令可以得到如下的结果： 

```
jerry
```  

可以使用 GNU/Linux 系统中的 env 命令查询其它环境变量的名字。

### FILENAME  

此变量表示当前文件名称。  

```
[jerry]$ awk 'END {print FILENAME}' marks.txt
```  

执行上面的命令可以得到如下的结果：  

```
marks.txt
```  

值得注意的是在开始块中FILENAME是未定义的。  

### FS  

此变量表示输入的数据域之间的分隔符，其默认值是空格。 你可以使用 -F 命令行选项改变它的默认值。  

```
[jerry]$ awk 'BEGIN {print "FS = " FS}' | cat -vte
```   

执行上面的命令可以得到如下的结果： 

```
FS =  $
```  

### NF  

此变量表示当前输入记录中域的数量。例如，下面这个例子只输出超过两个域的行：  

```
[jerry]$ echo -e "One Two\nOne Two Three\nOne Two Three Four" | awk 'NF > 2'
```  

执行上面的命令可以得到如下的结果： 

```
One Two Three
One Two Three Four
```  

### NR  

此变量表示当前记录的数量。（译注：该变量类似一个计数器，统计记录的数量）。下面例子会输出读入的前三行（NR<3）。  

```
[jerry]$ echo -e "One Two\nOne Two Three\nOne Two Three Four" | awk 'NR < 3'
```  

执行上面的命令可以得到如下的结果：  
```
One Two
One Two Three
```  
### FNR  

该变量与 NR 类似，不过它是相对于当前文件而言的。此变量在处理多个文件输入时有重要的作用。每当从新的文件中读入时 FNR 都会被重新设置为 0。  

### OFMT  

此变量表示数值输出的格式，它的默认值为 %.6g。  

```
[jerry]$ awk 'BEGIN {print "OFMT = " OFMT}'
```  

执行上面的命令可以得到如下的结果：  

```
OFMT = %.6g
```  

### OFS  

此变量表示输出域之间的分割符，其默认为空格。 
  
```
[jerry]$ awk 'BEGIN {print "OFS = " OFS}' | cat -vte
```  

执行上面的命令可以得到如下的结果： 

```
OFS =  $
```  

### ORS  

此变量表示输出记录（行）之间的分割符，其默认值是换行符。  

```
[jerry]$ awk 'BEGIN {print "ORS = " ORS}' | cat -vte
```  

执行上面的命令可以得到如下的结果： 

```
ORS = $
$
```  

### RLENGTH  

此变量表示 match 函数匹配的字符串长度。AWK 的 match 函数用于在输入的字符串中搜索指定字符串。  
  
```
[jerry]$ awk 'BEGIN { if (match("One Two Three", "re")) { print RLENGTH } }'
```  

执行上面的命令可以得到如下的结果： 

```
2
```  

### RS  

此变量表示输入记录的分割符，其默认值为换行符。  

```
[jerry]$ awk 'BEGIN {print "RS = " RS}' | cat -vte
```  

执行上面的命令可以得到如下的结果：  

```
RS = $
$
```   

### RSTART  

此变量表示由 match 函数匹配的字符串的第一个字符的位置。  

```
[jerry]$ awk 'BEGIN { if (match("One Two Three", "Thre")) { print RSTART } }'
```  

执行上面的命令可以得到如下的结果： 

```
9
```  

### SUBSEP  

此变量表示数组下标的分割行符，其默认值为 **\034** 。

```
[jerry]$ awk 'BEGIN { print "SUBSEP = " SUBSEP }' | cat -vte
```  

执行上面的命令可以得到如下的结果： 

```
SUBSEP = ^\$
```  

###$0  

此变量表示整个输入记录。

```
[jerry]$ awk '{print $0}' marks.txt
```  

执行上面的命令可以得到如下的结果：  

```
1)    Amit     Physics    80
2)    Rahul    Maths      90
3)    Shyam    Biology    87
4)    Kedar    English    85
5)    Hari     History    89
```  

### $n
此变量表示当前输入记录的第 n 个域，这些域之间由 FS 分割。 

```
[jerry]$ awk '{print $3 "\t" $4}' marks.txt
```   

执行上面的命令可以得到如下的结果：  

```
Physics    80
Maths      90
Biology    87
English    85
History    89
```   

## GNU AWK 特定的变量  

下面将介绍 GNU AWK 专有的变量：  
 
### ARGIND 
  
此变量表示当前文件中正在处理的 ARGV 数组的索引值。

```
[jerry]$ awk '{ print "ARGIND   = ", ARGIND; print "Filename = ", ARGV[ARGIND] }' junk1 junk2 junk3
```  

执行上面的命令可以得到如下的结果： 

```
ARGIND   =  1
Filename =  junk1
ARGIND   =  2
Filename =  junk2
ARGIND   =  3
Filename =  junk3
```  

### BINMODE  

此变量用于在非 POSIX 系统上指定 AWK 对所有文件的 I/O 都使用二进制模式。 数值1，2 或者 3 分别指定输入文件、输出文件或所有文件。 字符串值 r 或 w 分别指定输入文件或者输出文件使用二进制 I/O模式。 字符串值 rw 或 wr 指定所有文件使用二进制 I/O模式。  
  
### ERRNO  

此变量用于存储当 getline 重定向失败或者 close 函数调用失败时的失败信息。 
 
```
[jerry]$ awk 'BEGIN { ret = getline < "junk.txt"; if (ret == -1) print "Error:", ERRNO }'
```  

执行上面的命令可以得到如下的结果： 

```
Error: No such file or directory
```   

### FIELDWIDTHS  

该变量表示一个分割域之间的空格的宽度。当此变量被设置后， GAWK 将输入的域之间的宽度处理为固定宽度，而不是使用 FS 的值作为域间的分割符。  

### IGNORECASE  

当此变量被设置后，GAWK将变得大小写不敏感。下面是一个简单的例子：   

```
[jerry]$ awk 'BEGIN{IGNORECASE=1} /amit/' marks.txt
```  

执行上面的命令得到如下的结果：   

```
1)    Amit     Physics    80
```   

### LINT  

此变量提供了在 GAWK 程序中动态控制 --lint 选项的一种途径。当这个变量被设置后， GAWK 会输出 lint 警告信息。如果给此变量赋予字符值 fatal，lint 的所有警告信息将会变了致命错误信息(fatal errors)输出，这和 --lint=fatal 效果一样。 

```
[jerry]$ awk 'BEGIN {LINT=1; a}'
```  

执行上面的命令可以得到如下的结果：   

```
awk: cmd. line:1: warning: reference to uninitialized variable `a'
awk: cmd. line:1: warning: statement has no effect
```   

### PROCINFO  

这是一个关联数组变量，它保存了进程相关的信息。比如， 真正的和有效的 UID 值，进程 ID 值等等。  

```
[jerry]$ awk 'BEGIN { print PROCINFO["pid"] }'
```  

执行上面的命令可以得到如下的结果：   

```
4316
```   

### TEXTDOMAIN  

此变量表示　AWK 程序当前文本域。 它主要用寻找程序中的字符串的本地翻译，用于程序的国际化。  
   
```
[jerry]$ awk 'BEGIN { print TEXTDOMAIN }'
```  

执行上面的命令可以得到如下的结果：   

```
messages
```   

（译注：输出　message 是由于 TEXTDOMAIN 的默认值为 messages） 
上面所有的输出都是英文字符是因为本地语言环境配置为 en_IN 。





