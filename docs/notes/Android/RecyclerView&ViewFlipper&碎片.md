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

## ViewFlipper

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

## Fragment

### 静态添加碎

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
    val TAG = "CHEN_"
    
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
