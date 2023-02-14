# Java Study Notes 中部分

> by.Xiao_Chen

因内容较多，JavaStudyNotes分为三部分，此篇为中部分：

- 上部分：初识Java、Java基础语法、面向对象初级、中级和高级部分
- 中部分：枚举、注解、异常、常用类（包装类、String、Math、Object、System、日期类等）、Lambda表达式、集合
- 下部分：泛型、图形界面、线程、IO流、网络编程、正则表达式、反射、数据库编程

笔记仅供参考，查找方法更适合去[JavaAPI文档](https://docs.oracle.com/javase/8/docs/api/)，[中文文档下载（密码:chen）](https://wwxg.lanzoub.com/b02pzrdha) 

一些教程推荐：

- [XiaoChen/JavaStudyNotes](https://gitee.com/gitee-xiaochen/java-study-notes/blob/master/JavaNotes.md)

- [菜鸟Java教程](https://www.runoob.com/java/java-tutorial.html)

- [Quick Reference Java 备忘清单](http://bbs.laoleng.vip/reference/docs/java.html)

- [廖雪峰Java教程](https://www.liaoxuefeng.com/wiki/1252599548343744)

- [鱼皮Java学习路线](https://luxian.yupi.icu/#/roadmap/Java%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF)



# 枚举和注解

## 枚举

### 实现方式

**自定义类实现枚举**

1. 构造器私有化
2. 本类内部创建一组对象
3. 可以提供get方法，但是不要提供set方法，因为枚举对象值通常为只读
4. 对外暴露象（通过为对象添加 public final static 修饰符）（对枚举对象/属性使用final + static共同修饰，可以实现底层优化）
5. 枚举对象通常使用全部大写，常量的命名规范
6. 枚举对象根据需要，也可以有多个属性

**使用 enum 关键字实现枚举**

1. 使用关键字enum替代class（当我们使用 enum 关键字开发一个枚举类时，默认会继承 Enum 类, 而且是一个 final 类）
2. `public static final 类名 常量名 = new 类名(实参列表);`使用`常量名(实参列表);`替换
3. 如果有多个常量（对象），使用 ,号间隔即可
4. 如果使用 enum 来实现枚举，要求将定义常量对象，写在前面第一行
5. 如果我们使用的是无参构造器，创建常量对象，则可以省略()

### enum常用方法

1. toString：Enum 类已经重写过了，返回的是当前对象名，子类可以重写该方法，用于返回对象的属性信息

2. name：返回当前对象名（常量名），子类中不能重写

3. ordinal：返回当前对象的位置号，默认从 0 开始

4. values：返回当前枚举类中所有的常量

   ```java
   Season[] values = Season.values();
   System.out.println("===遍历取出枚举对象(增强 for)====");
   for (Season season: values) {//增强 for 循环
       System.out.println(season);
   }
   ```

5. valueOf：将字符串转换成枚举对象，要求字符串必须为已有的常量名，否则报异常

   ```java
   //1. 根据你输入的 "AUTUMN" 到 Season 的枚举对象去查找
   //2. 如果找到了，就返回，如果没有找到，就报错
   Season autumn1 = Season.valueOf("AUTUMN");
   System.out.println("autumn1=" + autumn1);
   ```

6. compareTo：比较两个枚举常量，比较的就是编号

   ```java
   //就是把 Season.AUTUMN 枚举对象的编号 和 Season.SUMMER 枚举对象的编号比较
   /*
   public final int compareTo(E o) {
   	return self.ordinal - other.ordinal;
   }
   Season.AUTUMN 的编号[2] - Season.SUMMER 的编号[3]
   */
   System.out.println(Season.AUTUMN.compareTo(Season.SUMMER));
   ```

### enum实现接口

1. 使用 enum 关键字后，就不能再继承其它类了，因为 enum 会隐式继承 Enum，而 Java 是单继承机制

2. 枚举类和普通类一样，可以实现接口，如下形式：

   `enum 类名 implements 接口1,接口2{}`



## 注解

### 注解的理解

1. 注解(Annotation)也被称为元数据(Metadata)，用于修饰解释 包、类、方法、属性、构造器、局部变量等数据信息
2. 和注释一样，注解不影响程序逻辑，但注解可以被编译或运行，相当于嵌入在代码中的补充信息
3. 在 JavaSE 中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。在 JavaEE 中注解占据了更重要的角色，例如用来配置应用程序的任何切面，代替 java EE 旧版中所遗留的繁冗代码和 XML 配置等

### 基本介绍

使用 Annotation 时要在其前面增加 @ 符号，并把该 Annotation 当成一个修饰符使用，用于修饰它支持的程序元素

三个基本的 Annotation：

1. @Override：限定某个方法，是重写父类方法, 该注解只能用于方法
2. @Deprecated：用于表示某个程序元素(类, 方法等)已过时
3. @SuppressWarnings：抑制编译器警告

### 应用案例

#### @Override注解的案例

> @Override：限定某个方法，是重写父类方法, 该注解只能用于方法

1. @Override注解放在子类方法上，表示子类的方法时重写了父类方法

2. 如果没有写@Override还是重写了父类方法

3. @Override只能修饰方法，不能修饰其他类，包，属性等等

4. 如果写了@Override注解，编译器就会去检查该方法是否真的重写了父类的方法，如果的确重写了，则编译通过，如果没有构成重写，则编译错误

5. @Override的源代码：

   ```java
   //@interface 表示一个 注解类
   @Target(ElementType.METHOD)//@Target是修饰注解的注解，称为元注解
   @Retention(RetentionPolicy.SOURCE)
   public @interface Override {
   }
   ```

#### @Deprecated注解的案例

> @Deprecated：用于表示某个程序元素(类, 方法等)已过时

1. @Deprecated修饰某个元素, 表示该元素已经过时

2. 即不在推荐使用，但是仍然可以使用

3. @Deprecated可以修饰方法，类，字段，包，参数等等

4. @Deprecated的作用可以做到新旧版本的兼容和过渡

5. @Deprecated的源代码：

   ```java
   @Documented
   @Retention(RetentionPolicy.RUNTIME)
   @Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, PARAMETER, TYPE})
   public @interface Deprecated {
   }
   ```

#### @SuppressWarnings注解的案例

> @SuppressWarnings: 抑制编译器警告

1. 当我们不希望看到这些警告的时候，可以使用 SuppressWarnings 注解来抑制警告信息

2. 在{""} 中，可以写入你希望抑制(不显示)警告信息

3. 可以指定的警告类型有:

   all，抑制所有警告
   boxing，抑制与封装/拆装作业相关的警告
   cast，抑制与强制转型作业相关的警告
   dep-ann，抑制与淘汰注释相关的警告
   deprecation，抑制与淘汰的相关警告
   fallthrough，抑制与switch陈述式中遗漏break相关的警告
   finally，抑制与未传回finally区块相关的警告
   hiding，抑制与隐藏变数的区域变数相关的警告
   incomplete-switch，抑制与switch陈述式(enum case)中遗漏项目相关的警告
   javadoc，抑制与javadoc相关的警告
   nls，抑制与非nls字串文字相关的警告
   null，抑制与空值分析相关的警告
   rawtypes，抑制与使用raw类型相关的警告
   resource，抑制与使用Closeable类型的资源相关的警告
   restriction，抑制与使用不建议或禁止参照相关的警告
   serial，抑制与可序列化的类别遗漏serialVersionUID栏位相关的警告
   static-access，抑制与静态存取不正确相关的警告
   static-method，抑制与可能宣告为static的方法相关的警告
   super，抑制与置换方法相关但不含super呼叫的警告
   synthetic-access，抑制与内部类别的存取未最佳化相关的警告
   sync-override，抑制因为置换同步方法而遗漏同步化的警告
   unchecked，抑制与未检查的作业相关的警告
   unqualified-field-access，抑制与栏位存取不合格相关的警告
   unused，抑制与未用的程式码及停用的程式码相关的警告

4. 关于@SuppressWarnings作用范围是和放置的位置相关

5. @SuppressWarnings的源代码：

   ```java
   @Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
   @Retention(RetentionPolicy.SOURCE)
   public @interface SuppressWarnings {
       String[] value();
   }
   ```

### 元 Annotation(元注解)

> JDK 的元 Annotation 用于修饰其他 Annotation 

#### 元注解的种类

1. Retention：指定注解的作用范围，三种 SOURCE,CLASS,RUNTIME
2. Target：指定注解可以在哪些地方使用
3. Documented：指定该注解是否会在 javadoc 体现
4. Inherited：子类会继承父类注解

#### @Retention注解

> 只能用于修饰一个Annotation定义，用于指定该Annotation可以保留多长时间，@Rentention包含一个RetentionPolicy类型的成员变量, 使用@Rentention时必须为该value成员变量指定值

@Retention的三种值：

1. RetentionPolicy.SOURCE：编译器使用后，直接丢弃这种策略的注释
2. RetentionPolicy.CLASS：编译器将把注解记录在 class 文件中，当运行 Java 程序时， JVM 不会保留注解，这是默认值
3. RetentionPolicy.RUNTIME：编译器将把注解记录在 class 文件中，当运行 Java 程序时，JVM 会保留注解. 程序可以通过反射获取该注解

#### @Target注解

> 用于修饰Annotation定义，用于指定被修饰的Annotation能用于修饰哪些元素
>
> @Target也包含一个名为value的成员变量

源码：

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Target {
    ElementType[] value();
}
```

#### @Documented注解

> 用于指定被该元Annotation修饰的Annotation类将被javadoc工具提取成文档，即在生成文档时，可以看到该注解

源码：

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.ANNOTATION_TYPE)
public @interface Documented {
}
```

#### @Inherited注解

> 被它修饰的Annotation将具有继承性，如果某个类被@Inherited修饰的Annotation，则其子类将自动具有该注解
>

# 异常-Exception

## 异常介绍

**基本概念：**

Java语言中，将程序执行中发生的不正常情况称为“异常”

**执行过程中所发生的异常事件可以分为两大类：**

1. Error（错误）：Java虚拟机无法解决的严重问题。如：JVM系统内部错误、资源耗尽等严重情况。比如：StackOverFlowError[栈溢出]和OOM(out of memory)，Error是严重错误，程序会崩溃
2. Exception：其他因编程错误或偶然的外在因素导致的一般性问题，可以使用针对性的代码进行处理。例如空指针访问，试图读取不存在的文件，网络连接中断等等，Exception分为两大类：运行时异常[程序运行时，发生的异常]和编译时异常[编程时，编译器检查出的异常]



## 异常体系图

<img src="https://pb.nichi.co/habit-limit-question" style="zoom: 50%;" /> 

**小结：**

1. 异常分为两大类，运行时异常和编译时异常
2. 运行时异常，编译器检查不出来。一般是指编程时的逻辑错误，是程序员应该避免其出现的异常。java.lang.RuntimeException类及它的子类都是运行时异常
3. 对于运行时异常，可以不作处理，因为这类异常很普遍，若全处理可能会对程序的可读性和运行效率产生影响
4. 编译时异常，是编译器要求必须处置的异常



## 运行时异常

**常见的运行时异常：**

1. NullPointerException 空指针异常
2. ArithmeticException 数学运算异常
3. ArrayIndexOutOfBoundsException 数组下标越界异常
4. ClassCastException 类型转换异常
5. NumberFormatException 数字格式不正确异常

**举例：**

1. NullPointerException 空指针异常

   当应用程序试图在需要对象的地方使用 null 时，抛出该异常

   ```java
   public class NullPointerException_ {
       public static void main(String[] args) {
           String name = null;
           System.out.println(name.length());//抛出NullPointerException异常
       }
   }
   ```

2. ArithmeticException 数学运算异常

   当出现异常的运算条件时，抛出此异常

   ```java
   public class NumberFormatException_ {
       public static void main(String[] args) {
           int n1 = 20;
           int n2 = 0;
           System.out.println(n1 / n2);//抛出ArithmeticException异常
       }
   }
   ```

3. ArrayIndexOutOfBoundsException 数组下标越界异常

   用非法索引访问数组时抛出的异常，如果索引为负或大于等于数组大小，则该索引为非法索引

   ```java
   public class ArrayIndexOutOfBoundsException_ {
       public static void main(String[] args) {
           int[] arr = {1,2,4};
           for (int i = 0; i <= arr.length; i++) {
               System.out.println(arr[i]);
           }
       }
   }
   ```

4. ClassCastException 类型转换异常

   当试图将对象强制转换为不是实例的子类时，抛出该异常

   ```java
   public class ClassCastException_ {
       public static void main(String[] args) {
           A b = new B(); //向上转型
           B b2 = (B)b;//向下转型，这里是 OK
           C c2 = (C)b;//这里抛出 ClassCastException
       }
   }class A {}
   class B extends A {}
   class C extends A {}
   ```

5. NumberFormatException 数字格式不正确异常

   当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常（使用异常我们可以确保输入是满足条件数字）

   ```java
   public class NumberFormatException_ {
       public static void main(String[] args) {
           String name = "你好世界";
           //将 String 转成
           int int num = Integer.parseInt(name);//抛出 NumberFormatException
           System.out.println(num);//1234
       }
   }
   ```



## 编译异常

> 编译异常是指在编译期间，就必须处理的异常，否则代码不能通过编译

**常见的运行时异常：**

1. SQLException 操作数据库时，查询表可能发生异常
2. IOException 操作文件时，发生的异常
3. FileNotFoundException 当操作一个不存在的文件时，发生异常
4. ClassNotFoundException 加载类，而该类不存在时，异常
5. EOFException 操作文件，到文件未尾，发生异常
6. IllegalArguementException 参数异常



## 异常处理

> 异常处理就是当异常发生时，对异常处理的方式

**异常处理的方式：**

1. try-catch-finally

   程序员在代码捕获发生的异常，自行处理

   ```java
   try{
       //代码可能有异常
   }catch(Exception e){
       //捕获到异常
       //1.当异常发生时
       //2.系统将异常封装成Exception 对象 e，传递给catch
       //3.得到异常对象后，程序员，自己处理
       //4.注意，如果没有发生异常catch代码块不执行
   }finally{
       //1.不管try代码块是否有异常发生，始终要执行finally
       //2.所以，通常将释放资源的代码，放在finally
   }
   ```

2. throws

   将发生的异常抛出，交给调用者（方法）来处理

   <img src="https://pb.nichi.co/entire-only-salad" style="zoom: 40%;" /> 



## try-catch异常处理

**基本介绍：**

1.  Java提供try和catch块来处理异常，try块用于包含可能出错的代码，catch块用于处理try块中发生的异常，可以根据需要在程序中有多个try-catch块

2. 基本语法：

   ```java
   try{
       //可疑代码
       //将异常生成对应的异常对象，传递给catch块
   }catch(异常){
       //对异常的处理
   }
   //如果没有finally，语法可疑通过
   ```

**注意事项和使用细节：**

1. 如果异常发生了，则异常发生后面的代码不会执行，直接进入到catch块
2. 如果异常没有发生，则顺序执行try的代码块，不会进入到catch
3. 如果希望不管是否发生异常，都执行某段代码（比如关闭连接，释放资源等）则使用finally
4. 可以有多个catch语句，捕获不同的异常（进行不同的业务处理），要求父类异常在后，子类异常在前，比如（Exception 在后，NullPointerException前），如果发生异常，只会匹配一个catch
5. 可以进行try-finally配合使用，这种用法相当于没有捕获异常，因此程序会直接崩掉/退出。应用场景，就是执行一段代码，不管是否发生异常，都必须执行某个业务逻辑
6. 如果没有出现异常，则执行try块中所有语句，不执行catch块中语句，如果有finally，最后还需要执行finally里面的语句
7. 如果出现异常，则try块中异常发生后，try块剩下的语句不再执行。将执行catch块中的语句，如果有finally，最后还需要执行finally里面的语句



## throws异常处理

**基本介绍：**

1. 如果一个方法（中的语句执行时）可能生成某种异常，但是并不能确定如何处理这种异常，则此方法应显示地声明抛出异常，表明该方法将不对这些异常进行处理，而由该方法的调用者负责处理。
2. 在方法声明中用throws语句可以声明抛出异常的列表，throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类

**注意事项和使用细节：**

1. 对于编译异常，程序中必须处理，比如try-catch或者throws
2. 对于运行时异常，程序中如果没有处理，默认就是throws的方式处理
3. 子类重写父类的方法时，对抛出异常的规定：子类重写的方法，所抛出的异常类型要么和父类抛出的异常一致，要么为父类抛出的异常的类型的子类型
4. 在throws过程中，如果有方法try-catch，就相当于处理异常，就可以不必throws
5. 方法抛出的编译异常调用方法时必须解决，否则会报错，运行异常不要求做显示处理，因为有默认处理机制



## 自定义异常

> 当程序中出现了某些“错误”，但该错误信息并没有在Throwable子类中描述处理，这个时候可以自己设计异常类，用于描述该错误信息

**自定义异常的步骤：**

1. 定义类：自定义异常类名（程序员自己写），继承Exception或RuntimeException
2. 如果继承Exception，属于编译异常
3. 如果继承RuntimeException，属于运行异常（一般来说，继承RuntimeException，好处是可以做默认处理机制，即比较方便）

```java
public class CustomException {
    public static void main(String[] args) /*throws AgeException*/ {
        int age = 180; //要求范围在 18 – 120 之间，否则抛出一个自定义异常
        if(!(age >= 18 && age <= 120)) {
            //这里我们可以通过构造器，设置信息
            throw new AgeException("年龄需要在 18~120 之间");
        }
        System.out.println("你的年龄范围正确.");
    }
}
//自定义一个异常
//1. 一般情况下，我们自定义异常是继承 RuntimeException
//2. 即把自定义异常做成 运行时异常，好处时，我们可以使用默认的处理机制
//3. 即比较方便
class AgeException extends RuntimeException {
    public AgeException(String message) {//构造器
        super(message);
    }
}
```

**throw和throws的区别：**

| 名称   | 意义                     | 位置       | 后面跟的东西 |
| ------ | ------------------------ | ---------- | ------------ |
| throws | 异常处理的一种方式       | 方法声明处 | 异常类型     |
| throw  | 手动生成异常对象的关键字 | 方法体中   | 异常对象     |



# 常用类

## 包装类

### 包装类的分类

1. 针对八种基本数据类型相应的引用类型——包装类
2. 有了类的特点，就可以调用类中的方法

| 基本数据类型 | 包装类    |
| ------------ | --------- |
| boolean      | Boolean   |
| char         | Character |
| byte         | Byte      |
| short        | Short     |
| int          | Integer   |
| long         | Long      |
| float        | Float     |
| double       | Double    |

<img src="https://pb.nichi.co/cigar-endless-circle" style="zoom: 50%;" /> 

<img src="https://pb.nichi.co/select-desk-gold" style="zoom:50%;" /> 

<img src="https://pb.nichi.co/apology-endless-sure" style="zoom:50%;" /> 

###  包装类和基本数据的转换 

1. jdk5前采用手动装箱和拆箱方式，装箱：基本类型 -> 包装类型，反之，拆箱

   ```java
   //手动装箱 int->Integer
   int n1 = 100;
   Integer integer = new Integer(n1);
   Integer integer1 = Integer.valueOf(n1);
   //手动拆箱 Integer -> int
   int i = integer.intValue();
   ```

2. jdk5以后（含jdk5）采用自动装箱和拆箱方式

   ```java
   int n2 = 200;
   //自动装箱 int->Integer
   Integer integer2 = n2; //底层使用的是 Integer.valueOf(n2)
   //自动拆箱 Integer->int
   int n3 = integer2; //底层仍然使用的是 intValue()方法
   ```

3. 自动装箱底层调用的是valueOf方法，比如`Inerger.valueOf()`

### 包装类型和 String 类型的相互转换

```java
public class WrapperVSString {
    public static void main(String[] args) {
        //包装类(Integer)->String
        Integer i = 100;//自动装箱
        //方式 1
        String str1 = i + "";
        //方式 2
        String str2 = i.toString();
        //方式 3
        String str3 = String.valueOf(i);
        //String -> 包装类(Integer)
        String str4 = "12345";
        Integer i2 = Integer.parseInt(str4);//使用到自动装箱
        Integer i3 = new Integer(str4);//构造器
        System.out.println("ok~~");
    }
}
```

### Integer 类和 Character 类的常用方法 

```java
public class WrapperMethod {
    public static void main(String[] args) {
        System.out.println(Integer.MIN_VALUE); //返回最小值
        System.out.println(Integer.MAX_VALUE);//返回最大值
        System.out.println(Character.isDigit('a'));//判断是不是数字
        System.out.println(Character.isLetter('a'));//判断是不是字母
        System.out.println(Character.isUpperCase('a'));//判断是不是大写
        System.out.println(Character.isLowerCase('a'));//判断是不是小写
        System.out.println(Character.isWhitespace('a'));//判断是不是空格
        System.out.println(Character.toUpperCase('a'));//转成大写
        System.out.println(Character.toLowerCase('A'));//转成小写
    }
}
```

### 注意事项和使用细节

```java
public static void main(String[] args) {
    Integer i = new Integer(1);
    Integer j = new Integer(1);
    System.out.println(i == j); //False
    //所以，这里主要是看范围 -128 ~ 127 就是直接返回
    /*
    1. 如果 i 在 IntegerCache.low(-128)~IntegerCache.high(127),就直接从数组返回
    2. 如果不在 -128~127,就直接 new Integer(i)
    public static Integer valueOf(int i) {
    	if (i >= IntegerCache.low && i <= IntegerCache.high)
    		return IntegerCache.cache[i + (-IntegerCache.low)];
    	return new Integer(i);
    }
    */
    Integer m = 1; //底层 Integer.valueOf(1); -> 阅读源码
    Integer n = 1;//底层 Integer.valueOf(1);
    System.out.println(m == n); //T
    //所以，这里主要是看范围 -128 ~ 127 就是直接返回
    //否则，就 new Integer(xx);
    Integer x = 128;//底层 Integer.valueOf(1);
    Integer y = 128;//底层 Integer.valueOf(1);
    System.out.println(x == y);//False
    
    Integer i1=127;
    int i2=127;
    //只有有基本数据类型，判断的是值是否相同
    System.out.println(i11==i12);//T
    
    Integer i3=128;
    int i4=128;
    System.out.println(i3==i4);//T
	}
}
```



## String类

### String类的理解

1. String对象用于保存字符串，也就是一组字符序列

2. 字符串常量对象是用双引号括起的字符序列

3. 字符串的字符使用 Unicode 字符编码，一个字符（不区分字母还是汉字）占两个字节

4. String 类有很多构造器，构造器的重载

   `String s1 = new String();`

   `String s2 = new String(String original);`

   `String s3 = new String(char[] a);`

   `String s4 = new String(char[] a,int startIndex,int count);`

   `String s5 = new String(byte[] b);`

5. String 类实现了接口 Serializable[说明String 可以串行化，即可以在网络传输] 和 接口 Comparable [说明String 对象可以比较大小]

6. String 是 final 类，不能被其他的类继承

7. String 有属性 `private final char value[]; `用于存放字符串内容

   注意：value 是一个 final 类型， 不可以修改，即 value 不能指向新的地址，但是单个字符内容是可以变化

   ```java
   String name = "jack";
   name = "tom";//ok
   final char[] value = {'a','b','c'};
   char[] v2 = {'t','o','m'};
   value[0] = 'H';
   //value = v2; 错误！不可以修改 value 地址
   ```

### 创建String对象

- 方式一：直接赋值`String s1 ="abc”`

  先从常量池查看是否有"abc"数据空间，如果有，直接指向; 如果没有则重新创建，然后指向。s1最终指向的是常量池的空间地址方式

- 方式二：调用构造器`String s2 = new String("abc");`

  先在堆中创建空间，里面维护了value属性，指向常量池的"abc"空间，如果常量池没有"abc"，重新创建，如果有，直接通过value指向，最终指向的是堆中的空间地址

- 内存分布图：

  <img src="https://pb.nichi.co/original-person-add" style="zoom:50%;" /> 

### 其他知识点

- 当调用intern方法时，如果池已经包含一个等于此String对象的字符串（用equals(Object)方法确定），则返回池中的字符串。否则，将此String对象添加到池中，并返回此String对象的引用

  解读：b.intern()方法最终返回的是常量池的地址（对象）

### 字符串的特性

1. String是一个final类，代表不可变的字符序列
2. 字符串是不可变的，一个字符串对象一旦被分配，其内容是不可变的

```java
String s1 = "hello";//先检查常量池有没有hello，没有就在常量池创建一个hello并指向
s1 = "haha";//先检查常量池有没有haha，没有就创建一个haha并指向
//创建了两个对象
```

```java
String a = "hello" + "abc";
//只创建了一个对象，编译器优化，等价于String a = "helloabc";
```

```java
String a = "hello";
String b = "abc";
String c = a + b;//创建了几个对象
//底层调用StringBuilder sb = new StringBuilder(); sb.append(a); ab.apped(b);
//sb是在堆中，并且append是在原来字符串的基础上追加的
//String c1 = "ab" + "cd";常量相加，看的是池 String c1 = a + b;变量相加，是在堆中
```

```java
public class test01 {
    public static void main(String[] args) {
        A ex = new A();
        ex.change(ex.str, ex.ch);//调用ex.change方法
        System.out.print(ex.str + "and");//输出为cgz and
        System.out.println(ex.ch);//have
    }
}
class A{
    String str = new String("cgz");
    final char[] ch = {'j','a','v','a'};
    public void change(String str,char ch[]){
        str = "java";
        //ex.str首先将str指向ex.str，然后str = "java"就是将str取消指向ex.str
        //而是指向常量池中的"java"，并且ex.str不变
        ch[0] = 'h';
        //char ch[]就直接指向ex.ch的地址
        //ch[0]='h'就直接改变堆中的ex.ch的0下标字符变为h
        
        /*以下引用自B站弹幕
        调用方法栈中的ch通过地址找到数组,将内容改变
        这里我想了好久,和大家分享下思路,主要在于引用数据类型是地址传递
        数组用final修饰,指的是数组内容指向栈中main方法ch的引用不可更改,并不是指内容
        根据String不可变性来讲,对String重新赋值即返回新地址,此时,地址返给形参
        方法结束后,形参数组销毁,但内容已经发生变化,形参String指向地址改变,然后销毁
        */
    }
}

```

### String的常用方法

1. equals 区分大小写，判断内容是否相等

2. equalsIgnoreCase 忽略大小写的判断内容是否相等

3. length 获取字符的个数，字符串的长度

4. indexOf 获取字符在字符串对象中第一次出现的索引，索引从 0 开始，如果找不到，返回-1

5. lastIndexOf 获取字符在字符串中最后一次出现的索引，索引从 0 开始，如果找不到，返回-1

   ```java
   s1 = "wer@terwe@g@";
   index = s1.lastIndexOf('@');
   System.out.println(index);//11
   System.out.println("ter 的位置=" + s1.lastIndexOf("ter"));//4
   ```

6. substring 截取指定范围的子串

   ```java
   String name = "hello,张三";
   //下面 name.substring(6) 从索引 6 开始截取后面所有的内容
   System.out.println(name.substring(6));//截取后面的字符
   //name.substring(0,5)表示从索引 0 开始截取，截取到索引 5-1=4 位置 即[0,5) 左闭右开
   System.out.println(name.substring(2,5));//llo
   ```

7. toUpperCase 转换成大写

8. toLowerCase 转换成小写

9. concat 拼接字符串

10. replace 替换字符串中的字符

    ```java
    String str1 = "jack,java,jack,java";
    // str1.replace() 方法执行后，返回的结果才是替换过的，注意对 str1 没有任何影响
    String str2 = str1.replace("jack","java");//将所有的jack替换成java
    System.out.println(str1);//jack,java,jack,java
    System.out.println(str2);//java,java,java,java
    ```

11. split 分割字符串，对于某些分割字符，我们需要 转义比如` | \\`等

    ```java
    String poem = "锄禾日当午,汗滴禾下土,谁知盘中餐,粒粒皆辛苦";
    // 1. 以 , 为标准对 poem 进行分割 , 返回一个数组
    // 2. 在对字符串进行分割时，如果有特殊字符，需要加入 转义符 \
    String[] split = poem.split(",");
    poem = "E:\\aaa\\bbb";
    split = poem.split("\\\\");
    System.out.println("==分割后内容===");
    for (int i = 0; i < split.length; i++) {
        System.out.println(split[i]);
    }
    ```

12. .toCharArray 转换成字符数组

    ```java
    s = "happy";
    char[] chs = s.toCharArray();
    for (int i = 0; i < chs.length; i++) {
        System.out.println(chs[i]);
    }
    ```

13. compareTo 比较两个字符串的大小，如果前者大，则返回正数，后者大，则返回负数，如果相等，返回 0

    ```java
    // (1) 如果长度相同，并且每个字符也相同，就返回 0
    // (2) 如果长度相同或者不相同，但是在进行比较时，可以区分大小
    // 就返回 if (c1 != c2) {
    // 			return c1 - c2;
    // 		 }
    // (3) 如果前面的部分都相同，就返回 str1.len - str2.len
    String a = "jcck";// len = 3
    String b = "jack";// len = 4
    System.out.println(a.compareTo(b)); // 返回值是 'c' - 'a' = 2 的值
    ```

14. format 格式字符串

    ```java
    String name = "john";
    int age = 10;
    double score = 56.857;
    char gender = '男';
    //将所有的信息都拼接在一个字符串.
    String info = "我的姓名是" + name + "年龄是" + age + ",
        成绩是" + score + "性别是" + gender + "。希望大家喜欢我！ ";
    System.out.println(info);
    //1. %s , %d , %.2f %c 称为占位符
    //2. 这些占位符由后面变量来替换
    //3. %s 表示后面由 字符串来替换
    //4. %d 是整数来替换
    //5. %.2f 表示使用小数来替换，替换后，只会保留小数点两位, 并且进行四舍五入的处理
    //6. %c 使用 char 类型来替换
    String formatStr = "我的姓名是%s 年龄是%d，成绩是%.2f 性别是%c.希望大家喜欢我！";
    String info2 = String.format(formatStr, name, age, score, gender);
    System.out.println("info2=" + info2);
    ```



## StringBuffer类

### 基本介绍

- java.lang.StringBuffer代表可变的字符序列，可以对字符串内容进行增删
- 很多方法与String相同，但StringBuffer是可变长度的
- StringBuffer是一个容器
- StringBuffer 的直接父类 是 AbstractStringBuilder
- StringBuffer 实现了 Serializable，即 StringBuffer 的对象可以串行化
- 在父类中 AbstractStringBuilder 有属性 char[] value，没有 final 修饰，所以该 value 数组存放字符串内容存放在堆中，且可修改
- StringBuffer 是一个 final 类，不能被继承
- 因为 StringBuffer 字符内容是存在 char[] value, 所以变化(增加/删除)不用每次都更换地址(即不是每次创建新对象)， 所以效率高于 String

### String和SringBuffer相互转换

```java
//String——>StringBuffer
String str = "hello tom";
//方式 1 使用构造器
//注意： 返回的才是 StringBuffer 对象，对 str 本身没有影响
StringBuffer stringBuffer = new StringBuffer(str);
//方式 2 使用 append 方法
StringBuffer stringBuffer1 = new StringBuffer();
stringBuffer1 = stringBuffer1.append(str);

//StringBuffer ->String
StringBuffer stringBuffer3 = new StringBuffer("hello jack");
//方式 1 使用 StringBuffer 提供的 toString 方法
String s = stringBuffer3.toString();
//方式 2 使用构造器来搞定
String s1 = new String(stringBuffer3);
```

### StringBuffer的常用方法

```java
public class StringBufferMethod {
    public static void main(String[] args) {
        StringBuffer s = new StringBuffer("hello");
        //增
        s.append(',');// "hello,"
        s.append("张三丰");//"hello,张三丰"
        s.append("赵敏").append(100).append(true).append(10.5);
        System.out.println(s);//"hello,张三丰赵敏100true10.5
        
        //删
        //删除索引为>=start && <end 处的字符
        s.delete(11, 14);//删除 11~14 的字符 [11, 14)
        System.out.println(s);//"hello,张三丰赵敏 true10.5"
        
        //改
        s.replace(9, 11, "周芷若");//使用 周芷若 替换 索引 9-11 的字符 [9,11)
        System.out.println(s);//"hello,张三丰周芷若true10.5"
        
        //查
        //查找指定的子串在字符串第一次出现的索引，如果找不到返回-1
        int indexOf = s.indexOf("张三丰");
        System.out.println(indexOf);//6
        
        //插
        s.insert(9, "赵敏");//在索引为 9 的位置插入 "赵敏",原来索引为 9 的内容自动后移
        System.out.println(s);//"hello,张三丰赵敏周芷若 true10.5"
        
        //长度
        System.out.println(s.length());//22 -> 底层重写了length()方法
        System.out.println(s);
    }
}
```



## StringBuilder类

### 基本介绍

1. 一个可变的字符序列。此类提供一个与StringBuffer兼容的API，但不保证同步（StringBuilder不是线程安全）。该类被设计用作StringBuffer的一个简易替换，用在字符串缓冲区被单个线程使用的时候。如果可能，建议优先采用该类。因为在大多数实现中，它比StringBuffer要快。
2. 在StringBuilder上的主要操作是append和insert方法，可以重载这些方法，以接受任意类型的数据。

### StringBuilder的常用方法

> StringBuilder 和 StringBuilder均代表可变的字符序列，方法是一样的，所以使用和StringBuilder一样

- StringBuilder 继承 AbstractStringBuilder 类
- 实现了 Serializable，说明 StringBuilder 对象是可以串行化(对象可以网络传输,可以保存到文件) 
- StringBuilder 是 final 类，不能被继承
- StringBuilder 对象字符序列仍然是存放在其父类 AbstractStringBuilder 的 char[] value; 因此，字符序列是堆中
- StringBuilder 的方法，没有做互斥的处理，即没有 synchronized 关键字，因此在单线程的情况下使用

### String、StringBuffer和StringBuilder的比较

1. StringBuilder 和 StringBuffer 非常类似，均代表可变的字符序列，而且方法也一样

2. String：不可变字符序列，效率低，但是复用率高

3. StringBuffer：可变字符序列、效率较高(增删)、线程安全

4. StringBuilder：可变字符序列、效率最高、线程不安全

5. String使用注意说明：

   string s="a";//创建了一个字符串

   s +"b”://实际上原来的"a"字符串对象已经丢弃了，现在又产生了一个字符串s+"b”(也就是”ab”)。如果多次执行这些改变串内容的操作，会导致大量副本字符串对象存留在内存中，降低效率。如果这样的操作放到循环中，会极大影响程序的性能 =>结论：如果我们对String 做大量修改,不要使用String

**String、StringBuffer和StringBuilder的效率测试：**

```java
public class StringVsStringBufferVsStringBuilder {
    public static void main(String[] args) {
        long startTime = 0L;
        long endTime = 0L;
        StringBuffer buffer = new StringBuffer("");
        startTime = System.currentTimeMillis();
        for (int i = 0; i < 80000; i++) {//StringBuffer 拼接 20000 次
            buffer.append(String.valueOf(i));
        }
        endTime = System.currentTimeMillis();
        System.out.println("StringBuffer 的执行时间：" + (endTime - startTime));
        
        StringBuilder builder = new StringBuilder("");
        startTime = System.currentTimeMillis();
        for (int i = 0; i < 80000; i++) {//StringBuilder 拼接 20000 次
            builder.append(String.valueOf(i));
        }
        endTime = System.currentTimeMillis();
        System.out.println("StringBuilder 的执行时间：" + (endTime - startTime));
        
        String text = "";
        startTime = System.currentTimeMillis();
        for (int i = 0; i < 80000; i++) {//String 拼接 20000
            text = text + i;
        }
        endTime = System.currentTimeMillis();
        System.out.println("String 的执行时间：" + (endTime - startTime));
    }
}
```

**String、StringBuffer和StringBuilder的选择：**

1. 如果字符串存在大量的修改操作，一般使用StringBuffer或StringBuilder
2. 如果字符串存在大量的修改操作，并在单线程的情况，使用StringBuilder
3. 如果字符串存在大量的修改操作，并在多线程的情况，使用StringBuffer
4. 如果我们字符串很少修改，被多个对象引用，使用String



### StringJoiner类
- JDK8出现的一个可变的操作字符串的容器，可以高效，方便的拼接字符串
- 在拼接的时候，可以指定间隔符号，开始符号，结束符号
- StringJoiner跟StringBuilder一样，也可以看成是一个容器，创建之后里面的内容是可变的
- 作用：提高字符串的操作效率，而且代码编写特别简洁，但是目前市场上很少有人用
- JDK8出现的

**构造方法：**

| 方法名                                            | 说明                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| public StringJoiner(间隔符号)                     | 创建一个StringJoiner对象，指定拼接时的间隔符号               |
| public StringJoiner(间隔符号，开始符号，结束符号) | 创建一个StringJoiner对象，指定拼接时的间隔符号、开始符号、结束符号 |

**方法：**

| 方法名                              | 说明                                         |
| ----------------------------------- | -------------------------------------------- |
| public StringJoiner add(添加的内容) | 添加数据，并返回对象本身                     |
| public int length()                 | 返回长度（字符出现的个数）                   |
| public String toString()            | 返回一个字符串（该字符串就是拼接之后的结果） |



## Math类

> Math类包含于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数

**常用方法：**

1. abs 绝对值

   `Math.abs(-9)//9`

2. pow 求幂

   `Math.pow(2,4)//2的4次方 16`

3. ceil 向上取整，返回 >= 该参数的最小整数(转成double)

   `Math.ceil(3.9)//4.0`

4. floor 向下取整，返回 <= 该参数的最大整数(转成double)

   `Math.floor(4.001)//4`

5. round 四舍五入 就等价于`Math.floor(该参数+0.5)`

   `Math.round(5.51)//6`

6. sqrt 求开方(返回的值为double)

   `Math.sqrt(9.0)//3.0`

7. random 求随机数 random 返回的是 0 <= x < 1 之间的一个随机小数

   ```java
   // 思考：请写出获取 a-b 之间的一个随机整数,a,b 均为整数 ，比如 a = 2, b=7
   // 即返回一个数 x 2 <= x <= 7
   //Math.random() * (b-a) 返回的就是 0 <= 数 <= b-a
   // (1) (int)(a) <= x <= (int)(a + Math.random() * (b-a +1) )
   // (2) 使用具体的数给小伙伴介绍 a = 2 b = 7
   // (int)(a + Math.random() * (b-a +1) ) = (int)( 2 + Math.random()*6)
   // Math.random()*6 返回的是 0 <= x < 6 小数
   // 2 + Math.random()*6 返回的就是 2<= x < 8 小数
   // (int)(2 + Math.random()*6) = 2 <= x <= 7
   // (3) 公式就是 (int)(a + Math.random() * (b-a +1) )
   for(int i = 0; i < 100; i++) {
       System.out.println((int)(2 + Math.random() * (7 - 2 + 1)));
   }
   ```

8. max , min 返回最大值和最小值

   `Math.min(1, 9)` `Math.max(45, 90)`



## Runtime类

> Runtime表示当前虚拟机的运行环境

1. `public static Runtime getRuntime()` 当前系统的运行环境对象
2. `public void exit(int status)` 停止虚拟机
3. `public int availableProcessors()` 获得CPU的线程数
4. `public long maxMemory()` JVM能从系统中获取总内存大小(单位byte)
5. `public long totalMemory()`JVM已经从系统中获取总内存大小(单位byte)
6. `public long freeMemory()` JVM剩余内存大小(单位byte)
7. `public Process exec(String command)` 运行cmd命令



## Object类

> Object是Java中的顶级父类。所有的类都直接或间接的继承于Object类

1. `public Object()` 无参构造
2. `public String toString()` 返回对象的字符串表示形式
3. `public boolean equals(object obj)` 比较两个对象是否相等
4. `protected object clone(int a)` 对象克隆



## Arrays类

> Arrays里面包含了一系列静态方法，用于管理或操作数组

**常用方法：**

1. toString 返回数组的字符串形式

   `Arrays.toString(arr)`

2. sort 排序（自然排序和定制排序）

   ```java
   Integer arr[] = {1, -1, 7, 0, 89};
   //1. 可以直接使用冒泡排序 , 也可以直接使用 Arrays 提供的 sort 方法排序
   //2. 因为数组是引用类型，所以通过 sort 排序后，会直接影响到 实参 arr
   //3. sort 重载的，也可以通过传入一个接口 Comparator 实现定制排序
   //4. 调用 定制排序 时，传入两个参数 (1) 排序的数组 arr
   // (2) 实现了 Comparator 接口的匿名内部类 , 要求实现 compare 方法
   //5. 先演示效果，再解释
   //6. 这里体现了接口编程的方式 , 看看源码，就明白
   // 源码分析
   //(1) Arrays.sort(arr, new Comparator()
   //(2) 最终到 TimSort 类的 private static <T> void binarySort(T[] a, int lo, int hi, int start,Comparator<? super T> c)()
   //(3) 执行到 binarySort 方法的代码, 会根据动态绑定机制 c.compare()执行我们传入的
   // 匿名内部类的 compare ()
   // 	while (left < right) {
   // 		int mid = (left + right) >>> 1;
   // 		if (c.compare(pivot, a[mid]) < 0)
   // 			right = mid;
   // 		else
   // 			left = mid + 1;
   // 		}
   //(4) new Comparator() {
   // 					@Override
   // 					public int compare(Object o1, Object o2) {
   // 						Integer i1 = (Integer) o1;
   // 						Integer i2 = (Integer) o2;
   // 						return i2 - i1;
   // 					}
   // 		}
   //(5) public int compare(Object o1, Object o2) 返回的值>0 还是 <0
   // 会影响整个排序结果, 这就充分体现了 接口编程+动态绑定+匿名内部类的综合使用
   // 将来的底层框架和源码的使用方式，会非常常见
   //Arrays.sort(arr);// 默认排序方法
   //定制排序
   Arrays.sort(arr, new Comparator() {
       @Override
       public int compare(Object o1, Object o2) {
           Integer i1 = (Integer) o1;
           Integer i2 = (Integer) o2;
           return i2 - i1;
       }
   });
   System.out.println("===排序后===");
   System.out.println(Arrays.toString(arr));
   ```

3. binarySearch 通过二分搜索法进行查找，要求必须排好序

   ```java
   Integer[] arr = {1, 2, 90, 123, 567};
   // binarySearch 通过二分搜索法进行查找，要求必须排好
   //1. 使用 binarySearch 二叉查找
   //2. 要求该数组是有序的. 如果该数组是无序的，不能使用 binarySearch
   //3. 如果数组中不存在该元素，就返回 return -(low + 1);// key not found.
   int index = Arrays.binarySearch(arr, 567);
   System.out.println("index=" + index);
   ```

4. copyOf 数组元素的复制

   ```java
   //1. 从 arr 数组中，拷贝 arr.length 个元素到 newArr 数组中
   //2. 如果拷贝的长度 > arr.length 就在新数组的后面 增加 null
   //3. 如果拷贝长度 < 0 就抛出异常 NegativeArraySizeException
   //4. 该方法的底层使用的是 System.arraycopy()
   Integer[] newArr = Arrays.copyOf(arr, arr.length);
   System.out.println("==拷贝执行完毕后==");
   System.out.println(Arrays.toString(newArr));
   ```

5. fill 数组元素的填充

   ```java
   Integer[] num = new Integer[]{9,3,2};
   //使用 99 去填充 num 数组，可以理解成是替换原理的元素
   Arrays.fill(num, 99);
   System.out.println("==num 数组填充后==");
   System.out.println(Arrays.toString(num));
   ```

6. equals 比较两个数组元素内容是否完全一致

   ```java
   //1. 如果 arr 和 arr2 数组的元素一样，则方法 true;
   //2. 如果不是完全一样，就返回 false
   boolean equals = Arrays.equals(arr, arr2);
   System.out.println("equals=" + equals);
   ```

7. asList 将一组值，转换成 list

   ```java
   //1. asList 方法，会将 (2,3,4,5,6,1)数据转成一个 List 集合
   //2. 返回的 asList 编译类型 List(接口)
   //3. asList 运行类型 java.util.Arrays#ArrayList, 是 Arrays 类的
   //   静态内部类 private static class ArrayList<E> extends AbstractList<E>implements RandomAccess, java.io.Serializable
   List asList = Arrays.asList(2,3,4,5,6,1);
   System.out.println("asList=" + asList);
   System.out.println("asList 的运行类型" + asList.getClass());
   ```



## System类

> System也是一个工具类，提供了一些与系统相关的方法

1. `public static void exit(int status)` 终止当前运行的Java虚拟机

   0：表示当前虚拟机是正常停止
   非0：表示当前虚拟机异常停止

2. `public static long currentTimeMillis()` 返回当前系统的时间毫秒值形式

   时间原点：1970年1月1日 08:00:00

3. `public static void arraycopy(数据源数组,起始索引,目的地数组,起始索引,拷贝个数)` 数组拷贝

1. exit 退出当前程序

   ```java
   //1. exit(0) 表示程序退出
   //2. 0 表示一个状态 , 正常的状态
   System.exit(0);
   ```

2. arraycopy 复制数组元素，比较适合底层调用，一般使用Arrays.copyOf完成复制数组

   ```java
   int[] src={1,2,3};
   int[] dest = new int[3];// dest 当前是 {0,0,0}
   //主要是搞清楚这五个参数的含义
   //     src：源数组
   //     * @param      src      the source array.
   //     srcPos：从源数组的哪个索引位置开始拷贝
   //     * @param      srcPos   starting position in the source array.
   //     dest：目标数组，即把源数组的数据拷贝到哪个数组
   //     * @param      dest     the destination array.
   //     destPos：把源数组的数据拷贝到目标数组的哪个索引
   //     * @param      destPos  starting position in the destination data.
   //     length：从源数组拷贝多少个数据到目标数组
   //     * @param      length   the number of array elements to be copied.
   System.arraycopy(src, 0, dest, 0, src.length);// int[] src={1,2,3};
    System.out.println("dest=" + Arrays.toString(dest));//[1, 2, 3]
   ```

3. currentTimeMillens 返回当前时间距离1970-1-1的毫秒数

   `System.currentTimeMillis()`

4. gc 运行垃圾回收机制

   `System.gc();`



## BigInteger和BigDecimal类

> BigInteger适合保存比较大的整型
>
> BigDecimal适合保存精度更高的浮点型

**常用方法：**

1. add 加
2. subtract 减
3. multiply 乘
4. divide 除

```java
import java.math.BigInteger;
public class BigInteger_ {
    public static void main(String[] args) {

        //当我们编程中，需要处理很大的整数，long 不够用
        //可以使用BigInteger的类来搞定
		//long l = 23788888899999999999999999999l;
		//System.out.println("l=" + l);
        BigInteger bigInteger = new BigInteger("23788888899999999999999999999");
        BigInteger bigInteger2 = new BigInteger("100");
        System.out.println(bigInteger);
        //1. 在对 BigInteger 进行加减乘除的时候，需要使用对应的方法，不能直接进行 + - * /
        //2. 可以创建一个 要操作的 BigInteger 然后进行相应操作
        BigInteger add = bigInteger.add(bigInteger2);
        System.out.println(add);//加
        BigInteger subtract = bigInteger.subtract(bigInteger2);
        System.out.println(subtract);//减
        BigInteger multiply = bigInteger.multiply(bigInteger2);
        System.out.println(multiply);//乘
        BigInteger divide = bigInteger.divide(bigInteger2);
        System.out.println(divide);//除
    }
}
```

```java
import java.math.BigDecimal;
public class BigDecimal_ {
    public static void main(String[] args) {
        //当我们需要保存一个精度很高的数时，double 不够用
        //可以是 BigDecimal
		//double d = 1999.11111111111999999999999977788d;
		//System.out.println(d);
        BigDecimal bigDecimal = new BigDecimal("1999.11111111111999999999999977788");
        BigDecimal bigDecimal2 = new BigDecimal("3");
        System.out.println(bigDecimal);
        //1. 如果对 BigDecimal进行运算，比如加减乘除，需要使用对应的方法
        //2. 创建一个需要操作的 BigDecimal 然后调用相应的方法即可
        System.out.println(bigDecimal.add(bigDecimal2));
        System.out.println(bigDecimal.subtract(bigDecimal2));
        System.out.println(bigDecimal.multiply(bigDecimal2));
        //System.out.println(bigDecimal.divide(bigDecimal2));//可能抛出异常ArithmeticException
        //在调用divide 方法时，指定精度即可. BigDecimal.ROUND_CEILING
        //如果有无限循环小数，就会保留 分子 的精度
        System.out.println(bigDecimal.divide(bigDecimal2, BigDecimal.ROUND_CEILING));
    }
}
```



## 日期类

### 第一代日期类

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
public class Date01 {
    public static void main(String[] args) throws ParseException {
        //1. 获取当前系统时间
        //2. 这里的Date 类是在java.util包
        //3. 默认输出的日期格式是国外的方式, 因此通常需要对格式进行转换
        Date d1 = new Date(); //获取当前系统时间
        System.out.println("当前日期=" + d1);
        Date d2 = new Date(9234567); //通过指定毫秒数得到时间
        System.out.println("d2=" + d2); //获取某个时间对应的毫秒数
        //1. 创建 SimpleDateFormat对象，可以指定相应的格式
        //2. 这里的格式使用的字母是规定好，不能乱写
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss E");
        String format = sdf.format(d1); // format:将日期转换成指定格式的字符串
        System.out.println("当前日期=" + format);
        //1. 可以把一个格式化的String 转成对应的 Date
        //2. 得到Date 仍然在输出时，还是按照国外的形式，如果希望指定格式输出，需要转换
        //3. 在把String->Date，使用的sdf格式需要和你给的String的格式一样，否则会抛出转换异常
        String s = "1996年01月01日 10:20:30 星期一";
        Date parse = sdf.parse(s);
        System.out.println("parse=" + sdf.format(parse));
    }
}
```

### 第二代日期类

> 第二代日期类主要是Calendar（日历）

```java
import java.util.Calendar;
public class Calendar_ {
    public static void main(String[] args) {
        //1. Calendar是一个抽象类， 并且构造器是private
        //2. 可以通过 getInstance() 来获取实例
        //3. 提供大量的方法和字段提供给程序员
        //4. Calendar没有提供对应的格式化的类，因此需要程序员自己组合来输出(灵活)
        //5. 如果我们需要按照 24小时进制来获取时间，Calendar.HOUR ==改成=> Calendar.HOUR_OF_DAY
        Calendar c = Calendar.getInstance(); //创建日历类对象//比较简单，自由
        System.out.println("c=" + c);
        //获取日历对象的某个日历字段
        System.out.println("年：" + c.get(Calendar.YEAR));
        // 这里为什么要 + 1, 因为Calendar 返回月时候，是按照 0 开始编号
        System.out.println("月：" + (c.get(Calendar.MONTH) + 1));
        System.out.println("日：" + c.get(Calendar.DAY_OF_MONTH));
        System.out.println("小时：" + c.get(Calendar.HOUR));
        System.out.println("分钟：" + c.get(Calendar.MINUTE));
        System.out.println("秒：" + c.get(Calendar.SECOND));
        //Calender 没有专门的格式化方法，所以需要程序员自己来组合显示
        System.out.println(c.get(Calendar.YEAR) + "年" + (c.get(Calendar.MONTH) + 1) + "月" + c.get(Calendar.DAY_OF_MONTH) + "日" + c.get(Calendar.HOUR_OF_DAY) + "时" + c.get(Calendar.MINUTE) + "分" + c.get(Calendar.SECOND) + "秒");
    }
}
```

### 第三代日期类

#### 前两代日期类的不足

- JDK 1.0中包含了一个java.util.Date类，但是它的大多数方法已经在JDK 1.1引入Calendar类之后被弃用了
- 而Calendar也存在问题是：
  1. 可变性：像日期和时间这样的类应该是不可变的
  2. 偏移性：Date中的年份是从1900开始的，而月份都从0开始
  3. 格式化：格式化只对Date有用，Calendar则不行
  4. 此外，它们也不是线程安全的；不能处理闺秒等（每隔2天，多出1s）

#### 第三代日期类

> LocalDate(日期/年月日)、LocalTime(时间/时分秒)、LocalDateTime(日期时间/年月日时分秒)，在JDK8加入

- LocalDate只包含日期，可以获取日期字段
- LocalTime只包含时间，可以获取时间字段
- LocalDateTime包含日期+时间，可以获取日期和时间字段

```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.format.DateTimeFormatter;
public class LocalDate_ {
    public static void main(String[] args) {
        //第三代日期
        //1. 使用now() 返回表示当前日期时间的 对象
        LocalDateTime ldt = LocalDateTime.now();//LocalDate.now();//LocalTime.now()
        System.out.println(ldt);
        //2. 使用DateTimeFormatter 对象来进行格式化
        // 创建 DateTimeFormatter对象
        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH时mm分ss秒");
        String format = dateTimeFormatter.format(ldt);
        System.out.println("格式化的日期=" + format);

        System.out.println("年=" + ldt.getYear());
        System.out.println("月=" + ldt.getMonth());
        System.out.println("月=" + ldt.getMonthValue());
        System.out.println("日=" + ldt.getDayOfMonth());
        System.out.println("时=" + ldt.getHour());
        System.out.println("分=" + ldt.getMinute());
        System.out.println("秒=" + ldt.getSecond());

        LocalDate now = LocalDate.now(); //可以获取年月日
        LocalTime now2 = LocalTime.now();//获取到时分秒

        //提供 plus 和 minus方法可以对当前时间进行加或者减
        //看看890天后，是什么时候 把 年月日-时分秒输出
        LocalDateTime localDateTime = ldt.plusDays(890);
        System.out.println("890天后=" + dateTimeFormatter.format(localDateTime));

        //看看在 3456分钟前是什么时候，把 年月日-时分秒输出
        LocalDateTime localDateTime2 = ldt.minusMinutes(3456);
        System.out.println("3456分钟前 日期=" + dateTimeFormatter.format(localDateTime2));
    }
}
```

#### Instant时间戳

- 类似于Date

- 提供了一系列和Date类转换的方式

  - Instant ——> Date：

    `Date date = Date.from(instant);`

  - Date ——> Instant：

    `Instant instant = date.toInstant();`

```java
import java.time.Instant;
import java.util.Date;
public class Instant_ {
    public static void main(String[] args) {
        //1.通过 静态方法 now() 获取表示当前时间戳的对象
        Instant now = Instant.now();
        System.out.println(now);
        //2. 通过 from 可以把 Instant转成 Date
        Date date = Date.from(now);
        //3. 通过 date的toInstant() 可以把 date 转成Instant对象
        Instant instant = date.toInstant();
    }
}
```

#### 更多方法

- 检查重复事件是否是闺年
- 增加日期的某个部分
- 使用plus方法测试增加时间的某个部分
- 使用minus方法测试查看一年前和一年后的日期

- 更多方法可以查看API



# Lambda表达式

**函数式编程：**

- 函数式编程(Functional programming)是一种思想特点
- 函数式编程思想，忽略面向对象的复杂语法，强调做什么，而不是谁去做
- 而Lambda表达式就是函数式思想的体现

**Lambda表达式的标准格式：**
Lambda表达式是JDK8开始后的一种新语法形式

```java
() -> {
    
}
```

- ( ) 对应着方法的形参
- -> 固定格式
- { } 对应值方法体

**案例：**

```java
Arrays.sort(arr,new Comparator<Integer>(){
    @Override
    public int compare(Integer o1, Integer o2) {
        return o1 - o2;
    }
});
//替换为Lambda
Arrays.sort(arr, (Integer o1, Integer o2) -> {
        return o1 - o2;
    }
);
```

**注意：**

- Lambda表达式可以用来简化匿名内部类的书写
- Lambda表达式只能简化函数式接口的匿名内部类的写法
- 函数式接口：有且仅有一个抽象方法的接口叫做函数式接口，接口上方可以加@Functionallnterface注解





# 集合

## 集合的理解和好处

**数组：**

1. 长度开始时必须指定，而且一旦指定，不能更改
2. 保存的必须为同一类型的元素
3. 使用数组进行增加/删除元素的示意代码，比较麻烦

**集合：**

1. 可以动态保存任意多个对象，使用比较方便
2. 提供了一系列方便的操作对象的方法：add、remove、set、get等



## 集合的框架体系

Java 的集合类很多，主要分为两大类：

1.单列集合 Collection接口：

<img src="https://pb.nichi.co/february-coin-announce" style="zoom:50%;" /> 

2.双列集合 Map接口：

<img src="https://pb.nichi.co/wisdom-canal-project" style="zoom:50%;" /> 



## Collection接口和常用方法

### Collection接口实现类的特点

1. Collection实现子类可以存放多个元素，每个元素可以是Object
2. 有些Collection的实现类，可以存放重复的元素，有些不可以
3. 有些Collection的实现类，有些是有序的(List)，有些不是有序(Set)
4. Collection接口没有直接的实现子类，是通过它的子接口Set 和 List 来实现的

### Collection接口常用方法

> 以实现子类 ArrayList 来演示

1. add：添加单个元素

   ```java
   list.add("jack");
   list.add(10);//list.add(new Integer(10))
   list.add(true);
   ```

2. remove：删除指定元素

   ```java
   list.remove(0);//删除第一个元素
   list.remove(true);//指定删除某个元素
   ```

3. contains：查找元素是否存在

   `list.contains("jack")`

4. size：获取元素个数

   `list.size()`

5. isEmpty：判断是否为空

   `list.isEmpty()`

6. clear：清空

   `list.isEmpty()`

7. addAll：添加多个元素

   ```java
   list2.add("红楼梦");
   list2.add("三国演义");
   list.addAll(list2);
   ```

8. containsAll:查找多个元素是否都存在

   `list.containsAll(list2)`

9. removeAll：删除多个元素

   ```java
   list.add("聊斋");
   list.removeAll(list2);
   System.out.println("list=" + list);//[聊斋]
   ```

### Collection接口遍历元素方式

1. 使用 Iterator(迭代器)

   基本介绍：

   1. Iterator对象称为迭代器，主要用于遍历 Collection 集合中的元素
   2. 所有实现了Collection接口的集合类都有一个iterator()方法，用以返回一个实现了lterator接口的对象，即可以返回一个迭代器
   3. lterator 仅用于遍历集合，lterator 本身并不存放对象

   执行原理：（idea快捷键：itit）

   ```java
   Iterator iterator = coll.iterator();//得到一个集合的迭代器
   //hasNext()方法判断是否还有下一个元素
   while(iterator.hasNext()){
       //next()作用：1.下移 2.将下移以后集合位置上的元素返回
       System.out.println(iterator.next());
   }
   //如果希望再次遍历，需要重置迭代器
   iterator = col.iterator();
   ```

   注意：在调用`iterator.next()`方法之前必须要调用`iterator.hasNext()`进行检测。若不调用，且下一条记录无效，直接调用`iterator.hasNext()`会抛出NoSuchElementException异常

2. 增强 for 循环

   > 增强for循环，可以代替iterator迭代器，特点：增强for就是简化版 的iterator，本质一样。只能用来遍历集合或数组

   基本语法：（idea快捷键：I）

   ```java
   for(元素类型 元素名 : 集合名或数组名){
       访问元素
   }
   ```



## List接口和常用方法

### List接口基本介绍

> List 接口是 Collection 接口的子接口 

1. List集合类中元素有序(即添加顺序和取出顺序一致)、且可重复

2. List集合中的每个元素都有其对应的顺序索引，即支持索引

3. List容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素

4. Java API中List接口的实现类有：

   AbstractList，AbstractSequentialList，**ArrayList**，AttributeList，CopyOnWriteArrayList，**LinkedList**，RoleList，RoleUnresolvedList，Stack，**Vector**

### List接口的常用方法

1. `void add(int index, Object ele)`：在index位置插入ele元素

   `list.add(1, "hello");`

2. `boolean addAll(int index, Collection eles)`：从index位置开始将eles中的所有元素添加进来

   `list.addAll(1, list2);`

3. `Object get(int index)`：获取指定index位置的元素

4. `int indexOf(Object obj)`：返回obj在集合中首次出现的位置

5. `int lastIndexOf(Object obj)`：返回obj在当前集合中末次出现的位置

6. `Object remove(int index)`：移除指定index位置的元素，并返回此元素

   `list.remove(0);`

7. `Object set(int index, Object ele)`：设置指定index位置的元素为ele , 相当于是替换

   `list.set(1, "jack");`

8.  `List subList(int fromIndex, int toIndex)`：返回从fromIndex到toIndex位置的子集合

   注意返回的子集合 fromIndex <= subList < toIndex

   `List returnlist = list.subList(0, 2);`

### List的三种遍历方式

1. 使用iterator

   ```java
   iterator iter = col.iterator();
   while(iter.hasNext()){
       Object o = iter.next();
   }
   ```

2. 使用增强for

   `for(Object o : col){}`

3. 使用普通for

   ```java
   for(int i = 0;i < list.size();i++){
       Object o = list.get(i);
       System.out.println(o);
   }
   ```



## ArrayList底层结构和源码分析

###  ArrayList的注意事项

1. permits all elements，including null，ArrayList 可以加入null，并且多个
2. ArrayList 是由数组来实现数据存储的
3. ArrayList 基本等同于Vector，但ArrayList是线程不安全(执行效率高)，在多线程情况下，不建议使用ArrayList

### ArrayList的底层操作机制

1. ArrayList中维护了一个Object类型的数组elementData

   `transient Object[] elementData;` transient 表示瞬间，短暂的，表示该属性不会被序列化

2. 当创建ArrayList对象时，如果使用的是无参构造器，则初始elementData容量为0，第1次添加，则扩容elementData为10，如需要再次扩容，则扩容elementData为1.5倍

3. 如果使用的是指定大小的构造器，则初始elementData容量为指定大小，如果需要扩容则直接扩容elementData为1.5倍



## Vector底层结构和源码剖析 

### Vector的基本介绍

1. Vector类的定义说明

   ```java
   public class Vector<E>
       extends AbstractList<E>
       implements List<E>, RandomAccess, Cloneable, java.io.Serializable{}
   ```

2. Vector底层也是一个对象数组

   `protected Object[] elementData;`

3. Vector是线程同步的，即线程安全，Vector类的操作方法带有**synchronized**

4. 在开发中，需要线程同步安全，考虑使用Vector

### Vector和ArrayList的比较

| 名称      | 底层结构 | 版本   | 线程安全(同步)效率 | 扩容倍数                                                     |
| --------- | -------- | ------ | ------------------ | ------------------------------------------------------------ |
| ArrayList | 可变数组 | jdk1.2 | 不安全，效率高     | 如果是有参构造1.5倍；如果是无参第一次10，第二次开始按1.5倍扩容 |
| Vector    | 可变数组 | jdk1.0 | 安全，效率不高     | 如果是无参，默认10，满后，就按两倍扩容；如果指定大小，则每次直接按两倍扩容 |



## LinkedList底层结构 

### LinkedList的全面说明 

1.  LinkedList底层实现了**双向链表**和**双端队列**特点
2. 可以添加任意元素（元素可以重复），包括null
3. 线程不安全，没有实现同步

### LinkedList的底层操作机制

1) LinkedList底层维护了一个双向链表

2) LinkedList中维护了两个属性first和last分别指向首节点和尾节点

3) 每个节点(Node对象)，里面又维护了prev、next、item三个属性，其中通过prev指向前一个，通过next指向后一个节点，最终实现双向链表

4) 所以LinkedList的元素的添加和删除，不是通过数组完成的，相对来说效率较高

5) 模拟一个简单的双向链表

   ```java
   public class LinkedList01 {
       public static void main(String[] args) {
           //模拟一个简单的双向链表
   
           Node jack = new Node("jack");
           Node tom = new Node("tom");
           Node hello = new Node("hello");
   
           //连接三个结点，形成双向链表
           //jack -> tom -> hello
           jack.next = tom;
           tom.next = hello;
           //hsp -> tom -> jack
           hello.pre = tom;
           tom.pre = jack;
   
           Node first = jack;//让first引用指向jack,就是双向链表的头结点
           Node last = hello; //让last引用指向hsp,就是双向链表的尾结点
   
   
           //演示，从头到尾进行遍历
           System.out.println("===从头到尾进行遍历===");
           while (true) {
               if(first == null) {
                   break;
               }
               //输出first 信息
               System.out.println(first);
               first = first.next;
           }
   
           //演示，从尾到头的遍历
           System.out.println("====从尾到头的遍历====");
           while (true) {
               if(last == null) {
                   break;
               }
               //输出last 信息
               System.out.println(last);
               last = last.pre;
           }
   
           //演示链表的添加对象/数据，是多么的方便
           //要求，是在 tom --------- hello直接，插入一个对象 smith
   
           //1. 先创建一个 Node 结点，name 就是 smith
           Node smith = new Node("smith");
           //下面就把 smith 加入到双向链表了
           smith.next = hello;
           smith.pre = tom;
           hello.pre = smith;
           tom.next = smith;
   
           //让first 再次指向jack
           first = jack;//让first引用指向jack,就是双向链表的头结点
   
           System.out.println("===从头到尾进行遍历===");
           while (true) {
               if(first == null) {
                   break;
               }
               //输出first 信息
               System.out.println(first);
               first = first.next;
           }
   
           last = hello; //让last 重新指向最后一个结点
           //演示，从尾到头的遍历
           System.out.println("====从尾到头的遍历====");
           while (true) {
               if(last == null) {
                   break;
               }
               //输出last 信息
               System.out.println(last);
               last = last.pre;
           }
       }
   }
   //定义一个Node 类，Node 对象 表示双向链表的一个结点
   class Node {
       public Object item; //真正存放数据
       public Node next; //指向后一个结点
       public Node pre; //指向前一个结点
       public Node(Object name) {
           this.item = name;
       }
       public String toString() {
           return "Node name=" + item;
       }
   }
   ```

### LinkedList 的增删改查案例

```java
import java.util.Iterator;
import java.util.LinkedList;

/**
 * @author 韩顺平
 * @version 1.0
 */
@SuppressWarnings({"all"})
public class LinkedListCRUD {
    public static void main(String[] args) {

        LinkedList linkedList = new LinkedList();
        linkedList.add(1);
        linkedList.add(2);
        linkedList.add(3);
        System.out.println("linkedList=" + linkedList);

        //演示一个删除结点的
        linkedList.remove(); // 这里默认删除的是第一个结点
        //linkedList.remove(2);

        System.out.println("linkedList=" + linkedList);

        //修改某个结点对象
        linkedList.set(1, 999);
        System.out.println("linkedList=" + linkedList);

        //得到某个结点对象
        //get(1) 是得到双向链表的第二个对象
        Object o = linkedList.get(1);
        System.out.println(o);//999

        //因为LinkedList 是 实现了List接口, 遍历方式
        System.out.println("===LinkeList遍历迭代器====");
        Iterator iterator = linkedList.iterator();
        while (iterator.hasNext()) {
            Object next =  iterator.next();
            System.out.println("next=" + next);

        }

        System.out.println("===LinkeList遍历增强for====");
        for (Object o1 : linkedList) {
            System.out.println("o1=" + o1);
        }
        System.out.println("===LinkeList遍历普通for====");
        for (int i = 0; i < linkedList.size(); i++) {
            System.out.println(linkedList.get(i));
        }


        //源码解读
        /* 1. LinkedList linkedList = new LinkedList();
              public LinkedList() {}
           2. 这时 linkeList 的属性 first = null  last = null
           3. 执行 添加
               public boolean add(E e) {
                    linkLast(e);
                    return true;
                }
            4.将新的结点，加入到双向链表的最后
             void linkLast(E e) {
                final Node<E> l = last;
                final Node<E> newNode = new Node<>(l, e, null);
                last = newNode;
                if (l == null)
                    first = newNode;
                else
                    l.next = newNode;
                size++;
                modCount++;
            }
         */
        /*
          源码解读 linkedList.remove(); // 这里默认删除的是第一个结点
          1. 执行 removeFirst
            public E remove() {
                return removeFirst();
            }
         2. 执行
            public E removeFirst() {
                final Node<E> f = first;
                if (f == null)
                    throw new NoSuchElementException();
                return unlinkFirst(f);
            }
          3. 执行 unlinkFirst, 将 f 指向的双向链表的第一个结点拿掉
            private E unlinkFirst(Node<E> f) {
                // assert f == first && f != null;
                final E element = f.item;
                final Node<E> next = f.next;
                f.item = null;
                f.next = null; // help GC
                first = next;
                if (next == null)
                    last = null;
                else
                    next.prev = null;
                size--;
                modCount++;
                return element;
            }
         */
    }
}
```

### ArrayList 和 LinkedList 比较

| 名称       | 底层结构 | 增删的效率         | 改查的效率 |
| ---------- | -------- | ------------------ | ---------- |
| ArrayList  | 可变数组 | 较低，数组扩容     | 较高       |
| LinkedList | 双向链表 | 较高，通过链表追加 | 较低       |

**如果选择ArrayList和LinkedList：**

1. 如果我们改查的操作多，选择ArrayList
2. 如果我们增删的操作多，选择LinkedList
3. 一般来说，在程序中，80%-90%都是查询，因此大部分情况下会选择ArrayList
4. 在一个项目中，根据业务灵活选择，也可能这样，一个模块使用的是ArrayList,另外一个模块是LinkedList,也就是说，要根据业务来进行选择



## Set接口和常用方法

### Set接口基本介绍

1. 无序（添加和取出的顺序不一致），没有索引
2. 不允许重复元素，所以最多包含一个null
3. JDK API中Set接口的实现类有：
   AbstractSet，ConcurrentHashMap.KeySetView，ConcurrentSkipListSet，CopyOnWriteArraySet，EnumSet，HashSet，JobStateReasons，LinkedHashSet，TreeSet

### Set接口的常用方法

和 List 接口一样, Set 接口也是 Collection 的子接口，因此，常用方法和 Collection 接口一样

### Set接口的遍历方式

同Collection的遍历方式一样，因为Set接口是Collection接口的子接口

1. 可以使用迭代器
2. 增强for
3. 不能使用索引的方式来获取

```java
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;
public class SetMethod {
    public static void main(String[] args) {
        //1. 以Set 接口的实现类 HashSet 来讲解Set 接口的方法
        //2. Set 接口的实现类的对象(Set接口对象), 不能存放重复的元素, 可以添加一个null
        //3. Set 接口对象存放数据是无序(即添加的顺序和取出的顺序不一致)
        //4. 注意：取出的顺序的顺序虽然不是添加的顺序，但是他的固定.
        Set set = new HashSet();
        set.add("john");
        set.add("lucy");
        set.add("john");//重复
        set.add("jack");
        set.add("hello");
        set.add("mary");
        set.add(null);
        set.add(null);//再次添加null
        for(int i = 0; i <10;i ++) {
            System.out.println("set=" + set);
        }
        //遍历
        //方式1： 使用迭代器
        System.out.println("=====使用迭代器====");
        Iterator iterator = set.iterator();
        while (iterator.hasNext()) {
            Object obj =  iterator.next();
            System.out.println("obj=" + obj);
        }
        set.remove(null);
        //方式2: 增强for
        System.out.println("=====增强for====");
        for (Object o : set) {
            System.out.println("o=" + o);
        }
        //set 接口对象，不能通过索引来获取
    }
}
```



## Set接口实现类-HashSet 

### HashSet基本介绍

1. HashSet实现了Set接口

2. HashSet实际上是HashMap，看下源码：

   ```java
   public HashSet() {
   	map = new HashMap<>();
   }
   ```

3. 可以存放null值，但只能有一个null

4. HashSet不保证元素是有序的，取决于hash后，再确定索引的结果（即，不保证存放元素的顺序和取出顺序一致）

5. 不能有重复元素/对象

### HashSet底层机制

> HashSet底层是HashMap，HashMap底层是（数组+链表+红黑树）

**HashSet添加机制：**

1. HashSet 底层是 HashMap
2. 添加一个元素时，先获取元素的哈希值（hashCode方法），然后对哈希值进行运算，得出一个索引值即为要存放在哈希表中的位置号
3. 找到存储数据表table，看这个索引位置是否已经存放的有元素
4. 如果该位置上没有其他元素，则直接存放
5. 如果有，调用 equals 比较，如果相同，就放弃添加，如果不相同，则以链表的方式添加
6. 在Java8中，如果一条链表的元素个数到达 TREEIFY_THRESHOLD（默认是 8），并且table的大小 >=MIN_TREEIFY_CAPACITY（默认64）就会进行树化（红黑树）

**HashSet数组扩容机制：**

1. HashSet 底层是 HashMap，第一次添加时，table 数组扩容到 16，临界值threshold(16) * 加载因子IoadFactor(0.75) = 12
2. 如果table 数组使用到了临界值 12，就会扩容到 16 * 2 = 32，新的临界值就是 32 * 0.75 = 24，依次类推
3. 在Java8中，如果一条链表的元素个数到达 TREEIFY_THRESHOLD（默认是 8）并且table的大小 >=MIN_TREEIFY_CAPACITY（默认64）就会进行树化（红黑树），否则仍然采用数组扩容机制

```java
import java.util.HashSet;
public class HashSetSource {
    public static void main(String[] args) {
        HashSet hashSet = new HashSet();
        hashSet.add("java");//到此位置，第1次add分析完毕.
        hashSet.add("php");//到此位置，第2次add分析完毕
        hashSet.add("java");
        System.out.println("set=" + hashSet);
        /*
        HashSet 源码解读
        1. 执行 HashSet()
            public HashSet() {
                map = new HashMap<>();
            }
        2. 执行 add()
           public boolean add(E e) {//e = "java"
                return map.put(e, PRESENT)==null;//(static) PRESENT = new Object();
           }
         3.执行 put() , 该方法会执行 hash(key) 得到key对应的hash值 算法h = key.hashCode()) ^ (h >>> 16)
             public V put(K key, V value) {//key = "java" value = PRESENT 共享
                return putVal(hash(key), key, value, false, true);
            }
         4.执行 putVal
         final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
                Node<K,V>[] tab; Node<K,V> p; int n, i; //定义了辅助变量
                //table 就是 HashMap 的一个数组，类型是 Node[]
                //if 语句表示如果当前table 是null, 或者 大小=0
                //就是第一次扩容，到16个空间.
                if ((tab = table) == null || (n = tab.length) == 0)
                    n = (tab = resize()).length;

                //(1)根据key，得到hash 去计算该key应该存放到table表的哪个索引位置
                //并把这个位置的对象，赋给 p
                //(2)判断p 是否为null
                //(2.1) 如果p 为null, 表示还没有存放元素, 就创建一个Node (key="java",value=PRESENT)
                //(2.2) 就放在该位置 tab[i] = newNode(hash, key, value, null)

                if ((p = tab[i = (n - 1) & hash]) == null)
                    tab[i] = newNode(hash, key, value, null);
                else {
                    //一个开发技巧提示： 在需要局部变量(辅助变量)时候，在创建
                    Node<K,V> e; K k; //
                    //如果当前索引位置对应的链表的第一个元素和准备添加的key的hash值一样
                    //并且满足 下面两个条件之一:
                    //(1) 准备加入的key 和 p 指向的Node 结点的 key 是同一个对象
                    //(2)  p 指向的Node 结点的 key 的equals() 和准备加入的key比较后相同
                    //就不能加入
                    if (p.hash == hash &&
                        ((k = p.key) == key || (key != null && key.equals(k))))
                        e = p;
                    //再判断 p 是不是一颗红黑树,
                    //如果是一颗红黑树，就调用 putTreeVal , 来进行添加
                    else if (p instanceof TreeNode)
                        e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
                    else {//如果table对应索引位置，已经是一个链表, 就使用for循环比较
                          //(1) 依次和该链表的每一个元素比较后，都不相同, 则加入到该链表的最后
                          //    注意在把元素添加到链表后，立即判断 该链表是否已经达到8个结点
                          //    , 就调用 treeifyBin() 对当前这个链表进行树化(转成红黑树)
                          //    注意，在转成红黑树时，要进行判断, 判断条件
                          //    if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY(64))
                          //            resize();
                          //    如果上面条件成立，先table扩容.
                          //    只有上面条件不成立时，才进行转成红黑树
                          //(2) 依次和该链表的每一个元素比较过程中，如果有相同情况,就直接break

                        for (int binCount = 0; ; ++binCount) {
                            if ((e = p.next) == null) {
                                p.next = newNode(hash, key, value, null);
                                if (binCount >= TREEIFY_THRESHOLD(8) - 1) // -1 for 1st
                                    treeifyBin(tab, hash);
                                break;
                            }
                            if (e.hash == hash &&
                                ((k = e.key) == key || (key != null && key.equals(k))))
                                break;
                            p = e;
                        }
                    }
                    if (e != null) { // existing mapping for key
                        V oldValue = e.value;
                        if (!onlyIfAbsent || oldValue == null)
                            e.value = value;
                        afterNodeAccess(e);
                        return oldValue;
                    }
                }
                ++modCount;
                //size 就是我们每加入一个结点Node(k,v,h,next), size++
                if (++size > threshold)
                    resize();//扩容
                afterNodeInsertion(evict);
                return null;
            }
         */
    }
}
```

```java
import java.util.HashSet;
import java.util.Objects;
public class HashSetIncrement {
    public static void main(String[] args) {
        /*
        HashSet底层是HashMap, 第一次添加时，table 数组扩容到 16，
        临界值(threshold)是 16*加载因子(loadFactor)是0.75 = 12
        如果table 数组使用到了临界值 12,就会扩容到 16 * 2 = 32,
        新的临界值就是 32*0.75 = 24, 依次类推
         */
        HashSet hashSet = new HashSet();
//        for(int i = 1; i <= 100; i++) {
//            hashSet.add(i);//1,2,3,4,5...100
//        }
        /*
        在Java8中, 如果一条链表的元素个数到达 TREEIFY_THRESHOLD(默认是 8 )，
        并且table的大小 >= MIN_TREEIFY_CAPACITY(默认64),就会进行树化(红黑树),
        否则仍然采用数组扩容机制
         */
//        for(int i = 1; i <= 12; i++) {
//            hashSet.add(new A(i));
//        }

  		//当我们向hashset增加一个元素，-> Node -> 加入table , 就算是增加了一个size++

        for(int i = 1; i <= 7; i++) {//在table的某一条链表上添加了 7个A对象
            hashSet.add(new A(i));//
        }

        for(int i = 1; i <= 7; i++) {//在table的另外一条链表上添加了 7个B对象
            hashSet.add(new B(i));//
        }
    }
}
class B {
    private int n;
    public B(int n) {
        this.n = n;
    }
    @Override
    public int hashCode() {
        return 200;
    }
}
class A {
    private int n;
    public A(int n) {
        this.n = n;
    }
    @Override
    public int hashCode() {
        return 100;
    }
}
```



## Map接口和常用方法

### Map接口实现类的特点

> 这里讲的是JDK8中的Map接口特点

1. Map 与 Collection 并列存在，用于保存具有映射关系的数据：Key-Value

2. Map 中的 key 和 value 可以是任何引用类型的数据，会封装到 HashMap$Node 对象中

3. Map 中的 key 不允许重复，原因和 HashSet 一样，前面分析过源码

4. Map 中的 value 可以重复

5. Map 的 key 可以为 null，value 也可以为 null 。注意：key 为null，只能有一个；value 为null，可以有多个

6. 常用String类作为 Map 的 key

7. key 和 value 之间存在单向一对一关系，即通过指定的 key 总能找到对应的 value

8. Map 存放数据的key-value示意图，一对 k-v 是放在一个HashMap$Node中的，又因为Node实现了Entry接口，有些书上也说一对k-v就是一个Entry

   <img src="https://pb.nichi.co/error-rhythm-athlete" style="zoom: 50%;" /> 

   ```java
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   import java.util.Set;
   public class MapSource_ {
       public static void main(String[] args) {
           Map map = new HashMap();
           map.put("no1", "jack");//k-v
           map.put("no2", "smith");//k-v
           map.put(new Car(), new Person());//k-v
           //1. k-v 最后是 HashMap$Node node = newNode(hash, key, value, null)
           //2. k-v 为了方便程序员的遍历，还会 创建 EntrySet 集合 ，该集合存放的元素的类型 Entry, 而一个Entry
           //   对象就有k,v EntrySet<Entry<K,V>> 即： transient Set<Map.Entry<K,V>> entrySet;
           //3. entrySet 中， 定义的类型是 Map.Entry ，但是实际上存放的还是 HashMap$Node
           //   这时因为 static class Node<K,V> implements Map.Entry<K,V>
           //4. 当把 HashMap$Node 对象 存放到 entrySet 就方便我们的遍历, 因为 Map.Entry 提供了重要方法
           //   K getKey(); V getValue();
           Set set = map.entrySet();
           System.out.println(set.getClass());// HashMap$EntrySet
           for (Object obj : set) {
               //System.out.println(obj.getClass()); //HashMap$Node
               //为了从 HashMap$Node 取出k-v
               //先做一个向下转型
               Map.Entry entry = (Map.Entry) obj;
               System.out.println(entry.getKey() + "-" + entry.getValue());
           }
           Set set1 = map.keySet();
           System.out.println(set1.getClass());
           Collection values = map.values();
           System.out.println(values.getClass());
       }
   }
   class Car {}
   class Person{}
   ```

### Map接口常用方法

1. put：添加元素
2. remove：根据键(key)删除映射关系
3. get：根据键(key)获取值
4. size：获取元素个数
5. isEmpty：判断个数是否为0
6. clear：清除所有元素
7. containsKey：查找键是否存在

### Map接口遍历方法

```java
import java.util.*;
public class MapFor {
    public static void main(String[] args) {

        Map map = new HashMap();
        map.put("no1", "jack");
        map.put("no2", "smith");
        map.put("no3", "mark");

        //第一组: 先取出 所有的Key , 通过Key 取出对应的Value
        Set keyset = map.keySet();
        //(1) 增强for
        System.out.println("-----第一种方式-------");
        for (Object key : keyset) {
            System.out.println(key + "-" + map.get(key));
        }
        //(2) 迭代器
        System.out.println("-----第二种方式--------");
        Iterator iterator = keyset.iterator();
        while (iterator.hasNext()) {
            Object key =  iterator.next();
            System.out.println(key + "-" + map.get(key));
        }

        //第二组: 把所有的values取出
        Collection values = map.values();
        //这里可以使用所有的Collections使用的遍历方法
        //(1) 增强for
        System.out.println("---取出所有的value 增强for----");
        for (Object value : values) {
            System.out.println(value);
        }
        //(2) 迭代器
        System.out.println("---取出所有的value 迭代器----");
        Iterator iterator2 = values.iterator();
        while (iterator2.hasNext()) {
            Object value =  iterator2.next();
            System.out.println(value);

        }

        //第三组: 通过EntrySet 来获取 k-v
        Set entrySet = map.entrySet();// EntrySet<Map.Entry<K,V>>
        //(1) 增强for
        System.out.println("----使用EntrySet 的 for增强(第3种)----");
        for (Object entry : entrySet) {
            //将entry 转成 Map.Entry
            Map.Entry m = (Map.Entry) entry;
            System.out.println(m.getKey() + "-" + m.getValue());
        }
        //(2) 迭代器
        System.out.println("----使用EntrySet 的 迭代器(第4种)----");
        Iterator iterator3 = entrySet.iterator();
        while (iterator3.hasNext()) {
            Object entry =  iterator3.next();
            //System.out.println(next.getClass());//HashMap$Node -实现-> Map.Entry (getKey,getValue)
            //向下转型 Map.Entry
            Map.Entry m = (Map.Entry) entry;
            System.out.println(m.getKey() + "-" + m.getValue());
        }
    }
}
```



## Map接口实现类-HashMap

### HashMap基本介绍

1. Map接口的常用实现类：HashMap、Hashtable和Properties
2. HashMap是 Map 接口使用频率最高的实现类
3. HashMap 是以 key-value 对的方式来存储数据（HashMap$Node类型）
4. key 不能重复，但是值可以重复，允许使用null键和null值
5. 如果添加相同的key，则会覆盖原来的key-value，等同于修改（key不会替换，val会替换）
6. 与HashSet一样，不保证映射的顺序，因为底层是以hash表的方式来存储的（jdk8的hashMap 底层数组+链表+红黑树）
7. HashMap没有实现同步，因此是线程不安全的,方法没有做同步互斥的操作，没有synchronized
8. HashMap底层维护了一个table，table表是一个数组，数组每个元素里放的是链表（HashMap$Node）或红黑树（HashMap$TreeNode），HashMap$Node实现了HashMap$Entry接口

### HashMap底层机制及源码剖析

1. HashMap底层维护了Node类型的数组table，默认为null
2. 当创建对象时，将加载因子(loadfactor)初始化为0.75
3. 当添加key-val时，通过key的哈希值得到在table的索引。然后判断该索引处是否有元素如果没有元素直接添加。如果该索引处有元素，继续判断该元素的key和准备加入的key是否相等，如果相等，则直接替换val；如果不相等需要判断是树结构还是链表结构，做出相应处理。如果添加时发现容量不够，则需要扩容。
4. 第1次添加，则需要扩容table容量为16，临界值(threshold)为12（16*0.75）
5. 以后再扩容，则需要扩容table容量为原来的2倍（32），临界值为原来的2倍，即24，依次类推
6. 在Java8中,如果一条链表的元素个数超过 TREEIFY_THRESHOLD（默认是 8），并且table的大小 >= MIN_TREEIFY_CAPACITY（默认64），就会进行树化（红黑树）

```java
import java.util.HashMap;
public class HashMapSource1 {
    public static void main(String[] args) {
        HashMap map = new HashMap();
        map.put("java", 10);//ok
        map.put("php", 10);//ok
        map.put("java", 20);//替换value
        System.out.println("map=" + map);
        /*源码解读
        1. 执行构造器 new HashMap()
           初始化加载因子 loadfactor = 0.75
           HashMap$Node[] table = null
        2. 执行put 调用 hash方法，计算 key的 hash值 (h = key.hashCode()) ^ (h >>> 16)
            public V put(K key, V value) {//K = "java" value = 10
                return putVal(hash(key), key, value, false, true);
            }
         3. 执行 putVal
         final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
                Node<K,V>[] tab; Node<K,V> p; int n, i;//辅助变量
                //如果底层的table 数组为null, 或者 length =0 , 就扩容到16
                if ((tab = table) == null || (n = tab.length) == 0)
                    n = (tab = resize()).length;
                //取出hash值对应的table的索引位置的Node, 如果为null, 就直接把加入的k-v
                //, 创建成一个 Node ,加入该位置即可
                if ((p = tab[i = (n - 1) & hash]) == null)
                    tab[i] = newNode(hash, key, value, null);
                else {
                    Node<K,V> e; K k;//辅助变量
                // 如果table的索引位置的key的hash相同和新的key的hash值相同，
                 // 并 满足(table现有的结点的key和准备添加的key是同一个对象  || equals返回真)
                 // 就认为不能加入新的k-v
                    if (p.hash == hash &&
                        ((k = p.key) == key || (key != null && key.equals(k))))
                        e = p;
                    else if (p instanceof TreeNode)//如果当前的table的已有的Node 是红黑树，就按照红黑树的方式处理
                        e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
                    else {
                        //如果找到的结点，后面是链表，就循环比较
                        for (int binCount = 0; ; ++binCount) {//死循环
                            if ((e = p.next) == null) {//如果整个链表，没有和他相同,就加到该链表的最后
                                p.next = newNode(hash, key, value, null);
                                //加入后，判断当前链表的个数，是否已经到8个，到8个，后
                                //就调用 treeifyBin 方法进行红黑树的转换
                                if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                                    treeifyBin(tab, hash);
                                break;
                            }
                            if (e.hash == hash && //如果在循环比较过程中，发现有相同,就break,就只是替换value
                                ((k = e.key) == key || (key != null && key.equals(k))))
                                break;
                            p = e;
                        }
                    }
                    if (e != null) { // existing mapping for key
                        V oldValue = e.value;
                        if (!onlyIfAbsent || oldValue == null)
                            e.value = value; //替换，key对应value
                        afterNodeAccess(e);
                        return oldValue;
                    }
                }
                ++modCount;//每增加一个Node ,就size++
                if (++size > threshold[12-24-48])//如size > 临界值，就扩容
                    resize();
                afterNodeInsertion(evict);
                return null;
            }
              5. 关于树化(转成红黑树)
              //如果table 为null ,或者大小还没有到 64，暂时不树化，而是进行扩容.
              //否则才会真正的树化 -> 剪枝
              final void treeifyBin(Node<K,V>[] tab, int hash) {
                int n, index; Node<K,V> e;
                if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY)
                    resize();
            }
         */
    }
}
```



## Map接口实现类-Hashtable

### 基本介绍

1. 存放的元素是键值对：即 K-V
2. hashtable的键和值都不能为null，否则会抛出NullPointerException
3. hashTable 使用方法基本上和HashMap一样
4. hashTable 是线程安全的(synchronized)，hashMap 是线程不安全的

### Hashtable和HashMap对比

| 名称      | 版本 | 线程安全(同步) | 效率 | 允许null键null值 |
| --------- | ---- | -------------- | ---- | ---------------- |
| HashMap   | 1.2  | 不安全         | 高   | 允许             |
| Hashtable | 1.0  | 安全           | 较低 | 不允许           |



## Map接口实现类-Properties

### 基本介绍

1. Properties类继承自Hashtable类并且实现了Map接口，也是使用一种键值对的形式来保存数据
2. 他的使用特点和Hashtable类似
3. Properties 还可以用于 从 xxx.properties 文件中，加载数据到Properties类对象，并进行读取和修改
4. 说明：工作后 xxx.properties 文件通常作为配置文件，这个知识点在IO流举例，[有兴趣可先看文章](https://www.cnblogs.com/xudong-bupt/p/3758136.html)

### 基本使用

1. put：增加，如果增加已存在key值，则为修改/替换
2. get：查找，通过key查找value
3. remove：删除，删除key所对应的key-value



## TreeSet和TreeMap

**TreeSet：**

```java
import java.util.Comparator;
import java.util.TreeSet;
public class TreeSet_ {
    public static void main(String[] args) {

        //1. 当我们使用无参构造器，创建TreeSet时，仍然是无序的
        //2. 老师希望添加的元素，按照字符串大小来排序
        //3. 使用TreeSet 提供的一个构造器，可以传入一个比较器(匿名内部类)
        //   并指定排序规则
        //4. 简单看看源码
        /*
        1. 构造器把传入的比较器对象，赋给了 TreeSet的底层的 TreeMap的属性this.comparator

         public TreeMap(Comparator<? super K> comparator) {
                this.comparator = comparator;
            }
         2. 在 调用 treeSet.add("tom"), 在底层会执行到

             if (cpr != null) {//cpr 就是我们的匿名内部类(对象)
                do {
                    parent = t;
                    //动态绑定到我们的匿名内部类(对象)compare
                    cmp = cpr.compare(key, t.key);
                    if (cmp < 0)
                        t = t.left;
                    else if (cmp > 0)
                        t = t.right;
                    else //如果相等，即返回0,这个Key就没有加入
                        return t.setValue(value);
                } while (t != null);
            }
         */

//        TreeSet treeSet = new TreeSet();
        TreeSet treeSet = new TreeSet(new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                //下面 调用String的 compareTo方法进行字符串大小比较
                //如果老韩要求加入的元素，按照长度大小排序
                //return ((String) o2).compareTo((String) o1);
                return ((String) o1).length() - ((String) o2).length();
            }
        });
        //添加数据.
        treeSet.add("jack");
        treeSet.add("tom");//3
        treeSet.add("sp");
        treeSet.add("a");
        treeSet.add("abc");//3

        System.out.println("treeSet=" + treeSet);
    }
}
```

**TreeMap：**

```java
import java.util.Comparator;
import java.util.TreeMap;
public class TreeMap_ {
    public static void main(String[] args) {
        //使用默认的构造器，创建TreeMap, 是无序的(也没有排序)
        //按照传入的 k(String) 的大小进行排序
		//TreeMap treeMap = new TreeMap();
        TreeMap treeMap = new TreeMap(new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                //按照传入的 k(String) 的大小进行排序
                //按照K(String) 的长度大小排序
                //return ((String) o2).compareTo((String) o1);
                return ((String) o2).length() - ((String) o1).length();
            }
        });
        treeMap.put("jack", "杰克");
        treeMap.put("tom", "汤姆");
        treeMap.put("kristina", "克瑞斯提诺");
        treeMap.put("smith", "斯密斯");
        treeMap.put("abc", "abc");//加入不了

        System.out.println("treemap=" + treeMap);

        /*
            解读源码：
            1. 构造器. 把传入的实现了 Comparator接口的匿名内部类(对象)，传给给TreeMap的comparator
             public TreeMap(Comparator<? super K> comparator) {
                this.comparator = comparator;
            }
            2. 调用put方法
            2.1 第一次添加, 把k-v 封装到 Entry对象，放入root
            Entry<K,V> t = root;
            if (t == null) {
                compare(key, key); // type (and possibly null) check

                root = new Entry<>(key, value, null);
                size = 1;
                modCount++;
                return null;
            }
            2.2 以后添加
            Comparator<? super K> cpr = comparator;
            if (cpr != null) {
                do { //遍历所有的key , 给当前key找到适当位置
                    parent = t;
                    cmp = cpr.compare(key, t.key);//动态绑定到我们的匿名内部类的compare
                    if (cmp < 0)
                        t = t.left;
                    else if (cmp > 0)
                        t = t.right;
                    else  //如果遍历过程中，发现准备添加Key 和当前已有的Key 相等，就不添加
                        return t.setValue(value);
                } while (t != null);
            }
         */
    }
}
```

**分析HashSet和TreeSet分别如何实现现去重的：**

1. HashSet的去重机制：hashCode() + equals()，底层先通过存入对象，进行运算得到一个 hash值，通过hash值得到对应的索引， 如果发现 table索引 所在的位置，没有数据，就直接存放，如果有数据，就进行遍历equals方法比较，如果比较后，不相同，就加入，否则就不加入
2. TreeSet的去重机制：如果你传入了一个Comparator匿名对象，就使用实现的compare去重，如果方法返回0，就认为是相同的元素素/数据，就不添加，如果你没有传入一个Comparator匿名对象，则以你添加的对象实现的Cornpareable接口的compareTo去重

**TreeSet和TreeMap注意事项补充：**

```java
import java.util.TreeSet;
public class Homework {
    public static void main(String[] args) {
        TreeSet treeSet = new TreeSet();
        //分析源码
        //add 方法，因为 TreeSet() 构造器没有传入Comparator接口的匿名内部类
        //所以在底层 Comparable<? super K> k = (Comparable<? super K>) key;
        //即 把 Perosn转成 Comparable类型
        treeSet.add(new Person());//ClassCastException
        treeSet.add(new Person());//compareTo return0则添加不进
        System.out.println(treeSet);
    }
}
//class Person{}//不继承Comparable会抛出ClassCastException异常
class Person implements Comparable{
    @Override
    public int compareTo(Object o) {
        return 0;
    }
}
```



## 总结-如何选择集合实现类

> 在开发中，选择什么集合实现类，主要取决于业务操作特点，然后根据集合实现类特性进行选择，分析如下：

1. 先判断存储的类型 (一组对象[单列]或一组键值对[双列])
2. 一组对象[单列]：Collection接口
   1. 允许重复：List
      1. 增删多：LinkedList [底层维护了一个双向链表]
      2. 改查多：ArrayList [底层维护 Object类型的可变数组]
   2. 不允许重复：Set
      1. 无序：HashSet [底层是HashMap ，维护了一个哈希表 即(数组+链表+红黑树)]
      2. 排序：TreeSet
      3. 插入和取出顺序一致：LinkedHashSet，维护数组+双向链表
3. 一组键值对[双列]：Map
   1. 键无序：HashMap[底层是 哈希表，jdk7：数组+链表，jdk8：数组+链表+红黑树]
   2. 键排序：TreeMap
   3. 键插入和取出顺序一致：LinkedHashMap
   4. 读取文件：Properties



## Collections工具类

### 基本介绍

1. Collections 是一个操作Set、List和Map等集合的工具类
2. Collections 中提供了一系列静态方法对集合元素进行排序、查询和修改等操作

### 常用方法

1. reverse(List)：反转 List 中元素的顺序

2. shuffle(List)：对 List 集合元素进行随机排序

3. sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序

4. sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序

   ```java
   //比如按照字符串的长度大小排序
   Collections.sort(list, new Comparator() {
       @Override public int compare(Object o1, Object o2) {
           //可以加入校验代码
           return ((String) o2).length() - ((String) o1).length();
       }
   });
   ```

5. swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换

6. Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素

7. Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素

   ```java
   //比如要返回长度最大的元素
   Object maxObject = Collections.max(list, new Comparator() {
       @Override
       public int compare(Object o1, Object o2) {
           return ((String)o1).length() - ((String)o2).length();
       }
   });
   ```

8. Object min(Collection) Object min(Collection，Comparator) 同max()

9. int frequency(Collection，Object)：返回指定集合中指定元素的出现次数

10. void copy(List dest,List src)：将 src 中的内容复制到 dest 中

    ```java
    //为了完成一个完整拷贝，我们需要先给 dest 赋值，大小和 src.size()一样
    //因为如果dest.size()小于src.size()就会抛出异常
    for(int i = 0; i < src.size(); i++) {
        dest.add("");
    }
    //拷贝
    Collections.copy(dest, src);
    ```

11. boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换 List 对象的所有旧值
