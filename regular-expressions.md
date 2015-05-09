#AWK——正则表达式  

AWK 可以方便高效地处理正则表达式。大量复杂的任务都可以由极其简单的正则表达式来解决。每一个精通命令行的人都知道正则表达式真正的威力所在。  
这一章将着重讲解标准正则表达式的使用方法。 

##点（Dot）

点字符（.）可以匹配除了行结束字符的所有字符。比如下面的便子就可以匹配 fin, fun, fan 等等。    

```
[jerry]$ echo -e "cat\nbat\nfun\nfin\nfan" | awk '/f.n/'
```  

执行上面命令可以得到如下结果：

```
fun
fin
fan
```  

##行开始

行开始符(^)匹配一行的开始。下面的示例将输出所有以字符串 The 开始的行。  

```
[jerry]$ echo -e "This\nThat\nThere\nTheir\nthese" | awk '/^The/'
```  

执行上面的命令可以得到如下结果：

```
There
Their
```  

##行结束

行结束符($)匹配一行的结束。下面的例子中将输出所有以字符 n 结束的行：  

```
[jerry]$ echo -e "knife\nknow\nfun\nfin\nfan\nnine" | awk '/n$/'
```  

执行上面的命令可以得到如下结果：

```
fun
fin
fan
```   

##匹配字符集  

匹配字符集用于匹配集合（由方括号表示）中的一个字符。如下例子中，匹配 Call 与 Tall 而不会匹配 Ball。

```
[jerry]$ echo -e "Call\nTall\nBall" | awk '/[CT]all/'
```  

执行上面的命令可以得到如下结果：

```
fun
fin
fan
```   

##排除集

正则匹配时会排除集合中的字符。如下例子中只会输出 Ball。

```
[jerry]$ echo -e "Call\nTall\nBall" | awk '/[^CT]all/'
```  

执行上面的命令可以得到如下结果：

```
Ball
```  

##或

竖线(|)允许正则表达式实现逻辑或运算. 下面例子将会输出 Ball 与 Call 。 

```
[jerry]$ echo -e "Call\nTall\nBall\nSmall\nShall" | awk '/Call|Ball/'
```  

执行上面的命令可以得到如下结果：

```
Call
Ball
```  

##最多出现一次

该符号( ？)前面的字符不出现或者出现一次。如下示例匹配 Colour 与 Color。 使用 ? 使得 u 变成了可选字符 。  

```
[jerry]$ echo -e "Colour\nColor" | awk '/Colou?r/'
```  

执行上面的命令可以得到如下结果：

```
Colour
Color
```  

##出现零次或多次  

该符号(＊) 允许其前的字符出现多次或者不出现。如下示例将匹配 ca，cat, catt 等等。  

```
[jerry]$ echo -e "ca\ncat\ncatt" | awk '/cat*/'
```  

执行上面的命令可以得到如下结果：

```
ca
cat
catt
``` 

##出现一次或多次

该符号(+)使得其前的字符出现一次或者多次。下面的例子会匹配一个 2 或者多个连续的 2。  

```
[jerry]$ echo -e "111\n22\n123\n234\n456\n222"  | awk '/2+/'
```  

执行上面的命令可以得到如下结果：

```
22
123
234
222
```   

##分组

括号用于分组而字符 | 用于提供多种选择。如下的正则表达式会匹配所有包含 Apple Juice 或 Aplle Cake 的行。  

```
[jerry]$ echo -e "Apple Juice\nApple Pie\nApple Tart\nApple Cake" | awk '/Apple (Juice|Cake)/'
```  

执行上面的命令可以得到如下结果：

```
Apple Juice
Apple Cake
```  
