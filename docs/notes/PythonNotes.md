# Python Notes

## Python 基础语法

### 注释

- 单行注释：

  ```python
  # 我是单行注释
  ```

- 多行注释

  ```python
  '''
  我是多行注释
  '''
  
  """
  我是多行注释
  """
  ```

### 输入输出语句

- 输出语句

  ```python
  print(内容1, 内容2, ......, 内容N)
  print("不换行",end="") # 不换行输出
  ```

- 输入语句

  ```python
  num = input("输入一个数字") // 输入的结果类型为str
  ```

### 运算符

- 算术（数学）运算符

  | 运算符 | 描述   |                             实例                             |
  | ------ | ------ | :----------------------------------------------------------: |
  | +      | 加     |                两个对象相加 a + b 输出结果 30                |
  | -      | 减     |      得到负数或是一个数减去另一个数 a - b 输出结果 -10       |
  | *      | 乘     | 两个数相乘或是返回一个被重复若干次的字符串 a * b 输出结果 200 |
  | /      | 除     |                       b / a 输出结果 2                       |
  | //     | 取整除 |   返回商的整数部分 9//2 输出结果 4 , 9.0//2.0 输出结果 4.0   |
  | %      | 取余   |               返回除法的余数 b % a 输出结果 0                |
  | **     | 指数   |      a**b 为10的20次方， 输出结果 100000000000000000000      |

- 赋值运算符

  | **运算符** | **描述**   | **实例**                                                     |
  | ---------- | ---------- | ------------------------------------------------------------ |
  | =          | 赋值运算符 | 把 = 号右边的结果 赋给 左边的变量，如 num = 1 + 2 * 3，结果num的值为7 |

- 复合赋值运算符

  | **运算符** | **描述**         | **实例**                      |
  | ---------- | ---------------- | ----------------------------- |
  | +=         | 加法赋值运算符   | c += a 等效于 c = c + a       |
  | -=         | 减法赋值运算符   | c -= a 等效于 c = c - a       |
  | *=         | 乘法赋值运算符   | c *= a 等效于 c = c * a       |
  | /=         | 除法赋值运算符   | c /= a 等效于 c = c / a       |
  | %=         | 取模赋值运算符   | c %= a 等效于 c = c % a       |
  | **=        | 幂赋值运算符     | c `**`= a 等效于 c = c `**` a |
  | //=        | 取整除赋值运算符 | c //= a 等效于 c = c // a     |

## 数据类型

### 查看数据类型

- type()

  ```python
  str = "Hello" 
  type(str) # <class 'str'>
  ```

- isinstance()

  ```python
  a = 111
  isinstance(a, int) #True
  ```

- isinstance 和 type 的区别在于：
  - type()不会认为子类是一种父类类型
  - isinstance()会认为子类是一种父类类型

### Number数字

Python3 支持 int、float、bool、complex（复数）

```python
>>> a, b, c, d = 20, 5.5, True, 4+3j
>>> print(type(a), type(b), type(c), type(d))
<class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
```

### list列表

- 定义列表：

  ```python
  name_list = ['Jack','Jone','Marry']
  print(name_list[1]) # Jone
  print(name_list[-1]) # Marry
  ```

- 常用方法：

  | 方法                    | 作用                                         |
  | ----------------------- | -------------------------------------------- |
  | 列表.append(元素)       | 向列表中追加一个元素                         |
  | 列表.extend(容器)       | 将数据容器的内容依次取出，追加到列表尾部     |
  | 列表.insert(下标, 元素) | 在指定下标处，插入指定的元素                 |
  | del 列表[下标]          | 删除列表指定下标元素                         |
  | 列表.pop(下标)          | 删除列表指定下标元素                         |
  | 列表.remove(元素)       | 从前向后，删除此元素第一个匹配项             |
  | 列表.clear()            | 清空列表                                     |
  | 列表.count(元素)        | 统计此元素在列表中出现的次数                 |
  | 列表.index(元素)        | 查找指定元素在列表的下标找不到报错ValueError |
  | len(列表)               | 统计容器内有多少元素                         |

### tuple元组

- 元组一旦定义完成就不可以修改

- 定义：

  ```python
  t1 = (1,'hello',True)
  ```

- 常用方法：

  | **方法**  | **作用**                                           |
  | --------- | -------------------------------------------------- |
  | index()   | 查找某个数据，如果数据存在返回对应的下标，否则报错 |
  | count()   | 统计某个数据在当前元组出现的次数                   |
  | len(元组) | 统计元组内的元素个数                               |

### str字符串

- 定义：

  ```python
  s1 = 'Hello'
  s2 = "Hello"
  s3 = """
  Hello
  """
  ```

- 字符串格式化：

  占位符

  | 格式符号 | 转化                             |
  | -------- | -------------------------------- |
  | %s       | 将内容转换成字符串，放入占位位置 |
  | %d       | 将内容转换成整数，放入占位位置   |
  | %f       | 将内容转换成浮点型，放入占位位置 |

  f”{变量}  {变量}”的方式进行快速格式化

  ```python
  name = "小陈公司"
  stock_price = 20.88
  stock_code = 610086
  stock_price_daily_growth_factor = 1.5
  growth_days = 8
  
  finally_stock_price = stock_price * stock_price_daily_growth_factor ** growth_days
  
  print(f"公司：{name}，股票代码：{stock_code}，当前股价：{stock_price}")
  print("每日增长系数是：%f，经过%d天的增长后，股价达到了：%.2f" % (stock_price_daily_growth_factor, growth_days, finally_stock_price))
  ```

- 常用方法：

  | 方法                               | 作用                                                         |
  | ---------------------------------- | ------------------------------------------------------------ |
  | 字符串[下标]                       | 根据下标索引取出特定位置字符                                 |
  | 字符串.index(字符串）              | 查找给定字符的第一个匹配项的下标                             |
  | 字符串.replace(字符串1, 字符串2)   | 将字符串内的全部字符串1，替换为字符串2不会修改原字符串，而是得到一个新的 |
  | 字符串.split(字符串)               | 按照给定字符串，对字符串进行分隔不会修改原字符串，而是得到一个新的列表 |
  | 字符串.strip()字符串.strip(字符串) | 移除首尾的空格和换行符或指定字符串                           |
  | 字符串.count(字符串)               | 统计字符串内某字符串的出现次数                               |
  | len(字符串)                        | 统计字符串的字符个数                                         |

### 序列的切片

- 序列支持切片，即：列表、元组、字符串，均支持进行切片操作切片：从一个序列中，取出一个子序列

- 语法：序列[起始下标:结束下标:步长]

- 表示从序列中，从指定位置开始，依次取出元素，到指定位置结束，得到一个新序列：

  - 起始下标表示从何处开始，可以留空，留空视作从头开始

  - 结束下标（不含）表示何处结束，可以留空，留空视作截取到结尾

  - 步长表示，依次取元素的间隔

    步长1表示，一个个取元素

    步长2表示，每次跳过1个元素取

    步长N表示，每次跳过N-1个元素取

    步长为负数表示，反向取（注意，起始下标和结束下标也要反向标记）

- 不会影响序列本身，而是会得到一个新的序列（列表、元组、字符串）

- 举例：

  ```python
  my_list = [1, 2, 3, 4, 5]
  new_list = my_list[1:4]	# 下标1开始，下标4（不含）结束，步长1
  print(new_list) # 结果：[2, 3, 4]
  my_tuple = (1, 2, 3, 4, 5)
  new_tuple = my_tuple[:]	# 从头开始，到最后结束，步长1
  print(new_tuple) # 结果：(1, 2, 3, 4, 5)
  my_list = [1, 2, 3, 4, 5]
  new_list = my_list[::2] # 从头开始，到最后结束，步长2
  print(new_list) # 结果：[1, 3, 5]
  my_str = "12345"
  new_str = my_str[:4:2] # 从头开始，到下标4（不含）结束，步长2
  print(new_str) # 结果："13"
  my_str = "12345"
  new_str = my_str[::-1] # 从头（最后）开始，到尾结束，步长-1（倒序）
  print(new_str) # 结果："54321"
  my_list = [1, 2, 3, 4, 5]
  new_list = my_list[3:1:-1] # 从下标3开始，到下标1（不含）结束，步长-1（倒序）
  print(new_list) # 结果：[4, 3]
  my_tuple = (1, 2, 3, 4, 5)
  new_tuple = my_tuple[:1:-2] # 从头（最后）开始，到下标1(不含)结束，步长-2（倒序）
  print(new_tuple) # 结果：(5, 3)
  ```

### set集合

- 不支持元素的重复（自带去重功能）、并且内容无序

- 定义：

  ```python
  names = {'Jack','Jone','marry','jack'}
  print(names) # {'Jack','Jone','marry'}
  ```

- 常用方法：

  | 方法                           | 作用                                                      |
  | ------------------------------ | --------------------------------------------------------- |
  | 集合.add(元素)                 | 集合内添加一个元素                                        |
  | 集合.remove(元素)              | 移除集合内指定的元素                                      |
  | 集合.pop()                     | 从集合中随机取出一个元素                                  |
  | 集合.clear()                   | 将集合清空                                                |
  | 集合1.difference(集合2)        | 得到一个新集合，内含2个集合的差集原有的2个集合内容不变    |
  | 集合1.difference_update(集合2) | 在集合1中，删除集合2中存在的元素集合1被修改，集合2不变    |
  | 集合1.union(集合2)             | 得到1个新集合，内含2个集合的全部元素原有的2个集合内容不变 |
  | len(集合)                      | 得到一个整数，记录了集合的元素数量                        |

### dict字典

- 定义：

  ```python
  stu_score = {'jack': 100, 'jone': 60, 'marry': 50}
  ```

- 常用方法：

  | 方法              | 作用                                          |
  | ----------------- | --------------------------------------------- |
  | 字典[Key]         | 获取指定Key对应的Value值                      |
  | 字典[Key] = Value | 添加或更新键值对                              |
  | 字典.pop(Key)     | 取出Key对应的Value并在字典内删除此Key的键值对 |
  | 字典.clear()      | 清空字典                                      |
  | 字典.keys()       | 获取字典的全部Key，可用于for循环遍历字典      |
  | len(字典)         | 计算字典内的元素数量                          |

### 通用操作

- 遍历：

  5类数据容器都支持for循环遍历

  列表、元组、字符串支持while循环，集合、字典不支持（无法下标索引）

- 通用统计功能：

  len(容器)统计容器的元素个数

  max(容器)统计容器的最大元素

  min(容器)统计容器的最小元素

### 数据类型转换

| 语句        | **说明**              |
| ----------- | --------------------- |
| int(x)      | 将x转换为一个整数     |
| float(x)    | 将x转换为一个浮点数   |
| str(x)      | 将对象 x 转换为字符串 |
| list(容器)  | 将给定容器转换为列表  |
| tuple(容器) | 将给定容器转换为元组  |
| set(容器)   | 将给定容器转换为集合  |

## 循环判断语句

### 判断语句

- if elif else

  ```python
  if 条件1:
      TODO...
  elif 条件2:
      TODO...
  elif 条件N:
      TODO...
  else:
      TODO...
  ```

### 循环语句

- while

  ```python
  while 条件:
      TODO...
      条件循环迭代...
  ```

- for in

  ```python
  hello = "Hello"
  for s in hello:
      print(s)
  ```

## 函数

### 定义

```python
def 函数(参数...):
    函数体
    return 返回值
```

### None类型

- None表示：空的、无实际意义的意思
- 函数返回的None，就表示，这个函数没有返回什么有意义的内容

### 函数多返回值

- 按照返回值的顺序，写对应顺序的多个变量接收即可

- 变量之间用逗号隔开

- 支持不同类型的数据return

  ```python
  def test_return():
      return 1,2
  x, y = test_return()
  print(x) # 1
  print(y) # 2
  ```

### 函数多种传参方式

- 位置参数：调用函数时根据函数定义的参数位置来传递参数

- 关键字参数：函数调用时通过“键=值”形式传递参数

  作用: 可以让函数更加清晰、容易使用，同时也清除了参数的顺序需求

  ```python
  def user_info(name, age, gender):
      print(f"姓名是:{name}, 年龄是:{age}, 性别是:{gender}")
  user_info('Jone', age=18, gender='男')
  user_info(age=18, gender='男', name='Jone') # 可以不按照参数的定义顺序传参
  ```

- 缺省参数：缺省参数也叫默认参数，用于定义函数，为参数提供默认值，调用函数时可不传该默认参数的值（注意：所有位置参数必须出现在默认参数前，包括函数定义和调用）

  作用: 当调用函数时没有传递参数, 就会使用默认是用缺省参数对应的值

  ```python
  def user_info(name, age, gender='男'):
      print(f"姓名是:{name}, 年龄是:{age}, 性别是:{gender}")
  user_info('Jack', 13)
  ```

- 不定长参数：不定长参数也叫可变参数. 用于不确定调用的时候会传递多少个参数(不传参也可以)的场景

  作用: 当调用函数时不确定参数个数时, 可以使用不定长参数

  ```python
  # 不定长 - 位置不定长, *号
  # 传进的所有参数都会被args变量收集，它会根据传进参数的位置合并为一个元组(tuple)，args是元组类型，这就是位置传递
  def user_info(*args):
      print(f"args参数的类型是：{type(args)}，内容是:{args}")
  user_info(1, 2, 3, '小明', '男孩')
  
  # 不定长 - 关键字不定长, **号
  # 参数是“键=值”形式的形式的情况下, 所有的“键=值”都会被kwargs接受, 同时会根据“键=值”组成字典
  def user_info(**kwargs):
      print(f"args参数的类型是：{type(kwargs)}，内容是:{kwargs}")
  user_info(name='小王', age=11, gender='男孩')
  ```

## 文件操作

### 读

| 操作                                  | 功能                                    |
| ------------------------------------- | --------------------------------------- |
| 文件对象 = open(file, mode, encoding) | 打开文件获得文件对象                    |
| 文件对象.read(num)                    | 读取指定长度字节不指定num读取文件全部   |
| 文件对象.readline()                   | 读取一行                                |
| 文件对象.readlines()                  | 读取全部行，得到列表                    |
| for line in 文件对象                  | for循环文件行，一次循环得到一行数据     |
| 文件对象.close()                      | 关闭文件对象                            |
| with open() as f                      | 通过with open语法打开文件，可以自动关闭 |

| **模式** | **描述**                                                     |
| -------- | ------------------------------------------------------------ |
| r        | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式 |
| w        | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，原有内容会被删除。如果该文件不存在，创建新文件 |
| a        | 打开一个文件用于追加。如果该文件已存在，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入 |

### 写

```python
# 1. 打开文件
f = open('python.txt', 'w')

# 2.文件写入
f.write('hello world')

# 3. 内容刷新
f.flush()

f.close()
```

### 追加

```python
# 1. 打开文件，通过a模式打开即可
f = open('python.txt', 'a')

# 2.文件写入
f.write('hello world')

# 3. 内容刷新
f.flush()
```

## 异常

```python
try:
    可能要发生异常的语句
except[异常 as 别名]:
    出现异常的准备手段
[else:]
	未出现异常时应做的事情
[finally:]
	不管出不出现都会做的事情
```

## 模块

### 模块的导入方式

- 模块在使用前需要先导入 导入的语法如下：

  ```python
  [from 模块名] import [模块 | 类 | 变量 | 函数 | *] [as 别名]
  ```

- 常用的组合形式如：

  - `import 模块名`

    ```python
    import 模块名
    import 模块名1，模块名2
    
    模块名.功能名()
    ```

  - `from 模块名 import 类、变量、方法等`

    ```python
    from 模块名 import 功能名
    
    功能名()
    ```

  - `from 模块名 import *`

    ```python
    from 模块名 import *
    
    功能名()
    ```

  - `import 模块名 as 别名`

    ```python
    # 模块定义别名
    import 模块名 as 别名
    
    # 功能定义别名
    from 模块名 import 功能 as 别名
    ```

  - `from 模块名`

  - `import 功能名 as 别名`

### 自定义模块

- 自定义模块并导入

  在Python代码文件中正常写代码即可，通过import、from关键字和导入Python内置模块一样导入即可使用

- `__main__`变量

  `if __name__ == “__main__”`表示，只有当程序是直接执行的才会进入if内部，如果是被导入的，则if无法进入

- `__all__`变量

  如果一个模块文件中有`__all__`变量，当使用`from xxx import *`导入时，只能导入这个列表中的元素

  ```python
  __all__ = ['test_A']
  def test_A():
      print('testA')
  def testB():
      print('testB')
      
  # 另一个文件中
  from my_module import * # 只会导入test_A函数
  ```

## 包

### 定义包

- 从物理上看，包就是一个文件夹，在该文件夹下包含了一个 `__init__.py` 文件，该文件夹可用于包含多个模块文件从逻辑上看，包的本质依然是模块
- 包的作用:当我们的模块文件越来越多时,包可以帮助我们管理这些模块, 包的作用就是包含多个模块，但包的本质依然是模块

### 导入包

- ```python
  import 包名.模块名
  
  包名.模块名.目标
  ```

- ```python
  # 注意：必须在__init__.py文件中添加__all__ = []，控制允许导入的模块列表
  from 包名 import *
  模块名.目标
  ```
  

### 安装第三方包

- cmd输入`pip install 包名称`
- 使用国内镜像`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 包名称`

## 面向对象

```python
class Person:
    name = None
    sex = None
    __hobby = None  # 私有属性，无法直接调用

    def __init__(self, name, age, hobby):
        self.name = name
        self.age = age
        self.__hobby = hobby

    def eat(self, food_name):
        print(f"{self.name}正在吃{food_name}")

    def __do_hobby(self):  # 私有方法，无法直接调用
        print(f"{self.name}正在{self.__hobby}")

    def public_do_hobby(self):
        self.__do_hobby()


person = Person("Jack", 18, "打篮球")
person.sex = "男"
person.__hobby = "打乒乓球"  # 私有成员，无法赋值
person.eat("火锅")
# person.do_hobby() # 报错
person.public_do_hobby()


class Student(Person):  # 继承
    def __init__(self, name, age, hobby, score: float):
        super().__init__(name, age, hobby)
        self.score = score

    def study(self):
        print(f"{self.name}正在学习，考了{self.score}分")


student: Student = Student("小明", 19, "学习", 100)  # 类型注解
student.study()

num: int = 10  # 类型注解
name = "Jack"  # type: str
my_list: list[int] = [1, 2, 3]
my_dict: dict[str, int] = {"age": 11, "num": 3}


def func(data: list) -> list:  # 方法类型注解
    return data


# Union
from typing import Union

my_list: list[Union[str, int]] = [1, 2, "jack", "小明"]
my_dict: dict[str, Union[str, int]] = {"name": "Jack", "age": 33}

```

| 方法       | 功能                                           | 解释                               |
| ---------- | ---------------------------------------------- | ---------------------------------- |
| `__init__` | 构造方法，可用于创建类对象的时候设置初始化行为 | 类似于Java的构造方法               |
| `__str__`  | 用于实现类对象转字符串的行为                   | 类似于Java重写toString()           |
| `__lt__`   | 用于2个类对象进行小于或大于比较                |                                    |
| `__le__`   | 用于2个类对象进行小于等于或大于等于比较        |                                    |
| `__eq__`   | 用于2个类对象进行相等比较                      | 类似于Java重写equals()和hashCode() |

