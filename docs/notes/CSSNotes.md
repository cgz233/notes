# CSS Notes

# CSS基础

## CSS简介

- CSS 的全称为：层叠样式表 ( Cascading Style Sheets ) 
- CSS 也是一种标记语言，用于给 HTML 结构设置样式，例如：文字大小、颜色、元素宽高等

## CSS的编写位置

### 行内样式

- 写在标签的 style 属性中，（又称：内联样式）
- 语法：`<h1 style="color:red;font-size:60px;">Hello,CSS</h1>`

### 内部样式

- 写在 html 页面内部，将所有的 CSS 代码提取出来，单独放在`<style>`标签中

- 语法：

  ```html
  <style>
  	h1 {
  		color: red;
  		font-size: 40px;
  	}
  </style>
  ```

### 外部样式

- 写在单独的 .css 文件中，随后在 HTML 文件中引入使用

- 语法：

  1. 新建一个扩展名为 .css 的样式文件，把所有 CSS 代码都放入此文件中

     ```css
     h1{
     	color: red;
     	font-size: 40px;
     }
     ```

  2. 在 HTML 文件中引入 .css 文件

     ```html
     <link rel="stylesheet" href="./xxx.css">
     ```

## 样式表优先级

- 优先级规则：**行内样式** > **内部样式** = **外部样式**
- 内部样式、外部样式，这二者的优先级相同，且：后面的会覆盖前面的（简记：“后来者居上”）
- 同一个样式表中，优先级也和编写顺序有关，且：后面的会覆盖前面的（简记：“后来者居上”）

## CSS语法规范

- CSS 语法规范由两部分构成：

  **选择器**：找到要添加样式的元素

  **声明块**：设置具体的样式（**声明块**是由一个或多个**声明**组成的），声明的格式为： 属性名: 属性值;

- 注释的写法：

  ```css
  /* 给h1元素添加样式 */
  h1 {
  	/* 设置文字颜色为红色 */
  	color: red;
  	/* 设置文字大小为40px */
  	font-size: 40px
  }
  ```



# CSS选择器

## CSS基本选择器

### 通配选择器

- 作用：可以选中所有的 HTML 元素

- 语法：

  ```css
  * {
  	属性名: 属性值;
  }
  ```

### 元素选择器

- 作用：为页面中 **某种元素** 统一设置样式

- 语法：

  ```css
  标签名 {
  	属性名: 属性值;
  }
  ```

### 类选择器

- 作用：根据元素的 class 值，来选中某些元素

- 语法：

  ```css
  .类名 {
  	属性名: 属性值;
  }
  ```

- 注意：

  1. 元素的 class 属性值不带`.`，但 CSS 的类选择器要带`.`
  2. class 值，是我们自定义的，按照标准：不要使用纯数字、不要使用中文、尽量使用英文与数字的组合，若由多个单词组成，使用 - 做连接，例如： left-menu ，且命名要有意义，做到 “见名知意”
  3. 一个元素不能写多个 class 属性
  4. 一个元素的 class 属性，能写多个值，要用空格隔开

### ID选择器

- 作用：根据元素的 id 属性值，来**精准的**选中**某个**元素

- 语法：

  ```css
  #id值 {
  	属性名: 属性值;
  }
  ```

## CSS复合选择器

### 交集选择器

- 作用：选中同时符合多个条件的元素

- 语法：`选择器1选择器2选择器3...选择器n {}`

- 举例：

  ```css
  /* 选中：类名为beauty的p元素，为此种写法用的非常多！！！！ */
  p.beauty {
  	color: blue;
  }
  /* 选中：类名包含rich和beauty的元素 */
  .rich.beauty {
  	color: green;
  }
  ```

- 注意：

  1. 有标签名，标签名必须写在前面
  2. 交集选择器中不可能出现两个元素选择器

### 并集选择器

- 作用：选中多个选择器对应的元素，又称：**分组选择器**

- 语法：`选择器1, 选择器2, 选择器3, ... 选择器n {}`

- 举例：

  ```css
  /* 选中id为peiqi，或类名为rich，或类名为beauty的元素 */
  #peiqi,
  .rich,
  .beauty {
      font-size: 40px;
      background-color: skyblue;
      width: 200px;
  }
  ```

### 后代选择器

- 作用：选中指定元素中，符合要求的后代元素

- 语法：`选择器1 选择器2 选择器3 ...... 选择器n {}` （先写祖先，再写后代）

  选择器之间，用空格隔开

- 举例：

  ```css
  /* 选中ul中的所有li */
  ul li {
  	color: red;
  }
  /* 选中ul中所有li中的a */
  ul li a {
  	color: orange;
  }
  /* 选中类名为subject元素中的所有li */
  .subject li {
  	color: blue;
  }
  /* 选中类名为subject元素中的所有类名为front-end的li */
  .subject li.front-end {
  	color: blue;
  }
  ```

- 注意：
  1. 后代选择器，最终选择的是后代，不选中祖先
  2. 儿子、孙子、重孙子，都算是后代
  3. 结构一定要符合之前讲的 HTML 嵌套要求，例如：不能 p 中写 h1 ~ h6

### 子代选择器

- 作用：选中指定元素中，符合要求的**子**元素（**儿子元素**）。（先写父，再写子）

- 语法：`选择器1 > 选择器2 > 选择器3 > ...... 选择器n {}`

  选择器之间，用 > 隔开

- 举例：

  ```css
  /* div中的子代a元素 */
  div>a {
  color: red;
  }
  /* 类名为persons的元素中的子代a元素 */
  .persons>a{
  	color: red;
  }
  ```

### 兄弟选择器

- 相邻兄弟选择器：

  - 作用：选中指定元素后，符合条件的**相邻兄弟**元素

  - 语法：`选择器1+选择器2 {}`

  - 举例：

    ```css
    /* 选中div后相邻的兄弟p元素 */
    div+p {
    	color:red;
    }
    ```

- 通用兄弟选择器：

  - 作用：选中指定元素后，符合条件的**所有兄弟**元素

  - 语法：`选择器1~选择器2 {}`

  - 举例：

    ```css
    /* 选中div后的所有的兄弟p元素 */
    div~p {
    	color:red;
    }
    ```

- 注意：两种兄弟选择器，选择的是**下面**的兄弟

### 属性选择器

- 作用：选中属性值符合一定要求的元素

- 语法：

  1. `[属性名]` 选中**具有**某个属性的元素
  2. `[属性名="值"]` 选中包含某个属性，且属性值**等于**指定值的元素
  3. `[属性名^="值"]` 选中包含某个属性，且属性值以指定的值**开头**的元素
  4. `[属性名$="值"]` 选中包含某个属性，且属性值以指定的值**结尾**的元素
  5. `[属性名*=“值”]` 选择包含某个属性，属性值**包含**指定值的元素

- 举例：

  ```css
  /* 选中具有title属性的元素 */
  div[title]{color:red;}
  /* 选中title属性值为atguigu的元素 */
  div[title="atguigu"]{color:red;}
  /* 选中title属性值以a开头的元素 */
  div[title^="a"]{color:red;}
  /* 选中title属性值以u结尾的元素 */
  div[title$="u"]{color:red;}
  /* 选中title属性值包含g的元素 */
  div[title*="g"]{color:red;}
  ```

### 伪类选择器

- 作用：选中特殊状态的元素

- 常用的伪类选择器：

  - **动态伪类：**

    1. `:link` 超链接**未被访问**的状态

    2. `:visited` 超链接**访问过**的状态

    3. `:hover` 鼠标**悬停**在元素上的状态

    4. `:active` 元素**激活**的状态

       以上四个注意点：遵循 LVHA 的顺序，即： link 、 visited 、 hover 、 active

    5. `:focus` 获取焦点的元素

       表单类元素才能使用 :focus 伪类

  - **结构伪类：**

    **常用的：**

    1. `:first-child` 所有兄弟元素中的**第一个**

    2. `:last-child` 所有兄弟元素中的**最后一个**

    3. `:nth-child(n)` 所有兄弟元素中的**第** **n** **个**

    4. `:first-of-type` 所有**同类型**兄弟元素中的**第一个**

    5. `:last-of-type` 所有**同类型**兄弟元素中的**最后一个**

    6. `:nth-of-type(n)` 所有**同类型**兄弟元素中的**第 n 个**

       关于 n 的值：

       1. 0 或 不写 ：什么都选不中
       2. n ：选中所有子元素
       3. 1~正无穷的整数 ：选中对应序号的子元素
       4. 2n 或 even ：选中序号为偶数的子元素
       5. 2n+1 或 odd ：选中序号为奇数的子元素
       6. -n+3 ：选中的是前 3 个

    **不常用：**

    1. :nth-last-child(n) 所有兄弟元素中的**倒数第** **n** **个**
    2. :nth-last-of-type(n) 所有**同类型**兄弟元素中的 **倒数第 n 个**
    3. :only-child 选择没有兄弟的元素（独生子女）
    4. :only-of-type 选择没有**同类型**兄弟的元素
    5. :root 根元素
    6. :empty 内容为空元素（空格也算内容）

  - **否定伪类：**

    :not(选择器) 排除满足括号中条件的元素

  - **UI伪类：**

    1. :checked 被选中的复选框或单选按钮
    2. :enable 可用的表单元素（没有 disabled 属性）
    3. :disabled 不可用的表单元素（有 disabled 属性）

  - **目标伪类（了解）**

    :target 选中锚点指向的元素。

  - **语言伪类（了解）**

    :lang() 根据指定的语言选择元素（本质是看 lang 属性的值）

### 伪元素选择器

- 作用：选中元素中的一些特殊位置

- 常用伪元素：

  `::first-letter` 选中元素中的**第一个文字**

  `::first-line` 选中元素中的**第一行文字**

  `::selection` 选中**被鼠标选中的**内容

  `::placeholder` 选中输入框的**提示文字**

  `::before` 在元素**最开始**的位置，创建一个子元素（必须用 content 属性指定内容）

  `::after` 在元素**最后**的位置，创建一个子元素（必须用 content 属性指定内容）

## 选择器的优先级

- 简单描述：

  **行内样式** > **ID选择器** > **类选择器** > **元素选择器** > **通配选择器**

- 详细描述：

  1. 计算方式：每个选择器，都可计算出一组权重，格式为： (a,b,c)

     a : **ID** 选择器的个数

     b : **类、伪类、属性** 选择器的个数

     c : **元素、伪元素** 选择器的个数

  2. 比较规则：按照**从左到右**的顺序，依次比较大小，当前位胜出后，后面的不再对比，例如：

     (1,0,0) > (0,2,2)

     (1,1,0) > (1,0,3)

     (1,1,3) > (1,1,2)

  3. 特殊规则：

     1. **行内样式**权重大于**所有选择器**
     2. !important 的权重，大于**行内样式**，大于**所有选择器**，**权重最高！**

  4. 图示：

     <img src="https://image.cgz233.cn/images/202304200906583.png" alt="image-20230420090557997" style="zoom: 15%;" /> 



# CSS常用属性

## 颜色的表示

### 颜色名

- 编写方式：直接使用颜色对应的英文单词，编写比较简单
- 具体颜色名参考 MDN 官方文档：https://developer.mozilla.org/en-US/docs/Web/CSS/named-color

### rgb或rgba

- 编写方式：使用 红、黄、蓝 这三种光的三原色进行组合
  - r 表示 红色
  - g 表示 绿色
  - b 表示 蓝色
  - a 表示 透明度

### HEX或HEXA

- HEX 的原理同与 rgb 一样，依然是通过：红、绿、蓝色 进行组合，只不过要用 6位（分成3组） 来表达，格式为：#rrggbb

## CSS字体属性

### 字体大小

- 属性名： font-size

- 作用：控制字体的大小

- 语法：

  ```css
  div {
  	font-size: 40px;
  }
  ```

### 字体族

- 属性名： font-family

- 作用：控制字体类型

- 语法：

  ```css
  div {
  	font-family: "STCaiyun","Microsoft YaHei",sans-serif
  }
  ```

### 字体风格

- 属性名： font-style

- 作用：控制字体是否为斜体

- 常用值：

  1. normal ：正常（默认值）
  2. italic ：斜体（使用字体自带的斜体效果）
  3. oblique ：斜体（强制倾斜产生的斜体效果）

- 语法：

  ```css
  div {
  	font-style: italic;
  }
  ```

### 字体粗细

- 属性名： font-weight、

- 作用：控制字体的粗细

- 常用值：

  - 关键词

    1. lighter：细
    2. normal：正常

    3. bold：粗
    4. bolder：很粗 （多数字体不支持）

  - 数值：

    1. 100~1000且无单位，数值越大，字体越粗（或一样粗，具体得看字体设计时的精确程度）

    2. 100~300等同于lighter，400~500 等同于normal，600及以上等同于bold

- 语法：

  ```css
  div {
  	font-weight: bold;
  }
  div {
  	font-weight: 600;
  }
  ```

### 字体复合写法

- 属性名： font ，可以把上述字体样式合并成一个属性
- 作用：将上述所有字体相关的属性复合在一起编写
- 编写规则：
  1. 字体大小、字体族必须都写上
  2. 字体族必须是最后一位、字体大小必须是倒数第二位。
  3. 各个属性间用空格隔开
- 实际开发中更推荐复合写法，但这也不是绝对的，比如只想设置字体大小，那就直接用 fontsize 属性

## CSS文本属性

### 文本颜色

- 属性名： color
- 作用：控制文字的颜色
- 可选值：
  1. 颜色名
  2. rgb 或 rgba
  3. HEX 或 HEXA （十六进制）
  4. HSL 或 HSLA

### 文本间距

- 字母间距： letter-spacing
- 单词间距： word-spacing （通过空格识别词）
- 属性值为像素（ px ），正值让间距增大，负值让间距缩小

### 文本修饰

- 属性名： text-decoration

- 作用：控制文本的各种装饰线

- 可选值：

  1. none ： 无装饰线（常用）

  2. underline ：下划线（常用）
  3. overline ： 上划线

  4. line-through ： 删除线

  可搭配如下值使用：

  1. dotted ：虚线
  2. wavy ：波浪线
  3. 也可以指定颜色

- 举例：

  ```css
  a {
  	text-decoration: none;
  }
  ```

### 文本缩进

- 属性名：text-indent

- 作用：控制文本首字母的缩进

- 属性值：css 中的长度单位，例如：px

- 举例：

  ```css
  div {
  	text-indent:40px;
  }
  ```

### 文本对齐_水平

- 属性名：text-align
- 作用：控制文本的水平对齐方式
- 常用值：
  1. left ：左对齐（默认值）
  2. right ：右对齐
  3. center ：居中对齐

### 行高

- 属性名： line-height
- 作用：控制一行文字的高度
- 可选值：
  1. normal ：由浏览器根据文字大小决定的一个默认值

  2. 像素( px )

  3. 数字：参考自身 font-size 的倍数（很常用）

  4. 百分比：参考自身 font-size 的百分比

- 备注：由于字体设计原因，文字在一行中，并不是绝对垂直居中，若一行中都是文字，不会太影响观感

- 举例：

  ```css
  div {
      line-height: 60px;
      line-height: 1.5;
      line-height: 150%;
  }
  ```

- 行高注意事项：

  1. line-height 过小会怎样？—— 文字产生重叠，且最小值是 0 ，不能为负数

  2. line-height 是可以继承的，且为了能更好的呈现文字，最好写数值

  3. line-height 和 height 是什么关系？

     设置了 height ，那么高度就是 height 的值

     不设置 height 的时候，会根据 line-height 计算高度

- 应用场景：

  1. 对于多行文字：控制行与行之间的距离

  2. 对于单行文字：让 height 等于 line-height ，可以实现文字垂直居中

  备注：由于字体设计原因，靠上述办法实现的居中，并不是绝对的垂直居中，但如果一行中都是文字，不会太影响观感

### 文本对齐_垂直

1. **顶部：**无需任何属性，在垂直方向上，默认就是顶部对齐

2. **居中：**对于单行文字，让 height = line-height 即可

3. **底部：**对于单行文字，目前一个临时的方式：

   让 line-height = ( height × 2 ) - font-size - x 

   备注： x 是根据字体族，动态决定的一个值

### vertical-align

- 属性名： vertical-align
- 作用：用于指定**同一行元素之间**，或 **表格单元格** 内文字的 **垂直对齐方式**
- 常用值：
  1. baseline （默认值）：使元素的基线与父元素的基线对齐。
  2. top ：使元素的**顶部**与其**所在行的顶部**对齐。
  3. middle ：使元素的**中部**与**父元素的基线**加上父元素**字母** x **的一半**对齐。
  4. bottom ：使元素的**底部**与其**所在行的底部**对齐
- 特别注意： vertical-align 不能控制块元素

## CSS列表属性

列表相关的属性，可以作用在 ul 、 ol 、 li 元素上

|CSS 属性名 |功能 |属性值|
|--|--|--|
|list-style-type |设置列表符号 |常用值如下：<br/>none ：不显示前面的标识（很常用！）<br/>square ：实心方块<br/>disc ：圆形<br/>decimal ：数字<br/>lower-roman ：小写罗马字<br/>upper-roman ：大写罗马字<br/>lower-alpha ：小写字母<br/>upper-alpha ：大写字母|
|list-style-position |设置列表符号的位置 |inside ：在 li 的里面 <br/>outside ：在 li 的外边|
|list-style-image| 自定义列表符号 |url(图片地址)|
|list-style |复合属性 |没有数量、顺序的要求|

## CSS表格属性

边框相关属性（所有元素都能用）

|CSS 属性名 | 功能 | 属性值 |
|---------|------|-----|
|border-width | 边框宽度 |CSS 中可用的长度值 |
|border-color | 边框颜色 |CSS 中可用的颜色值 |
|border-style | 边框风格 |none 默认值<br/>solid 实线<br/>dashed 虚线<br/>dotted 点线<br/>double 双实线 |
|border | 边框复合属性 | 没有数量、顺序的要求 |

表格独有属性

|CSS 属性名 |功能| 属性值|
|--|--|--|
|table-layout |设置列宽度| auto ：自动，列宽根据内容计算（默认值）<br/>fixed ：固定列宽，平均分 |
|border-spacing |单元格间距 |CSS 中可用的长度值<br/>生效的前提：单元格边框不能合并|
|border-collapse |合并单元格边框| collapse ：合并<br/>separate ：不合并 |
|empty-cells |隐藏没有内容的单元格| show ：显示，默认<br/>hide ：隐藏<br/>生效前提：单元格不能合并 |
|caption-side |设置表格标题位置|top ：上面（默认值）<br/>bottom ：在表格下面|

## CSS背景属性

|css 属性名 |功能 |属性值|
|--|--|--|
|background-color |设置背景颜色 |符合 CSS 中颜色规范的值。默认背景颜色是 transparent 。|
|background-image |设置背景图片 |url(图片的地址)|
|background-repeat |设置背景重复方式 |repeat ：重复，铺满整个元素，默认值<br/>repeat-x ：只在水平方向重复<br/>repeat-y ：只在垂直方向重复<br/>no-repeat ：不重复|
|background-position |设置背景图位置 |**通过关键字设置位置：**<br/>写两个值，用空格隔开<br/>水平：left、center、right<br/>垂直：top、center、bottom<br/>如果只写一个值，另一个方向的值取 center<br/>**通过长度指定坐标位置：**<br/>以元素左上角，为坐标原点，设置图片左上角的位置<br/>两个值，分别是x坐标和y坐标<br/>只写一个值，会被当做x坐标，y坐标取center|
|background |复合属性 |没有数量和顺序要求|

## CSS鼠标属性

| css 属性名 | 功能               | 属性值                                                       |
| ---------- | ------------------ | ------------------------------------------------------------ |
| cursor     | 设置鼠标光标的样式 | pointer ：小手<br/>move ：移动图标<br/>text ：文字选择器<br/>crosshair ：十字架<br/>wait ：等待<br/>help ：帮助 |

```css
/* 自定义鼠标光标 */
cursor: url("./arrow.png"),pointer;
```

# CSS盒子模型

 

## CSS长度单位

1. px ：像素

2. em ：相对元素 font-size 的倍数

3. rem ：相对根字体大小，html标签就是根

4. % ：相对父元素计算

## 元素的显示模式

### 块元素(block)

又称：块级元素

特点：

1. 在页面中**独占一行**，不会与任何元素共用一行，是从上到下排列的

2. 默认宽度：撑满**父元素**

3. 默认高度：由**内容**撑开

4. **可以**通过 CSS 设置宽高

元素列表：

1. 主体结构标签：`<html>`、`<body>`

2. 排版标签：`<h1>`~`<h6>`、`<hr>`、`<p>`、`<pre>`、`<div>`

3. 列表标签：`<ul>`、`<ol>`、`<li>`、`<dl>`、`<dt>`、`<dd>`

4. 表格相关标签：`<table>`、`<tbody>`、`<thead>`、`<tfoot>`、`<tr>`、`<caption>`

5. `<form>` 与 `<option>`

### 行内元素(inline)

又称：内联元素

特点:

1. 在页面中**不独占一行**，一行中不能容纳下的行内元素，会在下一行继续从左到右排列

2. 默认宽度：由**内容**撑开

3. 默认高度：由**内容**撑开

4. **无法**通过 CSS 设置宽高

元素列表：

1. 文本标签： `<br>`、`<em>`、`<strong>`、`<sup>`、`<sub>`、`<del>`、`<ins>`

2. `<a>`与`<label>`

### 行内块元素(inline-block)

又称：内联块元素

特点：

1. 在页面中**不独占一行**，一行中不能容纳下的行内元素，会在下一行继续从左到右排列

2. 默认宽度：由**内容**撑开
3. 默认高度：由**内容**撑开
4. **可以**通过 CSS 设置宽高

元素列表：

1. 图片：`<img>`

2. 单元格：`<td>`、`<th>`

3. 表单控件：`<input>`、`<textarea>`、`<select>`、`<button>`

4. 框架标签：`<iframe>`

## 修改元素的样式显示

通过CSS中的display属性可以修改元素的默认显示模式，常用值如下：

|值 |描述|
|--|--|
|none |元素会被隐藏|
|block |元素将作为块级元素显示|
|inline |元素将作为内联元素显示|
|inline-block |元素将作为行内块元素显示|

## 盒子模型的组成

CSS 会把所有的 HTML 元素都看成一个盒子，所有的样式也都是基于这个盒子

1. margin（外边距）：盒子与外界的距离
2. border（边框）：盒子的边框
3. padding（内边距）：紧贴内容的补白区域
4. content（内容）：元素中的文本或后代元素都是它的内容

<img src="C:\Users\20696\AppData\Roaming\Typora\typora-user-images\image-20230420212404134.png" alt="image-20230420212404134" style="zoom: 67%;" /> 

- 盒子的大小 = content + 左右 padding + 左右 border
- 注意：外边距 margin 不会影响盒子的大小，但会影响盒子的位置

## 盒子内容区(content)

|CSS 属性名 |功能 |属性值|
|--|--|--|
|width |设置内容区域宽度 |长度|
|max-width |设置内容区域的最大宽度 |长度|
|min-width |设置内容区域的最小宽度 |长度|
|height |设置内容区域的高度 |长度|
|max-height |设置内容区域的最大高度 |长度|
|min-height |设置内容区域的最小高度 |长度|

## 关于默认宽度

- 所谓的默认宽度，就是不设置width属性时，元素所呈现出来的宽度

- 总宽度 = 父的content - 自身的左右margin

- 内容区的宽度 = 父的content - 自身的左右margin - 自身的左右border - 自身的左右padding

## 盒子的内间距(padding)

|CSS 属性名 |功能 |属性值|
|--|--|--|
|padding-top |上内边距 |长度|
|padding-right |右内边距 |长度|
|padding-bottom |下内边距 |长度|
|padding-left |左内边距 |长度|
|padding| 复合属性 |长度，可以设置 1 ~ 4 个值|

padding 复合属性的使用规则：

1. padding: 10px; 四个方向内边距都是10px 

2. padding: 10px 20px; 上10px，左右20px（上下、左右）

3. padding: 10px 20px 30px; 上10px，左右 20px ，下 30px（上、左右、下）

4. padding: 10px 20px 30px 40px; 上10px，右20px，下30px，左40px（上、右、下、左）

注意点：

1. padding的值不能为负数

2. 行内元素的左右内边距是没问题的，上下内边距不能完美的设置

3. 块级元素、行内块元素，四个方向内边距都可以完美设置

## 盒子边框(border)

|CSS 属性名 |功能 |属性值|
|--|--|--|
|border-style |边框线风格<br/>复合了四个方向的边框风格 |none：默认值<br/>solid：实线<br/>dashed：虚线<br/>dotted：点线<br/>double：双实线<br/>......|
|border-width |边框线宽度<br/>复合了四个方向的边框宽度 |长度，默认3px|
|border-color |边框线颜色<br/>复合了四个方向的边框颜色 |颜色，默认黑色|
|border |复合属性 |值没有顺序和数量要求|
| border-left<br/>border-left-style<br/>border-left-width<br/>border-left-color<br/>border-right<br/>border-right-style<br/>border-right-width<br/>border-right-color<br/>border-top<br/>border-top-style<br/>border-top-width<br/>border-top-color<br/>border-bottom<br/>border-bottom-style<br/>border-bottom-width<br/>border-bottom-color | 分别设置各个方向的边框 |同上|

## 盒子外边距(margin)

|CSS 属性名 |功能 |属性值|
|--|--|--|
|margin-left| 左外边距| CSS 中的长度值|
|margin-right| 右外边距 |CSS 中的长度值|
|margin-top |上外边距 |CSS 中的长度值|
|margin-bottom |下外边距 |CSS 中的长度值|
|margin |复合属性，可以写1~4个值，规律同padding（顺时针） |CSS 中的长度值|

### margin的注意事项

1. 子元素的margin，是参考父元素的content计算的。（因为是父亲的content中承装着子元素）

2. 上margin、左margin：影响自己的位置；下 margin、右margin：影响后面兄弟元素的位置

3. 块级元素、行内块元素，均可以完美地设置四个方向的margin；但行内元素，左右margin可以完美设置，上下margin设置无效

4. margin的值也可以是auto，如果给一个块级元素设置左右margin都为auto，该块级元素会在父元素中水平居中

5. margin的值可以是负值

### margin塌陷问题

什么是 margin 塌陷？

- 第一个子元素的上 margin 会作用在父元素上，最后一个子元素的下 margin 会作用在父元素上

如何解决 margin 塌陷？

- 方案一： 

  给父元素设置不为0的padding

- 方案二： 

  给父元素设置宽度不为0的border 

- 方案三：

  给父元素设置css样式overflow:hidden

### margin合并问题

- 什么是 margin 合并？

  上面兄弟元素的下外边距和下面兄弟元素的上外边距会合并，取一个最大的值，而不是相加。

- 如何解决 margin 塌陷？

  无需解决，布局的时候上下的兄弟元素，只给一个设置上下外边距就可以了

## 处理溢出内容

|CSS 属性名 |功能 |属性值|
|--|--|--|
|overflow |溢出内容的处理方式 |visible ：显示，默认值<br/>hidden ：隐藏<br/>scroll ：显示滚动条，不论内容是否溢出<br/>auto ：自动显示滚动条，内容不溢出不显示|
|overflow-x| 水平方向溢出内容的处理方式| 同overflow|
|overflow-y |垂直方向溢出内容给的处理方式 |同overflow|

注意：

1. overflow-x、overflow-y不能一个是hidden，一个是 visible，是实验性属性，不建议使用

2. overflow常用的值是hidden和auto，除了能处理溢出的显示方式，还可以解决很多疑难杂症

## 隐藏元素的方式

- 方式一：visibility 属性

  visibility 属性默认值是 show ，如果设置为 hidden ，元素会隐藏

  元素看不见了，还占有原来的位置（元素的大小依然保持）

- 方式二：display属性

  设置 display:none ，就可以让元素隐藏

  彻底地隐藏，不但看不见，也不占用任何位置，没有大小宽高

## 样式的继承

有些样式会继承，元素如果本身设置了某个样式，就使用本身设置的样式；但如果本身没有设置某个样式，会从父元素开始一级一级继承（优先继承离得近的祖先元素）

- 会继承的CSS样式

  字体属性、文本属性（除了vertical-align）、文字颜色 等

- 不会继承的CSS样式

  边框、背景、内边距、外边距、宽高、溢出方式 等

一个规律：能继承的属性，都是不影响布局的，简单说：都是和盒子模型没关系的

## 默认样式

元素一般都些默认的样式，例如：

1. `<a>`元素：下划线、字体颜色、鼠标小手

2. `<h1>`~`<h6>` 元素： 文字加粗、文字大小、上下外边距

3. `<p>`元素：上下外边距

4. `<ul>`、`ol`元素：左内边距

5. body 元素： 8px 外边距（4个方向）

优先级：元素的默认样式 > 继承的样式，所以如果要重置元素的默认样式，选择器一定要直接选择器到该元素

## 布局小技巧

1. 行内元素、行内块元素，可以被父元素当做文本处理

   即：可以像处理文本对齐一样，去处理：行内、行内块在父元素中的对齐

   例如：text-align、line-height、text-indent等

2. 如何让子元素，在父亲中水平居中：

   若子元素为块元素，给父元素加上：`margin:0 auto;`

   若子元素为行内元素、行内块元素，给父元素加上：`text-align:center`

3. 如何让子元素，在父亲中垂直居中：

   若子元素为块元素，给子元素加上：`margin-top`，值为：`(父元素content－子元素盒子总高)/2`

   若子元素为行内元素、行内块元素：

   - 让父元素的`height = line-height`，每个子元素都加上：`vertical-align:middle;`
   - 补充：若想绝对垂直居中，父元素 font-size 设置为0

## 元素之间的空白问题

产生的原因：

- 行内元素、行内块元素，彼此之间的换行会被浏览器解析为一个空白字符

解决方案：

1. 去掉换行和空格（不推荐）

2. 给父元素设置`font-size:0`，再给需要显示文字的元素，单独设置字体大小（推荐）

## 行内块的幽灵空白问题

产生原因：

- 行内块元素与文本的基线对齐，而文本的基线与文本最底端之间是有一定距离的。

解决方案：

1. 给行行内块设置vertical，值不为baseline即可，设置为middel、bottom、top均可

2. 若父元素中只有一张图片，设置图片为display:block

3. 给父元素设置font-size: 0 。如果该行内块内部还有文本，则需单独设置fontsize

# 浮动

## 浮动的简介

- 在最初，浮动是用来实现文字环绕图片效果的，现在浮动是主流的页面布局方式之一

- 浮动相关属性

  |CSS 属性 |功能| 属性值|
  |--|--|--|
  |float |设置浮动| left：设置左浮动<br/>right：设置右浮动<br/>none：不浮动，默认值 |
  |clear |清除浮动<br/>清除前面兄弟元素浮动元素的响应| left：清除前面左浮动的影响<br/>right：清除前面右浮动的影响<br/>both：清除前面左右浮动的影响 |


## 元素浮动后的特点

1. 脱离文档流

2. 不管浮动前是什么元素，浮动后：默认宽与高都是被内容撑开（尽可能小），而且可以设置宽高

3. 不会独占一行，可以与其他元素共用一行

4. 不会margin合并，也不会margin塌陷，能够完美的设置四个方向的margin和padding

3. 不会像行内块一样被当做文本处理（没有行内块的空白问题）

## 浮动产生的影响

**产生的影响：**

- 对兄弟元素的影响：后面的兄弟元素，会占据浮动元素之前的位置，在浮动元素的下面；对前面的兄弟无影响
- 对父元素的影响：不能撑起父元素的高度，导致父元素高度塌陷；但父元素的宽度依然束缚浮动的元素

**解决浮动产生的影响：**

1. 给父元素指定高度

2. 给父元素也设置浮动，带来其他影响

3. 给父元素设置`overflow:hidden`

4. 在所有浮动元素的最后面，添加一个块级元素，并给该块级元素设置`clear:both`

5. 给浮动元素的父元素，设置伪元素，通过伪元素清除浮动，原理与方案四相同

   ```css
   .parent::after {
       content: "";
       display: block;
       clear:both;
   }
   ```

布局中的一个原则：设置浮动的时候，兄弟元素要么全都浮动，要么全都不浮动

## 利用浮动创建布局

<img src="https://image.cgz233.cn/images/202304211557176.png" alt="image-20230421155652617" style="zoom: 33%;" /> 

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .leftfix {
            float: left;
        }

        .rightfix {
            float: right;
        }

        .cleanfix::after {
            content: '';
            display: block;
            clear: both;
        }

        .outer {
            width: 960px;
            margin: 0 auto;
            text-align: center;
        }

        .banner {
            margin-top: 10px;
        }

        .logo {
            width: 200px;
        }

        .banner1 {
            width: 540px;
            margin: 0 10px;
        }

        .banner2 {
            width: 200px;
        }

        .logo,
        .banner1,
        .banner2 {
            height: 80px;
            background-color: #ccc;
            line-height: 80px;
        }

        .menu {
            width: 960px;
            height: 30px;
            background-color: #ccc;
            margin-top: 10px;
            line-height: 30px;
        }

        .content {
            margin-top: 10px;
        }

        .item1,
        .item2 {
            height: 198px;
            width: 368px;
            border: 1px solid black;
            margin-right: 10px;
            line-height: 198px;
        }

        .bottom {
            margin-top: 10px;
        }

        .item3,
        .item4,
        .item5,
        .item6 {
            height: 198px;
            width: 178px;
            border: 1px solid black;
            margin-right: 10px;
            line-height: 198px;
        }

        .item7,
        .item8,
        .item9 {
            height: 128px;
            width: 198px;
            border: 1px solid black;
            line-height: 128px;
        }

        .item8 {
            margin: 10px 0;
        }

        .footer {
            height: 60px;
            width: 960px;
            background-color: #ccc;
            margin-top: 10px;
            line-height: 60px;
        }
    </style>
</head>

<body>
    <div class="outer">
        <div class="banner cleanfix">
            <div class="logo leftfix">logo</div>
            <div class="banner1 leftfix">banner1</div>
            <div class="banner2 leftfix">banner2</div>
        </div>
        <div class="menu">菜单</div>
        <div class="content cleanfix">
            <div class="left leftfix">
                <div class="top cleanfix">
                    <div class="item1 leftfix">栏目一</div>
                    <div class="item2 leftfix">栏目二</div>
                </div>
                <div class="bottom cleanfix">
                    <div class="item3 leftfix">栏目三</div>
                    <div class="item4 leftfix">栏目四</div>
                    <div class="item5 leftfix">栏目五</div>
                    <div class="item6 leftfix">栏目六</div>
                </div>
            </div>
            <div class="right rightfix">
                <div class="item7">栏目七</div>
                <div class="item8">栏目八</div>
                <div class="item9">栏目九</div>
            </div>
        </div>
        <div class="footer">页脚</div>
    </div>
</body>

</html>
```

# 定位

## 相对定位

**如何设置相对定位？**

- 给元素设置`position:relative`即可实现相对定位

- 可以使用`left`、`right`、`top`、`bottom`四个属性调整位置

**相对定位的参考点在哪里？**

- 相对自己原来的位置

**相对定位的特点：**

1. 不会脱离文档流，元素位置的变化，只是视觉效果上的变化，不会对其他元素产生任何影响

2. 定位元素的显示层级比普通元素高，无论什么定位，显示层级都是一样的

   默认规则是：

   - 定位的元素会盖在普通元素之上
   - 都发生定位的两个元素，后写的元素会盖在先写的元素之上

3. `left`不能和`right`一起设置，`top`和`bottom`不能一起设置

4. 相对定位的元素，也能继续浮动，但不推荐这样做

5. 相对行为的元素，也能通过 margin 调整位置，但不推荐这样做

## 绝对定位

**如何设置绝对定位？**

- 给元素设置`position: absolute`即可实现绝对定位
- 可以使用`left`、`right`、`top`、`bottom`四个属性调整位置

**绝对定位的参考点在哪里？**

- 参考它的包含块
- 什么是包含块？
  1. 对于没有脱离文档流的元素：包含块就是父元素
  2. 对于脱离文档流的元素：包含块是第一个拥有定位属性的祖先元素（如果所有祖先都没定位，那包含块就是整个页面）

**绝对定位元素的特点：**

1. 脱离文档流，会对后面的兄弟元素、父元素有影响

2. `left`不能和`right`一起设置，`top`和`bottom`不能一起设置

3. 绝对定位、浮动不能同时设置，如果同时设置，浮动失效，以定位为主

4. 绝对定位的元素，也能通过`margin`调整位置，但不推荐这样做

5. 无论是什么元素（行内、行内块、块级）设置为绝对定位之后，都变成了定位元素

   何为定位元素？ —— 默认宽、高都被内容所撑开，且能自由设置宽高

## 固定定位

**如何设置为固定定位？**

- 给元素设置`position: fixed`即可实现固定定位
- 可以使用`left`、`right`、`top`、`bottom`四个属性调整位置

**固定定位的参考点在哪里？**

- 参考它的视口

  什么是视口？—— 对于 PC 浏览器来说，视口就是我们看网页的那扇“窗户”

**固定定位元素的特点：**

1. 脱离文档流，会对后面的兄弟元素、父元素有影响

2. `left`不能和`right`一起设置，`top`和`bottom`不能一起设置

3. 固定定位和浮动不能同时设置，如果同时设置，浮动失效，以固定定位为主

4. 固定定位的元素，也能通过`margin`调整位置，但不推荐这样做

5. 无论是什么元素（行内、行内块、块级）设置为固定定位之后，都变成了定位元素

## 粘性定位

**如何设置为粘性定位？**

- 给元素设置`position:sticky`即可实现粘性定位
- 可以使用`left`、`right`、`top`、`bottom`四个属性调整位置，不过最常用的是`top`值

**粘性定位的参考点在哪里？**

- 离它最近的一个拥有“滚动机制”的祖先元素，即便这个祖先不是最近的真实可滚动祖先

**粘性定位元素的特点：**

- 不会脱离文档流，它是一种专门用于窗口滚动时的新的定位方式

- 最常用的值是`top`值

- 粘性定位和浮动可以同时设置，但不推荐这样做

- 粘性定位的元素，也能通过`margin`调整位置，但不推荐这样做

## 定位层级

1. 定位元素的显示层级比普通元素高，无论什么定位，显示层级都是一样的

2. 如果位置发生重叠，默认情况是：后面的元素，会显示在前面元素之上

3. 可以通过 css 属性`z-index`调整元素的显示层级

4. `z-index`的属性值是数字，没有单位，值越大显示层级越高

5. 只有定位的元素设置`z-index`才有效

6. 如果`z-index`值大的元素，依然没有覆盖掉`z-index`值小的元素，那么请检查其包含块的层级

## 定位的特殊应用

**注意：**

1. 发生固定定位、绝对定位后，元素都变成了定位元素，默认宽高被内容撑开，且依然可以设置宽高

2. 发生相对定位后，元素依然是之前的显示模式

3. 以下所说的特殊应用，只针对 绝对定位 和 固定定位 的元素，不包括相对定位的元素

**让定位元素的宽充满包含块**

1. 块宽想与包含块一致，可以给定位元素同时设置`left`和`right`为`0`

2. 高度想与包含块一致，`top`和`bottom`设置为`0`

**让定位元素在包含块中居中**

1. 方案一：

   ```css
   left:0;
   right:0;
   top:0;
   bottom:0;
   margin:auto;
   ```

2. 方案二：

   ```css
   left: 50%;
   top: 50%;
   margin-left: 负的宽度一半;
   margin-top: 负的高度一半;
   ```

