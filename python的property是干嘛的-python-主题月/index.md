# Python的@property是干嘛的？


通常，当我们需要对对象的敏感属性或者不希望外部直接访问的属性进行私有化，但是某些时候我们又需要对这些私有属性进行修改，该怎么处理呢？

# 1、几个概念

- \_a(前置单下划线)，这种属性仅表示约定的私有，非真正的私有。
- \__a(前置双下划线)，这种属性表示私有，无法在外部访问。
- \__a__(前后双下划线)，这种属性标识系统属性。(可选)
- a_(后置单下划线)，这种属性是为了避免和保留关键字冲突。(可选)

# 2、举个例子

## 定义一个类：

```py
class Student(object):

    _sex='male'

    __age=0
```

执行：（私有属性无法在外部访问）

```py
>>> stu = Student()
>>> stu._sex
'male'
>>> stu.__age
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Student' object has no attribute '__age'
>>>
```

# 3、解决问题

从上面的类中我们可以看到，私有属性无法在类实例中访问，怎么办呢？当我们需要对类的私有属性__age进行查询和修改的时候，我们可以定义get_age和set_age去实现。

```py
class Student(object):

    _sex='male'

    __age=0

    def get_age(self):
        return self.__age

    def set_age(self,age):
        self.__age = age
```

执行：

```py
>>> stu = Student()
>>> stu.get_age()   
0
>>> stu.set_age(18) 
>>> stu.get_age()   
18
>>>
```

# 4、换个方法

但是上面的这种方式略显复杂，如果在私有属性较多的类中就不太适用了，所以我们期望寻求一种更简单的方式去解决这个问题，比如将这个私有属性转化为另一个属性。告诉你个好消息，Python已经帮我们实现了，这就是@property。

```py
class Student(object):

    _sex='male'

    __age=0

    def get_age(self):
        return self.__age

    def set_age(self,age):
        self.__age = age
    
    @property
    def age(self):
        return self.__age
```

执行：

```py
>>> from payhlib import Student
>>> s = Student()
>>> s.age
0
>>> s.set_age(19)
>>> s.age
19
>>
```

在上面我们将__age私有属性转换为了age属性，你可能会想，既然私有属性转换为了属性，那我们是不是可以直接修改它呢？答案是不行，因为property虽然将__age转换为了属性，但是其不具备setter功能，需要我们去添加。

```py
>>> from payhlib import Student
>>> s = Student()
>>> s.age  
0
>>> s.age=20
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: can't set attribute
>>>
```

添加setter方法

```py
class Student(object):

    _sex='male'

    __age=0

    def get_age(self):
        return self.__age

    def set_age(self,age):
        self.__age = age
    
    @property
    def age(self):
        return self.__age
    
    @age.setter
    def age(self,value):
        self.__age=value
```

执行：

```py
>>> from payhlib import Student
>>> s = Student()
>>> s.age
0
>>> s.age=20
>>> s.age    
20
>>>
```

到此，@peoperty分享完毕，关于它的实现原理你可以查看源码进行研究。
图片


