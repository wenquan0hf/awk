# 输出重定向  

到目前为止我们输出的数据都是输出到标准输出流中。不过我们也可以将数据输出重定向到文件中。重定向操作往往出现在 print 或者 printf 语句中。 AWK 中的重定向方法与 shell 重定向十分相似，除了 AWK 重定向只用于 AWK 程序中外。本章节将讲述重定向的使用方法：  

## 重定向操作符  

重定向操作符的使用方法如下：
  
```
print DATA > output-file
```  

上面重定向操作将输出数据重定向到 output-file 中。如果 output-file 文件不存在，则先创建该文件。使用这种重定向方式时，数据输出前会将 output-file 文件中原有的数据删除。下面的示例将 Hello,World!!! 消息重定向输出到文件中。

先创建文件并在文件中输入一些数据。  

```
[jerry]$ echo "Old data" > /tmp/message.txt 
[jerry]$ cat /tmp/message.txt
```  

执行上面的命令可以得到如下的结果：  

```
Old data
```  

再用 AWK 重定向操作符重定向数据到文件 message.txt 中。  

```
[jerry]$ awk 'BEGIN { print "Hello, World !!!" > "/tmp/message.txt" }'
[jerry]$ cat /tmp/message.txt
```  

执行上面的命令可以得到如下的结果：  

```
Hello, World !!!
```  

## 追加重定向  

追加重定向操作符的语法如下：  

```
print DATA >> output-file
```  

用这种重定向方式将数据追加到 output-file 文件的末尾。如果文件不存在则先创建该文件。示例如下：  

创建文件并输入一些数据：  

```
[jerry]$ echo "Old data" > /tmp/message.txt 
[jerry]$ cat /tmp/message.txt
```  

执行上面的命令可以得到如下的结果：  

```
Old data
``` 

再使用 AWK 追加操作符追加内容到文件中：  

```
[jerry]$ awk 'BEGIN { print "Hello, World !!!" > "/tmp/message.txt" }'
[jerry]$ cat /tmp/message.txt
```  

执行上面的命令可以得到如下的结果：  

```
Old data
Hello, World !!!
```  

## 管道  

除了使用文件在程序之间传递数据之外，AWK 还提供使用管道将一个程序的输出传递给另一个程序。这种重定向方式会打开一个管道，将对象的值通过管道传递给管道另一端的进程，然后管道另一端的进程执行命令。下面是管道的使用方法：  

```
print items | command
``` 

下面的例子中我们使用 tr 命令将小写字母转换成大写。  

```
[jerry]$ awk 'BEGIN { print "hello, world !!!" | "tr [a-z] [A-Z]" }'
```  

执行上面的命令可以得到如下的结果：  

```
HELLO, WORLD !!!
```  

## 双向通信通道  

AWK 允许使用 |& 与一个外部进程通信，并且可以双向通信。下面的例子中，我们仍然使用 tr 命令将字母转换为大写字母。 command.awk 文件内容如下：  

```
BEGIN {
	cmd = "tr [a-z] [A-Z]"
	print "hello, world !!!" |& cmd
	close(cmd, "to")
	cmd |& getline out
	print out;
	close(cmd);
}
```  

执行上面的命令可以得到如下的结果：  

```
HELLO, WORLD !!!
``` 

脚本的内容看上去很神秘吗？让我们一步一步揭开它神秘的面纱。 

- 第一条语句 cmd = "tr [a-z] [A-Z]" 在AWK 中建立了一个双向的通信通道。
- 第二条语句 print 为 tr 命令提供输入。&| 表示双向通信。  
- 第三条语句 close(cmd, "to") 执行后关闭 to 进程。  
- 第四条语句 cmd |& getline out 使用 getline 函数将输出存储到 out 变量中。  
- 接下来的输出语句打印输出的内容，最后 close 函数关闭 cmd。


