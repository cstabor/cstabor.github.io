---
layout: post
title:  "python study"
date:   2016-05-28 22:13:36 +0800
categories: python 
---

### 常识
* 用缩进作为语句分组
False:0 None 空的量

## 基础函数

```
strHello = "the length of (%s) is %d" %('Hello World',len('Hello World'))
print strHello
```
#输出果：the length of (Hello World) is 11


### print自动换行

print 会自动在行末加上回车,如果不需回车，只需在print语句的结尾添加一个逗号”,“，就可以改变它的行为。

```
for i in range(0,5):
    print i,
```
或直接使用下面的函数进行输出：

```
sys.stdout.write("输出的字串")
```

### 三个读read(),readline()和readlines()

将文本文件的内容读入可以操作的字符串变量非常容易。文件对象提供了三个“读”方法： .read()、.readline() 和 .readlines()。每种方法可以接受一个变量以限制每次读取的数据量，但它们通常不使用变量。 .read() 每次读取整个文件，它通常用于将文件内容放到一个字符串变量中。然而 .read() 生成文件内容最直接的字符串表示，但对于连续的面向行的处理，它却是不必要的，并且如果文件大于可用内存，则不可能实现这种处理。

.readline() 和 .readlines() 非常相似。它们都在类似于以下的结构中使用：

```
fh = open( 'c:\\autoexec.bat')         
  for line in fh.readlines():                     
    print line.readline() # 每次只读取一行，比 .readlines()慢。仅当没有足够内存可以一次读取整个文件时，才应该使用.readline()。
    print line.readlines() # 一次读取整个文件和.read()一样。自动将文件内容分析成一个行的列表，该列表可以由 `for... in ...` 结构进行处理

```
写：writeline()是输出后换行，下次写会在下一行写。write()是输出后光标在行末不会换行，下次写会接着这行写。

global 全局变量

查找帮助：help(list.append)

删除变量：del(var)

### list 列表
[]
list.append(var)
list.remove(var)

del(list[]) 删除变量
del(var) 可以删除任何变量

### dict 字典
{}
字典是python的唯一映射类型（哈希表）
zip 将两个列表的值按照元组合并成列表
字典的键是不可变对象
dict.keys()
dict.values()
dict.item()
dict={1:'gavin', 2:'tan'}

使用工厂方法生成字典： dict = dict((['x', 1], ['y', 2]))
内建方法：{}.fromkeys(['x', 'y'], -1)

f or i in dict:

字典数据更新
字典不是有序的【无序hash】
dict.pop(var)   弹出key 为 var 的值，字典内删除。
dict.clear()  清空字典

str 可将字典转化成字符串

zip 慢
copy
str.join('str')  字符串连接

dict.get(key)
dict.get(key, error)  当key 不存在时，返回错误


多重循环 rang(i, j:step)

返回元组
for i,j in dict.items():
     print i
     print j

Ctrl + c
keyboardInterupt


使用变量来引用函数(python 中的大多数对象),比如foo=math.sqrt 之后，就可以使用foo(xx) 来对xx 求平方根了。

nan 是一个特殊值的简写， not a number(非数值）

@todo
Submit在交互式解释器内使用if语句，需要按2次回车，if 语句才能执行。第五章将对其原因进行解释。


/usr/local/env python

__future__

### import

```
from math import sqrt
sqrt(xx)

from math import *
sqrt()

import math
math.sqrt(xx)
```

str, repr, 反引号，可以将python值转换成字符串的3种方法

序列是基本的数据结构
python 中包含6种内建的序列：列表， 元组 【字符串，unicode字符串， buffer对象， xrange 对象】
列表：可以修改 [1,2,3] mutable
元组：不能修改 (1,2,3)

序列（列表，元组），映射（字典）是两类主要的容器

[start:end-1:step]
开始点的元素在结果内，结束点的元素不在结果内

序列相加：[1,2,3] + [4, 5,6]
相同类型的序列才可以相加


```
[None]*5
[None, None, None, None, None]
```

使用in 检查值是否在序列中。

append, pop( 默认最后一个）
insert, pop(0)

注意：这些方法修改列表却不返回值，原地修改。
list.remove
list.reverse
list.sort

获取排序列表副本的方法
li = sorted(list)

li.sort(cmp) 可实现同样的功能 li.sort()

list.sort()
可选参数: cmp, key, reverse, 倒序排列
list.sort(reverse=True)


### pip
pip是一个安装和管理 Python 包的工具 ,是easy_install的替代品。
install:

```
yum install epel-release
yum install python-pip
```


s = ['a', 'b', 'c', 'd']
a = 'hello'
b = 'python'
c = 1
print '%s %s %s %s' % (a, b, c, s)
输出结果：hello python 1 ['a', 'b', 'c', 'd']

字符串倒叙
方法一，使用[::-1]：
s = 'python'
print s[::-1]
方法二，使用reverse()方法：
l = list(s)
l.reverse()
print ''.join(l)

3.Python中的strip用于去除字符串的首位字符，查找到空格为止。同理，lstrip用于去除左边的字符，rstrip用于去除右边的字符。这三个函数都可传入一个参数，指定要去除的首尾字符。注意的是，传入的是一个字符数组，编译器去除两端所有相应的字符，直到没有匹配的字符，比如：

theString = 'saaaay yes no yaaaass'
print theString.strip('say')
theString依次被去除首尾在['s'，'a'，'y']数组内的字符，直到字符在不数组内。
输出的结果为：yes no

python调试
python -m pdb myscript.py #注意这会重启myscript.py

可以在程序中这么设置断点：
import pdb;
pdb.set_trace()

可以修改变量的值，但是要注意，前面加上！比如要修改final的值，应该这样!final="newvalue"

支持命令：
    p 打印变量
    n next
    step 细点运行
    c continue
    l list
    a args 打印当前函数的参数
    condition bpnumber [condition]
    clear/disable/enable 清除/禁用/使能断点
    q quit

学习过程
1、python中文件名即使模块明，如系统存在一个库叫string则如果用户自定义一个string.py的文件，当运行这个文件的时候系统将会将这个文件生成string.pyc，这时候如果用户使用
import string
这个时候导入的将使用户自定义string.py 的文件内容

2、print "xxx"
SyntaxError: invalid syntax

备注：python3里print是函数不是语法， 要加括号
正确的写法：print("xxx")

3、这是文件编码必须在第一行或者第二行
# encoding=gbk
这里encoding=gbk之间不能有空格

出错点在于 s= '哈哈' 
python默认是acii模式，换成utf-8也不支持中文，虽然说utf-8是全世界语言通行的，但是由于windows系统内并没有完全实现utf-8的全部编码。
如果你要显示中文的话换成gbk模式，文件里有非ASCII字符，须要在第一行或第二行指定编码声明：
这里必须是在第一行或者第二行指定编码声明
# coding=gbk
s = "中文"
print s

4、只有在形参末尾的参数才可以使用默认参数值，即你不能再声明形参的时候，先声明有默认值得形参而后声明没有默认值的参数

5、关键参数
     如果你的某个函数有许多参数，而你只是想指定其中的一部分，那么你可以通过命名来为这些参数赋值———这被称为关键参数———我们使用名字（关键字）而不是位置（一般我们都使用位置来给参数指定实参），这样的优势是，我们不用担心参数的顺序，使用函数变得更加简单，假设很多参数都有默认值，我们可以只给我们想要的那些参数赋值。

6、return
     没有返回值的return语句等价于return None,None是python中表示没有任何东西的特殊类型，如果一个变量的值是None，可以表示他没有值。
     除非你提供自己的return语句，每个函数都在结尾暗含有 return None语句。任何没有返回值的函数都会默认返回None

7、pass语句在python中表示一个空的语句块
     def someFunc():
          pass
8、文档字符串，函数在第一个逻辑行的字符串是这个函数的文档字符串，注意DocStrings也适用于模块和类。
     文档字符串的惯例是，一个多行字符串，它的首行以大写字母开始，句号结尾。第二行是空行，从第三行开始是详细的描述。
     可以使用__doc__注意这是双下划线，调用printMax函数的文档字符串属性（属于函数的名称）。注意在python中每一样东西都是作为对象的，包括函数。
     python中的help()，它就是抓取函数的__doc__属性，然后整洁的展示给你。
     
9、模块
     模块基本上就是一个包含了所有你定义的函数和变量的文件，为了能在其他程序中重用模块，模块的文件名必须以.py为扩展名

     python执行import sys语句的时候，它在sys.path变量中所列的目录中寻找sys.py模块，如果找到了这个文件，这个模块的主块中的语句江北运行，然后这个模块能被你使用，注意：初始化过程仅仅在我们第一次输入模块的时候进行，sys是system的缩写。
     可以自定义模块，并且定义其中的变量和函数，可以再其他模块中导入并调用
      如果是当前正在运行的模块则__name__的值为 __main__(说明这个模块式被用户单独运行的，我们可以进行一些操作），如果不是则显示模块名称

10、字节编译的.pyc文件
     在一个模块中导入另一个模块相对来说是件比较费时的事情，所以python做了一些技巧，以便import模块更加快一些，一种方法是创建字节编译文件，这些文件以.pyc作为扩展名。字节编译文件与python变换程序的中间状态有关，当你下次从别的程序输入这个模块的时候，.pyc文件十分有用，它会快很多，因为一部导入模块所需要需要的处理已经完成，另外这些字节编译文件也是平台无关的。
     Python语言写的程序不需要编译成二进制代码。你可以直接从源代码 运行 程序。在计算机内部，Python解释器把源代码转换成称为字节码的中间形式，然后再把它翻译成计算机使用的机器语言并运行。事实上，由于你不再需要担心如何编译程序，如何确保连接转载正确的库等等，所有这一切使得使用Python更加简单。由于你只需要把你的Python程序拷贝到另外一台计算机上，它就可以工作了，这也使得你的Python程序更加易于移植。

12、from..import
     如果你想要直接导入argv变量到你的程序中（避免在每次使用时都打sys), 那么你可以使用from sys import argv语句，如果你想要输入所有sys模块使用的名字，那么你可以使用from sys import *语句，这对于所有模块都使用，一般来说避免使用from..import而使用import语句，因为这样可以使你的程序更加易读，也可以避免名称的冲突。
     from mymodule import say, version # 这里可以导入函数名和变量名

13、__name__
     假如我们只想在程序本身被使用的时候运行主块，而在它被别的模块输入的时候不运行主块，通过模块的__name__属性完成
14、dir()函数
     可以使用内建的dir函数来列出模块定义的标示符（函数，类，变量）
     当你为dir()提供一个模块名的时候，它返回模块定义的名称列表，如果不提供参数，它返回当前模块中定义的名称列表
15、数据结构
     列表，元祖，字典，序列，引用
     python中有三中内建的数据结构：列表，元组，字典

     列表：中括号
     列表是可变的数据结构，可以添加任何种类的对象包括数甚至是其他列表
     列表是使用对象和类的一个例子，当你使用变量i 并给它赋值的时候，比如赋值整数5， 你可以认为你创建了一个类（类型）int的对象实例（i），你可以看一下help(int)理解
     在for循环的过程中print i，这里使用一个逗号来消除每行结尾的换行符。
     list.sort()排序影响的是列表本身，而不是返回修改后的列表，这个与字符串的工作方式不同。同时这也从侧面说明了，列表时可变的，而字符串是不可变的。

     元组：圆括号
     元组和字符串是一样的，是不可变的。元组通过圆括号中用逗号分割的项目定义。
     元组通常用在使语句或者用户定义的函数能够安全地采用一组值得时候，即使使用的元组的值不会改变。
     len函数可以用来获取元组的长度，这也表明元组也是一个序列
     可以通过方括号的形式来访问元组中的项目
     一个空的元组由一对空的圆括号组成，如mytuple=().
     含有单个元素的元组就不那么简单了，你必须在第一个项目（元素）后面跟一个逗号，这样python才能区分元组和表达式中一个带圆括号的对象。例如：mytuple=(2,)
     列表中的列表不会失去它的身份。
     
     元组的通常用法是在打印语句中。
     print 语句可以使用跟着%符号的元组的字符串
     print '%s is %d' % (name, age)

     字典：键必须是唯一的
     注意：只能使用不可变的对象（比如字符串）来作为字典的键，但是你可以把可变的或者不可变的对象作为字典的值，总体来说：使用简单对象作为键
     键值对在字典中的方式标记：d = {key1:value1, key2:value2}，注意键值对使用冒号分割，而键值对之间用逗号分割。字典的键值对是没有顺序的。
     字典是dict类的实例
     关键字参数和字典，使用字典做关键字参数，当你在使用变量的时候，他只不过是使用一个字典的键（符号表）

     序列：列表和元组，字符串都是序列
     特点：索引操作符合切片操作，索引操作符可以让我们从序列中抓取一个特定的项目（元素），切片操作符让我们能够获取到到一部分序列
     切片操作符：是序列名后跟一个方括号，方括号中是一对可选的数字，并用冒号分开。
     第一个参数：冒号之前，表示切片开始的位置，
     第二个参数：冒号之后，表示切片到哪里结束
     如果不指定第一个数，python 会从序列首开始，如果没有指定第二个数，则python会停止在序列的结尾

     引用：
     当你创建一个对象并给它赋一个变量的时候，这个变量仅仅引用哪个对象，而不是表示对象本身！也就是说，变量名指向你计算机中存储哪个对象的内存，这个被称作名称到对象的绑定。一般来说，开发人员不需要关心这个。
     复制一个列表或者类似的序列或者其他复杂对象（不是整数那样的简单对象）那么你需要使用切片操作来取得拷贝。myList = shopList[:]
     如果你只想要使用另外一个变量名，两个名称都引用同一个对象，如果你不小心，可能会引起不必要的麻烦。

     字符串方法


第11章     面向对象
1、属于一个对象或者类的变量被称为域。
     域有两种类型，属于每个实例/类的对象或属于类本身，本别称为实例变量和类变量。
p72     16:46
21:40回来
21:03开始
     类的方法与普通的函数只有一个特别的区别，他们必须有一个额外的第一个参数名称，但是在调用这个方法的时候你不为这个参数赋值，python会提供这个值。这个特别的变量是指对象本身，按照惯例它的名称是self.
     如果你有一个不需要参数的方法，你还是得给这个方法定义一个self参数。
     pass 表示空白块
     创建对象：使用类名后跟一对圆括号来创建一个对象（实例）
     <__main__.Person instance at )xfyfcb18c>:表示已经在__main__模块中有一个Person类的实例。注意：这里将存储对象的计算机内存地址也打印出来了。python可以再任何空位存储对象。
     对象的方法：和函数的区别，只是多了一个额外的self变量。
2、__init__方法
     在python的类中有很多方法的名字有特殊的意义。
     __init__方法在类的一个对象被建立时，马上运行。这个方法可以用来对你的对象做一些希望的初始化。注意名称的开头和结尾都是双下划线。
     在函数中直接创建类的成员属性。
3、类与对象的方法
     类变量：是由一个类的所有对象（实例）共享使用，只有一个类变量的拷贝，所以当某个对象对类变量做了改动的时候，这个改动会反应到所有其他的实例上。
     对象变量：是由类的所有对象(实例）拥有，因此每个对象有自己对这个域的一份拷贝，即他们不是共享的，在一个类的不同实例中，虽然变量有相同的名称，但是他们互不关联。
     类变量：直接定义到类中和方法同级
     __del__当对象不再被使用时，该方法被调用，但是很多时候我们很难保证这个方法在什么时候被调用
     对象的销毁过程符合栈的方式，先进后出，先创建的对象最后被销毁
     备注：python中所有的类成员（包括数据成员）都是公共的，所有的方法都是有效的。特殊：如果你使用的数据成员是以双下划线开始的如：__name，在python的名称管理体系中会把他作为私有变量。
     惯例：如果某个变量只想在类或者对象中使用，就应该以下划线前缀。这个并非python所必须。
4、继承
     为了使用继承，我们把基类的名称作为一个元组跟在定义类的类名称之后。python不会自动的调用基类的constructor，必须要显示的执行调用才可以。
     python中可以同名方法覆盖，子类方法可以覆盖父类方法，当调用方法的时候如果不能在当前类中找出方法，它开始在基类中逐个查找。基类：在类定义时候，元组中声明的。
     多重继承：如果在继承元组中列了一个以上的类，那么它就被称作多重继承。
     
第十二章     输入输出
1、raw_input(),print
     file('xx.txt')，如果没有指定模式，读模式会作为默认的模式
2、存储器
     python提供一个标准的模块，称为pickle。使用它你可以再文件中存储任何python对象，之后你可以将他完整无缺的取出来。这被称为持久地存储对象。
     cPickle，它的功能和pickle模块完全相同，只不过它是C语言编写的，因此要快很多（比pickle快1000倍）
     pickle     泡菜，腌制品
     
第十三章     异常
1、try..except
     通常的语句放在try块中，而把错误处理放在except块中
     可以让try..catch块关联上一个else从句，当没有异常发生的时候，else从句将被执行。
2、异常引发
     可以使用raise语句引发异常，指明错误异常的名称和伴随异常出发的异常对象。你可以引发的错误或异常应该分别是一个Error或Exception类的直接或间接导出类。






python 应用场景
承担者数据挖掘
数据分析
日志分析
自动化外链
爬虫和分析页面数据建设等等，
我相信也是其他人员的利器，比如系统管理员，动画制作人员，科学实验人员。


65页


主页 ：http://www.python.org/

python中文教程 ：
http://www.woodpecker.org.cn/obp/diveintopython-zh-5.4/zh-cn/dist/html/toc/index.html

python中文社区 ：
http://python.cn/
python 中文手册
http://www.pythonet.cn

ChinaUNIX论坛区的python版 
http://bbs.chinaunix.net/forum-55-1.html

一本最佳的python入门书籍 (英文）
http://china-pub.shop.eol.cn/computers/common/info.asp?id=25523
一个很好的开源pythonIDE 
http://stani.be/python/spe/blog/

http://www.okpython.com
老黄纸条箱（黄冬）http://blog.opensource.org.cn/hdcola/
Limodou的学习笔记（木头）网址：http://blog.donews.com/limodou/ http://limodou.javaeye.com/
邱英波 http://www.dup2.org/blog
肥三的专栏——热酷网CTO梁冰鸿 网址：http://blog.csdn.net/FeiSan

社区/论坛
灵蛇网：http://bbs.pythonid.com/
Python中文社区：http://www.pythonbbs.cn
http://bbs.chinaunix.net/thread-1164933-1-1.html
