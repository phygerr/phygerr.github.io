# Python的闭包是什么？


# 什么是闭包


Python中的闭包是一个比较模糊的概念，有很多朋友都认为不好理解，但是随着深入学习，就会发现闭包无论如何都是需要去理解的，下面我将自己对闭包的理解进行阐述，希望能够对你有所帮助 ~



我们可以将闭包理解为一种特殊的函数，这种函数由两个函数的嵌套组成，且称之为外函数和内函数，外函数返回值是内函数的引用，此时就构成了闭包。





# 闭包的格式



如下：

```py
def 外层函数(参数):
    def 内层函数():
        print("内层函数执行", 参数)

    return 内层函数


内层函数的引用 = 外层函数("传入参数")
内层函数的引用()
```

外层函数中的参数，不一定要有，据情况而定，但是一般情况下都会有并在内函数中使用到



# 闭包的实例


如下：

```py
def outfunc(a):   # 定义外函数

    def infunc(b):  # 定义内函数
        return a*b  # 内函数的返回值

    return infunc   # 外函数的返回值，返回内函数的对象

func_instance = outfunc(8)   # 外函数的实例，是一个function对象
print(type(func_instance))   # 打印外函数实例的类型
res = func_instance(10)      # 外函数实例的调用
print(res)
```

**输出**

```py
➜  test git:(master) ✗ python3 testpy.py
<class 'function'>
80
```

在上面的代码中，内函数直接使用了外函数的变量值，那如果想要在内函数中对外函数的变量值进行修改，怎么操作呢？


# 修改外函数的变量值


想要修改外函数的变量值，需要用到nonlocal关键字。

```py
def outfunc(a):

    def infunc(b):
        nonlocal a
        a = a*2
        return a*b

    return infunc

func_instance = outfunc(8)
print(type(func_instance))
res = func_instance(10)
print(res)
```

**输出**

```
➜  test git:(master) ✗ python3 testpy.py
<class 'function'>
160
```

如上即可。


# 闭包的使用场景


Python中，闭包的主要用途就是用于装饰器的实现。后续讲解。


还有就是可以简化参数重复传递，比如：

```py
def add(a,b,c):
    print(a*b*c)

add(1,2,1)
add(1,2,2)
add(1,2,3)
add(1,2,4)
add(1,2,5)
```

**输出**

```py
➜  test git:(master) ✗ python3 testpy.py 
2
4
6
8
10
```

你会发现，a和b是固定不变的，我们怎么样才能减少a和b的传参，而只改变c的值呢？这个时候闭包就起到了作用。


```py
def addNew(a,b):

    def addC(c):
        return a*b*c

    return addC
            
func_ins = addNew(1,2)
print(func_ins(1))
print(func_ins(2))
print(func_ins(3))
print(func_ins(4))
print(func_ins(5))
```

**输出**

```
➜  test git:(master) ✗ python3 testpy.py
2
4
6
8
10
```

