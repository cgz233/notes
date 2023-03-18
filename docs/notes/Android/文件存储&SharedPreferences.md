## 文件存储

### 将数据存储到文件中

步骤：

- 通过openFileOutput()方法能够得到一个FileOutputStream对象，然后借助它构建出一个OutputStreamWriter对象，接着再使用OutputStreamWriter构建出一个BufferedWriter对象，这样你就可以通过BufferedWriter将文本内容写入文件中了

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)


    }

    override fun onDestroy() {
        super.onDestroy()
        val inputText = editText.text.toString()
        save(inputText) // 在活动销毁时将数据存储到文件中
    }

    private fun save(inputText: String) {
        try {
            // Context类中提供了一个openFileOutput()方法，可以用于将数据存储到指定的文件中
            // 第一个参数是文件名，在文件创建的时候使用，注意这里指定的文件名不可以包含路径，所有的文件都默认存储到/data/data/<pack age name>/files/ 目录下
            // 第二个参数是文件的操作模式，主要有MODE_PRIVATE和MODE_APPEND两种模式可选
            // 默认是MODE_PRIVATE，表示当指定相同文件名的时候，所写入的内容将会覆盖原文件中的内容
            // 而MODE_APPEND则表示如果该文件已存在，就往文件里面追加内容，不存在就创建新文件
            val output = openFileOutput("data", Context.MODE_PRIVATE)
            val writer = BufferedWriter(OutputStreamWriter(output))
            writer.use { // use函数是Kotlin提供的一个内置扩展函数，它会保证在Lambda表达式中的代码全部执行完之后自动将外层的流关闭，这样就不需要我们再编写一个finally语句，手动去关闭流了
                it.write(inputText)
            }
        } catch (e: Exception) {
            e.printStackTrace()
        }
    }
}
```

### 从文件中读取数据

步骤：

- 通过openFileInput()方法获取了一个FileInputStream对象，然后借助它又构建出了一个InputStreamReader对象，接着再使用InputStreamReader构建出一个BufferedReader对象，这样我们就可以通过BufferedReader将文件中的数据一行行读取出来，并拼接到StringBuilder对象当中，最后将读取的内容返回就可以了

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        val inputText = load() // 读取文件中的文字
        if (inputText.isNotEmpty()) {
            editText.setText(inputText)
            editText.setSelection(inputText.length) // 将输入光标移到文本末
            Toast.makeText(this, "Restoring succeeded", Toast.LENGTH_SHORT).show()
        }
    }
    private fun load(): String { // 读取数据
        val context = StringBuilder()
        try {
            // Context类中还提供了一个openFileInput()方法，用于从文件中读取数据
            // 它只接收一个参数，即要读取的文件名，然后系统会自动到/data/data/<pack age name>/files/ 目录下加载这个文件
            // 并返回一个FileInputStream对象，得到这个对象之后，再通过流的方式就可以将数据读取出来
            val input = openFileInput("data")
            val reader = BufferedReader(InputStreamReader(input))
            reader.use {
                reader.forEachLine { // 个forEachLine函数是Kotlin 提供的一个内置扩展函数，它会将读到的每行内容都回调到Lambda表达式中
                    context.append(it)
                }
            }
        } catch (e: Exception) {
            e.printStackTrace()
        }
        return context.toString()
    }
}
```

## SharedPreferences存储

### 将数据存储到SharedPreferences中

步骤：

1. 首先调用getSharedPreferences方法获得一个SharedPreferences对象
2. 然后调用SharedPreferences对象的edit()方法获取一个SharedPreferences.Editor对象
3. 向SharedPreferences.Editor对象中添加数据，比如添加一个布尔型数据就使用putBoolean()方法，添加一个字符串则使用putString()方法，以此类推
4. 调用apply()方法将添加的数据提交，从而完成数据存储操作

```kotlin
class SharedPreferencesActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_shared_preferences)
        saveButton.setOnClickListener {
            // 第一个参数用于指定SharedPreferences文件的名称，如果指定的文件不存在则会创建一个
            // SharedPreferences文件都是存放在/data/data/<package name>/shared_prefs/目录下的
            // 第二个参数用于指定操作模式，目前只有默认的MODE_PRIVATE这一种模式可选，它和直接传入0的效果是相同的，表示只有当前的应用程序才可以对这个SharedPreferences文件进行读写
            val editor = getSharedPreferences("data", Context.MODE_PRIVATE).edit()
            editor.apply {
                putString("name", "Tom")
                putInt("age", 18)
                putBoolean("married", false)
                apply() // 提交数据
            }
        }
    }
}
```

点击按钮后传入的数据：

```xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
    <string name="name">Tom</string>
    <boolean name="married" value="false" />
    <int name="age" value="18" />
</map>
```

### 从SharedPreferences中读取数据

- SharedPreferences对象中提供了一系列的get方法，用于读取存储的数据
- 每种get方法都对应了SharedPreferences.Editor中的一种put方法，比如读取一个布尔型数据就使用getBoolean()方法，读取一个字符串就使用getString()方法

```kotlin
class SharedPreferencesActivity : AppCompatActivity() {
    val TAG = "CHEN_"
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_shared_preferences)
        restoreButton.setOnClickListener {
            getSharedPreferences("data", Context.MODE_PRIVATE).apply {
            	// 第一个参数是键，传入存储数据时使用的键就可以得到相应的值了
				// 第二个参数是默认值，即表示当传入的键找不到对应的值时会以什么样的默认值进行返回
                val name = getString("name", "")
                val age = getInt("age", 0)
                val married = getBoolean("married", false)
                Log.d(TAG, "name=$name")
                Log.d(TAG, "age=$age")
                Log.d(TAG, "married=$married")
            }
        }
    }
}
```







