# CSS随手记

## 语法

```html
<style>
    h1{
        color: blue;
        font-size: 12px;
    }
</style>
```

## CSS的引入方式

- **内联样式**

  在相关的标签内使用样式（style）属性，缺乏整体性和规划性，不利于维护，维护成本高

  `<p style="background: orange; font-size: 24px;">CSS<p>`

- **内部样式**

  使用 `<style>` 标签在文档头部定义内部样式表，单个页面内的CSS代码具有统一性和规划性，便于维护，但是在多个页面之间容易混乱

  ```html
  <head>
      <style>
         h1 {
             background: red;
         }
      </style>
  </head>
  ```

- **外部样式**

  每个页面使用 `<link>` 标签链接到样式表， `<link>` 标签在（文档的）头部

  ```html
  <link rel="stylesheet" type="text/css" href="xxx.css">
  ```

## 选择器

- **全局选择器**

  可以与任何元素匹配，优先级最低，一般做样式初始化

  ```css
  *{
       margin: 0;
       padding: 0;
   }
  ```

- **元素选择器**

  HTML文档中的元素，`p、b、div、a、img、body`等

  ```css
  p{
      font-size:14px;
  }
  ```

- **类选择器**

  ```html
  <h2 class="oneclass">你好</h2>
  /*定义类选择器*/
  .oneclass{
  	width:800px;
  }
  ```

  特点

  1. 类选择器可以被多种标签使用
  2. 类名不能以数字开头
  3. 同一个标签可以使用多个类选择器。用空格隔开

- **ID选择器**

  ```html
  <h2 id="mytitle">你好</h2>
  #mytitle{
      border:3px dashed green;
  }
  ```

- **合并选择器**

  `选择器1,选择器2,...{ }`

  ```css
  .header, .footer{
      height:300px;
  }
  ```

- **选择器的优先级**

  CSS中,权重用数字衡量

  元素选择器的权重为: 1

  class选择器的权重为: 10

  id选择器的权重为: 100

  内联样式的权重为: 1000

  优先级从高到低: 行内样式 > ID选择器 > 类选择器 > 元素选择器


## 字体属性

- `color:red;` `color:#ff0000;` `color:rgb(255,0,0);` `color:rgba(255,0,0,.5);` 文本颜色

- `font-size:40px;` 文本大小

- font-weight 设置文本的粗细

  | 值      | 描述                                       |
  | ------- | ------------------------------------------ |
  | bold    | 粗体                                       |
  | bolder  | 更粗的字体                                 |
  | lighter | 更细的字体                                 |
  | 100~900 | 定义由细到粗  400等同默认，而700等同于bold |

- font-style 指定文本的字体样式

  | 值     | 描述       |
  | ------ | ---------- |
  | normal | 默认值     |
  | italic | 定义斜体字 |

- `font-family:"Microsoft YaHei","Simsun","SimHei";` 设置指定元素的字体

## 背景属性

CSS背景属性主要有以下几个

| 属性                | 描述                 |
| ------------------- | -------------------- |
| background-color    | 设置背景颜色         |
| background-image    | 设置背景图片         |
| background-position | 设置背景图片显示位置 |
| background-repeat   | 设置背景图片如何填充 |
| background-size     | 设置背景图片大小属性 |

### background-color属性

该属性设置背景颜色

```css
<div class="box"></div>
.box{
    width: 300px;
    height: 300px;
    background-color: palevioletred;
}
```

### background-image属性

设置元素的背景图像

元素的背景是元素的总大小，包括填充和边界（不包括外边距）。默认情况下background-image属性放置在元素的左上角，如果图像不够大的话会在垂直和水平方向平铺图像，如果图像大小超过元素大小从图像的左上角显示元素大小的那部分

```css
<div class="box"></div>
.box{
    width: 600px;
    height: 600px;
    background-image: url("images/img1.jpg");
}
```

### background-repeat属性

该属性设置如何平铺背景图像

| 值        | 说明             |
| --------- | ---------------- |
| repeat    | 默认值           |
| repeat-x  | 只向水平方向平铺 |
| repeat-y  | 只向垂直方向平铺 |
| no-repeat | 不平铺           |

```css
.box{
    width: 600px;
    height: 600px;
    background-color: #fcc;
    background-image: url("images/img1.jpg");
    background-repeat: no-repeat;
}
```

### background-size属性

该属性设置背景图像的大小

| 值         | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| length     | 设置背景图片的宽度和高度，第一个值宽度，第二个值高度，如果只是设置一个，第二个值auto |
| percentage | 计算相对位置区域的百分比，第一个值宽度，第二个值高度，如果只是设置一个，第二个值auto |
| cover      | 保持图片纵横比并将图片缩放成完全覆盖背景区域的最小大小       |
| contain    | 保持图片纵横比并将图像缩放成适合背景定位区域的最大大小       |

```css
.box{
    width: 600px;
    height: 600px;
    background-image: url("images/img1.jpg");
    background-repeat: no-repeat;
    background-size: 100% 100%;
}
```

### background-position属性

该属性设置背景图像的起始位置，其默认值是：0% 0%

| 值            | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| left  top     | 左上角                                                       |
| left center   | 左 中                                                        |
| left bottom   | 左 下                                                        |
| right top     | 右上角                                                       |
| right center  | 右 中                                                        |
| right bottom  | 右 下                                                        |
| center top    | 中 上                                                        |
| center center | 中 中                                                        |
| center bottom | 中 下                                                        |
| x%  y%        | 第一个值是水平位置，第二个值是垂直位置，左上角是0%  0%，右下角是100%  100% 。如果只指定了一个值，其他值默认是50%。默认是0%  0% |
| xpos ypos     | 单位是像素                                                   |

```css
.box{
    width: 600px;
    height: 600px;
    background-color: #fcc;
    background-image: url("images/img1.jpg");
    background-repeat: no-repeat;
    background-position: center;
}
```

## 文本属性

### text-align

指定元素文本的水平对齐方式

| 值     | 描述                 |
| ------ | -------------------- |
| left   | 文本居左排列，默认值 |
| right  | 把文本排列到右边     |
| center | 把文本排列到中间     |

```css
h1 {text-align:center}
h2 {text-align:left}
h3 {text-align:right}
```

### text-decoration

text-decoration 属性规定添加到文本的修饰，下划线、上划线、删除线等

| 值           | 描述       |
| ------------ | ---------- |
| underline    | 定义下划线 |
| overline     | 定义上划线 |
| line-through | 定义删除线 |

```css
h1 {text-decoration:overline} 
h2 {text-decoration:line-through} 
h3 {text-decoration:underline}
```

### text-transform

text-transform 属性控制文本的大小写

| 值         | 描述                 |
| ---------- | -------------------- |
| captialize | 定义每个单词开头大写 |
| uppercase  | 定义全部大写字母     |
| lowercase  | 定义全部小写字母     |

```css
h1 {text-transform:uppercase;}
h2 {text-transform:capitalize;}
p {text-transform:lowercase;}
```

### text-indent

text-indent 属性规定文本块中首行文本的缩进

```css
p{
	text-indent:50px;
}
```

> **温馨提示**
>
> 负值是允许的。如果值是负数，将第一行左缩进