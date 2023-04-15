# Kt问题

1. 使用companion object全部包裹即可类名加方法名getDefaultList调用

   ```kotlin
   class Planet(image: Int, name: String, desc: String) { // 行星图片、名称、描述
   
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
               var planetList = arrayListOf<Planet>()
               iconArray.forEachIndexed { index, i ->
                   var planet = Planet(i, nameArray[i], descArray[i])
                   planetList.add(planet)
               }
               return planetList
           }
       }
   
   }
   ```

2. 调用外部类，`this@Class名`

3. `::变量名.isInitialized`可用于判断变量是否已经初始化

