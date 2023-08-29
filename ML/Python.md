# Python

特点：

- 解释型语言，没有编译环节
- 面向对象语言

## 输出函数

```python
print(a) 
```

输入：a是数字、字符串或表达式

输出：可以输出到控制台或文件

```python
# a+：a代表写入文件，如果文件存在则在末尾追加，不存在则创建文件；+代表用于更新文件
fp = open('D:/text.txt', 'a+')
print('hello world', file=fp)
fp.close()
```

## 转义字符

```python
# \n 开启新的一行，即换行；
# \t 作用是跳格，即跳到下一个“制表位置”；
# \r 回车，即将光标跳到当前行的起始位置’
# \b 退格，即光标往前退一个字符
print('hello\nworld')
print('hello00\tworld')
print('helloooo\tworld')
print('hello\rworld')
print('hello\bworld')

# 当字符串中包含反斜杠、单引号和双引号等有特殊用途的字符时，必须使用反斜杠对这些字符进行转义
print('http:\\\\ww.baidu.com')
print('老师说\'你好\'')

# 若不希望字符串中的转义字符起作用，在字符串前面加上原字符：r或者R，且字符串的最后一个字符不能是单数个反斜杠
print(r'hello\nworld')
```

## 变量

变量由三部分组成

- 标识：表示对象所存储的内存地址，使用内置函数id(obj)来获取
- 类型：表示对象的数据类型，使用内置函数type(obj)来获取
- 值：表示对象所存储的具体数据，使用print(obj)进行打印输出

### 变量的作用域

程序代码能访问该变量的区域

- 局部变量 在函数体内定义的变量，只在函数内有效，局部变量使用global声明，这个变量就会变成全局变量

  ![image-20220919090757897](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919090757897.png)

- 全局变量  函数体外定义的变量，可以作用于函数内外

## 数据类型

- 整形 int 可以表示正数，负数和0，默认为十进制

  ```python
  print('十进制', 118)
  print('二进制', 0b11011)
  print('八进制', 0o176)
  print('十六进制', 0x1EAF)
  ```

- 浮点数 float

  `浮点数的计算需要引入decimal模块，机器在小数转化成二进制时会有误差`

- 布尔 bool 可以转化为整数0和1

  ```python
  f1 = True
  print(f1, type(f1))
  print(f1 + 1)
  ```

- 字符串 str 

  `可以用单引号、双引号、三引号进行定义，但是单引号和双引号定义的字符串必须在一行，三引号定义的字符串可以分布在连续的多行`

### 数据类型转换

![image-20220912150721809](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220912150721809.png)

ex：

- 文字类和小数类字符串，无法转化为帧数
- 浮点数转化成整数，抹零取整，
- 文字类无法转化成浮点数
- 整数转成浮点数，末尾为.0

## 注释

单行注释：以#开头，直到换行结束

```python
# 我是单行注释
```

多行注释：将一对三引号之间的代码成为多行注释

```python
'''
a = 2
print(a)
'''
```

中文编码声明注释：在文件开头加上中文声明注释，用于指定源码文件的编码格式

```python
#coding:gdk
```

## 输入函数

> ```python
> present = input('你叫什么名字')
> print(present)
> ```
>
> 作用：接受来自用户的输入
>
> 返回值类型：输入值的类型为str
>
> 值的存储：使用=对输入的值进行存储

## 运算符

- 算术运算符

  - 标准运算符 加+ 减 -  乘*  除/   整除//  （只取整数部分，一正一负，向下取整，及进一位）
  - 取余运算符 % （余数=被除数-除数*商）
  - 幂运算符 **  （2**2 = 4 二的二次方）

- 赋值运算符  运算顺序从右到左

  - 链式赋值时，多个引用指向一个数据对象 例如 a = b = c = 2

    ![image-20220915125934187](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220915125934187.png)

  - 参数赋值  a-=10 => a = a-10

  - 系列解包赋值  a,b,c=20,30,40  要求等号左右的变量和值的个数对应

    例如：交换两个变量的值 a,b = b,a

- 比较运算符

  -  ＞ ＜ ＞= ＜=  ==  !=  比较值
  - is   is not    比较标识  例如 print(a is b) 

- 布尔运算符

  - and 与
  - or 或
  - not 取反
  - in 包含
  - not in 不包含

- 位运算符 将数据转化为二进制进行加算

  - 位与 &
  - 位或 |
  - 左移位 <<
  - 右移位 >>

### 运算符的优先级

先数字运算之间，先算乘除后算加减，有幂运算先算幂运算

然后是位运算，先左右移，再与，再或

然后是比较运算符

然后是布尔运算符 and之后是or

最后是赋值运算符 = 

（有括号先算括号）

![image-20220915135814129](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220915135814129.png)

## 对象的布尔值

Python一切皆对象，所有对象都有个布尔值，通过**bool()函数**来获取对象的布尔值

一下对象的布尔值为False

- False
- 0
- None
- 空字符串
- 空列表 bool(list()) bool([])
- 空元组 bool(truple())
- 空字典 bool({})   bool(dict())
- 空集合 bool(set())

## 多分支结构

- if xx:
- elif xx:
- elif xx:
- ...
- else:

## 条件表达式

if......else的简写

`x if 判断条件 else y` 

如果判断条件的布尔值是True 条件表达式返回x，否则返回y

## pass语句

```python
pass
```

什么都不做，只是一个占位符，用在语法上需要语句的地方，用于在没想好代码怎么写的时候搭建语法结构用

## 内置函数range(start,stop,step)

用于生成一个整数序列

- range(10)  返回一个迭代器对象
- list(range(10)) 返回一个 0-10的步长为1的list对象
- list(range(1,10)) 返回一个 1-9的步长为1的list对象
- list(range(1,10,2))  返回一个 1-9的步长为2的list对象

**优点**：不管range对象表示的整数序列有多长，所有range对象占用的内存空间都是相同的，因为只需要存储start、stop、step。只有用到range对象时，才回去计算序列中的相关元素。

in 、not in 可以判断整数序列中是否存在指定的整数

## 循环

### while循环

![image-20220915150242357](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220915150242357.png)

### for in 循环

for 自定义的变量 in 可迭代对象

### 流程控制语句

- break
- continue

## else语句

- 与if搭配，if条件表达式不成立时 执行else
- 与while和for in搭配， 没有碰到break的时候执行else

## 列表

列表变量存储的是一个对象的**引用**

![image-20220915152232101](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220915152232101.png)

### 列表的创建

- 使用中括号 lst = ['hello','world',98]
- 使用内置函数 lst2 = list(['hello','world',98])

### 列表的特点

- 列表元素按顺序有序排序
- 索引映射唯一个数据
- 列表可以存储重复数据
- 任意数据类型混存
- 根据需要动态分配和回收内存

### 列表指定元素的索引

```python
lst = ['hello','world',98,'hello']
print(lst.idnex('hello'))

#在指定位置查找
print(lst.idnex('hello'),1,4)
```

- 若列表中有相同的元素，则返回以第一个查到的元素的索引
- 若列表中不存在该元素，则会抛异常

### 获取列表中的单个元素

- 正向索引：从0到N-1 例如lst[0]
- 逆向索引从-N到-1，例如：lst[-N]
- 指定索引不存在，抛异常

### 获取列表的多个元素

切片：列表名[start : stop : step]

切片的结果：原列表片段的拷贝

切片的范围：[start , stop]

```python
lst = [10, 20, 30, 40, 50, 60, 70, 80]
print(lst[1: 6: 1])
print(lst[1: 6:])  # 默认步长为1
print(lst[: 6:2])  # 默认start为1
print(lst[1::2])  # 默认stop为最后一个
print(lst[::-1])  # 列表逆序
print(lst[6::-1])  # 从第6个逆序
print(lst[6:0:-2])  # 从第6个到第一个步长为2的逆序
```

![image-20220915154824096](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220915154824096.png)

### 列表元素的增删改查

**查询**

元素 in 列表名 

元素 not in 列表名

**增加**

```python
lst = [10,20,30]
lst.append(100) #在列表的末尾添加一个元素
lst2 = ['hello','world']
lst.extend(lsy2) #在列表的末尾添加至少一个元素，接受一个list对象
lst.insert(1,90) #在任意位置上添加一个元素
lst[1:] = lst3 #在列表的任意位置添加多个元素，接收一个list对象 (切片)

```

**删除**

```python
lst = [10,20,30,40,50,60,30]
lst.remove(30) #从列表移除一个元素，若有重复元素只移除第一个，若不存在则抛异常
lst.pop(1) #根据所以移除元素，若不存在则抛异常，不指定参数，默认删除列表最后一个元素
new_list = lst[1:3] #切片删除，将产生一个新的列表对象
lst[1:3] = [] #切片删除，不产生新的列表对象
lst.clear() #清除列表中的所有元素
del lst #删除列表对象
```

**修改**

```python
lst = [10,20,30,40,50,60,30] 
lst[2] = 100 #使指定的索引修改对应的值
lst[1:3] = [200,300,400]#为指定的切片赋予一个新的值
```

### 列表的排序

```python
lst = [20,40,10,98,54]
lst.sort() #默认按照升序进行排序
lst.sort(reverse=True) #按照降序排序

new_lst = sorted(lst)#使用内置函数sorted排序，会产生新的列表对象，默认为升序
new_lst = sorted(lst，reverse=True) #降序排序，
```

### 列表生成式

```python
lst = [i for i in range(1,10)]
```

![image-20220915191447158](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220915191447158.png)

## 字典

 Python内置的数据结构之一，和列表一样是个**可变序列**（可以进行增删改操作），以**键值对**的方式存储数据（要求是不可变序列），字典是个**无序** （存放位置通过hash(key)计算而得）的序列

![image-20220916103051643](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916103051643.png)

![image-20220916103412192](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916103412192.png)

**实现原理**

与查字典类似，根据hash(key)查到value所在的位置，再获取相应的值，查找效率很高

### 常用操作

#### 创建

```python
#使用花括号
score={'Tom':100,'Jerry':98,'Bob':45}

#使用内置韩式
dict({name='jack',age=20})
```

#### 取值

```python
score = {'Tom': 100, 'Jerry': 98, 'Bob': 45}
# 直接获取，若值不存在会报错
print(score['Tom'])
# 通过get函数获取
print(score.get('Tom'))
# 若查找元素不存在可以返回一个默认值
print(score.get('Sarry', 99))
```

#### 增删改查

```python
score = {'Tom': 100, 'Jerry': 98, 'Bob': 45}
# 查找指定key在字典中是否存在
print('Tom' in score)
print('Tom' not in score)

# 根据key值删除整个键值对
del score['Tom']
print(score)

# 清除字典元素
score.clear()
print(score)

# 新增元素
score['Marry'] = 98
print(score)

# 修改元素
score['Marry'] = 88
print(score)
```

#### 视图

- keys() => 获取字典中所有key

- values() => 获取字典中所有value

- items() => 获取字典中所有的键值对

  ```python
  score = {'Tom': 100, 'Jerry': 98, 'Bob': 45}
  # 获取所有key
  keys = score.keys()
  print(keys)
  print(type(keys))
  print(list(keys))
  
  # 获取所有值
  values = score.values()
  print(values)
  print(type(values))
  print(list(values))
  
  # 获取所有键值对
  items = score.items()
  print(items)
  print(type(items))
  print(list(items))  # 元组
  
  ```

  ![image-20220916105038442](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916105038442.png)

#### 遍历

```python
for item in score:
    print(item, score[item], score.get(item))
```

### 特点

- 键不允许重复，value可以重复
- 字典中的元素是无序的
- key必须为不可变对象（list就不可以）
- 可以动态伸缩
- 内存耗费较大，是一种空间换时间的策略

### 字典生成式

内置函数**zip()**，用可迭代的对象作为参数，将对象中对应的元素打包成一个元祖，然后返回由这些元组组成的列表，长度由最短的对象的长度决定

```python
items = ['Fruits', 'Books', 'Others']
prices = [95, 78, 85]
d = {item: price for item, price in zip(items, prices)}
print(d)
```

## 元组

Python内置的数据结构之一，是个**不可变序列**

![image-20220916111757515](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916111757515.png)

![image-20220916111744159](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916111744159.png)

*为什么元组被设计成不可变序列*

在多任务环境下，同时操作对象时**不需要加锁**（可变序列就需要加锁），在程序中应该尽量使用不可变序列

注意：元祖中存储的是**对象的引用**

- 若元祖中对象本身是不可变对象，则不能再引用其他对象 （元组中的元素是不可更改的）
- 如果元祖中的对象是可变对象，则可变对象的引用不允许改变，但数据可以改变

### 常用操作

#### 创建

```python
# 使用小括号创建
t = ('Python', 'world', 85)
print(t)
print(type(t))

# 省略小括号
t2 = 'Python', 'world', 85
print(t2)
print(type(t2))

# 只包含一个元素的元组需要加逗号
t3 = 'Python',
print(t3)
print(type(t3))

# 使用内置函数tuple()
t1 = tuple(('Python', 'world', 85))
print(t1)
print(type(t1))
```

#### 遍历

```python
t = ('Python', 'world', 85)
# 直接通过索引获取
print(t[0])
# 通过for in 遍历
for item in t:
    print(item)

```

## 集合

- Python提供的内置数据结构，属于**可变类型**的序列
- 相当于**没有value的字典**，也是通过hash函数计算的存储位置
- 集合中的元素**不允许重复**
- 集合中的元素是无序的

![image-20220916130119444](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916130119444.png)

### 常用操作

#### 创建

```python
# 通过{}创建
s1 = {2, 3, 4, 5, 5, 6, 7, 7}
print(s1)
# 通过内置函数set()创建
s2 = set(range(6))
print(s2, type(s2))
s3 = set([1, 2, 3, 4, 5, 5, 6, 7, 7])
print(s3, type(s3))
s4 = set((1, 2, 3, 4, 5, 5, 6, 7, 7))
print(s4, type(s4))
s5 = set('Python')
print(s5, type(s5))
s6 = set({2, 3, 4, 5, 5, 6, 7, 7})
print(s6, type(s6))
s7 = {}
print(type(s7))
s8 = set()
print(type(s8))

```

![image-20220916130821274](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916130821274.png)

#### 增删改查

```python
s = {10, 20, 30, 405, 60}
# 集合的判断
print(10 in s)
print(10 not in s)

# 集合的新增
s.add(80)  # 一次添加一个元素
print(s)
s.update({200, 400, 300})  # 一次至少添加一个元素
print(s)
s.update([100, 99, 8])
s.update((78, 64, 56))
print(s)

# 集合的删除,若没有则会抛异常
s.remove(100)
print(s)
# 集合的删除,若没有也不会抛异常
s.discard(500)
print(s)
# 随机删除一个元素,是个无参函数
s.pop()
print(s)
# 清空集合
s.clear()
print(s)
```

### 集合的关系

- 相等 通过 == 或者!= 进行判断
-  通过调用 issubset() 进行判断
- 是否是另一个集合的超集，通过 issuperset() 进行判断
- 是否两个集合没有交集，通过 isdisjoint() 进行判断

```python
# 两个集合的元素相同就相等，顺序无所谓
s = {10, 20, 30, 40}
s2 = {40, 20, 30, 10}
print(s == s2)

# 是否是另一个集合的子集
s1 = {10, 20, 30, 40, 50, 60}
s2 = {10, 20, 30, 40}
s3 = {10, 20, 90}
print(s2.issubset(s1))
print(s3.issubset(s1))

# 是否是另一个集合的超集，和子集关系正好相反
print(s1.issuperset(s2))
print(s1.issuperset(s3))

# 两个集合是否有交集
print(s2.isdisjoint(s3))  # 有交集为False

s4 = {100, 200, 300}
print(s2.isdisjoint(s4))  # 没有交集则为True
```

### 数学操作

- 交集
- 并集
- 差集
- 对称差集

```python
# 交集
s1 = {10, 20, 30, 40}
s2 = {20, 30, 40, 50, 60}
print(s1.intersection(s2))
print(s1 & s2)  # intersection 与 & 等价，交集操作

# 并集
print(s1.union(s2))  # 去掉重复元素
print(s1 | s2)  # union等价与 |，并集操作

# 差集
print(s1.difference(s2))
print(s1 - s2)
print(s2.difference(s1))
print(s2 - s1) # difference等价于 -，差集操作

# 对称差集
print(s1.symmetric_difference(s2))
print(s1 ^ s2) # symmetric_difference等价于 ^，对称差集操作
```

### 集合生成式

![image-20220916133348960](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916133348960.png)

```python
s = {i*i for i in range(10)}
```

![image-20220916133557592](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916133557592.png)

## 字符串

基本数据类型，是**不可变**的字符序列

### 字符串的驻留机制

仅保存一份相同且不可变字符串的方法，不同的值被存放在字符串的驻留池中，Python的驻留机制**对相同的字符串只保留一份拷贝**，后续创建相同字符串时，**不会开辟新空间**，而是把该字符串的地址付给新创建的变量。

![image-20220916135032145](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916135032145.png)

符合驻留机制的几种情况：

- 字符串的长度为0或1时
- 符合标识符（字母、数字、下划线）的字符串
- 字符串只在编译时进行驻留，而非运行时
- [-5,256]之间的整数数字
- 可以使用sys包里面的 a=sys.intern(b) 来进行强制驻留 （pycharm 进行了强制处理，都驻留了，所以只能在交互模式下运行才有效果）

**优缺点**

当需要值相同的字符串时，可以直接从字符串池里拿来使用，避免频繁的创建和销毁，**提升效率和节约内存**，因此拼接字符串和修改字符串是比较影响性能的

在需要进行字符串拼接时建议使用str类型的**join方法**，而非+，因为join()方法是先计算出所有字符中的长度，然后再拷贝，**只new一次对象**，效率要比+效率高

### 常用操作

#### 查询

- index() 查找子串substr第一次出现的位置，如果查找的子串不存在时，则抛异常
- rindex() 查找子串substr最后一次出现的位置，若不存在则抛异常
- find() 查找子串substr第一次出现的位置，不存在则返回-1
- rfind()查找子串substr最后一次出现的位置，不存在则返回-1

 ![image-20220916142832448](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916142832448.png)

#### 大小写转化 

*转化完之后会产生一个新的字符串*

- upper() 字符串中所有的字符都转化成大写字母
- lower() 把字符串中所有字符都转成小写字母
- swapcase() 把字符串中所有的大写字母转成小写字母，把所有小写字母转成大写字母
- capitalize() 把第一个字服转化成大写，其余字符转化成小写
- title() 把每个单词的第一个字符转换为大写，每个单词的剩余字符转化为小写

#### 对齐

- center() 居中对齐，第一个参数指定**宽度**，第二个参数指定填充符，第二个参数是可选的，**默认是空格**，如果设置宽度小于实际宽度则返回原字符串
- ljust() 左对齐，第一个参数指定宽度，第二个参数指定填充符，第二个参数是可选的，**默认是空格**，如果设置宽度小于实际宽度则返回原字符串
- rjust() 右对齐，第一个参数指定宽度，第二个参数指定填充符，第二个参数是可选的，**默认是空格**，如果设置宽度小于实际宽度则返回原字符串
- zjust() 右对齐，左边用0填充，只接受一个参数，用于指定字符串的宽度，如果设置宽度小于实际宽度则返回原字符串

#### 分割

- split() 
  - 从字符串的左边开始分割，默认的分割字符是空格字符串，返回的值都是一个列表
  - 可以通过参数 sep 指定分割字符串时的分隔符
  - 通过参数 maxsplit 指定分割字符串时的最大分割次数，在经过最大次分割之后，剩余的子串会单独做为一部分
- rsplit()
  - 从字符串的右边开始分割，默认的分割字符是空格字符串，返回的值都是一个列表
  - 可以通过参数 sep 指定分割字符串时的分隔符
  - 通过参数 maxsplit 指定分割字符串时的最大分割次数，在经过最大次分割之后，剩余的子串会单独做为一部分

#### 判断

- isidentifier() 判断指定的字符串是不是合法的标识符（字母数字下划线）
- isspace() 判断指定的字符串是否全部由空白字符组成（回车、换行、水平制表符）
- isalpha() 判断指定的字符串是否全部由字母组成
- isdecimal() 判断指定字符串是否全部由十进制的数字组成
- isnumeric() 判断指定的字符串是否全部由数字组成
- isalnum() 判断指定字符串是否全部由字母和数字组成

#### 替换

replace()  **第一个参数**指定被替换的子串，**第二个参数**指定替换子串的字符串，该方法返回替换后得到的字符串，替换前的字符串不发生变化，调用该方法时可以通过第**三个参数**指定最大替换次数

#### 合并

join() 将列表或元组中的字符串合并成一个字符串

```python
lst = ['hello', 'java', 'Python']
print('|'.join(lst))
print(''.join(lst))

t = ('hello', 'java', 'Python')
print(''.join(t))

print('*'.join('Python'))
```

![image-20220916153435945](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916153435945.png)

#### 比较

运算符  \> \>= < <= == !=

比较规则：从左到右依次比较两个字符串字符的值，直到两个字符串中的字符不相等时，其比较结果就是字符串的比较结果，后续字符将不再被比较

比较原理：通过内置函数**ord**可以的到指定字符的ordinal value，通过ordinal value进行比较，与之对应通过ordinal value得出字符的内置函数是**chr()**

*== 与 is 的区别*

- == 比较的是value
- is 比较的是 id

#### 切片

字符串时不可变类型，不具备增删改等操作，切片操作将产生新的对象

![image-20220916155121306](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916155121306.png)

```python
s = 'hello,Python'
s1 = s[:5]  # 没指定起始位置，从零开始 到5-1 = 4
s2 = s[6:]  # 没指定结束为止，切到字符串的最后从 6 到最后一位
s3 = '!'

newstr = s1 + s2 + s3

print(s1)
print(s2)
print(newstr)

print(s[1:5:1])
print(s[::2])
print(s[::-1])  # 默认从字符串的最后一个元素开始，到字符串的第一个元素结束，因为步长为负数
print(s[-6::])
```

#### 格式化字符串

%做占位符![image-20220916160043363](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916160043363.png)

{}做占位符

![image-20220916160052841](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916160052841.png)

```python
name = 'Tom'
age = 20
print('I am %s, I am %d' % (name, age))

print('I am {0}，I am {1}'.format(name, age))

print(f'I am {name}，I am {age}')
```

精度格式化

```python
print('%d' % 99)
print('%10d' % 99)  # 10表示宽度
print('%f' % 3.1415926)
print('%.3f' % 3.1415926)  # 保留三位小数
print('%10.3f' % 3.1415926)  # 同时表示宽度和精度
print('{}'.format(3.1415926))
print('{:.3}'.format(3.1415926))  # .3表示一共3位数
print('{:.3f}'.format(3.1415926))  # .3f表示3位小数
print('{:10.3f}'.format(3.1415926))  # 同时设置宽度和精度
```

![image-20220916161015608](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916161015608.png)

#### 编码转换

为什么需要转化：

![image-20220916161048556](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220916161048556.png)

- 编码：将字符串转换为二进制数据（bytes）
- 解码：将bytes类型的数据转换成字符串类型

```python
s = '天涯共此时'
# 编码
print(s.encode(encoding='GBK'))  # 在这种编码格式汇总，一个中文占两个字节
print(s.encode(encoding='UTF-8'))  # 在这种编码格式汇总，一个中文占三个字节

# 解码
# byte代表的就是一个二进制数据（字节类型的数据）
byte = s.encode(encoding='GBK')  # 编码
print(byte.decode(encoding='GBK'))  # 解码

byte = s.encode(encoding='UTF-8')  # 编码
print(byte.decode(encoding='UTF-8'))  # 解码
```

## 函数

函数就是执行特定任务和完成特定功能的一段代码

**意义**

- 复用代码
- 隐藏实现细节
- 提高可维护性
- 提高可读性便于调试

**创建**

![image-20220919080909415](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919080909415.png)

**过程**

![image-20220919081040420](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919081040420.png)

```python
def calc(a, b):
    return a + b


c = calc(2, 3)
print(c)
```

### 参数传递

- 形式参数，形参 位置在函数的定义处
- 实际参数，实参 位置在函数的调用处

**传递方式**

- 位置传参：根据形参对应的位置进行参数传递

  ![image-20220919081520811](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919081520811.png)

- 关键字传参：根据形参名称进行实参传递

  ![image-20220919081548631](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919081548631.png)

```python
def calc(a, b):
    return a + b


# 位置传参
c = calc(2, 3)
print(c)
# 关键字传参
c = calc(b=4, a=3)
print(c)
```

位置传参和关键字传参方法可以同时使用

```python
def fun(a, b, c, d):
    print('a=', a)
    print('b=', b)
    print('c=', c)
    print('d=', d)


fun(10, 20, d=40, c=30)
```

![image-20220919085337381](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919085337381.png)

若想要后面一部分只采用关键字实参传递方式，需要在定义式**用*将参数隔开**

![image-20220919085502811](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919085502811.png)

在函数调用过程中，进行参数的传递

- 不可变对象，在函数体的修改不会影响实参的值
- 可变对象，在函数体的修改会影响到实参的值

![image-20220919081937457](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919081937457.png)

### 返回值

- 返回值如果是一个，直接返回类型
- 返回值如果是多个，返回的结果为元组

### 参数定义

**默认参数**

函数定义时给形参设置默认值，只有与默认值不符的时候才需要传递实参

![image-20220919082638349](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919082638349.png)

```python
def calc(a, b=10):
    return a + b


print(calc(2))
print(calc(b=4, a=3))
```

![image-20220919082753870](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919082753870.png)

**个数可变的位置参数**

- 定义函数时，可能无法事先确定传递的位置实参的个数时，使用可变的位置参数

- 使用 * 定义个数可变的位置形参

- 结果为一个**元组**

  ![image-20220919083021916](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919083021916.png)

  

**个数可变的关键字形参**

- 定义函数时，无法事先确定传递的关键字实参的个数时，使用可变的关键字传参
- 使用 ** 定义个数可变的关键字传参
- 结果为一个**字典**

```python
# 可变的位置参数
def fun(*args):
    print(args)


fun(10)
fun(10, 20)
fun(10, 20, 50)


def fun1(**args):
    print(args)


# 可变的关键字参数
fun1(a=10)
fun1(a=10, b=20)
fun1(a=10, b=20, c=30)

# 可变的位置参数和关键字参数只能为一个,二者同时存在时，可变的位置参数需要在可变的关键字参数之前
```

函数调用时的可变参数

```python
def fun(a, b, c):
    print('a=', a)
    print('b=', b)
    print('c=', c)



fun(10, 20, 30)
lst = [11, 22, 33]
fun(*lst)
fun(a=100, b=200, c=300)
dic = {'a': 111, 'b': 222, 'c': 333}
fun(**dic)
```

![image-20220919084603179](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919084603179.png)

### 递归函数

如果在一个函数的函数体内调用了该函数本身，这个函数就成为递归函数

**组成部分**

递归调用与递归终止条件

**递归的调用过程**

- 每递归调用一次函数，都会在栈内存分配一个栈帧
- 每执行完一次函数，就会释放相应的空间

**优缺点**

- 占用内存多，**效率低下**
- 思路和代码**简单**

```python
def fac(n):
    if n == 1:
        return 1
    else:
        return n * fac(n - 1)


print(fac(6))
```

**斐波那契数列**

```python
def fib(n):
    if n == 1:
        return 1
    elif n == 2:
        return 1
    else:
        return fib(n - 1) + fib(n - 2)


# 打印斐波那契数列某位上的数值
print(fib(6))
# 打印斐波那契数列
print([fib(i) for i in range(1, 7)])
```

## Bug

SyntaxError 语法错误

![image-20220919100828788](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919100828788.png)

IndexError 索引越界问题

KeyError 映射中没有这个键

NameError 未声明/初始化对象（没有属性）

ValueError 传入无效的参数

ZeroDivisionError 除（或取模）零

## 异常处理机制

### try...except结构

可以在异常出现时及时捕获，然后内部消化，让程序继续运行

![image-20220919101139912](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919101139912.png)

**多个excpet结构**

捕获异常的顺序按照先子类后父类的顺序，为了避免遗漏可能出现的异常，可以在最后增加BaseException

![image-20220919101658920](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919101658920.png)

```python
try:
    a = int(input('请输入第一个整数'))
    b = int(input('请输入第二个整数'))
    result = a / b
    print('结果为', result)
except ZeroDivisionError:
    print('对不起，除数不允许为0')
except ValueError:
    print('只能输入数字类型数据')
except BaseException as e:
    print(e)
print('程序结束')
```

**try...except...else结构**

如果try块没有抛出异常，则执行else块，如果抛出异常，则执行except块

![image-20220919102109707](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919102109707.png)

**try...except...else...finally结构**

finally块无论是否发生异常都会执行，一般用于释放try块申请的资源

![image-20220919102200743](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919102200743.png)

### traceback模块

使用traceback模块打印异常信息

```python
import traceback

try:
    a = int(input('请输入第一个整数'))
    b = int(input('请输入第二个整数'))
    result = a / b
    print('结果为', result)
except:
    traceback.print_exc()
```

![image-20220919102900518](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919102900518.png)

## 面向过程与面向对象

![image-20220919104438588](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919104438588.png)

## 类与对象

### 类

多个类似事物组成的群体的统称，能够帮助我们快速理解和判断事物的性质

#### 类的创建

![image-20220919104818513](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919104818513.png)

```python
class Student:  # Student为类名，有一个或多个单词组成，每个单词的首字母大写，其余小写
    # 直接写在类里面的变量，成为类属性
    native_place = '吉林'

    # 实例方法
    def eat(self):
        print('学生在吃饭...')

    # 静态方法
    @staticmethod
    def method():
        print('这是静态方法')

    # 类方法
    @classmethod
    def cm(cls):
        print('这是类方法')

    # 初始化方法 self.name成为实体属性，进行了一个赋值的操作，将局部变量的name值赋给实体属性
    def __init__(self, name, age):
        self.name = name
        self.age = age

```

#### 类属性

类中方法外的变量成为类属性，被该类的所有对象所共享

```python
# 直接写在类里面的变量，成为类属性
native_place = '吉林'
```

#### 类方法

使用@classmethod修饰的方法，实用类名直接访问的方法

```python
# 类方法
@classmethod
def cm(cls):
    print('这是类方法')
```

#### 静态方法

使用@staticmethod修饰的方法，使用类名直接访问

```python
# 静态方法
@staticmethod
def method():
    print('这是静态方法')
```

### 对象

某个类下具体的个体，成为实例或者对象

**Python中一切皆对象**

```python
class Student:  # Student为类名，有一个或多个单词组成，每个单词的首字母大写，其余小写
    pass


print(id(Student))
print(type(Student))
print(Student)
```

![image-20220919105110160](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919105110160.png)

#### 对象的创建

类的实例化，有了实例就可以调用类中的内容

实例名 = 类名（）

![image-20220919105852274](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919105852274.png)

### 动态绑定属性与方法

Python是动态语言，在创建对象之后，可以动态地绑定属性和方法

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def eat(self):
        print(self.name + '在吃饭')


stu1 = Student('张三', 20)
stu2 = Student('李四', 30)

# 为对象动态绑定属性和方法,仅限这个实例拥有
stu1.gender = '女'


def show():
    print("这是动态添加的方法")


stu1.show = show
stu1.show()
stu2.show()  # stu2里没有

print(stu1.name, stu1.age, stu1.gender)
print(stu2.name, stu2.age, stu2.gender)  # stu2里没有
```

![image-20220919152912873](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220919152912873.png)

## 面向对象

**面向对象的三大特征**

### 封装 

提高程序的安全性

将数据（属性）和行为（方法）包装到类对象中。在方法内部对属性进行操作，在类对象的外部调用方法，无需关心方法内部的具体实现细节，从而隔离了复杂度

在Python中没有专门的修饰符用于属性的私有，如果该属性不希在类对象外部被访问，前面有两个_

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.__age = age

    def eat(self):
        print(self.name + '在吃饭')

    def getAge(self):
        print(self.__age)


stu1 = Student('张三', 20)

stu1.getAge()
# print(stu1.__age) 从外部是无法访问到的

print(stu1._Student__age) #在类的外面可以通过 _Student__age进行访问
```

### 继承

提高代码的复用性

- 如果一个类没有继承任何类，则默认继承Object
- Python支持多继承
- 定义子类时，必须在其构造函数中调用父类的构造函数

![image-20220920123134336](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220920123134336.png)

**语法格式**

class 子类类名(父类1，父类2...):

​	pass

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def info(self):
        print(self.name, self.age)


class Student(Person):
    def __init__(self, name, age, stu_no):
        super().__init__(name, age)
        self.stu_no = stu_no


class Teacher(Person):
    def __init__(self, name, age, teacher_no):
        super().__init__(name, age)
        self.teacher_no = teacher_no


stu = Student('张三', 20, '1001')
teacher = Teacher('李四', 34, '2002')

stu.info()
teacher.info()
```

**多继承**

![image-20220920124219187](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220920124219187.png)

#### 方法重写

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def info(self):
        print(self.name, self.age)


class Student(Person):
    def __init__(self, name, age, stu_no):
        super().__init__(name, age)
        self.stu_no = stu_no

    def info(self):
        super().info()
        print('学号', self.stu_no)


class Teacher(Person):
    def __init__(self, name, age, teacher_no):
        super().__init__(name, age)
        self.teacher_no = teacher_no

    def info(self):
        super().info()
        print('工号', self.teacher_no)


stu = Student('张三', 20, '1001')
teacher = Teacher('李四', 34, '2002')

stu.info()
teacher.info()
```

#### Object类

- Object类是**所有类的父类**，因此所有类都有object类的属性和方法

- 内置函数 **dir()** 可以查看指定对象所有属性

  ```python
  class Student:
      pass
  
  
  stu = Student()
  print(dir(stu))
  '''
  所有Object具有的属性
  ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__']
  
  '''
  ```

- Object有一个\_str\_（）方法，用于返回一个对于“**对象的描述”**，对应于内置函数str() 经常用于print()方法，帮我们查看对象的信息，所以我们经常会对\_str\_（）进行重写

  ```python
  class Student:
      def __init__(self, name, age):
          self.name = name
          self.age = age
  
      def __str__(self):
          return '我的名字是{0}，今年{1}岁了'.format(self.name, self.age)
  
  
  stu = Student('张三', 20)
  print(stu)  # 默认调用__str()__这样个方法
  print(type(stu))
  ```

  ![image-20220920152023546](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220920152023546.png)

  

### 多态

- 提高程序的可扩展性和可维护性
- 简单来说就是具有多种形态，他指的是：即便不知道一个变量所引用的对象到底是什么类型，依然可以通过这个变量调用方法，在**运行过程中根据变量所引用对象的类型**，**动态**决定调用哪个对象的方法

```python
class Animal:
    def eat(self):
        print('动物会吃...')


class Dog(Animal):
    def eat(self):
        print("狗吃骨头...")


class Cat(Animal):
    def eat(self):
        print("猫吃鱼...")


class Person:
    def eat(self):
        print("人吃五谷杂粮...")


def fun(obj):
    obj.eat()


fun(Cat())
fun(Dog())
fun(Animal())
print('-------------------')
fun(Person())
```

![image-20220920153430383](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220920153430383.png)

#### 静态语言与动态语言关于多态的区别

静态：java 动态：python

**静态语言实现多态的三个必要条件**

- 继承
- 方法重写
- 父类引用指向子类对象

动态语言的多态崇尚“**鸭子类型**”，不需要关心对象是什么类型，到底是不是鸭子，只关心对象的行为，行为像鸭子即可

### 特殊的属性和方法

#### 属性

```python
class A:
    pass


class B:
    pass


class C(A, B):
    def __init__(self, name, age):
        self.name = name
        self.age = age


# 创建C类的对象
x = C('JACK', 20)  # x是C类型的一个实例对象
print(x.__dict__)  # 实例对象的属性字典
print(C.__dict__)  # 类对象的属性字典

print(x.__class__)  # 输出了对象所属的类
print(C.__bases__)  # 输出C类父类型的元素
print(C.__base__)  # 输出离C类最近的父类型的元素，基类
print(C.__mro__)  # 输出类的层次结构
print(A.__subclasses__()) #子类的列表
```

![image-20220920154542529](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220920154542529.png)

#### 方法

- \_\_len\_\_() 通过重写  \_\_len\_\_() 方法，让内置函数len()的参数可以是自定义类型
- \_\_add\_\_() 通过重写\_\_add\_\_() 方法，可是自定义对象具有+功能

```python
a = 20
b = 100
c = a + b  # 两个整数类型的对象的相加操作
d = a.__add__(b)

print(c)
print(d)


class Student:
    def __init__(self, name):
        self.name = name

    def __add__(self, other):
        return self.name + other.name

    def __len__(self):  # 通过编写类的__len__，可以使对象获取到长度
        return len(self.name)


stu1 = Student('张三')
stu2 = Student('Jack')

s = stu1 + stu2  # 实现了两个对象的加法运算（因为编写了__add__方法）
print(s)

print(stu1.__len__())
print(stu2.__len__())
```

![image-20220920165043566](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220920165043566.png)

- \_\_new\_\_() 用于创建对象

- \_\_init\_\_() 对创建的对象进行初始化

  **工作过程**

  ```python
  class Person:
  
      def __new__(cls, *args, **kwargs):  # 用于创建对象的
          print("__new__被调用执行了，cls的id值为{0}".format(id(cls)))
          obj = super().__new__(cls)
          print("创建的对象的id为：{0}".format(id(obj)))
          return obj
  
      def __init__(self, name, age):
          print("__init__被调用执行了，self的id值为{0}".format(id(self)))
          self.name = name
          self.age = age
  
  
  print('object这个类对象的id为：{0}'.format(id(object)))
  print('object这个类对象的id为：{0}'.format(id(Person)))
  
  # 创建Person类的实例对象
  p1 = Person("张三", 20)
  print("p1这个Person类的实例对象的id:{0}".format(id(p1)))
  
  ```

  ![image-20220920173211355](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220920173211355.png)

  ![image-20220920173143993](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220920173143993.png)

### 类的浅拷贝与深拷贝

**变量的赋值操作**

- 只是形成两个变量，实际上还是指向同一个对象

  ![image-20220921085730493](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220921085730493.png)

  ```python
  class CPU:
      pass
  
  
  class Disk:
      pass
  
  
  class Computer:
      def __init__(self, cpu, disk):
          self.cpu = cpu
          self.disk = disk
  
  
  # 变量的赋值
  cpu1 = CPU()
  cpu2 = cpu1
  print(id(cpu1), id(cpu2))  # 2655700541392 2655700541392 二者地址值相同
  ```

**浅拷贝**

- Python拷贝一般都是浅拷贝，拷贝时，对象包含的子对象内容不拷贝，因此，源对象与拷贝对象会引用同一个子对象

  ![image-20220921092149198](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220921092149198.png)

  ```python
  class CPU:
      pass
  
  
  class Disk:
      pass
  
  
  class Computer:
      def __init__(self, cpu, disk):
          self.cpu = cpu
          self.disk = disk
  
  
  cpu1 = CPU()
  # 类的浅拷贝
  disk = Disk()
  computer = Computer(cpu1, disk)
  
  import copy
  
  computer2 = copy.copy(computer)
  print(disk)
  print(computer, computer.cpu, computer.disk)
  print(computer2, computer2.cpu, computer2.disk)
  # compuer he computer2 两个对象的id不一样，但是子对象的id都一样
  # <__main__.Computer object at 0x000001CDDA755F70> <__main__.CPU object at 0x000001CDDA755FD0> <__main__.Disk object at 0x000001CDDA755FA0>
  # <__main__.Computer object at 0x000001CDDA755D90> <__main__.CPU object at 0x000001CDDA755FD0> <__main__.Disk object at 0x000001CDDA755FA0>
  ```

**深拷贝**

- 使用copy模块的deepcopy函数,递归拷贝对象中包含的子对象,源对象和拷贝对象所有的子对象也不相同

  ![image-20220921092454416](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220921092454416.png)

  ```python
  class CPU:
      pass
  
  
  class Disk:
      pass
  
  
  class Computer:
      def __init__(self, cpu, disk):
          self.cpu = cpu
          self.disk = disk
  
  
  cpu1 = CPU()
  # 类的浅拷贝
  disk = Disk()
  computer = Computer(cpu1, disk)
  
  import copy
  
  computer3 = copy.deepcopy(computer)
  
  print(disk)
  print(computer, computer.cpu, computer.disk)
  print(computer3, computer3.cpu, computer3.disk)
  
  #computer3 和 computer 对象的id 都不一致，且子对象的id也不一致
  # <__main__.Disk object at 0x0000026E593A5FA0>
  # <__main__.Computer object at 0x0000026E593A5F70> <__main__.CPU object at 0x0000026E593A5FD0> <__main__.Disk object at 0x0000026E593A5FA0>
  # <__main__.Computer object at 0x0000026E593A5D30> <__main__.CPU object at 0x0000026E593A5A30> <__main__.Disk object at 0x0000026E593A5730>
  ```

## 模块（Modules）

- 函数与模块的关系：一个模块中可以包含N多个函数
- 在Python中一个扩展名为.py的文件就是一个模块
- 使用模块的**好处**
  - 方便其他程序和脚本的导入并使用
  - 避免函数名和变量名冲突
  - 提高代码的可维护性
  - 提高代码的可重用性

![image-20220921093104096](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220921093104096.png)

### 自定义模块

#### 创建

新建一个.py文件，名称尽量不要与Python自带的标准模块名称相同

#### 导入

> import 模块名称 [as 别名]
>
> from 模块名称 import 函数/变量/类

```python
import math
from math import pi
```

### 以主程序形式运行

在每个模块的定义中都包括一个记录模块名称的变量\_\_name\_\_,程序可以检查该变量，以确定他们在哪个模块中执行。如果一个模块不是被导入到其他程序中执行，那么他可能在解释器的顶级模块中执行，顶级模块的_\_\_name\_\__变量的值为\_\_main\_\_

```python
id __name__ == '__main__' :
	pass
```

自定义模块：

```python
def add(a, b):
    return a + b


if __name__ == '__main__':
    print(add(10, 20))
```

主程序

```python
import calc

print(calc.add(100, 200))
```

### 内置模块

- sys  与Python解释器及其环境操作相关的标准坤

- time  提供与时间相关的各种函数的标准库

- os  提供了访问操作系统服务功能的标准库

- calendar  提供与日期相关的各种函数的标准库

- urllib  用于读取来自网上（服务器）的数据标准库

- json  用于使用JSON序列化和反序列化对象

- re  用于在字符串中执行正则表达式匹配和替换

- math  提供标准算数运算函数的标准库

- decimal  用于进行精准控制运算精度、有效数位和四舍五入操作的十进制运算

- logging  提供了灵活的记录事件、错误、警告和调试信息等日志信息的功能

  ```python
  import math
  import sys
  import time
  import urllib.request
  
  
  print(sys.getsizeof(24))
  print(sys.getsizeof(True))
  
  print(time.time())  # 秒
  print(time.localtime(time.time()))  # 具体时间
  
  
  print(urllib.request.urlopen('https://www.baidu.com').read()) #爬虫
  print(math.pi)
  ```

### 第三方模块

pip install 模块名

import 模块名

```python
import time

import schedule


def job():
    print("哈哈！！")


schedule.every(3).seconds.do(job)

while True:
    schedule.run_pending()
    time.sleep(1)

```

## 包

包是一个分层次的目录结构，它将一组功能相近的**模块组织**在一个**目录**下

![image-20220921153907470](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220921153907470.png)

**作用**：

- 代码规范
- 避免模块名称冲突

包与目录的**区别**

- 包含\_\_init\_\_.py文件的目录称为包
- 目录里通常不包含\_\_init\_\_.py文件

**导入**

import 包名.模块名

```python
# 导入Package
import package1.module_A
import package1.module_A as ma  # 给包起别名

from package1 import module_A
from package1.module_A import a
# 使用from...import可以导入包、模块、函数、变量
```

## 文件操作

### 编码格式

**常见的字符编码格式**

- Python的解释器使用的是Unicode（内存）

- .py文件再次攀上使用UTF-8存储（外存）

  ![image-20220921173341292](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220921173341292.png)

### 文件读写

文件的读写俗称“IO操作”

**操作流程**

![image-20220922092302832](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220922092302832.png)

**操作原理**

![image-20220922092321680](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220922092321680.png)

**操作**

内置函数open()创建文件对象

![image-20220922092515487](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220922092515487.png)

通过IO流将磁盘文件中的内容与程序中的对象中的内容进行同步

**语法**

![image-20220922092528257](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220922092528257.png)

```python
file = open('a.txt', 'r')
print(file.readlines()) #读多行
file.close()
```

### 常用方法

- read([size])  从文件读取size个字节或字符的内容返回，若省略[size]，则读取到文件末尾，即一次读取文件所有内容
- readline() 从文本文件读取一行内容
- readlines()  把文本文件中每一行都作为独立的字符串对象，并将这些对象放入列表返回
- write(str)  将字符串str内容写入文件
- writelines(s_list)  将字符串列表s_lsit写入文本文件，不添加换行符
- seek(offset,[whence])  把文件指针移动到新的位置，offset表示相对于whence的位置：offset：为正往结束方向移动，为负向开始移动
  - whence不同的值代表不同含义
  - 0：从文件头开始计算（默认）
  - 1：从当前位置开始计算
  - 2：从文件尾开始计算
- tell()  返回文件指针的当前位置
- flush()  把缓冲区的内容写入文件，，但不关闭文件
- close()  把缓冲区的内容写入文件，同时关闭文件，释放文件对象相关资源

```python
# file = open('a.txt', 'r')
# print(file.read(2))
# print(file.readline())
# print(file.readlines())


# file = open('a.txt', 'a')
# # file.write('hello')
# lst = ['java', 'go', 'python']
# file.writelines(lst)
# file.close()

# file = open('a.txt', 'r')
# file.seek(2)
# print(file.read())
# print(file.tell())
# file.close()

file = open('a.txt', 'a')
file.write('hello')
# file.flush()
file.write('world')
file.close()
```

### with语句

with语句可以自动管理上下文资源，不论什么原因跳出with块，都能确保文件正确的关闭，以此来达到释放资源的目的

![image-20220922143341823](https://raw.githubusercontent.com/Thea-wyj/pic/main/img/image-20220922143341823.png)

```python
# coding=UTF-8
# MyContentMgr 实现了特殊方法__enter__和__exit__，称为该类对象遵守了上下文管理器协议，该类对象的实例对象，称为上下文管理器
# MyContentMgr()就被称为上下文管理器


class MyContentMgr(object):
    def __enter__(self):
        print("enter方法被调用执行了")
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print("exit方法被执行调用了") #无论因为何种情况跳出with语句，都会执行exit方法

    def show(self):
        print("show方法被执行调用了")


with MyContentMgr() as file:
    file.show()
```

**文件复制**

```python
with open('logo.png', 'rb') as src_file:
    with open('logo2.png', 'wb') as target_file:
        target_file.write(src_file.read())
```

## 目录操作

- os模块是Python内置的与操作系统功能和文件系统相关的模块，该模块中的语句的执行结果通常与操作系统有关，在不同的操作系统上运行，得到的结果可能不一样。

- os模块与os.path模块用于对目录或文件进行操作

  - getcwd() 返回当前的工作目录

  - listdir(path) 返回指定路径下的文件和目录信息

  - mkdir(path,[mode]) 创建目录

  - nakedirs(path1/path2...[,mode]) 创建多级目录

  - rmdir(path)  删除目录

  - remove(path1/path2)  删除多级目录

  - chdir(path) 将path设置为当前工作目录

```python
import os

# os.system('notepad.exe') # 打开记事本
# os.system('calc.exe') # 打开计算器

# os.startfile('D:\\Program\\tim\\Bin\\TIM.exe') # 运行可执行文件

print(os.getcwd())

lst = os.listdir('../python_test')
print(lst)

# os.mkdir('newdir2')

# os.makedirs('A/B/C')

# os.rmdir('newdir2')

# os.removedirs('A/B/C')

os.chdir('D:\\codes\\test')

print(os.getcwd())
```

**path模块操作目录相关函数**

- abspath(path)  用于获取文件或目录的绝对路径
- exists(path)  用于判断文件或目录是否存在，如果存在返回True
- join(path,name)  将目录与目录或者文件名拼接起来
- spliext()  分离文件名和扩展名
- basename(path)  从一个目录中提取文件名
- dirname(path)  从一个路径中提取文件路径，不包括文件名
- isdir(path)  用于判断是否路径

```python
import os.path

print(os.path.abspath('main.py'))  # D:\codes\python_test\main.py

print(os.path.exists('main.py'), os.path.exists('a.py'))  # True False

print(os.path.join('D:\\codes', 'main.py'))  # D:\codes\main.py

print(os.path.split('D:\\codes\\python_test\\main.py'))  # ('D:\\codes\\python_test', 'main.py')

print(os.path.splitext('main.py'))  # ('main', '.py')

print(os.path.basename('D:\\codes\\python_test\\main.py'))  # main.py
print(os.path.dirname('D:\\codes\\python_test\\main.py'))  # D:\codes\python_test
print(os.path.isdir('D:\\codes\\python_test\\main.py'))  # False
```

### 课堂案例

获取一个目录下的所有.py文件

```python
import os
path = os.getcwd()
lst = os.listdir(path)
for filename in lst:
    if filename.endswith('.py'):
        print(filename)
```

