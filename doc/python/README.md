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

语言对比：
![语言对比](./1471883732619.png)

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
- 可以用`# -*- coding: utf-8 -*-`指定字符`UTF-8`，以便支持中文；
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
	- `[x * x for x in range(1, 11)]`：生成列表；
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
``` python
if score >= 90:
    print 'excellent'
elif score >= 80:
    print 'good'
elif score >=60:
    print 'passed'
else:
    print 'failed'
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

``` python
def fun(x, y, f):
    return f(x) + f(y)
# 将abs函数作为参数传入
print fun(1, -2, abs)
```

### 6.3 内置高阶函数
`map(function, sequence)`：将函数作用于每个对象，得到一个新的集合；