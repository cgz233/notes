# JavaScript Note

# 基础

## 书写位置

1. 书写在body标签内部

   ```html
   <!DOCTYPE html>
   <html lang="cn">
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
   </head>
   <body>
       <!-- 内部js -->
       <script>
           // 页面弹出警示框
           alert('你好,js~')
       </script>
   </body>
   </html>
   ```

2. 书写在外部，在body中引用

   ```javascript
   // 外部js文件内容
   alert('我是外部的js')
   ```

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
   </head>
   <body>
       <script src="js/my.js">
           // 中间不能写内容
       </script>
   </body>
   </html>
   ```

## 输入和输出

- 输出

  JavaScript 可以接收用户的输入，然后再将输入的结果输出：

  `alert()`、`document.wirte()`

  以数字为例，向 `alert()` 或 `document.write()`输入任意数字，他都会以弹窗形式展示（输出）给用户

- 输入

  向 `prompt()` 输入任意内容会以弹窗形式出现在浏览器中，一般提示用户输入一些内容

```javascript
// 文档输出内容
document.write('我是div标签')
document.write('<h1>我是标题</h1>')
// 控制台打印输出
console.log("看看对不对")
// 输入语句
prompt('请输入你的年龄')
```

## 变量

- 使用let或var声明，var过时，var可以多次声明，let不可以
- const声明一个常量

## 数组

- 声明：`let 数组名 = [数据1, 数据2，... , 数据n]`
- 添加：`push(元素)`方法向数组末尾添加一个元素，`unshift(元素)`方法向数组开头添加一个元素
- 删除：`pop()`方法删除数组最后的一个元素，`shift()`删除数组第一个元素，`splice(起始位置,删除元素个数)`方法删除指定元素

## 数据类型

- 基本数据类型：

  - number 数字型

    运算符：

    - +
    - -
    - *
    - /
    - %

    - NaN代表一个计算错误，它是一个不正确或者未定义的数学操作所得到的结果，NaN是粘性的，任何对NaN的操作都会返回NaN

  - string 字符串型

    模板字符串

    ```javas
    `文字${变量}`
    ```

    ```javascript
    let age = 18
    document.write(`我今年${age}岁了`)
    ```

  - boolen 布尔型

    true or false

  - undefined 未定义型

    只声明变量，不赋值，变量默认为undefined

  - null 空类型

    null 和 undefined 区别：

    - undefined表示没有赋值
    - null 表示赋值了，但是内容为空

    官方解释：把null作为尚未创建的对象

- 引用数据类型：

  - object 对象

检测数据类型：

- typeof运算符可以返回被检测的数据类型，支持两种语法形式：
  1. 作为运算符：`typeof x`（常用）
  2. 函数形式：`typeof(x)`

## 类型转换

- 隐式转换
  - 和字符串相加就会变成字符串
  - +'字符串'，字符串是数字，就会变成number，如果不是就会成NaN
  - 数字-字符串&字符串-数字 就会隐式转换成字符串
- 显示转换
  - `Number(数据)`字符串转换成数字 `Number('111') // 111` `Number('a') // NaN`
  - `parseInt(数据)`只保留整数 `parseInt('12.34px') // 12`
  - `parseFloat(数据)`可以保留小数 `parseInt('12.34px') // 12.34`
- 转换为Boolean型：显示转换：‘’ 、0、undefined、null、false、NaN 转换为布尔值后都是false, 其余则为 true
- null 经过数字转换变为0

## 运算符

- 赋值运算符：+= -= /= %=

- 自增自减运算符：++ --

- 比较运算符：> < >= <=

  ===  左右两边是否**类型**和**值**都相等
  
  ==   左右两边**值**是否相等
  
  !=   左右值不相等
  
  !==  左右两边是否不全等

- 逻辑运算符：&& || ! 与或非

## 逻辑控制

判断：

- if else if else
- 三元运算符：条件 ? 表达式1 : 表达式2
- switch case break default 和java一样

循环：

- while
- for 都和java用法相同

## 函数

- 声明：

  ```javascript
  function say(str1 = 'a',str2 = 'b'){
      console.log(`hi${str1}${str2}`)
      return `${str1}${str2}
  }
  ```

- 调用：`say('hello','hi)`

- 注意：

  - 函数可以没有return，这种情况默认返回值为 undefined
  - return会立即结束当前函数
  - 函数内部只能出现1 次 return，并且 return 下一行代码不会再被执行，所以return 后面的数据不要换行写

匿名函数：

- 函数表达式：

  ```javascript
  let fn = function(x, y) {
      console.log(x + y)
  }
  fn(1 + 2) // 3
  ```

- 立即执行函数

  ~~~javascript
  (function(){xxxx})();
  (function(){xxxx}());
  
  (function(x, y){ console.log(x + y)} )(1 + 2); // 3
  ~~~

  无需调用，立即执行，其实本质已经调用了

  多个立即执行函数之间用分号隔开

## 对象

- 定义：

  ```javascript
  let chen = {
      uname : 'xiaochen',
      age : 18,
      gender : '男'
  }
  ```

- 增删改查：

  ```javascript
  chen.hobby = '打代码' // 增加爱好
  delete chen.gender // 删除性别
  chen.uname = 'XiaoChen' // 修改名字
  console.log(chen.age) // 查询并在控制台打印年龄
  ```

- 访问对象的第二种方法：`对象['属性名']` []里必须要加''

  ```javascript
  let phone = {
      'goods-name': '小米13',
      price: 3999,
      color: '白'
  }
  console.log(phone['goods-name'])
  console.log(phone['price'])
  ```

- 对象的方法

  ```javascript
  let obj = {
      uname: 'chen',
      write: function () {
          console.log('写代码');
      }
  }
  // 调用
  obj.write()
  ```

- 使用for-in遍历对象，for-in不推荐遍历数组(因为遍历得到的是数字下边，还是字符串形式'0','1','2')

  ```javascript
  for (let k in obj) {
      console.log(k) // 得到的是对象的属性名
      console.log(obj[k]) // 使用属性名取出属性对应的值
  }
  ```

## 内置对象

### Math

`Math` 是 JavaScript 中内置的对象，称为数学对象，这个对象下即包含了属性，也包含了许多的方法

**属性**

- Math.PI，获取圆周率

**方法**

- Math.random，生成 0 到 1 间的随机数

- Math.ceil，数字向上取整

- Math.floor，数字向下取整

- Math.round，四舍五入取整

- Math.max，在一组数中找出最大的

- Math.min，在一组数中找出最小的

- Math.pow，幂方法，求某个数的多少次方 `Math.pow(4, 2) // 求 4 的 2 次方`

- Math.sqrt，平方根 `Math.sqrt(16)`

**随机数**

- 生成0-10的随机数：`Math.floor(Math.random() * (10 + 1))`
- 生成5-10的随机数：`Math.floor(Math.random() * (5 + 1)) + 5`
- 生成N-M之间的随机数：`Math.floor(Math.random() * (M - N + 1)) + N`

### Date

- `Date.now`方法返回当前时间距离时间零点（1970年1月1日 00:00:00 UTC）的毫秒数，相当于 Unix 时间戳乘以1000

- `Date`对象提供了一系列`get*`方法，用来获取实例对象某个方面的值

  **实例方法get类**

  getTime()：返回实例距离1970年1月1日00:00:00的毫秒数
  getDate()：返回实例对象对应每个月的几号（从1开始）
  getDay()：返回星期几，星期日为0，星期一为1，以此类推
  getYear()：返回距离1900的年数
  getFullYear()：返回四位的年份
  getMonth()：返回月份（0表示1月，11表示12月）
  getHours()：返回小时（0-23）
  getMilliseconds()：返回毫秒（0-999）
  getMinutes()：返回分钟（0-59）
  getSeconds()：返回秒（0-59）



# APIs

