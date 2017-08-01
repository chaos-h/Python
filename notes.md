#Notes for Python
## Basics
1.字典的迭代
	默认情况下，dict迭代的是key,假如有一个字典d，key的迭代可以`for key in d`。如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`。
2. 判断一个对象是否可迭代
	通过collections模块的Iterable类型判断。
	```
	from collections import Iterable
	isinstance('abc', Iterabe)
	```
3.生成器
>不创建完整的list,一边循环一边计算的机制，称为生成器：generator。

类似于一次存储单个值的列表，用`next()`函数一次获取一个值，generator可迭代，也可以通过循环的方式取值。

+ 生成生成器的两种方法
	- 方法一：和生成列表的式子一样，但是`[]`变成`（）`
	    ```python
	    l = (x or x in range(10))
	    ```
	- 方法二：(yied + 函数)这个时候不叫函数，叫生成器, 返回的是生成器变量
	`yield 是一个类似 return 的关键字，迭代一次遇到yield时就返回yield后面的值。重点是：下一次迭代时，从上一次迭代遇到的yield后面的代码开始执行`

	```python
	def fib(max):
	    n, a, b = 0, 0, 1
	    while n < max:
	        yield b
	        a, b = b, a + b
	        n = n + 1
	    return 'done'
	```
	变成generator的函数，在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。
+ 访问
	- next()
	`generator保存的是算法，每次调用next(l)，就计算出l的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出StopIteration的错误。`
	```python
	r = next(l) # r = 0
	r = next(l) # r =1
	```
	- loop
	```python
	for x in  l:
		print(x)
	```
+ 取得生成器的返回值
	用for循环调用generator时，发现拿不到generator的return语句的返回值。如果想要拿到返回值，必须捕获StopIteration错误，返回值包含在StopIteration的value中
```python
while True:
        try:
            x = next(g)
            print('g:', x)
        except StopIteration as e:
            print('Generator return value:', e.value)
            break
```
4. 迭代器

> 可以被next()函数调用并不断返回下一个值的对象称为迭代器：Iterator。
同样可以用isinstance()判断一个对象是否是Iterator对象。

`生成器都是Iterator对象，但list、dict、str虽然是Iterable，却不是Iterator。把list、dict、str等Iterable变成Iterator可以使用iter()函数`
Iterator是惰性计算的序列，所以我们可以用Python表示“全体自然数”，“全体素数”这样的序列，而代码非常简洁。例子见`fileter`部分的求素数函数。

5. 函数式编程
	函数式编程就是一种抽象程度很高的编程范式，纯粹的函数式编程语言编写的函数没有变量，因此，任意一个函数，只要输入是确定的，输出就是确定的，这种纯函数我们称之为没有副作用。而允许使用变量的程序设计语言，由于函数内部的变量状态不确定，同样的输入，可能得到不同的输出，因此，这种函数是有副作用的。

	函数式编程的一个特点就是，允许把函数本身作为参数传入另一个函数，还允许返回一个函数！

Python对函数式编程提供部分支持。由于Python允许使用变量，因此，Python不是纯函数式编程语言。
	+ 高阶函数
		- 函数名是一个变量
		```python
		f = abs
		f(-2) # equal to abs(-2)
		abs = 10
		abs(-8)# here erro comes for abs now is a int , 10
		```
		- 高阶函数
		既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。
		```python
		def add(x, y, f):
		    return f(x) + f(y)
		add(5, -6, abs)
		```
		编写高阶函数，就是让函数的参数能够接收别的函数。
	+ map/reduce
		- map(func,Iterable)
		map()函数接收两个参数，一个是函数，一个是Iterable，map将传入的函数依次作用到序列的每个元素，并把结果作为新的Iterator返回。
		```python
		def f(x):
		        return x * x
		r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
		# r is a iterator, you could change it into list by list(r)
		```
		- reduce(func, list)
		reduce把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算，其效果就是：`reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)`
		```python
		from functools import reduce
		    def add(x, y):
		        return x + y
		reduce(add, [1, 3, 5, 7, 9]) # 25
		```
	+ filter
		和map()类似，filter()也接收一个函数和一个序列。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素,返回对象是Iterator。
		```python
		def not_empty(s):
		    return s and s.strip()
		list(filter(not_empty, ['A', '', 'B', None, 'C', '  ']))
		```
			- 用filter求素数(埃氏筛法)
			```
			def _odd_iter():
			    n = 1
			    while True:
			        n = n + 2
			        yield n
			def _not_divisible(n):
				return lambda x: x % n > 0
			def primes():
			    yield 2
			    it = _odd_iter() # 初始序列
			    while True:
			        n = next(it) # 返回序列的第一个数
			        yield n
			        it = filter(_not_divisible(n), it) # 构造新序列
			#注意到primes()是一个无限序列
			```
	+ sorted
		- 可对list排序，默认升序， 返回一个list
		`sorted([25,38,-9,76])`
		- `sorted()`是高阶函数，可以接收`key`函数来实现自定义排序，`key`将作用于list里面每个元素，如对按绝对值排序
		`sorted([25,38,-9,76], key = abs)`
		-  字符串按ASCII大小，'Z' < 'a' ，忽略大小写如下
		`sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower)`
		- 要进行反向排序，不必改动key函数，可以传入第三个参数`reverse=True`
		`sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)`
	+ 返回函数
		- 一个函数可以返回一个计算结果，也可以返回一个函数。
		```python
		def lazy_sum(*args):
		    def sum():
		        ax = 0
		        for n in args:
		            ax = ax + n
		        return ax
		    return sum
		f = lazy_sum()
		m = f()#这个时候才计算结果
		```
		**注意**:`调用函数f时，才真正计算求和的结果`
		在函数lazy\_sum中又定义了函数sum，并且，内部函数sum可以引用外部函数lazy\_sum的参数和局部变量，当lazy_sum返回函数sum时，相关参数和变量都保存在返回的函数中，这种程序结构称为“闭包（Closure）”
		`当我们调用lazy_sum()时，每次调用都会返回一个新的函数，即使传入相同的参数`
		```
		 f1 = lazy_sum(1, 3, 5, 7, 9)
		 f2 = lazy_sum(1, 3, 5, 7, 9)
		 f1==f2 #False
		```
		- **返回一个函数时，牢记该函数并未执行，返回函数中不要引用任何可能会变化的变量,特别注意循环变量。**
		```python
		def count():
		    fs = []
		    for i in range(1, 4):
		        def f():
		             return i*i
		        fs.append(f)
		    return fs
		pass
		f1, f2, f3 = count() # 三个函数调用的结果都是9,因为它们在调用的时候才执行，那个时候引用的变量`i`已经变成了3
		```
		**解决：**如果一定要引用循环变量，那就得再创建一个函数，用该函数的参数绑定循环变量当前的值，无论该循环变量后续如何更改，已绑定到函数参数的值不变
		```python3
		def count():
		    def f(j):
		        def g():
		            return j*j
		        return g
		    fs = []
		    for i in range(1, 4):
		        fs.append(f(i)) # f(i)立刻被执行，因此i的当前值被传入f()
		    return fs
		```
	+ 匿名函数 `lambda`
		`lambda x：f(x) ` f(x)是关于x的一个表达式，只能有一个，返回值局势表达式的结果。
		匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量，再利用变量来调用该函数。
		```python3
		f = lambda x: x * x
		f(3)
		```
		也可以把匿名函数作为返回值返回
		```python3
		def build(x, y):
		    return lambda: x * x + y * y
		```
	+ 装饰器 Decorator
		- 定义
		本质上，decorator就是一个返回函数的高阶函数, 是在代码运行期间动态增加功能的方式。
		```python3
		'''定义一个能打印日志的decorator'''
		def log(func):
		    def wrapper(*args, **kw):
		        print('call %s():' % func.__name__)
		        return func(*args, **kw)
		    return wrapper
		```
		- 使用
		Python的@语法，把decorator置于函数的定义处即可
		```python
		@log
		def now():
		    print('2015-3-25'）
		 # 调用now()的时候，会先打印"call now()",相当于执行了语句：now = log(now)
		```
		如果decorator本身需要传入参数，那就需要编写一个返回decorator的高阶函数，写出来会更复杂。
		```python3
		def log(text):
		    def decorator(func):
		        def wrapper(*args, **kw):
		            print('%s %s():' % (text, func.__name__))
		            return func(*args, **kw)
		        return wrapper
		    return decorator
		```
		使用
		```
		@log('execute')
		def now():
		    print('2015-3-25')
		#相当于now = log('execute')(now)
		```
		**注意：**返回的那个wrapper()函数名字就是'wrapper'，所以，需要把原始函数的\__name__等属性复制到wrapper()函数中，否则，有些依赖函数签名的代码执行就会出错。
		**解决：**使用Python内置的functools.wraps，定义wrapper()的前面加上@functools.wraps(func)即可。
		所以，完整的写法应该是
		```
		# 不带参数
		```python3
		import functools
		def log(func):
		    @functools.wraps(func)
		    def wrapper(*args, **kw):
		        print('call %s():' % func.__name__)
		        return func(*args, **kw)
		    return wrapper
		```
		```python3
		# 带参数
		def log(text):
		    def decorator(func):
		        @functools.wraps(func)
		        def wrapper(*args, **kw):
		            print('%s %s():' % (text, func.__name__))
		            return func(*args, **kw)
		        return wrapper
		    return decorator
		```
	+ 偏函数
		当函数的参数个数太多，需要简化时，使用functools.partial可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单
		```
		int2 = functools.partial(int, base=2)
		int2('1000000')#相当于int2('1000000', base = 2)
		max2 = functools.partial(max, 10)
		max2(5,6,7)#相当于arg = (10,5,6,7),max(*arg)
		```













## builtin_function and module
1.  enumerate
`enumerate 函数可以可以把一个list变成索引-元素对，这样就可以在for循环中同时迭代**索引**和**元素**本身`
可以以此模仿c或java的下标循环。
```python
for  i, value in enumerate(['a', 'b', 'c']):
        print(i,value)
```
