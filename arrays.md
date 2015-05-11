# 数组　　

AWK 有关联数组这种数据结构，而这种数据结构最好的一个特点就是它的索引值不需要是连续的整数值。我们既可以使用数字也可以使用字符串作为数组的索引。除此之外，关联数组也不需要提前声明其大小，因为它在运行时可以自动的增大或减小。这一章节中将会讲解 AWK 数组的使用方法。  

如下为数组使用的语法格式：  

```
array_name[index]=value
```  

其中 array_name 是数组的名称，index 是数组索引，value 为数组中元素所赋予的值。  

## 创建数组

为了进一步了解数组，我们先来看一下如何创建数组以及如何访问数组元素：  

```
[jerry]$ awk 'BEGIN {
fruits["mango"]="yellow";
fruits["orange"]="orange"
print fruits["orange"] "\n" fruits["mango"]
}'
```  

 执行上面的命令可以得到如下的结果：   

```
orange
yellow
```   

在上面的例子中，我们定义了一个水果(fruits)数组，该数组的索引为水果名称，值为水果的颜色。可以使用如下格式访问数组元素：  

```
array_name[index] 
```  

## 删除数组元素

插入元素时我们使用赋值操作符。删除数组元素时，我们则使用 delete 语句。如下所示：  

```
delete array_name[index]
```  

下面的例子中，数组中的 orange 元素被删除（删除命令没有输出）：   

```
[jerry]$ awk 'BEGIN {
fruits["mango"]="yellow";
fruits["orange"]="orange";
delete fruits["orange"];
print fruits["orange"]
}'
```  

## 多维数组

AWK 本身只支持多维数组，不过我们可以很容易地使用一维数组模拟实现多维数组。  

如下示例为一个 3x3 的三维数组：  

```
100 200 300
400 500 600
700 800 900
```  

上面的示例中，array[0][0] 存储 100，array[0][1] 存储 200 ，依次类推。为了在 array[0][0] 处存储100, 我们可以使用如下语法：  

```
array["0,0"] = 100
``` 

尽管在示例中，我们使用了 0,0 作为索引，但是这并不是两个索引值。事实上，它是一个字符串索引 0,0。

下面是模拟二维数组的例子：  

```
[jerry]$ awk 'BEGIN {
array["0,0"] = 100;
array["0,1"] = 200;
array["0,2"] = 300;
array["1,0"] = 400;
array["1,1"] = 500;
array["1,2"] = 600;
# print array elements
print "array[0,0] = " array["0,0"];
print "array[0,1] = " array["0,1"];
print "array[0,2] = " array["0,2"];
print "array[1,0] = " array["1,0"];
print "array[1,1] = " array["1,1"];
print "array[1,2] = " array["1,2"];
}'
```  

 执行上面的命令可以得到如下结果：   

```
array[0,0] = 100
array[0,1] = 200
array[0,2] = 300
array[1,0] = 400
array[1,1] = 500
array[1,2] = 600
```  

在数组上可以执行很多操作，比如，使用 asort 完成数组元素的排序，或者使用 asorti 实现数组索引的排序等等。我们会在后面的章节中介绍可以对数组进行操作的函数。 

