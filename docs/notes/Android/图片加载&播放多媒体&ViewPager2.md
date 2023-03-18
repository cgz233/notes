## 图片加载

### 使用Glide加载网络图片

- [Glide v4中文文档](https://muyangmin.github.io/glide-docs-cn/)
- Glide可以直接将加载网络图片到ImageView

1. 导入依赖

   ```groovy
   implementation ("com.github.bumptech.glide:glide:4.11.0")
   ```

2. 用法

   ```kotlin
   Glide.with(活动实例).load(网址字符串http/https).into(图像视图ImageView)
   ```

3. Gilde默认采用FIT_CENTER，相当于在load和into方法调用fitCenter方法

   ```kotlin
   Glide.with(this).load(url).fitCenter().into(imageView)
   ```

4. 除了fitCenter方法，还提供了centerCrop方法、centerInside方法，还支持圆形裁剪，只需要调用circleCrop方法

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <Button
        android:id="@+id/showImageBtn"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Show Image"/>

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

</LinearLayout>
```

```kotlin
class MainActivity : AppCompatActivity() {

    private val url = "https://image.cgz233.cn/test.jpg"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        showImageBtn.setOnClickListener {
            Glide.with(this).load(url).fitCenter().into(imageView)
        }
    }
}
```

### 利用Glide实现图片三级缓存

- Gilde默认开启三级缓存机制

- 定制Glide

  ```kotlin
  val builder = Glide.with(this).load(url) // 构建一个加载网络图片的建造器 
  val options = RequestOptions().apply { // 创建Glide的请求选项
      // 个性化定制Gilde
  }
  // 在图像视图上展示网络图片，apply方法表示启用指定的请求选项
  builder.apply(options).into(imageView)
  ```

- RequestOptions的方法：

  - placeholder：设置加载开始的占位图

  - error：设置发送错误的提示图

  - override：设置图片的尺寸

  - diskCacheStrategy：设置指定的缓存策略

    | DiskCacheStrategy类的缓存策略 | 说明                       |
    | ----------------------------- | -------------------------- |
    | AUTOMATIC                     | 自动选择缓存策略           |
    | NONE                          | 不缓存图片                 |
    | DATA                          | 只缓存压缩后的图片         |
    | ALL                           | 同时缓存原始图片和压缩图片 |

  - skipMemoryCache：设置是否跳过内存缓存

  - disallHardwareConfig：关闭硬件加速，防止过大尺寸的图片加载报错

  - fitCenter：保持图片的宽高比例居中显示

  - centerCrop：保持图片的宽高比例，充满整个视图

  - centerInside：保持图片的宽高比例，在图像内部居中显示

  - circleCrop：展示圆形裁剪后的图片

```kotlin
class MainActivity : AppCompatActivity() {

    private val url = "https://image.cgz233.cn/test.jpg"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        showImageBtn.setOnClickListener {
            val builder = Glide.with(this).load(url) // 构建一个加载网络图片的建造器
            val options = RequestOptions().apply { // 创建Glide的请求选项
                placeholder(R.drawable.abc) // 设置加载开始的占位图
                error(R.drawable.abc) // 设置发送错误的提示图
                diskCacheStrategy(DiskCacheStrategy.DATA) // 设置指定的缓存策略
            }
            // 在图像视图上展示网络图片，apply方法表示启用指定的请求选项
            builder.apply(options).into(imageView)
        }
    }
}
```

### 使用Glide加载特殊图像

- 加载GIF图像（和普通图片用法相同）

  ```kotlin
  Glide.with(this).load(gif).into(imageView)
  ```

- 加载视频指定帧，使用RequestOptions.frameOf()方法

  ```kotlin
  val options = RequestOptions.frameOf(5 * 1000 * 1000.toLong())
  Glide.with(this).load("https://image.cgz233.cn/cat.mp4").apply(options).into(imageView)
  ```

  ```kotlin
  class MainActivity : AppCompatActivity() {
  
      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_main)
          ......
          showVideoBtn.setOnClickListener {
              val options = getOptions(0)
              Glide.with(this).load("https://image.cgz233.cn/cat.mp4").apply(options).into(imageView)
          }
      }
  
      // 获取指定时间点的请求参数
      @SuppressLint("CheckResult")
      private fun getOptions(position: Int): RequestOptions {
          // 指定某个时间位置的帧，单位微妙
          val options = RequestOptions.frameOf(position * 1000 * 1000.toLong())
          // 获取最近的视频帧
          options.set(VideoDecoder.FRAME_OPTION, MediaMetadataRetriever.OPTION_CLOSEST)
          // 执行从视频帧到位图对象的转换操作
          options.transform(object : BitmapTransformation() {
              override fun updateDiskCacheKey(p0: MessageDigest) {
                  try {
                      p0.update(packageName.toByte())
                  } catch (e: Exception) {
                      e.printStackTrace()
                  }
              }
              override fun transform(p0: BitmapPool, p1: Bitmap, p2: Int, p3: Int): Bitmap {
                  return p1
              }
          })
          return options
      }
  }
  ```

## 播放多媒体文件

### 播放音频

- 播放音频使用MediaPlayer类

- 常用控制方法：

  |方法名 |功能描述|
  |--|--|
  |setDataSource() |设置要播放的音频文件的位置|
  |prepare() |在开始播放之前调用，以完成准备工作|
  |start()| 开始或继续播放音频|
  |pause() |暂停播放音频|
  |reset() |将MediaPlayer 对象重置到刚刚创建的状态|
  |seekTo() |从指定的位置开始播放音频|
  |stop() |停止播放音频。调用后的MediaPlayer 对象无法再播放音频|
  |release() |释放与MediaPlayer 对象相关的资源|
  |isPlaying() |判断当前MediaPlayer 是否正在播放音频|
  |getDuration() |获取载入的音频文件的时长|

**使用步骤：**

1. 创建一个MediaPlayer实例化对象
2. 使用setDataSource方法设置音频的路径
3. 调用prepare方法使MediaPlayer进入准备状态
4. 调用start方法播放音频
5. 调用pause暂停，调用stop停止

```kotlin
class MainActivity2 : AppCompatActivity() {

    private val mediaPlayer = MediaPlayer()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main2)

        //mediaPlayer.setAudioStreamType(AudioManager.STREAM_MUSIC)
        mediaPlayer.setDataSource("https://image.cgz233.cn/test.mp3")

        musicPlayBtn.setOnClickListener {
            if (!mediaPlayer.isPlaying){
                mediaPlayer.prepare()
                mediaPlayer.start()
            }
        }
        musicPauseBtn.setOnClickListener {
            if (mediaPlayer.isPlaying){
                mediaPlayer.pause()
            }
        }

        musicStopBtn.setOnClickListener {
            if (mediaPlayer.isPlaying) {
                mediaPlayer.stop()
            }
        }
    }

    override fun onDestroy() {
        super.onDestroy()
        mediaPlayer.stop()
        mediaPlayer.release()
    }
}
```

### 播放视频

- 使用VideoView类

- 常用方法：

  |方法名 |功能描述|
  |--|--|
  |setVideoPath() |设置要播放的视频文件的位置|
  |start() |开始或继续播放视频|
  |pause() |暂停播放视频|
  |resume() |将视频从头开始播放|
  |seekTo() |从指定的位置开始播放视频|
  |isPlaying() |判断当前是否正在播放视频|
  |getDuration() |获取载入的视频文件的时长|
  |suspend() |释放ViedoView所占用的资源|

**使用步骤：**

1. 在布局中添加一个VideoView组件

   ```xml
   <VideoView
       android:id="@+id/videoView"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"/>
   ```

2. 调用VideoView的setVideoURI设置播放地址

3. 调用start方法，开始播放，调用pause暂停播放，调用resume重新播放，调用suspend释放资源

4. ```
   <VideoView
       android:id="@+id/videoView"
       android:layout_width="match_parent"
       android:layout_height="wrap_content"/>
   ```

```kotlin
class MainActivity2 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main2)

        val uri = Uri.parse("https://image.cgz233.cn/cat.mp4")
        videoView.setVideoURI(uri) // 设置视频播放的Uri地址

        videoPlayBtn.setOnClickListener {
            videoView.start() // 开始播放
        }
        videoPauseBtn.setOnClickListener {
            videoView.pause() // 暂停播放

        }
        videoReplayBtn.setOnClickListener {
            videoView.resume() // 重新播放

        }
    }

    override fun onDestroy() {
        super.onDestroy()
        videoView.suspend()
    }
}
```

## ViewPager2

1. 导入依赖，需要RecycleView做适配器

   ```groovy
   implementation 'androidx.recyclerview:recyclerview:1.2.1'
   implementation 'androidx.viewpager2:viewpager2:1.0.0'
   ```

2. 在布局中添加ViewPager2

   ```xml
   <androidx.viewpager2.widget.ViewPager2
       android:id="@+id/viewPager2"
       android:layout_width="match_parent"
       android:layout_height="match_parent"/>
   ```

3. 使用RecycleView.Adapter编写ViewPager2的适配器

   ```kotlin
   class ViewPager2Adapter(private val context: Context, private val viewPager2ImageList: List<Int>): RecyclerView.Adapter<ViewPager2Adapter.ViewHolder>() {
   
       inner class ViewHolder(view:View): RecyclerView.ViewHolder(view) {
           val xiaoxinImage = view.findViewById<ImageView>(R.id.xiaoxinImage)
       }
   
       override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
           val view =
               LayoutInflater.from(parent.context).inflate(R.layout.layout_adapter, parent, false)
           return ViewHolder(view)
       }
   
       override fun getItemCount(): Int = viewPager2ImageList.size
   
       override fun onBindViewHolder(holder: ViewHolder, position: Int) {
           Glide.with(context).load(viewPager2ImageList[position]).into(holder.xiaoxinImage)
       }
   }
   ```

4. 在活动页面设置ViewPager2的适配器

   ```kotlin
   class MainActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)
           val viewPager2ImageList = arrayListOf(R.drawable.xiaoxin0,R.drawable.xiaoxin1,R.drawable.xiaoxin2,R.drawable.xiaoxin3)
           viewPager2.adapter = ViewPager2Adapter(this@MainActivity,viewPager2ImageList)
       }
   }
   ```

利用Handler实现轮播效果：

```kotlin
private fun handlerPostDelayed(){ // 实现轮播效果
    handler.postDelayed({
        var currentItem = viewPager2.currentItem
        currentItem++
        if (currentItem == viewPager2ImageList.size){
            viewPager2.setCurrentItem(0,false)
        }else{
            viewPager2.setCurrentItem(currentItem,true)
        }
        handlerPostDelayed()
    },1500)
}
```

