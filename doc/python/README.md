#Python - 学习笔记

## 1. 简介
适合的领域：
- Web网站和各种网络服务；
- 系统工具和脚本；
- 作为胶水预言把其他语言开发模块包装起来方便使用；
- 跨平台；

不适合的领域：
- 贴近硬件的代码；
- 移动开发；
- 游戏开发；


缺点：
- 不能加密；
- 运行速度慢；

版本：
- `2.7`：第三方库较多；
- `3.3` ：语法和2.7版本不兼容；

## 2. 变量和数据类型
### 2.1 基本数据类型
- 整数：`1`, `100`, `-100`;
- 浮点数：`1.2`, `3.14`, `1.23e9`;
- 字符串：`'str'`,`"abcd"`;
- 空值：`None`;
- 布尔值：`False`,`True`,`and`,`or`,`not`;

### 2.2 注释
注释用`#`作为开头：
``` python
# 这是一些注释
# print 'hello world'
```

### 2.3 变量
- 变量名必须是大小写英文、数字和下划线（_）的组合，且不能用数字开头。
- 变量本身的类型是不固定的，是一种动态语言；
``` python
a = 123    # a是整数
print a
a = 'imooc'   # a变为字符串
print a
```

### 2.4 字符串
- 单引号或双引号包围的文本为字符串；
- 特殊字符需要使用转义符号；
- 在字符串前加前缀`r`表示`raw`字符串，里面的字符都不需要转义了；
- 在字符串前加前缀`u`表示`unicode`字符串，支持中文等编码；
- 可以用`'''str'''`表示多行字符串；
- 可以用`# -*- coding: utf-8 -*-`指定字符`UTF-8`，以便支持中文；必须写在文件的第一行；
- 可以用`str[index]`访问字符串的某一个字符；
- 可以用`str[start:end:step]`对字符串进行切片；
``` python
# 指定字符编码
# -*- coding: utf-8 -*-
# 基本字符串
str = 'Learn "Python" in imooc'
# raw字符串
str = 'Line 1\nLine 2\nLine 3'
# 多行字符串
str = '''Line 1
Line 2
Line 3'''
```

### 2.5 整数和浮点数
- 支持基本的四则运算；
- 有小数点的数字为浮点数；
- 整数之间的计算结果为整数，整数和浮点数的运算结果为浮点数；
``` python
1 + 2    # ==> 整数 3
1.0 + 2.0    # ==> 浮点数 3.0
```

### 2.6 布尔类型
- 只有`True`和`False`两个取值；
- `0`,`空字符串`,`None`当做`False`看待；
- 短路计算；
``` python
a = True
print a and 'a=T' or 'a=F' # ==> a=T
```
## 3.  集合
### 3.1 list
- 定义列表
	- `list`是一种有序集合，可以新增，删除元素；
	- 使用`[ ]`可以定义一个`list`对象；
	- `list`中的元素不要求是相同的数据类型；
- 访问列表
	- 可以使用下表索引访问列表`list[1]`，索引从0开始，注意不要越界；
	- 可以使用负数的`倒序索引`访问列表`list[-1]`，即为倒数第一个元素；
	- `len(list)`可以计算列表的长度；
- 切片
	- `L[m:n]`：索引m到n的元素，不包括n；
	- `L[:]`全部元素；
	- `L[:n]`小于n的元素；
	- `L[m:]`大于m的元素；
	- `L[m:n:x]`：从m开始，每x个元素取一个数，直到n；
	- 倒序切片，第一个元素是`-1`；
- 操作列表
	- 使用`append(e)`在列表的尾部加入元素；
	- 使用`insert(index,e)`在列表中加入元素；
	- 使用`pop()`方法可以删掉`list`的最后一个元素，并返回最后一个元素；
	- 使用`pop(index)`方法可以删掉指定下标的元素；
- 列表生成
	- `[x * x for x in range(1, 11)]`：生成列表，不包括最后一个元素；
	- `[generate_tr(name, score) for name, score in d.iteritems()]`：生成表达式可以是函数；
	- `[ x.upper() for x in L if isinstance(x, str)]`：可以加条件判断过滤；
``` python
# 定义list
L = ['Adam', 95.5, 'Lisa', 85, 'Bart', 59]
# 下标访问
print L[0]
print L[-1]
# 操作元素
L.insert(2, 'Paul')
L.append('Jack')
L.pop()
```

### 3.2 tuple
- `tuple`为只读的列表，一旦创建就不能修改了；
- `tuple`使用`( )`进行定义；
- 使用`t[1]`访问元组的元素；
- 定义单元数元组需要多加一个逗号`(0, )`
```python
# 定义tuple
t = (0,1, 2, 3, 4, 5, 6, 7, 8, 9)

# 单元素元组
t = (0, )
```

### 3.3 dict
- `dict`就是哈希表，使用花括号`{ key:value,key:value}`语法定义；
- 使用`dict[key]`访问`dict`的元素，`key`不存在会报错；
- 使用`dict.get(key)`访问`dict`元素，`key`不存在会返回`None`；
- 使用`dict.pop(key)`返回并删除一个元素；
- 可以使用`for key in dict`遍历`dict`；
- 可以使用`for key, value in dict.itmes()`遍历`dict`；
- 可以使用`for k, v in kwargs.iteritems()`遍历`dict`;
- `dict.values() `获取值的列表；
- 

``` python
# 定义dict
d = {
    'Adam': 95,
    'Lisa': 85,
    'Bart': 59
}
# 访问dict
 d.get('Adam')
 d['Lisa']
# 判断key是否存在
'Adam' in d
# 遍历dict
for k in d:
    print k, d[k]
# 遍历dict
for k, v in d.items():
    print k, v
```

### 3.4 set
- `set`和`list`类似，但是`set`是无序的，且元素不能重复；
- 使用`set(list)`定义一个`set`；
- 使用`s.remove(item)`删除一个元素；
- 使用`s.add(item)`加入一个元素；
- 访问`set`的元素，其实就是判断元素是否在`set`中；
- 可以使用`for key in set`遍历`set`

``` python
# 定义
s = set(['A', 'B', 'C'])
# 访问
'A' in set
# 遍历

```

## 4. 条件判断和循环
### 4.1 if
>缩进规则：相同缩进的代码为代码块；4个空格；

- `if`语句后为布尔表达式，用`:`表示代码块开始；
- 可以使用`if-elif-else`格式；
- 可以使用表达式形式`c = a if a>b else b`；
``` python
if score >= 90:
    print 'excellent'
elif score >= 80:
    print 'good'
elif score >=60:
    print 'passed'
else:
    print 'failed'

# 单行形式
(t2 - t1) * 1000 if unit=='ms' else (t2 - t1)
```

### 4.2 for 循环
- 可以采用`for in`关键词遍历列表或元组；
- 可以使用`break`退出循环；`continue`继续循环；
``` python
L = [75, 92, 59, 68]
sum = 0.0
for v in L:
    sum += v
print sum / 4
```

### 4.3 while 循环
- 和其他语言一样，根据布尔表达式判断是否继续循环；
- 可以使用`break`退出循环；`continue`继续循环；
``` python
while x <= 100:
    sum += x
    x += 1
print sum
```

## 5. 函数
### 5.1 常用函数
####5.1.1 内置函数：
- `cmp(x, y)`：比较函数；
- `int()`：转换为整数；
- `float()`：转换为浮点数；
- `str()`：转换为字符串；
- `len()`：求集合长度；
- `zip(seq1,seq2)`：将两个集合合并成一个，每个元素是一个元组；
- `range(start,top,setp)`：创建序列；
- `enumerate(iterable)`：将集合的每个元素变成有序号的元组；
- `isinstance(x, str)`：判断变量的类型；

#### 5.1.2 math
- `math.sqrt(x)`:平方根；

#### 5.1.3 str
可以在`str`上调用也可以直接在字符串上调用；
- `lower(s)`
- `upper(s)`
- `strip(s, chars)`：前后去除指定字符；

#### 5.1.4 time
- `time()`：当前时间；

### 5.1.5 os.path
- `isdir()`
- `isfile()`

### 5.2 定义函数
- 使用`def`关键词定义一个函数，依次写出函数名、参数、冒号；
- 使用`retutn`语句进行返回；
- 可以返回多值`return x, y`，实际上是一个`tuple`；
- 可以定义默认参数`def fun(x=0)`，默认参数只能定义在必须参数后面；
- 可以定义可变参数`def fun(*args)`，实际上就是传入一个`tuple`；

```
# 定义函数
def square_of_sum(L):
    sum = 0
    for i in L:
        sum += i * i
    return sum
# 返回多值
def swap(a, b):
    return b, a
x, y = swap(1, 10)
# 默认参数
def incr(v=0):
    v += 1
    return v
```

## 6.  函数式编程
### 6.1 特点
- 把计算视为函数而非指令；
- 纯函数式编程：不需要变量，没有副作用，测试简单；
- 支持高阶函数，函数可以作为变量传入，代码简洁；
- 支持闭包，能够返回函数；
- 有限度的支持匿名函数；

### 6.2 高阶函数
- 变量可以指向函数，可以对变量进行调用；
- 函数名其实就是指向函数的变量；
- 高阶函数：能够接受函数作为参数的函数；
- 函数可以作为返回值；
``` python
def fun(x, y, f):
    return f(x) + f(y)
# 将abs函数作为参数传入
print fun(1, -2, abs)
```

### 6.3 内置高阶函数
- `map(function, sequence)`：将函数作用于每个对象，得到一个新的集合；
- `reduce(function sequence)`：对list的每个元素反复调用函数f，并返回最终结果值；
- `fliter(function, sequence)`：对于list的每个元素，检查其是否满足函数f，返回满足的元素list；
- `sorted(iterable, cmp)`：自定义排序；

### 6.4 闭包
- 内层函数**引用了外层函数的变量**（参数也算变量），然后返回内层函数的情况，称为闭包（`Closure`）；
- 要正确使用闭包，就要**确保引用的局部变量在函数返回后不能变**；

``` python 
# 高阶函数与闭包
def count():
    fs = []
    for i in range(1, 4):
        def g(x):
            def f():
                v = x
                return v * v
            return f
        fs.append(g(i))
    return fs
f1, f2, f3 = count()
print f1(), f2(), f3()	# 1, 4, 9
```

### 6.5 匿名函数
- 匿名函数 `lambda x: x * x` 
- 关键字`lambda` 表示匿名函数，冒号前面的 x 表示函数参数；
- 匿名函数只能有一个表达式，不写return；
- 返回函数的时候，也可以返回匿名函数；

### 6.6  装饰器
- 定义了一个函数，需要在代码运行时增强其功能，又不希望修改其代码；
- `Python`的 `decorator` 本质上就是一个高阶函数，它接收一个函数作为参数，然后，返回一个新函数；
- `Python`中的`@`语法就是为了简化装饰器的调用；
- 可以将通用的切面功能抽取出来，避免重复编写代码；
	- `@log`
	- `@performance`
	- `@transaction`
- 可以定义带参数的装饰器，需要再包装一层；
- 可以使用`@functools.wraps(f)`，可以将原函数的所有必要属性都一个一个复制到新函数上；

``` python
def performance(unit):
    def fn_wrapper(f):
        @functools.wraps(f)
        def fn(*args, **kwargs):
            start = time.time()
            result = f(*args, **kwargs)
            end = time.time()
            interval = end - start
            print 'call ' + f.__name__ + ' use ' + str(interval) + unit
            return result
        return fn
    return fn_wrapper

@performance('sss')
def factorial(n):
    return reduce(lambda x, y: x*y, range(1, n+1))
```

### 6.7 偏函数
- 偏函数即为把一个参数多的函数变成一个参数少的新函数；
- `functools.partial`就是帮助我们创建一个偏函数；

``` python 
# 创建了一个内置函数sorted的偏函数
cmp_ignore_case = functools.partial(sorted, cmp=lambda x, y: cmp(x.upper(), y.upper()))
```

## 7. 模块和包
- 所有代码放到一个py文件中，无法维护；
- 如果将代码拆分到多个py文件中，同一个名字的变量可以互补影响；
- 模块的名称即为`py`文件的名称；包就是文件夹，且可以有多级；
- 包下面必须有一个`__init__.py`；
- 需要引用模块时，使用`import`命令导入需要使用的模块；
- 同名的模块可以放到不同的包中，完整的模块名不冲突即可；

常用模块
- `math`
- `time`
- `os`
- `json`

### 7.1 导入模块
- 使用`import`可以导入其他模块；
- 使用`from .. import ...`可以导入模块下指定的函数；
- 使用`as`可以在导入指定函数时进行重命名；
- 可以使用`try: except:`语法进行动态导入；
- 当新版本的一个特性与旧版本不兼容时，该特性将会在旧版本中添加到`__future__`中；

``` python
# 导入模块
import math
# 导入函数
from math import pow, sin, log
 # 别名
from logging import log as logger  
# 动态导入
try:
    import json
except ImportError:
    import simplejson as json
# 新特性
from __future__ import unicode_literals
```

### 7.2 安装第三方模块
基本方式：
- `easy_install`
- `pip` - 官方推荐的安装方式；


## 8. 面向对象
### 8.1 类与实例
- 通过`class`关键字定义类；
- 通过`类名()`创建类的实例；

``` python
# 定义一个类
class Person(object):
    pass
# 创建实例
p1 = Person()
```
### 8.2 实例属性
- **动态实例属性**：`Python`是动态语言，对每一个实例，都可以直接给他们的属性赋值；
- **初始化实例属性**：可以使用`__init__()`方法，该方法在实例被创建时自动调用；
	- 相当于构造函数；在创建实例时，需要提供相对应的参数；
	- 第一个参数`self`默认传入自身的引用；
	- 可以使用`**kwargs`在最后一个参数传入`dict`参数；
	- 可以使用`setattr(object, name, value)`设置属性的值；
	- 如果一个属性由双下划线开头(`__`)，该属性就无法被外部访问
	- `__xxx__`的属性时python中的特殊属性，可以被外部访问；
	- 按照习惯，单下划线开头的属性也不应该被外部访问；

``` python
class Person(object):
    def __init__(self, name, birth, gender, **kwargs):
        self.name = name
        self.birth = birth
        self.gender = gender
        self.__score = 123;
        for k, v in kwargs.iteritems():
            setattr(self, k, v)
```

### 8.3 类属性
> 绑定在一个实例上的属性不会影响其他实例，如果在类上绑定一个属性，则所有实例都可以访问类的属性。实例属性每个实例各自拥有，互相独立，而类属性有且只有一份；相当于**静态成员变量**。
- 可以在类中直接定义类属性，相当于定义了一个静态成员变量；
- 使用类属性时，可以通过类名直接访问，如`Person.count`；
- 类属性也可以通过实例访问，但是当实例属性和类属性重名时，实例属性优先级高，它将屏蔽掉对类属性的访问；
- `object`类是所有类的父类；
- Python pass是空语句，是为了保持程序结构的完整性，pass 不做任何事情，一般用做占位语句。

``` python
class Person(object):
    count = 0
    def __init__(self, name):
        Person.count += 1
        self.name = name
        
p1 = Person('Bob')
print Person.count
p2 = Person('Alice')
print Person.count
p3 = Person('Tim')
print Person.count

```

### 8.4 实例方法
- 实例的方法就是在类中定义的函数，它的第一个参数永远是 self，指向调用该方法的实例本身，其他参数和一个普通函数一样；
- 使用`def`关键词定义实例方法；
- 在 `class` 中定义的实例方法其实也是属性，它实际上是一个函数对象；
- 函数和方法的区别：
	- 方法：类内普通方法，类方法；
	- 函数：普通函数，类内的静态方法；

```python
class Person(object):
    def __init__(self, name):
        self.__name = name
    def get_name(self):
        return self.__name
```

### 8.5 类方法
- 通过标记一个 `@classmethod`，该方法将绑定到类上，而非类的实例；
- 类方法的第一个参数将传入类本身，通常将参数名命名为 `cls`；
- 因为是在类上调用，而非实例上调用，因此类方法无法获得任何实例变量，只能获得类的引用；

``` python
class Person(object):
    __count = 0
    @classmethod
    def how_many(cls):
        return cls.__count

    def __init__(self, name):
        self.name = name
        Person.__count += 1
```

## 9. 继承
### 9.1 继承一个类
- 父类需要在类定义中指定`class chile(Parent)`；
- 需要在`__init__`方法中显示调用父类的构造方法初始化父类属性`super(Child, self).__init__()`；
- 也可在`__init__`方法中使用`Person.__init__(self)`初始化父类属性；
- 可以使用`isinstance(p_object, class_or_type_or_tuple)`方法判断对象是否为某类型；

``` python
class Person(object):
    def __init__(self, name, gender):
        self.name = name
        self.gender = name
class Teacher(Person):
    def __init__(self, name, gender, course):
        Person.__init__(self, name, gender)
        self.course = course
```

### 9.2 多态
- 类具有继承关系，并且子类类型可以向上转型看做父类类型；
- 调用方法时，先查找它自身的定义，如果没有定义，则顺着继承链向上查找，直到在某个父类中找到为止；
- 动态语言和静态语言（例如Java）最大的差别之一。动态语言调用实例方法，不检查类型，只要方法存在，参数正确，就可以调用；

### 9.3 多重继承
- 继承自多个父类时可以使用逗号分隔`class chile(Parent1, Parent2)`；
- 需要分别调用两个父类的构造方法`Parent.__init__(self)`；

``` python
class C(A, B)
    def __init__(self, a, b):
        A.__init__(self, a)
        B.__init__(self, b)
```

### 9.4 获取对象信息
- `isinstance()`：判断是否是某种类型的实例；
- `type()`：返回一个`Type`对象，即为变量的类型；
- `dir()`：获取变量所有的属性；
- `getattr(obj, attr)`：获取对象的某个属性；
- `setattr(obj, attr, value)`：设置对象的某个属性；

``` python
class Person(object):
    def __init__(self, name, gender, **kw):
        self.name = name
        self.gender = gender
        for k, v in kw.iteritems():
            setattr(self, k, v)
```


## 10. 定制类
### 10.1 特殊方法
- 特殊方法定义在`class`中；
- 不需要直接调用；
- `Python`的某些函数或操作符会调用对应的特殊方法；
- 只需要编写用到的特殊方法；
- 有关联性的特殊方法必须要同时实现；

### 10.2 常见特殊方法
#### 10.2.1 `__str__`和`__repr__`
- 如果要把一个类的实例变成 `str`，就需要实现特殊方法`__str__()`；
- Python 定义了`__str__()`和`__repr__()`两种方法，`__str__()`用于显示给用户，而`__repr__()`用于显示给开发人员；

``` python
class Student(Person):
    def __init__(self, name, gender, score):
        super(Student, self).__init__(name, gender)
        self.score = score
    def __str__(self):
        return '(Student: %s, %s, %s)' % (self.name, self.gender, self.score)
    __repr__ = __str__
```

#### 10.2.2 `__cmp__`
- 对 int、str 等内置数据类型排序时，Python的 sorted() 按照默认的比较函数 cmp 排序；
- 如果对一组 `Student` 类的实例排序时，就必须提供我们自己的特殊方法 `__cmp__()`；

``` python
def __cmp__(self, s):
    if self.score == s.score:
        return cmp(self.name, s.name)
    return -cmp(self.score, s.score)
```

#### 10.2.3 `__len__`
- 一个类表现得像一个`list`，要获取有多少个元素，就得用 `len()` 函数；
- 要让 `len()` 函数工作正常，类必须提供一个特殊方法`__len__()`，它返回元素的个数；

``` python
def __len__(self):
    return len(self.numbers)
```

#### 10.2.4  数学运算符
- `__add__`
- `__sub__`
- `__mul__`
- `__div__`

#### 10.2.5  类型转换
结果转为 int 或 float 
- `__int__`
- `__float__`
``` python
def __int__(self):
    return self.p // self.q

def __float__(self):
    return float(self.p) / self.q
```

#### 10.2.6 @property
- `@property`：可以将方法当做属性来调用；
- `@attrName.setter`：将方法当做属性来用赋值；
``` python
class Student(object):
    def __init__(self, name, score):
        self.name = name
        self.__score = score
    @property
    def score(self):
        return self.__score
    @score.setter
    def score(self, score):
        if score < 0 or score > 100:
            raise ValueError('invalid score')
        self.__score = score
    @property
    def grade(self):
        if self.score < 60:
            return 'C'
        if self.score < 80:
            return 'B'
        return 'A'
s = Student('Bob', 59)
print s.grade
s.score = 60
print s.grade
s.score = 99
print s.grade
```

#### 10.2.7 `__slots__`
- `__slots__`是指一个类允许的属性列表；
- `__slots__`的目的是限制当前类所能拥有的属性，如果不需要添加任意动态的属性，使用`__slots__`也能节省内存；

``` python
class Person(object):
    __slots__ = ('name', 'gender')
    def __init__(self, name, gender):
        self.name = name
        self.gender = gender
```


#### 10.2.8 `__call__`
- 在Python中，函数其实是一个对象；
- 一个类实例也可以变成一个可调用对象，只需要实现一个特殊方法`__call__()`；

## 其他
### 异常处理
``` python
try:
    print p.name
    print p.__score
except AttributeError:
    print 'attributeerror'
```
### 格式化输出
```
print '(Student: %s, %s, %s)' % (self.name, self.gender, self.score)
```