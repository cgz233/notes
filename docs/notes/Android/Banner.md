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