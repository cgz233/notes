# Flutter Notes

## Widget

### Container

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

TextStyle参数：

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

  导入本地图片需要现在pubspec.yaml文件中配置

  ```yaml
      assets:
      - images/2.0x/a.jpg
      - images/3.0x/a.jpg
      - images/a.jpg
  ```

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

// 圆形裁剪图片 第一种方法，设置Container圆角
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

CircleAvatar实现圆形图片：

```dart
const CircleAvatar(
    radius: 50, // 圆的半径大小
    backgroundImage:
    NetworkImage("https://image.cgz233.cn/test.jpg")
)
```

ClipRRect裁切圆角：

```dart
ClipRRect(
  borderRadius:
      const BorderRadius.vertical(top: Radius.circular(10)), // 裁切顶部两角
  child: Image.network(
    'https://image.cgz233.cn/test.jpg',
    height: 135,
    fit: BoxFit.cover
  )
)
```

### Icon

自定义图标

首先在pubspec.yaml文件中配置字体文件位置

```yaml
  fonts:
   - family: MyIcon
     fonts:
       - asset: fonts/iconfont.ttf
```

定义一个图标类，IconData第一个参数传入的是字体的unicode十六进制编码

```dart
import 'package:flutter/material.dart';

class MyIcon {
  static const IconData java =
      IconData(0xf1d7, fontFamily: 'MyIcon', matchTextDirection: true);

  static const IconData kotlin =
      IconData(0xebed, fontFamily: 'MyIcon', matchTextDirection: true);

  static const IconData flutter =
      IconData(0xe7e0, fontFamily: 'MyIcon', matchTextDirection: true);
}
```

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Column(
      children: const [
        Icon(
          Icons.search, // 官方图标
          size: 80,
          color: Colors.blue,
        ),
        Icon(
          MyIcon.java, // 自定义图标
          size: 80,
          color: Colors.blue,
        ),
        Icon(
          MyIcon.kotlin, // 自定义图标
          size: 80,
          color: Colors.blue,
        ),
        Icon(
          MyIcon.flutter, // 自定义图标
          size: 80,
          color: Colors.blue,
        )
      ],
    );
  }
}
```

### ListView

|名称 |类型 |说明|
|--|--|--|
|scrollDirection |Axis |Axis.horizontal水平列表<br/>Axis.vertical垂直列表|
|padding| EdgeInsetsGeometry |内边距|
|resolve |bool |组件反向排序|
|children |List| 列表元素|

```dart
// 创建ListView 使用ListView.builder
class NewsList2 extends StatelessWidget {
  const NewsList2({super.key});

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
        itemCount: newsListData.length,
        itemBuilder: (context, index) {
          return ListTile(
              leading: Image.network(
                'http://192.168.1.211:10001${newsListData[index]['cover']}',
                width: 100,
                height: 100,
                fit: BoxFit.cover,
              ),
              title: Text(
                newsListData[index]['title'],
                maxLines: 1,
                overflow: TextOverflow.ellipsis,
              ),
              subtitle: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(
                    newsListData[index]['content'],
                    maxLines: 1,
                    overflow: TextOverflow.ellipsis,
                  ),
                  Text(
                    "发布时间：${newsListData[index]['publishDate']}",
                    maxLines: 1,
                    overflow: TextOverflow.ellipsis,
                  ),
                  Text(
                    "评论数量：${newsListData[index]['commentNum']}",
                    maxLines: 1,
                    overflow: TextOverflow.ellipsis,
                  ),
                ],
              ));
        });
  }
}

// 创建ListView 遍历数组
class NewsList extends StatelessWidget {
  const NewsList({super.key});

  List<Widget> _initData() {
    List<Widget> list = [];

    for (var news in newsListData) {
      list.add(
        ListTile(
          visualDensity: const VisualDensity(vertical: 4),
          leading: Image.network(
            'http://192.168.1.211:10001${news['cover']}',
            fit: BoxFit.cover,
            width: 100,
            height: 100,
          ),
          title:
              Text(news['title'], maxLines: 1, overflow: TextOverflow.ellipsis),
          subtitle: Text(news['content'],
              maxLines: 2, overflow: TextOverflow.ellipsis),
          trailing: const Icon(
            Icons.chevron_right,
            size: 30,
          ),
        ),
      );
    }

    return list;
  }

  @override
  Widget build(BuildContext context) {
    return ListView(
      children: _initData(),
    );
  }
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  List<Widget> _initListData() {
    List<Widget> list = [];
    for (var i = 0; i < 20; i++) {
      list.add(ListTile(
        leading: Image.network('https://image.cgz233.cn/test.jpg',
            width: 60, fit: BoxFit.cover),
        title: const Text('宠物猫即将迎来32岁 主人欲申请吉尼斯世界纪录',
            maxLines: 1, overflow: TextOverflow.ellipsis),
        subtitle: const Text(
            '据英国《都市报》4月6日报道，近日，来自英国的Lila Brissett正在为自己的宠物猫Rosie筹备32岁的生日庆典。Rosie的年龄相当于人类144岁，Lila觉得它可能是世界上最长寿的猫，打算为它申请吉尼斯世界纪录。 ',
            maxLines: 2,
            overflow: TextOverflow.ellipsis),
      ));
    }

    return list;
  }

  @override
  Widget build(BuildContext context) {
    return ListView(
        scrollDirection: Axis.vertical,
        padding: const EdgeInsets.all(10),
        children: _initListData());
  }
}
```

### GridView

|名称 |类型 |说明|
|--|--|--|
|scrollDirection| Axis |滚动方法|
|padding |EdgeInsetsGeometry |内边距|
|resolve| bool |组件反向排序|
|crossAxisSpacing|double| 水平子Widget之间间距                 |
|mainAxisSpacing| double |垂直子Widget之间间距|
|crossAxisCount |int 用在GridView.count| 一行的Widget数量 |
|maxCrossAxisExtent |double 用在GridView.extent| 横轴子元素的最大长度 |
|childAspectRatio |double| 子Widget宽高比例|
|childrenIstanbul| List |表格元素列表|
|gridDelegate |SliverGridDelegateWithFixedCrossAxisCount<br/>SliverGridDelegateWithMaxCrossAxisExtent |控制布局主要用在GridView.builder里面|

通过GridView.count 实现网格布局

```dart
class NewsGrid extends StatelessWidget {
  const NewsGrid({super.key});

  List<Widget> _initData() {
    var list = newsListData.map((e) {
      return Container(
        decoration: BoxDecoration(
            border: Border.all(color: Colors.grey),
            borderRadius: BorderRadius.circular(10)),
        child: Column(
          children: [
            // 裁切图片上方圆角，避免溢出
            ClipRRect(
              borderRadius:
                  const BorderRadius.vertical(top: Radius.circular(10)),
              child: Image.network(
                'http://192.168.1.211:10001${e['cover']}',
                height: 135,
                fit: BoxFit.cover,
              ),
            ),
            Text(
              e['title'],
              maxLines: 2,
              overflow: TextOverflow.ellipsis,
            )
          ],
        ),
      );
    });
    return list.toList();
  }

  @override
  Widget build(BuildContext context) {
    return GridView.count(
      padding: const EdgeInsets.all(20),
      // 垂直子Widget之间间距
      mainAxisSpacing: 10,
      // 水平子Widget之间间距
      crossAxisSpacing: 10,
      // 一行的Widget数量
      crossAxisCount: 2,
      // 子Widget宽高比例
      childAspectRatio: 0.96,
      children: _initData(),
    );
  }
}
```

通过GridView.extent 实现网格布局

```dart
class MyApp2 extends StatelessWidget {
  const MyApp2({super.key});

  @override
  Widget build(BuildContext context) {
    return GridView.extent(
      //横轴子元素的最大长度
      maxCrossAxisExtent: 50,
      children: const [
        Icon(Icons.wallpaper),
        Icon(Icons.dangerous),
        Icon(Icons.safety_check),
        Icon(Icons.label),
        Icon(Icons.vaccines),
        Icon(Icons.qr_code),
        Icon(Icons.e_mobiledata),
        Icon(Icons.r_mobiledata),
        Icon(Icons.abc),
        Icon(Icons.one_x_mobiledata),
      ],
    );
  }
}
```

GridView.builder实现动态网格布局

```dart
class NewsGrid extends StatelessWidget {
  const NewsGrid({super.key});

  Widget _initData(context, index) {
    return Container(
      decoration: BoxDecoration(
          border: Border.all(color: Colors.grey),
          borderRadius: BorderRadius.circular(10)),
      child: Column(
        children: [
          // 裁切图片上方圆角，避免溢出
          ClipRRect(
            borderRadius: const BorderRadius.vertical(top: Radius.circular(10)),
            child: Image.network(
              'http://192.168.1.211:10001${newsListData[index]['cover']}',
              height: 135,
              fit: BoxFit.cover,
            ),
          ),
          Text(
            newsListData[index]['title'],
            maxLines: 2,
            overflow: TextOverflow.ellipsis,
          )
        ],
      ),
    );
  }

  // 使用SliverGridDelegateWithFixedCrossAxisCount
  @override
  Widget build(BuildContext context) {
    return GridView.builder(
        itemCount: newsListData.length,
        padding: const EdgeInsets.all(20),
        gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
          // 垂直子Widget之间间距
          mainAxisSpacing: 10,
          // 水平子Widget之间间距
          crossAxisSpacing: 10,
          // 一行的Widget数量
          crossAxisCount: 2,
          // 子Widget宽高比例
          childAspectRatio: 0.97,
        ),
        itemBuilder: _initData);
  }

// 使用SliverGridDelegateWithMaxCrossAxisExtent
// @override
// Widget build(BuildContext context) {
//   return GridView.builder(
//       itemCount: newsListData.length,
//       padding: const EdgeInsets.all(20),
//       gridDelegate: const SliverGridDelegateWithMaxCrossAxisExtent(
//         // 垂直子Widget之间间距
//         mainAxisSpacing: 10,
//         // 水平子Widget之间间距
//         crossAxisSpacing: 10,
//         maxCrossAxisExtent: 200,
//         // 子Widget宽高比例
//         childAspectRatio: 0.97,
//       ),
//       itemBuilder: _initData);
// }
}
```

### Padding

|属性 |说明|
|--|--|
|padding |padding值, EdgeInsetss设置填充的值|
|child |子组件|

### Row&Column

|属性| 说明|
|--|--|
|mainAxisAlignment |主轴的排序方式|
|crossAxisAlignment| 次轴的排序方式|
|children |组件子元素|

double.infifinity和double.maxFinite

- double.infifinity 和double.maxFinite可以让当前元素的width或者height达到父元素的尺寸

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      crossAxisAlignment: CrossAxisAlignment.center,
      children: [
        Container(
          width: 100,
          height: 100,
          decoration: const BoxDecoration(color: Colors.green),
        ),
        Container(
          width: 100,
          height: 100,
          decoration: const BoxDecoration(color: Colors.blue),
        ),
        Container(
          width: 100,
          height: 100,
          decoration: const BoxDecoration(color: Colors.red),
        )
      ]
    );
  }
}
```

### Flex&Expanded

`Flex`组件可以沿着水平或垂直方向排列子组件，如果知道主轴方向，使用`Row`或`Column`会方便一些，因为`Row`和`Column`都继承自`Flex`，参数基本相同，所以能使用Flex的地方基本上都可以使用`Row`或`Column`，`Flex`本身功能是很强大的，它也可以和`Expanded`组件配合实现弹性布局

```dart
  @override
  Widget build(BuildContext context) {
    return Flex(
      // 设置Flex的排列方向，vertical和Column类似，horizontal和Row类似
      direction: Axis.vertical,
      mainAxisAlignment: MainAxisAlignment.start,
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Container(
          width: double.infinity,
          height: 200,
          decoration: const BoxDecoration(color: Colors.green),
        ),
        const Padding(padding: EdgeInsets.all(5)),
        SizedBox(
          height: 200,
          child: Flex(
            direction: Axis.horizontal,
            children: [
              // Expanded搭配Flex使用，flex属性可以设置在Flex中占比，类似于Android中weight属性
              Expanded(
                  flex: 2,
                  child: Container(
                    decoration: const BoxDecoration(color: Colors.blue),
                  )),
              const Padding(padding: EdgeInsets.all(5)),
              Expanded(
                  flex: 1,
                  child: Column(
                    children: [
                      Expanded(
                          flex: 1,
                          child: Container(
                            decoration:
                                const BoxDecoration(color: Colors.orange),
                          )),
                      const Padding(padding: EdgeInsets.all(5)),
                      Expanded(
                          flex: 1,
                          child: Container(
                            decoration: const BoxDecoration(color: Colors.red),
                          )),
                    ],
                  ))
            ],
          ),
        )
      ],
    );
  }
```

### Stack&Align&Positioned

#### Stack

Stack表示堆的意思（类似Android FrameLayout），可以用Stack或者Stack结合Align或者Stack结合Positiond来实现页面的定位布局

|属性| 说明|
|--|--|
|alignment| 配置所有子元素的显示位置|
|children| 子组件|

#### Align

Align组件可以调整子组件的位置，Stack组件中结合Align组件也可以控制每个子元素的显示位置

|属性| 说明|
|--|--|
|alignment |配置所有子元素的显示位置|
|child| 子组件|

#### Positioned

Stack组件中结合Positioned组件也可以控制每个子元素的显示位置

|属性 |说明|
|--|--|
|top |子元素距离顶部的距离|
|bottom| 子元素距离底部的距离|
|left| 子元素距离左侧距离|
|right| 子元素距离右侧距离|
|child| 子组件|
|width |组件的高度（注意：宽度和高度必须是固定值，没法使用double.infinity）|
|height |子组件的高度|

获取屏幕宽度和高度

```dart
final size = MediaQuery.of(context).size;
final width = size.width;
final height = size.height;
```

综合案例

```dart
  @override
  Widget build(BuildContext context) {
    final size = MediaQuery.of(context).size;
    return Stack(
      alignment: Alignment.topLeft,
      children: [
        ListView(
          padding: const EdgeInsets.only(top: 50),
          children: const [
            ListTile(
              title: Text('Test1'),
            ),
            ListTile(
              title: Text('Test2'),
            ),
          ],
        ),
        Positioned(
            top: 0,
            left: 0,
            width: size.width,
            height: 50,
            child: Container(
              alignment: Alignment.center,
              decoration: const BoxDecoration(color: Colors.green),
              child: const Text('Hello'),
            ))
      ],
    );
  }
```

### AspectRatio

- AspectRatio的作用是根据设置调整子元素child的宽高比
- AspectRatio首先会在布局限制条件允许的范围内尽可能的扩展，widget的高度是由宽度和比率决定的，类似于BoxFit中的contain，按照固定比率去尽量占满区域
- 如果在满足所有限制条件过后无法找到一个可行的尺寸，AspectRatio最终将会去优先适应布局限制条件，而忽略所设置的比率

|属性 |说明|
|--|--|
|aspectRatio| 宽高比，最终可能不会根据这个值去布局，具体则要看综合因素，外层是否允许按照这种比率进行布局，这只是一个参考值|
|child| 子组件|

### Card

|属性 |说明|
|--|--|
|margin |外边距|
|child| 子组件|
|elevation |阴影值的深度|
|color |背景颜色|
|shadowColor |阴影颜色|
|margin |外边距|
|clipBehavior | clipBehavior 内容溢出的剪切方式<br/>Clip.none：不剪切<br/>Clip.hardEdge：裁剪但不应用抗锯齿<br/>Clip.antiAlias：裁剪而且抗锯齿<br/>Clip.antiAliasWithSaveLayer：带有抗锯齿的剪辑，并在剪辑之后立即保存saveLayer |
|Shape |Card的阴影效果，默认的阴影效果为圆角的长方形边<br/>`shape: const RoundedRectangleBorder(borderRadius:BorderRadius.all(Radius.circular(10)))`|



```dart
  @override
  Widget build(BuildContext context) {
    return ListView(
      children: [
        Card(
          margin: const EdgeInsets.all(10),
          elevation: 10,
          shape:
              RoundedRectangleBorder(borderRadius: BorderRadius.circular(15)),
          clipBehavior: Clip.antiAlias,
          child: Column(
            children: [
              AspectRatio(
                  aspectRatio: 16 / 9,
                  child: Image.network(
                    'https://image.cgz233.cn/bac.jpg',
                    fit: BoxFit.cover,
                  )),
              ListTile(
                  leading: const CircleAvatar(
                      radius: 28,
                      backgroundImage:
                          NetworkImage('https://image.cgz233.cn/xin.jpg')),
                  title: const Text('XiaoChen'),
                  subtitle: Row(
                    children: const [
                      Icon(
                        Icons.email,
                        size: 20,
                      ),
                      Padding(padding: EdgeInsets.all(3)),
                      Text('admin@cgz233.cn'),
                    ],
                  ))
            ],
          ),
        )
      ],
    );
  }
```









