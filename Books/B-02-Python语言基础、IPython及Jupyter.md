[TOC]

# 1.0 Python解释器
Python是一种解释型语言。Python解释器通过一次执行一条语句来运行程序。
# 2.0 IPython和Jupyter notebook基础
Jupyter项目中的主要组件就是notebook，这是一种交互式的文档类型，可以用编写代码、文本（可以带标记）、数据可视化以及其他输出。

需要启动Jupyter时，可以在终端中国呢运行jupyter notebook命令
```
$ jupyter notebook
```
## 2.1对象内省
在一个变量名的前后使用问号（？）可以显示一些关于该对象的概要信息。这就是对象内省。
如果对象是一个函数或实例方法且文档字符串已经写好，则文档字符串会显示出来。
使用双问号？？可以显示函数的源代码.
？可以通过把一些字符和通配符（*）结合在一起，会显示所有匹配通配符表达式的命名。例如
```
np.*load*?
```
## 2.2%run命令
可以在Ipython绘画中使用%run命令运行任意的Python程序文件。假设你已经在hello_world.py中写好了如下的简单脚
```
def f(x,y,z):
    return (x+y)/z
a = 5
b = 6
c = 7.5
result = f(a,b,c)
```
可以将文件名作为参数传给%run命令
```

%run hello_world.py
```
如果没有异常，文件中定义的所有变量（倒入的，函数中得到、全局定义的）在成功运行后，可以在IPython命令行中使用。
如果一个Python脚本需要命令行提供参数（通过sys.argv获取），那么则需要在命令行的文件路径后面加上参数进行传递


%load魔法函数：导入一个代码单元

%paste %cpaste 执行剪贴板中的程序

## 魔术命令
IPython的特殊命令（没有内建到Python自身去）被称为魔术命令。这些命令被设计用骨简化常见任务，确保用户更容易控制IPython系统的行为。
魔术命令的前缀符号是百分号%。
%timeit：检查一段Python语句的执行时间
魔术函数也可以不加百分号%就使用，只要没有变量被定义为与魔术函数相同的名字即可。这种特性被称为自动魔术。通过%automagic进行启动/禁用关。
%pwd


建议使用%quickref 或者%magic探索所有的特殊命令


# matplotlib集成
IPython
能在分析计算领域流行的原因之一，就是他和数据可视化、用户界面库（如matplotlib）的良好集成。
%matplotlib魔术函数可以设置matplotlib与IPython命令行或Jupyter notebook的集成。
这个命令很重要，否则你创建的图可能不会出现（notebook），或者直到结束也无法控制会话（命令行）

在IPyhton命令行中，运行%matplotlib命令可以生成多个绘图窗口，而无需干扰控制台的会话。
在Jupyter中，命令会有些许不同 %matplotlib inline

# 3.0 Python语言基础
## 3.1语言语义

* 1、缩进取代大括号：冒号代表缩进块的开始，单个代码块中所有的代码必须要保持相同的缩进，知道代码块结束。
* 2、不用；做结尾，但是同一行内可以用分号进行分割
* 3、一切都是对象：每一个数值、字符串、数据结构、函数、类、模块以及所有存在于Python解释器中食物，都是Python对象。每个对象都会关联到一种类型（例如字符串、函数）和内部数据。
* 4、注释：#
* 5、函数和对象方法的调用：调用函数时，向函数括号传递0或多个参数，通常会把返回值赋值给一个变量：
```
result = f(x,y,z)

g()
```

几乎所有的Python对象都有内部函数，称为方法，可以访问对象内部的内容。你可以通过以下语法调用它们：
```
obj.some_method(x,y,z)
```

函数传参既可以是未知传参也可以是关键字传参。
* 6、变量和参数传递
```
a= [1,2,3]

b = a
```
在Python中对一个变量（或者变量名）赋值时，，你就创建了一个指向等号右边对象的引用。
在一些语言中，会是数据[1,2,3]被拷贝的过程。在Python中，a和b实际上是指向了相同的对象，即原来的[1,2,3]
* 7、动态引用、强类型
与Java和C++等大多数编译型语言不通，Python中的对象引用不涉及类型。
变量是不分类型的，但是对象引用是强类型的
可以使用isinstance函数来检查一个对象是否是特定类型的实例
```
a = 5
isinstance(a,int)
isinstance(a,(int,float))
```
* 8、属性和方法：属性和方法都可以通过obj.attribute_name的语法进行调用
属性和方法也可以通过getattr函数获得
```
getattr9a,'split')
```
* 9、鸭子类型
只关心是否具有某种方法，而不关心是否是某种具体类型。
在编写接受多多种类型输入的函数时，可以用到，常见的例如编写接受任意序列类型（列表、远足、n维数组），甚至是一个迭代器的函数时使用这项功能。
* 10、导入
```
#some_module.py
def f(x):
    return x + 2
def g(a,b):
    return a +b
```
从另一个相同路径下的文件链接到some_module.py中定义的变量和函数
```
import some_module
result = some_module.f(5)
pi = some_module.PI
```
or

```
from some_module import f,g,PI
result = g(5,PI)
```
or
```
import some_module as sm
from some_module import PI as pi, g as gf
r1 = sm.f(pi)
r2 = gf(6,pi)
```

* 11、二元运算符和比较运算
+ - * / . <= != true/false等

检查两个引用是否指向同一个对象，可以使用is关键字。
is not 
list函数总是创建一个新的Python列表（即一份拷贝）

* 12、可变对象和不可变对象
列表、字典、NumPy数组都是可变对象，大多数用户定义的类型也是可变的
字符窜、元组是不可变的

## 3.2 标量类型
Python的标准库中拥有一个小的内建类型集合，用来处理数值数据、字符串、布尔值以及日期和时间。
这类单值类型有时被称为标量类型，我们管它称为标量。
None str bytes float bool int
* 1、数值类型
int float
int 可以存储任意大小数字：
flaot标识浮点数，可以用科学记数法表示 5.78e-5

整数除法/会把结果自动转型为浮点数


// C语言风格的整数除法（去除了非整数结果的小数部分）
* 2、字符串
单引号或者双引号写入一个字符串的字面值。
含有换行的多行字符串，可以使用三个单引号或者双引号。
Python的字符串是不可变的，无法修改
很多Python对象可以通过str函数转化为字符串

字符串死Unicode字符的序列，因此可以被看作是除了列表和元组外的另一种序列：
```
In:s = 'python'
In:list(s)
Out:['p','y','t','h','o','n']

```
```
In:s[:3]
Out:'pyt'
```
s[:3]这种语法被称为切片，在多种Python序列中有实现。在数据分析计算中广泛使用

\转义符号
r取消转义
字符串对象拥有一个format方法，可以用来代替字符串中的格式化参数，并产生一个新的字符串：
```
In:template = '{0:.2f} {1:s} are worh US${2:d}'

```
在这个字符串中
.{0:.2f}表示将第一个参数格式化为2位小数的浮点数
.{1:s}表示将第二个参数格式化为字符串
.{2:d}表示将第三个桉树格式化整数
为了替代这些格式化参数，我们将含有参数的序列传给format方法

```
In:template.format(4.500,'asdasd',1)
Out:'4.5 asdasd are worth US$1'
```
* 3、字节与Unicode
在Python3.0以上，Unicode称为字符串类型的一等类，用于更好的兼容处理ASCII和非ASCII文本。在Python的早期版本中，字符串完全是字节，而没有显式的Unicode编码。
我们可以使用encode方法将这个Unicode字符串转换为UTF-8字节
还可以使用decode对一个已知Unicode编码的字节对象进行解码
* 4、 布尔值
* 5、类型转换
str、bool、int和float既是数据类型，同时也是可以将其他数据类型转换为这些类型的函数。
* 6、None
None是Python的null值类型。如果一个函数没有显式的返回值，则它会隐式的返回None
None是NoneType的唯一实例。
* 7、日期和时间
datetime包含了datetime、data和time类型。
对于datetime实例，可以分别使用date和time方法获取他的date和time对象：
strtime方法可以将datetime转换为字符串
字符串可以通过strptime函数转换为datetime对象

## 3.3 控制流
* 1、if、elif和else

和Java、C++一样 ，and or判断时，会有短路现象。
* 2、for循环
for循环用于遍历一个集合（例如列表或元组）或一个迭代器。
continue：跳过本次循环
break：跳出该循环体

如果集合或迭代器中的元素是一个序列（比如元组或者列表），它们可以在for循环语句中很方便的通过拆包称为变量
```
for a,b,c in iterator
```

* 3、while循环
* 4、pass
表示什么也不做，不执行任何操作，之所以需要它，是因为Python使用了缩进来分隔代码块。
* 5、range
range函数返回一个迭代器，该迭代器生成一个等差整数序列。
```
In:range(10)
Out:range(0,10)
In:list(range(10))
Out:[0,1,2,3,4,5,6,7,8,9,10]

```
起始和结尾、步进（可以是负）可以传参给range函数。
range产生的整数包含起始但不包含结尾。
range常用于根据序列的索引遍历序列。
* 6、三元表达式
容易影响阅读


