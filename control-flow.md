#AWK——控制流　　

与其实的编程语言一样，AWK 同样提供了条件语句控制程序的执行流程。这一章中我们会介绍 AWK 中条件语句的使用方法。

##IF 语句

条件语句测试条件然后根据条件选择执行相应的动作。下面是条件语句的语法：  

```
if (condition)
    action
```  

也可以使用花括号来执行一组操作：   

```
if (condition)
{
    action-1
    action-1
    .
    .
    action-n
}
```  

下面的例子判断数字是奇数还是偶数：  

```
[jerry]$ awk 'BEGIN {num = 10; if (num % 2 == 0) printf "%d is even number.\n", num }'
```  

执行上面的命令可以得到如下的结果：   

```
10 is even number.
```  

##IF - ELSE 语句

if-else语句中允许在条件为假时执行另外一组的动作。下面为 if-else 的语法格式：  

```
if (condition)
    action-1
else
    action-2
```  

其中，条件为真时执行 action-1，条件为假时执行 action-2。下面是使用该语句判断数字是否为偶数的例子：  

```
[jerry]$ awk 'BEGIN {num = 11; if (num % 2 == 0) printf "%d is even number.\n", num; else printf "%d is odd number.\n", num }'
```  

执行上面的操作可以得到如下的结果：   

```
11 is odd number.
```  

##if-else-if 梯

我们可以很轻松地使用多个 if-else 语句构造 if-else-if 梯从而实现多个条件的判断。示例如下：  

```
[jerry]$ awk 'BEGIN {
a=30;
if (a==10)
  print "a = 10";
else if (a == 20)
  print "a = 20";
else if (a == 30)
  print "a = 30";
}'
```  

执行上面的命令可以得到如下的结果：   

```
a = 30
```  

