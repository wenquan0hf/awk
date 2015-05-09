#AWK-工作流程

这一章节中，我们将解释 AWK 是如何工作的。 要想成为 AWK 专家，你必须得了解其内部工作的原理。 AWK 执行的流程非常简单：读( Read )、执 行（ Execute )与重复( Repeat )。下面的流程图描述出了 AWK 的工作流程：

![](./images/awk_workflow.jpg)  

###读（Read） 
 
AWK 从输入流（文件、管道或者标准输入）中读入一行然后将其存入内存中。

###执行(Execute)  

对于每一行输入，所有的 AWK 命令按顺执行。 默认情况下，AWK 命令是针对于每一行输入，但是我们可以将其限制在指定的模式中。

###重复（Repeate）

一直重复上述两个过程直到文件结束。  

##程序的结构

我们已经见过 AWK 程序的工作流程。 现在让我们一起来学习 AWK 程序的结构。

### 开始块（BEGIN block）

开始块的语法格式如下所示：  

```
BEGIN {awk-commands}
```  

顾名思义，开始块就是在程序启动的时候执行的代码部分，并且它在整个过程中只执行一次。 一般情况下，我们在开始块中初始化一些变量。BEGIN 是 AWK 的关键字，因此它必须是大写的。 不过，请注意，开始块部分是可选的，你的程序可以没有开始块部分。  

###主体块（Body Block） 
 
主体部分的语法要求如下： 
 
```
/pattern/ {awk-commands}
```  

对于每一个输入的行都会执行一次主体部分的命令。默认情况下，对于输入的每一行，AWK 都会很执行命令。但是，我们可以将其限定在指定的模式中。 注意，在主体块部分没有关键字存在。 
 
### 结束块（END Block）

下面是结束块的语法格式：  

```
END {awk-commands}
```
  
结束块是在程序结束时执行的代码。 END 也是 AWK 的关键字，它也必须大写。 与开始块相似，结束块也是可选的。

###示例  

先创建一个名为 **marks.txt** 的文件。其中包括序列号、学生名字、课程名称与所得分数。  
  
```
1)    Amit     Physics    80
2)    Rahul    Maths      90
3)    Shyam    Biology    87
4)    Kedar    English    85
5)    Hari     History    89
```  

接下来，我们将使用 AWK 脚本来显示输出文件中的内容，同时输出表头信息。  
  
```
[jerry]$ awk 'BEGIN{printf "Sr No\tName\tSub\tMarks\n"} {print}' marks.txt
```  

执行上面的代码后，将会输出如下的结果：  

```
Sr No Name     Sub        Marks
1)    Amit     Physics    80
2)    Rahul    Maths      90
3)    Shyam    Biology    87
4)    Kedar    English    85
5)    Hari     History    89
```  

程序启动时，AWK 在开始块中输出表头信息。在主体块中，AWK 每读入一行就将读入的内容输出至标准输出流中，一直到整个文件被全部读入为止。