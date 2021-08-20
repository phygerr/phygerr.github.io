# Python的封装继承多态和多重继承


> 相信你一定知道继承，多态和封装。封装通常是为了提供统一接口而将具体实现过程或者属性以方法或者类的方式对外呈现；继承就是子类继承父类从而拥有父类的方法和属性；多态是继承了同一个父类的不同子类分别重写了父类的某个方法而使得这个方法在不同的子类中有不同的实现。



多重继承即子类继承多个父类，拥有多个父类的方法和属性。



# 1、封装



比如我们想实现输入两个数字就可以计算其乘积。



## 第一种方式：

```py
def ret2x(x,y):
    sum=0
    while x>0:
        sum+=y
        x-=1 
    return sum
>>> ret2x(2,8) 
16
>>> ret2x(90,8) 
720
>>>
```

## 第二种方式：

```py
def ret2x(x,y):
    return x*y
>>> ret2x(2,8) 
16
>>> ret2x(90,8) 
720
>>>
```

可以看到执行结果一毛一样，对于使用者来说，不关注也看不到ret2x的具体实现，只需要调用拿到结果即可。



# 2、继承



## 定义Chinese类继承Human类：

```py
class Human(object):
    hum = '人类'

    def kind(self):
        print("人类...")

class Chinese(Human):
    chin = '中国人'
```

执行：

```py
>>> from payhlib import Chinese
>>> c = Chinese()
>>> c.hum
'人类'
>>> c.chin
'中国人'
>>> c.kind()
人类...
>>>
```

Chinese类继承了Human类，所以Chinese的对象拥有了Human父类的hum属性和kind方法。



# 3、多态



## 继续在继承的基础上进行演示：

```py
class Human(object):
    hum = '人类'

    def kind(self):
        print("人类...")

    def country(self):
        pass

class Chinese(Human):
    chin = '中国人'

    def country(self):
        print('北京')

class Japanese(Human):
    jap = '曰笨人'

    def country(self):
        print('冻京')
Chinese类和Japanese类分别实现了父类Human的country方法。
```


执行：

```py
>>> from payhlib import *
>>> a = Chinese()
>>> b = Japanese()
>>> a.country()
北京
>>> b.country()
冻京
>>> a.kind()
人类...
>>> b.kind()
人类...
>>>
```

中国人和曰笨人都是人类，但是中国的首都是北京，曰笨的首都是冻京。



# 4、多重继承



讲了这么多，现在进入正题，我们都知道世界上人类按照性别可以分为男和女。如果我们于上面的Chinese类和Japanese增加性别相关属性和方法，就可以通过多重继承实现。


```py
class Human(object):
    hum = '人类'

    def kind(self):
        print("人类...")

    def country(self):
        pass

class Sex(object):
    summary = '性别类'

    def male(self):
        print('男人')

    def female(self):
        print('女人')

class Chinese(Human,Sex):
    chin = '中国人'

    def country(self):
        print('北京')

class Japanses(Human,Sex):
    jap = '曰笨人'

    def country(self):
        print('冻京')
```

执行：

```py
>>> from payhlib import *
>>> a = Chinese()
>>> b = Japanses()
>>> a.kind()
人类...
>>> b.kind()
人类...
>>> a.male()
男人
>>> b.female()
女人
>>> a.hum
'人类'
>>> a.summary
'性别类'
>>>
```

Chinese类即拥有Human类的方法属性，也拥有Sex类的方法和属性。



## 多重继承+多态的效果：

```py
class Human(object):
    hum = '人类'

    def kind(self):
        print("人类...")

    def country(self):
        pass

class Sex(object):
    summary = '性别类'

    def male(self):
        print('男人')

    def female(self):
        print('女人')

class Chinese(Human,Sex):
    chin = '中国人'

    def country(self):
        print('北京')

    def male(self):
        print('中国男人')

    def female(self):
        print('中国女人')

class Japanses(Human,Sex):
    jap = '曰笨人'

    def country(self):
        print('冻京')

    def male(self):
        print('曰笨男人')

    def female(self):
        print('曰笨女人')
```            

执行：

```py
>>> from payhlib import *
>>> a = Chinese()  
>>> b = Japanses()
>>> a.kind()
人类...
>>> b.kind()   
人类...
>>> a.country()
北京
>>> b.country() 
冻京
>>> a.male()
中国男人
>>> b.male() 
曰笨男人
>>> a.female() 
中国女人
>>> b.female() 
曰笨女人
>>> a.summary  
'性别类'
>>> b.summary 
'性别类'
>>>
```

Chinese类和Japanese类同时继承了Human类和Sex类，所有Chinese的对象和Japanese的对象就拥有了Human和Sex的属性和方法，但是他们又分别重写了父类的country和male即female方法。这种多重继承的方式也称MixIn（混入）。

