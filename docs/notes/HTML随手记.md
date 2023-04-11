# HTML随手记

## 标签

- `<p>段落</p>` 文本段落

- `<h1>标题</h1>` 标题，h1-h6

- `<div></div> `页面内容的划分或部分

- `<br/>` 换行

- `<hr color="" width="" size="" align=""/>` 水平分割线

- `<img src="" alt="" title="" width="" heigth="">` 图片

- `<a href="url">链接文本</a>` 超链接

- `<span></span>` 其他内容中的文本部分

- 文本格式标签

  <b>粗体文字</b>
  <strong>这段文字很重要</strong>
  <i>斜体文本</i>
  <em>这段文字被强调</em>
  <u>下划线文本</u>

  <pre>预格式化文本</pre>
  <code>源代码</code>
  <del>删除的文字</del>
  <mark>突出显示的文本 (HTML5)</mark>
  <ins>插入的文本</ins>
  <sup>使文本上标</sup>
  <sub>使文本下标</sub>
  <small>使文本变小</small>

  <pre>预格式化文本</pre>
  <kbd>Ctrl</kbd>

  <blockquote>文本块引用</blockquote>

- 表格

  快速生成表格结构：`table>tr*n>td*n{单元格}`

  <table>
    <thead>
        <tr>
          <td>name</td>
          <td>age</td>
        </tr>
    </thead>
    <tbody>
        <tr>
          <td>Roberta</td>
          <td>39</td>
        </tr>
        <tr>
          <td>Oliver</td>
          <td>25</td>
        </tr>
    </tbody>
  </table>

  单元格合并：

  - 水平合并：colspan
  - 垂直合并：rowspan

  <table border="1" width="500px" height="200px">
      <tr>
          <td colspan="3">单元格1单元格2单元格3</td>
          <td>单元格4</td>
          <td>单元格5</td>
      </tr>
      <tr>
          <td rowspan="2">单元格6-11</td>
          <td>单元格7</td>
          <td rowspan="3">单元格81318</td>
          <td colspan="2" rowspan="2">单元格9101415</td>
      </tr>
      <tr>
          <td>单元格12</td>
      </tr>
      <tr>
          <td>单元格16</td>
          <td>单元格17</td>
          <td>单元格19</td>
          <td>单元格20</td>
      </tr>
  </table>

- 无序列表

  <ul>
    <li>I'm an item</li>
    <li>I'm another item</li>
    <li>I'm another item</li>
  </ul>

- 有序列表

  <ol>
    <li>I'm the first item</li>
    <li>I'm the second item</li>
    <li>I'm the third item</li>
  </ol>

  `<ol>`type属性：1 a A i I

- form表单

  `<form action="url" method="get|post" name="myform"></form>`

  一个完整的表单包含三个基本组成部分：表单标签、表单域、表单按钮

  <form>
      <input type="text">
      <input type="submit">
  </form>

- 块元素和行内元素

  HTML5出现之前，经常把元素按照块级元素和内联元素来区分。在HTML5中，元素不再按照这种⽅式来区分， 而是按照内容模型来区分，分为元数据型(metadata content)、区块型(sectioning content)、标题型(heading content)、文档流型(flow content)、语句型(phrasing content)、内嵌型(embedded content)、交互型 (interactive content)。元素不属于任何⼀个类别，被称为穿透的，元素可能属于不止⼀个类别，称为混合的

  详细参考地址：https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/Content_categories

  |                   块级元素                   |                   内联元素                   |
  | :------------------------------------------: | :------------------------------------------: |
  | 块元素会在页面中独占一行（自上向下垂直排列） | 行内元素不会独占页面中的一行，只占自身的大小 |
  |          可以设置width，height属性           |      行内元素设置width，height属性无效       |
  |  ⼀般块级元素可以包含行内元素和其他块级元素  |    ⼀般内联元素包含内联元素不包含块级元素    |

  常见块级元素：div、form、h1~h6、hr、p、table、ul等
  
  常见内联元素(行内元素)：a、b、em、i、span、strong等 
  
  行内块级元素（特点：不换行、能够识别宽高）：button、img、input等
  
- H5新增标签

  `<div>`容器元素，也是页面中见到的最多的元素

  div实现

  ![image-20211126150749756](E:\尚学堂前端\1.第一章：HTML5\md文档\imgs\image-20211126150749756.png)

  

  H5新标签实现

  ![image-20211126150757403](E:\尚学堂前端\1.第一章：HTML5\md文档\imgs\image-20211126150757403.png)

  **H5新标签**

  1. `<header></header>`  头部
  2. `<nav></nav>`  导航
  3. `<section></section>`定义文档中的节,比如章节、页眉、页脚
  4. `<aside></aside>`  侧边栏
  5. `<footer></footer>` 脚部
  6. `<article></article>`  代表一个独立的、完整的相关内容块,例如一篇完整的论坛帖子，一篇博客文章，一个用户评论等



