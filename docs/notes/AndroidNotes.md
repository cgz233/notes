# Android开发笔记

> by.Xiao_Chen

相关教程：

- [Google官方开发者指南](https://developer.android.google.cn/guide)
- [Android Studio 键盘快捷键 & Quick Reference](http://bbs.laoleng.vip/reference/docs/android-studio.html)
- [Android基础入门教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/android-tutorial-intro.html)
- [XML 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/xml/xml-tutorial.html)



# 开发基础

**App开发语言**

- App 开发主要有两大技术路线，分别是原生开发和混合开发

- Android 的官方编程语言包括 Java 和 Kotlin

**App工程目录结构** 

- App工程分为两个层次，第一个层次是项目，另一个层次是模块

- 模块依附于项目，每个项目至少有一个模块，也能拥有多个模块

- 一般所言的“编译运行App”，指的是运行某个模块，而非运行某个项目，因为模块才对应实际的App

**App项目的目录说明** 

- App项目下面有两个分类：app（代表app模块）、Gradle Scripts

- App下面有3个子目录，Gradle Scripts下面主要是工程的编译配置文件

**Gradle** 

- Gradle 是一个项目自动化构建工具，帮我们做了依赖、打包、部署、发布、各种渠道的差异管理等工作

**编译配置文件** **build.gradle** 

- 项目级别的 build.gradle 指定了当前项目的总体编译规则

- 模块级别的 build.gradle 对应于具体模块，每个模块都有自己的 build.gradle，它指定了当前模块的详细编译规则

**清单文件** 

- 每个应用的根目录中都必须包含一个 AndroidManifest.xml，并且文件名必须一模一样

  这个文件中包含了APP的配置信息，系统需要根据里面的内容运行APP的代码，显示界面

**什么是** **Activity** 

- Activity 是一个应用程序组件，提供一个屏幕，用户可以用来交互为了完成某项任务

**界面显示与逻辑处理** 

- 利用 XML 标记描绘应用界面，使用Java代码书写程序逻辑

**利用** **XML** **标记描绘应用界面** 

- 把 App 的界面设计与代码逻辑分开的好处： 
  - 使用 XML 文件描述 APP 界面，可以很方便地在 Android Studio 上预览界面效果
  - 一个界面布局可以被多处代码复用，反过来，一个 Java 代码也可能适配多个界面布局

**创建新的** **App** **页面** 

- 完整的页面创建过程包括三个步骤：
  - 在 layout 目录下创建 XML 文件
  - 创建与 XML 文件对应的 Java 代码
  - 在 AndroidManifest.xml 中注册页面配置

**快速生成页面源码** 

- 依次选择右键菜单New → Activity → Empty Activity，弹出图示的页面创建窗口

- 输入各项信息后，单击窗口右下角的 Finish 按钮，即可完成新页面的创建动作



# 简单控件

## 文本显示

### 设置文本内容

- 在 XML 文件中通过属性 android:text 设置文本 

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical">
  
      <TextView
          android:id="@+id/tv_hello"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:text="小陈安卓开发"/>
  
  </LinearLayout>
  ```

- 在 Java 代码中调用文本视图对象的 setText 方法设置文本

  ```java
  public class TextActivity extends AppCompatActivity {
      @Override
      protected void onCreate(@Nullable Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_text);
          TextView tvHello = findViewById(R.id.tv_hello);
          tvHello.setText("XiaoChenAndroid");
      }
  }
  ```

**引用字符串资源**

- 在XML文件中引用（@string/***） 

  ```xml
  android:text="@string/hello"
  ```

- 在Java代码中引用（R.string.***）

  ```java
  tvHello.setText(R.string.hello);
  ```

### 设置文本的大小

- 在 Java 代码中调用 setTextSize 方法，即可指定文本大小

  ```java
  textView.setTextSize(30);
  ```

- 在 XML 文件中则通过属性 android:textSize 指定文本大小，此时需要指定字号单位

  ```xml
  android:textSize="30px"
  ```

  - px：它是手机屏幕的最小显示单位，与设备的显示屏有关
  - dp：它是与设备无关的显示单位，只与屏幕的尺寸有关
  - sp：它专门用来设置字体大小，在系统设置中可以调整字体大小

### 设置文本的颜色

- 在 Java 代码中调用 setTextColor 方法即可设置文本颜色，具体色值可从 Color 类取

  ```java
  textView.setTextColor(Color.GREEN);
  ```

| Color  | 颜色 | Color       | 颜色 |
| ------ | ---- | ----------- | ---- |
| BLACK  | 黑色 | GREEN       | 绿色 |
| DKGRAY | 深灰 | BLUE        | 蓝色 |
| GRAY   | 灰色 | YELLOW      | 黄色 |
| LTGRAY | 浅灰 | CYAN        | 青色 |
| WHITE  | 白色 | MAGENTA     | 玫红 |
| RED    | 红色 | TRANSPARENT | 透明 |

- 在XML文件中则通过属性android:textColor指定文本颜色，色值由透明度alpha和RGB 三原色（红色red、绿色green、蓝色blue）联合定义

  ```xml
  android:textColor="#00ff00"
  ```

**设置背景颜色**

- 在java中

  ```java
  TextView tv_code_background = findViewById(R.id.tv_code_background);
  //tv_code_background.setBackgroundColor(Color.GREEN);
  tv_code_background.setBackgroundResource(R.color.green);
  ```

- 在xml中

  ```xml
  android:background="@color/green"
  ```

**RGB颜色定义**

- 色值有八位十六进制数与六位十六进制数两种表达方式，例如八位编码FFEEDDCC中，FF表示透明度，EE表示红色的浓度，DD表示绿色的浓度，CC表示蓝色的浓度。（java六位默认透明，xml默认不透明）

  ```
  TextView tv_code_eight = findViewById(R.id.tv_code_eight);
  tv_code_eight.setTextColor(0xff00ff00);
  TextView tv_code_six = findViewById(R.id.tv_code_six);
  tv_code_six.setTextColor(0x00ff00);
  ```

- 透明度为FF表示完全不透明，为00表示完全透明。RGB三色的数值越大，表示颜色越浓，也就越亮；数值越小，表示颜色越淡，也就越暗

**使用色值定义文字颜色** 

- 在Java代码中设置色值需要添加0x前缀表示十六进制数

- 在XML文件中设置色值需要添加“#”前缀

**引用颜色资源**（与字符串类似）

- 在XML文件中引用（@color/***）

- 在Java代码中引用（R.color.***）



## 视图基础

### 设置视图的宽高

- 视图宽度通过属性android:layout_width表达，视图高度通过属性android:layout_height表达，宽高的取值主要有下列三种： 
  - match_parent：表示与上级视图保持一致
  - wrap_content：表示与内容自适应
  - 以dp为单位的具体尺寸

```xml
	<TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:background="#00ffff"
        android:text="视图宽高采用wrap_content定义"
        android:textColor="#000000"
        android:textSize="17sp" />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:background="#00ffff"
        android:text="视图宽采用match_parent定义"
        android:textColor="#000000"
        android:textSize="17sp" />

    <TextView
        android:layout_width="300dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="5dp"
        android:background="#00ffff"
        android:text="视图宽度采用固定大小"
        android:textColor="#000000"
        android:textSize="17sp" />
```

**在代码中设置视图宽高** 

- 首先确保XML中的宽高属性值为wrap_content，接着打开该页面对应的Java代码，依序执行以下三个步骤： 
  - 调用控件对象的getLayoutParams方法，获取该控件的布局参数
  - 布局参数的width属性表示宽度，height属性表示高度，修改这两个属性值
  - 调用控件对象的setLayoutParams方法，填入修改后的布局参数使之生效

```java
public class VIewBorderActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_view_border);
        TextView tv_code = findViewById(R.id.tv_code);
        // 获取tv_code的布局参数（含宽度和高度）
        ViewGroup.LayoutParams params = tv_code.getLayoutParams();
        // 修改布局参数中的宽度数值，注意默认px单位，需要把dp数值转为px数值，可以单独写一个Utils工具类
        params.width = Utils.dip2px(this,300);
        // 设置tv_code的布局参数
        tv_code.setLayoutParams(params);
    }
}

public class Utils { // 工具类
    // 根据手机的分辨率从 dp 的单位转化成 px(像素)
    public static int dip2px(Context context,float dpValue){
        // 获取当前手机的像素密度（1个dp对应几个px）
        float scale = context.getResources().getDisplayMetrics().density;
        // 四舍五入取整
        return (int)(dpValue * scale + 0.5f);
    }
}
```

### 设置视图的间距

- 设置视图的间距有两种方式： 
  - 采用layout_margin属性，它指定了当前视图与周围平级视图之间的距离。包括layout_margin、layout_marginLeft、layout_marginTop、layout_marginRight、layout_marginBottom
  - 采用padding属性，它指定了当前视图与内部下级视图之间的距离。包括padding、paddingLeft、paddingTop、paddingRight、paddingBottom

```xml
<!-- 最外层的布局背景为蓝色 -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="300dp"
    android:background="#00AAFF"
    android:orientation="vertical">

    <!-- 中间层的布局背景为黄色 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_margin="20dp"
        android:background="#FFFF99"
        android:padding="60dp">

        <!-- 最内层的视图背景为红色 -->
        <View
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:background="#FF0000" />
        
    </LinearLayout>
</LinearLayout>
```

### 设置视图的对齐方式

- 设置视图的对齐方式有两种途径： 
  - 采用layout_gravity属性，它指定了当前视图相对于上级视图的对齐方式
  - 采用gravity属性，它指定了下级视图相对于当前视图的对齐方式

- layout_gravity与gravity的取值包括：left、top、right、bottom，还可以用竖线连接各取值，例如“left|top”表示即靠左又靠上，也就是朝左上角对齐

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="300dp"
    android:background="#ffff99"
    android:orientation="horizontal">

    <!-- 第一个子布局背景为红色，它在上级视图中朝下对齐，它的下级视图则靠左对齐 -->
    <LinearLayout
        android:layout_width="0dp"
        android:layout_height="200dp"
        android:layout_gravity="bottom"
        android:layout_margin="10dp"
        android:layout_weight="1"
        android:background="#ff0000"
        android:padding="10dp"
        android:gravity="left">
        <!-- 内部视图的宽度和高度都是100dp，且背景色为青色 -->
        <View
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:background="#00ffff"/>
    </LinearLayout>

    <!-- 第二个子布局背景为红色，它在上级视图中朝上对齐，它的下级视图则靠右对齐 -->
    <LinearLayout
        android:layout_width="0dp"
        android:layout_height="200dp"
        android:layout_gravity="top"
        android:layout_margin="10dp"
        android:layout_weight="1"
        android:padding="10dp"
        android:background="#ff0000"
        android:gravity="right">
        
        <!-- 内部视图的宽度和高度都是100dp，且背景色为青色 -->
        <View
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:background="#00ffff"/>

    </LinearLayout>
</LinearLayout>
```



## 常用布局

### 线性布局LinearLayout

- 线性布局内部的各视图有两种排列方式： 
  - orientation属性值为horizontal时，内部视图在水平方向从左往右排列
  - orientation属性值为vertical时，内部视图在垂直方向从上往下排列

- 如果不指定orientation属性，则LinearLayout默认水平方向排列

**线性布局的权重** 

- 线性布局的权重概念，指的是线性布局的下级视图各自拥有多大比例的宽高

- 权重属性名叫layout_weight，但该属性不在LinearLayout节点设置，而在线性布局的直接下级视图设置，表示该下级视图占据的宽高比例。 
  - layout_width填0dp时，layout_weight表示水平方向的宽度比例
  - layout_height填0dp时，layout_weight表示垂直方向的高度比例

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

<!--    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="横排第一个"
            android:textSize="17sp"
            android:textColor="#000000"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="横排第二个"
            android:textSize="17sp"
            android:textColor="#000000"/>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="竖排第一个"
            android:textSize="17sp"
            android:textColor="#000000"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="竖排第二个"
            android:textSize="17sp"
            android:textColor="#000000"/>
    </LinearLayout>-->

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="横排第一个"
            android:textSize="17sp"
            android:textColor="#000000"/>

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="横排第二个"
            android:textSize="17sp"
            android:textColor="#000000"/>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:layout_weight="1"
            android:text="竖排第一个"
            android:textSize="17sp"
            android:textColor="#000000"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:layout_weight="1"
            android:text="竖排第二个"
            android:textSize="17sp"
            android:textColor="#000000"/>
    </LinearLayout>

</LinearLayout>
```

### 相对布局RelativeLayout

- 相对布局的下级视图位置由其他视图决定。用于确定下级视图位置的参照物分两种： 
  - 与该视图自身平级的视图
  - 该视图的上级视图（也就是它归属的RelativeLayout） 

- 如果不设定下级视图的参照物，那么下级视图默认显示在RelativeLayout内部的左上角

**相对位置的取值**

| 相对位置的属性取值       | 相对位置说明                     |
| ------------------------ | -------------------------------- |
| layout_toLeftOf          | 当前视图在指定视图的左边         |
| layout_toRightOf         | 当前视图在指定视图的右边         |
| layout_above             | 当前视图在指定视图的上方         |
| layout_below             | 当前视图在指定视图的下方         |
| layout_alignLeft         | 当前视图与指定视图的左侧对齐     |
| layout_alignRight        | 当前视图与指定视图的右侧对齐     |
| layout_alignTop          | 当前视图与指定视图的顶部对齐     |
| layout_alignBottom       | 当前视图与指定视图的底部对齐     |
| layout_centerInParent    | 当前视图在上级视图中间           |
| layout_centerHorizontal  | 当前视图在上级视图的水平方向居中 |
| layout_centerVertical    | 当前视图在上级视图的垂直方向居中 |
| layout_alignParentLeft   | 当前视图与上级视图的左侧对齐     |
| layout_alignParentRight  | 当前视图与上级视图的右侧对齐     |
| layout_alignParentTop    | 当前视图与上级视图的顶部对齐     |
| layout_alignParentBottom | 当前视图与上级视图的底部对齐     |

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="150dp">
    <TextView
        android:id="@+id/tv_center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_centerInParent="true"
        android:text="我在中间"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_center_horizontal"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_centerHorizontal="true"
        android:text="我在水平中间"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_center_vertical"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_centerVertical="true"
        android:text="我在垂直中间"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_parent_left"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_alignParentLeft="true"
        android:text="我在上级左边对齐"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_parent_right"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_alignParentRight="true"
        android:text="我在上级右边对齐"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_parent_top"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_alignParentTop="true"
        android:text="我在上级顶部对齐"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_parent_bottom"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_alignParentBottom="true"
        android:text="我在上级底部对齐"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_left_center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_toLeftOf="@id/tv_center"
        android:layout_alignTop="@id/tv_center"
        android:text="我在中间左边"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_right_center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_toRightOf="@id/tv_center"
        android:layout_alignBottom="@id/tv_center"
        android:text="我在中间右边"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_above_center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_above="@id/tv_center"
        android:layout_alignLeft="@id/tv_center"
        android:text="我在中间上面"
        android:textSize="11sp"
        android:textColor="#000000"/>
    <TextView
        android:id="@+id/tv_below_center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#ffffff"
        android:layout_below="@id/tv_center"
        android:layout_alignRight="@id/tv_center"
        android:text="我在中间下面"
        android:textSize="11sp"
        android:textColor="#000000"/>
</RelativeLayout>
```

### 网格布局GridLayout

- 网格布局支持多行多列的表格排列

- 网格布局默认从左往右、从上到下排列，它新增了两个属性：
  - columnCount属性，它指定了网格的列数，即每行能放多少个视图
  - rowCount属性，它指定了网格的行数，即每列能放多少个视图
- 补充
  - layout_columnWeight：设置列的权重  `android:layout_columnWeight="1"`
  - layout_rowWeight：设置行的权重 `android:layout_rowWeight="1"`

```xml
<GridLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:columnCount="2"
    android:rowCount="2">
    <TextView
        android:layout_width="0dp"
        android:layout_columnWeight="1"
        android:layout_height="60dp"
        android:background="#ffcccc"
        android:gravity="center"
        android:text="浅红色"
        android:textColor="#000000"
        android:textSize="17sp" />
    <TextView
        android:layout_width="0dp"
        android:layout_columnWeight="1"
        android:layout_height="60dp"
        android:background="#ffaa00"
        android:gravity="center"
        android:text="橙色"
        android:textColor="#000000"
        android:textSize="17sp" />
    <TextView
        android:layout_width="0dp"
        android:layout_columnWeight="1"
        android:layout_height="60dp"
        android:background="#00ff00"
        android:gravity="center"
        android:text="绿色"
        android:textColor="#000000"
        android:textSize="17sp" />
    <TextView
        android:layout_width="0dp"
        android:layout_columnWeight="1"
        android:layout_height="60dp"
        android:background="#660066"
        android:text="深紫色"
        android:gravity="center"
        android:textColor="#000000"
        android:textSize="17sp" />
</GridLayout>
```

### 滚动视图ScrollView

- 滚动视图有两种： 
  - ScrollView，它是垂直方向的滚动视图；垂直方向滚动时，layout_width属性值设置为match_parent，layout_height属性值设置为wrap_content
  - HorizontalScrollView，它是水平方向的滚动视图；水平方向滚动时，layout_width属性值设置为wrap_content，layout_height属性值设置为match_parent

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <HorizontalScrollView
        android:layout_width="wrap_content"
        android:layout_height="200dp">
        <!-- 水平方向的线性布局，两个子视图的颜色分别为青色和黄色 -->
        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:orientation="horizontal">
            <View
                android:layout_width="300dp"
                android:layout_height="match_parent"
                android:background="#aaffff" />
            <View
                android:layout_width="300dp"
                android:layout_height="match_parent"
                android:background="#ffff00" />
        </LinearLayout>
    </HorizontalScrollView>
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <!-- 垂直方向的线性布局，两个子视图的颜色分别为绿色和橙色 -->
        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:orientation="vertical">
            <View
                android:layout_width="match_parent"
                android:layout_height="400dp"
                android:background="#00ff00" />
            <View
                android:layout_width="match_parent"
                android:layout_height="400dp"
                android:background="#ffffaa" />
        </LinearLayout>
    </ScrollView>
</LinearLayout>
```



## 按钮触控

### 按钮控件Button

- 按钮控件Button由TextView派生而来，它们之间的区别有：
  - Button拥有默认的按钮背景，而TextView默认无背景
  - Button的内部文本默认居中对齐，而TextView的内部文本默认靠左对齐
  - Button会默认将英文字母转为大写，而TextView保持原始的英文大小写

- 与TextView相比，Button增加了两个新属性： 
  - textAllCaps属性，它指定了是否将英文字母转为大写，为true是表示自动转为大写，为false表示不做大写转换
  - onClick属性，它用来接管用户的点击动作，指定了点击按钮时要触发哪个方法

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="5dp">
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:text="下面的按钮英文默认大写"
        android:textColor="@color/black"
        android:textSize="17sp"/>
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hello World"
        android:textColor="@color/black"
        android:textSize="17sp"/>
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:text="下面的按钮英文保持原状"
        android:textColor="@color/black"
        android:textSize="17sp"/>
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hello World"
        android:textAllCaps="false"
        android:textColor="@color/black"
        android:textSize="17sp"/>
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="直接指定点击方法"
        android:textAllCaps="false"
        android:textColor="@color/black"
        android:textSize="17sp"
        android:onClick="doClick"/>
    <TextView
        android:id="@+id/tv_result"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="这里查看按钮的点击结果"
        android:textColor="@color/black"
        android:textSize="17sp"/>
</LinearLayout>
```

```java
public class ButtonStyleActivity extends AppCompatActivity {
    private TextView tv_result;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_button_style);
        tv_result = findViewById(R.id.tv_result);//控件的初始化 一般放在onCreate里 优点：只需要执行一次
    }
    public void doClick(View view){
        String desc = String.format("%s 您点击了按钮： %s", DateUtil.getNowTime(),((Button)view).getText());
        tv_result.setText(desc);
    }
}
public class DateUtil {
    public static String getNowTime(){//单独定义一个方法获取当前时间
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("HH:mm:ss");
        return simpleDateFormat.format(new Date());
    }
}
```

### 点击事件和长按事件 

- 监听器，意思是专门监听控件的动作行为。只有控件发生了指定的动作，监听器才会触发开关去执行对应的代码逻辑

- 按钮控件有两种常用的监听器：

  - 点击监听器，通过setOnClickListener方法设置。按钮被按住少于500毫秒时，会触发点击事件

    ```xml
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">
        <Button
            android:id="@+id/btn_click_single"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="指定单独的点击监听"
            android:textColor="@color/black"
            android:textSize="15sp"/>
        <TextView
            android:id="@+id/tv_result"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="5dp"
            android:gravity="center"
            android:textColor="@color/black"
            android:textSize="15sp"
            android:text="这里查看按钮的点击结果"/>
        <Button
            android:id="@+id/btn_click_public"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="指定公共的点击事件监听"
            android:textColor="@color/black"
            android:textSize="15sp"/>
    </LinearLayout>
    ```

    ```java
    public class ButtonClickActivity extends AppCompatActivity implements View.OnClickListener{
        private TextView tv_result;
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_button_click);
            tv_result = findViewById(R.id.tv_result);
            Button btn_click_single = findViewById(R.id.btn_click_single);
            btn_click_single.setOnClickListener(new MyOnClickListener(tv_result));
            Button btn_click_public = findViewById(R.id.btn_click_public);
            btn_click_public.setOnClickListener(this);
        }
        @Override
        public void onClick(View v) {//通过继承接口实现其方法，用if判断点击的哪个按钮来进行操作 优点：减少重写内部类
            if(v.getId() == R.id.btn_click_public){
                String desc = String.format("%s 您点击了按钮： %s", DateUtil.getNowTime(),((Button)v).getText());
                tv_result.setText(desc);
            }
        }
        static class MyOnClickListener implements View.OnClickListener{//建议static，防止内存泄漏（非静态内部类可能会导致内存泄漏）
            private final TextView tv_result;
            public MyOnClickListener(TextView tv_result) {
                this.tv_result = tv_result;
            }
            @Override
            public void onClick(View v) {
                String desc = String.format("%s 您点击了按钮： %s", DateUtil.getNowTime(),((Button)v).getText());
                tv_result.setText(desc);
            }
        }
    }
    ```

  - 长按监听器，通过setOnLongClickListener方法设置。按钮被按住超过500毫秒时，会触发长按事件

    ```xml
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">
        <Button
            android:id="@+id/btn_long_click"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="指定长按的点击监听"
            android:textColor="@color/black"
            android:textSize="15sp"/>
        <TextView
            android:id="@+id/tv_result"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="5dp"
            android:gravity="center"
            android:textColor="@color/black"
            android:textSize="15sp"
            android:text="这里查看按钮的点击结果"/>
    </LinearLayout>
    ```

    ```java
    public class ButtonLongClickActivity extends AppCompatActivity {
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_button_long_click);
            TextView tv_result = findViewById(R.id.tv_result);
            Button btn_long_click = findViewById(R.id.btn_long_click);
            //匿名内部类方式
            btn_long_click.setOnLongClickListener(v -> {
                String desc = String.format("%s 您点击了按钮： %s", DateUtil.getNowTime(),((Button)v).getText());
                tv_result.setText(desc);
                return true;
            });
        }
    }
    ```

### 禁用与恢复按钮 

- 在实际业务中，按钮通常拥有两种状态，即不可用状态与可用状态，它们在外观和功能上的区别如下：
  - 不可用按钮：按钮不允许点击，即使点击也没反应，同时按钮文字为灰色
  - 可用按钮：按钮允许点击，点击按钮会触发点击事件，同时按钮文字为正常的黑色

- 是否允许点击由enabled属性控制，属性值为true时表示允许点击，为false时表示不允许点击

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
        <Button
            android:id="@+id/btn_enable"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="启用测试按钮"
            android:textColor="@color/black"
            android:textSize="17sp" />
        <Button
            android:id="@+id/btn_disable"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="禁用测试按钮"
            android:textColor="@color/black"
            android:textSize="17sp" />
    </LinearLayout>
    <Button
        android:id="@+id/btn_test"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:enabled="false"
        android:text="测试按钮"
        android:textColor="#888888"
        android:textSize="17sp" />
    <TextView
        android:id="@+id/tv_result"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="这里查看测试按钮的点击结果"
        android:textColor="@color/black"
        android:textSize="17sp" />
</LinearLayout>
```

```java
public class ButtonEnableActivity extends AppCompatActivity implements View.OnClickListener {
    private Button btn_test;
    private TextView tv_result;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_button_enable);
        Button btn_enable = findViewById(R.id.btn_enable);
        Button btn_disable = findViewById(R.id.btn_disable);
        btn_test = findViewById(R.id.btn_test);
        tv_result = findViewById(R.id.tv_result);
        btn_enable.setOnClickListener(this);
        btn_disable.setOnClickListener(this);
        btn_test.setOnClickListener(this);
    }
    @Override
    public void onClick(View v) {
        switch (v.getId()){
            case R.id.btn_enable:
                //启用当前控件
                btn_test.setEnabled(true);
                btn_test.setTextColor(Color.BLACK);
                break;
            case R.id.btn_disable:
                //禁用当前控件
                btn_test.setEnabled(false);
                btn_test.setTextColor(Color.GRAY);
                break;
            case R.id.btn_test:
                String desc = String.format("%s 您点击了按钮： %s", DateUtil.getNowTime(),((Button)v).getText());
                tv_result.setText(desc);
                break;
        }
    }
}
```



## 图像显示

### 图像视图ImageView

- 图像视图展示的图片通常位于res/drawable***目录，设置图像视图的显示图片有两种方式： 

  - 在XML文件中，通过属性android:src设置图片资源，属性值格式形如“@drawable/不含扩展名的图片名称”

    ```xml
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">
        <ImageView
            android:id="@+id/iv_scale"
            android:layout_width="match_parent"
            android:layout_height="220dp"
            android:layout_marginTop="5dp"
            android:src="@drawable/xiaoxin"
            android:scaleType="centerInside"/>
    </LinearLayout>
    ```

  - 在Java代码中，调用setImageResource方法设置图片资源，方法参数格式形如“R.drawable.不含扩展名的图片名称”

    ```java
    public class ImageScaleActivity extends AppCompatActivity {
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_image_scale);
            ImageView iv_scale = findViewById(R.id.iv_scale);
            iv_scale.setImageResource(R.drawable.xiaoxin);
            iv_scale.setScaleType(ImageView.ScaleType.CENTER);
        }
    }
    ```

| XML中的缩放类型 | ScaleType类中的缩放类型 | 说明                                                   |
| --------------- | ----------------------- | ------------------------------------------------------ |
| fitXY           | FIT_XY                  | 拉伸图片使其正好填满视图（图片可能被拉伸变形）         |
| fitStart        | FIT_START               | 保持宽高比例，拉伸图片使其位于视图上方或左侧           |
| fitCenter       | FIT_CENTER              | 保持宽高比例，拉伸图片使其位于视图中间                 |
| fitEnd          | FIT_END                 | 保持宽高比例，拉伸图片使其位于视图下方或右侧           |
| center          | CENTER                  | 保持图片原尺寸，并使其位于视图中间                     |
| centerCrop      | CENTER_CROP             | 拉伸图片使其充满视图，并位于视图中间                   |
| centerInside    | CENTER_INSIDE           | 保持宽高比例，缩小图片使之位于视图中间（只缩小不放大） |

- 注意到centerInside和center的显示效果居然一模一样，这缘于它们的缩放规则设定。表面上fitCenter、centerInside、center三个类型都是居中显示，且均不越过图像视图的边界。它们之间的区别在于：fitCenter既允许缩小图片、也允许放大图片，centerInside只允许缩小图片、不允许放大图标，而center自始至终保持原始尺寸（既不允许缩小图片、也不允许放大图片）。因此，当图片尺寸大于视图宽高，centerInside与fitCenter都会缩小图片，此时它俩的显示效果相同；当图片尺寸小于视图宽高，centerInside与center都保持图片大小不变，此时它俩的显示效果相同

### 图像按钮ImageButton

- ImageButton是显示图片的图像按钮，但它继承自ImageView，而非继承Button

- ImageButton和Button之间的区别有：
  - Button既可显示文本也可显示图片，ImageButton只能显示图片不能显示文本
  - ImageButton上的图像可按比例缩放，而Button通过背景设置的图像会拉伸变形
  - Button只能靠背景显示一张图片，而ImageButton可分别在前景和背景显示图片，从而实现两张图片叠加的效果

**ImageButton的使用场合**

- 在某些场合，有的字符无法由输入法打出来，或者某些文字以特殊字体展示，就适合适合先切图再放到ImageButton。例如：开平方符号 ，等等

- ImageButton与ImageView之间的区别有： 
  - ImageButton有默认的按钮背景，ImageView默认无背景
  - ImageButton默认的缩放类型为center，而ImageView默认的缩放类型为fitCenter

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <ImageButton
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:src="@drawable/sqrt"
        android:scaleType="fitCenter"/>
</LinearLayout>
```

### 同时展示文本与图像

- 同时展示文本与图像的可能途径包括：
  1. 利用LinearLayout对ImageView和TextView组合布局
  2. 通过按钮控件Button的drawable***属性设置文本周围的图标
     - drawableTop：指定文字上方的图片
     - drawableBottom：指定文字下方的图片
     - drawableLeft：指定文字左边的图片
     - drawableRight：指定文字右边的图片
     - drawablePadding：指定图片与文字的间距

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="图标在左"
        android:drawableLeft="@drawable/ic_about"
        android:background="#FFFFFF"
        android:drawablePadding="5dp"/>
</LinearLayout>
```



## 补充

### ViewFlipper图片切换

- ViewFlipper的父类是ViewAnimator

- ViewAnimator类有4个和动画相关的方法：
  - setInAnimation：设置View进入屏幕时使用的动画，该方法有两个版本接受单个参数，类型为android.view.animation.Animation，接受两个参数，类型为Context和int，分别为Context对象和动画资源ID
  - setOutAnimation：设置View退出屏幕时使用的动画，参数含义与setlnAnimation方法一样
  - showNext: 用于显示下一个View
  - showPrevious: 用于显示上一个View

- 一般不直接使用ViewAnimator而是使用它的两个子类ViewFlipper和ViewSwitcher
- ViewFlipper可以用来指定FrameLayout内多个View之间的切换效果可以一次指定也可以每次切换的时候都指定单独的效果
- ViewFlipper额外提供了如下几个方法:
  - isFlipping:用来判断View切换是否正在进行
  - setFilpinterval:设置View之间切换的时间间隔
  - startFlipping:使用上面设置的时间间隔来开始切换所有的View，切换会循环进行
  - stopFlipping:停止View切换

使用方法：

1. 在布局中添加ViewFlipper，在ViewFlipper中添加ImageView

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:app="http://schemas.android.com/apk/res-auto"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">
   
       <ViewFlipper
           android:id="@+id/viewFlipper"
           android:layout_width="match_parent"
           android:layout_height="wrap_content">
   
           <ImageView
               android:id="@+id/imageView"
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:layout_gravity="center_horizontal"
               app:srcCompat="@drawable/a" />
   
           <ImageView
               android:id="@+id/imageView2"
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:layout_gravity="center_horizontal"
               app:srcCompat="@drawable/b" />
   
           <ImageView
               android:id="@+id/imageView3"
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:layout_gravity="center_horizontal"
               app:srcCompat="@drawable/c" />
   
       </ViewFlipper>
   
       <Button
           android:id="@+id/btn_shou"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:text="手动切换" />
   
       <Button
           android:id="@+id/btn_auto"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:text="开启自动切换" />
   </LinearLayout>
   ```

2. 设置按钮的点击事件，调用showNext切换下一张图片，调用stopFlipping关闭自动切换，调用flipInterval设置切换时间间隔，调用startFlipping开启自动切换，调用inAnimation设置切换动画

   ```kotlin
   class ViewFlipperActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_view_flipper)
   
           btn_shou.setOnClickListener {
               viewFlipper.showNext() // 切换到下一张图片
           }
           btn_auto.setOnClickListener {
               if (viewFlipper.isFlipping){ // 如果正在自动切换
                   viewFlipper.stopFlipping() // 关闭自动切换
                   btn_auto.text = "开启自动切换"
               }else{
   //                val annotation = AnimationUtils.loadAnimation(this, R.anim.ltorin) // 获取动画资源
   ////                viewFlipper.inAnimation = annotation // 设置切换动画
                   viewFlipper.flipInterval = 1000 // 设置自动切换时间为1s
                   viewFlipper.startFlipping() // 开始自动切换
                   btn_auto.text = "关闭自动切换"
               }
           }
       }
   }
   ```



### Menu菜单

创建步骤：

1. 在res目录下创建一个menu文件夹（New -> Directory）

2. 创建menu文件（New -> Menu resource file）

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <menu xmlns:android="http://schemas.android.com/apk/res/android">
       <item
           android:id="@+id/add_item"
           android:title="Add"/>
       <item
           android:id="@+id/remove_item"
           android:title="Remove"/>
   </menu>
   ```

3. 在Activity页面重写onCreateOptionsMenu方法，显示菜单

   ```kotlin
   override fun onCreateOptionsMenu(menu: Menu?): Boolean {
       menuInflater.inflate(R.menu.main,menu) // 使用Kotlin语法糖，直接调用封装好的get方法
       return true
   }
   ```

4. 在Activity页面重写onOptionsItemSelected方法，定义菜单响应事件

   ```kotlin
   override fun onOptionsItemSelected(item: MenuItem): Boolean {
       when(item.itemId){
           R.id.add_item -> Toast.makeText(this,"ADD",Toast.LENGTH_SHORT).show()
           R.id.remove_item -> Toast.makeText(this,"REMOVE",Toast.LENGTH_SHORT).show()
       }
       return true
   }
   ```

### ProgressBar进度条

- 属性：

  - `android:max`进度条的最大值
  - `android:progress`进度条已完成进度值
  - `android:indeterminate`如果设置成true，则进度条不精确显示进度
  - `style="?android:attr/progressBarStyleHorizontal"`水平进度条
  - `android:visibility`进度条可见性，visible可见，invisible不可见但占用空间，gone不可见不占用空间

- 示例：

  ```xml
  <ProgressBar
      android:id="@+id/progressBar"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:visibility="visible"
      style="?android:attr/progressBarStyleHorizontal"
      android:max="100"/>
  ```

  ```kotlin
  // 设置可见性示例代码
  findViewById<Button>(R.id.button).setOnClickListener {
      var progressBar = findViewById<ProgressBar>(R.id.progressBar)
      if (progressBar.visibility == View.VISIBLE) {
          progressBar.visibility = View.GONE // 设置为不可见
      } else {
          progressBar.visibility = View.VISIBLE // 设置为可见
      }
  }
  // 设置进度代码
  findViewById<Button>(R.id.button).setOnClickListener{
      var progressBar = findViewById<ProgressBar>(R.id.progressBar)
      progressBar.progress = progressBar.progress +10 // 每点一下按钮进度加10
  }
  ```

  

# 活动Activity

## 启停活动页面

### Activity 的启动和结束

- 从当前页面跳到新页面，跳转代码如下：

  - startActivity(new Intent(源页面.this, 目标页面.class));

  ```java
  public class ActStartActivity extends AppCompatActivity implements View.OnClickListener {
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_act_start);
          findViewById(R.id.btn_act_next).setOnClickListener(this);
      }
      @Override
      public void onClick(View v) {
          //启动新页面
          startActivity(new Intent(this,ActFinishActivity.class));
      }
  }
  ```

- 从当前页面回到上一个页面，相当于关闭当前页面，返回代码如下：

  - finish(); // 结束当前的活动页面

  ```java
  public class ActFinishActivity extends AppCompatActivity implements View.OnClickListener {
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_act_finish);
          findViewById(R.id.iv_back).setOnClickListener(this);
          findViewById(R.id.btn_finish).setOnClickListener(this);
      }
      @Override
      public void onClick(View v) {
          if (v.getId() == R.id.iv_back || v.getId() == R.id.btn_finish) {
              //结束当前活动页面
              finish();
          }
      }
  }
  ```



### Activity的生命周期

<img src="https://developer.android.google.cn/guide/components/images/activity_lifecycle.png" alt="[activity_lifecycle.png (513×663) (google.cn)](https://developer.android.google.cn/guide/components/images/activity_lifecycle.png)" /> 

- onCreate：创建活动。此时会把页面布局加载进内存，进入了初始状态
- onStart：开启活动。此时会把活动页面显示在屏幕上，进入了就绪状态
- onResume：恢复活动。此时活动页面进入活跃状态，能够与用户正常交互，例如允许响应用户的点击动作、允许用户输入文字等
- onPause：暂停活动。此时活动页面进入暂停状态（也就是退回就绪状态），无法与用户正常交互
- onStop：停止活动。此时活动页面将不在屏幕上显示
- onDestroy：销毁活动。此时回收活动占用的系统资源，把页面从内存中清除掉
- onRestart：重启活动。处于停止状态的活动，若想重新开启的话，无须经历onCreate的重复创建过程，而是走onRestart的重启过程
- onNewIntent：重用已有的活动实例

**各状态之间的切换过程**

- 打开新页面的方法调用顺序为：
  - onCreate→onStart→onResume 

- 关闭旧页面的方法调用顺序为：
  - onPause→onStop→onDestroy

```mermaid
graph LR
	A([不存在]) --> |onCreate| B([初始状态])
	B --> |onDestroy| A
	B --> |onStart| C([就绪状态])
	C --> |onStop| B
	C --> |onResume| D([活跃状态])
	D --> |onPause| C
```

**相关文章**

[了解 Activity 生命周期  | Android 开发者  | Android Developers (google.cn)](https://developer.android.google.cn/guide/components/activities/activity-lifecycle)

[Activity生命周期详解 - 简书 (jianshu.com)](https://www.jianshu.com/p/730f7f499790)

### Activity 的启动模式

**在配置文件中指定启动模式**

```xml
<activity android:name=".JumpFirstActivity" android:launchMode="standard" />
```

| launchMode属性值 | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| standard         | 标准模式，无论何时启动哪个活动，都是重新创建该页面的实例并放入栈顶。如果不指定launchMode属性，则默认为标准模式 |
| singleTop        | 启动新活动时，判断如果栈顶正好就是该活动的实例，则重用该实例；否则创建新的实例并放入栈顶，也就是按照standard模式处理 |
| singleTask       | 启动新活动时，判断如果栈中存在该活动的实例，则重用该实例，并清除位于该实例上面的所有实例；否则按照standard模式处理 |
| singleInstance   | 启动新活动时，将该活动的实例放入一个新栈中，原栈的实例列表保持不变 |

**详解**

1. **默认启动模式 standard**

   该模式可以被设定，不在 manifest 设定时候，Activity 的默认模式就是 standard。在该模式下，启动的 Activity 会依照启动顺序被依次压入 Task 栈中

   <img src="https://pb.nichi.co/consider-proof-divide" style="zoom: 67%;" /> 

2. **栈顶复用模式 singleTop**

   在该模式下，如果栈顶 Activity 为我们要新建的 Activity（目标Activity），那么就不会重复创建新的Activity

   <img src="https://pb.nichi.co/real-dream-drink" style="zoom:67%;" /> 

3. **栈内复用模式 singleTask**

   与 singleTop 模式相似，只不过 singleTop 模式是只是针对栈顶的元素，而 singleTask 模式下，如果task 栈内存在目标 Activity 实例，则将 task 内的对应 Activity 实例之上的所有 Activity 弹出栈，并将对应 Activity 置于栈顶，获得焦点

   <img src="https://pb.nichi.co/embrace-tiny-toast" style="zoom:67%;" /> 

4. **全局唯一模式 singleInstance**

   在该模式下，我们会为目标 Activity 创建一个新的 Task 栈，将目标 Activity 放入新的 Task，并让目标Activity获得焦点。新的 Task 有且只有这一个 Activity 实例。 如果已经创建过目标 Activity 实例，则不会创建新的 Task，而是将以前创建过的 Activity 唤醒

   <img src="https://pb.nichi.co/roast-desk-already" style="zoom:67%;" /> 

**在代码里面设置启动标志** 

- 启动标志的取值说明如下： 

  - Intent.FLAG_ACTIVITY_NEW_TASK：开辟一个新的任务栈

    此 Flag 跟 singleInstance 很相似，在给目标 Activity 设立此 Flag 后，会根据目标 Activity 的affinity 进行匹配，如果已经存在与其affinity 相同的 task，则将目标 Activity 压入此 Task。反之没有的话，则新建一个 task，新建的 task 的 affinity 值与目标 Activity 相同，然后将目标 Activity 压入此栈

    但它与 singleInstance 有不同的点，两点需要注意的地方：

    - 新的 Task 没有说只能存放一个目标 Activity，只是说决定是否新建一个 Task，而 singleInstance模式下新的 Task 只能放置一个目标 Activity

    - 在同一应用下，如果 Activity 都是默认的 affinity，那么此 Flag 无效，而 singleInstance 默认情况也会创建新的 Task

  - Intent.FLAG_ACTIVITY_SINGLE_TOP：当栈顶为待跳转的活动实例之时，则重用栈顶的实例

    此 Flag 与静态设置中的 singleTop 效果相同

  - Intent.FLAG_ACTIVITY_CLEAR_TOP：当栈中存在待跳转的活动实例时，则重新创建一个新实例，并清除原实例上方的所有实例

    当设置此 Flag 时，目标 Activity 会检查 Task 中是否存在此实例，如果没有则添加压入栈。如果有，就将位于 Task 中的对应 Activity 其上的所有 Activity 弹出栈，此时有以下两种情况：

    - 如果同时设置 Flag_ACTIVITY_SINGLE_TOP ，则直接使用栈内的对应 Activity

      ```java
      intent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP | Intent.FLAG_ACTIVITY_SINGLE_TOP);
      ```

    - 没有设置，则将栈内的对应 Activity 销毁重新创建

  - Intent.FLAG_ACTIVITY_NO_HISTORY：栈中不保存新启动的活动实例

  - Intent.FLAG_ACTIVITY_CLEAR_TASK：跳转到新页面时，栈中的原有实例都被清空

**举例**

1. **在两个活动之间交替跳转**

   JumpFirstActivity 跳转到 JumpSecondActivity
   
   ```java
   // 创建一个意图对象，准备跳到指定的活动页面
   Intent intent = new Intent(this, JumpSecondActivity.class);
   // 当栈中存在待跳转的活动实例时，则重新创建该活动的实例，并清除原实例上方的所有实例
   intent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP); // 设置启动标志
   startActivity(intent); // 跳转到意图对象指定的活动页面
   ```
   
   JumpSecondActivity 跳转到 JumpFirstActivity
   
   ```java
   // 创建一个意图对象，准备跳到指定的活动页面 
   Intent intent = new Intent(this, JumpFirstActivity.class); 
   // 当栈中存在待跳转的活动实例时，则重新创建该活动的实例，并清除原实例上方的所有实例 
   intent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP); // 设置启动标志 
   startActivity(intent); // 跳转到意图指定的活动页面

2. **登录成功后不再返回登录页面**

   ```java
   // 创建一个意图对象，准备跳到指定的活动页面 
   Intent intent = new Intent(this, LoginSuccessActivity.class); 
   // 设置启动标志：跳转到新页面时，栈中的原有实例都被清空，同时开辟新任务的活动栈 
   intent.setFlags(Intent.FLAG_ACTIVITY_CLEAR_TASK | Intent.FLAG_ACTIVITY_NEW_TASK); 
   startActivity(intent); // 跳转到意图指定的活动页面
   ```



## 在活动之间传递消息

### 显式Intent和隐式Intent

- Intent是各个组件之间信息沟通的桥梁，它用于Android各组件之间的通信，主要完成下列工作：
  - 标明本次通信请求从哪里来、到哪里去、要怎么走
  - 发起方携带本次通信需要的数据内容，接收方从收到的意图中解析数据
  - 发起方若想判断接收方的处理结果，意图就要负责让接收方传回应答的数据内容

**Intent意图的组成部分**

| 元素名称  | 设置方法     | 说明与用途                                               |
| --------- | ------------ | -------------------------------------------------------- |
| Component | setComponent | 组件，它指定意图的来源与目标组件，它指定意图的来源与目标 |
| Action    | setAction    | 动作，它指定意图的动作行为                               |
| Data      | setData      | 即Uri，它指定动作要操纵的数据路径                        |
| Category  | addCategory  | 类别，它指定意图的操作类别                               |
| Type      | setType      | 数据类型，它指定消息的数据类型                           |
| Extras    | putExtras    | 扩展信息，它指定装载的包裹信息                           |
| Flags     | setFlags     | 标志位，它指定活动的启动标志                             |

**显式Intent**

- 显式Intent，直接指定来源活动与目标活动，属于精确匹配。它有三种构建方式：

  - 在Intent的构造函数中指定

    ```java
    Intent intent = new Intent(this, ActNextActivity.class); // 创建一个目标确定的意图
    ```

  - 调用意图对象的setClass方法指定

    ```java
    Intent intent = new Intent(); // 创建一个新意图
    intent.setClass(this, ActNextActivity.class); // 设置意图要跳转的目标活动
    ```

  - 调用意图对象的setComponent方法指定

    ```java
    Intent intent = new Intent(); // 创建一个新意图
    // 创建包含目标活动在内的组件名称对象
    ComponentName component = new ComponentName(this, ActNextActivity.class);
    intent.setComponent(component); // 设置意图携带的组件信息
    ```

**隐式Intent**

- 隐式Intent，没有明确指定要跳转的目标活动，只给出一个动作字符串让系统自动匹配，属于模糊匹配。动作名称既可以通过setAction方法指定，也可以通过构造函数Intent(String action)直接生成意图对象。常见的系统动作如下表： 

  | Intent 类的系统动作常量名 | 系统动作的常量值             | 说明            |
  | ------------------------- | ---------------------------- | --------------- |
  | ACTION_MAIN               | android.intent.action.MAIN   | App启动时的入口 |
  | ACTION_VIEW               | android.intent.action.VIEW   | 向用户显示数据  |
  | ACTION_SEND               | android.intent.action.SEND   | 分享内容        |
  | ACTION_CALL               | android.intent.action.CALL   | 直接拨号        |
  | ACITON_DIAL               | android.intent.action.DIAL   | 准备拨号        |
  | ACTION_SENDTO             | android.intent.action.SENDTO | 发送短信        |
  | ACTION_ANSWER             | android.intent.action.ANSWER | 接听电话        |

- 调用系统拨号举例

  ```java
  String phoneNo = "12345";
  Intent intent = new Intent(); // 创建一个新意图
  //intent.setAction(Intent.ACTION_SENDTO); // 设置意图动作为准备发送短信
  //Uri uri2 = Uri.parse("smsto:" + phoneNo); // 声明一个发送短信的Uri
  intent.setAction(Intent.ACTION_DIAL); // 设置意图动作为准备拨号
  Uri uri = Uri.parse("tel:" + phoneNo); // 声明一个拨号的Uri
  intent.setData(uri); // 设置意图前往的路径
  startActivity(intent); // 启动意图通往的活动页面
  ```

- 隐式Intent还用到了过滤器的概念，把不符合匹配条件的过滤掉，剩下符合条件的按照优先顺序调用。譬如创建一个App模块，AndroidManifest.xml里的intent-filter就是配置文件中的过滤器。像最常见的首页活动MainAcitivity，它的activity节点下面便设置了action和category的过滤条件。其中android.intent.action.MAIN表示App的入口动作，而android.intent.category.LAUNCHER表示在桌面上显示App图标，配置样例如下：

  ```xml
  <activity android:name=".MainActivity">
      <intent-filter>
          <action android:name="android.intent.action.CHEN" />
          <category android:name="android.intent.category.DEFAULT" />
      </intent-filter>
  </activity>
  ```

  调用

  ```java
  intent.setAction("android.intent.action.CHEN");
  intent.addCategory(Intent.CATEGORY_DEFAULT);
  startActivity(intent);
  ```

### 向下一个Activity发送数据

- Intent使用Bundle对象存放待传递的数据信息

- Bundle对象操作各类型数据的读写方法说明见下表

  | 数据类型     | 读方法             | 写方法             |
  | ------------ | ------------------ | ------------------ |
  | 整型数       | getInt             | putInt             |
  | 浮点数       | getFloat           | putFloat           |
  | 双精度数     | getDouble          | putDouble          |
  | 布尔值       | getBoolean         | putBoolean         |
  | 字符串       | getString          | putString          |
  | 字符串数组   | getStringArray     | putStringArray     |
  | 字符串列表   | getStringArrayList | putStringArrayList |
  | 可序列化结构 | getSerializable    | putSerializable    |

- **Bundle** 
  
  - 在代码中发送消息包裹，调用意图对象的putExtras方法，即可存入消息包裹
  - 在代码中接收消息包裹，调用意图对象的getExtras方法，即可取出消息包裹
  
- 举例
  
  
  ```java
  //在活动之间传递数据的例子，首先在上一个活动使用包裹封装好数据，把包裹塞给意图对象，再调用startActivity方法跳到意图指定的目标活动
  // 创建一个意图对象，准备跳到指定的活动页面
  Intent intent = new Intent(this, ActReceiveActivity.class);
  Bundle bundle = new Bundle(); // 创建一个新包裹
  // 往包裹存入名为request_time的字符串
  bundle.putString("request_time", DateUtil.getNowTime());
  // 往包裹存入名为request_content的字符串
  bundle.putString("request_content", tv_send.getText().toString()); 
  intent.putExtras(bundle);// 把快递包裹塞给意图
  startActivity(intent);// 跳转到意图指定的活动页面
  ```
  
  ```java
  //然后在下一个活动中获取意图携带的快递包裹，从包裹取出各参数信息，并将传来的数据显示到文本视图
  // 从布局文件中获取名为tv_receive的文本视图
  TextView tv_receive = findViewById(R.id.tv_receive);
  // 从上一个页面传来的意图中获取快递包裹
  Bundle bundle = getIntent().getExtras();
  // 从包裹中取出名为request_time的字符串
  String request_time = bundle.getString("request_time");
  // 从包裹中取出名为request_content的字符串
  String request_content = bundle.getString("request_content");
  String desc = String.format("收到请求消息：\n请求时间为%s\n请求内容为%s", request_time, request_content);
  tv_receive.setText(desc); // 把请求消息的详情显示在文本视图上
  ```
  

### 向上一个Activity返回数据

- 处理下一个页面的应答数据，详细步骤说明如下： 

  - 上一个页面打包好请求数据，调用startActivityForResult方法（已过时）执行跳转动作

    - ```java
      //新方法
      ActivityResultLauncher<Intent> register = registerForActivityResult(new ActivityResultContracts.StartActivityForResult(), new ActivityResultCallback<ActivityResult>() {
          @Override
          public void onActivityResult(ActivityResult result) {
      		//重写回调方法
          }
      });
      ```

    - ```java
      register.launch(intent);//在按钮动作里调用
      ```

  - 下一个页面接收并解析请求数据，进行相应处理

  - 下一个页面在返回上一个页面时，打包应答数据并调用setResult方法返回数据包裹

  - 上一个页面重写方法onActivityResult，解析获得下一个页面的返回数据

代码演示

```java
public class ActRequestActivity extends AppCompatActivity implements View.OnClickListener {
    
    private static final String mRequest = "小陈Android开发中，对吧";
    private ActivityResultLauncher<Intent> register;
    private TextView tv_response;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_act_request);
        
        TextView tv_request = findViewById(R.id.tv_request);
        tv_request.setText("待发送的消息：" + mRequest);

        tv_response = findViewById(R.id.tv_response);

        findViewById(R.id.btn_request).setOnClickListener(this);

        register = registerForActivityResult(new ActivityResultContracts.StartActivityForResult(), result -> {
            if (result != null){
                Intent intent = result.getData();
                // 意图非空，结果代码为成功
                if (intent != null && result.getResultCode() == Activity.RESULT_OK){
                    Bundle bundle = intent.getExtras();// 从返回的意图中获取快递包裹
                    // 从包裹中取出名叫response_time的字符串
                    String response_time = bundle.getString("response_time");
                    // 从包裹中取出名叫response_content的字符串
                    String response_content = bundle.getString("response_content");
                    String desc = String.format("收到返回消息：\n应答时间为%s\n应答内容为%s", response_time, response_content);
                    tv_response.setText(desc);// 把返回消息的详情显示在文本视图上
                }
            }
        });
    }

    @Override
    public void onClick(View v) {
        // 创建一个意图对象，准备跳到指定的活动页面
        Intent intent = new Intent(this, ActResponseActivity.class);
        Bundle bundle = new Bundle(); // 创建一个新包裹
        // 往包裹存入名为request_time的字符串
        bundle.putString("request_time", DateUtil.getNowTime());
        // 往包裹存入名为request_content的字符串
        bundle.putString("request_content",mRequest);
        intent.putExtras(bundle); // 把快递包裹塞给意图
        register.launch(intent);
    }
}
```

```java
public class ActResponseActivity extends AppCompatActivity implements View.OnClickListener {

    private static final String mResponse = "对的，正在学";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_act_response);
        TextView tv_request = findViewById(R.id.tv_request);
        tv_response.setText("待返回的消息为：" + mResponse);
        
        // 从上一个页面传来的意图中获取快递包裹
        Bundle bundle = getIntent().getExtras();
        // 从包裹中取出名为request_time的字符串
        String request_time = bundle.getString("request_time");
        // 从包裹中取出名为request_content的字符串
        String request_content = bundle.getString("request_content");
        String desc = String.format("收到请求消息：\n请求时间为%s\n请求内容为%s", request_time, request_content);
        tv_request.setText(desc); // 把请求消息的详情显示在文本视图上

        findViewById(R.id.btn_response).setOnClickListener(this);

        TextView tv_response = findViewById(R.id.tv_response);
       
    }
    @Override
    public void onClick(View v) {
        Intent intent = new Intent();// 创建一个新意图
        Bundle bundle = new Bundle();// 创建一个新包裹
        // 往包裹存入名为response_time的字符串
        bundle.putString("response_time", DateUtil.getNowTime());
        // 往包裹存入名为response_content的字符串
        bundle.putString("response_content",mResponse);
        intent.putExtras(bundle);// 把快递包裹塞给意图
        // 携带意图返回上一个页面 RESULT_OK表示处理成功
        setResult(Activity.RESULT_OK,intent);
        finish();// 结束当前的活动页面 就会自动返回上一个页面
    }
}
```



## 为活动补充附加信息

### 利用资源文件配置字符串

- res\values\strings.xml 可用来配置字符串形式的参数

- 在活动页面的Java代码中，调用getString方法即可根据“R.string.参数名称”获得指定参数的字符串值

```xml
<!-- 在strings.xml里 -->
<string name="weather_str">晴天</string>
```

```java
//在java代码中
// 显示字符串资源
private void showStringResource() {
    String value = getString(R.string.weather_str);// 从strings.xml获取名叫 weather_str的字符串值 
    tv_resource.setText("来自字符串资源：今天的天气是"+value); // 在文本视图上显示文字
}
```

### 利用元数据传递配置信息

- 元数据是一种描述其他数据的数据，它相当于描述固定活动的参数信息

- 在activity节点内部添加meta-data标签，通过属性name指定元数据的名称，通过属性value指定元数据的值

```xml
<activity android:name=".MetaDataActivity">
    <meta-data
               android:name="weather"
               android:value="@string/weather_str"
               />
</activity>
```

**在代码中获取元数据** 

- 在Java代码中，获取元数据信息的步骤分为下列三步：
  - 调用getPackageManager方法获得当前应用的包管理器
  - 调用包管理器的getActivityInfo方法获得当前活动的信息对象
  - 活动信息对象的metaData是Bundle包裹类型，调用包裹对象的getString即可获得指定名称的参数值

```java
public class MetaDataActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_meta_data);
        TextView tv_meta = findViewById(R.id.tv_meta);
        // 获取应用包管理器
        PackageManager pm = getPackageManager();
        try {
            // 从应用包管理器中获取当前的活动信息
            ActivityInfo info = pm.getActivityInfo(getComponentName(), PackageManager.GET_META_DATA);
            // 获取活动附加的元数据信息
            Bundle bundle = info.metaData;
            // 从包裹中取出名叫weather的字符串
            String weather = bundle.getString("weather");
            // 在文本视图上显示文字
            tv_meta.setText(weather);
        } catch (PackageManager.NameNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### 给应用页面注册快捷方式

- 元数据不仅能传递简单的字符串参数，还能传送更复杂的资源数据，比如支付宝的快捷方式菜单

**利用元数据配置快捷菜单** 

- 元数据的meta-data标签除了前面说到的name属性和value属性，还拥有resource属性，该属性可指定一个XML文件，表示元数据想要的复杂信息保存于XML数据之中
- 利用元数据配置快捷菜单的步骤如下所示：
  - 在res/values/strings.xml添加各个菜单项名称的字符串配置
  - 创建res/xml/shortcuts.xml，在该文件中填入各组菜单项的快捷方式定义（每个菜单对应哪个活动页面）
  - 给activity节点注册元数据的快捷菜单配置

**res/xml/shortcuts.xml文件中配置：**

- shortcutId：快捷方式的编号

- enabled：是否启用快捷方式（true表示启用，false表示禁用）

- icon：快捷菜单左侧的图标

- shortcutShortLabel：快捷菜单的短标签

- shortcutLongLabel：快捷菜单的长标签。优先展示长标签的文本，长标签放不下时才展示短标签的文本

```xml
<shortcuts xmlns:android="http://schemas.android.com/apk/res/android">
    <shortcut
        android:enabled="true"
        android:icon="@mipmap/ic_launcher"
        android:shortcutId="first"
        android:shortcutLongLabel="@string/first_long"
        android:shortcutShortLabel="@string/first_short">
        <!-- targetClass指定了点击该项菜单后要打开哪个活动页面 -->
        <intent
            android:action="android.intent.action.VIEW"
            android:targetClass="com.xiaochen.app02.ActStartActivity"
            android:targetPackage="com.xiaochen.app02" />
        <categories android:name="android.shortcut.conversation" />
    </shortcut>
</shortcuts>
```

**在AndroidManifest.xml主Activity中配置：**

配置meta-data元数据，作用是告诉App首页有个快捷方式菜单，其资源内容参见位于xml目录下的

```xml
<activity
    android:name=".ActStartActivity"
    android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
    <!-- 指定快捷方式。在桌面上长按应用图标，就会弹出@xml/shortcuts所描述的快捷菜单 -->
    <meta-data
        android:name="android.app.shortcuts"
        android:resource="@xml/shortcuts" />
</activity>
```

> 补充：

- Toast使用方法

  1. 调用Toast类的静态方法`makeTest()`创建一个Toast对象
  2. `makeTest()`需要三个参数，第一个是Context上下文，传入this即可；第二个为Toast显示的文本内容；第三个为Toast显示时长，有两种可供选择：`Toast.LENGTH_SHORT`和`Toast.LENGTH_LONG`
  3. 调用`show()`方法就可以显示出来

  ```kotlin
  Toast.makeText(this,"Hello,Android!",Toast.LENGTH_SHORT).show()
  ```



# 广播

## 收发应用广播

### 收发标准广播

**与广播有关的方法主要有以下三个：**

1. sendBroadcast：发送广播
2. registerReceiver：注册广播接收器，可在onStart或onResume方法中注册接收器
3. unregisterReceiver：注销广播接收器，可在onStop或onPause方法中注销接收器

**发送标准广播：**

- 两步，创建意图对象，调用sendBroadcast

```java
// 这是广播的动作名称，发送广播和接收广播都以它作为接头暗号
private final static String STANDARD_ACTION = "com.example.mytest.standardstandard";

Intent intent = new Intent(STANDARD_ACTION); // 创建指定动作的意图
sendBroadcast(intent); // 发送标准广播
```

**定义广播接收器：**

- 广播发送出来，需要有设备去接收广播，也就是广播接收器

- 接收器主要做两个事情：一个是接收什么样的广播，另一个是收到广播要做什么
- 由于接收器的处理逻辑大同小异，因此Android提供了抽象接收器基类BroadcastReceiver
- 定义接收器方法：
  - 继承BroadcastReceiver
  - 重写接收器的onReceive方法，方法内部先判断当前广播是否符合待接收广播的名称，通过效验开展业务逻辑

```java
// 定义一个标准广播的接收器
private class StandardReceiver extends BroadcastReceiver {
    // 一旦接收到标准广播，马上触发接收器的onReceive方法
    @Override
    public void onReceive(Context context, Intent intent) {
        // 广播意图非空，且接头暗号正确
        if (intent != null && intent.getAction().equals(STANDARD_ACTION)) {
            mDesc = String.format("%s\n%s 收到一个标准广播", mDesc, DateUtil.getNowTime());
            tv_standard.setText(mDesc);
        }
    }
}
```

**开关广播接收器：**

- 避免浪费资源
- 活动页面启动注册接收器
- 活动页面停止注销接收器

```java
private StandardReceiver standardReceiver; // 声明一个标准广播的接收器实例

@Override
protected void onStart() {
    super.onStart();
    standardReceiver = new StandardReceiver(); // 创建一个标准广播的接收器
    // 创建一个意图过滤器，只处理STANDARD_ACTION的广播
    IntentFilter filter = new IntentFilter(STANDARD_ACTION);
    registerReceiver(standardReceiver, filter); // 注册接收器，注册之后才能正常接收广播
}

@Override
protected void onStop() {
    super.onStop();
    unregisterReceiver(standardReceiver); // 注销接收器，注销之后就不再接收广播
}
```

### 收发有序广播

由于广播没指定唯一的接收者，因此可能存在多个接收器，接收器没有按照顺序接收广播，可能导致处理冲突

1. 发送广播时要注明这是个有序广播调用sendOrderedBroadcast方法才能发送有序广播
2. 定义有序广播的接收器接收器的定义代码基本不变，唯一的区别是：如果在接收器的内部代码调用abortBroadcast方法，就会中断有序广播
3. 注册有序广播的多个接收器为了给接收器排队，还需调用意图过滤器的setPriority方法设置优先级，优先级越大的接收器，越先收到有序广播。

```java
public class BroadOrderActivity extends AppCompatActivity implements View.OnClickListener {
    private final static String TAG = "BroadOrderActivity";
    private final static String ORDER_ACTION = "com.example.mytest.order";
    private CheckBox ck_abort;
    private TextView tv_order;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_broad_order);
        ck_abort = findViewById(R.id.ck_abort);
        tv_order = findViewById(R.id.tv_order);
        findViewById(R.id.btn_send_order).setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.btn_send_order) {
            tv_order.setText("");
            Intent intent = new Intent(ORDER_ACTION); // 创建一个指定动作的意图
            sendOrderedBroadcast(intent, null); // 发送有序广播
        }
    }

    @Override
    protected void onStart() {
        super.onStart();
        // 多个接收器处理有序广播的顺序规则为：
        // 1、优先级越大的接收器，越早收到有序广播；
        // 2、优先级相同的时候，越早注册的接收器越早收到有序广播
        orderAReceiver = new OrderAReceiver(); // 创建一个有序广播的接收器A
        // 创建一个意图过滤器A，只处理ORDER_ACTION的广播
        IntentFilter filterA = new IntentFilter(ORDER_ACTION);
        filterA.setPriority(8); // 设置过滤器A的优先级，数值越大优先级越高
        registerReceiver(orderAReceiver, filterA); // 注册接收器A，注册之后才能正常接收广播
        orderBReceiver = new OrderBReceiver(); // 创建一个有序广播的接收器B
        // 创建一个意图过滤器A，只处理ORDER_ACTION的广播
        IntentFilter filterB = new IntentFilter(ORDER_ACTION);
        filterB.setPriority(10); // 设置过滤器B的优先级，数值越大优先级越高
        registerReceiver(orderBReceiver, filterB); // 注册接收器B，注册之后才能正常接收广播
    }

    @Override
    protected void onStop() {
        super.onStop();
        unregisterReceiver(orderAReceiver); // 注销接收器A，注销之后就不再接收广播
        unregisterReceiver(orderBReceiver); // 注销接收器B，注销之后就不再接收广播
    }

    private OrderAReceiver orderAReceiver; // 声明有序广播接收器A的实例
    // 定义一个有序广播的接收器A
    private class OrderAReceiver extends BroadcastReceiver {
        // 一旦接收到有序广播，马上触发接收器的onReceive方法
        @Override
        public void onReceive(Context context, Intent intent) {
            if (intent != null && intent.getAction().equals(ORDER_ACTION)) {
                String desc = String.format("%s%s 接收器A收到一个有序广播\n",
                        tv_order.getText().toString(), DateUtil.getNowTime());
                tv_order.setText(desc);
                if (ck_abort.isChecked()) {
                    abortBroadcast(); // 中断广播，此时后面的接收器无法收到该广播
                }
            }
        }
    }

    private OrderBReceiver orderBReceiver; // 声明有序广播接收器B的实例
    // 定义一个有序广播的接收器B
    private class OrderBReceiver extends BroadcastReceiver {
        // 一旦接收到有序广播B，马上触发接收器的onReceive方法
        @Override
        public void onReceive(Context context, Intent intent) {
            if (intent != null && intent.getAction().equals(ORDER_ACTION)) {
                String desc = String.format("%s%s 接收器B收到一个有序广播\n",
                        tv_order.getText().toString(), DateUtil.getNowTime());
                tv_order.setText(desc);
                if (ck_abort.isChecked()) {
                    abortBroadcast(); // 中断广播，此时后面的接收器无法收到该广播
                }
            }
        }
    }
}
```

### 收发静态广播

**广播有两种注册方式**

1. 在代码中注册接收器，该方式被称作动态注册

2. 在AndroidManifest.xml中注册接收器，该方式被称作静态注册。静态注册时，receiver配置示例如下：

   ```xml
   <receiver
       android:name=".receiver.ShockReceiver"
       android:enabled="true"
       android:exported="true"></receiver>
   ```

**如何发送静态广播**

为了让应用能够接收静态广播，需要给静态广播指定包名，也就是调用意图对象的setComponent方法设置组件路径

```java
String receiverPath = "com.example.chapter04.receiver.ShockReceiver";
// 创建一个指定动作的意图
Intent intent = new Intent(ShockReceiver.SHOCK_ACTION);
// 发送静态广播时，需要通过setComponent方法指定接收器的完整路径
ComponentName componentName  = new ComponentName(this, receiverPath);
intent.setComponent(componentName);  // 设置意图的组件信息
sendBroadcast(intent);  // 发送静态广播
```

**完整代码：**

```xml
<receiver
    android:name=".receiver.ShockReceiver"
    android:enabled="true"
    android:exported="true">
    <intent-filter>
        <action android:name="com.example.mytest.shock" />
    </intent-filter>
</receiver>
```

```java
public class ShockReceiver extends BroadcastReceiver {
    private static final String TAG = "ShockReceiver";
    // 静态注册时候的action、发送广播时的action、接收广播时的action，三者需要保持一致
    public static final String SHOCK_ACTION = "com.example.chapter04.shock";
    @Override
    public void onReceive(Context context, Intent intent) {
        Log.d(TAG, "onReceive");
        if (intent.getAction().equals(ShockReceiver.SHOCK_ACTION)){
            // 从系统服务中获取震动管理器
            Vibrator vb = (Vibrator) context.getSystemService(Context.VIBRATOR_SERVICE);
            vb.vibrate(500); // 命令震动器吱吱个若干秒，这里的500表示500毫秒
        }
    }
}
```

```java
public class BroadStaticActivity extends AppCompatActivity implements View.OnClickListener {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_broad_static);
        findViewById(R.id.btn_send_shock).setOnClickListener(this);
    }
    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.btn_send_shock) {
            // Android8.0之后删除了大部分静态注册，防止退出App后仍在接收广播，
            // 为了让应用能够继续接收静态广播，需要给静态注册的广播指定包名。
            String receiverPath = "com.example.chapter04.receiver.ShockReceiver";
            Intent intent = new Intent(ShockReceiver.SHOCK_ACTION); // 创建一个指定动作的意图
            // 发送静态广播之时，需要通过setComponent方法指定接收器的完整路径
            ComponentName componentName  = new ComponentName(this, receiverPath);
            intent.setComponent(componentName); // 设置意图的组件信息
            sendBroadcast(intent); // 发送静态广播
            Toast.makeText(this, "已发送震动广播", Toast.LENGTH_SHORT).show();
        }
    }
}
```



## 监听系统广播

### 接收分钟到达广播

除了应用自身的广播，系统也会发出各式各样的广播，通过监听这些系统广播，App能够得知周围环境发生了什么变化，从而按照最新环境调整运行逻辑。分钟到达广播便是系统广播之一，每当时钟到达某分零秒，也就是跳到新的分钟时刻，系统就通过全局大喇叭播报分钟广播。App只要在运行时侦听分钟广播Intent.ACTION_TIME_TICK，即可在分钟切换之际收到广播信息

由于分钟广播属于系统广播，发送操作已经交给系统了，因此若要侦听分钟广播，App只需实现该广播的接收操作。具体到编码上，接收分钟广播可分解为下面3个步骤：

1. 定义一个分钟广播的接收器，并重写接收器的onReceive方法，补充收到广播之后的处理逻辑
2. 重写活动页面的onStart方法，添加广播接收器的注册代码，注意要让接收器过滤分钟到达广播Intent.ACTION_TIME_TICK
3. 重写活动页面的onStop方法，添加广播接收器的注销代码

核心代码和标准广播差不多，主要就是将意图过滤器设置成：Intent.ACTION_TIME_TICK

```java
public class SystemMinuteActivity extends AppCompatActivity {

    private TextView tv_minute; // 声明一个文本视图对象
    private String desc = "开始侦听分钟广播，请稍等。注意要保持屏幕亮着，才能正常收到广播";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_system_minute);
        tv_minute = findViewById(R.id.tv_minute);
        tv_minute.setText(desc);
    }

    @Override
    protected void onStart() {
        super.onStart();
        timeReceiver = new TimeReceiver(); // 创建一个分钟变更的广播接收器
        // 创建一个意图过滤器，只处理系统分钟变化的广播
        IntentFilter filter = new IntentFilter(Intent.ACTION_TIME_TICK);
        registerReceiver(timeReceiver, filter); // 注册接收器，注册之后才能正常接收广播
    }

    @Override
    protected void onStop() {
        super.onStop();
        unregisterReceiver(timeReceiver); // 注销接收器，注销之后就不再接收广播
    }

    private TimeReceiver timeReceiver; // 声明一个分钟广播的接收器实例
    private class TimeReceiver extends BroadcastReceiver {
        // 一旦接收到分钟变更的广播，马上触发接收器的onReceive方法
        @Override
        public void onReceive(Context context, Intent intent) {
            if (intent != null) {
                desc = String.format("%s\n%s 收到一个分钟到达广播%s", desc, DateUtil.getNowTime(), intent.getAction());
                tv_minute.setText(desc);
            }
        }
    }
}
```

### 接收网络变更广播

接收网络变更广播可分解为下面3个步骤：

1. 定义一个网络广播的接收器，并重写接收器的onReceive方法，补充收到广播之后的处理逻辑
2. 重写活动页面的onStart方法，添加广播接收器的注册代码，注意要让接收器过滤网络变更广播android.net.conn.CONNECTIVITY_CHANGE。
3. 步骤三，重写活动页面的onStop方法，添加广播接收器的注销代码

上述3个步骤中，尤为注意第一步骤，因为onReceive方法只表示收到了网络广播，至于变成哪种网络，还得把广播消息解包才知道是怎么回事。网络广播携带的包裹中有个名为networkInfo的对象，其数据类型为NetworkInfo，于是调用NetworkInfo对象的相关方法，即可获取详细的网络信息。下面是NetworkInfo的常用方法说明：

- getType：获取网络类型

  | ConnectivityManager 类的网络类型 | 说明             |
  | -------------------------------- | ---------------- |
  | TYPE_WIFI                        | 无线热点 WiFi    |
  | TYPE_MOBILE                      | 数据连接         |
  | TYPE_WIMAX                       | WIMAX            |
  | TYPE_ETHERNET                    | 以太网           |
  | TYPE_BLUETOOTH                   | 蓝牙             |
  | TYPE_VPN                         | 虚拟专业网络 VPN |

- getTypeName：获取网络类型的名称

- getSubtype：获取网络子类型。当网络类型为数据连接时，子类型为2G/3G/4G的细分类型，如CDMA、EVDO、HSDPA、LTE等

  <img src="https://pb.nichi.co/arena-soup-attitude" style="zoom: 50%;" /> 

- getSubtypeName：获取网络子类型的名称

- getState：获取网络状态

  | NetworkInfo.State 的网络状态 | 说明     |
  | ---------------------------- | -------- |
  | CONNECTING                   | 正在连接 |
  | CONNECTED                    | 已连接   |
  | SUSPENDED                    | 挂起     |
  | DISCONNECTING                | 正在断开 |
  | DISCONNECTED                 | 已断开   |
  | UNKNOWN                      | 未知     |

```java
public class SystemNetworkActivity extends AppCompatActivity {

    private String desc = "开始侦听网络变更广播，请开关WLAN或者数据连接，再观察广播结果";
    private TextView tv_network;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_system_network);
        tv_network = findViewById(R.id.tv_network);
    }

    @Override
    protected void onStart() {
        super.onStart();
        networkReceiver = new NetworkReceiver();// 创建一个网络变更的广播接收器
        // 创建一个意图过滤器，只处理网络状态变化的广播
        IntentFilter filter = new IntentFilter("android.net.conn.CONNECTIVITY_CHANGE");
        registerReceiver(networkReceiver, filter); // 注册接收器，注册之后才能正常接收广播
    }

    @Override
    protected void onStop() {
        super.onStop();
        unregisterReceiver(networkReceiver); // 注销接收器，注销之后就不再接收广播
    }

    private NetworkReceiver networkReceiver; // 声明一个网络变更的广播接收器实例

    // 定义一个网络变更的广播接收器
    private class NetworkReceiver extends BroadcastReceiver {
        // 一旦接收到网络变更的广播，马上触发接收器的onReceive方法

        @Override
        public void onReceive(Context context, Intent intent) {
            if (intent != null) {
                NetworkInfo networkInfo = intent.getParcelableExtra("networkInfo");
                String networkClass = NetworkUtil.getNetworkClass(networkInfo.getSubtype());
                desc = String.format("%s\n%s 收到一个网络变更广播，网络大类为%s，" + "网络小类为%s，网络制式为%s，网络状态为%s", desc, DateUtil.getNowTime(), networkInfo.getTypeName(), networkInfo.getSubtypeName(), networkClass, networkInfo.getState().toString());
                tv_network.setText(desc);
            }
        }

    }
}
```

### 收发定时管理器广播

- Android提供了专门的定时管理器AlarmManager，它利用系统闹钟定时发送广播，常见方法： 
  - set：设置一次性定时器
  - setAndAllowWhileIdle：设置一次性定时器，即使设备处于空闲状态，也会保证执行定时器
  - setRepeating：设置重复定时器，但系统不保证按时发送广播
  - cancel：取消指定延迟意图的定时器

- 定时管理器使用了PendingIntent，它与Intent之间的差异主要有下列三点：
  - PendingIntent代表延迟的意图，它指向的组件不会马上激活；而Intent代表实时的意图，它指向的组件会马上激活
  - PendingIntent是一类消息的组合，不但包含目标的Intent对象，还包含请求代码、请求方式等信息
  - PendingIntent对象在创建之时便已知晓将要用于活动还是广播

如何收发定时管理器广播：

1. 定义定时器的广播接收器

   ```java
   // 声明一个闹钟广播事件的标识串
   private String ALARM_ACTION = "com.example.chapter04.alarm";
   private String mDesc = ""; // 闹钟时间到达的描述
   // 定义一个闹钟广播的接收器
   public class AlarmReceiver extends BroadcastReceiver {
       // 一旦接收到闹钟时间到达的广播，马上触发接收器的onReceive方法
       @Override
       public void onReceive(Context context, Intent intent) {
           if (intent != null) {
               mDesc = String.format("%s\n%s 闹钟时间到达", mDesc, DateUtil.getNowTime());
               tv_alarm.setText(mDesc);
               // 从系统服务中获取震动管理器
               Vibrator vb = (Vibrator) context.getSystemService(Context.VIBRATOR_SERVICE);
               vb.vibrate(500); // 命令震动器吱吱个若干秒
               if (ck_repeate.isChecked()) { // 需要重复闹钟广播
                   sendAlarm(); // 发送闹钟广播
               }
           }
       }
   }
   ```

2. 开关定时器的广播接收器

   ```java
   private AlarmReceiver alarmReceiver; // 声明一个闹钟的广播接收器
   @Override
   public void onStart() {
       super.onStart();
       alarmReceiver = new AlarmReceiver(); // 创建一个闹钟的广播接收器
       // 创建一个意图过滤器，只处理指定事件来源的广播
       IntentFilter filter = new IntentFilter(ALARM_ACTION);
       registerReceiver(alarmReceiver, filter); // 注册接收器，注册之后才能正常接收广播
   }
   
   @Override
   public void onStop() {
       super.onStop();
       unregisterReceiver(alarmReceiver); // 注销接收器，注销之后就不再接收广播
   }
   ```

3. 设置定时器的播报规则

   ```java
   // 发送闹钟广播
   private void sendAlarm() {
       Intent intent = new Intent(ALARM_ACTION); // 创建一个广播事件的意图
       // 创建一个用于广播的延迟意图
   	// 针对 S+（版本 10000 及更高版本）要求在创建 PendingIntent 时指定 FLAG_IMMUTABLE 或 FLAG_MUTABLE 之一。
       // 强烈考虑使用 FLAG_IMMUTABLE，仅当某些功能依赖于 PendingIntent 是可变的时才使用 FLAG_MUTABLE
       PendingIntent pIntent = PendingIntent.getBroadcast(this, 0,intent,
               PendingIntent.FLAG_IMMUTABLE);
       // 从系统服务中获取闹钟管理器
       AlarmManager alarmMgr = (AlarmManager) getSystemService(ALARM_SERVICE);
       long delayTime = System.currentTimeMillis() + mDelay*1000; // 给当前时间加上若干秒
       if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
           // 允许在空闲时发送广播，Android6.0之后新增的方法
           alarmMgr.setAndAllowWhileIdle(AlarmManager.RTC_WAKEUP, delayTime, pIntent);
       } else {
           // 设置一次性闹钟，延迟若干秒后，携带延迟意图发送闹钟广播（但Android6.0之后，set方法在暗屏时不保证发送广播，必须调用setAndAllowWhileIdle方法）
           alarmMgr.set(AlarmManager.RTC_WAKEUP, delayTime, pIntent);
       }
   //    // 设置重复闹钟，每隔一定间隔就发送闹钟广播（但从Android4.4开始，setRepeating方法不保证按时发送广播）
   //    alarmMgr.setRepeating(AlarmManager.RTC_WAKEUP, System.currentTimeMillis(),
   //            (long) mDelay*100, pIntent);
   }
   ```



## 捕获屏幕的变更事件

### 竖屏与横屏切换

为了避免横竖屏切换时重新加载界面的情况，Android设计了一种配置变更机制，在指定的环境配置发生变更之时，无须重启活动页面，只需执行特定的变更行为。该机制的编码过程分为两步：修改AndroidManifest.xml、修改活动页面的Java代码

1. 修改AndroidManifest.xml，给activity节点增加 android:configChanges 属性

   ```xml
   <activity
   	android:name=".ChangeDirectionActivity"
   	android:configChanges="orientation|screenLayout|screenSize" />
   ```
   
   | configChanges属性的取值 | 说明                                           |
   | ----------------------- | ---------------------------------------------- |
   | orientation             | 屏幕方向发生改变                               |
   | screenLayout            | 屏幕的显示发生改变，例如在全屏和分屏之间切换   |
   | screenSize              | 屏幕大小发生改变，例如在竖屏与横屏之间切换     |
   | keyboard                | 键盘发生改变，例如使用了外部键盘               |
   | keyboardHidden          | 软键盘弹出或隐藏                               |
   | navigation              | 导航方式发生改变，例如采用了轨迹球导航         |
   | fontScale               | 字体比例发生改变，例如在系统设置中调整默认字体 |
   | locale                  | 设备的本地位置发生改变，例如切换了系统语言     |
   | uiMode                  | 用户界面的模式发生改变，例如开启了夜间模式     |
   
2. 修改活动页面的Java代码，重写活动的 onConfigurationChanged 方法，补充对应的代码处理逻辑

   ```java
   public class ChangeDirectionActivity extends AppCompatActivity {
       private TextView tv_monitor; // 声明一个文本视图对象
       private String mDesc = ""; // 屏幕变更的描述说明
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_change_direction);
           tv_monitor = findViewById(R.id.tv_monitor);
       }
       // 在配置项变更时触发。比如屏幕方向发生变更等等
       // 有的手机需要在系统的“设置→显示”菜单开启“自动旋转屏幕”，或者从顶部下拉，找到“自动旋转”图 标并开启
       @Override public void onConfigurationChanged(Configuration newConfig) {
           super.onConfigurationChanged(newConfig);
           switch (newConfig.orientation) {// 判断当前的屏幕方向
               case Configuration.ORIENTATION_PORTRAIT:// 切换到竖屏
                   mDesc = String.format("%s%s %s\n", mDesc, DateUtil.getNowTime(), "当前屏幕为竖屏方向");
                   tv_monitor.setText(mDesc);
                   break;
               case Configuration.ORIENTATION_LANDSCAPE: // 切换到横屏
                   mDesc = String.format("%s%s %s\n", mDesc, DateUtil.getNowTime(), "当前屏幕为横屏方向");
                   tv_monitor.setText(mDesc);
                   break;
               default:
                   break;
           }
       }
   }
   ```

如果希望App始终保持竖屏界面，即使手机旋转为横屏也不改变App的界面方向，可以修改AndroidManifest.xml，给activity节点添加android:screenOrientation属性，并将该属性设置为portrait表示垂直方向，也就是保持竖屏界面；若该属性为landscape则表示水平方向，也就是保持横屏界面

```xml
<activity
	android:name=".ActTestActivity"
	android:screenOrientation="portrait"/>
```

### 回到桌面与切换到任务列表

- 若想知晓是否回到桌面，以及是否打开任务列表，均需收听系统广播Intent.ACTION_CLOSE_SYSTEM_DIALOGS

- 至于如何区分当前广播究竟是回到桌面还是打开任务列表，则要从广播意图中获取原因reason字段，该字段值为homekey时表示回到桌面，值为recentapps 时表示打开任务列表

步骤：

1. 定义广播接收器，过滤Intent.ACTION_CLOSE_SYSTEM_DIALOGS

   ```java
   // 定义一个返回到桌面的广播接收器
   private class DesktopReceiver extends BroadcastReceiver {
       // 在收到返回桌面广播时触发
       @Override
       public void onReceive(Context context, Intent intent) {
           if (intent != null && intent.getAction().equals(Intent.ACTION_CLOSE_SYSTEM_DIALOGS)) {
               String reason = intent.getStringExtra("reason");// 获取变更原因
               // 按下了主页键或者任务键
               if (!TextUtils.isEmpty(reason) && (reason.equals("homekey") || reason.equals("recentapps"))){
                   showChangeStatus(reason); // 显示变更的状态
               }
           }
       }
   }
   ```

2. 在onCreate方法中注册接收器，在onDestroy方法中注销接收器

   ```java
   private DesktopReceiver desktopReceiver; // 声明一个返回桌面的广播接收器对象
   
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_return_desktop);
       tv_monitor = findViewById(R.id.tv_monitor);
       desktopReceiver = new DesktopReceiver();
       IntentFilter filter = new IntentFilter(Intent.ACTION_CLOSE_SYSTEM_DIALOGS);
       registerReceiver(desktopReceiver, filter);
   }
   
   @Override
   protected void onDestroy() {
       super.onDestroy();
       unregisterReceiver(desktopReceiver);
   }
   ```

3. 处理监听到返回桌面或任务列表的代码逻辑，比如开启画中画

   ```java
   // 显示变更的状态
   private void showChangeStatus(String reason) {
       mDesc = String.format("%s%s 按下了%s键\n", mDesc, DateUtil.getNowTime(), reason);
       tv_monitor.setText(mDesc);
       // 安卓8.0之后才有画中画模式
       if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O
               && !isInPictureInPictureMode()) {// 当前未开启画中画模式
           // 创建画中画模式的参数构造器
           PictureInPictureParams.Builder builder = new PictureInPictureParams.Builder();
           // 设置宽高比例值，第一个参数表示分子，第二个参数表示分母
           // 下面的10/5=2，表示画中画窗口的宽度是高度的两倍
           Rational rational = new Rational(10, 5);
           builder.setAspectRatio(rational); // 设置画中画窗口的宽高比例
           // 进入画中画模式，注意enterPictureInPictureMode是Android8.0之后新增的方法
           enterPictureInPictureMode(builder.build());
       }
   }
   ```

4. 以上代码用于开启画中画模式，但有时希望在进入画中画之际调整界面，则需重写活动的onPictureInPictureModeChanged方法，该方法在应用进入画中画模式或退出画中画模式时触发，在此可补充相应的处理逻辑

   ```java
   // 在进入画中画模式或退出画中画模式时触发
   @Override
   public void onPictureInPictureModeChanged(boolean isInPictureInPictureMode, Configuration newConfig) {
       super.onPictureInPictureModeChanged(isInPictureInPictureMode, newConfig);
       if (isInPictureInPictureMode) {
           Log.d("zhen", "进入画中画");
       } else {
           Log.d("zhen", "退出画中画");
       }
   }
   ```

5. 在AndroidManifest.xml中开启画中画支持，也就是给activity节点添加supportsPictureInPicture属性并设为true

   ```xml
   <activity
       android:name=".ReturnDesktopActivity"
       android:configChanges="orientation|screenLayout|screenSize"
       android:exported="true"
       android:supportsPictureInPicture="true"/>
   ```



# 服务Service

## Service的启动和停止

### Service的生命周期

- onCreater：创建服务

- onStart：开始服务，Android 2.0以下版本使用，已启用

- onStartCommand：开始服务，Android 2.0以上版本使用，返回值说明见下表

  | 返回值类型                | 返回值说明                                             |
  | ------------------------- | ------------------------------------------------------ |
  | START_STICKY              | 黏性的服务                                             |
  | START_NOT_STICKY          | 非黏性的服务                                           |
  | START_REDELIVER_INTENT    | 重传Intent的服务                                       |
  | START_STICKY_COMPATIBLITY | START_STICKY的兼容版本，但不保证服务被杀掉后一定能重启 |

- onDestroy：销毁服务

- onBind：绑定服务

- onUnbind：解除绑定，返回值为true为允许再次绑定，之后再绑定不会调用onBind方法而是onRebind方法；返回值为false表示只能绑定一次

- onReband：重新绑定，只有onUnbind返回true时，才会调用此方法

调用顺序：

- 使用startService和stopService方法启停服务会依次调用：onCreater -> onStartCommand -> onDestroy
- 使用bindService和unbindService方法绑定解绑服务会依次调用：绑定 onCreater ->  ----> 解绑 onUnbind -> onDestroy

### 创建Service

1. 创建一个类继承Service类，重写其方法

2. 在AndroidManifest.xml文件中配置

   ```xml
   <service
       android:name=".service.NormalService"
       android:enabled="true"
       android:exported="true" />
   ```

代码示例

```java
public class NormalService extends Service {

    private void refresh(String text){
        ServiceNormalActivity.showText(text);
    }

    @Override
    public void onCreate() { // 创建服务
        super.onCreate();
        refresh("onCreate");
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) { // 启动服务
        refresh("onStartCommand. flags=" + flags);
        return START_STICKY;
    }

    @Override
    public void onDestroy() { // 销毁服务
        super.onDestroy();
        refresh("onDestroy");
    }

    @Override
    public IBinder onBind(Intent intent) {// 绑定服务，普通服务不存在绑定和解绑流程
        refresh("onBind");
        return null;
    }

    @Override
    public void onRebind(Intent intent) { // 重新绑定服务
        super.onRebind(intent);
        refresh("onRebind");
    }

    @Override
    public boolean onUnbind(Intent intent) { // 解绑服务
        refresh("onUnbind");
        return true; // 返回false表示只能绑定一次，返回true表示允许绑定多次
    }
}
```

**启动停止Service**

1. 创建指向服务的意图对象

   `Intent intent = new Intent(this,NormalService.class);`

2. 调用startService方法即可启动服务

   `startService(intent);`

3. 调用stopService方法即可关闭服务

   `stopService(intent);`

代码示例

```java
public class ServiceNormalActivity extends AppCompatActivity implements View.OnClickListener {

    private static TextView tv_normal;
    private static String mDesc;
    private Intent mIntent;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_service_normal);

        tv_normal = findViewById(R.id.tv_normal);
        findViewById(R.id.btn_start).setOnClickListener(this);
        findViewById(R.id.btn_stop).setOnClickListener(this);
        mDesc = "";

        mIntent = new Intent(this, NormalService.class);
    }

    public static void showText(String desc){
        if (tv_normal != null) {
            mDesc = String.format("%s%s %s\n", mDesc, DateUtil.getNowDateTime("HH:mm:ss"), desc);
            tv_normal.setText(mDesc);
        }
    }

    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.btn_start){
            startService(mIntent);
        }else if (v.getId() == R.id.btn_stop){
            stopService(mIntent);
        }
    }
}
```



## 服务的绑定与解绑

推荐文章：[Android 绑定服务 bindService[通俗易懂]](https://cloud.tencent.com/developer/article/2032849)

```java
public class BindImmediateService extends Service {
    private static final String TAG = "BindImmediateService";
    private final IBinder mBinder = new LocalBinder(); // 创建一个粘合剂对象
    // 定义一个当前服务的粘合剂，用于将该服务黏到活动页面的进程中
    public class LocalBinder extends Binder {
        public BindImmediateService getService() {
            return BindImmediateService.this;
        }
    }

    private void refresh(String text) {
        Log.d(TAG, text);
        BindImmediateActivity.showText(text);
    }

    @Override
    public void onCreate() { // 创建服务
        super.onCreate();
        refresh("onCreate");
    }

    @Override
    public void onDestroy() { // 销毁服务
        super.onDestroy();
        refresh("onDestroy");
    }

    @Override
    public IBinder onBind(Intent intent) { // 绑定服务。返回该服务的粘合剂对象
        Log.d(TAG, "绑定服务开始旅程！");
        refresh("onBind");
        return mBinder;
    }

    @Override
    public void onRebind(Intent intent) { // 重新绑定服务
        super.onRebind(intent);
        refresh("onRebind");
    }

    @Override
    public boolean onUnbind(Intent intent) { // 解绑服务
        Log.d(TAG, "绑定服务结束旅程！");
        refresh("onUnbind");
        return true; // 返回false表示只能绑定一次，返回true表示允许多次绑定
    }

}
```

```java
public class BindImmediateActivity extends AppCompatActivity implements View.OnClickListener {
    private static final String TAG = "BindImmediateActivity";
    private static TextView tv_immediate; // 声明一个文本视图对象
    private Intent mIntent; // 声明一个意图对象
    private static String mDesc; // 日志描述

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_bind_immediate);
        tv_immediate = findViewById(R.id.tv_immediate);
        findViewById(R.id.btn_start_bind).setOnClickListener(this);
        findViewById(R.id.btn_unbind).setOnClickListener(this);
        mDesc = "";
        // 创建一个通往立即绑定服务的意图
        mIntent = new Intent(this, BindImmediateService.class);
    }

    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.btn_start_bind) { // 点击了绑定服务按钮
            // 绑定服务。如果服务未启动，则系统先启动该服务再进行绑定
            boolean bindFlag = bindService(mIntent, mServiceConn, Context.BIND_AUTO_CREATE);
            Log.d(TAG, "bindFlag=" + bindFlag);
        } else if (v.getId() == R.id.btn_unbind) { // 点击了解绑服务按钮
            if (mBindService != null) {
                // 解绑服务。如果先前服务立即绑定，则此时解绑之后自动停止服务
                unbindService(mServiceConn);
            }
        }
    }

    public static void showText(String desc) {
        if (tv_immediate != null) {
            mDesc = String.format("%s%s %s\n", mDesc, DateUtil.getNowDateTime("HH:mm:ss"), desc);
            tv_immediate.setText(mDesc);
        }
    }

    private BindImmediateService mBindService; // 声明一个服务对象
    private ServiceConnection mServiceConn = new ServiceConnection() {
        // 获取服务对象时的操作
        @Override
        public void onServiceConnected(ComponentName name, IBinder service) {
            // 如果服务运行于另外一个进程，则不能直接强制转换类型，否则会报错
            mBindService = ((BindImmediateService.LocalBinder) service).getService();
            Log.d(TAG, "onServiceConnected");
        }

        // 无法获取到服务对象时的操作
        @Override
        public void onServiceDisconnected(ComponentName name) {
            mBindService = null;
            Log.d(TAG, "onServiceDisconnected");
        }
    };
}
```

## 活动与服务的交互

每个服务的黏合剂都得从Binder派生而来，除了定义getService方法返回当前服务对象外，黏合剂还可以定义一般的数据交互方法，用于同活动代码往来通信

```java
public class DataService extends Service {
    private static final String TAG = "DataService";
    private final IBinder mBinder = new LocalBinder(); // 创建一个粘合剂对象
    // 定义一个当前服务的粘合剂，用于将该服务黏到活动页面的进程中
    public class LocalBinder extends Binder {
        public DataService getService() {
            return DataService.this;
        }

        // 获取数字描述
        public String getNumber(int number) {
            return "我收到了数字"+number;
        }
    }

    @Override
    public IBinder onBind(Intent intent) { // 绑定服务。返回该服务的粘合剂对象
        Log.d(TAG, "绑定服务开始旅程！");
        return mBinder;
    }

    @Override
    public boolean onUnbind(Intent intent) { // 解绑服务
        Log.d(TAG, "绑定服务结束旅程！");
        return true; // 返回false表示只能绑定一次，返回true表示允许多次绑定
    }
}
```

活动代码在调用bindService时，第二个参数为ServiceConnection类型，表示绑定结果的连接对象。这个连接对象来自接口ServiceConnection，它的onServiceConnected方法在连接成功时回调,onServiceDisconnected方法在连接断开时回调。重写ServiceConnection的onServiceConnected方法，即可拿到已绑定服务的黏合剂对象。有了服务的黏合剂，才能通过黏合剂获取服务内部的情况，调用其方法

```java
private DataService.LocalBinder mBinder; // 声明一个粘合剂对象
private ServiceConnection mServiceConn = new ServiceConnection() {
    // 获取服务对象时的操作
    @Override
    public void onServiceConnected(ComponentName name, IBinder service) {
        // 如果服务运行于另外一个进程，则不能直接强制转换类型，否则会报错
        mBinder = (DataService.LocalBinder) service;
        // 活动代码通过粘合剂与服务代码通信
        String response = mBinder.getNumber(new Random().nextInt(100));
        tv_result.setText(DateUtil.getNowTime()+" 绑定服务应答："+response);
        Log.d(TAG, "onServiceConnected");
    }
    // 无法获取到服务对象时的操作
    @Override
    public void onServiceDisconnected(ComponentName name) {
        mBinder = null;
        Log.d(TAG, "onServiceDisconnected");
    }
};
```



# 中级控件

## 图形定制

### 图形Drawable

- Drawable 类型表达了各种各样的图形，包括图片、色块、画板、背景等
- 包含图片在内的图形文件放在res目录的各个drawable目录下，其中drawable目录一般保存描述性的XML文件，而图片文件一般放在具体分辨率的drawable目录下
  - drawable-ldpi里面存放低分辨率的图片（如240×320）
  - drawable-mdpi里面存放中等分辨率的图片（如320×480）
  - drawable-hdpi里面存放高分辨率的图片（如480×800），一般对应4英寸～4.5英寸的手机
  - drawable-xhdpi里面存放加高分辨率的图片（如720×1280），一般对应5英寸～5.5英寸的手机
  - drawable-xxhdpi里面存放超高分辨率的图片（如1080×1920），一般对应6英寸～6.5英寸的手机。
  - drawable-xxxhdpi里面存放超超高分辨率的图片（如1440×2560），一般对应7英寸以上的平板电脑
- 各视图的background属性、ImageView 和 ImageButton的src属性、TextView和Button四个方向的drawable***系列属性都可以引用图形文件

### 形状图形

- Shape图形又称形状图形，它用来描述常见的几何形状，包括矩形、圆角矩形、圆形、椭圆等等

- 形状图形的定义文件放在drawable目录下，它是以shape标签为根节点的XML描述文件。根节点下定义

  了6个节点，分别是：

  - shape（形状）

    shape是形状图形文件的根节点，它描述了当前是哪种几何图形

    - rectangle：矩形，默认值
    - oval：椭圆，此时corners节点会失效
    - line：直线，此时必须设置stroke节点，不然会报错
    - ring：圆环

  - size（尺寸）

    size是shape的下级节点，它描述了形状图形的宽高尺寸（若无size节点，则表示宽高与宿主视图一样大小）

    - height：像素类型，图形高度

    - width：像素类型，图形宽度

  - stroke（描边）

    stroke是shape的下级节点，它描述了形状图形的描边规格。若无stroke节点，则表示不存在描边

    - color：颜色类型，描边的颜色
    - dashGap：像素类型，每段虚线之间的间隔
    - dashWidth：像素类型，每段虚线的宽度（若dashGap和dashWidth有一个值为0，则描边为实线）
    - width：像素类型，描边的厚度

  - corners（圆角）

    corners是shape的下级节点，它描述了形状图形的圆角大小。若无corners节点，则表示没有圆角

    - bottomLeftRadius：像素类型，左下圆角的半径
    - bottomRightRadius：像素类型，右下圆角的半径
    - topLeftRadius：像素类型，左上圆角的半径
    - topRightRadius：像素类型，右上圆角的半径
    - radius：像素类型，4个圆角的半径（若有上面4个圆角半径的定义，则不需要radius定义）

  - solid（填充）

    solid是shape的下级节点，它描述了形状图形的填充色彩。若无solid节点，则表示无填充颜色

    - color：颜色类型，内部填充的颜色

  - padding（间隔）

    padding是shape的下级节点，它描述了形状图形与周围边界的间隔。若无padding节点，则表示四周不设间隔

    - top：像素类型，与上方的间隔
    - bottom：像素类型，与下方的间隔
    - left：像素类型，与左边的间隔
    - right：像素类型，与右边的间隔

  - gradient（渐变）

    gradient是shape的下级节点，它描述了形状图形的颜色渐变。若无gradient节点，则表示没有渐变效果

    - angle：整型，渐变的起始角度。为0时表示时钟的9点位置，值增大表示往逆时针方向旋转。例如，值为90表示6点位置，值为180表示3点位置，值为270表示0点/12点位置。

    - type：字符串类型，渐变类型

      | 渐变类型 | 说明                                            |
      | -------- | ----------------------------------------------- |
      | linear   | 线性渐变，默认值                                |
      | radial   | 放射渐变，起始颜色就是圆心颜色                  |
      | sweep    | 滚动渐变，即一个线段以某个端点为圆心做360度旋转 |

    - centerX：浮点型，圆心的X坐标。当android:type="linear"时不可用

    - centerY：浮点型，圆心的Y坐标。当android:type="linear"时不可用

    - gradientRadius：整型，渐变的半径。当android:type="radial"时需要设置该属性

    - centerColor：颜色类型，渐变的中间颜色

    - startColor：颜色类型，渐变的起始颜色

    - endColor：颜色类型，渐变的终止颜色

    - useLevel：布尔类型，设置为true为无渐变色、false为有渐变色

- 案例

  ```xml
  <!-- 圆角矩形 -->
  <shape xmlns:android="http://schemas.android.com/apk/res/android">
      <!-- 指定了形状内部的填充颜色 -->
      <solid android:color="#ffdd66" />
      <!-- 指定了形状轮廓的粗细与颜色 -->
      <stroke
          android:width="1dp"
          android:color="#aaaaaa" />
      <!-- 指定了形状四个圆角的半径 -->
      <corners android:radius="10dp"/>
  </shape>
  <!-- 椭圆 -->
  <shape xmlns:android="http://schemas.android.com/apk/res/android"
      android:shape="oval">
      <!-- 指定了形状内部的填充颜色 -->
      <solid android:color="#ff66aa" />
      <!-- 指定了形状轮廓的粗细与颜色 -->
      <stroke
          android:width="1dp"
          android:color="#aaaaaa" />
  </shape>
  ```

### 九宫格图片

- 将某张图片设置成视图背景时，如果图片尺寸太小，则系统会自动拉伸图片使之填满背景
- 可是一旦图片拉得过大，其画面容易变得模糊
- 为了解决这个问题，Android专门设计了点九图片。点九图片的扩展名是png，文件名后面常带有“.9”字样。因为该图片划分了3×3的九宫格区域，所以得名点九图片，也叫九宫格图片。如果背景是一个形状图形，其stroke节点的width属性已经设置了固定数值（如1dp），那么无论该图形被拉到多大，描边宽度始终是1dp。点九图片的实现原理与之类似，即拉伸图形时，只拉伸内部区域，不拉伸边缘线条。
- 为了演示九宫格图片的展示效果，要利用Android Studio制作一张点九图片。首先在drawable目录下找到待加工的原始图片button_pressed_orig.png，右击它弹出右键菜单。选择右键菜单下面的“Create 9-Patch files…”，并在随后弹出的对话框中单击OK按钮。接着drawable目录自动生成一个名为“button_pressed_orig.9.png”的图片，双击该文件，主界面右侧弹出如图5-5所示的点九图片的加工窗口。

### 状态列表图形

- Button按钮的背景在正常情况下是凸起的，在按下时是凹陷的，从按下到弹起的过程，用户便能知道点击了这个按钮

**创建过程：**

右击drawable目录，并依次选择右键菜单的New→Drawable resource file，在弹窗中输入文件名称再单击OK按钮，即可自动生成一个XML描述文件。往该文件填入下面的状态列表图形定义：

```xml
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@drawable/button_pressed" android:state_pressed="true" />
    <item android:drawable="@drawable/button_normal"/>
</selector>
```

上述XML文件的关键点是state_pressed属性，该属性表示按下状态，值为true表示按下时显示button_pressed图像，其余情况显示button_normal图像

**状态类型的取值说明** 

- 状态列表图形不仅用于按钮控件，还可用于其他拥有多种状态的控件

| 状态类型的属性名称 | 说明         | 适用的控件                          |
| ------------------ | ------------ | ----------------------------------- |
| state_pressed      | 是否按下     | 按钮Button                          |
| state_checked      | 是否勾选     | 复选框CheckBox、单选按钮RadioButton |
| state_focused      | 是否获取焦点 | 文本编辑框EditText                  |
| state_selected     | 是否选中     | 各控件通用                          |



## 选择按钮

### 复合按钮CompoundButton

- CompoundButton类是抽象的复合按钮，由它派生而来的子类包括：复选框CheckBox、单选按钮RadioButton以及开关按钮Switch

- 复合按钮的继承关系：

  <img src="https://pb.nichi.co/onion-flash-shuffle" style="zoom:67%;" /> 

- CompoundButton在XML文件中主要使用下面两个属性
  - checked：指定按钮的勾选状态，true表示勾选，false则表示未勾选。默认为未勾选
  - button：指定左侧勾选图标的图形资源，如果不指定就使用系统的默认图标

- CompoundButton在Java代码中主要使用下列4种方法
  - setChecked：设置按钮的勾选状态。
  - setButtonDrawable：设置左侧勾选图标的图形资源。
  - setOnCheckedChangeListener：设置勾选状态变化的监听器。
  - isChecked：判断按钮是否勾选。

### 复选框CheckBox

- 复选框CheckBox是CompoundButton一个最简单的实现控件，点击复选框将它勾选，再次点击取消勾选
- 复选框对象调用setOnCheckedChangeListener方法设置勾选监听器，这样在勾选和取消勾选时就会触发监听器的勾选事件

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="5dp">
    <CheckBox
        android:id="@+id/ck_system"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:padding="5dp"
        android:text="这是系统的CheckBox" />
    <CheckBox
        android:id="@+id/ck_custom"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:button="@drawable/check_box_selector"
        android:checked="true"
        android:padding="5dp"
        android:text="这个CheckBox换了图标" />
</LinearLayout>
```

```java
// 该页面实现了接口OnCheckedChangeListener，意味着要重写勾选监听器的onCheckedChanged方法
public class CheckBoxActivity extends AppCompatActivity implements CompoundButton.OnCheckedChangeListener {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_check_box);
        // 从布局文件中获取名叫ck_system的复选框
        CheckBox ck_system = findViewById(R.id.ck_system);
        // 从布局文件中获取名叫ck_custom的复选框
        CheckBox ck_custom = findViewById(R.id.ck_custom);
        // 给ck_system设置勾选监听器，一旦用户点击复选框，就触发监听器的onCheckedChanged方法
        ck_system.setOnCheckedChangeListener(this);
        // 给ck_custom设置勾选监听器，一旦用户点击复选框，就触发监听器的onCheckedChanged方法
        ck_custom.setOnCheckedChangeListener(this);
    }
    @Override
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        String desc = String.format("您%s了这个CheckBox",isChecked ? "勾选" : "取消勾选");
        buttonView.setText(desc);
    }
}
```

### 开关按钮Switch

- Switch 是开关按钮，它在选中与取消选中时可展现的界面元素比复选框丰富

- Switch 控件新添加的XML属性说明如下：
  - textOn：设置右侧开启时的文本
  - textOff：设置左侧关闭时的文本
  - track：设置开关轨道的背景
  - thumb：设置开关标识的图标

系统默认Switch开关：

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="5dp">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_gravity="start"
            android:layout_weight="1"
            android:padding="5dp"
            android:text="Switch开关：" />
        <Switch
            android:id="@+id/sw_status"
            android:layout_width="80dp"
            android:layout_height="30dp"
            android:layout_gravity="end"
            android:padding="5dp" />
    </LinearLayout>
    <TextView
        android:id="@+id/tv_result"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:gravity="start" />
</LinearLayout>
```

```java
public class SwitchDefaultActivity extends AppCompatActivity implements CompoundButton.OnCheckedChangeListener {
    private TextView tv_result;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_switch_default);
        Switch sw_status = findViewById(R.id.sw_status);
        tv_result = findViewById(R.id.tv_result);
        sw_status.setOnCheckedChangeListener(this);
    }
    @Override
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        String desc = String.format("Switch按钮的状态是%s", isChecked ? "开" : "关");
        tv_result.setText(desc);
    }
}
```

可以利用CheckBox实现仿IOS开关：

- 现在要让Android实现类似iOS的开关按钮，主要思路是借助状态列表图形，首先创建一个图形专用的XML文件，给状态列表指定选中与未选中时候的开关图标，如下所示：

  ```xml
  <selector xmlns:android="http://schemas.android.com/apk/res/android">
      <item android:state_checked="true" android:drawable="@drawable/switch_on"/>
      <item android:drawable="@drawable/switch_off"/>
  </selector>
  ```

- 然后把CheckBox标签的background属性设置为@drawable/switch_selector，同时将button属性设置

  为@null。完整的CheckBox标签内容示例如下：

  ```xml
  <CheckBox
      android:id="@+id/ck_status"
      android:layout_width="60dp"
      android:layout_height="30dp"
      android:layout_gravity="end"
      android:background="@drawable/switch_selector"
      android:button="@null" />
  ```

### 单选按钮RadioButton

- 单选按钮要在一组按钮中选择其中一项，并且不能多选，这要求有个容器确定这组按钮的范围，这个容器便是单选组RadioGroup
- RadioGroup实质上是个布局，同一组RadioButton都要放在同一个RadioGroup节点下，除了RadioButton，也允许放置其他控件

**单选组的用法**

- 判断选中了哪个单选按钮，通常不是监听某个单选按钮，而是监听单选组的选中事件
- 下面是RadioGroup常用的3个方法：
  - check：选中指定资源编号的单选按钮
  - getCheckedRadioButtonId：获取选中状态单选按钮的资源编号
  - setOnCheckedChangeListener：设置单选按钮勾选变化的监听器

**代码演示：**

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="5dp">
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="请选择您的性别" />
    <RadioGroup
        android:id="@+id/rg_gender"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
        <RadioButton
            android:id="@+id/rb_male"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="男"/>
        <RadioButton
            android:id="@+id/rb_female"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="女"/>
    </RadioGroup>
    <TextView
        android:id="@+id/tv_result"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:gravity="start" />
</LinearLayout>
```

```java
public class RadioHorizontalActivity extends AppCompatActivity implements RadioGroup.OnCheckedChangeListener {
    private TextView tv_result;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_radio_horizontal);
        RadioGroup rg_gender = findViewById(R.id.rg_gender);
        tv_result = findViewById(R.id.tv_result);
        rg_gender.setOnCheckedChangeListener(this);
    }
    @Override
    public void onCheckedChanged(RadioGroup group, int checkedId) {
        switch (checkedId){
            case R.id.rb_male:
                tv_result.setText("男孩");
                break;
            case R.id.rb_female:
                tv_result.setText("女孩");
                break;
        }
    }
}
```



## 文本输入

### 编辑框EditText

- EditText 是文本编辑框，用户可在此输入文本等信息
- EditText 的常用属性说明如下：
  - inputType：指定输入的文本类型。若同时使用多种文本类型，则可使用竖线“|”把多种文本类型拼接起来
  - maxLength：指定文本允许输入的最大长度
  - hint：指定提示文本的内容
  - textColorHint：指定提示文本的颜色

| 输入类型       | 说明                                                       |
| -------------- | ---------------------------------------------------------- |
| text           | 文本                                                       |
| textPassword   | 文本密码。显示时用圆点“·”代替                              |
| number         | 整型数                                                     |
| numberSigned   | 带符号的数字。允许在开头带负号“－”                         |
| numberDecimal  | 带小数点的数字                                             |
| numberPassword | 数字密码。显示时用圆点“·”代替                              |
| datetime       | 时间日期格式。除了数字外，还允许输入横线、斜杆、空格、冒号 |
| date           | 日期格式。除了数字外，还允许输入横线“-”和斜杆“/”           |
| time           | 时间格式。除了数字外，还允许输入冒号“:”                    |

**案例演示：**

- 用户名

  ```xml
  <EditText
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:hint="请输入用户名"
      android:inputType="text" />
  ```

- 密码

  ```xml
  <EditText
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:hint="请输入密码"
      android:inputType="textPassword" />
  ```

- 无边框

  ```xml
  <EditText
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:layout_marginTop="5dp"
      android:background="@null"
      android:hint="我的边框不见了"
      android:inputType="text" />
  ```

- 圆角矩形边框

  ```xml
  <EditText
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:layout_marginTop="5dp"
      android:background="@drawable/editext_selector"
      android:hint="我的边框是圆角"
      android:inputType="text" />
  ```

  此外还需要定义图形文件

  ```xml
  <selector xmlns:android="http://schemas.android.com/apk/res/android">
      <item android:state_focused="true" android:drawable="@drawable/shape_edit_focus"/>
      <item android:drawable="@drawable/shape_edit_normal"/>
  </selector>
  ```
  
  drawable/shape_edit_focus.xml

  ```xml
  <shape xmlns:android="http://schemas.android.com/apk/res/android">
      <!-- 指定了形状内部的填充颜色 -->
      <solid android:color="#ffffff" />
      <!-- 指定了形状轮廓的粗细与颜色 -->
      <stroke
          android:width="1dp"
          android:color="#0000ff" />
      <!-- 指定了形状四个圆角的半径 -->
      <corners android:radius="5dp" />
      <!-- 指定了形状四个方向的间距 -->
      <padding
          android:bottom="2dp"
          android:left="2dp"
          android:right="2dp"
          android:top="2dp" />
  </shape>
  ```
  
  drawable/shape_edit_normal
  
  ```xml
  <shape xmlns:android="http://schemas.android.com/apk/res/android">
      <!-- 指定了形状内部的填充颜色 -->
      <solid android:color="#ffffff" />
      <!-- 指定了形状轮廓的粗细与颜色 -->
      <stroke
          android:width="1dp"
          android:color="#aaaaaa" />
      <!-- 指定了形状四个圆角的半径 -->
      <corners android:radius="5dp" />
      <!-- 指定了形状四个方向的间距 -->
      <padding
          android:bottom="2dp"
          android:left="2dp"
          android:right="2dp"
          android:top="2dp" />
  </shape>
  ```

### 焦点变更监听器

- 编辑框点击两次后才会触发点击事件，因为第一次点击只触发焦点变更事件，第二次点击才触发点击事件
- 若要判断是否切换编辑框输入，应当监听焦点变更事件，而非监听点击事件
- 调用编辑框对象的setOnFocusChangeListener方法，即可在光标切换之时（获得光标和失去光标）触发焦点变更事件

**监听焦点变更事件的演示效果** 

- 手机号码未输满11位，就点击密码框，此时校验不通过，一边弹出提示文字，一边把焦点拉回手机框

  ```java
  public class EditFocusActivity extends AppCompatActivity implements View.OnFocusChangeListener {
      private EditText et_phone;
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_edit_focus);
          et_phone = findViewById(R.id.et_phone);
          // 从布局文件中获取名为et_password的编辑框
          EditText et_password = findViewById(R.id.et_password);
          // 给编辑框注册一个焦点变化监听器，一旦焦点发生变化，就触发监听器的onFocusChange方法
          et_password.setOnFocusChangeListener(this);
      }
  // 焦点变更事件的处理方法，hasFocus表示当前控件是否获得焦点
  // 为什么光标进入事件不选onClick？因为要点两下才会触发onClick动作（第一下是切换焦点动作）
      @Override
      public void onFocusChange(View v, boolean hasFocus) {
          if (hasFocus){
              String phone = et_phone.getText().toString();
              // 手机号码不足11位
              if (TextUtils.isEmpty(phone) || phone.length() < 11){
                  // 手机号码编辑框请求焦点，也就是把光标移回手机号码编辑框
                  et_phone.requestFocus();
                  Toast.makeText(this,"请输入11位手机号码",Toast.LENGTH_SHORT).show();
              }
          }
      }
  }
  ```

### 文本变化监听器

- 判断手机号输入满11位后自动关闭软键盘，或者密码输入满6位后自动关闭软键盘，此时要注册文本变化监听器

- 达到指定位数便自动关闭键盘的功能，可以再分解为两个独立的功能点

  - 如何关闭软键盘

    ```java
    public static void hideOneInputMethod(Activity act, View v) {
        //从系统服务中获取输入法管理器
        InputMethodManager imm = (InputMethodManager) act.getSystemService(Context.INPUT_METHOD_SERVICE);
        //关闭屏幕上的输入法软键盘
        imm.hideSoftInputFromWindow(v.getWindowToken(),0);
    }
    ```

  - 如何判断已输入的文字达到指定位数

    该功能点要求实时监控当前已输入的文本长度，这个监控操作用到文本监听器接口TextWatcher，该接口提供了3个监控方法，具体说明如下：

    - beforeTextChanged：在文本改变之前触发

    - onTextChanged：在文本改变过程中触发

    - afterTextChanged：在文本改变之后触发

    首先给手机号码编辑框和密码编辑框分别注册监听器

    ```java
    // 从布局文件中获取名为et_phone的手机号码编辑框
    EditText et_phone = findViewById(R.id.et_phone);
    // 从布局文件中获取名为et_password的密码编辑框
    EditText et_password = findViewById(R.id.et_password);
    // 给手机号码编辑框添加文本变化监听器
    et_phone.addTextChangedListener(new HideTextWatcher(et_phone, 11));
    // 给密码编辑框添加文本变化监听器
    et_password.addTextChangedListener(new HideTextWatcher(et_password, 6));
    ```

    定义一个编辑框监听器，在输入文本达到指定长度时自动隐藏输入法
    
    ```java
    private class HideTextWatcher implements TextWatcher {
        private EditText mView;//声明一个编辑框对象
        private int mMaxLength;//声明一个最大长度变量
        public HideTextWatcher(EditText v, int maxLength) {
            this.mView = v;
            this.mMaxLength = maxLength;
        }
        // 在编辑框的输入文本变化前触发
        @Override
        public void beforeTextChanged(CharSequence s, int start, int count, int after) {
        }
        // 在编辑框的输入文本变化时触发
        @Override
        public void onTextChanged(CharSequence s, int start, int before, int count) {
        }
        //在编辑框的输入文本变化后触发
        @Override
        public void afterTextChanged(Editable s) {
            String str = s.toString(); // 获得已输入的文本字符串
            // 输入文本达到11位（如手机号码），或者达到6位（如登录密码）时关闭输入
            if (str.length() ==  mMaxLength){
                //隐藏输入法
                ViewUtil.hideOneInputMethod(EditHideActivity.this,mView); // 隐藏输入法软键盘
            }
        }
    }
    ```



## 对话框

### 提醒对话框AlertDialog

- AlertDialog 可以完成常见的交互操作，例如提示、确认、选择等功能。AlertDialog借助建造器 AlertDialog.Builder 才能完成参数设置，AlertDialog.Builder的常用方法说明如下
  - setIcon：设置对话框的标题图标
  - setTitle：设置对话框的标题文本
  - setMessage：设置对话框的内容文本
  - setPositiveButton：设置肯定按钮的信息，包括按钮文本和点击监听器
  - setNegativeButton：设置否定按钮的信息，包括按钮文本和点击监听器
  - setNeutralButton：设置中性按钮的信息，包括按钮文本和点击监听器，该方法比较少用
- 调用建造器的 create 方法生成对话框实例，再调用对话框实例的show方法，在页面上弹出提醒对话框

```java
// 创建提醒对话框的建造器
AlertDialog.Builder builder = new AlertDialog.Builder(this);
builder.setTitle("尊敬的用户");// 设置对话框的标题文本
builder.setMessage("你真的要卸载我吗？"); // 设置对话框的内容文本
// 设置对话框的肯定按钮文本及其点击监听器
builder.setPositiveButton("残忍卸载", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        tv_alert.setText("卸载了");
    }
});
// 设置对话框的否定按钮文本及其点击监听器
builder.setNegativeButton("我再想想", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialog, int which) {
        tv_alert.setText("取消了");
    }
});
AlertDialog dialog = builder.create();// 根据建造器构建提醒对话框对象
dialog.show(); // 显示提醒对话
```

>补充：在Kotlin中使用

可以使用apply函数来简化写法

```kotlin
AlertDialog.Builder(this).apply {
    setTitle("This is Dialog")
    setMessage("Something important.")
    setCancelable(false)
    setPositiveButton("OK") { dialog, which ->
    }
    setNegativeButton("Cancel") { dialog, which ->
    }
    show()
}
```

### 日期对话框DatePickerDialog

- 日期选择器 DatePicker可以让用户选择具体的年月日
- 但 DatePicker并非弹窗模式，而是在当前页面占据一块区域，并且不会自动关闭
- DatePickerDialog相当于在AlertDialog上装载了DatePicker，编码时只需要调用构造方法设置当前的年月日，然后调用show方法即可弹出日期对话框
- 日期选择事件则由监听器OnDateSetListener负责响应，在该监听器的onDateSet方法中，开发者获取用户选择的具体日期，再做后续处理
- 注意：onDateSet的月份参数，起始值为0而不是1（1月 -> 0月 ，12月 -> 11月）

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <Button
        android:id="@+id/btn_date"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="请选择日期"/>
    <DatePicker
        android:id="@+id/dp_date"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:datePickerMode="spinner"
        android:calendarViewShown="false"/>
    <Button
        android:id="@+id/btn_ok"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="确定"/>
    <TextView
        android:id="@+id/tv_date"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
</LinearLayout>
```

```java
public class DatePickerActivity extends AppCompatActivity implements View.OnClickListener, DatePickerDialog.OnDateSetListener {
    private DatePicker dp_date;; // 声明一个文本视图对象
    private TextView tv_date;// 声明一个日期选择器对象
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_date_picker);
        findViewById(R.id.btn_ok).setOnClickListener(this);
        findViewById(R.id.btn_date).setOnClickListener(this);
        tv_date = findViewById(R.id.tv_date);
        // 从布局文件中获取名叫dp_date的日期选择器
        dp_date = findViewById(R.id.dp_date);
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.btn_ok:
                // 获取日期对话框设定的年月份
                String desc = String.format("您选择的日期是%d年%d月%d日", dp_date.getYear(), dp_date.getMonth() + 1, dp_date.getDayOfMonth());
                tv_date.setText(desc);
                break;
            case R.id.btn_date:
                // 获取日历的实例，里面包含了当前的年月日
                Calendar calendar = Calendar.getInstance();
                calendar.get(Calendar.YEAR);
                calendar.get(Calendar.MARCH);
                calendar.get(Calendar.DAY_OF_MONTH);
                DatePickerDialog dialog = new DatePickerDialog(this, this, 2004, 2 ,10);
                // 显示日期对话框
                dialog.show();
                break;
        }
    }
    
    // 一旦点击日期对话框上的确定按钮，就会触发监听器的onDateSet方法
    @Override
    public void onDateSet(DatePicker view, int year, int month, int dayOfMonth) {
        String desc = String.format("您选择的日期是%d年%d月%d日", year, month+1, dayOfMonth);
        tv_date.setText(desc);
    }
}
```

### 时间对话框TimePickerDialog

- 时间选择器 TimePicker 可以让用户选择具体的小时和分钟
- TimePickerDialog 的用法类似 DatePickerDialog

```java
public class TimePickerActivity extends AppCompatActivity implements View.OnClickListener, TimePickerDialog.OnTimeSetListener {
    private TextView tv_time;
    private TimePicker tp_time;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_time_picker);
        findViewById(R.id.btn_ok).setOnClickListener(this);
        findViewById(R.id.btn_time).setOnClickListener(this);
        tp_time = findViewById(R.id.tp_time);// 从布局文件中获取名叫tp_time的时间选择器
        tp_time.setIs24HourView(true);
        tv_time = findViewById(R.id.tv_time);
    }
    @Override
    public void onClick(View v) {
        switch (v.getId()){
            case R.id.btn_ok:
                String desc = String.format("您选择的时间是%d时%d分",tp_time.getHour(),tp_time.getMinute());
                tv_time.setText(desc);
                break;
            case R.id.btn_time:
                // 获取日历的一个实例，里面包含了当前的时分秒
                Calendar calendar = Calendar.getInstance();
                // 构建一个时间对话框，该对话框已经集成了时间选择器
                TimePickerDialog dialog = new TimePickerDialog(this, android.R.style.Theme_Holo_Light_Dialog, this, calendar.get(Calendar.HOUR_OF_DAY), calendar.get(Calendar.MINUTE), true);// true表示24小时制，false表示12小时制
                dialog.show();
                break;
        }
    }
    // 一旦点击时间对话框上的确定按钮，就会触发监听器的onTimeSet方法
    @Override
    public void onTimeSet(TimePicker view, int hourOfDay, int minute) {
        // 获取时间对话框设定的小时和分钟
        String desc = String.format("您选择的时间是%d时%d分",hourOfDay,minute);
        tv_time.setText(desc);
    }
}
```



# 数据存储

## 共享参数SharedPreferences

### 共享参数的用法

- SharedPreferences是Android的一个轻量级存储工具，采用的存储结构是Key-Value的键值对方式

- 共享参数的存储介质是符合XML规范的配置文件。保存路径是：/data/data/应用包名/shared_prefs/文件名.xml

- 下面是一个共享参数的XML文件示例：

  ```xml
  <?xml version='1.0' encoding='utf-8' standalone='yes' ?>
  <map>
      <string name="name">Mr Lee</string>
      <int name="age" value="30" />
      <boolean name="married" value="true" />
      <float name="weight" value="100.0" />
  </map>
  ```

**共享参数的使用场景**

- 共享参数主要适用于如下场合：
  - 简单且孤立的数据。若是复杂且相互间有关的数据，则要保存在数据库中
  - 文本形式的数据。若是二进制数据，则要保存在文件中
  - 需要持久化存储的数据。在App退出后再次启动时，之前保存的数据仍然有效
- 实际开发中，共享参数经常存储的数据有App的个性化配置信息、用户使用App的行为信息、临时需要保存的片段信息等

```java
// 从share.xml中获取共享参数对象
SharedPreferences shared = getSharedPreferences("share", MODE_PRIVATE);

// 下面是写入共享参数的代码例子
SharedPreferences.Editor editor = shared.edit();  // 获得编辑器的对象
editor.putString("name", "Mr Lee");  // 添加一个名叫name的字符串参数
editor.putInt("age", 30);  // 添加一个名叫age的整型参数
editor.putBoolean("married", true);  // 添加一个名叫married的布尔型参数
editor.putFloat("weight", 100f);  // 添加一个名叫weight的浮点数参数
editor.commit();  // 提交编辑器中的修改

// 下面是读取共享参数的代码例子
String name = shared.getString("name", "");  // 从共享参数中获得名叫name的字符串
int age = shared.getInt("age", 0);  // 从共享参数中获得名叫age的整型数
boolean married = shared.getBoolean("married", false);  // 从共享参数中获得名叫married的布尔数
float weight = shared.getFloat("weight", 0);  // 从共享参数中获得名叫weight的浮点数
```

### 实现记住密码功能

利用共享参数对该项目进行改造，使之实现记住密码的功能：

- 声明一个共享参数对象，并在onCreate函数中调用getSharedPreferences方法获取共享参数的实例
- 登录成功时，如果用户勾选了“记住密码”，就使用共享参数保存手机号码与密码
- 再次打开登录页面时，App从共享参数中读取手机号码与密码，并展示在界面上

```java
// 下面是利用共享参数保存密码的代码
// 如果勾选了“记住密码”，则把手机号码和密码都保存到共享参数中
if (bRemember) {
    SharedPreferences.Editor editor = mShared.edit();  // 获得编辑器的对象
    editor.putString("phone", et_phone.getText().toString());  // 添加名叫phone的手机号码
    editor.putString("password", et_password.getText().toString());  // 添加名叫password的密码
    editor.commit();  // 提交编辑器中的修改
}

// 下面是利用共享参数读取密码的代码
// 从share.xml中获取共享参数对象
mShared = getSharedPreferences("share_login", MODE_PRIVATE);
// 获取共享参数中保存的手机号码
String phone = mShared.getString("phone", "");
// 获取共享参数中保存的密码
String password = mShared.getString("password", "");
et_phone.setText(phone);  // 给手机号码编辑框填写上次保存的手机号
et_password.setText(password);  // 给密码编辑框填写上次保存的密码
```

### 利用设备浏览器寻找共享参数文件

- 共享参数的文件路径为“/data/data/应用包名/shared_prefs/***.xml”，单击Android Studio右下角的竖排标签“Device File Explorer”，即可打开设备文件浏览器



## 数据库SQLite

### SQL的基本语法

- 标准的SQL语句分为三类：数据定义、数据操纵和数据控制，但不同的数据库往往有自己的实现
- SQLite是一种小巧的嵌入式数据库，由于它属于轻型数据库，不涉及复杂的数据控制操作，因此App开发只用到数据定义和数据操纵两类SQL
- SQLite的SQL语法与通用的SQL语法略有不同

**SQLite的数据定义语言**

- 数据定义语言（DDL）描述了怎样变更数据实体的框架结构

- DDL语言主要包括三种操作：创建表格、删除表格、修改表结构

  - 创建表格

    格式为“CREATE  TABLE  IF  NOT  EXISTS  表格名称 (以逗号分隔的各字段定义);”

    ```sqlite
    CREATE TABLE IF NOT EXISTS user_info (
        _id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
        name VARCHAR NOT NULL,
        age INTEGER NOT NULL,
        height LONG NOT NULL,
        weight FLOAT NOT NULL,
        married INTEGER NOT NULL,
        update_time VARCHAR NOT NULL);
    ```

  - 删除表格

    格式为“DROP  TABLE  IF  EXISTS  表格名称;”

    ```sqlite
    DROP TABLE IF EXISTS user_info;
    ```

  - 修改表结构

    格式为“ALTER  TABLE  表格名称  修改操作;”

    SQLite只支持增加字段，不支持修改字段，也不支持删除字段

    ```sqlite
    ALTER TABLE user_info ADD COLUMN phone VARCHAR;

**SQLite的数据操纵语言**

- 数据操纵语言（DML）它描述了怎样处理数据实体的内部记录

- 表格记录的操作类型包括添加、删除、修改、查询四类：

  - 添加记录

    格式为“INSERT  INTO  表格名称 (以逗号分隔的字段名列表)  VALUES  (以逗号分隔的字段值列表);”

    ```sqlite
    INSERT INTO user_info (name,age,height,weight,married,update_time)
    VALUES ('张三',20,170,50,0,'20200504');
    ```

  - 删除记录

    格式为“DELETE  FROM  表格名称  WHERE  查询条件;”

    ```sqlite
    DELETE FROM user_info WHERE name='张三';
    ```

  - 修改记录

    格式为“UPDATE  表格名称  SET  字段名=字段值  WHERE  查询条件;”

    ```sqlite
    UPDATE user_info SET married=1 WHERE name='张三';
    ```

  - 查询记录

    格式为“SELECT  以逗号分隔的字段名列表  FROM  表格名称  WHERE  查询条件;”

    ```sqlite
    SELECT name FROM user_info WHERE name='张三';
    ```

    带条件排序查询，格式为“SELECT  以逗号分隔的字段名列表  FROM  表格名称  ORDER  BY  字段名  ASC或DESC;” 其中ASC代表升序，DESC代表降序

    ```sqlite
    SELECT * FROM user_info ORDER BY age ASC;
    ```

### 数据库管理器SQLiteDatabase

SQL语句毕竟只是SQL命令，若要在Java代码中操纵SQLite，还需专门的工具类。SQLiteDatabase便是Android提供的SQLite数据库管理器，开发者可以在活动页面代码调用openOrCreateDatabase方法获取数据库实例，参考代码如下：

```java
// 创建名为test.db的数据库。数据库如果不存在就创建它，如果存在就打开它
SQLiteDatabase db = openOrCreateDatabase(getFilesDir() + "/test.db", Context.MODE_PRIVATE, null);
String desc = String.format("数据库%s创建%s", db.getPath(), (db!=null)?"成功":"失 败");
tv_database.setText(desc);
// deleteDatabase(getFilesDir() + "/test.db"); // 删除名为test.db数据库
```

SQLiteDatabase是SQLite的数据库管理类，它提供了若干操作数据表的API，常用的方法有3类：

1. 管理类，用于数据库层面的操作
   - openDatabase：打开指定路径的数据库
   - isOpen：判断数据库是否已打开
   - close：关闭数据库
   - getVersion：获取数据库的版本号
   - setVersion：设置数据库的版本号
2. 事务类，用于事务层面的操作
   - beginTransaction：开始事务
   - setTransactionSuccessful：设置事务的成功标志
   - endTransaction：结束事务
3. 数据处理类，用于数据表层面的操作
   - execSQL：执行拼接好的SQL控制语句
   - delete：删除符合条件的记录
   - update：更新符合条件的记录
   - insert：插入一条记录
   - query：执行查询操作，返回结果集的游标
   - rawQuery：执行拼接好的SQL查询语句，返回结果集的游标

### 数据库帮助器SQLiteOpenHelper

SQLiteOpenHelper是Android提供的数据库辅助工具，用于指导开发者进行SQLite的合理使用

SQLiteOpenHelper的具体使用步骤如下：

1. 新建一个继承自SQLiteOpenHelper的数据库操作类，提示重写onCreate和onUpgrade两个方法
2. 封装保证数据库安全的必要方法，包括以下三种。获取单例对象：确保App运行时数据库只被打开一次，避免重复打开引起错误。打开数据库连接：读连接可调用SQLiteOpenHelper的getReadableDatabase方法获得，写连接可调用getWritableDatabase获得。关闭数据库连接：数据库操作完了，调用SQLiteDatabase对象的close方法关闭连接
3. 提供对表记录进行增加、删除、修改、查询的操作方法

**游标Cursor**

- 调用SQLiteDatabase的query和rawQuery方法时，返回的都是Cursor对象，因此获取查询结果要根据游标的指示一条一条遍历结果集合
- Cursor的常用方法可分为3类：
- 游标控制类方法，用于指定游标的状态
  - close：关闭游标
  - isClosed：判断游标是否关闭
  - isFirst：判断游标是否在开头
  - isLast：判断游标是否在末尾

- 游标移动类方法，把游标移动到指定位置
  - moveToFirst：移动游标到开头
  - moveToLast：移动游标到末尾
  - moveToNext：移动游标到下一条记录
  - moveToPrevious：移动游标到上一条记录
  - move：往后移动游标若干条记录
  - moveToPosition：移动游标到指定位置的记录
- 获取记录类方法，可获取记录的数量、类型以及取值
  - getCount：获取结果记录的数量
  - getInt：获取指定字段的整型值
  - getLong：获取指定字段的长整型值
  - getFloat：获取指定字段的浮点数值
  - getString：获取指定字段的字符串值
  - getType：获取指定字段的字段类型

```java
public class UserDBHelper extends SQLiteOpenHelper {

    private static final String DB_NAME = "user.db";
    private static final String TABLE_NAME = "user_info";
    private static final int DB_VERSION = 2;
    private static UserDBHelper mHelper = null;
    private SQLiteDatabase mRDB = null;
    private SQLiteDatabase mWDB = null;

    private UserDBHelper(Context context) {
        super(context, DB_NAME, null, DB_VERSION);
    }

    // 利用单例模式获取数据库帮助器的唯一实例
    public static UserDBHelper getInstance(Context context) {
        if (mHelper == null) {
            mHelper = new UserDBHelper(context);
        }
        return mHelper;
    }

    // 打开数据库的读连接
    public SQLiteDatabase openReadLink() {
        if (mRDB == null || !mRDB.isOpen()) {
            mRDB = mHelper.getReadableDatabase();
        }
        return mRDB;
    }

    // 打开数据库的写连接
    public SQLiteDatabase openWriteLink() {
        if (mWDB == null || !mWDB.isOpen()) {
            mWDB = mHelper.getWritableDatabase();
        }
        return mWDB;
    }

    // 关闭数据库连接
    public void closeLink() {
        if (mRDB != null && mRDB.isOpen()) {
            mRDB.close();
            mRDB = null;
        }

        if (mWDB != null && mWDB.isOpen()) {
            mWDB.close();
            mWDB = null;
        }
    }

    // 创建数据库，执行建表语句
    @Override
    public void onCreate(SQLiteDatabase db) {
        String sql = "CREATE TABLE IF NOT EXISTS " + TABLE_NAME + " (" +
                "_id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL," +
                " name VARCHAR NOT NULL," +
                " age INTEGER NOT NULL," +
                " height LONG NOT NULL," +
                " weight FLOAT NOT NULL," +
                " married INTEGER NOT NULL);";
        db.execSQL(sql);
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        String sql = "ALTER TABLE " + TABLE_NAME + " ADD COLUMN phone VARCHAR;";
        db.execSQL(sql);
        sql = "ALTER TABLE " + TABLE_NAME + " ADD COLUMN password VARCHAR;";
        db.execSQL(sql);
    }

    public long insert(User user) {
        ContentValues values = new ContentValues();
        values.put("name", user.name);
        values.put("age", user.age);
        values.put("height", user.height);
        values.put("weight", user.weight);
        values.put("married", user.married);
        // 执行插入记录动作，该语句返回插入记录的行号
        // 如果第三个参数values 为Null或者元素个数为0，由于insert()方法要求必须添加一条除了主键之外其它字段为Null值的记录，
        // 为了满足SQL语法的需要， insert语句必须给定一个字段名 ，如：insert into person(name) values(NULL)，
        // 倘若不给定字段名 ， insert语句就成了这样： insert into person() values()，显然这不满足标准SQL的语法。
        // 如果第三个参数values 不为Null并且元素的个数大于0 ，可以把第二个参数设置为null 。
        //return mWDB.insert(TABLE_NAME, null, values);

        try {
            mWDB.beginTransaction();
            mWDB.insert(TABLE_NAME, null, values);
            //int i = 10 / 0;
            mWDB.insert(TABLE_NAME, null, values);
            mWDB.setTransactionSuccessful();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            mWDB.endTransaction();
        }

        return 1;
    }

    public long deleteByName(String name) {
        //删除所有
        //mWDB.delete(TABLE_NAME, "1=1", null);
        return mWDB.delete(TABLE_NAME, "name=?", new String[]{name});
    }

    public long update(User user) {
        ContentValues values = new ContentValues();
        values.put("name", user.name);
        values.put("age", user.age);
        values.put("height", user.height);
        values.put("weight", user.weight);
        values.put("married", user.married);
        return mWDB.update(TABLE_NAME, values, "name=?", new String[]{user.name});
    }

    public List<User> queryAll() {
        List<User> list = new ArrayList<>();
        // 执行记录查询动作，该语句返回结果集的游标
        Cursor cursor = mRDB.query(TABLE_NAME, null, null, null, null, null, null);
        // 循环取出游标指向的每条记录
        while (cursor.moveToNext()) {
            User user = new User();
            user.id = cursor.getInt(0);
            user.name = cursor.getString(1);
            user.age = cursor.getInt(2);
            user.height = cursor.getLong(3);
            user.weight = cursor.getFloat(4);
            //SQLite没有布尔型，用0表示false，用1表示true
            user.married = (cursor.getInt(5) == 0) ? false : true;
            list.add(user);
        }
        return list;
    }

    public List<User> queryByName(String name) {
        List<User> list = new ArrayList<>();
        // 执行记录查询动作，该语句返回结果集的游标
        Cursor cursor = mRDB.query(TABLE_NAME, null, "name=?", new String[]{name}, null, null, null);
        // 循环取出游标指向的每条记录
        while (cursor.moveToNext()) {
            User user = new User();
            user.id = cursor.getInt(0);
            user.name = cursor.getString(1);
            user.age = cursor.getInt(2);
            user.height = cursor.getLong(3);
            user.weight = cursor.getFloat(4);
            //SQLite没有布尔型，用0表示false，用1表示true
            user.married = (cursor.getInt(5) == 0) ? false : true;
            list.add(user);
        }
        return list;
    }
}
```



## 存储卡

### 私有存储空间与公共存储空间

- Android把外部存储分成了两块区域，一块是所有应用均可访问的公共空间，另一块是只有应用自己才可访问的私有空间

- 为了更规范地管理手机存储空间，Android从7.0开始将存储卡划分为私有存储和公共存储两大部分，也就是分区存储方式，系统给每个App都分配了默认的私有存储空间。App在私有空间上读写文件无须任何授权，但是若想在公共空间读写文件，则要在AndroidManifest.xml里面添加下述的权限配置

  ```xml
  <!-- 存储卡读写 -->
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAG" />
  ```

- 若想获取公共空间的存储路径，调用的是Environment.getExternalStoragePublicDirectory方法；若想获取应用私有空间的存储路径，调用的是getExternalFilesDir方法

  ```java
  String fileName = System.currentTimeMillis() + ".txt";
  String directory = null;
  // 外部存储的私有空间
  directory = getExternalFilesDir(Environment.DIRECTORY_DOWNLOADS).toString();
  // 获取外部存储的公共空间
  directory = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DOWNLOADS).toString();
  // 内部存储私有空间
  directory = getFilesDir().toString();
  path = directory + File.separatorChar + fileName;
  ```

### 在存储卡上读取文本文件

- 文本文件的读写一般借助于FileOutputStream和FileInputStream
  - FileOutputStream用于写文件
  - FileInputStream用于读文件

```java
// 把字符串保存到指定路径的文本文件
public static void saveText(String path, String txt) {
    BufferedWriter os = null;
    try {
        // 根据指定的文件构建文件输出流对象
        os = new BufferedWriter(new FileWriter(path));
        os.write(txt); // 把字符串写入文件输出流
    } catch (Exception e) {
        e.printStackTrace();
    }finally {
        if (os != null) {
            try {
                os.close();
            }catch (IOException e){
                e.printStackTrace();
            }
        }
    }
}
// 从指定路径的文本文件中读取内容字符串
public static String openText(String path) {
    BufferedReader is = null;
    StringBuilder sb = new StringBuilder();
    try {
        // 根据指定的文件构建文件输入流对象
        is = new BufferedReader(new FileReader(path));
        String line = null;
        while ((line = is.readLine()) != null){
            sb.append(line);
        }
    } catch (Exception e) {
        e.printStackTrace();
    }finally {
        if (is != null) {
            try {
                is.close();
            }catch (IOException e){
                e.printStackTrace();
            }
        }
    }
    return sb.toString();
}
```

### 在存储卡上读写图片文件

- Android的位图工具是Bitmap，App读写Bitmap可以使用性能更好的BufferedOutputStream和BufferedInputStream

  ```java
  // 把位图数据保存到指定路径的图片文件
  public static void saveImage(String path, Bitmap bitmap) {
      // 根据指定的文件路径构建文件输出流对象
      try (FileOutputStream fos = new FileOutputStream(path)) {
          // 把位图数据压缩到文件输出流中
          bitmap.compress(Bitmap.CompressFormat.JPEG, 80, fos);
      } catch (Exception e) {
          e.printStackTrace();
      }
  }
  // 从指定路径的图片文件中读取位图数据
  public static Bitmap openImage(String path) {
      Bitmap bitmap = null; // 声明一个位图对象
      // 根据指定的文件路径构建文件输入流对象
      try (FileInputStream fis = new FileInputStream(path)) {
          bitmap = BitmapFactory.decodeStream(fis); // 从文件输入流中解码位图数据
      } catch (Exception e) {
          e.printStackTrace();
      }
      return bitmap; // 返回图片文件中的位图数据
  }
  ```

- Android还提供了BitmapFactory工具用于读取各种来源的图片，相关方法如下：

  - decodeResource：该方法可从资源文件中读取图片信息
  - decodeFile：该方法可将指定路径的图片读取到Bitmap对象
  - decodeStream：该方法从输入流中读取位图数据

  ```java
  String fileName = System.currentTimeMillis() + ".jpeg";
  // 获取当前App的私有下载目录
  path = getExternalFilesDir(Environment.DIRECTORY_DOWNLOADS).toString() + File.separatorChar +fileName;
  // 从指定的资源文件中获取位图对象
  Bitmap b1 = BitmapFactory.decodeResource(getResources(), R.drawable.xiaoxin2);
  // 把位图对象保存为图片文件
  FileUtil.saveImage(path, b1);
  ```

- 图像视图ImageView提供了下列方法显示各种来源的图片：

  - setImageResource：设置图像视图的图片资源，该方法的入参为资源图片的编号，形如“R.drawable.去掉扩展名的图片名称”
  - setImageBitmap：设置图像视图的位图对象，该方法的入参为Bitmap类型
  - setImageURI：设置图像视图的路径对象，该方法的入参为Uri类型。字符串格式的文件路径可通过代码“Uri.parse(file_path)”转换成路径对象

  ```java
  // 先调用FileUtil.openImage获得位图，再调用setImageBitmap方法
  //Bitmap b2 = FileUtil.openImage(path);
  //iv_content.setImageBitmap(b2);
  
  // 先调用decodeFile方法获得位图，再调用setImageBitmap方法
  //Bitmap b2 = BitmapFactory.decodeFile(path);
  //iv_content.setImageBitmap(b2);
  
  iv_content.setImageResource(R.drawable.xiaoxin1);
  
  // 直接调用setImageURI方法，设置图像视图的路径对象
  //iv_content.setImageURI(Uri.parse(path));
  ```



## 应用组件Application

### Application的生命周期

- Application是Android的一大组件，在App运行过程中有且仅有一个Application对象贯穿整个生命周期

- 在AndroidManifest.xml里面，activity节点的上级正是application节点。如果给application节点指定android:name属性，则表示App将运行自定义名称的Application代码

- 继承Application之后可供重写的方法主要有以下3个

  onCreate：在App启动时调用，Application的onCreate方法调用先于Activity的onCreate方法调用

  onTerminate：在App终止时也不会调用，纯属摆设，永远不会被调用

  onConfigurationChanged：在配置改变时调用，例如从竖屏变为横屏

### 利用Application操作全局变量

- 全局的意思是其他代码都可以引用该变量，因此全局变量是共享数据和消息传递的好帮手
- 适合在Application中保存的全局变量主要有下面3类数据
  1. 会频繁读取的信息，如用户名、手机号等
  2. 不方便由意图传递的数据，例如位图对象、非字符串类型的集合对象等
  3. 容易因频繁分配内存而导致内存泄漏的对象，如Handler对象等

**全局变量的实现**

- Java代码可利用自定义Application的静态成员变量实现全局变量的功能。具体需要完成以下3项工作

  1. 写一个继承自Application的类MainApplication。该类要采用单例模式，内部声明自身类的一个静态成员对象，然后提供该静态对象的获取方法getInstance

     ```java
     public class MyApplication extends Application {
     
         private static MyApplication mApp;// 声明一个当前应用的静态实例
         // 声明一个公共的信息映射对象，可当作全局变量使用
         public HashMap<String, String> infoMap = new HashMap<>();
         // 利用单例模式获取当前应用的唯一实例
         public static MyApplication getInstance(){
             return mApp;
         }
         // 在App启动时调用
         @Override
         public void onCreate() {
             super.onCreate();
             mApp = this;// 在打开应用时对静态的应用实例赋值
             Log.d("chenNB","MyApplication onCreate");
         }
     
     }
     ```

  2. 在Activity中调用MainApplication的getInstance方法，获得MainApplication的一个静态对象，通过该对象访问MainApplication的公共变量和公共方法

  3. 不要忘了在AndroidManifest.xml中注册新定义的Application类名，即在application节点中增加android:name属性，值为“.MainApplication”

### 利用Room简化数据库操作

- 使用数据库帮助器编码的时候，开发者每次都得手工实现以下代码逻辑
  1. 重写数据库帮助器的onCreate方法，添加该表的建表语句
  2. 在插入记录之时，必须将数据实例的属性值逐一赋给该表的各字段
  3. 在查询记录之时，必须遍历结果集游标，把各字段值逐一赋给数据实例
  4. 每次读写操作之前，都要先开启数据库连接；读写操作之后，又要关闭数据库连接

**Room框架的导入**

- Room是谷歌公司推出的数据库处理框架，该框架同样基于SQLite，但它通过注解技术极大简化了数据库操作，减少了原来相当一部分编码工作量

- 在使用Room之前，要先修改模块的build.gradle文件，往dependencies节点添加下面两行配置，表示导入指定版本的Room库

  ```groovy
  implementation 'androidx.room:room-runtime:2.4.2'
  annotationProcessor 'androidx.room:room-compiler:2.4.2'
  ```

**Room框架的编码步骤**

- 以录入书籍信息为例，使用Room框架的编码过程分为下列五步

  1. 编写书籍信息表对应的实体类，该类添加“@Entity”注解

     ```java
     //书籍信息
     @Entity
     public class BookInfo {
         /*@PrimaryKey(autoGenerate = true) 表示自增长
         private int id;*/
         @PrimaryKey // 该字段是主键，不能重复
         @NonNull // 主键必须是非空字段
         private String name; // 书籍名称
         private String author; // 作者
         private String press; // 出版社
         private double price; // 价格
     }
     ```

  2. 编写书籍信息表对应的持久化类，该类添加“@Dao”注解

     ```java
     @Dao
     public interface BookDao {
     
         @Query("SELECT * FROM BookInfo") // 设置查询语句
         List<BookInfo> queryAllBook(); // 加载所有书籍信息
     
         @Query("SELECT * FROM BookInfo WHERE name = :name") // 设置带条件的查询语句
         BookInfo queryBookByName(String name); // 根据名字加载书籍
     
         @Insert(onConflict = OnConflictStrategy.REPLACE) // 记录重复时替换原记录
         void insertOneBook(BookInfo book); // 插入一条书籍信息
     
         @Insert
         void insertBookList(List<BookInfo> bookList); // 插入多条书籍信息
     
         @Update(onConflict = OnConflictStrategy.REPLACE)// 出现重复记录时替换原记录
         int updateBook(BookInfo book); // 更新书籍信息
     
         @Delete
         void deleteBook(BookInfo book); // 删除书籍信息
     
         @Query("DELETE FROM BookInfo WHERE 1=1") // 设置删除语句
         void deleteAllBook(); // 删除所有书籍信息
     }
     ```

  3. 编写书籍信息表对应的数据库类，该类从RoomDatabase派生而来，并添加“@Database”注解

     ```java
     //entities表示该数据库有哪些表，version表示数据库的版本号
     //exportSchema表示是否导出数据库信息的json串，建议设为false，若设为true还需指定json文件的保存路径
     @Database(entities = {BookInfo.class},version = 1, exportSchema = false)
     public abstract class BookDatabase extends RoomDatabase {
         // 获取该数据库中某张表的持久化对象
         public abstract BookDao bookDao();
     }
     ```

     ```groovy
     javaCompileOptions {
         annotationProcessorOptions {
             arguments = ["room.schemaLocation": "$projectDir/schemas".toString()]//指定数据库schema导出的位置
         }
     }
     ```

  4. 在自定义的Application类中声明书籍数据库的唯一实例

     ```java
     
     public class MainApplication extends MultiDexApplication {
         private final static String TAG = "MainApplication";
         private static MainApplication mApp; // 声明一个当前应用的静态实例
         private BookDatabase bookDatabase; // 声明一个书籍数据库对象
         // 利用单例模式获取当前应用的唯一实例
         public static MainApplication getInstance() {
             return mApp;
         }
         @Override
         public void onCreate() {
             super.onCreate();
             Log.d(TAG, "onCreate");
             mApp = this; // 在打开应用时对静态的应用实例赋值
             // 构建书籍数据库的实例
             bookDatabase = Room.databaseBuilder(mApp, BookDatabase.class,"BookInfo")
                     .addMigrations() // 允许迁移数据库（发生数据库变更时，Room默认删除原数据库再创建新数据库。如此一来原来的记录会丢失，故而要改为迁移方式以便保存原有记录）
                     .allowMainThreadQueries() // 允许在主线程中操作数据库（Room默认不能在主线程中操作数据库）
                     .build();
         }
         // 获取书籍数据库的实例
         public BookDatabase getBookDB(){
             return bookDatabase;
         }
     }
     ```

  5. 在操作书籍信息表的地方获取数据表的持久化对象

     ```java
     // 从App实例中获取唯一的书籍持久化对象
     BookDao bookDao = MainApplication.getInstance().getBookDB().bookDao();
     // 增
     BookInfo b1 = new BookInfo();
     b1.setName(name);
     b1.setAuthor(author);
     b1.setPress(press);
     b1.setPrice(Double.parseDouble(price));
     bookDao.inset(b1);
     // 删 删除id为1的结果
     BookInfo b2 = new BookInfo();
     b2.setId(1);
     bookDao.delete(b2);
     // 改
     BookInfo b3 = new BookInfo();
     BookInfo b4 = bookDao.queryByName(name);// 根据名字查询到数据库中已有的记录
     b3.setId(b4.getId());
     b3.setName(name);
     b3.setAuthor(author);
     b3.setPress(press);
     b3.setPrice(Double.parseDouble(price));
     bookDao.update(b3);
     // 查 查询所有结果打印到日志
     List<BookInfo> list = bookDao.queryAll();
     for (BookInfo b : list) {
         Log.d("chenNB",b.toString());
     }
     ```



# 共享数据

## 在应用之间共享数据

- 内容提供器涵盖与内部数据存取有关的一系列组件，完整的内容组件由内容提供器ContentProvider、内容解析器ContentResolver、内容观察器ContentObserver三部分组成
- ContentProvider给App存取内部数据提供了统一的外部接口，让不同的应用之间得以互相共享数据
- ContentProvider可操作当前设备其他应用的内部数据，它是一种中间层次的数据存储形式

### 通过ContentProvider封装数据

**Uri(通用资源标识符 Universal Resource Identifer)：**

- Uri代表数据操作的地址，每一个ContentProvider都会有唯一的地址。ContentProvider使用的Uri语法结构：
  - `content://authority/data_path/id`
  - `content:// `是通用前缀，表示该Uri用于ContentProvider定位资源
  - `authority`是授权者名称，用来确定具体由哪一个ContentProvider提供资源，因此一般authority都由类的小写全称组成，以保证唯一性
  - `data_path `是数据路径，用来确定请求的是哪个数据集
  - `id `是数据编号，用来请求单条数据，如果是多条这个字段忽略

1. 编写用户信息表的数据库帮助器

   ```java
   public class UserDBHelper extends SQLiteOpenHelper {
       private static final String TAG = "UserDBHelper";
       private static final String DB_NAME = "user.db"; // 数据库的名称
       private static final int DB_VERSION = 1; // 数据库的版本号
       private static UserDBHelper mHelper = null; // 数据库帮助器的实例
       public static final String TABLE_NAME = "user_info"; // 表的名称
   
       private UserDBHelper(Context context) {
           super(context, DB_NAME, null, DB_VERSION);
       }
   
       private UserDBHelper(Context context, int version) {
           super(context, DB_NAME, null, version);
       }
   
       // 利用单例模式获取数据库帮助器的唯一实例
       public static UserDBHelper getInstance(Context context, int version) {
           if (version > 0 && mHelper == null) {
               mHelper = new UserDBHelper(context, version);
           } else if (mHelper == null) {
               mHelper = new UserDBHelper(context);
           }
           return mHelper;
       }
   
       // 创建数据库，执行建表语句
       public void onCreate(SQLiteDatabase db) {
           Log.d(TAG, "onCreate");
           String drop_sql = "DROP TABLE IF EXISTS " + TABLE_NAME + ";";
           Log.d(TAG, "drop_sql:" + drop_sql);
           db.execSQL(drop_sql);
           String create_sql = "CREATE TABLE IF NOT EXISTS " + TABLE_NAME + " ("
                   + "_id INTEGER PRIMARY KEY  AUTOINCREMENT NOT NULL,"
                   + "name VARCHAR NOT NULL," + "age INTEGER NOT NULL,"
                   + "height INTEGER NOT NULL," + "weight FLOAT NOT NULL," + ");";
           Log.d(TAG, "create_sql:" + create_sql);
           db.execSQL(create_sql); // 执行完整的SQL语句
       }
   
       // 升级数据库，执行表结构变更语句
       public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
       }
   }
   ```

2. 编写内容提供器的基础字段

   定义一个类实现接口BaseColumns

   ```java
   public class UserInfoContent implements BaseColumns {
       // 这里的名称必须与AndroidManifest.xml里的android:authorities保持一致
       public static final String AUTHORITIES = "com.example.app07_server.provider.UserInfoProvider";
       // 内容提供器的外部表名
       public static final String TABLE_NAME = UserDBHelper.TABLE_NAME;
       // 访问内容提供器的Uri
       public static final Uri CONTENT_URI = Uri.parse("content://" + AUTHORITIES + "/user");
       // 下面是该表各个字段的名称
       public static final String USER_NAME = "name";
       public static final String USER_AGE = "age";
       public static final String USER_HEIGHT = "height";
       public static final String USER_WEIGHT = "weight";
   }
   ```

3. 创建内容提供器

   提供菜单选择 New -> Other -> ContentProvider 快捷创建内容提供器，也可以创建一个类继承ContentProvider，重写其方法，然后在AndroidManifest中注册配置

   ```xml
   <provider
       android:name=".provider.UserInfoProvider"
       android:authorities="com.example.app07_server.provider.UserInfoProvider"
       android:enabled="true"
       android:exported="true"/> 
   ```

   然后在UserInfoProvider中，在onCreate中实例化数据库帮助器，增加增删改查业务逻辑

   ```java
   public class UserInfoProvider extends ContentProvider {
   
       private UserDBHelper userDB; // 声明一个用户数据库的帮助对象
       public static final int USER_INFO = 1; // Uri匹配时的代号
       public static final UriMatcher uriMatcher = new UriMatcher(UriMatcher.NO_MATCH);
       static { // 往Uri匹配器中添加指定的数据路径
           uriMatcher.addURI(UserInfoContent.AUTHORITIES, "/user", USER_INFO);
       }
   
       // 创建ContentProvider时调用，可在此获取具体的数据库帮助器实例
       @Override
       public boolean onCreate() {
           userDB = UserDBHelper.getInstance(getContext(), 1);
           return true;
       }
   
       // 插入数据
       @Override
       public Uri insert(Uri uri, ContentValues values) {
           if (uriMatcher.match(uri) == USER_INFO) { // 匹配到了用户信息表
               // 获取SQLite数据库的写连接
               SQLiteDatabase db = userDB.getWritableDatabase();
               // 向指定的表插入数据，返回记录的行号
               long rowId = db.insert(UserInfoContent.TABLE_NAME, null, values);
               if (rowId > 0) { // 判断插入是否执行成功
                   // 如果添加成功，就利用新记录的行号生成新的地址
                   Uri newUri = ContentUris.withAppendedId(UserInfoContent.CONTENT_URI, rowId);
                   // 通知监听器，数据已经改变
                   getContext().getContentResolver().notifyChange(newUri, null);
               }
               db.close(); // 关闭SQLite数据库连接
           }
           return uri;
       }
   
       // 根据指定条件删除数据
       @Override
       public int delete(Uri uri, String selection, String[] selectionArgs) {
           int count = 0;
           if (uriMatcher.match(uri) == USER_INFO) { // 匹配到了用户信息表
               // 获取SQLite数据库的写连接
               SQLiteDatabase db = userDB.getWritableDatabase();
               // 执行SQLite的删除操作，并返回删除记录的数目
               count = db.delete(UserInfoContent.TABLE_NAME, selection, selectionArgs);
               db.close(); // 关闭SQLite数据库连接
           }
           return count;
       }
   
       // 根据指定条件查询数据库
       @Override
       public Cursor query(Uri uri, String[] projection, String selection,
                           String[] selectionArgs, String sortOrder) {
           Cursor cursor = null;
           if (uriMatcher.match(uri) == USER_INFO) { // 匹配到了用户信息表
               // 获取SQLite数据库的读连接
               SQLiteDatabase db = userDB.getReadableDatabase();
               // 执行SQLite的查询操作
               cursor = db.query(UserInfoContent.TABLE_NAME,
                       projection, selection, selectionArgs, null, null, sortOrder);
               // 设置内容解析器的监听
               cursor.setNotificationUri(getContext().getContentResolver(), uri);
           }
           return cursor; // 返回查询结果集的游标
       }
   
       // 获取Uri支持的数据类型，暂未实现
       @Override
       public String getType(Uri uri) {
           throw new UnsupportedOperationException("Not yet implemented");
       }
   
       // 更新数据，暂未实现
       @Override
       public int update(Uri uri, ContentValues values, String selection, String[] selectionArgs) {
           throw new UnsupportedOperationException("Not yet implemented");
       }
   }
   ```

### 通过ContentResolver访问数据

如果客户端App想访问对方的内部数据，就要借助内容解析器ContentResolver。内容解析器是客户端App操作服务端数据的工具，与之对应的内容提供器则是服务端的数据接口。在活动代码中调用getContentResolver方法，即可获取内容解析器的实例。ContentResolver提供的方法与ContentProvider一一对应，比如insert、delete、query、update、getType等，甚至连方法的参数类型都雷同

首先需要借助ContentValues存储ContentResolver可以处理的一组值，然后调用insert方法，使之往内容提供器插入一条用户信息

```java
// 添加一条用户记录
private void addUser(UserInfo user){
    ContentValues name = new ContentValues();
    name.put("name",user.name);
    name.put("age",user.age);
    name.put("height",user.height);
    name.put("weight",user.weight);
    name.put("married",0);
    // 通过内容解析器往指定Uri添加用户信息
    getContentResolver().insert(UserInfoContent.CONTENT_URI,name);
    Toast.makeText(this, "添加成功", Toast.LENGTH_SHORT).show();
}
```

删除

```java
private void deleteAllUser() {
    getContentResolver().delete(UserInfoContent.CONTENT_URI,"1=1",null);
    Toast.makeText(this, "删除成功", Toast.LENGTH_SHORT).show();
}
```

查询操作调用query方法会返回游标对象，这个游标正是SQLite的游标Cursor，query方法的输入参数有好几个，具体说明如下：

- uri：Uri类型，指定本次操作的数据表路径

- projection：字符串数组类型，指定将要查询的字段名称列表

- selection：字符串类型，指定查询条件

- selectionArgs：字符串数组类型，指定查询条件中的参数取值列表

- sortOrder：字符串类型，指定排序条件

```java
@SuppressLint("Range")
private void showAllUser(){ // 显示所有的用户记录
    int index = 0;
    List<UserInfo> userList = new ArrayList<>();
    // 通过内容解析器从指定Uri中获取用户记录的游标
    Cursor cursor = getContentResolver().query(
            UserInfoContent.CONTENT_URI, null, null, null, null);
    // 循环取出游标指向的每条用户记录
    while (cursor.moveToNext()){
        UserInfo user = new UserInfo();
        user.id = cursor.getInt(cursor.getColumnIndex(UserInfoContent._ID));
        user.name = cursor.getString(cursor.getColumnIndex(UserInfoContent.USER_NAME));
        user.age = cursor.getInt(cursor.getColumnIndex(UserInfoContent.USER_AGE));
        user.height = cursor.getInt(cursor.getColumnIndex(UserInfoContent.USER_HEIGHT));
        user.weight = cursor.getFloat(cursor.getColumnIndex(UserInfoContent.USER_WEIGHT));
        Log.d(TAG, user.toString());
        Toast.makeText(this, "查询成功", Toast.LENGTH_SHORT).show();
    }
    cursor.close(); // 关闭数据库游标
}
```



## 使用内容组件获取通讯信息

### 运行时动态申请权限

推荐文章：[Android开发学习日记--运行时动态申请应用权限](https://blog.csdn.net/m0_52238102/article/details/125947193)

申请权限，首先需要在Manifest注册

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

如果是Android6.0以上才用动态申请权限，步骤：

1. 检查APP是否开启了指定权限，调用ContextCompat的checkSelfPermission方法，该方法的第一个参数为活动实例，第二个参数为待检查的权限名称

   checkSelfPermission方法是有返回值的，返回PackageManager.PERMISSION_GRANTED表示已授权，返回PackageManager.PERMISSION_DENIED表示未授权

2. 请求系统弹窗，以便用户选择是否开启权限。调用ActivityCompat的requestPermissions方法，即可命令系统自动弹出权限申请窗口，该方法的第一个参数为活动实例，第二个参数为待申请的权限名称数组，第三个参数为本次操作的请求代码

3. 判断用户的权限选择结果。回调方法onRequestPermissionsResult，如果当前页面请求弹出权限申请窗口，那么该Activity页面的Java代码必须重写onRequestPermissionsResult方法，并在该方法内部处理用户的权限选择结果

运行时动态申请权限的工具类：

```java
public class PermissionUtil {
    private final static String TAG = "PermissionUtil";

    // 检查某个权限。返回true表示已启用该权限，返回false表示未启用该权限
    public static boolean checkPermission(Activity act, String permission, int requestCode) {
        return checkPermission(act, new String[]{permission}, requestCode);
    }

    // 检查多个权限。返回true表示已完全启用权限，返回false表示未完全启用权限
    public static boolean checkPermission(Activity act, String[] permissions, int requestCode) {
        boolean result = true;
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            int check = PackageManager.PERMISSION_GRANTED;
            // 通过权限数组检查是否都开启了这些权限
            for (String permission : permissions) {
                check = ContextCompat.checkSelfPermission(act, permission);// 检查权限是否开启
                if (check != PackageManager.PERMISSION_GRANTED) {
                    break; // 有个权限没有开启，就跳出循环
                }
            }
            if (check != PackageManager.PERMISSION_GRANTED) {
                // 未开启该权限，则请求系统弹窗，好让用户选择是否立即开启权限
                ActivityCompat.requestPermissions(act, permissions, requestCode);
                result = false;
            }
        }
        return result;
    }

    // 检查权限结果数组，返回true表示都已经获得授权。返回false表示至少有一个未获得授权
    public static boolean checkGrant(int[] grantResults) {
        boolean result = true;
        if (grantResults != null) {
            for (int grant : grantResults) { // 遍历权限结果数组中的每条选择结果
                if (grant != PackageManager.PERMISSION_GRANTED) { // 未获得授权
                    result = false;
                }
            }
        } else {
            result = false;
        }
        return result;
    }
}
```

Activity页面：

```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        findViewById(R.id.btn_file_write).setOnClickListener(this);
        findViewById(R.id.btn_file_read).setOnClickListener(this);

    }
    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.btn_file_write){ // 申请写存储卡权限
            if (PermissionUtil.checkPermission(this,
                    Manifest.permission.WRITE_EXTERNAL_STORAGE,R.id.btn_file_write % 65536)){
                Toast.makeText(this, "允许", Toast.LENGTH_SHORT).show();
            }
        } else if (v.getId() == R.id.btn_file_read) { // 申请读存储卡权限
            if (PermissionUtil.checkPermission(this,
                    Manifest.permission.READ_EXTERNAL_STORAGE,R.id.btn_file_read % 65536)){
                Toast.makeText(this, "允许", Toast.LENGTH_SHORT).show();
            }
        }
    }
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        // requestCode不能为负数，也不能大于2的16次方即65536
        if (requestCode == R.id.btn_file_write % 65536){
            if (PermissionUtil.checkGrant(grantResults)){ // 用户同意授权
                Toast.makeText(this, "允许", Toast.LENGTH_SHORT).show();
            }else {
                Toast.makeText(this, "没有允许", Toast.LENGTH_SHORT).show();
            }
        } else if (requestCode == R.id.btn_file_read % 65536) {
            if (PermissionUtil.checkGrant(grantResults)){
                Toast.makeText(this, "允许", Toast.LENGTH_SHORT).show();
            }else {
                Toast.makeText(this, "没有允许", Toast.LENGTH_SHORT).show();
            }
        }
    }
}
```

- Android10以上默认开启沙箱模式，不允许直接使用公共空间的文件路径，所以要修改AndroidManifest.xml，给application添加`android:requestLegacyExternalStorage="true"`属性

- 从Android11开始，为了让应用在升级时也能正常访问公共空间，还得修改AndroidManifest.xml，给application添加`android:preserveLegacyExternalStorage="true"`属性，表示暂时关闭沙箱模式

**权限名称的取值说明：**

| 代码中的权限名称                           | 权限说明   |
| ------------------------------------------ | ---------- |
| Manifest.permission.READ_EXTERNAL_STORAGE  | 读存储卡   |
| Manifest.permission.WRITE_EXTERNAL_STORAGE | 写存储卡   |
| Manifest.permission.READ_CONTACTS          | 读联系人   |
| Manifest.permission.WRITE_CONTACTS         | 写联系人   |
| Manifest.permission.SEND_SMS               | 发送短信   |
| Manifest.permission.RECEIVER_SMS           | 接收短信   |
| Manifest.permission.READ_SMS               | 读短信     |
| Manifest.permission.READ_CALL_LOG          | 读通话记录 |
| Manifest.permission.WRITE_CALL_LOG         | 写通话记录 |
| Manifest.permission.CAMERA                 | 相机       |
| Manifest.permission.RECORD_AUDIO           | 录音       |
| Manifest.permission.ACCESS_FINE_LOCATION   | 精确定位   |

### 利用ContentResolver读写联系人

访问系统的通讯数据之前，得先在AndroidManifest.xml添加相应的权限配置，常见的通讯权限配置主要有下面几个：

```xml
<!-- 联系人/通讯录。包括读联系人、写联系人 -->
<uses-permission android:name="android.permission.READ_CONTACTS"/>
<uses-permission android:name="android.permission.WRITE_CONTACTS"/>
<!-- 短信。包括发送短信、接收短信、读短信-->
<uses-permission android:name="android.permission.SEND_SMS"/>
<uses-permission android:name="android.permission.RECEIVE_SMS"/>
<uses-permission android:name="android.permission.READ_SMS"/>
<!-- 通话记录。包括读通话记录、写通话记录 -->
<uses-permission android:name="android.permission.READ_CALL_LOG"/>
<uses-permission android:name="android.permission.WRITE_CALL_LOG"/>
```

尽管系统允许App通过内容解析器修改联系人列表，但操作过程比较烦琐，因为一个联系人可能有多个电话号码，还可能有多个邮箱，所以系统通讯录将其设计为3张表，分别是联系人基本信息表、联系号码表、联系邮箱表，于是每添加一位联系人，就要调用至少三次insert方法

- raw_contacts表

  <img src="https://pb.nichi.co/gallery-agree-develop"  /> 

- data表

  记录了用户的通讯录所有数据，包括手机号，显示名称等，但是里面的mimetype_id表示不同的数据类型，这与表mimetypes表中的*id*相对应，raw_contact_id 与下面的 raw_contacts表中的 id 相对应

  ![](https://pb.nichi.co/typical-present-trap) 

- mimetypes表

  ![](https://pb.nichi.co/journey-track-novel) 

**添加步骤：**

1. 往raw_contacts表中添加联系人，获取联系人编号

2. 往data表中插入信息，分别插入姓名、电话、邮箱，插入步骤：

   1. 创建一个配对`ContentValues name = new ContentValues();`

   2. 往配对中加入信息，分别加入raw_contacts表中的编号、数据类型、姓名（或电话邮箱）、联系类型（电话，邮箱专属）

      ```java
      name.put(ContactsContract.Contacts.Data.RAW_CONTACT_ID, contactId); // 往配对中添加联系人编号
      // 往配对中添加“姓名”的数据类型
      name.put(ContactsContract.Contacts.Data.MIMETYPE,ContactsContract.CommonDataKinds.StructuredName.CONTENT_ITEM_TYPE);
      name.put(ContactsContract.Contacts.Data.DATA2,contact.name); // 往配对中添加联系人的姓名
      ```

   3. 通过ContentResolver来插入信息`resolver.insert(ContactsContract.Data.CONTENT_URI,name);`

```java
// 往手机通讯录添加一个联系人（包括姓名、电话号码、电子邮箱）
public static void addContacts(ContentResolver resolver, Contact contact) {
/*        // 构建一个指向系统联系人提供器的Uri
    Uri raw_uri = Uri.parse("content://com.android.contacts/raw_contacts"); // 也就是ContactsContract.RawContacts.CONTENT_URI*/
    ContentValues values = new ContentValues(); // 创建新的配对
    Uri insert = resolver.insert(ContactsContract.RawContacts.CONTENT_URI, values); // 往raw_contacts中添加联系人记录
    long contactId = ContentUris.parseId(insert); // 获取联系人的编号

/*        // 构建一个指向系统联系人的Uri对象
    Uri uri = Uri.parse("content://com.android.contacts/data"); // ContactsContract.Data.CONTENT_URI*/
    Uri uri = ContactsContract.Data.CONTENT_URI; // 指向系统联系人的Uri

    ContentValues name = new ContentValues(); // 创建新的配对
    // 往配对中添加联系人编号
    name.put(ContactsContract.Contacts.Data.RAW_CONTACT_ID, contactId); // ContactsContract.Contacts.Data.RAW_CONTACT_ID = "raw_contact_id"
    // 往配对中添加“姓名”的数据类型
    name.put(ContactsContract.Contacts.Data.MIMETYPE,ContactsContract.CommonDataKinds.StructuredName.CONTENT_ITEM_TYPE);
    name.put(ContactsContract.Contacts.Data.DATA2,contact.name); // 往配对中添加联系人的姓名
    resolver.insert(uri,name); // 往提供器中添加联系人的姓名记录

    ContentValues phone = new ContentValues(); // 创建新的配对
    phone.put(ContactsContract.Contacts.Data.RAW_CONTACT_ID,contactId); // 往配对中添加联系人编号
    // 往配对中添加“电话号码”的数据类型
    phone.put(ContactsContract.Contacts.Data.MIMETYPE,ContactsContract.CommonDataKinds.Phone.CONTENT_ITEM_TYPE);
    phone.put(ContactsContract.Contacts.Data.DATA1,contact.phone); // 往配对中添加联系人的电话号码
    phone.put(ContactsContract.Contacts.Data.DATA2,ContactsContract.CommonDataKinds.Phone.TYPE_MOBILE); // 联系类型，1表示家庭，2表示手机，3表示工作
    resolver.insert(uri,phone); // 往提供器中添加联系人的电话号码记录

    ContentValues email = new ContentValues(); // 创建新的配对
    email.put(ContactsContract.Contacts.Data.RAW_CONTACT_ID,contactId); // 往配对中添加联系人编号
    // 往配对中添加“邮箱”的数据类型
    email.put(ContactsContract.Contacts.Data.MIMETYPE,ContactsContract.CommonDataKinds.Email.CONTENT_ITEM_TYPE);
    email.put(ContactsContract.Contacts.Data.DATA1,contact.email); // 往配对中添加联系人的邮箱
    email.put(ContactsContract.Contacts.Data.DATA2,ContactsContract.CommonDataKinds.Email.TYPE_WORK); // 联系类型，1表示家庭，2表示工作
    resolver.insert(uri,email); // 往提供器中添加联系人的邮箱记录

}
```

**批量添加联系人：**

- 每一次操作都是一个 ContentProviderOperation，构建一个操作集合，然后一次性执行
- 好处是，要么全部成功，要么全部失败，保证了事务的一致性

```java
// 往手机通讯录一次性添加一个联系人信息（包括主记录、姓名、电话号码、电子邮箱）
public static void addFullContacts(ContentResolver resolver, Contact contact){
    // 创建一个插入联系人主记录的内容操作器
    ContentProviderOperation op_main = ContentProviderOperation
            .newInsert(ContactsContract.RawContacts.CONTENT_URI)
            .withValue(ContactsContract.RawContacts.ACCOUNT_NAME,null)
            .build();

    // 创建一个插入联系人姓名记录的内容操作器
    ContentProviderOperation op_name = ContentProviderOperation
            .newInsert(ContactsContract.Data.CONTENT_URI)
            .withValueBackReference(ContactsContract.Contacts.Data.RAW_CONTACT_ID,0)
            .withValue(ContactsContract.Contacts.Data.MIMETYPE,ContactsContract.CommonDataKinds.StructuredName.CONTENT_ITEM_TYPE)
            .withValue(ContactsContract.Contacts.Data.DATA2,contact.name)
            .build();

    // 创建一个插入联系人电话记录的内容操作器
    ContentProviderOperation op_phone = ContentProviderOperation
            .newInsert(ContactsContract.Data.CONTENT_URI)
            .withValueBackReference(ContactsContract.Contacts.Data.RAW_CONTACT_ID,0)
            .withValue(ContactsContract.Contacts.Data.MIMETYPE,ContactsContract.CommonDataKinds.Phone.CONTENT_ITEM_TYPE)
            .withValue(ContactsContract.Contacts.Data.DATA1,contact.phone)
            .withValue(ContactsContract.Contacts.Data.DATA2,ContactsContract.CommonDataKinds.Phone.TYPE_MOBILE)
            .build();

    // 创建一个插入联系人邮箱记录的内容操作器
    ContentProviderOperation op_email = ContentProviderOperation
            .newInsert(ContactsContract.Data.CONTENT_URI)
            .withValueBackReference(ContactsContract.Contacts.Data.RAW_CONTACT_ID,0)
            .withValue(ContactsContract.Contacts.Data.MIMETYPE,ContactsContract.CommonDataKinds.Email.CONTENT_ITEM_TYPE)
            .withValue(ContactsContract.Contacts.Data.DATA1,contact.email)
            .withValue(ContactsContract.Contacts.Data.DATA2,ContactsContract.CommonDataKinds.Phone.TYPE_MOBILE)
            .build();
    // 声明一个内容操作器的列表，并将上面四个操作器添加到该列表中
    ArrayList<ContentProviderOperation> operations = new ArrayList<>();
    operations.add(op_main);
    operations.add(op_name);
    operations.add(op_phone);
    operations.add(op_email);

    try {
        // 批量提交四个操作
        resolver.applyBatch(ContactsContract.AUTHORITY,operations);
    } catch (OperationApplicationException e) {
        throw new RuntimeException(e);
    } catch (RemoteException e) {
        throw new RuntimeException(e);
    }

}
```

**查询步骤：**

- 先查询 raw_contacts 表，会返回一个游标，然后遍历游标，先获取id，然后根据 raw_contacts_id 去查询 data 表
- 遍历data表，根据mimetype取出数据

```java
@SuppressLint("Range")
public static ArrayList<Contact> readPhoneContacts(ContentResolver resolver){
    // 先查询 raw_contacts 表，在根据 raw_contacts_id 去查询 data 表
    Cursor cursor = resolver.query(ContactsContract.RawContacts.CONTENT_URI,
            new String[]{ContactsContract.RawContacts._ID}, null, null, null);
    ArrayList<Contact> contactList = new ArrayList<>();
    while (cursor.moveToNext()){
        int rawContactId = cursor.getInt(0);
        Uri uri = Uri.parse("content://com.android.contacts/contacts/" + rawContactId + "/data");
        Cursor dataCursor = resolver.query(uri,new String[]{ContactsContract.Contacts.Data.MIMETYPE, 
                ContactsContract.Contacts.Data.DATA1,ContactsContract.Contacts.Data.DATA2}, null, null, null);
        Contact contact = new Contact();
        while (dataCursor.moveToNext()){
            String type = dataCursor.getString(dataCursor.getColumnIndex(ContactsContract.Contacts.Data.MIMETYPE));
            String data = dataCursor.getString(dataCursor.getColumnIndex(ContactsContract.Contacts.Data.DATA1));
            switch (type){
                case ContactsContract.CommonDataKinds.StructuredName.CONTENT_ITEM_TYPE:
                    contact.name = data;
                    break;
                case ContactsContract.CommonDataKinds.Phone.CONTENT_ITEM_TYPE:
                    contact.phone = data;
                    break;
                case ContactsContract.CommonDataKinds.Email.CONTENT_ITEM_TYPE:
                    contact.email = data;
                    break;
            }
        }
        dataCursor.close();
        contactList.add(contact);
    }
    return contactList;
}
```

### 利用ContentObserver监听短信

**内容观察器：**

- 想要实时获取用户数据，就需要使用内容观察器ContentObserver
- 内容观察器和内容提供器用法类似，要先从ContentObserver派生一个新的观察器，通过ContentResolver对象调用相应的方法注册或注销观察器
  - registerContentObserver：内容解析器要注册内容观察器
  - unregisterContentObserver：内容解析器要注销内容观察器
  - notifyChange：通知内容观察器发生了数据变化，此时会触发观察器的onChange方法

**通过内容观察器监听短信：**

1. 创建一个从ContentObserver派生的类，重写回调方法onChange，补充其中代码逻辑
2. 在onCreate中注册内容观察器，在onDestroy中注销内容观察器

```java
public class MonitorSmsActivity extends AppCompatActivity {
    private Handler mHandler = new Handler(); // 声明一个处理器对象
    private SmsGetObserver mObserver;
    private static TextView tv_result;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_monitor_sms);
        tv_result = findViewById(R.id.tv_result);
        // 给指定Uri注册内容观察器，一旦发生数据变化，就触发观察器的onChange方法
        Uri uri = Uri.parse("content://sms");
        // notifyForDescendants：
        // 第二个参数为false：表示精确匹配，即只匹配该Uri，为true：表示可以同时匹配其派生的Uri
        // 假设UriMatcher 里注册的Uri共有一下类型：
        // 1.content://AUTHORITIES/table
        // 2.content://AUTHORITIES/table/#
        // 3.content://AUTHORITIES/table/subtable
        // 假设我们当前需要观察的Uri为content://AUTHORITIES/student:
        // 如果发生数据变化的 Uri 为 3
        // 当notifyForDescendants为false，那么该ContentObserver会监听不到，但是当notifyForDescendants 为ture，能捕捉该Uri的数据库变化。
        mObserver = new SmsGetObserver(this, mHandler);
        // 给指定的Uri注册内容观察器，一旦数据发送变化，就会触发观察器的onChange方法
        getContentResolver().registerContentObserver(Telephony.Sms.CONTENT_URI, true, mObserver);
    }
    @Override
    protected void onDestroy() {
        super.onDestroy();
        getContentResolver().unregisterContentObserver(mObserver); // 注销内容观察器
    }
    private static class SmsGetObserver extends ContentObserver {
        private Context mContext;
        public SmsGetObserver(Context context, Handler handler) {
            super(handler);
            mContext = context;
        }

        @SuppressLint("Range")
        @Override
        public void onChange(boolean selfChange, @Nullable Uri uri) {
            super.onChange(selfChange, uri);
            // onChange会多次调用，收到一条短信会调用两次onChange
            // mUri===content://sms/raw/20
            // mUri===content://sms/inbox/20
            // 安卓7.0以上系统，点击标记为已读，也会调用一次
            // mUri===content://sms
            // 收到一条短信都是uri后面都会有确定的一个数字，对应数据库的_id，比如上面的20
            if (uri == null) {
                return;
            }
            if (uri.toString().contains("content://sms/raw") || uri.toString().equals("content://sms")) {
                return;
            }
            // 通过内容解析器获取符合条件的结果集游标
            Cursor cursor = mContext.getContentResolver().query(uri, new String[]{"address", "body", "date"}, null, null, " date desc");
            if (cursor.moveToNext()) {
                // 短信的发送号码
                String sender = cursor.getString(cursor.getColumnIndex("address"));
                // 短信内容
                String content = cursor.getString(cursor.getColumnIndex("body"));
                tv_result.setText(String.format("sender:%s,content:%s", sender, content));
            }
            cursor.close();
        }
    }
}
```

## 在应用之间共享文件

### 使用相册图片发送彩信

- 想要从相册选取图片，就要调用Intent.ACTION_GET_CONTENT隐式意图
- 然后注册返回活动结果registerForActivityResult，如果result.getResultCode() == RESULT_OK，表明选择了图片，然后通过result.getData().getData()就可以获取图片的Uri
- 跳转到相册选择图片

```java
// 注册一个善后工作的活动结果启动器，获取指定类型的内容
ActivityResultLauncher<String> resultLauncher = registerForActivityResult(new ActivityResultContracts.GetContent(), uri -> {
    if (uri != null) {
        // 根据指定图片的Uri，获得自动缩小后的位图对象
        Bitmap bitmap = BitmapUtil.getAutoZoomImage(PhotoImageActivity.this, uri);
        iv_chose_image.setImageBitmap(bitmap); // 设置图像视图的位图对象
        //iv_chose_image.setImageURI(uri);
    }
});
// 点击按钮时触发活动结果启动器，传入待获得内容的文件类型
findViewById(R.id.btn_chose_image_plus).setOnClickListener(v -> resultLauncher.launch("image/*"));
```

完整代码：


```java
public class SendMmsActivity extends AppCompatActivity implements View.OnClickListener {
    private ImageView iv_appendix;
    private ActivityResultLauncher<Intent> mResultLauncher;
    private EditText et_phone;
    private EditText et_title;
    private EditText et_message;
    private Uri picUri;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_send_mms);
        et_phone = findViewById(R.id.et_phone);
        et_title = findViewById(R.id.et_title);
        et_message = findViewById(R.id.et_message);
        iv_appendix = findViewById(R.id.iv_appendix);
        iv_appendix.setOnClickListener(this);
        findViewById(R.id.btn_send_mms).setOnClickListener(this);
        mResultLauncher = registerForActivityResult(new ActivityResultContracts.StartActivityForResult(), new ActivityResultCallback<ActivityResult>() {
            @Override
            public void onActivityResult(ActivityResult result) {
                if (result.getResultCode() == RESULT_OK){ // 从相册选择了一张照片
                    Intent intent = result.getData();
                    // 获得选中图片的路径对象
                    picUri = intent.getData();
                    if (picUri != null){ // 数据非空，表示选中了某张照片
                        // ImageView 显示刚刚选中的图片
                        iv_appendix.setImageURI(picUri);
                    }
                }
            }
        });
    }
    @Override
    public void onClick(View v) {
        if (v.getId() == R.id.iv_appendix){
            // 跳转到系统相册，选择图片，并返回
            Intent intent = new Intent(Intent.ACTION_GET_CONTENT);
            // 设置内容类型为图片类型
            intent.setType("image/*");
            // 打开系统相册，并等待图片选择结果
            mResultLauncher.launch(intent);
        }else if (v.getId() == R.id.btn_send_mms){
            // 发送带图片的彩信
            sendMms(et_phone.getText().toString(),
                    et_title.getText().toString(),
                    et_message.getText().toString());
        }
    }
    private void sendMms(String phone, String title, String message) {
        Intent intent = new Intent(Intent.ACTION_SEND);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        // Intent 的接受者将被准许读取Intent携带的Uri数据
        intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
        // 彩信发送的目标号码
        intent.putExtra("address",phone);
        // 彩信的标题
        intent.putExtra("subject",title);
        // 彩信的内容
        intent.putExtra("sms_body",message);
        // 彩信的图片附件
        intent.putExtra(Intent.EXTRA_STREAM,picUri);
        // 彩信的附件类型
        intent.setType("image/*");
        // 因为未指定要打开哪个页面，所以系统会在底部弹出选择窗口
        startActivity(intent);
        Toast.makeText(this, "请在弹窗中选择短信或者信息应用", Toast.LENGTH_SHORT).show();
    }
}
```



# 高级控件

## 下拉列表

### 下拉框Spinner

- 有两种模式，一种下拉模式（dropdown），一种对话框模式（dialog），设置`android:spinnerMode`属性可以修改

  ```xml
  <Spinner
      android:id="@+id/sp_dropdown"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:spinnerMode="dropdown" />
  ```

- 在Java代码中，Spinner还可以调用下列4个方法

  - setPrompt：设置标题文字。注意对话框模式才显示标题，下拉模式不显示标题
  - setAdapter：设置列表项的数据适配器
  - setSelection：设置当前选中哪项。注意该方法要在setAdapter方法后调用
  - setOnItemSelectedListener：设置下拉列表的选择监听器，该监听器要实现接口OnItemSelectedListener

  使用步骤：

  1. 创建一个集合来存储要展示的文字

  2. 创建一个数组适配器ArrayAdapter，第一个参数传入上下文，第二个参数传入布局，可为android.R.layout.simple_list_item_1（这是一个

     Android 内置的布局文件，里面只有一个TextView ，可用于简单地显示一段文本），第三个参数传入数组

  3. 调用下拉框的setPrompt方法，传入数组适配器

  4. 调用下拉框的setOnItemSelectedListener方法，设置点击事件监听，重写onItemSelected（选中之后执行）和onNothingSelected（什么也没选），补充逻辑

  ```kotlin
  class SpinnerDialogActivity : AppCompatActivity(), AdapterView.OnItemSelectedListener {
      
      private val startArray = listOf("水星", "金星", "地球", "火星", "木星", "土星")
  
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_spinner_dialog)
  
          // 声明一个下拉列表的数组适配器
          val adapter = ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, startArray)
          // 初始化下拉框
          findViewById<Spinner>(R.id.sp_dialog).apply {
              // 设置下拉框的标题。对话框模式才显示标题，下拉模式不显示标题
              prompt = "请选择行星"
              // 设置下拉框的数组适配器
              setAdapter(adapter)
              // 下拉列表默认显示第一项
              setSelection(0)
              // 给下拉框设置选择监听器，一旦用户选中某一项，就触发监听器的onItemSelected方法
              onItemSelectedListener = this
          }
      }
  
      // 选中之后执行
      override fun onItemSelected(parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
          ToastUtil.show(this, "您选择的是${startArray[position]}")
      }
  
      // 什么也没选
      override fun onNothingSelected(parent: AdapterView<*>?) {
  
      }
  }
  ```

### 数组适配器ArrayAdapter

- 最简单的适配器，只展示一行文字

- 运用数组适配器分成下列步骤：
  - 编写列表项的XML文件，内部布局只有一个TextView标签
  - 调用ArrayAdapter的构造方法，填入待展现的字符串数组，以及列表项的XML文件（R.layout.item_select）
  - 调用下拉框控件的setAdapter方法，传入第二步得到的适配器实例

### 简单适配器SimpleAdapter

- SimpleAdapter 允许在列表项中同时展示文本与图片

- 集合当中的数据与条目布局的对应关系

  <img src="https://image.cgz233.cn/images/202302212130252.png" alt="image-20230221213029898" style="zoom: 67%;" /> 

- 使用步骤：

  1. 分别创建图片和名称集合
  2. 创建`List<? extends Map<String, ?>>`形式的集合，遍历图片和名称集合，将参数放入
  3. 创建SimpleAdapter，SimpleAdapter的第一个参数为上下文，第二个参数为`List<? extends Map<String, ?>>`形式的集合，第三个参数为布局，第四个参数为集合第一个String的值，第五个参数为布局参数对应第四个参数id
  4. 设置下拉框的adapter为刚创建的SimpleAdapter

  ```kotlin
  class SpinnerIconActivity : AppCompatActivity(), AdapterView.OnItemSelectedListener {
  
      private val iconArray = listOf(
          R.drawable.shuixing, R.drawable.jinxing, R.drawable.diqiu,
          R.drawable.huoxing, R.drawable.muxing, R.drawable.tuxing
      )
  
      private val startArray = listOf("水星", "金星", "地球", "火星", "木星", "土星")
  
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_spinner_icon)
  
          initSpinnerForSimpleAdapter() // 初始化下拉框
      }
  
      private fun initSpinnerForSimpleAdapter() {
          // 声明一个映射对象的列表，用于保存行星的图标与名称配对信息
          val list = ArrayList<Map<String, Any>>()
          // 遍历数组，将数据添加到数组当中
          iconArray.forEachIndexed { index, i ->
              val map = mapOf("icon" to i, "name" to startArray[index])
              list.add(map) // 把行星图标与名称的配对映射添加到列表
          }
          // 声明一个下拉列表的简单适配器，其中指定了图标与文本两组数据
          val simpleAdapter = SimpleAdapter(
              this,
              list,
              R.layout.item_simple,
              arrayOf("icon", "name"),
              intArrayOf(R.id.iv_icon, R.id.tv_name)
          )
          // 初始化下拉框
          findViewById<Spinner>(R.id.sp_icon).apply {
              prompt = "请选择行星" // 设置下拉框的标题
              adapter = simpleAdapter // 设置下拉框的简单适配器
              setSelection(0) // 设置默认选择第一个
              onItemSelectedListener = this@SpinnerIconActivity // 设置监听
          }
      }
      override fun onItemSelected(parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
          ToastUtil.show(this, "您选择的是${startArray[position]}")
      }
      override fun onNothingSelected(parent: AdapterView<*>?) {
      }
  }
  ```

## 列表类视图

### 基本适配器BaseAdapter

- Android提供了一种适应性更强的基本适配器BaseAdapter，它允许开发者在别的代码文件中进行逻辑处理

- 条目与数据集合对应关系

  <img src="https://image.cgz233.cn/images/202302222307614.png" alt="image-20230222230707085" style="zoom:67%;" /> 

- 从BaseAdapter派生的数据适配器主要实现下面5个方法

  - 构造函数：指定适配器需要处理的数据集合
  - getCount：获取数据项的个数
  - getItem：获取列表项的数据
  - getItemId：获取列表项的编号
  - getView：获取每项的展示视图，并操纵每项的内部控件

实现步骤：

- 数据类

  ```kotlin
  class Planet(val image: Int, val name: String, val desc: String) { // 行星图片、名称、描述
  
      companion object {
          private val iconArray = arrayOf(
              R.drawable.shuixing, R.drawable.jinxing, R.drawable.diqiu,
              R.drawable.huoxing, R.drawable.muxing, R.drawable.tuxing
          )
  
          private val nameArray = arrayOf("水星", "金星", "地球", "火星", "木星", "土星")
  
          private val descArray = arrayOf(
              "水星是太阳系八大行星最内侧也是最小的一颗行星，也是离太阳最近的行星",
              "金星是太阳系八大行星之一，排行第二，距离太阳0.725天文单位",
              "地球是太阳系八大行星之一，排行第三，也是太阳系中直径、质量和密度最大的类地行星，距离太阳1.5亿公里",
              "火星是太阳系八大行星之一，排行第四，属于类地行星，直径约为地球的53%",
              "木星是太阳系八大行星中体积最大、自转最快的行星，排行第五。它的质量为太阳的千分之一，但为太阳系中其它七大行星质量总和的2.5倍",
              "土星为太阳系八大行星之一，排行第六，体积仅次于木星"
          )
  
          fun getDefaultList(): List<Planet> {
              val planetList = arrayListOf<Planet>()
              for (i in iconArray.indices) {
                  planetList.add(Planet(iconArray[i], nameArray[i], descArray[i]))
              }
              return planetList
          }
      }
  
  }
  ```

1. 编写列表项的布局文件item_list.xml

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:orientation="horizontal">
       <ImageView
           android:id="@+id/iv_icon"
           android:layout_width="0dp"
           android:layout_height="80dp"
           android:layout_weight="1"
           android:scaleType="fitCenter"
           tools:src="@drawable/diqiu"/>
       <LinearLayout
           android:layout_width="0dp"
           android:layout_height="match_parent"
           android:layout_marginLeft="5dp"
           android:layout_weight="3"
           android:orientation="vertical">
           <TextView
               android:id="@+id/tv_name"
           android:layout_width="match_parent"
           android:layout_height="0dp"
           android:layout_weight="1"
           android:gravity="start|center"
           android:textColor="@color/black"
           android:textSize="20dp"
           tools:text="地球"/>
   
           <TextView
               android:id="@+id/tv_desc"
               android:layout_width="match_parent"
               android:layout_height="0dp"
               android:layout_weight="2"
               android:gravity="start|center"
               android:textColor="@color/black"
               android:textSize="13sp"
               tools:text="地球是太阳系八大行星之一，排行第三，也是太阳系中直径、质量和密度最大的类地行星，距离太阳1.5亿公里"/>
       </LinearLayout>
   </LinearLayout>
   ```

2. 写个新的适配器继承BaseAdapter，实现对列表项的管理操作。需要编写适配器的三个方法：

   1. 创建构造方法，传入列表项需要的数据列表
   2. 重写getCount方法，返回列表项的个数
   3. 重写getView方法，根据item_list.xml里面的布局，返回指定位置的列表项的视图内容

   ```kotlin
   class PlanetBaseAdapter(private val mContext: Context, private val mPlanetList: List<Planet>) :
       BaseAdapter() {
       // 获取列表项的个数
       override fun getCount(): Int {
           return mPlanetList.size
       }
   
       override fun getItem(position: Int): Any {
           return mPlanetList[position]
       }
   
       override fun getItemId(position: Int): Long {
           return position.toLong()
       }
   
       override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View? {
   
           var convertView = convertView
           val holder: ViewHolder
           if (convertView == null) { // 转换视图为空
               // 根据布局文件item_list.xml生成转换视图对象
               convertView = LayoutInflater.from(mContext).inflate(R.layout.item_list, null)
               holder = ViewHolder() // 创建一个新的视图持有者
               holder.iv_icon = convertView.findViewById(R.id.iv_icon)
               holder.tv_name = convertView.findViewById(R.id.tv_name)
               holder.tv_desc = convertView.findViewById(R.id.tv_desc)
               // 将视图持有者保存到转换视图当中
               convertView.tag = holder
           } else {  // 转换视图非空
               holder = convertView.tag as ViewHolder // 从转换视图中获取之前保存的视图持有者
           }
   
           // 给控制设置好数据
           val planet = mPlanetList[position]
           holder.iv_icon.setImageResource(planet.image)
           holder.tv_name.text = planet.name
           holder.tv_desc.text = planet.desc
           holder.iv_icon.requestFocus()
           return convertView
       }
   
       class ViewHolder {
           lateinit var iv_icon: ImageView
           lateinit var tv_name: TextView
           lateinit var tv_desc: TextView
       }
   }
   ```

3. 在页面代码中创建该适配器实例，并交给下拉框设置适配器

   ```kotlin
   class BaseAdapterActivity : AppCompatActivity(), AdapterView.OnItemSelectedListener {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_base_adapter)
           // 构建一个行星列表的适配器
           val baseAdapter = PlanetBaseAdapter(this, Planet.getDefaultList())
           // 从布局文件中获取名叫sp_planet的下拉框
           val sp_planet = findViewById<Spinner>(R.id.sp_planet)
           sp_planet.apply {
               prompt = "请选择行星" // 设置下拉框的标题
               adapter = baseAdapter // 设置下拉框的列表适配器
               setSelection(0) // 设置下拉框默认显示第一项
               onItemSelectedListener = this@BaseAdapterActivity // 给下拉框设置选择监听器
           }
   
       }
   
       override fun onItemSelected(parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
           ToastUtil.show(this, "你选择的是${Planet.getDefaultList()[position].name}")
       }
   
       override fun onNothingSelected(parent: AdapterView<*>?) {
           TODO("Not yet implemented")
       }
   }
   ```

### 列表视图ListVie

- ListView 允许在页面上分行展示数据列表

- 修改分隔线样式要在XML文件中同时设置divider与dividerHeight两个属性

- 若想取消按压列表项之时默认的水波背景，可在XML文件中设置也可在Java代码中设置

  | XML中的属性   | ListView类的设置方法 | 说明                                                    |
  | ------------- | -------------------- | ------------------------------------------------------- |
  | divider       | setDivider           | 指定分隔线的图形。如需取消分隔线，可将该属性值设为@null |
  | dividerHeight | setDividerHeight     | 指定分隔线的高度                                        |
  | listSelector  | setSelector          | 指定列表项的按压背景（状态图形格式）                    |

使用步骤：

1. 添加ListView布局

   ```xml
   <ListView
       android:id="@+id/lv_planet"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:divider="@null"
       android:dividerHeight="0dp"
       android:listSelector="@color/transparent"/>
   ```

2. 往视图内填充数据，先利用基本适配器实现列表适配器，然后调用setAdapter方法设置适配器对象，添加点击事件监听，补充其逻辑

   ```kotlin
   class ListViewActivity : AppCompatActivity(), AdapterView.OnItemClickListener,
       AdapterView.OnItemLongClickListener {
       @SuppressLint("UseCompatLoadingForDrawables")
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_list_view)
   
           // 创建适配器
           val baseAdapter = PlanetBaseAdapter(this, Planet.getDefaultList())
           findViewById<ListView>(R.id.lv_planet).apply {
               adapter = baseAdapter // 设置列表视图的适配器
               onItemClickListener = this@ListViewActivity // 设置点击事件监听
               onItemLongClickListener = this@ListViewActivity // 设置长按事件监听
           }
       }
   
       override fun onItemClick(parent: AdapterView<*>?, view: View?, position: Int, id: Long) {
           ToastUtil.show(this, "你点击了${Planet.getDefaultList()[position].name}")
       }
   
       override fun onItemLongClick(
           parent: AdapterView<*>?,
           view: View?,
           position: Int,
           id: Long
       ): Boolean {
           ToastUtil.show(this, "你长按了${Planet.getDefaultList()[position].name}")
           return true
       }
   }
   ```

修改列表视图的分割线样式：

- 修改分隔线样式要在XML文件中同时设置divider（分隔图片）与dividerHeight（分隔高度）两个属性
  - divider属性设置为@null时，不能再将dividerHeight属性设置为大于0的数值
  - 通过代码设置的话，务必先调用setDivider方法再调用setDividerHeight方法

```kotlin
if (isChecked) { // 显示分隔线
    val drawable = resources.getDrawable(R.color.black, theme) // 从资源文件获得图形对象
    lv_planet.divider = drawable // 设置列表视图的分隔线
    lv_planet.dividerHeight = Utils.dip2px(this, 0.5) // 设置列表视图的分隔线高度
} else { // 不显示分隔线
    lv_planet.divider = null // 设置列表视图的分隔线
    lv_planet.dividerHeight = 0  // 设置列表视图的分隔线高度
}
```

修改列表视图的按压背景：

- 在xml中设置取消按压背景

  ```xml
  android:listSelector="#00000000"
  ```

- 在代码中取消按压背景的话，调用setSelector方法不能设置null值，因为null值会在运行时报空指针异常。正确的做法是先从资源文件获得透明色的图形对象，再调用setSelector方法设置列表项的按压状态图形，设置按压背景的代码如下所示：

  ```kotlin
  if (isChecked) { // 显示按压背景
      val drawable = resources.getDrawable(R.drawable.list_selector, theme) // 从资源文件获得图形对象
      lv_planet.selector = drawable // 设置列表项的按压状态图形
  } else { // 隐藏按压背景
      val drawable = resources.getDrawable(R.color.transparent, theme) // 从资源文件获得图形对象
      lv_planet.selector = drawable // 设置列表项的按压状态图形
  }
  ```

注意：

1. 在XML文件中，如果ListView后面还有其他平级的控件，就要将ListView的高度设为0dp，同时权重设为1，确保列表视图扩展到剩余的页面区域；如果ListView的高度设置为wrap_content，系统就只给列表视图预留一行高度，如此一来只有列表的第一项会显示，其他项不显示，这显然不是我们所期望的。因此建议列表视图的尺寸参数按照如下方式设置：

   ```xml
   <ListView
       android:id="@+id/lv_planet"
       android:layout_width="match_parent"
       android:layout_height="0dp"
       android:layout_weight="1"/>
   ```

2. 通常只要调用setOnItemClickListener方法设置点击监听器，点击列表项即可触发列表项的点击事件，但是如果列表项中存在编辑框或按钮（含Button、ImageButton、Checkbox等），点击列表项就无法触发点击事件了。为了规避焦点抢占的问题，列表视图允许开发者自行设置内部视图的焦点抢占方式，该方式在XML文件中由descendantFocusability属性指定，在代码中由setDescendantFocusability方法设置

   列表视图的焦点抢占方式：

   | 抢占方式说明     | 代码中的焦点抢占类型              | XML文件中的抢占类型 |
   | ---------------- | --------------------------------- | ------------------- |
   | 在子控件之前处理 | ViewGroup.FOCUS_BEFOR_DESCENDANTS | beforDescendants    |
   | 在子控件之后处理 | ViewGroup.FOCUS_AFTER_DESCENDANTS | afterDescendants    |
   | 不让子控件处理   | ViewGroup.FOCUS_BLOCK_DESCENDANTS | blocksDescendants   |

   注意焦点抢占方式不是由ListView设置，而是由列表项的根布局设置，也就是item_***.xml的根节点

> 使用ArrayAdapter创建ListView

1. 在活动页面布局中加入ListView

   ```xml
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">
   
       <ListView
           android:id="@+id/lv_test"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"/>
   
   </LinearLayout>
   ```

2. 创建适配器对应的视图

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="match_parent"
       android:layout_height="130dp"
       android:orientation="horizontal">
   
       <ImageView
           android:id="@+id/iv_icon"
           android:layout_width="0dp"
           android:layout_height="match_parent"
           android:layout_weight="1"
           tools:src="@drawable/huawei" />
   
       <LinearLayout
           android:layout_width="0dp"
           android:layout_height="match_parent"
           android:layout_weight="2"
           android:orientation="vertical">
   
           <TextView
               android:id="@+id/tv_name"
               android:layout_width="match_parent"
               android:layout_height="0dp"
               android:layout_weight="1"
               android:gravity="center"
               android:textColor="@color/black"
               android:textSize="28sp"
               tools:text="Mate30" />
   
           <TextView
               android:id="@+id/tv_desc"
               android:layout_width="match_parent"
               android:layout_height="0dp"
               android:layout_weight="3"
               android:gravity="center"
               android:textColor="@color/black"
               android:textSize="17sp"
               tools:text="华为 HUAWEI Mate30 8GB+256GB 丹霞橙 5G全网通 全面屏手机" />
   
       </LinearLayout>
   
   </LinearLayout>
   ```

3. 创建适配器继承ArrayAdapter

   ```kotlin
   class ListTestAdapter(activity: Activity, val resourceId: Int, goodsList: List<GoodsInfo>) :
       ArrayAdapter<GoodsInfo>(activity, resourceId, goodsList) {
   
       inner class ViewHolder(
           val goodsImage: ImageView,
           val goodsName: TextView,
           val goodsDesc: TextView
       )
       
       override fun getView(position: Int, convertView: View?, parent: ViewGroup): View {
           val view: View
           val viewHolder: ViewHolder
           if (convertView == null) { // 如果没有加载过布局，创建新布局
               view = LayoutInflater.from(context).inflate(resourceId, parent, false)
               val goodsImage: ImageView = view.findViewById(R.id.iv_icon)
               val goodsName: TextView = view.findViewById(R.id.tv_name)
               val goodsDesc: TextView = view.findViewById(R.id.tv_desc)
               viewHolder = ViewHolder(goodsImage, goodsName, goodsDesc)
               view.tag = viewHolder
           } else { // 如果加载过布局，复用
               view = convertView
               viewHolder = view.tag as ViewHolder
           }
   
           val goods = getItem(position) // 获取当前商品实例
           if (goods != null) {
               viewHolder.goodsImage.setImageResource(goods.pic) // 设置商品图片
               viewHolder.goodsName.text = goods.name // 设置商品名称
               viewHolder.goodsDesc.text = goods.desc // 设置商品描述
           }
           return view
       }
   }
   ```

4. 在活动页面设置适配器

   ```kotlin
   class ListTestActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_list_test)
           findViewById<ListView>(R.id.lv_test).apply {
               adapter =
                   ListTestAdapter(this@ListTestActivity, R.layout.list_item, GoodsInfo.defaultList)
           }
       }
   }
   ```

### 网格视图GridView

- 网格视图GridView也是常见的列表类视图，它用于分行分列显示表格信息，比列表视图更适合展示物品清单

- 沿用列表视图的3个方法setAdapter、setOnItemClickListener、setOnItemLongClickListener，网格视图还新增了部分属性与方法

  | XML中的属性       | GridView类的设置方法 | 说明                                                         |
  | ----------------- | -------------------- | ------------------------------------------------------------ |
  | horizontalSpacing | setHorizontalSpacing | 指定网格项在水平方向的间距                                   |
  | verticalSpacing   | setVerticalSpacing   | 指定网格项在垂直方向的间距                                   |
  | numColumns        | setNumColumns        | 指定列的数目                                                 |
  | stretchMode       | setStretchMode       | 指定剩余空间的拉伸模式                                       |
  | columnWidth       | setColumnWidth       | 指定每列的宽度。拉伸模式为spacingWidth、 spacingWidthUniform时，必须指定列宽 |

- GridView拉伸模式取值

  | XML中的拉伸模式     | GridView类的拉伸模式    | 说明                                                  |
  | ------------------- | ----------------------- | ----------------------------------------------------- |
  | none                | NO_STRETCH              | 不拉伸                                                |
  | columnWidth         | STRETCH_COLUMN_WIDTH    | 若有剩余空间，则拉伸列宽挤掉空隙                      |
  | spacingWidth        | STRETCH_SPACING         | 若有剩余空间，则列宽不变，把空间分配到每 列间的空隙   |
  | spacingWidthUniform | STRETCH_SPACING_UNIFORM | 若有剩余空间，则列宽不变，把空间分配到每 列左右的空隙 |

使用方法：

1. 添加GridView视图

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">
   
       <GridView
           android:id="@+id/gv_planet"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:horizontalSpacing="3dp"
           android:numColumns="2"
           android:stretchMode="columnWidth" />
   
   </LinearLayout>
   ```

2. 编写网格视图的适配器

   ```kotlin
   class PlanetGridAdapter(private val mContext: Context, private val mPlanetList: List<Planet>) :
       BaseAdapter() {
       // 获取列表项的个数
       override fun getCount(): Int {
           return mPlanetList.size
       }
   
       override fun getItem(position: Int): Any {
           return mPlanetList[position]
       }
   
       override fun getItemId(position: Int): Long {
           return position.toLong()
       }
   
       override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View? {
   
           var convertView = convertView
           val holder: ViewHolder
           if (convertView == null) { // 转换视图为空
               // 根据布局文件item_list.xml生成转换视图对象
               convertView = LayoutInflater.from(mContext).inflate(R.layout.item_grid, null)
               holder = ViewHolder() // 创建一个新的视图持有者
               holder.iv_icon = convertView.findViewById(R.id.iv_icon)
               holder.tv_name = convertView.findViewById(R.id.tv_name)
               holder.tv_desc = convertView.findViewById(R.id.tv_desc)
               // 将视图持有者保存到转换视图当中
               convertView.tag = holder
           } else {  // 转换视图非空
               holder = convertView.tag as ViewHolder // 从转换视图中获取之前保存的视图持有者
           }
   
           // 给控制设置好数据
           val planet = mPlanetList[position]
           holder.iv_icon.setImageResource(planet.image)
           holder.tv_name.text = planet.name
           holder.tv_desc.text = planet.desc
           holder.iv_icon.requestFocus()
           return convertView
       }
   
       class ViewHolder {
           lateinit var iv_icon: ImageView
           lateinit var tv_name: TextView
           lateinit var tv_desc: TextView
       }
   }
   ```

3. 在Activity页面设置适配器和点击事件监听

   ```kotlin
   class GridViewActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_grid_view)
   
           findViewById<GridView>(R.id.gv_planet).apply {
               adapter = PlanetGridAdapter(this@GridViewActivity, Planet.getDefaultList()) // 设置适配器
               setOnItemClickListener { _, _, position, _ -> // 设置点击事件监听
                   ToastUtil.show(
                       this@GridViewActivity,
                       "点击了${Planet.getDefaultList()[position].name}"
                   )
               }
           }
       }
   }
   ```

## RecyclerView滚动控件

### 基本用法

1. 打开build.gradle，在dependencies中添加RecyclerView库

   ```groovy
   dependencies {
       ...
       implementation 'androidx.recyclerview:recyclerview:1.0.0'
       ...
   }
   ```

2. 在活动页面局部中添加recycleView控件，要填写完整包名

   ```xml
   <androidx.recyclerview.widget.RecyclerView
       android:id="@+id/recyclerview"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```

3. 创建RecyclerView的适配器，该适配器要继承于`RecyclerView.Adapter`，并将泛型指定为FruitAdapter.ViewHolder

   在适配器中创建内部类，继承自RecyclerView.ViewHolder

   重写onCreateViewHolder onBindViewHolder getItemCount方法，补充代码逻辑

   ```kotlin
   class FruitAdapter(private val fruitList: List<Fruit>) : RecyclerView.Adapter<FruitAdapter.ViewHolder>() {
   
       inner class ViewHolder(view: View) : RecyclerView.ViewHolder(view) {
           val fruitImage: ImageView = view.findViewById(R.id.fruitImage) // 获取图片控件
           val fruitName: TextView = view.findViewById(R.id.fruitName) // 获取文本控件
       }
   
       override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
           val view =
               LayoutInflater.from(parent.context).inflate(R.layout.fruit_item, parent, false) // 加载布局
           return ViewHolder(view) // 返回创建ViewHolder实例，并返回
       }
   
       override fun onBindViewHolder(holder: ViewHolder, position: Int) {
           val fruit = fruitList[position] // 获取数据
           holder.fruitImage.setImageResource(fruit.imageId) // 设置图片
           holder.fruitName.text = fruit.name // 设置名称
       }
   
       override fun getItemCount(): Int = fruitList.size // 返回数据源的长度
   
   }
   ```

4. 在活动页面设置RecyclerView的布局管理器和适配器

   ```kotlin
   class RecyclerActivity : AppCompatActivity() {
   
       private val fruitList = ArrayList<Fruit>()
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_recycler)
   
           initFruits() // 初始化水果数据
           recyclerview.layoutManager = LinearLayoutManager(this) // 设置布局管理器
           recyclerview.adapter = FruitAdapter(fruitList) // 设置recyclerview的适配器
       }
   
       private fun initFruits() {
       	// 省略初始化水果数据
       }
   }
   ```

- 运行效果<img src="https://image.cgz233.cn/images/202303030932065.png" alt="image-20230303093216401" style="zoom: 33%;" /> 

### 实现横向滚动和瀑布流布局

**实现横向滚动：**

1. 更改fruit_item.xml布局，设置为垂直排列

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="80dp"
       android:layout_height="wrap_content"
       android:orientation="vertical">
   
       <ImageView
           android:id="@+id/fruitImage"
           android:layout_width="40dp"
           android:layout_height="40dp"
           android:layout_gravity="center_horizontal"
           android:layout_marginTop="10dp"
           tools:src="@drawable/apple_pic" />
   
   
       <TextView
           android:id="@+id/fruitName"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_gravity="center_horizontal"
           android:layout_marginTop="10dp"
           tools:text="Apple" />
   
   </LinearLayout>
   ```

2. 在活动页面将RecyclerView的布局管理器的orientation属性，设置为LinearLayoutManager.HORIZONTAL

   ```kotlin
   recyclerview.layoutManager = LinearLayoutManager(this).apply { // 设置布局管理器
       orientation = LinearLayoutManager.HORIZONTAL // 设置为横向布局
   }
   ```

- 运行效果<img src="https://image.cgz233.cn/images/202303030943485.png" alt="image-20230303094347291" style="zoom: 50%;" /> 

- RecyclerView还提供了GridLayoutManager网格布局和SuggeredGridLayoutManager瀑布流布局

**实现瀑布流布局：**

1. 更改fruit_item.xml布局，将宽度设置为match_parent，因为瀑布流的布局是根据列数自动匹配的，而不是一个固定值

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:layout_margin="5dp"
       android:orientation="vertical">
   
       <ImageView
           android:id="@+id/fruitImage"
           android:layout_width="40dp"
           android:layout_height="40dp"
           android:layout_gravity="center_horizontal"
           android:layout_marginTop="10dp"
           tools:src="@drawable/apple_pic" />
   
       <TextView
           android:id="@+id/fruitName"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_gravity="left"
           android:layout_marginTop="10dp"
           tools:text="Apple" />
   
   </LinearLayout>
   ```

2. 在活动页面更改布局管理器为SuggeredGridLayoutManager，第一个参数为布局的列数，第二个参数为布局的排列方向

   StaggeredGridLayoutManager.VERTICAL表示纵向排列

   因为瀑布流布局要求各个子项的高度不同才能看出明显效果，所以这里把水果名称设置为1-20随机数量

   ```kotlin
   class RecyclerActivity : AppCompatActivity() {
   
       private val fruitList = ArrayList<Fruit>()
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_recycler)
   
           initFruits() // 初始化水果数据
           recyclerview.layoutManager =
               StaggeredGridLayoutManager(3, StaggeredGridLayoutManager.VERTICAL)
           recyclerview.adapter = FruitAdapter(fruitList) // 设置recyclerview的适配器
   
       }
   
       private fun initFruits() {
           repeat(2) {
               fruitList.add(Fruit(getRandomLengthString("Apple"), R.drawable.apple_pic))
               fruitList.add(Fruit(getRandomLengthString("Banana"), R.drawable.banana_pic))
               fruitList.add(Fruit(getRandomLengthString("Orange"), R.drawable.orange_pic))
               fruitList.add(Fruit(getRandomLengthString("Watermelon"), R.drawable.watermelon_pic))
               fruitList.add(Fruit(getRandomLengthString("Pear"), R.drawable.pear_pic))
               fruitList.add(Fruit(getRandomLengthString("Grape"), R.drawable.grape_pic))
               fruitList.add(Fruit(getRandomLengthString("Pineapple"), R.drawable.pineapple_pic))
               fruitList.add(Fruit(getRandomLengthString("Strawberry"), R.drawable.strawberry_pic))
               fruitList.add(Fruit(getRandomLengthString("Cherry"), R.drawable.cherry_pic))
               fruitList.add(Fruit(getRandomLengthString("Mango"), R.drawable.mango_pic))
           }
       }
   
       private fun getRandomLengthString(str: String): String {
           val n = (1..20).random()
           val builder = StringBuilder()
           repeat(n) {
               builder.append(str)
           }
           return builder.toString()
       }
   }
   ```

- 运行效果<img src="https://image.cgz233.cn/images/202303031009314.png" alt="Screenshot_1677808563" style="zoom: 33%;" /> 

### RecyclerView的点击事件

- 要想设置RecyclerView的点击事件，需要在适配器重写的onCreateViewHolder方法中设置

  viewHolder.itemView.setOnClickListener可以设置整个布局的点击事件

  viewHolder.控件名.setOnClickListener可以设置单独控件的点击事件

  ```kotlin
  override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
      val view =
          LayoutInflater.from(parent.context).inflate(R.layout.fruit_item, parent, false) // 加载布局
      val viewHolder = ViewHolder(view) // 加载布局中的控件
      viewHolder.itemView.setOnClickListener { // 设置整个视图的点击事件
          val position = viewHolder.adapterPosition // 获取点击的编号
          val fruit = fruitList[position]// 获取点击的编号
          Toast.makeText(parent.context, "你点击了${fruit.name}", Toast.LENGTH_SHORT).show()
      }
      viewHolder.fruitImage.setOnClickListener { // 设置图片的点击事件
          val position = viewHolder.adapterPosition // 获取点击的编号
          val fruit = fruitList[position] // 获取点击的编号
          Toast.makeText(parent.context, "你点击了${fruit.name}图片", Toast.LENGTH_SHORT).show()
      }
      return viewHolder
  }
  ```

### 编写聊天界面

1. 编写聊天界面xml布局，使用RecyclerView和EditText和Button

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">
   
       <androidx.recyclerview.widget.RecyclerView
           android:id="@+id/recyclerView"
           android:layout_width="match_parent"
           android:layout_height="0dp"
           android:layout_weight="1" />
   
       <LinearLayout
           android:layout_width="match_parent"
           android:layout_height="wrap_content">
   
           <EditText
               android:id="@+id/inputText"
               android:layout_width="0dp"
               android:layout_height="wrap_content"
               android:layout_weight="1"
               android:hint="请输入..."
               android:maxLines="2" />
   
           <Button
               android:id="@+id/send"
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:text="发送" />
   
       </LinearLayout>
   
   </LinearLayout>
   ```

2. 分别别写发送对话框和接收对话框布局

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:padding="10dp">
   
       <LinearLayout
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_gravity="left"
           android:background="@drawable/message_left">
   
           <TextView
               android:id="@+id/leftMsg"
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:layout_gravity="center"
               android:layout_margin="10dp"
               android:textColor="#fff" />
   
       </LinearLayout>
   
   </FrameLayout>
   ```

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:padding="10dp">
   
       <LinearLayout
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_gravity="right"
           android:background="@drawable/message_right">
   
           <TextView
               android:id="@+id/rightMsg"
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:layout_gravity="center"
               android:layout_margin="10dp"
               android:textColor="#000" />
   
       </LinearLayout>
   
   </FrameLayout>
   ```

3. 编写信息适配器

   ```kotlin
   class MsgAdapter(val msgList: List<Msg>) : RecyclerView.Adapter<RecyclerView.ViewHolder>() {
   
       inner class LeftViewHolder(view: View) : RecyclerView.ViewHolder(view) {
           val leftMsg: TextView = view.findViewById(R.id.leftMsg)
       }
   
       inner class RightViewHolder(view: View) : RecyclerView.ViewHolder(view) {
           val rightMsg: TextView = view.findViewById(R.id.rightMsg)
       }
   
       override fun getItemViewType(position: Int): Int = msgList[position].type // 获取当前组件类型
   
       override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): RecyclerView.ViewHolder =
           if (viewType == Msg.TYPE_RECEIVED) {
               val view =
                   LayoutInflater.from(parent.context).inflate(R.layout.msg_left_item, parent, false)
               LeftViewHolder(view)
           } else {
               val view =
                   LayoutInflater.from(parent.context).inflate(R.layout.msg_right_item, parent, false)
               RightViewHolder(view)
           }
   
       override fun onBindViewHolder(holder: RecyclerView.ViewHolder, position: Int) {
           val msg = msgList[position]
           when (holder) {
               is LeftViewHolder -> holder.leftMsg.text = msg.content
               is RightViewHolder -> holder.rightMsg.text = msg.content
           }
       }
   
       override fun getItemCount(): Int = msgList.size
   
   }
   ```

4. 编写活动页面的逻辑

   ```kotlin
   class MsgActivity : AppCompatActivity(), View.OnClickListener {
   
       private val msgList = ArrayList<Msg>() // 定义一个信息数组
       private lateinit var msgAdapter: MsgAdapter // 定义一个信息适配器
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_msg)
           initMsg() // 初始化信息
           msgAdapter = MsgAdapter(msgList) // 初始化适配器
           recyclerView.apply {
               layoutManager = LinearLayoutManager(this@MsgActivity)// 设置RecyclerView的布局管理器
               recyclerView.adapter = msgAdapter // 设置RecyclerView的适配器
           }
           send.setOnClickListener(this) // 设置发送按钮的点击事件
       }
   
       override fun onClick(v: View?) {
           when (v) {
               send -> { // 如果点击了发送按钮
                   val content = inputText.text.toString() // 获取输入框中的内容
                   if (content.isNotEmpty()) { // 如果内容不为空
                       val msg = Msg(content, Msg.TYPE_SENT) // 新建一个Msg对象，将文本存入
                       msgList.add(msg) // 将Msg对象存入数组
                       msgAdapter.notifyItemChanged(msgList.size - 1) // 当有新消息时，刷新RecyclerView中的显示
                       recyclerView.scrollToPosition(msgList.size - 1) // 将RecyclerView定位到最后一行
                       inputText.setText("") // 清空输入框的内容
                   }
               }
           }
       }
   
       private fun initMsg() {
           val msg1 = Msg("你好", Msg.TYPE_RECEIVED)
           val msg2 = Msg("Hello", Msg.TYPE_SENT)
           val msg3 = Msg("在学Android", Msg.TYPE_RECEIVED)
           msgList.add(msg1)
           msgList.add(msg2)
           msgList.add(msg3)
       }
   }
   ```

- 运行效果<img src="https://image.cgz233.cn/images/202303031635671.png" alt="Screenshot_1677832502" style="zoom:25%;" /> 

## 翻页类视图

### 翻页视图ViewPager

- 翻页视图使用翻页适配器PagerAdapter
- 翻页视图使用页面变更监听器OnPageChangeListener监听页面切换事件

- 翻页视图3个常用方法
  - setAdapter：设置页面项的适配器。适配器用的是PagerAdapter及其子类
  - setCurrentItem：设置当前页码，也就是要显示哪个页面
  - addOnPageChangeListener：添加翻页视图的页面变更监听器。该监听器需实现接口OnPageChangeListener下的3个方法：
    - onPageScrollStateChanged：在页面滑动状态变化时触发
    - onPageScrolled：在页面滑动过程中触发
    - onPageSelected：在选中页面时，即滑动结束后触发

使用方法：

1. 添加ViewPager翻页视图

   ```xml
   <!-- 注意翻页视图ViewPager的节点名称要填全路径 -->
   <androidx.viewpager.widget.ViewPager
       android:id="@+id/vp_content"
       android:layout_width="match_parent"
       android:layout_height="400dp"/>
   ```

2. 编写网页视图的适配器，该适配器需要继承PagerAdapter

   ```kotlin
   class ImagePagerAdapter(private val mContext: Context, private val mPlanetList: List<Planet>) :
       PagerAdapter() {
   
       // 声明一个图像视图列表
       private var mViewList: MutableList<ImageView> = ArrayList()
   
       init {
           // 给每个商品分配一个专用的图像视图
           for (info in mPlanetList) {
               val view = ImageView(mContext).apply {
                   layoutParams = ViewGroup.LayoutParams(
                       ViewGroup.LayoutParams.MATCH_PARENT,
                       ViewGroup.LayoutParams.WRAP_CONTENT
                   )
                   setImageResource(info.image)
               }
               mViewList.add(view)
           }
       }
   
       override fun getCount(): Int {
           return mViewList.size
       }
   
       override fun isViewFromObject(view: View, `object`: Any): Boolean {
           return view == `object`
       }
   
       // 实例化指定位置的页面，并将其添加到容器中
       override fun instantiateItem(container: ViewGroup, position: Int): Any {
           // 添加一个view到container中，而后返回一个跟这个view可以关联起来的对象，
           // 这个对象能够是view自身，也能够是其余对象，
           // 关键是在isViewFromObject可以将view和这个object关联起来
           val view = mViewList[position]
           container.addView(view)
           return view
       }
   
       // 从容器中销毁指定位置的页面
       override fun destroyItem(container: ViewGroup, position: Int, `object`: Any) {
           container.removeView(mViewList[position])
       }
   }
   ```

3. 在Activity页面给翻页视图添加适配器和点击事件监听

   ```kotlin
   class ViewPagerActivity : AppCompatActivity(), ViewPager.OnPageChangeListener {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_view_pager)
           // 初始化翻页视图
           findViewById<ViewPager>(R.id.vp_content).apply {
               adapter = ImagePagerAdapter(this@ViewPagerActivity, Planet.getDefaultList()) // 添加适配器
               addOnPageChangeListener(this@ViewPagerActivity) // 给翻页视图添加页面变更监听器
           }
       }
   
       // 翻页状态改变时触发。state取值说明为：0表示静止，1表示正在滑动，2表示滑动完毕
       // 在翻页过程中，状态值变化依次为：正在滑动→滑动完毕→静止
       override fun onPageScrollStateChanged(state: Int) {
   
       }
   
       // 在翻页过程中触发。该方法的三个参数取值说明为 ：第一个参数表示当前页面的序号
       // 第二个参数表示页面偏移的百分比，取值为0到1；第三个参数表示页面的偏移距离
       override fun onPageScrolled(position: Int, positionOffset: Float, positionOffsetPixels: Int) {
   
       }
   
       // 在翻页结束后触发。position表示当前滑到了哪一个页面
       override fun onPageSelected(position: Int) {
           ToastUtil.show(this, "当前是${Planet.getDefaultList()[position].name}")
       }
   }
   ```

### 翻页标签栏PagerTabStrip

- Android提供了翻页标签栏PagerTabStrip，它能够在翻页视图上方显示页面标题

使用步骤：

1. 在ViewPager节点下添加PagerTabStrip

   ```xml
   <!-- 注意翻页视图ViewPager的节点名称要填全路径 -->
   <androidx.viewpager.widget.ViewPager
       android:id="@+id/vp_content"
       android:layout_width="match_parent"
       android:layout_height="400dp">
   
       <!-- 注意翻页标签栏PagerTabStrip的节点名称要填全路径 -->
       <androidx.viewpager.widget.PagerTabStrip
           android:id="@+id/pts_tab"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"/>
   
   </androidx.viewpager.widget.ViewPager>
   ```

2. 在翻页适配器的代码中重写getPageTitle方法，在不同位置返回对应的标题文本

   ```kotlin
   override fun getPageTitle(position: Int): CharSequence? {
       return mPlanetList[position].name
   }
   ```

3. 若想修改翻页标签栏的文本样式，必须在Java代码中调用setTextSize和setTextColor方法才行，因为PagerTabStrip不支持在XML文件中设置文本大小和文本颜色，只能在代码中设置文本样式

   ```kotlin
   // 初始化翻页标签栏
   private fun initPagerStrip() {
       findViewById<PagerTabStrip>(R.id.pts_tab).apply {
           setTextSize(TypedValue.COMPLEX_UNIT_SP, 20.toFloat()) // 设置翻页标签栏的文本大小
           setTextColor(Color.BLACK) // 设置翻页标签栏的文本颜色
       }
   }
   ```

## 碎片Fragment

### 碎片的静态注册

1. 创建碎片 New -> Fragment -> Fragment(Blank)

2. 编写碎片的XML布局

   ```xml
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:orientation="horizontal"
       android:background="#bbffbb">
   
       <TextView
           android:id="@+id/tv_adv"
           android:layout_width="0dp"
           android:layout_height="match_parent"
           android:layout_weight="1"
           android:gravity="center"
           android:text="广告图片"
           android:textColor="#000000"
           android:textSize="17sp" />
   
       <ImageView
           android:id="@+id/iv_adv"
           android:layout_width="0dp"
           android:layout_height="match_parent"
           android:layout_weight="4"
           android:src="@drawable/adv"
           android:scaleType="fitCenter" />
   
   </LinearLayout>
   ```

3. java代码中指向该布局

   ```java
   class StaticFragment : Fragment() {
   
       // 创建视图
       override fun onCreateView(
           inflater: LayoutInflater, container: ViewGroup?,
           savedInstanceState: Bundle?
       ): View? {
           Log.d(TAG, "Fragment onCreateView")
           return inflater.inflate(R.layout.fragment_static, container, false)
       }
   }
   ```

4. 在活动的xml布局中调用

   fragment节点必须指定id属性，否则App运行会报错

   fragment节点必须通过name属性指定碎片类的完整路径

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">
   
       <!-- 把碎片当作一个控件使用，其中android:name指明了碎片来源 -->
       <fragment
           android:id="@+id/fragment_static"
           android:name="com.example.mytest2.fragment.StaticFragment"
           android:layout_width="match_parent"
           android:layout_height="40dp" />
   
   </LinearLayout>
   ```

静态注册时的生命周期：

- 碎片在静态注册时的生命周期，像活动的基本生命周期方法onCreate、onStart、onResume、onPause、onStop、onDestroy，碎片同样也有，而且还多出了下面5个生命周期方法
  - onAttach：与活动页面结合
  - onCreateView：创建碎片视图
  - onActivityCreated：在活动页面创建完毕后调用
  - onDestroyView：回收碎片视图
  - onDetach：与活动页面分离

<img src="https://image.cgz233.cn/images/202302281725352.png" alt="image-20230228172503373" style="zoom:67%;" /> 

<img src="https://image.cgz233.cn/images/202302281727733.png" alt="image-20230228172723997" style="zoom:67%;" /> 

```kotlin
class StaticFragment : Fragment() {

    val TAG = "CHEN_"

    // 把碎片贴到页面上
    override fun onAttach(context: Context) {
        super.onAttach(context)
        Log.d(TAG, "Fragment onAttach")
    }

    // 页面创建
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.d(TAG, "Fragment onCreate")
    }

    // 创建视图
    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        Log.d(TAG, "Fragment onCreateView")
        return inflater.inflate(R.layout.fragment_static, container, false)
    }

    // 在活动页面创建之后
    override fun onActivityCreated(savedInstanceState: Bundle?) {
        super.onActivityCreated(savedInstanceState)
        Log.d(TAG, "Fragment onActivityCreated")
    }

    // 页面启动
    override fun onStart() {
        super.onStart()
        Log.d(TAG, "Fragment onStart")
    }

    // 页面恢复
    override fun onResume() {
        super.onResume()
        Log.d(TAG, "Fragment onResume")
    }

    // 页面暂停
    override fun onPause() {
        super.onPause()
        Log.d(TAG, "Fragment onPause")
    }

    // 页面停止
    override fun onStop() {
        super.onStop()
        Log.d(TAG, "Fragment onStop")
    }

    // 销毁碎片视图
    override fun onDestroyView() {
        super.onDestroyView()
        Log.d(TAG, "Fragment onDestroyView")
    }

    // 页面销毁
    override fun onDestroy() {
        super.onDestroy()
        Log.d(TAG, "Fragment onDestroy")
    }

    // 把碎片从页面撕下来
    override fun onDetach() {
        super.onDetach()
        Log.d(TAG, "Fragment onDetach")
    }

}
```

### 碎片的动态注册

- 静态注册是在XML文件中直接添加fragment节点，而动态注册迟至代码执行时才动态添加碎片
- 动态生成的碎片基本给翻页视图使用，要知道ViewPager和Fragment可是一对好搭档

使用步骤：

1. 创建一个碎片

   写一个newInstance方法用来获取碎片实例，newInstance方法返回一个碎片实例，碎片实例应添加包裹，包裹里添加图片和商品描述

   重写onCreate方法，取出包裹的数据

   重写onCreateView方法，返回一个视图，注意要设置好商品的图片和描述

   ```kotlin
   class DynamicFragment : Fragment() {
       private var image_id: Int = 0 // 图片资源id
       private var desc: String? = null // 商品描述
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           arguments?.let {
               image_id = it.getInt("image_id") // 获取包裹中的商品图片资源
               desc = it.getString("desc") // 获取包裹中的商品描述
           }
       }
   
       override fun onCreateView(
           inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?
       ): View? = inflater.inflate(R.layout.fragment_dynamic, container, false).apply {
           findViewById<ImageView>(R.id.iv_pic).setImageResource(image_id) // 设置商品图片
           findViewById<TextView>(R.id.tv_desc).text = desc // 设置商品描述
       }
   
       companion object {
           @JvmStatic
           fun newInstance(image_id: Int, desc: String) = // 直接返回添加好包裹的DynamicFragment实例
               DynamicFragment().apply {
                   arguments = Bundle().apply {
                       putInt("image_id", image_id) // 往包裹存入图片的资源编号
                       putString("desc", desc) // 往包裹存入商品描述
                   }
               }
       }
   }
   ```

2. 创建碎片适配器，应继承于FragmentPagerAdapter，需要传入一个FragmentManager碎片管理器

   重写getCount方法获取碎片个数，重写getItem方法获取指定位置的碎片Fragment，重写getPageTitle获得指定碎片页的标题文本

   ```kotlin
   class MobilePagerAdapter(
       fm: FragmentManager,
       private val goodsList: List<GoodsInfo>
   ) : // 传入FragmentManager碎片管理器和商品集合
       FragmentPagerAdapter(fm) {
   
       override fun getCount(): Int { // 获取碎片Fragment的个数
           return goodsList.size
       }
   
       override fun getItem(position: Int): Fragment { // 获取指定位置的碎片Fragment
           return DynamicFragment.newInstance(goodsList[position].pic, goodsList[position].desc)
       }
   
       override fun getPageTitle(position: Int): CharSequence? { // 获得指定碎片页的标题文本
           return goodsList[position].name
       }
   
   }
   ```

3. 最后应在Activity里添加ViewPager视图，然后在Java代码中设置适配器和默认显示的视图等

   ```kotlin
   class FragmentDynamicActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_fragment_dynamic)
   
           findViewById<ViewPager>(R.id.vp_content).apply {
               adapter = MobilePagerAdapter(supportFragmentManager, GoodsInfo.defaultList) // 设置适配器
               currentItem = 0 // 设置默认显示第一个
           }
       }
   }
   ```

## Fragment（第一行代码）

### 静态添加碎片

1. 创建一个碎片的布局

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">
   
       <Button
           android:id="@+id/button"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_gravity="center_horizontal"
           android:text="Button" />
   
   </LinearLayout>
   ```

2. 创建一个类，该类需继承于Fragment，并重写onCreateView方法，返回一个布局

   ```kotlin
   class LeftFragment : Fragment() {
       override fun onCreateView(
           inflater: LayoutInflater,
           container: ViewGroup?,
           savedInstanceState: Bundle?
       ): View? {
           return inflater.inflate(R.layout.left_fragment, container, false)
       }
   }
   ```

3. 在活动页面布局添加fragment控件，控件的name属性指向创建的Fragment类全路径

   ```xml
   <fragment
       android:id="@+id/leftFrag"
       android:name="com.example.fragmentapplication.LeftFragment"
       android:layout_width="0dp"
       android:layout_height="match_parent"
       android:layout_weight="1" />
   ```

### 动态添加碎片

1. 在活动布局中添加一个FrameLayout子布局，它是Android中最简单的一种布局，所有的控件默认都会摆放在布局的左上角。由于这里仅需要在布局里放入一个Fragment ，不需要任何定位，因此非常适合使用FrameLayout

   ```xml
   <FrameLayout
       android:id="@+id/rightLayout"
       android:layout_width="0dp"
       android:layout_height="match_parent"
       android:layout_weight="1">
   
   </FrameLayout>
   ```

2. 创建FrameLayout类和布局，和静态添加一样

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:background="#ffff00"
       android:orientation="vertical">
   
       <TextView
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_gravity="center_horizontal"
           android:text="This is another right fragment"
           android:textSize="24sp" />
   
   </LinearLayout>
   ```

   ```kotlin
   class AnotherRightFragment : Fragment() {
       override fun onCreateView(
           inflater: LayoutInflater,
           container: ViewGroup?,
           savedInstanceState: Bundle?
       ): View? {
           return inflater.inflate(R.layout.another_right_fragment, container, false)
       }
   }
   ```

3. 在活动页面往子布局中添加碎片

   添加碎片步骤：

   1. 通过getSupportFragmentManager获取碎片管理器
   2. 通过beginTransaction方法开启事务
   3. 调用replace方法，向布局内添加或替换Fragment
   4. 调用commit方法提交事务

   ```kotlin
   class MainActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)
   
           button.setOnClickListener { // 当点击按钮后
               replaceFragment(AnotherRightFragment()) // 添加AnotherRightFragment碎片
           }
           replaceFragment(RightFragment()) // 添加RightFragment碎片
       }
   
       private fun replaceFragment(fragment: Fragment) {
           val fragmentManager = supportFragmentManager // 获取碎片管理器
           val transaction = fragmentManager.beginTransaction() // 开启一个事务
           transaction.replace(R.id.rightLayout, fragment) // 向布局内添加或替换Fragment
           transaction.commit() // 提交事务
       }
   }
   ```

### 在Fragment中实现返回栈

- 要想通过点击返回按钮返回上一个Fragment，就要在添加事务时调用addToBackStack方法

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        button.setOnClickListener { // 当点击按钮后
            replaceFragment(AnotherRightFragment()) // 添加AnotherRightFragment碎片
        }
        replaceFragment(RightFragment()) // 添加RightFragment碎片
    }

    private fun replaceFragment(fragment: Fragment) {
        val fragmentManager = supportFragmentManager // 获取碎片管理其实
        val transaction = fragmentManager.beginTransaction() // 开启一个事务
        transaction.replace(R.id.rightLayout, fragment) // 向布局内添加或替换Fragment
        
        transaction.addToBackStack(null) // 将事务添加到返回栈中
        
        transaction.commit() // 提交事务
    }
}
```

### Fragment和Activity之间的交互

- 在Activity中获取Fragment实例

  FragmentManager提供了一个类似于findViewById()的方法，专门用于从布局文件中获取Fragment的实例

  ```kotlin
  val fragment = supportFragmentManager.findFragmentById(R.id.leftFrag) as LeftFragment
  ```

- kotlin-android-extensions插件也对findFragmentById()方法进行了扩展，允许我们直接使用布局文件中定义的Fragment id名称来自动获取相应的Fragment实例

  ```
  val fragment = leftFrag as LeftFragment
  ```

- 在Fragment获取Activity实例

  在每个Fragment中都可以通过调用getActivity()方法来得到和当前Fragment相关联的Activity实例

  ```kotlin
  if (activity != null) { 
  	val mainActivity = activity as MainActivity 
  }
  ```

### Fragment的生命周期

**Fragment的四种状态：**

1. 运行状态

   当一个Fragment 所关联的Activity 正处于运行状态时，该Fragment 也处于运行状态。

2. 暂停状态

   当一个Activity 进入暂停状态时（由于另一个未占满屏幕的Activity 被添加到了栈顶），与它相关联的Fragment 就会进入暂停状态。

3. 停止状态

   当一个Activity 进入停止状态时，与它相关联的Fragment 就会进入停止状态，或者通过调用FragmentT ransaction 的remove()、replace()方法将Fragment 从Activity 中移除，但在事务提交之前调用了addToBackStack()方法，这时的Fragment 也会进入停止状态。总的来说，进入停止状态的Fragment 对用户来说是完全不可见的，有可能会被系统回收

4. 销毁状态

   Fragment 总是依附于Activity 而存在，因此当Activity 被销毁时，与它相关联的Fragment 就会进入销毁状态。或者通过调用FragmentT ransaction 的remove()、replace()方法将Fragment 从Activity 中移除，但在事务提交之前并没有调用addToBackStack()方法，这时的Fragment 也会进入销毁状态

**相比于Activity附加的回调方法：**

- onAttach()：当Fragment 和Activity 建立关联时调用
- onCreateView()：为Fragment 创建视图（加载布局）时调用
- onActivityCreated()：确保与Fragment 相关联的Activity 已经创建完毕时调用
- onDestroyView()：当与Fragment 关联的视图被移除时调用
- onDetach()：当Fragment 和Activity 解除关联时调用

**Fragment的生命周期：**

<img src="https://image.cgz233.cn/images/202203031951.png" style="zoom:33%;" />  

```kotlin
class RightFragment : Fragment() {
    companion object {
        const val TAG = "RightFragment"
    }
    override fun onAttach(context: Context) {
        super.onAttach(context)
        Log.d(TAG, "onAttach")
    }
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.d(TAG, "onCreate")
    }
    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?,
                              savedInstanceState: Bundle?): View? {
        Log.d(TAG, "onCreateView")
        return inflater.inflate(R.layout.right_fragment, container, false)
    }
    override fun onActivityCreated(savedInstanceState: Bundle?) {
        super.onActivityCreated(savedInstanceState)
        Log.d(TAG, "onActivityCreated")
    }
    override fun onStart() {
        super.onStart()
        Log.d(TAG, "onStart")
    }
    override fun onResume() {
        super.onResume()
        Log.d(TAG, "onResume")
    }
    override fun onPause() {
        super.onPause()
        Log.d(TAG, "onPause")
    }
    override fun onStop() {
        super.onStop()
        Log.d(TAG, "onStop")
    }
    override fun onDestroyView() {
        super.onDestroyView()
        Log.d(TAG, "onDestroyView")
    }
    override fun onDestroy() {
        super.onDestroy()
        Log.d(TAG, "onDestroy")
    }
    override fun onDetach() {
        super.onDetach()
        Log.d(TAG, "onDetach")
    }
}
```

