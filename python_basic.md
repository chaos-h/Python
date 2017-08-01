---
 @Author:      liyu
 @DateTime:    2016-10-03 14:53:17
 @Description: python learning notes
---

# 基础语法

1. # !/usr/bin/python
# -*- coding:utf-8 -*-
# 第一个注释用于指定编译器
# 第二个注释用于中文编码，python3是不用的

2. 标识符
组成：字母、数字、下划线组成。
注意：不能以数字开头。
其他：_example1 以单下划线开头的代表不能直接访问的类属性，
      __example2 以双下划线开头的代表类的私有成员
      \__example3__ 以双下划线开头和结尾的（__foo__）代表python里特殊方法专用的标识，如__init__（）代表类的构造函数。

3. 行和缩进
Python的代码块不使用大括号（{}）来控制类，函数以及其他逻辑判断。python最具特色的就是用缩进来写模块。
*所有代码块语句必须包含相同的缩进空白数量*

4. 多行语句
Python语句中一般以新行作为为语句的结束符。
但是我们可以使用斜杠（ \）将一行的语句分为多行显示。但是，语句中包含[], {} 或 () 括号就不需要使用多行连接符。

5. 注释
单行#
多行 """ """ or ''' '''

6. 字符串
''
""
''' '''or""" """ 可多行文本

7. 空行
函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。类和函数入口之间也用一行空行分隔，以突出函数入口的开始。
空行与代码缩进不同，空行并不是Python语法的一部分。书写时不插入空行，Python解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。
记住：空行也是程序代码的一部分。

8. 等待用户输入

```python
raw_input("\n\nPress the enter key to exit.")
```


9. 同一行显示多条语句，语句间用*;*隔开




# 变量类型

1.Python 中的变量赋值不需要类型声明。
每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。=
*赋值*
单个：x='how are you'
多个：x=y=c=1
      x,y,z=1,2.0,'may'

2. 标准数据类型
每个数据都是一个对象，可用 *del*语句删除对象的引用。

>del语法  del var1[,var2[,var3[....,varN]]]]
使用eg：del var
del var_a，var_b

- numbers(数字)
	* int
	* long 12L(也可小写)
	* float
	* complex（复数）实部虚部都是浮点型 如1+2j，complex(12,3.0)
	
- strings(字符串)
	* 字符串切片 str='howtolove' str[0:2]是'ho'*准确的说是[0,2)*
	str[2:]是'wtolove'
	str[2]是'w'
	str[-1] 'e'(倒数第一)
	* 加号（+）是字符串连接运算符，星号（*）是重复操作
	str*2 'howtolovehowtolove'
	str+'isdifficule' 是'howtoloveisdifficult'

- list(列表)
	* [a1,a2,...,an] ai 可以是数字，字符串，列表
	list=[123,12.0,'giw']
	* 可切片
	* 支持+和*号操作
	* 更新：list[1]=123.4

- tuple(元组)
	* 类似列表，但是用()标识，且元素不可改变，但是可以组合，如tuple3 = tuple1 + tuple2
	  (123,12.3,'how')
	* 只有一个元素时，元素后面要加一个逗号 tup1 = (50,)
	* 任意无符号的对象，以逗号隔开，默认为元组 如 tuple1 = 123, 124, 125


- dictionary(字典)
	* 列表有序，字典*无序*  ；列表可通过偏移来取，字典通过键来取
	* {key1:value1,key2:value2,...,keyn:vlauen}
	me={'name':'liyu','sex':'male','age':18,3:1234}
  * add me['state'] = 'chaos'
	* 取值
		*  me['name'] 是 'liyu'
		*  me[3] 是 1234
		*  me.keys() 所有键值 ['name','sex','age',3]
		*  me.vlaues() 所有值 ['liyu','male',18,1234]
	* 不允许同一个键出现两次。创建时如果同一个键被赋值两次，第一个值会被覆盖
	* 键必须不可变，所以可以用数字，字符串或元组充当，所以用列表就不行（列表可变）

3. 类型转换
数据类型的转换，只需要将数据类型作为函数名即可.
eg.
int(x [,base])
将x转换为一个整数
long(x [,base] )
将x转换为一个长整数
float(x)
将x转换到一个浮点数
complex(real [,imag])
创建一个复数
str(x)
将对象 x 转换为字符串
repr(x)
将对象 x 转换为表达式字符串
eval(str)
用来计算在字符串中的有效Python表达式,并返回一个对象
tuple(s)
将序列 s 转换为一个元组
list(s)
将序列 s 转换为一个列表
set(s)
转换为可变集合
dict(d)
创建一个字典。d 必须是一个序列 (key,value)元组。
frozenset(s)
转换为不可变集合
chr(x)
将一个整数转换为一个字符
unichr(x)
将一个整数转换为Unicode字符
ord(x)
将一个字符转换为它的整数值
hex(x)
将一个整数转换为一个十六进制字符串
oct(x)
将一个整数转换为一个八进制字符串

# 运算符
1. 各种运算符

- 算术运算符
	* x**y x的y次幂
	* x//y 整除，取商的整数部分
- 比较运算符
	* !=和<>都是不等
- 赋值运算符
- 位运算符
- 逻辑运算符
	* x and y  布尔"与" - 如果 x 为 False，x and y 返回 False，否则它返回 y 的计算值。
	* x or y 布尔"或"	- 如果 x 是非 0，它返回 x 的值，否则它返回 y 的计算值。
	* not y 布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。
 - 成员运算符(判断成员是否在字符串或者列表或者元组中)
 	* in 
 	* not in
 	* a=2,b=[1,2,3] a in b 为true，a not in b 是 fals
 - 身份运算符(比较两个对象的存储单元)
 	* is x is y 如果id(x)==id(y),返回1
 	* is not
 
 2. 算符优先级
 由高到低
**	        指数 (最高优先级)
~ + -	    按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@)
* / % //	乘，除，取模和取整除
+ -	        加法减法
>> <<		右移，左移运算符
&			位 'AND'
^ |			位运算符
<= < > >=	比较运算符
<> == !=	等于运算符
= %= /= //= -= += *= **=	赋值运算符
is is not	身份运算符
in not in	成员运算符
not or and	逻辑运算符

# 条件语句
任何非0和非空（null）值为True，0 或者 null为False.
注意：Ture 和 False 在python 里面是可以用的，首字母大写，不要忘记

- 无swith语句

- 基本形式
if 判断条件：
    执行语句……
else：
    执行语句……

- 当判断条件为多个值
if 判断条件1:
    执行语句1……
elif 判断条件2:
    执行语句2……
elif 判断条件3:
    执行语句3……
else:
    执行语句4……

- 你也可以在同一行的位置上使用if条件判断语句

# 循环语句

1. while循环
格式：
while 判断条件：
    执行语句……
2. for循环
 for循环可以遍历任何序列的项目，如一个列表或者一个字符串。
 格式：
 for iterating_var in sequence:
   statements(s)
 两种方式例子：
eg1.

```python
 for letter in 'Python':     
    print '当前字母 :', letter
```
eg2.通过序列索引迭代

```python
fruits = ['banana', 'apple',  'mango']
for index in range(len(fruits)):
   print '当前水果 :', fruits[index]
```
*内置函数 len() 和 range(),函数 len() 返回列表的长度，即元素的个数。 range返回一个序列的数。*

eg3. else

```python
for num in range(10,20):  # 迭代 10 到 20 之间的数字
   for i in range(2,num): # 根据因子迭代
      if num%i == 0:      # 确定第一个因子
         j=num/i          # 计算第二个因子
         print '%d 等于 %d * %d' % (num,i,j)
         break            # 跳出当前循环
   else:                  # 循环的 else 部分
      print num, '是一个质数'
```


3. 循环嵌套
4. break 语句
5. continue 语句
6. pass 语句
Python pass是空语句，是为了保持程序结构的完整性。
pass 不做任何事情，一般用做占位语句。
7. 循环中的else语句
for … else 表示这样的意思，for 中的语句和普通的没有区别，else 中的语句会在循环正常执行完（即 for 不是通过 break 跳出而中断的）的情况下执行，while … else 也是一样。
8. 无限循环可以用ctrl+c 来中断


# 函数

1. 标准格式
- 函数代码块以 def 关键词开头，后接函数标识符名称和圆括号()。
- 任何传入参数和自变量必须放在圆括号中间。圆括号之间可以用于定义参数。
- 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
- 函数内容以冒号起始，并且缩进。
- return [表达式] 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回 None。

---
def functionname( parameters ):
   "函数_文档字符串"
   function_suite
   return [expression]
---

2. 参数
所有参数（自变量）在Python里都是按引用传递。如果你在函数里修改了参数，那么在调用这个函数的函数里，原始的参数也被改变了。
几种参数分类
* 必备参数（正常函数）
	* 顺序，个数严格要求
* 关键字参数(与调用密切相关，在调用时括号内对形参赋值)
	* 对顺序不看重
	
```python
def printinfo( name, age ):
   "打印任何传入的字符串"
   print "Name: ", name;
   print "Age ", age;
   return;
 
#调用printinfo函数
printinfo( age=50, name="miki" );
```
结果：Name:  miki
	  Age  50

* 默认参数（形参有缺省值）
	* 可覆盖，可缺省

```python
#可写函数说明
def printinfo( name, age = 35 ):
   "打印任何传入的字符串"
   print "Name: ", name;
   print "Age ", age;
   return;
 
#调用printinfo函数
printinfo( age=50, name="miki" );
printinfo( name="miki" );
```

* 不定长参数（变量加星号）
	* 用于不指定个数的参数
	* 加了星号（*）的变量名会存放所有未命名的变量参数

```python
# 可写函数说明
def printinfo( arg1, *vartuple ):
   "打印任何传入的参数"
   print "输出: "
   print arg1
   for var in vartuple:
      print var
   return;
 
# 调用printinfo 函数
printinfo( 10 );
printinfo( 70, 60, 50 );
```
结果：
输出:
10
输出:
70
60
50

3. lamhda（匿名函数）
格式：
lambda [arg1 [,arg2,.....argn]]:expression
eg1

```python
# 可写函数说明
sum = lambda arg1, arg2: arg1 + arg2;
 
# 调用sum函数
print "相加后的值为 : ", sum( 10, 20 )
print "相加后的值为 : ", sum( 20, 20 )
```
4. 局部变量和全局变量
在函数里面声明和使用的变量默认是局部变量，如果要在函数里面对全局变量进行赋值操作，要使用global声明。
表达式：global VarName

5. docstring(文档字符串)
  在函数，模块，类中，用来作说明的字符串。
  惯例:
  首行大写字母开头，句号结束
  第二行为空行
  第三行开始详细描述

  调用：
  functionname.__doc__(双下划线)，python里面都是对象

  python 内嵌的help(),就是抓取这个字符串

# 模块
1. python 模块
简单地说，模块就是一个保存了Python代码的文件。模块能定义函数，类和变量。模块里也能包含可执行的代码。
模块也是Python对象，具有随机的名字属性用来绑定或引用。


例子：
假设有一个模块support.py，内容如下

```python
def print_func( par ):
   print "Hello : ", par
   return
```
2. import语句
想使用Python源文件，只需在另一个源文件里执行import语句，语法如下：
import module1[, module2[,... moduleN]

当解释器遇到import语句，如果模块在当前的搜索路径就会被导入。
搜索路径是一个解释器会先进行搜索的所有目录的列表。
一个模块只会被导入一次，不管你执行了多少次import

```python
# 导入模块
import support
 
# 现在可以调用模块里包含的函数了
support.print_func("Zara")
```
输出结果：Hello : Zara

3. from...import
从模块中导入一个指定的部分到当前命名空间中
语法：from modname import name1[, name2[, ... nameN]]
如：from support import print_func
这样就可以直接使用print_func函数，而不必加前缀

4. from...import*
语法：from modname import *
把一个模块的所有内容全都导入到当前的命名空间

6. 模块定位
导入一个模块时，python解释器的搜索顺序是
	* 当前目录
	* shell变量PYTHONPATH下的目录
		- win set PYTHONPATH=c:\python20\lib;
		- unix set PYTHONPATH=/usr/local/lib/python
	* 查看默认路径（安装路径）
7. 命名空间和作用域
变量：拥有匹配对象的名字（标识符）
命名空间：包含了变量名称们（键）和它们各自相应的对象们（值）的字典。
如果一个局部变量和一个全局变量重名，则局部变量会覆盖全局变量。
每个函数都有自己的命名空间。类的方法的作用域规则和通常函数的一样。
如果要给全局变量在一个函数里赋值，必须使用global语句。

7.1 dir()函数
dir()函数一个排好序的字符串列表，内容是一个模块里定义过的名字。
返回的列表容纳了在一个模块里定义的所有模块，变量和函数。

eg.

```python
import math
content = dir(math)
print content;
```
7.2 globals() and locals()
根据调用地方的不同，globals()和locals()函数可被用来返回全局和局部命名空间里的名字。
如果在函数内部调用locals()，返回的是所有能在该函数里访问的命名。
如果在函数内部调用globals()，返回的是所有在该函数里能访问的全局名字。
两个函数的返回类型都是字典。所以名字们能用keys()函数摘取。

7.3 reload()
当一个模块被导入到一个脚本，模块顶层部分的代码只会被执行一次。
因此，如果你想重新执行模块里顶层部分的代码，可以用reload()函数。该函数会重新导入之前导入过的模块。语法如下：
reload(module_name)
注意：module_name要直接放模块的名字，而不是一个字符串形式
如:reload(hello)

7.4 模块的__name__以及使用
模块本身__name__的值是__main__
当模块被import时，__name__值变化
所以可以在模块中植入以下代码，决定是否在模块引用时候执行

```python
if __name__ == '__main__':
    print 'hello ,me!'#可更改
else:
    print 'who are you'
```
被第一次import的时候，将输出 who are you


8. python的包
包是一个分层次的文件目录结构，它定义了一个由模块及子包，和子包下的子包等组成的Python的应用环境。
包的标志：含有__init__.py模块
在__init__.py import相关的函数，那么import这个包就可以使用它

例子：
Phone/Isdn.py 含有函数Isdn()
Phone/G3.py 含有函数G3()
在Phone目录下创建file __init__.py：
Phone/__init__.py
内容如下：
from Isdn import Isdn
from G3 import G3

使用：

、# 导入 Phone 包
import Phone
 
Phone.Isdn()
Phone.G3()


#面向对象编程
 1. 创建类

     class ClassName:
     '类的帮助信息'   #类文档字符串
     class_suite  #类体
     
类的帮助信息可以通过ClassName.__doc__查看。
class_suite 由类成员，方法，数据属性组成。

 2. 可以更改，添加，删除类的属性

 3. 以函数的方式访问属性
	- getattr(obj, name[, default]) : 访问对象的属性,返回属性值。
	- hasattr(obj,name) : 检查是否存在一个属性。
	- setattr(obj,name,value) : 设置一个属性。如果属性不存在，会创建一个新属性。
	- delattr(obj, name) : 删除属性。
 4.  内置类属性
	* __dict__ : 类的属性（包含一个字典，由类的数据属性组成）
	* __doc__ :类的文档字符串
	* __name__: 类名
	* __module__: 类定义所在的模块（类的全名是'__main__.className'，如果类位于一个导入模块mymod中，那么className.__module__ 等于 mymod）
	* __bases__ : 类的所有父类构成元素（包含了一个由所有父类组成的元组

 5. 对象销毁（垃圾回收）
 同Java语言一样，Python使用了引用计数这一简单技术来追踪内存中的对象。
在Python内部记录着所有使用中的对象各有多少引用。
一个内部跟踪变量，称为一个引用计数器。
当对象被创建时， 就创建了一个引用计数， 当这个对象不再需要时， 也就是说， 这个对象的引用计数变为0 时， 它被垃圾回收。但是回收不是"立即"的， 由解释器在适当的时机，将垃圾对象占用的内存空间回收。

```
		a = 40      # 创建对象  <40>
		b = a       # 增加引用， <40> 的计数
		c = [b]     # 增加引用.  <40> 的计数
		
		del a       # 减少引用 <40> 的计数
		b = 100     # 减少引用 <40> 的计数
		c[0] = -1   # 减少引用 <40> 的计数
```

析构函数 __del__ ，__del__在对象销毁的时候被调用，当对象不再被使用时，__del__方法运行：

 6. 继承
 
 继承语法: 
 class 派生类名（基类名）：//... 基类名写作括号里，基本类是在类定义的时候，在*元组*之中指明的

 继承的特点：
	1：在继承中基类的构造（__init__()方法）不会被自动调用，它需要在其派生类的构造中亲自专门调用。
	2：在调用基类的方法时，需要加上基类的类名前缀，且需要带上self参数变量。区别于在类中调用普通函数时并不需要带上self参数
	3：Python总是首先查找对应类型的方法，如果它不能在派生类中找到对应的方法，它才开始到基类中逐个查找。（先在本类中查找调用的方法，找不到才去基类中找）。


 7. 如果父类方法无法满足需要，可以重写方法
 基础重载方法：
 下表列出了一些通用的功能，你可以在自己的类重写：
	序号	方法, 描述 & 简单的调用
	1)	__init__ ( self [,args...] )
	构造函数
	简单的调用方法: obj = className(args)
	2)	__del__( self )
	析构方法, 删除一个对象
	简单的调用方法 : del obj
	3)	__repr__( self )
	转化为供解释器读取的形式
	简单的调用方法 : repr(obj)
	4)	__str__( self )
	用于将值转化为适于人阅读的形式
	简单的调用方法 : str(obj)
	5)	__cmp__ ( self, x )
	对象比较
	简单的调用方法 : cmp(obj, x)

	python也支持运算符的重载：见下例子


```python
#!/usr/bin/python

class Vector:
   def __init__(self, a, b):
      self.a = a
      self.b = b

   def __str__(self):
      return 'Vector (%d, %d)' % (self.a, self.b)
   
   def __add__(self,other):
      return Vector(self.a + other.a, self.b + other.b)

v1 = Vector(2,10)
v2 = Vector(5,-2)
print v1 + v2
```
结果：Vector(7,8)

 8. 私有属性和方法
 类的私有属性
\__private_attrs：两个下划线开头，声明该属性为私有，不能在类地外部被使用或直接访问。在类内部的方法中使用时 self.__private_attrs。

类的方法
在类地内部，使用def关键字可以为类定义一个方法，与一般函数定义不同，类方法必须包含参数self,且为第一个参数

类的私有方法
\__private_method：两个下划线开头，声明该方法为私有方法，不能在类地外部调用。在类的内部调用 self.__private_methods

*注意*：Python不允许实例化的类访问私有数据，但你可以使用 object._className__attrName 访问属性

一个类教学例子

```python
# -*- coding:utf-8 -*-
"""This module practice the attributes of oop"""


class FirstClass:
    """first class

    This class is for testing the attributes of oop"""
    count = 0  # 类变量

    def __init__(self, name, age, sex):  # 构造函数
        self.name = name  # 实例变量
        self.age = age
        self.sex = sex
        FirstClass.count += 1  # 对类变量的操作

    def show_info(self):
        print 'name:' + self.name + '   age:' + str(self.age) + '    sex:' + self.sex

    def __del__(self):
        print self.__class__.__name__+"is deleted"  # __class__ attr is used when class attr is called

# 直接在类外访问类成员或属性
print "There are %d in total" % FirstClass.count
# 创建对象并访问属性
little_class = FirstClass('angle', '18', 'girl')
little_class.show_info()
# 添加，删除，修改类的属性
little_class.hobby = 'reading'  # 添加属性
little_class.age = 20  # 更改属性
del little_class.sex  # 删除属性
# 以函数的方式访问对象的属性
if hasattr(little_class, 'hobby'):  # hasattr(obj,name)
    print 'hooray'
else:
    print 'oh,dude,you are dump'

setattr(little_class, 'mate', 'yes')  # setattr(obj,name,value)
if getattr(little_class, 'mate') == 'yes':  # getattr(obj, name,default) get the value of the attr
    print 'fantastic, you are not a lonely dog'
else:
    print 'ok, actually you are not the only one that are an lonely dog'
delattr(little_class, 'mate')

# 类的内置属性
print FirstClass.__doc__  # print the docstring
print FirstClass.__module__  # the module "__main__" for the original
print FirstClass.__bases__  # the father classes
print FirstClass.__name__  # the name of the class
print FirstClass.__dict__  # the dict of all attr

obj1 = little_class
obj2 = obj1
print id(little_class), id(obj1), id(obj2)
del little_class
del obj1
del obj2

# 继承


class Student(FirstClass):
    """STUDENTS HEIR

    This class is just for test heir attr"""
    def __init__(self, grade, name, age, sex, hobby):
        self.grade = grade
        self.hobby = hobby
        FirstClass.__init__(self, name, age, sex)  # 记得调用父类方法时要加上self变量

    def __del__(self):
        print self.__class__.__name__+"is done"
    #重写方法
    def show_info(self):
        print "name:"+self.name+"   age:"+str(self.age)+"   sex:"+self.sex+"    hobby:"+self.hobby+"    grade:"+str(self.grade)
        # 注意有字符串和数字时候的问题

std = Student(2, "morning", 19, "MALE", "READING")
print std.hobby
print std.sex
std.show_info()

# 运算符重载


class Vector:
    """Class Vector
    This class is created for testing the overwriting of the operation pattern"""
    def __init__(self, a, b):
        self.a = a
        self.b = b

    def __str__(self):
        return "Vector(%d,%d)" % (self.a, self.b)

    def __add__(self, other):
        return Vector(self.a+other.a, self.b+other.b)

v1 = Vector(1, 2)
V2 = Vector(2, 3)
print v1+V2

# 私有属性和变量


class Myself:
    """Class Mself"""
    __identity = 'student'

    def __init__(self, name, age, sex):
        self.age = age
        self.name = name
        self.sex = sex

    def __set_identity(self):
        self.__identity = raw_input("hey ,hornored agent,choose an identity you want:")

    def __show(self):
        print "name:"+self.name
        print 'identity:'+self.__identity
        print 'age:%d' % self.age
        print 'sex:'+self.sex

    def who(self):
        self.__show()
        self.__set_identity()
m = Myself('YUli', 19, 'male')
m.who()
# Python不允许实例化的类访问私有数据，但你可以使用 object._className__attrName 访问属性
print m._Myself__identity


```

# 异常
1. 异常处理

语法：
try:
<语句>        #运行别的代码
except <名字>：
<语句>        #如果在try部份引发了'name'异常
except <名字>，<数据>:
<语句>        #如果引发了'name'异常，获得附加的数据
else:
<语句>        #如果没有异常发生