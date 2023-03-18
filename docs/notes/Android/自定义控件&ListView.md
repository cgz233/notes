# 自定义控件

## 引入布局

- 创建标题栏 title.xml

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:background="@drawable/title_bg">
  
      <Button
          android:id="@+id/titleBack"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_gravity="center"
          android:layout_margin="5dp"
          android:background="@drawable/back_bg"
          android:text="Back"
          android:textColor="#ffffff" />
  
      <TextView
          android:id="@+id/titleText"
          android:layout_width="0dp"
          android:layout_height="wrap_content"
          android:layout_gravity="center"
          android:layout_weight="1"
          android:gravity="center"
          android:text="Title Text"
          android:textColor="#fff"
          android:textSize="24sp" />
  
      <Button
          android:id="@+id/titleEdit"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_gravity="center"
          android:layout_margin="5dp"
          android:background="@drawable/edit_bg"
          android:text="Edit"
          android:textColor="#fff" />
  
  </LinearLayout>
  ```

- 从其他布局中引入

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:layout_width="match_parent"
      android:layout_height="match_parent">
  
      <include layout="@layout/title" />
      
  </LinearLayout>
  ```

- 在Activity中调用getSupportActionBar()方法来获得ActionBar实例，然后调用hide()方法将标题隐藏

  ```kotlin
  class ViewActivity : AppCompatActivity() {
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_view)
          supportActionBar?.hide()
      }
  }
  ```

  或者修改主题（res/values/themes.xml）为NoActionBar也可隐藏ActionBar
  
  ```xml
  <style name="Theme.KtApplication" parent="Theme.MaterialComponents.DayNight.NoActionBar.Bridge">
  ```

## 创建自定义控件

- 新建TitleLayout继承自LinearLayout，让他自定义标题栏控件

  ```kotlin
  class TitleLayout(context: Context, attrs: AttributeSet) : LinearLayout(context, attrs) {
      init {
          LayoutInflater.from(context).inflate(R.layout.title, this)
      }
  }
  ```

  这里我们在TitleLayout 的主构造函数中声明了Context 和AttributeSet 这两个参数，在布局中引入TitleLayout 控件时就会调用这个构造函数。然后在init结构体中需要对标题栏布局进行动态加载，这就要借助LayoutInflflater 来实现了。通过LayoutInflflater 的from()方法可以构建出一个LayoutInflater对象，然后调用inflate()方法就可以动态加载一个布局文件。inflate()方法接收两个参数：第一个参数是要加载的布局文件的id，这里我们传入R.layout.title；第二个参数是给加载好的布局再添加一个父布局，这里我们想要指定为TitleLayout ，于是直接传入this

- 在布局中添加自定义控件

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:layout_width="match_parent"
      android:layout_height="match_parent">
  
      <com.example.ktapplication.TitleLayout
          android:layout_width="match_parent"
          android:layout_height="wrap_content"/>
  
  </LinearLayout>
  ```

- 为标题栏中的按钮注册点击事件，修改TitleLayout 中的代码

  ```kotlin
  class TitleLayout(context: Context, attrs: AttributeSet) : LinearLayout(context, attrs) {
      init {
          LayoutInflater.from(context).inflate(R.layout.title, this)
          findViewById<Button>(R.id.titleBack).setOnClickListener {
              val activity = context as Activity
              activity.finish()
          }
          findViewById<Button>(R.id.titleEdit).setOnClickListener {
              Toast.makeText(context, "You clicked Edit button", Toast.LENGTH_SHORT).show()
          }
      }
  }
  ```



# ListView

## ListView的简单用法

- 在布局中创建ListView

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical">
  
      <ListView
          android:id="@+id/listView"
          android:layout_width="match_parent"
          android:layout_height="match_parent"/>
  
  </LinearLayout>
  ```

- 借助适配器来往ListView中添加数据，Android中提供了很多适配器的实现类，这里使用ArrayAdapter，它可以通过泛型来指定要适配的数据类型，然后在构造函数中把要适配的数据传入。ArrayAdapter有多个构造函数的重载，由于我们这里提供的数据都是字符串，因此将ArrayAdapter的泛型指定为String，然后在ArrayAdapter的构造函数中依次传入Activity的实例、ListView 子项布局的id，以及数据源。注意，我们使用了android.R.layout.simple_list_item_1作为ListView子项布局的id，这是一个Android 内置的布局文件，里面只有一个TextView ，可用于简单地显示一段文本。这样适配器对象就构建好了

  最后，还需要调用ListView的setAdapter()方法，将构建好的适配器对象传递进去，这样ListView 和数据之间的关联就建立完成了

  ```kotlin
  class ListViewActivity : AppCompatActivity() {
  
      private val data = listOf(
          "Apple", "Banana", "Orange", "Watermelon",
          "Pear", "Grape", "Pineapple", "Strawberry", "Cherry", "Mango",
          "Apple", "Banana", "Orange", "Watermelon", "Pear", "Grape",
          "Pineapple", "Strawberry", "Cherry", "Mango"
      )
  
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_list_view)
          
          var adapter = ArrayAdapter<String>(this, android.R.layout.simple_expandable_list_item_1, data)
          var listView = findViewById<ListView>(R.id.listView)
          listView.adapter = adapter
      }
  }
  ```

## 定制ListView的界面

