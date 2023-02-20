# Kotlin Notes

> By.[XioChen](https://www.cgz233.cn)

相关教程

- [Kotlin 官方文档](https://kotlinlang.org/)
- [Google Kotlin](https://developer.android.google.cn/kotlin?hl=zh-cn)
- [Kotlin 语言中文站](https://www.kotlincn.net/)
- [菜鸟教程](https://www.runoob.com/kotlin/kotlin-tutorial.html)



# 变量和函数

## 变量

- val 不可变的变量(value) 对应java中final
- var 可变的变量(variable) 对应java中非final

- `val a = 10`自动推导成整形变量
- `val a : Int = 10`声明变量类型

- Kotlin对象数据类型：Int,Long,Short,Float,Double,Boolean,Char,Byte

> 补充：

- 编译时常量

  - 编译时常量只能在函数之外定义，因为编译时常量必须在编译时赋值，而函数都是在运行时才调用，函数内的变量也是在运行时赋值，编译时常量要在这些变量赋值前就已存在
  - 编译时常量只能是常见的基本数据类型：String、lnt、Double、Float、Long、Short、Byte、Char、Boolean

  ```kotlin
  const val MAX = 200
  fun main(){
      // const val MIn = 1 错误
  }
  ```

- 查看Kotlin字节码

  - 双击Shift，输入Show Kotlin Bytecode
  - Tools -> Kotlin -> Show Kotlin Bytecode

- 字符串内嵌表达式

  - Kotlin允许在字符串里嵌如`${}`这种语法结构的表达式，并在运行时使用表达式结果替换这一部分
  
    ```kotlin
    "hello, ${obj.name}. nice to meet you!"
  
  - 当表达式中仅有一个变量时，可以省略大括号
  
    ```kotlin
    "hello, $name. nice to meet you!"
    ```

## 函数

- main函数

  ```kotlin
  fun main(){
  }
  
- 函数定义

  ```kotlin
  fun methodName(param1: Int, param2: Int): Int{
      return 0
  }
  ```
  
  fun 是定义函数的关键字，紧跟后面的是函数名，再后面是一对括号，里面可以声明该函数接收的参数，参数声明的格式为`参数名: 参数类型`，不接收函数就写一对空括号即可，参数后面的部分是返回类型，没有返回就可以不写（也可以写Unit）

- 举例

  ```kotlin
  fun largerNum(num1: Int,num2:Int): Int{
      return max(num1,num2)
  }
  ```

  当一个函数只有一行代码时，可以不写函数体，直接将唯一的代码写在函数定义的尾部，中间用等号连接

  ```kotlin
  fun largerNum(num1: Int, num2: Int): Int = max(num1, num2)
  ```

  出于kotlin的推导机制，由于max函数返回的是一个Int值，所以不用再显示地声明返回值类型，进一步化简

  ```kotlin
  fun largerNum(num1: Int, num2: Int) = max(num1, num2)
  ```

> 补充：

- 函数的参数默认值

  - 默认值参：如果不打算传入值参，可以预先给参数指定默认值

    ```kotlin
    fun fix(name: String, age: Int = 2) {
        println(name + age)
    }
    ```

  - 具体函数参数：如果使用命名值参，就可以不用管值参的顺序

    ```kotlin
    fun main() {
        fix(age = 4, name = "jack")
    }
    ```

- Unit函数

  不是所有函数都有返回值，Kotlin中没有返回值的函数叫Unit函数，也就是说他们的返回类型是Unit。在Kotlin之前，函数不返回任何东西用void描述，意思是“没有返回类型，不会带来什么，忽略它”，也就是说如果函数不返回任何东西，就忽略类型。但是，Void这种解决方案无法解释现代语言的一个重要特征，泛型

- Nothing类型

  TODO函数的任务就是抛出异常，就是永远别指望它运行成功，返回Nothing类型

- 反引号中的函数名

  Kotlin可以使用空格和特殊字符对函数命名，不过函数名要用一对反引号括起来。为了支持Kotlin和Java互操作，而Kotlin和Java各自却有着不同的保留关键字，不能作为函数名，使用反引号括住函数名就能避免任何冲突

- 函数引用

  要把函数作为参数传给其他函数使用，除了传lambda表达式，kotlin还提供了其他方法，传递函数引用，函数引用可以把一个具名函数转换成一个值参，使用lambda表达式的地方，都可以使用函数引用

  要获得函数引用，使用`::`操作符，后跟要引用的函数名

  ```kotlin
  fun main() {
      showOnBoard("卫生纸", ::getDiscountWords)
  }
  fun showOnBoard(goodsName: String, showDiscount: (String, Int) -> String) {
      val hour = (1..24).shuffled().last()
      println(showDiscount(goodsName, hour))
  }
  fun getDiscountWords(goodsName: String, hour: Int): String {
      val currentYear = 2023
      return "$currentYear 年，双十一$goodsName 促销倒计时：$hour 小时"
  }
  ```

- 函数类型作为返回类型

  函数类型也是有效的返回类型，也就是说可以定义一个能返回函数的函数

  ```kotlin
  fun main() {
      val getDiscountWords = configDiscountWords()
      println(getDiscountWords("牙膏"))
  }
  fun configDiscountWords(): (String) -> String {
      val currentYear = 2023
      val hour = (1..24).shuffled().last()
      return { goodsName: String ->
          "$currentYear 年，双十一$goodsName 促销倒计时：$hour 小时"
      }
  }
  ```

# 逻辑控制

## if条件语句

Kotlin中的if语句相比于java有一个额外的功能，就是可以有返回值

```kotlin
fun largerNum(num1: Int, num2: Int): Int {
    var value = if (num1 > num2) {
        num1
    } else {
        num2
    }
    return value
}
```

去掉多余的变量value

```kotlin
fun largerNum(num1: Int, num2: Int): Int {
    return if (num1 > num2) {
        num1
    } else {
        num2
    }
}
```

当代码只有一行时可以省略函数体

```kotlin
fun largerNum(num1: Int, num2: Int) = if (num1 > num2) {
    num1
} else {
    num2
}
```

```kotlin
fun largerNum(num1: Int, num2: Int) = if (num1 > num2) num1 else num2
```

## when条件语句

- 类似switch，但比switch强大的多

  ```kotlin
  fun getScore(name: String) = when (name) {
      "Tom" -> 86
      "Jim" -> 77
      "Jack" -> 95
      "Lily" -> 100
      else -> 0
  }
  ```

  

- when语句允许传入一个任意类型的参数，然后可以在when的结构体系中定义一系列的条件，格式是：`匹配值 -> { 执行逻辑 }`，只有一行代码时{}可以省略

- 除了精确匹配外，when还允许类型匹配

  ```kotlin
  fun checkNumber(num: Number) {
      when (num) {
          is Int -> println("number is Int")
          is Double -> println("number is Double")
          else -> println("number not support")
      }
  }
  ```
  
  is关键字相当于java中的instanceof关键字
  
  Number是Kotlin内置的抽象类，Int、Long、Float、Double等与数字相关的类都是它的子类
  
- when语句还有一种不带参数的方法

  ```kotlin
  fun getScore(name: String) = when {
      name == "Tom" -> 86
      name == "Jim" -> 77
      name == "Jack" -> 95
      name == "Lily" -> 100
      else -> 0
  }
  ```

  假设所有以Tom名字开头的人，都是86分

  ```kotlin
  fun getScore(name: String) = when {
      name.startsWith("Tom") -> 86
      name == "Jim" -> 77
      name == "Jack" -> 95
      name == "Lily" -> 100
      else -> 0
  }
  ```

## 循环语句

- while和java中用法相同

- Kotlin在for循环中做了大幅度修改，Java中最常用的for-i循环在Kotlin中直接被舍弃，而java中另一种for-each循环则被Kotlin进行了大幅度加强，变成了for-in循环

- 在Kotlin中，可以使用`val range = 0..10`来表示一个区间，表示[0-10]，`..` 是创建两端闭区间的关键字

- 有了区间就可以通过for-in遍历这个区间

  ```kotlin
  fun main() {
      for (i in 0..10){
          println(i)
      }
  }
  ```

- 在Kotlin中，可以使用`until`关键字来创建一个左闭右开的区间，如`val range = 0 until 10`，表示[0,10)

- 默认情况下，for-in循环每次执行循环时都会在区间范围内递增1，相当于Java中for-i循环中i++的效果，如果要跳过其中的一些元素，可以使用`step`关键字

  ```kotlin
  fun main() {
      for (i in 0 until 10 step 2) {
          println(i)
      }
  }
  ```

- 如果想创建一个降序的区间，可以使用`downTo`关键字

  ```kotlin
  fun main() {
      for (i in 10 downTo 1) {
          println(i)
      }
  }
  ```



# 面向对象编程

## 类与对象

- 使用class关键字声明对象，和java一致

- 创建对象

  ```kotlin
  class Person {
      var name = ""
      var age = 0;
      fun eat() {
          println(name + " is eating. He is " + age + " years old.")
      }
  }
  ```

- 实例化对象，和java类似，只是去掉了new关键字

  ```kotlin
  val p = Persion()
  ```

- 调用

  ```kotlin
  fun main() {
      val p = Person()
      p.name = "Jack"
      p.age = 18
      p.eat()
  }
  ```

> 补充：

- Kotlin中调用Java封装好的get和set方法，可以直接使用字段名进行赋值和读取，Kotlin会在背后自动将方法转成get和set方法

  ```java
  public class Book {
      private int pages;
      public int getPages(){
          return pages;
      }
      public void setPages(int pages){
          this.pages = pages;
      }
  }
  ```

  ```kotlin
  val book = Book()
  book.pages = 500
  val bookPages = book.pages
  ```

- Class对象：

  Java中的`Activty.class`相当于Kotlin中的`Activity::class.java`

## 继承与构造函数

### 继承

- 在Kotlin中想要继承一个类，首先要让这个类可以继承，在Kotlin中，任何一个非抽象类默认都是不可以被继承的，相当于在java中声明了final关键字，所以说要想继承这个类，就要在这个类前面加上open关键字

  ```kotlin
  open class Person(){}
  ```

- 第二步就是要让子类来继承，在java中使用的是extends，而在Kotlin中变成了一个:

  ```kotlin
  class Student : Person() {
      var sno = ""
      var grade = 0
  }
  ```

### 构造函数

- Kotlin将构造函数分为了两种：主构造函数和次构造函数

- 主构造函数的特点是没有函数体，直接定义在类名后面

  ```Kotlin
  class Student(val son: String, val grade: Int) : Person() {}
  ```
  
   这就表面在实例化时，必须传入这两个参数
  
  ```kotlin
  val student = Student("a123",5)
  ```
  
- Kotlin提供了一个init结构体，所有主构造函数的逻辑都写在里面

  ```kotlin
  class Student(val son: String, val grade: Int) : Person() {
      init {
          println("son is" + son)
          println("grade is" + grade)
      }
  }
  ```

- 父类主构造函数有参数

  ```kotlin
  open class Person(val name: String, val age: Int) {
  	...
  }
  ```
  
   子类继承时就要在父类中传入参数
  
  ```kotlin
  class Student(val son: String, val grade: Int, name: String, age: Int) : Person(name, age) {
      init {
          println("son is" + son)
          println("grade is" + grade)
      }
  }
  ```

- Kotlin规定，当一个类既有主构造函数又有次构造函数时，所有的构造函数都必须调用主构造函数（包括间接调用）

  次构造函数是通过constructor关键字来定义的，这里定义两个次构造函数，第一个次构造函数接收name和age参数，然后他又通过this关键字调用主构造函数并将son和grade这两个参数赋值成初始值；第2个构造函数不接受任何参数，它通过this关键字调用了我们刚才定义的第一个构造函数并将name和age参数也赋值成初始值

  ```
  class Student(val son: String, val grade: Int, name: String, age: Int) : Person(name, age) {
      constructor(name: String, age: Int) : this("", 0, name, age) {
      }
      constructor() : this("", 0) {
      }
  }
  ```

- 当类中只有次构造函数没有主构造函数，这种情况真的十分少见，但在Kotlin中是允许的，当一个类没有显式的定义主构造函数且定义了次构造函数，它就是没有主构造函数的

  ```kotlin
  class Student : Person {
      constructor(name: String, age: Int) : super(name, age) {
      }
  }
  ```
  
  因为student类的后面没有显式的定义组构造函数，同时又定义了次构造函数，所以现在student类是没有主构造函数的，那么既然没有主构造函数，所以继承person的时候也不需要再加上括号了。另外，由于没有主构造函数，次构造函数只能直接调用父类的构造函数，上述代码也是将this关键字换成了super关键字。

## 接口和修饰符

### 接口

- 接口定义

  ```kotlin
  interface Study {
      fun readBook()
      fun doHomework()
  }
  ```

- 使用接口

  Java中继承的关键是字是extends，实现接口使用的关键字是implements，而Kotlin中统一使用`:`中间用`,`进行分隔

  Kotlin中使用override关键字来重写父类或者实现接口中的函数

  ```kotlin
  class Student(name: String, age: Int) : Person(name, age), Study {
      override fun readBook() {
          println(name + " is reading.")
      }
      override fun doHomework() {
          println(name + " is dping homewrok.")
      }
  }
  ```

- Kotlin中允许接口中定义的函数进行默认实现

  在实现接口时，就可以自由选择实现或不实现

  ```kotlin
  interface Study {
      fun readBook()
      fun doHomework() {
          println("do homework default implementation.")
      }
  }
  ```

### 修饰符

| 修饰符    | Java                               | Kotlin             |
| --------- | ---------------------------------- | ------------------ |
| public    | 所有类可见                         | 所有类可见（默认） |
| private   | 当前类可见                         | 当前类可见         |
| protected | 当前类、子类、同一包路径下的类可见 | 当前类、子类可见   |
| default   | 同一包路径下的类可见（默认）       | 无                 |
| internal  | 无                                 | 同一模块中的类可见 |

## 数据类与单例类

### 数据类

- 数据类通常要重写equals()、hashCode()、toString()方法

  在java中实现

  ```java
  public class Cellphone {
      String brand;
      double price;
  
      public Cellphone(String brand, double price) {
          this.brand = brand;
          this.price = price;
      }
  
      @Override
      public boolean equals(Object o) {
          if (this == o) return true;
          if (!(o instanceof Cellphone)) return false;
          Cellphone cellphone = (Cellphone) o;
          return Double.compare(cellphone.price, price) == 0 && Objects.equals(brand, cellphone.brand);
      }
  
      @Override
      public int hashCode() {
          return Objects.hash(brand, price);
      }
  
      @Override
      public String toString() {
          return "Cellphone{" +
                  "brand='" + brand + '\'' +
                  ", price=" + price +
                  '}';
      }
  }
  ```

  而在Kotlin中极其简单
  
  当使用了data关键字，就表明希望这一个类是数据类， Kotlin会根据主造函数中的参数帮你将equals()、hashCode()、toString()等固定且无实际逻辑意义的方法自动生成
  
  当一个类中没有任何代码的时候，还可以将尾部的大括号省略
  
  ```kotlin
  data class Cellphone(val brand: String, val price: Double)
  ```

### 单例类

- java中实现

  ```java
  public class Singleton {
      public static Singleton instance;
      private Singleton() {
      }
      private synchronized static Singleton getInstance() {
          if (instance == null) {
              return new Singleton();
          }
          return instance;
      }
      public void singletonTest() {
          System.out.println("singletonTest is called.");
      }
  }
  ```

  调用

  ```java
  Singleton singleton = Singleton.getInstance();
  singleton.singletonTest();
  ```

- 在Kotlin中创建一个单例的方式极其简单，只需要将class关键字改成object关键字即可

  快捷方式 New -> Kotlin File/Class 在弹出的对话框中选择Object

  ```kotlin
  Object Singleton {
      fun singletonTest() {
          println("singletonTest is called.")
      }
  }
  ```

  调用

  ```kotlin
  Singleton.singletonTest()
  ```

  这种写法虽然看上去像是静态方法的调用，但其实Kotlin在背后自动帮我们创建了一个Singleton类的实例，并且保证全局只会存在一个Singleton实例



# Lambda编程

## 集合的创建与遍历

**List集合：**

- ```kotlin
  val list = ArrayList<String>()
  list.add("Apple")
  list.add("Banana")
  list.add("Orange")
  list.add("Pear")
  list.add("Grape")
  ```

- 以上方法比较繁琐，Kotlin提供了内置的`listOf()`函数来简化初始化集合的写法

  ```kotlin
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape")
  ```

- 使用`for-in`遍历集合

  ```kotlin
  for (fruit in list){
      println(fruit)
  }
  ```

- `listOf()`函数创建的是一个不可变的集合，不可变就无法对其进行添加、修改或删除操作

  要创建可变的集合，使用`mutableListOf()`函数即可

  ```kotlin
  val list = mutableListOf<String>("Apple", "Banana", "Orange", "Pear", "Grape")
  list.add("Watermelon")
  println(list)
  ```

**Set集合：**

- Set集合和List集合用法类似，`setOf()`创建不可变集合，`mutableSetOf()`创建可变集合
- Set集合底层是使用hash映射机制来存放数据的，因此无法保证集合中的元素有序，这是与List最大的不同之处

**Map集合：**

- Map集合是一种键值对形式的数据结构，传统的Map用法是先创建一个Map实例，再将一个个键值对数据添加到Map中

  ```kotlin
  val map = HashMap<String, Int>()
  map.put("Apple", 1)
  map.put("Banana", 2)
  map.put("Orange", 3)
  map.put("Pear", 4)
  map.put("Grape", 5)
  ```

- 这种写法和Java相似，但在Kotlin中不推荐使用`put()`和`get()`方法来对Map进行添加和读取，而是更推荐一种类似于数组下标的语法结构

  比如，向Map中添加一条数据：`map["Apple"] = 1`，从Map中读取一条数据：`val number = map["Apple"]`

  ```kotlin
  // 优化之后
  val map = HashMap<String, Int>()
  map["Apple"] = 1
  map["Banana"] = 2
  map["Orange"] = 3
  map["Pear"] = 4
  map["Grape"] = 5
  ```

- 可以继续使用`mapOf()`和`mutableMapOf()`来继续简化Map的用法

  在mapOf中，可以直接传入初始化的键值对组合来完成对Map的创建

  ```kotlin
  val map = mapOf<String,Int>("Apple" to 1, "Banana" to 2, "Orange" to 3, "Pear" to 4, "Grape" to 5)
  ```
  
  这里看上去好像是用to关键字连接，其实to并不是关键字，而是infix函数
  
- 使用for-in遍历Map

  ```kotlin
  for ((fruit, number) in map) { // 将Map的键值对声明到一对括号里
      println("fruit is $fruit, number is $number")
  }
  ```

## 集合的函数式API

- Lambda表达式的语法结构：`{参数名1: 参数类型, 参数名2: 参数类型 -> 函数体}`

- `maxBy()`函数：

  maxBy函数接收的参数是一个Lambda类型的参数，并且会在遍历集合时将每次遍历的值作为参数传递给Lambda表达式

  maxBy的工作原理是根据传入的条件来遍历集合，从而找到该条件的最大值

  举例：找出集合中单词最长的水果

  ```kotlin
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon")
  val lambda = { fruit: String -> fruit.length }
  val maxLengthFruit = list.maxBy(lambda)
  ```

  直接将Lambda表达式传入函数当中

  ```kotlin
  val maxLengthFruit = list.maxBy({ fruit: String -> fruit.length })
  ```

  Kotlin规定，当Lambda是函数的最后一个参数时，可以将Lambda表达式移到括号外

  ```kotlin
  val maxLengthFruit = list.maxBy() { fruit: String -> fruit.length }
  ```

  如果Lambda参数是函数唯一一个参数的话，还可以将函数的括号省略

  ```kotlin
  val maxLengthFruit = list.maxBy { fruit: String -> fruit.length }
  ```

  利用Kotlin的推导机制，Lambda在大多数情况下不必声明参数类型

  ```kotlin
  val maxLengthFruit = list.maxBy { fruit -> fruit.length }
  ```

  当Lambda表达式只有一个参数时，可以使用it关键字来代替

  ```kotlin
  val maxLengthFruit = list.maxBy { it.length }
  ```

- `map()`函数：

  map函数用于将集合中的每个元素都映射成一个另外的值，映射规则在Lambda表达式中指定，最终返回一个新的集合

  举例：让所有水果名变成大写

  ```kotlin
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon")
  val newList = list.map { it.toUpperCase() }
  ```

- `filter()`函数：

  filter函数是用来过滤集合中的数据的，它可以单独使用，也可以配合map使用

  举例：保留五个字以内的水果

  ```kotlin
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon")
  val newList = list.filter { it.length <= 5 }.map { it.uppercase(Locale.getDefault()) }
  // 如果先调用map函数再调用filter函数，效率就会差很多，因为这样相当于把集合中所有的元素都进行一次映射转换后再过滤
  ```

- `any()`和`all()`函数：

  any函数用于判断集合中是否至少存在一个元素满足条件

  all函数用于判断集合中是否所有元素都满足指定条件

  ```kotlin
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape", "Watermelon")
  val anyResult = list.any { it.length <= 5} // true
  val allResult = list.all { it.length <= 5} // false
  ```

> 补充：

- 匿名函数

  匿名函数有类型，可以作为变量赋值给函数类型变量；匿名函数不需要return关键字返回数据，匿名函数会隐式返回最后一行语句

  ```kotlin
  val say: () -> String = {
      val hello = "hello"
      "say $hello"
  }
  ```

  匿名函数可以带一个或多个参数，参数的类型放在匿名函数的类型定义中，参数名则放在函数定义中

  ```kotlin
  val say: (String) -> String = { name ->
      val hello = "hello"
      "$name say $hello"
  }
  println(say("Jack"))
  ```

  只有一个参数的匿名函数，可以使用it代替参数名

  ```kotlin
  val say: (String) -> String = {
      val hello = "hello"
      "$it say $hello"
  }
  ```

  定义一个变量时，如果已把匿名函数作为变量赋值给它，就不需要显示指明变量类型

  ```kotlin
  val say = {
      val hello = "hello"
      "say $hello"
  }
  ```

  类型推断也支持带参数的匿名函数，但为了帮助编译器更准确地推断变量类型，匿名函数的参数名和参数类型必须有

  ```kotlin
  val say = { name: String, age: Int ->
      val hello = "hello"
      "$name is $age years old, say $hello"
  }
  ```

  

## Java函数式API

- 使用条件：

  如果在Kotlin代码中调用了一个Java方法，并且该方法接收一个Java单抽象方法接口参数，就可以使用函数式API

  Java单抽象方法接口指的是接口中只有一个待实现的方法，如果接口中有多个待实现的方法，则无法使用函数式API

- 使用方法，以Thread类的构造方法接收一个Runnable参数为例：

  ```java
  // 用Java实现
  new Therad(new Runnalble() {
      @Override
      public void run() {
          System.out.println("Thread is running")
      }
  }).start()；
  ```

  ```kotlin
  // 翻译成Kotlin版
  Thread(object : Runnable {
      override fun run() {
          println("Thread is running")
      }
  }).start()
  ```

  Ktolin中匿名类和Java中写法有些区别，Kotlin舍弃了new关键字，因此创建匿名类不能再使用new，而是该用了object关键字

  因为Thread类的构造方法符合函数式API，以下是精简代码

  ```kotlin
  Thread(Runnable {
      println("Thread is running")
  }).start()
  ```

  如果一个Java方法的参数列表中有且仅有一个Java单抽象方法接口参数，还可以省略接口名

  当然和之前函数式API用法类似，还可以将表达式移到括号外以及省略括号

  ```kotlin
  Thread {
      println("Thread is running")
  }.start()
  ```

- 在Android开发中使用：button注册点击事件

  ```kotlin
  button.setOnClickListener {
  }
  ```



# 空指针检查

## 可空类型系统

- Kotlin中默认所有参数和变量都不能为空，如果程序程序存在空指针的风险，编译时就会直接报错

- 可为空的类型系统：在类名的后面加上一个问号（比如Int 表示不可为空，Int?表示可为空）

  ```kotlin
  fun main() {}
  	doStudy(null)
  }
  fun doStudy(study: Study?) {
      // 直接这样也是不可编译的
      // study.readBook()
      // study.doHomework()
      // 解决方法
      if (study != null) {
          study.readBook()
          study.doHomework()
      }
  }
  ```

## 判空辅助工具

- `?.`操作符：

  当对象不为空时正常调用相应的方法，当对象为空时什么都不做

  ```kotlin
  if (a != null) {
      a.doSomething()
  }
  
  // 使用?.操作符可以简化成
  a?.doSomething()
  
  // 对doStudy()方法进行简化
  fun doStudy(study: Study?) {
      study?.readBook()
      study?.doHomework()
  }
  ```

- `?:`操作符：

  这个操作符左右两边各接收一个表达式，如果左边表达式的结果不为空就返回左边表达式的结果，否则就返回右边表达式的结果

  ```kotlin
  val c = if (a != null){
      a
  }else {
      b
  }
  // 使用?:操作符简化
  val c = a ?: b
  ```

- 举例，编写一个函数获取文本长度：

  ```kotlin
  fun getTextLength(text: String): Int {
      if (text != null) {
          return text.length
      }
      return 0
  }
  // 借助操作符简化
  fun getTextLength(text: String?) = text?.length ?: 0
  ```

- 如果想要进行强行编译，可以使用非空断言工具，在对象后面加上`!!`

  ```kotlin
  fun printUpperCase() {
      val upperCase = content!!.toUpperCase() // 可能会抛出空指针异常
      println(upperCase)
  }
  ```

- let函数：

  这个函数提供了函数式API的编程接口，并将原始调用对象作为参数传递到Lambda表达式中

  ```kotlin
  // 示例代码
  obj.let { obj2 -> // 这里为了防止变量重名，改为了obj2，但实际还是同一个对象
      // 具体业务逻辑
  }
  // 这里调用obj对象的let函数，然后Lambda表达式中的代码就会立即执行，并且这个obj对象本身还会作为参数传递到Lambda表达式中
  ```

  ```kotlin
  // 对doStudy()方法进行简化
  fun doStudy(study: Study?) {
      study?.let { stu ->
          stu.readBook()
          stu.doHomework()
      }
  }
  // Lambda表达式中只有一个参数时，可以不用声明参数，直接使用it关键字代替
  fun doStudy(study: Study?) {
      study?.let {
          it.readBook()
          it.doHomework()
      }
  }
  ```



# 标准函数和静态方法

## 标准函数

- Kotlin中的标准函数指的是`Standard.kt`文件中定义的函数

- let函数：主要作用就是配合`?.`操作符进行判空操作，详细看空指针检查

- with函数：

  with函数接收两个参数：第一个参数是一个任意类型的对象，第二个参数是一个Lambda表达式

  with函数会在Lambda表达式中提供第一个参数对象的上下文，并使用Lambda表达式的最后一行代码作为返回值返回

  ```kotlin
  val result = with(obj) {
      // 这里是obj的上下文
      "value" // with函数的返回值
  }
  ```

  它的作用是连续调用一个对象的多个方法时让代码变得精简

  ```kotlin
  // 不使用with
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape")
  val builder = StringBuilder()
  builder.append("Start eating fruits.\n")
  for (fruits in list) {
      builder.append(fruits).append("\n")
  }
  builder.append("Ate all fruits")
  val result = builder.toString()
  println(result)
  ```

  ```kotlin
  // 使用with函数精简
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape")
  val result = with(StringBuffer()){
      append("Start eating fruits.\n")
      for (fruits in list) {
          append(fruits).append("\n")
      }
      append("Ate all fruits")
      toString()
  }
  println(result)
  ```

- run函数：

  和with类似，但run函数通常不会直接调用，而是在某个对象的基础上调用

  run只接收一个Lambda参数，并且会在Lambda表达式中提供调用对象的上下文

  ```kotlin
  val result = obj.run {
  	// 这里是obj的上下文
      "value" // run函数的返回值
  }
  ```

  ```kotlin
  // 使用run改写
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape")
  val result = StringBuffer().run {
      append("Start eating fruits.\n")
      for (fruits in list) {
          append(fruits).append("\n")
      }
      append("Ate all fruits")
      toString()
  }
  println(result)
  ```

- apply函数

  和run类似，也要在某个函数上调用，只接收一个Lambda参数，也会在Lambda提供调用对象的上下文

  但apply无法指定返回值，而是自动返回调用对象本身

  ```kotlin
  val result = obj.apply {
      // 这里是obj的上下文
  }
  // result == obj
  ```

  ```kotlin
  // 使用apply改写
  val list = listOf<String>("Apple", "Banana", "Orange", "Pear", "Grape")
  val result = StringBuffer().apply{
      append("Start eating fruits.\n")
      for (fruits in list) {
          append(fruits).append("\n")
      }
      append("Ate all fruits")
  }
  println(result.toString())
  ```

## 定义静态方法

- 像工具类这种功能，Kotlin推荐使用单例类来创建

- ```kotlin
  object Util {
      fun doAction() {
          println("do action")
      }
  }
  ```

  这里`doAction()`方法虽然不是静态方法，但可以直接使用`Util.doAction()`调用

- 如果想让一个方法变成类似于静态方法调用的方式，就可以使用`companion object {}`包围方法

  ```kotlin
  class Util {
      companion object {
          fun doAction() {
              println("do action")
          }
      }
  }
  ```

  doAction()方法其实也并不是静态方法，companion object这个关键字实际上会在Util类的内部创建一个伴生类，而doAction()方法就是定义在这个伴生类里面的实例方法。只是Kotlin会保证Util类始终只会存在一个伴生类对象，因此调用Util.doAction()方法实际上就是调用了Util类中伴生对象的doAction()方法

- 如果想要真正的静态方法，有两种方法：注解和顶层方法

  注解：直接在单例类或companion object中的方法上加上@JvmStatic注解，就会成为真正的静态方法

  @JvmStatic只能加在单例类或companion object中，加在普通方法会报错

  ```kotlin
  companion object {
      @JvmStatic 
      fun doAction() {
          println("do action")
      }
  }
  ```

  顶层方法指的就是那些没有定义在任何类中的方法，Kotlin 编译器会将所有的顶层方法全部编译成静态方法

  在Kotlin中可以直接调用顶层方法，不用管包名路径，也不用创建实例，直接键入doSomething()即可

  在Java中调用顶层方法，因为Kotlin 编译器会自动创建一个叫作`文件名Kt` 的Java 类，所有调用的话就是`文件名Kt.doSomething()`



# 字符串操作-数字类型-标准库函数

## 字符串操作

- 字符串截取，substring函数支持IntRange类型（表示一个整数范围的类型）的参数，until创建的范围不包括上限值

  ```kotlin
  const val NAME = "Jimmy's friend"
  fun main() {
      val index = NAME.indexOf('\'')
      //val str = NAME.substring(0, index)
      val str = NAME.substring(0 until index)
      println(str)
  }
  ```

- Spit函数返回的是List集合数据，List集合又支持解构语法特性，它允许你在一个表达式里给多个变量赋值，解构常用来简化变量的赋值

  ```kotlin
  const val NAMES = "Jack,Jim,Tom"
  fun main() {
      val (Jack, Jim, Tom) = NAMES.split(",")
      println("$Jack $Jim $Tom")
  }
  ```

- replace字符串替换

  ```kotlin
  fun main() {
      // 加密替换一个字符串
      val str1 = "The people's Republic of China."
      // 第一个参数是正则表达式，用来决定要替换哪些字符
      // 第二个参数是匿名函数，用来确定该如何替换正则表达式搜索到的字符
      val str2 = str1.replace(Regex("[aeiou]")) {
          when(it.value){
              "a" -> "8"
              "e" -> "6"
              "i" -> "9"
              "o" -> "1"
              "u" -> "3"
              else -> it.value
          }
      }
      println(str1)
      println(str2)
  }
  ```

- 字符串比较

  在Kotlin中，用==检查两个字符串中的字符是否匹配，用===检查两个变量是否指向内存堆上同一对象，而在Java中==做引用比较，做结构比较时用equals方法

  ```kotlin
  fun main() {
      val str1 = "Jack"
      val str2 = "Jack"
      val str3 = "jack".capitalize()
      println(str1 == str2) //true
      println(str1 === str2) //true
      println(str1 === str3) //false
  }
  ```

- 遍历字符

  ```kotlin
  fun main() {
      "The People's Republic of China".forEach {
          print(it)
      }
  }
  ```

## 数字类型

- 安全转换函数

  Kotlin提供了toDoubleOrNull和toIntOrNulll这样的安全转换函数，如果数值不能正确转换，与其触发异常不如干脆返回null值

  ```kotlin
  fun main() {
      //val num1: Int = "8.687".toInt() // 抛出NumberFormatException
      val num1: Int? = "8.687".toIntOrNull() // 返回null
      println(num1)
  }
  ```

- Double转Int

  精度损失与四舍五入

  ```kotlin
  println(8.985.toInt()) // 8
  println(8.985.roundToInt()) // 9
  ```

- Double类型格式化

  格式化字符串是一串特殊字符，它决定该如何格式化数据

  ```kotlin
  val s = "%.2f".format(8.98765)
  println(s) // 8.99
  ```





