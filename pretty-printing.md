#AWK——优雅地输出 
 
前面我们已经用过了 AWK 中的 print 函数与 printf 函数，它们将数据输出到标准输出流中。其实 printf 函数的功能远比我们前面演示的强大。这个函数是从 C 语言中借鉴来而的，主要用于生成格式化的输出。下面是 printf 的使用方法：  

```
printf fmt, expr-list
```  

其中，fmt 是字符串常量或者格式规格说明字符串，expr-list 是与格式说明相对应的参数列表。  

##转义序列  

与一般字符串一样，格式化字符串也能内嵌转义序列。 AWK 支持的转义序列如下：  

###换行符  

下面的例子中使用换行符将 Hello 与 World 分开输出到独立两行：  

```
[jerry]$ awk 'BEGIN { printf "Hello\nWorld\n" }'
```  

执行上面的命令可以得到如下的结果：  

```
Hello
World
```  

###水平制表符  

如下示例，使用制表符显示不同的域：  

```
[jerry]$ awk 'BEGIN { printf "Sr No\tName\tSub\tMarks\n" }'
```  

执行上面的命令可以得到如下的结果：  

```
Sr No    Name    Sub Marks
```   

###垂直制表符  

如下示例，使用垂直制表符输出不同域：  

```
[jerry]$ awk 'BEGIN { printf "Sr No\vName\vSub\vMarks\n" }'
```  

执行上面的命令可以得到如下的结果：  

```
Sr No
    Name
        Sub
            Marks
```   

###退格符  

下面的例子中，我们在每个域输出后都再输出退格符（最后一个域除外）。这样前三个域的每一域的最后一个字符都会被删除。比如说，Field 1 输出为 Field。因为最后一个字符被退格符删除。不过Field 4可以正常显示，因为在Field 4输出后没有输出退格符。  

```
[jerry]$ awk 'BEGIN { printf "Field 1\bField 2\bField 3\bField 4\n" }'
```  

执行上面的命令可以得到如下的结果：  

```
Field Field Field Field 4
```  

###回车  

下面的例子中，我们在每个域输出后输出一个回车符，随后输出的域会覆盖之前输出的内容。也就是说，我们只能看到最后输出的 Field 4。  

```
[jerry]$ awk 'BEGIN { printf "Field 1\rField 2\rField 3\rField 4\n" }'
```  

执行上面的命令可以得到如下的结果：  

```
Field 4
```  

###换页符  

下面的例子中每个域后输出后输出一个换页符：  

```
[jerry]$ awk 'BEGIN { printf "Sr No\fName\fSub\fMarks\n" }'
```  

执行上面的命令可以得到如下的结果：  

```
Sr No
    Name
        Sub
            Marks
```

##格式说明符  

与 C 语言一样，AWK 也定义了格式说明符。 AWK 的 printf 允许如下的格式的转换：  

###%c  

输出单个字符。如果参数是个数值，那么数值也会被当作字符然后输出。如果参数是字符串，那么只会输出字符串的第一个字符。
  
```
[jerry]$ awk 'BEGIN { printf "ASCII value 65 = character %c\n", 65 }'
```  

执行上面的命令可以得到如下的结果：  

```
ASCII value 65 = character A
```  

###%d 与 %i  

输出十进制数的整数部分。  

```
[jerry]$ awk 'BEGIN { printf "Percentags = %d\n", 80.66 }'
```  

执行上面的命令可以得到如下的结果：  

```
Percentags = 80
```  

###%e 与 %E  

以 [-]d.dddddde[+-]dd 的格式输出浮点数。  

```
[jerry]$ awk 'BEGIN { printf "Percentags = %E\n", 80.66 }'
```  

执行上面的命令可以得到如下的结果：  

```
Percentags = 8.066000e+01
```  

%E 格式使用 E 而不是 e。  

```
[jerry]$ awk 'BEGIN { printf "Percentags = %e\n", 80.66 }'
```  

执行上面的命令可以得到如下的结果：  

```
Percentags = 8.066000E+01
```  

###%f  

以 [-]ddd.dddddd 的格式输出浮点数。  

```
[jerry]$ awk 'BEGIN { printf "Percentags = %f\n", 80.66 }'
```  

执行上面的命令可以得到如下的结果：  

```
Percentags = 80.660000
```  

###%g 与 %G  

输出浮点数，使用 %e 或 %E 转换。但它们会删除那些对数值无影响的 0。

```
[jerry]$ awk 'BEGIN { printf "Percentags = %g\n", 80.66 }'
```  

执行上面的命令可以得到如下的结果：  

```
Percentags = 80.66
```  

%G 使用 %E 格式化，而不是 %e。  

```
[jerry]$ awk 'BEGIN { printf "Percentags = %e\n", 80.66 }'
```  

执行上面的命令可以得到如下的结果：  

```
Percentags = 80.66
```  

###%o  

无符号八进制输出。  

```
[jerry]$ awk 'BEGIN { printf "Octal representation of decimal number 10 = %o\n", 10}'
```  

执行上面的命令可以得到如下的结果：  

```
Octal representation of decimal number 10 = 12
```  

###%u  

无符号十进制数输出。  

```
[jerry]$ awk 'BEGIN { printf "Unsigned 10 = %u\n", 10 }'
```  

执行上面的命令可以得到如下的结果：  

```
Unsigned 10 = 10
```  

###%x 与 %X  

输出十六进制无符号数。%X 中使用大写字母，%x 使用小写字母。  

```
[jerry]$ awk 'BEGIN { printf "Hexadecimal representation of decimal number 15 = %x\n", 15}'
```  

执行上面的命令可以得到如下的结果：  

```
Hexadecimal representation of decimal number 15 = f
```  

使用 %X 的输出结果如下：  

```
[jerry]$ awk 'BEGIN { printf "Hexadecimal representation of decimal number 15 = %X\n", 15}'
```  

执行上面的命令可以得到如下的结果：  

```
Hexadecimal representation of decimal number 15 = F
```  

###%%  

输出百分号（%），不需要输入参数。  

```
[jerry]$ awk 'BEGIN { printf "Percentags = %d%%\n", 80.66 }'
```  

执行上面的命令可以得到如下的结果：  

```
Percentags = 80%
``` 

##% 的可选参数

% 可以使用如下可选参数：  

###宽度  

输出域会被填充满足宽度要求。默认情况下使用空格字符填充。但是，当标志 0 被设置后会使用 0 填充。

```
[jerry]$ awk 'BEGIN { num1 = 10; num2 = 20; printf "Num1 = %10d\nNum2 = %10d\n", num1, num2 }'
```  

执行上面的命令可以得到如下的结果：  

```
Num1 =         10
Num2 =         20
```  

###前导零

紧接在 % 后的零被当作标示，表示输出应该使用零填充而不是空格字符。请注意，只有当域的宽度比要求宽度小时该标示才会有效。示例如下：  

```
[jerry]$ awk 'BEGIN { num1 = -10; num2 = 20; printf "Num1 = %05d\nNum2 = %05d\n", num1, num2 }'
```  

执行上面的命令可以得到如下的结果：  

```
Num1 = -0010
Num2 = 00020
``` 

###左对齐  

输出域被设置为左对齐。当输出字符串字符数比指定宽度少时，你可能希望在输出它时能左对齐。比如，在右边添加空格符。在 % 之后数字之前使用减号（-）即可指定输出左对齐。下面的例子中，AWK 的输出做为 cat 的输入，在 cat 中输出行结束符号（$）。

```
[jerry]$ awk 'BEGIN { num = 10; printf "Num = %-5d\n", num }' | cat -vte
```  

执行上面的命令可以得到如下的结果：  

```
Num1 = -0010
Num2 = 00020
``` 

###符号前缀  

输出数值的符号，正号也输出。  

```
[jerry]$ awk 'BEGIN { num1 = -10; num2 = 20; printf "Num1 = %+d\nNum2 = %+d\n", num1, num2 }'
```  

执行上面的命令可以得到如下的结果：  

```
Num1 = -10
Num2 = +20
```  

###哈希（Hash） 

使用 Hash 可以为 %o 的结果前添加0，为 %x 或 %X 输出的结果前添加 0x 或 0X （结果不为零时），为 %e，%E，%f，%F添加小数点；对于 %g 或 %G，使用哈希可以其尾部的零。使用示例如下：  

```
[jerry]$ awk 'BEGIN { printf "Octal representation = %#o\nHexadecimal representaion = %#X\n", 10, 10}'
```  

执行上面的命令可以得到如下的结果：  

```
Octal representation = 012
Hexadecimal representation = 0XA
```  
