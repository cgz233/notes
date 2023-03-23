## Banner实现轮播图

[Banner GitHub项目地址](https://github.com/youth5201314/banner)

基于Banner 1.4.1版本

1. 导入Banner依赖

2. 在布局中添加Banner控件

   ```xml
   <com.youth.banner.Banner
       android:id="@+id/banner"
       android:layout_width="match_parent"
       android:layout_height="400dp"
       app:image_scale_type="center_crop" />
   ```

3. 调用setImageLoader方法，设置Banner的适配器，传入一个ImageLoader接口的实现，重写接口的displayImage方法，该方法第一个参数为上下文，第二个参数为图片资源地址，第三个参数为ImageView，可以通过Glide来加载图片

4. 调用setImages方法设置图片资源数组，调用setBannerAnimation方法设置横幅动画，调用isAutoPlay传入true开启自动切换，调用setDelayTime设置切换时间，调用setOnBannerListener设置点击事件监听

5. 最后调用start方法显示Banner

   ```kotlin
   class BannerActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_banner)
           val bannerList = arrayListOf(
               R.drawable.xiaoxin0,
               R.drawable.xiaoxin1,
               R.drawable.xiaoxin2,
               R.drawable.xiaoxin3
           )
           banner.apply {
               setImageLoader(object : ImageLoader() {
                   override fun displayImage(p0: Context?, p1: Any?, p2: ImageView?) {
                       if (p0 != null && p2 != null) {
                           Glide.with(p0).load(p1).apply(RequestOptions().transform(RoundedCorners(100))).into(p2)
                       }
                   }
               })
               setBannerAnimation(Transformer.Default) // 设置横幅动画
               setImages(bannerList) // 设置图片资源数组
               setDelayTime(2000) // 设置播放速度
               isAutoPlay(true) // 设置自动切换
               setIndicatorGravity(BannerConfig.CENTER)
               setOnBannerListener {
                   Toast.makeText(this@BannerActivity,"111",Toast.LENGTH_SHORT).show()
               }
               start() // 启动Banner
           }
       }
   }
   ```



## BottomNavigationView

1. 导入material依赖

   ```kotlin
   implementation 'com.google.android.material:material:1.2.1'
   ```

2. 在布局中添加BottomNavigationView

   app:menu：声明导航按钮，它的指是一个menu文件

   app:labelVisibilityMode：导航按钮的显示模式，取值有

   - labeled：几个导航按钮全部显示文字
   - unlabeled：几个导航按钮全部不显示文字
   - selected：只有选中的按钮显示文字
   - auto：小于等于3个按钮时全部显示文字（即labeled），大于3个按钮时只有选中的按钮显示文字（即selected）

   ```xml
   <com.google.android.material.bottomnavigation.BottomNavigationView
       android:id="@+id/bottomNav"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       app:menu="@menu/bottom_nav_menu"
       app:labelVisibilityMode="labeled"
       android:background="#fff"/>
   ```

3. 创建menu文件，每个item都是一个按钮，最后添加到BottomNavigationView中的app:menu节点中

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <menu xmlns:android="http://schemas.android.com/apk/res/android">
   
       <item
           android:id="@+id/menu_home"
           android:icon="@drawable/selector_home_bg"
           android:title="主页" />
   
       <item android:id="@+id/menu_find"
           android:icon="@drawable/selector_find_bg"
           android:title="查找"/>
   
       <item android:id="@+id/menu_mine"
           android:icon="@drawable/selector_mine_bg"
           android:title="我的"/>
   
   </menu>
   ```

4. 设置导航栏的选定监听，最后应返回true

   ```kotlin
   bottomNav.setOnNavigationItemSelectedListener { // 设置底部导航点击事件监听
       when (it.itemId) {
           R.id.menu_home -> viewPager2.currentItem = 0
           R.id.menu_find -> viewPager2.currentItem = 1
           R.id.menu_mine -> viewPager2.currentItem = 2
       }
       true
   }
   ```

5. 利用Bange设置新消息提醒

   ```kotlin
   val badge = bottomNav.getOrCreateBadge(R.id.menu_mine) // 创建新消息提醒
   badge.number = 100 // 设置数字
   badge.maxCharacterCount = 3 // 设置显示的最大长度
   ```

   移除提醒

   ```kotlin
   bottomNav.removeBadge(R.id.menu_mine)

6. 使用Bange报错`    java.lang.RuntimeException: Unable to start activity ComponentInfo{com.example.navapplication/com.example.navapplication.MainActivity}: java.lang.IllegalArgumentException: The style on this component requires your app theme to be Theme.MaterialComponents (or a descendant).`

   主题须改为material

   ```xml
   <resources>
       <!-- Base application theme. -->
       <style name="AppTheme" parent="Theme.MaterialComponents.Light.DarkActionBar">
           <!-- Customize your theme here. -->
           <item name="colorPrimary">@color/colorPrimary</item>
           <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
           <item name="colorAccent">@color/colorAccent</item>
       </style>
   </resources>
   ```



## ViewPager2+Fragment+BottomNavigationView创建底部导航栏

1. 在Activity布局中添加ViewPager2和BottomNavigationView，并设置BottomNavigationView的menu菜单

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       xmlns:app="http://schemas.android.com/apk/res-auto"
       android:orientation="vertical">
   
       <androidx.viewpager2.widget.ViewPager2
           android:id="@+id/viewPager2"
           android:layout_width="match_parent"
           android:layout_height="0dp"
           android:layout_weight="1"/>
   
       <com.google.android.material.bottomnavigation.BottomNavigationView
           android:id="@+id/bottomNav"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           app:menu="@menu/bottom_nav_menu"
           app:labelVisibilityMode="labeled"
           android:background="#fff"/>
   
   </LinearLayout>
   ```

2. 创建ViewPager2适配器，这里用FragmentStateAdapter

   ```kotlin
   class FragmentAdapter(
       fragment: FragmentManager,
       lifecycle: Lifecycle,
       private val list: List<Fragment>
   ) :
       FragmentStateAdapter(fragment, lifecycle) {
   
       override fun getItemCount(): Int = list.size
   
       override fun createFragment(position: Int): Fragment = list[position]
   }
   ```

3. 创建Fragment，用于展示每页的画面

   ```kotlin
   private const val ARG_PARAM1 = "param1"
   
   class MainFragment : Fragment() {
       private var param1: String? = null
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           arguments?.let {
               param1 = it.getString(ARG_PARAM1)
           }
       }
   
       override fun onCreateView(
           inflater: LayoutInflater, container: ViewGroup?,
           savedInstanceState: Bundle?
       ): View? {
           return inflater.inflate(R.layout.fragment_main, container, false).apply {
               textView.text = param1
           }
       }
   
       companion object {
   
           @JvmStatic
           fun newInstance(param1: String) =
               MainFragment().apply {
                   arguments = Bundle().apply {
                       putString(ARG_PARAM1, param1)
                   }
               }
       }
   }
   ```

   Fragment布局

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent">
   
       <TextView
           android:id="@+id/textView"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:layout_centerInParent="true"
           android:textSize="20sp"
           android:text="Fragment" />
   
   </RelativeLayout>
   ```

4. 在活动页面中：

   1. 创建Fragment数组，并设置ViewPager2的适配器
   2. 通过registerOnPageChangeCallback方法注册ViewPager2的滑动监听，滑动时切换BottomNavigationView的选项
   3. 通过setOnNavigationItemSelectedListener注册BottomNavigationView的点击监听，点击之后切换ViewPager2的页面

   ```kotlin
   class MainActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)
   
           val list = initList() // 初始化Fragment数组
           val adapter = FragmentAdapter(supportFragmentManager, lifecycle, list) // 创建一个Fragment的适配器
   
           viewPager2.apply {
               setAdapter(adapter) // 设置ViewPager2适配器
               registerOnPageChangeCallback(object :
                   ViewPager2.OnPageChangeCallback() { // 注册ViewPager2滑动事件监听
                   override fun onPageSelected(position: Int) {
                       super.onPageSelected(position)
                       when (position) {
                           0 -> bottomNav.selectedItemId = R.id.menu_home
                           1 -> bottomNav.selectedItemId = R.id.menu_find
                           2 -> bottomNav.selectedItemId = R.id.menu_mine
                       }
                   }
               })
           }
   
           bottomNav.setOnNavigationItemSelectedListener { // 设置底部导航点击事件监听
               when (it.itemId) {
                   R.id.menu_home -> viewPager2.currentItem = 0
                   R.id.menu_find -> viewPager2.currentItem = 1
                   R.id.menu_mine -> {
                       viewPager2.currentItem = 2
                       bottomNav.removeBadge(R.id.menu_mine) // 移除消息提醒
                   }
               }
               true
           }
   
   //        val badge = bottomNav.getOrCreateBadge(R.id.menu_mine) // 创建新消息提醒
   //        badge.number = 100 // 设置数字
   //        badge.maxCharacterCount = 3 // 设置显示的最大长度
   
       }
   
       private fun initList(): ArrayList<Fragment> { // 初始化碎片数组
           val fragmentHome = MainFragment.newInstance("主页Fragment")
           val fragmentFind = MainFragment.newInstance("发现Fragment")
           val fragmentMine = MainFragment.newInstance("我的Fragment")
   
           return arrayListOf(fragmentHome, fragmentFind, fragmentMine)
       }
   }
   ```







