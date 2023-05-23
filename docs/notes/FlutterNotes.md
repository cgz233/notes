# Flutter Notes

## 组件

### Container容器组件

|名称| 功能|
|--|--|
|alignment| topCenter：顶部居中对齐topLeft：顶部左对齐topRight：顶部右对齐center：水平垂直居中对齐centerLeft：垂直居中水平居左对齐centerRight：垂直居中水平居右对齐bottomCenter底部居中对齐bottomLeft：底部居左对齐bottomRight：底部居右对齐|
|decoration| decoration: BoxDecoration(color: Colors.blue, border: Border.all(color: Colors.red, width: 2.0), borderRadius:BorderRadius.circular((8)),// 圆角 ，boxShadow: [BoxShadow(color: Colors.blue, offset: Offset(2.0, 2.0),blurRadius: 10.0)]) //LinearGradient 背景线性渐变 RadialGradient径向渐变gradient: LinearGradient(colors: [Colors.red, Colors.orange]) |
|margin| margin属性是表示Container与外部其他组件的距离。 EdgeInsets.all(20.0),|
|padding| padding就是Container的内边距，指Container边缘与Child之间的距离 padding:EdgeInsets.all(10.0)|
|transform| 让Container容易进行一些旋转之类的transform: Matrix4.rotationZ(0.2)|
|height| 容器高度|
|width| 容器宽度|
|child| 容器子元素|

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Center(
        child: Container(
            alignment: Alignment.center,
            width: 200,
            height: 200,
            decoration: BoxDecoration(
                // 背景颜色
                color: Colors.yellowAccent,
                // 边框
                border: Border.all(color: Colors.red, width: 5),
                // 阴影
                boxShadow: const [
                  BoxShadow(color: Colors.green, blurRadius: 30)
                ],
                // 圆角
                borderRadius: BorderRadius.circular(20),
                // 背景渐变
                gradient: const LinearGradient(
                    colors: [Colors.yellow, Colors.orange])),
            transform: Matrix4.translationValues(40, 0, 0),
            // 位移
            child: const Text(
              '你好Flutter',
              style: TextStyle(color: Colors.blueAccent, fontSize: 30),
            )));
  }
}

class MyButton extends StatelessWidget {
  const MyButton({super.key});

  @override
  Widget build(BuildContext context) {
    return Container(
        alignment: Alignment.center,
        width: 200,
        height: 40,
        // padding: const EdgeInsets.all(4),
        margin: const EdgeInsets.fromLTRB(0, 40, 0, 0),
        decoration: BoxDecoration(
            color: Colors.blue, borderRadius: BorderRadius.circular(10)),
        child: const Text(
          'Button',
          style: TextStyle(color: Colors.white, fontSize: 17),
        ));
  }
}
```

### Text

|名称| 功能|
|--|--|
|textAlign| 文本对齐方式（center居中，left左对齐，right右对齐，justfy两端对齐）|
|textDirection| 文本方向（ltr从左至右，rtl从右至左）|
|overflow| 文字超出屏幕之后的处理方式（clip裁剪，fade渐隐，ellipsis省略号）|
|textScaleFactor| 字体显示倍率|
|maxLines| 文字显示最大行数|
|style| 字体的样式设置

TextStyle参数

|名称| 功能|
|--|--|
|decoration| 文字装饰线（none没有线，lineThrough删除线，overline上划线，underline下划线）|
|decorationColor| 文字装饰线颜色|
|decorationStyle| 文字装饰线风格（[dashed,dotted]虚线，double两根线，solid一根实线，wavy波浪线）|
|wordSpacing| 单词间隙（如果是负值，会让单词变得更紧凑|
|letterSpacing| 字母间隙（如果是负值，会让字母变得更紧凑）|
|fontStyle| 文字样式（italic斜体，normal正常体）|
|fontSize| 文字大小|
|color| 文字颜色|
|fontWeight| 字体粗细（bold粗体，normal正常体）|

```dart
class MyText extends StatelessWidget {
  const MyText({super.key});

  @override
  Widget build(BuildContext context) {
    return Container(
      width: 200,
      height: 200,
      margin: const EdgeInsets.fromLTRB(0, 50, 0, 0),
      decoration: const BoxDecoration(color: Colors.green),
      child: const Text(
        'HelloHelloHello1111111111',
        textAlign: TextAlign.right,
        maxLines: 1,
        overflow: TextOverflow.ellipsis,
        style: TextStyle(
            fontSize: 20,
            fontWeight: FontWeight.bold,
            letterSpacing: 6,
            decoration: TextDecoration.underline),
      ),
    );
  }
}
```

### Image

- Image.asset 本地图片
- Image.network 网络图片
|名称| 类型| 说明|
|--|--|--|
|alignment| Alignment| 图片的对齐方式|
|color和colorBlendMode| |设置图片的背景颜色，通常和colorBlendMode配合一起使用，这样可以是图片颜色和背景色混合。上面的图片就是进行了颜色的混合，绿色背景和图片红色的混合|
|fit| BoxFit| fit属性用来控制图片的拉伸和挤压，这都是根据父容器来的。<br/>BoxFit.fill:全图显示，图片会被拉伸，并充满父容器<br/>BoxFit.contain:全图显示，显示原比例，可能会有空隙<br/>BoxFit.cover：显示可能拉伸，可能裁切，充满（图片要充满整个容器，还不变形）<br/>BoxFit.fitWidth：宽度充满（横向充满），显示可能拉伸，可能裁切<br/>BoxFit.fitHeight ：高度充满（竖向充满）,显示可能拉伸，可能裁切<br/>BoxFit.scaleDown：效果和contain差不多，但是此属性不允许显示超过源图片大小，可小不可大 |
|repeat| 平铺 |ImageRepeat.repeat : 横向和纵向都进行重复，直到铺满整个画布<br/>ImageRepeat.repeatX: 横向重复，纵向不重复<br/>ImageRepeat.repeatY：纵向重复，横向不重复|
|width| |宽度 一般结合ClipOval才能看到效果|
|height| |高度 一般结合ClipOval才能看到效果|

```dart
// 加载网络图片
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Container(
      width: 150,
      height: 150,
      decoration: const BoxDecoration(color: Colors.green),
      child: Image.network(
        'https://image.cgz233.cn/test.jpg',
        alignment: Alignment.center,
        fit: BoxFit.cover,
      ),
    );
  }
}

// 圆形裁剪图片 第一中方法，设置Container圆角
class CircularImage extends StatelessWidget {
  const CircularImage({super.key});

  @override
  Widget build(BuildContext context) {
    return Container(
      width: 200,
      height: 200,
      decoration: BoxDecoration(
          borderRadius: BorderRadius.circular(100),
          image: const DecorationImage(
              image: NetworkImage('https://image.cgz233.cn/test.jpg'),
              fit: BoxFit.cover)),
    );
  }
}

// 圆形裁剪图片 第二种方法，使用ClipOval
class ClipImage extends StatelessWidget {
  const ClipImage({super.key});

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      child: ClipOval(
        child: Image.network(
          'https://image.cgz233.cn/test.jpg',
          fit: BoxFit.cover,
          width: 150,
          height: 150,
        ),
      ),
    );
  }
}

// 加载本地图片
class LocalImage extends StatelessWidget {
  const LocalImage({super.key});

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      width: 150,
      height: 150,
      child: Image.asset(
        'images/a.jpg',
      ),
    );
  }
}
```

