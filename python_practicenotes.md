#python_practice notes
> Pick up some notes when practicing python on hackrank website.Some interesting things and tips maybe.

## basis
1. assignment 
`var, var1, var2 = 1, 2, 3`

2. the difference with division and print function between python 2 and python 3

- division
[division problem](https://www.hackerrank.com/challenges/python-division/tutorial)

- print
[print distinction](https://www.hackerrank.com/challenges/python-print/tutorial)


## tips
1. input 
- n integers in a line
example: 1 2 3 4 5
`integer_list = map(int, input().split())`
*this is in python2,for python3 ,the map fuction return a map object rather than a list*
- dictionary like input
example :mary 12 14 15
`name, *line = input().split()`



2. Another awesome use of tuples is as keys in a dictionary. In other words, tuples are hashable.

3.  List Comprehensions 
[ List Comprehensions ](https://www.hackerrank.com/challenges/list-comprehensions)
[or this](http://treyhunner.com/2015/12/python-list-comprehensions-now-in-color/)
- mode 1
[ expression-involving-loop-variable for loop-variable in sequence ]
- mode 2
[ expression-involving-loop-variables for outer-loop-variable in outer-sequence for inner-loop-variable in inner-sequence ]
- mode 3
[ expression-involving-loop-variable for loop-variable in sequence if boolean-expression-involving-loop-variable ]


```python
# mode1
ListOfNumbers = [ x for x in range(10) ] # List of integers from 0 to 9 
# mode 2
ListofNumbers = [ x for rows in data for x in rows]
# mode 3
ListOfThreeMultiples = [x for x in range(10) if x % 3 == 0] # Multiples of 3 below 10
```

4. sort() can set the key&inverse to design your own sort



## built-in functions

1. eval
>The eval function lets a python program run python code within itself.
```python
if __name__ == '__main__':
    N = int(input())
    List = []
    for x in range(N):
        line = input().split(' ')
        cmd = line[0]
        paras = line[1:]
        if cmd == 'print' :
            print(List)
        else:
            cmd += '('+','.join(paras)+')'
            eval('List.'+cmd)
```

2.map()

>map(function, iterable, ...)	
Apply function to every item of iterable and return a list of the results.

[detail](https://my.oschina.net/zyzzy/blog/115096)
map(f, iterable)
基本上等于：
[f(x) for x in iterable]
*this is in python2,for python3 ,the map fuction return a map object rather than a list,but a map object is iterable*

3. filter()
[Python filter()](https://www.programiz.com/python-programming/methods/built-in/filter)

```
The filter() method is equivalent to:

# when function is defined
(element for element in iterable if function(element))

# when function is None
(element for element in iterable if element)
```
4. any(iterable) and all(iterable)
the former return True if there exists some elements that are true,the latter return true only all elements are True.

5. getattr()

>getattr(object, name[, default]) -> value
Get a named attribute from an object; getattr(x, 'y') is equivalent to x.y.
When a default argument is given, it is returned when the attribute doesn't
exist; without it, an exception is raised in that case.

```python
s = [3,5,5]
getattr(s,"sort") #is equivalent to s.sort()
```

## modules

1. textwrap
String associated module,contains two convenient functions,textwrap.wrap()and textwrap.fill().

The wrap() function wraps a single paragraph in text (a string) so that every line is width characters long at most.It returns a list of output lines.
The fill() function wraps a single paragraph in text and returns a single string containing the wrapped paragraph.



## else

1. hash()

>A hash function is any function that can be used to map data of arbitrary size to data of fixed size.

2. program_thinking
whenever there is a problem that requires a solution,alway think the extreme answer first.
(思考问题的时候总是要先考虑特殊情况) 
