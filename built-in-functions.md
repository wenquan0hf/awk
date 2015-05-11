# 内置函数  

AWK 为程序开发者提供了丰富的内置函数。这一章节会讲解 AWK 提供的算术函数、字符串操作函数、时间操作相关的函数、位操作函数以及其它各种各样的函数。  

## 算术函数

AWK  提供了如下的内置算术运算函数：  

### atan2(y,x)  

该函数返回正切值 y/x 的角度值，角度以弧度为单位。示例如下：  

```
[jerry]$ awk 'BEGIN {
  PI = 3.14159265
  x = -10
  y = 10
  result = atan2 (y,x) * 180 / PI;

  printf "The arc tangent for (x=%f, y=%f) is %f degrees\n", x, y, result
}'
```  

执行上面的命令得到如下结果：  

```
The arc tangent for (x=-10.000000, y=10.000000) is 135.000000 degrees
```  

### cos(expr) 

该函数返回 expr 的余弦值， 输入参数以弧度为单位。示例如下：  

```
[jerry]$ awk 'BEGIN {
  PI = 3.14159265
  param = 60
  result = cos(param * PI / 180.0);

  printf "The cosine of %f degrees is %f.\n", param, result
}'
```

执行上面的命令得到如下的结果：  

```
The cosine of 60.000000 degrees is 0.500000.
```  

### exp(expr)

此函数返回自然数 e 的 expr 次幂。

```
[jerry]$ awk 'BEGIN {
  param = 5
  result = exp(param);

  printf "The exponential value of %f is %f.\n", param, result
}'
```

执行上面的命令可以得到如下的结果：  

```
The exponential value of 5.000000 is 148.413159.
```  

### int(expr)  

此函数返回数值 expr 的整数部分。示例如下：  

```
[jerry]$ awk 'BEGIN {
  param = 5.12345
  result = int(param)

  print "Truncated value =", result
}'
```

执行上面的命令可以得到如下的结果：  

```
Truncated value = 5
```  

### log(expr)  

此函数计算 expr 自然对数。 

```
[jerry]$ awk 'BEGIN {
  param = 5.5
  result = log (param)

  printf "log(%f) = %f\n", param, result
}'
```

执行上面的命令可以得到如下的结果：  

```
log(5.500000) = 1.704748
```  

### rand

rand 函数返回一个大于等于 0 小于 1 的随机数 N（0<= N < 1）。示例如下：  

```
[jerry]$ awk 'BEGIN {
  print "Random num1 =" , rand()
  print "Random num2 =" , rand()
  print "Random num3 =" , rand()
}'
```

执行上面的命令可以得到如下的结果：  

```
Random num1 = 0.237788
Random num2 = 0.291066
Random num3 = 0.845814
```   

### sin(expr)  

正弦函数返回角度 expr  的正弦值，角度以弧度为单位。示例如下：  

```
[jerry]$ awk 'BEGIN {
  PI = 3.14159265
  param = 30.0
  result = sin(param * PI /180)

  printf "The sine of %f degrees is %f.\n", param, result
}'
```

执行上面的命令可以得到如下的结果：  

```
The sine of 30.000000 degrees is 0.500000.
```   

### sqrt(expr)  

此函数计算 expr 的平方根。

```
[jerry]$ awk 'BEGIN {
  param = 1024.0
  result = sqrt(param)

  printf "sqrt(%f) = %f\n", param, result
}'
```

执行上面的命令可以得到如下的结果：  

```
sqrt(1024.000000) = 32.000000
```   

### srand([expr])  

此函数使用种子值生成随机数，数值　expr 作为随机数生成器的种子值。如果没有指定 expr 的值则函数默认使用当前系统时间作为种子值。  

```
[jerry]$ awk 'BEGIN {
  param = 10

  printf "srand() = %d\n", srand()
  printf "srand(%d) = %d\n", param, srand(param)
}'
```

执行上面的命令得到如下的结果：  

```
srand() = 1
srand(10) = 1417959587
``` 

## 字符串函数  

AWK 提供了下面所示的字符串操作函数：  

### asort(arr,[, d [,how] ])

asort 函数使用 GAWK 值比较的一般规则排序 arr 中的内容，然后用以 1 开始的有序整数替换排序内容的索引。  

```
[jerry]$ awk 'BEGIN {
	arr[0] = "Three"
	arr[1] = "One"
	arr[2] = "Two"

	print "Array elements before sorting:"
	for (i in arr) {
		print arr[i]
	}

	asort(arr)

	print "Array elements after sorting:"
	for (i in arr) {
		print arr[i]
	}
}'
```  

执行上面的命令可以得到如下的结果：  

```
Array elements before sorting:
Three
One
Two
Array elements after sorting:
One
Three
Two
```  

### asorti(arr,[, d [,how] ])  

asorti 函数的行为与 asort 函数的行为很相似，二者的差别在于  aosrt 对数组的值排序，而 asorti 对数组的索引排序。  

```
[jerry]$ awk 'BEGIN {
	arr["Two"] = 1
	arr["One"] = 2
	arr["Three"] = 3

	asorti(arr)

	print "Array indices after sorting:"
	for (i in arr) {
		print arr[i]
	}
}'
```

执行上面的命令可以得到如下的结果：  

```
Array indices after sorting:
One
Three
Two
```  

### gsub(regx,sub, string)  

gsub 是全局替换( global substitution )的缩写。它将出现的子串（sub）替换为 regx。第三个参数 string 是可选的，默认值为 $0，表示在整个输入记录中搜索子串。  

```
[jerry]$ awk 'BEGIN {
	str = "Hello, World"

	print "String before replacement = " str

	gsub("World", "Jerry", str)

	print "String after replacement = " str
}'
```

执行上面的命令可以得到如下的结果：  

```
String before replacement = Hello, World
String after replacement = Hello, Jerry
```  

### index(str,sub)  

index 函数用于检测字符串 sub 是否是 str 的子串。如果 sub 是 str 的子串，则返回子串 sub 在字符串 str 的开始位置；若不是其子串，则返回 0。str 的字符位置索引从 1 开始计数。  

```
[jerry]$ awk 'BEGIN {
	str = "One Two Three"
	subs = "Two"

	ret = index(str, subs)

	printf "Substring \"%s\" found at %d location.\n", subs, ret
}'
```

执行上面的命令可以得到如下的结果：  

```
Substring "Two" found at 5 location.
```  

### length(str)  

length 函数返回字符串的长度。  

```
[jerry]$ awk 'BEGIN {
	str = "Hello, World !!!"

	print "Length = ", length(str)
}'
```

执行上面的命令可以得到如下的结果：  

```
Length = 16
``` 

### match(str, regex)  

match 返回正则表达式在字符串 str 中第一个最长匹配的位置。如果匹配失败则返回0。  

```
[jerry]$ awk 'BEGIN {
	str = "One Two Three"
	subs = "Two"

	ret = match(str, subs)

	printf "Substring \"%s\" found at %d location.\n", subs, ret
}'
```

执行上面的命令可以得到如下的结果：  

```
Substring "Two" found at 5 location.
``` 

### split(str, arr,regex)

split 函数使用正则表达式 regex 分割字符串 str。分割后的所有结果存储在数组 arr 中。如果没有指定 regex 则使用 FS 切分。  

```
[jerry]$ awk 'BEGIN {
	str = "One,Two,Three,Four"

	split(str, arr, ",")

	print "Array contains following values"

	for (i in arr) {
		print arr[i]
	}
}'
```

执行上面的命令可以得到如下的结果：  

```
Array contains following values
One
Two
Three
Four
```  

### sprintf(format,expr-list)  

sprintf 函数按指定的格式（ format ）将参数列表 expr-list 构造成字符串然后返回。  

```
[jerry]$ awk 'BEGIN {
	str = sprintf("%s", "Hello, World !!!")

	print str
}'
```

执行上面的命令可以得到如下的结果：  

```
Hello, World !!!
```  

### strtonum(str)  

strtonum 将字符串 str 转换为数值。 如果字符串以 0 开始，则将其当作十进制数；如果字符串以 0x 或 0X 开始，则将其当作十六进制数；否则，将其当作浮点数。  

```
[jerry]$ awk 'BEGIN {
	print "Decimal num = " strtonum("123")
	print "Octal num = " strtonum("0123")
	print "Hexadecimal num = " strtonum("0x123")
}'
```

执行上面的命令可以得到如下的结果：  

```
Decimal num = 123
Octal num = 83
Hexadecimal num = 291
```  

### sub(regex,sub,string)  

sub 函数执行一次子串替换。它将第一次出现的子串用 regex  替换。第三个参数是可选的，默认为 $0。  

```
[jerry]$ awk 'BEGIN {
	str = "Hello, World"

	print "String before replacement = " str

	sub("World", "Jerry", str)

	print "String after replacement = " str
}'
```  

执行上面的命令可以得到如下的结果：  

```
String before replacement = Hello, World
String after replacement = Hello, Jerry
```  

### substr(str, start, l)  

substr 函数返回 str 字符串中从第 start 个字符开始长度为 l 的子串。如果没有指定 l 的值，返回 str 从第 start 个字符开始的后缀子串。 

```
[jerry]$ awk 'BEGIN {
	str = "Hello, World !!!"
	subs = substr(str, 1, 5)

	print "Substring = " subs
}'
```  

执行上面的命令可以得到如下的结果：  

```
Substring = Hello
```  

### tolower(str)  

此函数将字符串 str 中所有大写字母转换为小写字母然后返回。注意，字符串 str 本身并不被改变。    

```
[jerry]$ awk 'BEGIN {
	str = "HELLO, WORLD !!!"

	print "Lowercase string = " tolower(str)
}'
```

执行上面的命令可以得到如下的结果：  

```
Lowercase string = hello, world !!!
``` 
 
### toupper(str)  

此函数将字符串 str 中所有小写字母转换为大写字母然后返回。注意，字符串 str 本身不被改变。    

```
[jerry]$ awk 'BEGIN {
	str = "hello, world !!!"

	print "Uppercase string = " toupper(str)
}'
```  

执行上面命令可以得到如下的结果：  

```
Uppercase string = HELLO, WORLD !!!
```  

## 时间函数

AWK 提供了如下的内置时间函数：  

### systime  

此函数返回从 Epoch 以来到当前时间的秒数（在 POSIX 系统上，Epoch 为1970-01-01 00:00:00 UTC）。  

```
[jerry]$ awk 'BEGIN {
	print "Number of seconds since the Epoch = " systime()
}'
```  

执行上面的命令可以得到如下的结果：  

```
Number of seconds since the Epoch = 1418574432
``` 

### mktime(dataspec)  

此函数将字符串 dataspec 转换为与 systime 返回值相似的时间戳。 dataspec 字符串的格式为 YYYY MM DD HH MM SS。

```
[jerry]$ awk 'BEGIN {
	print "Number of seconds since the Epoch = " mktime("2014 12 14 30 20 10")
}'
```

执行上面的命令可以得到如下的结果：  

```
Number of seconds since the Epoch = 1418604610
```  

### strftime([format [, timestamp[, utc-flag]]])  

此函数根据 format 指定的格式将时间戳 timestamp 格式化。  

```
[jerry]$ awk 'BEGIN {
	print strftime("Time = %m/%d/%Y %H:%M:%S", systime())
}'
```

执行上面的的命令可以得到如下的结果：  

```
Time = 12/14/2014 22:08:42
```  

下面是 AWK 支持的不同的日期格式说明：  
| 日期格式规范    | 描述           |   
|:-------------|:-------------| 
| ％a           | 星期缩写(Mon-Sun)。 |  
| %A            | 星期全称（Monday-Sunday）。      |
| %b            | 月份缩写（Jan）。     |  
| ％B           | 月份全称（January）。 |  
| %c            | 本地日期与时间。      |  
| %C            | 年份中的世纪部分，其值为年份整除100。  |  
| %d	        |十进制日期(01-31)   |  
|%D	            |等价于 %m/%d/%y.|  
|%e	            |日期，如果只有一位数字则用空格补齐|  
|%F	            |等价于 %Y-%m-%d，这也是 ISO 8601 标准日期格式。|  
|%g	            |ISO8610 标准周所在的年份模除 100（00-99)。比如，1993 年 1 月 1 日属于 1992 年的第 53 周。所以，虽然它是 1993 年第 1 天，但是其　ISO8601 标准周所在年份却是 1992。同样，尽管 1973 年 12 月 31 日属于 1973 年但是它却属于 1994 年的第一周。所以 1973 年 12 月 31 日的 ISO8610　标准周所在的年是 1974 而不是 1973。|  
|%G	            |ISO 标准周所在年份的全称。|  
|%h          	|等价于 %b.|  
|%H             |用十进制表示的 24 小时格式的小时(00-23)|  
|%I             |用十进制表示的 12 小时格式的小时（00-12）|  
|%j             |一年中的第几天（001-366）|
|%m             |月份（01-12）|  
|%M             |分钟数（00-59)|  
|%n             |换行符 (ASCII LF)|  
|%p             |十二进制表示法（AM/PM）|  
|%r             |十二进制表示法的时间（等价于 %I:%M:%S %p）。|  
|%R             |等价于 %H:%M。|  
|%S             |时间的秒数值（00-60）|  
|%t             |制表符 (tab)|  
|%T             |等价于 %H:%M:%S。|  
|%u             |以数字表示的星期(1-7),1 表示星期一。|  
|%U             |一年中的第几个星期（第一个星期天作为第一周的开始），00-53|  
|%V             |一年中的第几个星期（第一个星期一作为第一周的开始），01-53。|  
|%w             |以数字表示的星期（0-6），0表示星期日 。|  
|%W             |十进制表示的一年中的第几个星期（第一个星期一作为第一周的开始），00-53。|  
|%x             |本地日期表示|  
|%X             |本地时间表示|  
|%y             |年份模除 100。|  
|%Y             |十进制表示的完整年份。|  
|%z             |时区，表示格式为+HHMM（例如，格式要求生成的 RFC 822或者 RFC 1036 时间头）|  
|%Z             |时区名称或缩写，如果时区待定则无输出。|

## 位操作函数

AWK 提供了如下的内置的位操作函数：  

### and

执行位与操作。  

```
[jerry]$ awk 'BEGIN {
	num1 = 10
	num2 = 6

	printf "(%d AND %d) = %d\n", num1, num2, and(num1, num2)
}'
```  

执行上面的命令可以得到如下的结果：  

```
(10 AND 6) = 2
```  
  
### compl  

按位求补。 

```
[jerry]$ awk 'BEGIN {
	num1 = 10

	printf "compl(%d) = %d\n", num1, compl(num1)
}'
```  

执行上面的命令可以得到如下的结果：  

```
compl(10) = 9007199254740981
```  

### lshift  

左移位操作。  

```
[jerry]$ awk 'BEGIN {
	num1 = 10

	printf "lshift(%d) by 1 = %d\n", num1, lshift(num1, 1)
}'
```  

执行上面的命令可以得到如下的结果：   
 
```
lshift(10) by 1 = 20
```  
  
### rshift  

向右移位操作。 

```
[jerry]$ awk 'BEGIN {
	num1 = 10

	printf "rshift(%d) by 1 = %d\n", num1, rshift(num1, 1)
}'
```  

执行上面的命令可以得到如下的结果：  

```
rshift(10) by 1 = 5
```  

### or

按位或操作。  

```
[jerry]$ awk 'BEGIN {
	num1 = 10
	num2 = 6

	printf "(%d OR %d) = %d\n", num1, num2, or(num1, num2)
}'
```

执行上面的命令可以得到如下的结果：  

```
(10 OR 6) = 14
```  

### xor  

按位异或操作。  

```
[jerry]$ awk 'BEGIN {
	num1 = 10
	num2 = 6

	printf "(%d XOR %d) = %d\n", num1, num2, xor(num1, num2)
}'
```  

执行上面的命令可以得到如下的结果：  

```
(10 bitwise xor 6) = 12
```  
  
## 其它函数  

其它函数中主要包括:  

### close(expr)  

关闭管道的文件。  

```
[jerry]$ awk 'BEGIN {
	cmd = "tr [a-z] [A-Z]"
	print "hello, world !!!" |& cmd
	close(cmd, "to")
	cmd |& getline out
	print out;
	close(cmd);
}'
```  

执行上面的命令可以得到如下的结果：  

```
HELLO, WORLD !!!
```  

脚本的内容看上去很神秘吗？让我们来揭开它神秘的面纱。

- 第一条语句 cmd = "tr [a-z] [A-Z]" 在　AWK 中建立了一个双向的通信通道。
- 第二条语句 print 为 tr 命令提供输入。&| 表示双向通信。  
- 第三条语句 close(cmd, "to") 完成执行后关闭 to 进程。  
- 第四条语句 cmd |& getline out 使用 getline 函数将输出存储到 out 变量中。  
- 接下来的输出语句打印输出的内容，最后 close 函数关闭 cmd。

### delete  

delete 被用于从数组中删除元素。下面的例子演示了如何使用 delete：  

```
[jerry]$ awk 'BEGIN {
	arr[0] = "One"
	arr[1] = "Two"
	arr[2] = "Three"
	arr[3] = "Four"

	print "Array elements before delete operation:"
	for (i in arr) {
		print arr[i]
	}

	delete arr[0]
	delete arr[1]

	print "Array elements after delete operation:"
	for (i in arr) {
		print arr[i]
	}
}'
```  

执行上面的命令可以得到如下的结果：  

```
Array elements before delete operation:
One
Two
Three
Four

Array elements after delete operation:
Three
Four
```  

### exit  

该函数终止脚本执行。它可以接受可选的参数 expr 传递 AWK  返回状态。示例如下：  

```
[jerry]$ awk 'BEGIN {
	print "Hello, World !!!"

	exit 10

	print "AWK never executes this statement."
}'
```  

执行上面的命令可以得到如下的结果：  

```
Hello, World !!!
```  

### flush  

flush 函数用于刷新打开文件或管道的缓冲区。 使用方法如下：  

```
fflush([output-expr])
```  

如果没有提供 output-expr，fflush 将刷新标准输出。若 output-epxr 是空字符串 ("")，fflush 将刷新所有打开的文件和管道。 

### getline  

getline 函数读入下一行。示例中使用 getline 从文件 marks.txt 中读入一行并输出：  

```
[jerry]$ awk '{getline; print $0}' marks.txt 
```  

执行上面的命令可以得到如下的结果：   

```
2)	Rahul	Maths	90
4)	Kedar	English	85
5)	Hari	History	89
```  

脚本看似工作正常，但是第一行去哪儿了呢？让我们理一下整个过程。刚启动时，AWK 从文件 marks.txt 中读入一行存储到变量 $0 中。在下一条语句中，我们使用 getline 读入下一行。 因此 AWK 读入第二行并存储到 $0 中。最后，AWK 使用 print 输出第二行的内容。这个过程一直到文件结束。  

### next  

next 停止处理当前记录，并且进入到下一条记录的处理过程。下面的例子中，当模式串匹配成功后程序并不执行任何操作：  

```
[jerry]$ awk '{if ($0 ~/Shyam/) next; print $0}' marks.txt
```  

执行上面的命令可以得到如下的结果：   

```
1)	Amit	Physics	80
2)	Rahul	Maths	90
4)	Kedar	English	85
5)	Hari	History	89
```  

### nextfile  

nextfile 停止处理当前文件，从下一个文件第一个记录开始处理。下面的的例子中，匹配成功时停止处理第一个文件转而处理第二个文件：  
首先创建两个文件。 file1.txt 内容如下:  

```
file1:str1
file1:str2
file1:str3
file1:str4
```  

文件 file2.txt 内容如下：  

```
file2:str1
file2:str2
file2:str3
file2:str4
```  

现在我们来测试  nextfile 函数。  

```
[jerry]$ awk '{ if ($0 ~ /file1:str2/) nextfile; print $0 }' file1.txt file2.txt
```  

执行上面的命令可以得到如下的结果：  

```
file1:str1
file2:str1
file2:str2
file2:str3
file2:str4
```  

### return   

return 用于从用户自定义的函数中返回值。请注意，如果没有指定返回值，那么的返回值是未定义的。下面的例子演示了 return 的使用方法：  
首先，创建文件 functions.awk，内容如下：  

```
function addition(num1, num2)
{
	result = num1 + num2

	return result
}

BEGIN {
	res = addition(10, 20)
	print "10 + 20 = " res
}
```  

执行上面的命令可以得到如下的结果：  

```
10 + 20 = 30
``` 

### system  

system 函数可以执行特定的命令然后返回其退出状态。返回值为 0 表示命令执行成功；非 0 表示命令执行失败。下面的示例中执行 Date 显示当前的系统时间，然后输出命令的返回状态：  

```
[jerry]$ awk 'BEGIN { ret = system("date"); print "Return value = " ret }'
```  

执行上面的命令可以得到如下的结果：  

```
Sun Dec 21 23:16:07 IST 2014
Return value = 0
``` 
