# 彻底搞清楚Python的装饰器


# 什么是装饰器


接[“闭包”是什么？](https://juejin.cn/post/6983491735288545287/)，我们可以认为装饰器就是一个闭包函数，同时它也返回了一个函数。



你也可以认为装饰器就是将函数作为参数传递到方法中，进行加工，再返回出来。


# 装饰器的使用场景

1、附加功能（统一日志格式，定时器）

2、数据的清理和添加（注入类似动态token的数据，修改清理内部数据）

3、函数注册等


# 装饰器的demo


# 1、实现函数在执行前后所花费的时间

装饰器的使用格式：@decorator

```py
# 定义装饰器
import time
def execTime(func):
    def inner(*args,**kwargs):    # 接收参数
        time1 = time.time()
        res = func(*args,**kwargs)
        time2 = time.time()
        print(func.__name__,'执行花费',time2-time1,'s')
        return res    # 返回func的返回值
    return inner  # 返回inner方法对象

# 在execAdd方法上使用execTime装饰器
@execTime
def execAdd(a,b):
    time.sleep(1)
    return a+b

# 调用execAdd
res = execAdd(1,2)
print(res)
```

**运行结果：**

```
python3 test.py
execAdd 执行花费 1.0000572204589844 s
3
```

# 2、实现日志的统一打印

```py
import time,logging
def execTime(func):
    def inner(*args,**kwargs):
        time1 = time.time()
        # 添加方法开始的日志
        logging.warning('now func {} start...'.format(func.__name__))
        res = func(*args,**kwargs)
        # 添加方法结束的日志
        logging.warning('now func {} finished...'.format(func.__name__))
        time2 = time.time()
        print(func.__name__,'执行花费',time2-time1,'s','\n')
        return res
    return inner

@execTime
def execAdd(a,b):
    time.sleep(1)
    return a+b

@execTime
def sayHi(name):
    print('hello,{}.'.format(name))

sayHi('phyger')
res = execAdd(1,2)
print(res)
```

**输出**

```py
python3 test.py
WARNING:root:now func sayHi start...
hello,phyger.
WARNING:root:now func sayHi finished...
sayHi 执行花费 0.00700068473815918 s

WARNING:root:now func execAdd start...
WARNING:root:now func execAdd finished...
execAdd 执行花费 1.0020573139190674 s

3
```

你会看到上面的两个方法在执行前后都会被增加开始和结束的告警日志，而且会统计方法的执行时间，通过这种方式我们可以方便快捷的对方法进行封装。


# 注意


当我们执行以下代码时：

```py
@execTime
def sayHi(name):
    print('hello,{}.'.format(name))
```

**输出**

```
python3 test.py
WARNING:root:now func sayHi start...
hello,phyger.
WARNING:root:now func sayHi finished...
sayHi 执行花费 0.018001317977905273 s

inner
```

sayHi方法的name竟然是装饰器的内函数的方法，这不是我们的期望结果啊。我们方法的name和注释被装饰器内函数重写了，我们怎么解决这个问题呢？



Python帮我提供了一个函数来解决这个问题，他就是functools.wraps。

我们重写装饰器来看看效果：

```py
from functools import wraps
import time,logging
def execTime(func):

    @wraps(func)
    def inner(*args,**kwargs):
        time1 = time.time()
        logging.warning('now func {} start...'.format(func.__name__))
        res = func(*args,**kwargs)
        logging.warning('now func {} finished...'.format(func.__name__))
        time2 = time.time()
        print(func.__name__,'执行花费',time2-time1,'s','\n')
        return res
    return inner
    
# 调用
sayHi('phyger')
print(sayHi.__name__)
```


**输出**

```
test.py
WARNING:root:now func sayHi start...
hello,phyger.
WARNING:root:now func sayHi finished...
sayHi 执行花费 0.003000020980834961 s

sayHi
```

你能看到，使用了装饰器的sayHi方法的__name__值已经是它自身的值了。



如果你想在当前装饰器的基础上再增加功能，那么你可能需要使用类装饰器，因为类的继承特性可以很好的解决你这个需求。关于类装饰器我们后面再介绍。

