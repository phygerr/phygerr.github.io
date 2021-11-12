# Python装饰器进阶（类装饰器+带参数的装饰器+多装饰器）


接[【简明】彻底搞清楚Python的装饰器](https://juejin.cn/post/6983494077782163464)，我们继续介绍类装饰器+带参数的装饰+多装饰器，顾名思义类装饰器就是类闭包。

# 定义一个类装饰器


需求：实现一个类装饰器，能够在方法执行时打印日志，并且发送通知到指定地方。

```py
from functools import wraps

class logAndNotify(object):

    # 初始化，定义日志路径
    def __init__(self,logfile='service.log'):
        self.logfile = logfile
    
    # 使类成为可调用对象
    def __call__(self,func):

        @wraps(func)
        def wrap_func(*args,**kwargs):
            info = func.__name__+'was called'

            # 实现写日志
            with open(self.logfile,'a') as f:
                f.write(info+'\n')
            
            # 实现通知
            self.notify()

            return func(*args,**kwargs)
        return wrap_func
    
    def notify(self):
        print('notify has been send...')

@logAndNotify()
def sayHi(name):
    print('hello',name,'!')

res = sayHi('phyger')
print(res)
```

**执行结果**：

```
➜ RemoteWorking git:(master) ✗ /usr/bin/python3 /root/RemoteWorking/test/test.py
notify has been send...
hello phyger !
None
```



# 类装饰器功能扩展

如果我们想要在此类装饰器的基础上，增加发送邮件的功能，就可以利用类的继承特性来实现。

```py
from functools import wraps


class logAndNotify(object):

    # 初始化，定义日志路径
    def __init__(self, logfile="service.log"):
        self.logfile = logfile

    # 使类成为可调用对象
    def __call__(self, func):
        @wraps(func)
        def wrap_func(*args, **kwargs):
            info = func.__name__ + "was called"

            # 实现写日志
            with open(self.logfile, "a") as f:
                f.write(info + "\n")
            # 实现通知
            self.notify()

            return func(*args, **kwargs)

        return wrap_func

    def notify(self):
        print("notify has been send...")


class NewWarp(logAndNotify):

    # 初始化邮件地址
    def __init__(self, email_address='phyger@qq.com', *args, **kwargs):
        self.email_address = email_address
        super(NewWarp,self).__init__(*args, **kwargs)

    # 重写notify方法
    def notify(self):
        print("notify has been send...")
        print('email sended...to',self.email_address)
    

@NewWarp()
def sayHi(name):
    print("hello", name, "!")


res = sayHi("phyger")
print(res)
```

**执行结果**：


```
➜ RemoteWorking git:(master) ✗ /usr/bin/python3 /root/RemoteWorking/test/test.py
notify has been send...
email sended...to phyger@qq.com
hello phyger !
None
```

# 带参数的装饰器

当我们需要根据不同的场景对函数进行不同的装饰操作的时候，我们需要使用到带参数的装饰器。

例：日志级别控制

```py
import logging
from functools import wraps


def logg(level):
   
    def mid(func):
        @wraps(func)
        def inner(*args, **kwargs):
            # log设置
            #logging.basicConfig(format=' %(asctime)s - %(levelname)s -%(message)s')
            logging.basicConfig(format = '"%(asctime)s - %(filename)s[line:%(lineno)d] - %(levelname)s: %(message)s"')
            logger = logging.getLogger()
            logger.setLevel(level)

            # logger打印
            logger.info('{} start...'.format(func.__name__))
            logger.error('{} errors...'.format(func.__name__))
            logger.warn('{} warnning...'.format(func.__name__))
            logger.debug('{}end...'.format(func.__name__))
            return func(*args, **kwargs)
        return inner
    return mid

@logg(level='DEBUG')
def sayHi(name):
    print('hi,',name)

@logg(level='INFO')
def sayBye(name):
    print('bye',name)

sayHi(name='phyger')
sayBye(name='phyger')
```            

**执行输出**：


```
➜ RemoteWorking git:(master) ✗ /usr/bin/python3 /root/RemoteWorking/test/test.py
"2020-10-31 11:23:42,161 - test.py[line:15] - INFO: sayHi start..."
"2020-10-31 11:23:42,161 - test.py[line:16] - ERROR: sayHi errors..."
"2020-10-31 11:23:42,162 - test.py[line:17] - WARNING: sayHi warnning..."
"2020-10-31 11:23:42,162 - test.py[line:18] - DEBUG: sayHiend..."
hi, phyger
"2020-10-31 11:23:42,162 - test.py[line:15] - INFO: sayBye start..."
"2020-10-31 11:23:42,162 - test.py[line:16] - ERROR: sayBye errors..."
"2020-10-31 11:23:42,162 - test.py[line:17] - WARNING: sayBye warnning..."
bye phyger
```

**可以看到**：

- 当设置最高级别ERROR的时候，所有级别的日志都打印。

- 当设置INFO级别的的时候，DEBUG最低级别的日志不打印。


# 多装饰器


当有多个不能够耦合的功能需要在函数上增加时，我们需要使用多个装饰器，怎么用呢？

例：实现日志和发送通知的分离

```py
import logging
from functools import wraps


def wrap1(func):
    def inner1(*args, **kwargs):
        print('start')
        func(*args, **kwargs)
        print('end')
        return True
    return inner1

def wrap2(func):
    def inner2(*args, **kwargs):
        print("msg has sended...")
        func(*args, **kwargs)
        return True
    return inner2


@wrap1
@wrap2
def sayHi(name):
    print('hi',name)

sayHi(name='phyher')
```            

**执行输出**：


```
➜ RemoteWorking git:(master) ✗ /usr/bin/python3 /root/RemoteWorking/test/test.py
start
msg has sended...
hi phyher
end
```
