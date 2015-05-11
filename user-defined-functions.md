# 用户自定义函数  

函数是程序的基本构造部分。AWK 允许我们自定义函数。事实上，大部分的程序功能都可以被切分成多个函数，这样每个函数可以独立的编写与测试。函数不仅提高了代码的复用度也提高代码的鲁棒性。  

下面是用户自定义函数的一般形式：  

```
function function_name(argument1, argument2, ...)
{
	function body
}
```  

上述定义函数的语法中： 

function_name 是用户自定义函数的名称。函数名称应该以字母开头，其后可以是数字、字母或下划线的自由组合。AWK 保留的关键字不能作为用户自定义函数的名称。 

自定义函数可以接受多个输入参数，这些参数之间通过逗号分隔。参数并不是必须的。我们也可以定义没有任何输入参数的函数。  

function body 是函数体部分，它包含 AWK 程序代码。

下面我们实现了两个简单函数，它们分别返回两个数值中的最小值和最大值。我们在主函数 main 中调用了这两个函数。 文件 functions.awk 内容如下：  

```  

\# Returns minimum number
function find_min(num1, num2)
{
  if (num1 < num2)
    return num1
  return num2
}

\# Returns maximum number
function find_max(num1, num2)
{
  if (num1 > num2)
    return num1
  return num2
}

\# Main function
function main(num1, num2)
{
  # Find minimum number
  result = find_min(10, 20)
  print "Minimum =", result
  
  # Find maximum number
  result = find_max(10, 20)
  print "Maximum =", result
}

\# Script execution starts here
BEGIN {
  main(10, 20)
}  
```  
  
执行上面的命令可以得到如下的结果：   

```
Minimum = 10
Maximum = 20
```

