# 循环　　

除了前面介绍的条件语句，AWK 还提供了循环语句。该语句的作用就是当条件为真时重复执行一系列的命令。本章将讲解 AWK 中循环语句的使用方法。

## For 

For 循环的语法如下：  

```
for (initialisation; condition; increment/decrement)
    action
```  

for 语句首先执行初始化动作( initialisation )，然后再检查条件( condition )。如果条件为真，则执行动作( action )，然后执行递增( increment )或者递减( decrement )操作。只要条件为真循环就会一直执行。每次循环结束都会进条件检查，若条件为假则结束　循环。下面的例子使用 For 循环输出数字 1 至 5：  

```
[jerry]$ awk 'BEGIN { for (i = 1; i <= 5; ++i) print i }'
```   

执行上面的命令可以得到如下结果：  

```
1
2
3
4
5
```  

## While

While 循环会一直执行动作直到逻辑条件为假为止。其使用方法如下：  

```
while (condition)
    action
```  

AWK 首先检查条件是否为真，若条件为真则执行动作。此过程一直重复直到条件为假时，则停止。下面是使用 While 循环输出数字 1 到 5 的例子：  

```
[jerry]$ awk 'BEGIN {i = 1; while (i < 6) { print i; ++i } }'
```   

执行上面的命令可以得到如下的结果：  

```
1
2
3
4
5
```  

## Do-While 

Do-While 循环与 While 循环相似，但是 Do-While 的条件测试放到了循环的尾部。下面是 do-while 的语法：  

```
do
    action
while (condition)
```  

在 do-while 循环中，无论条件是真是假，循环语句至少执行一次，执行后检查条件真假。下面是使用 do-While 循环输出数字 1 到 5 的例子：  

```
[jerry]$ awk 'BEGIN {i = 1; do { print i; ++i } while (i < 6) }'
```   

执行上面的命令可以得到如下的结果：  

```
1
2
3
4
5
``` 

## Break

顾名思义，break 用以结束循环过程。在下面的示例子中，当计算的和大于 50 的时候使用 break 结束循环过程：  

```
[jerry]$ awk 'BEGIN {sum = 0; for (i = 0; i < 20; ++i) { sum += i; if (sum > 50) break; else print "Sum =", sum } }'
```   

执行上面的命令可以得到如下的结果：  

```
Sum = 0
Sum = 1
Sum = 3
Sum = 6
Sum = 10
Sum = 15
Sum = 21
Sum = 28
Sum = 36
Sum = 45
``` 

## Continue

Continue 语句用于在循环体内部结束本次循环，从而直接进入下一次循环迭代。当我们希望跳过循环中某处数据处理时就会用到 Continue。下面的例子输出 1 到 20 之间的偶数：  

```
[jerry]$ awk 'BEGIN {for (i = 1; i <= 20; ++i) {if (i % 2 == 0) print i ; else continue} }'
```   

执行上面的命令可以得到如下的结果：  

```
2
4
6
8
10
12
14
16
18
20
``` 

## Exit

Exit 用于结束脚本程序的执行。该函数接受一个整数作为参数表示 AWK 进程结束状态。 如果没有提供该参数，其默认状态为 0 。下面例子中当和大于 50 时结束 AWK 程序。  

```
[jerry]$ awk 'BEGIN {sum = 0; for (i = 0; i < 20; ++i) { sum += i; if (sum > 50) exit(10); else print "Sum =", sum } }'
```   

执行上面的命令可以得到如下的结果：  

```
Sum = 0
Sum = 1
Sum = 3
Sum = 6
Sum = 10
Sum = 15
Sum = 21
Sum = 28
Sum = 36
Sum = 45
```  

让我们检查一下脚本执行后的返回状态：  

```
[jerry]$ echo $?
```   

执行上面的命令可以得到如下的结果：  

```
19
```
