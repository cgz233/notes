# Java Study Notes 下部分

> by.Xiao_Chen

因内容较多，JavaStudyNotes分为三部分：

- 上部分：初识Java、Java基础语法、面向对象初级、中级和高级部分
- 中部分：枚举、注解、异常、常用类（包装类、String、Math、Object、System、日期类等）、Lambda表达式、集合
- 下部分：泛型、图形界面、线程、IO流、网络编程、反射、正则表达式、数据库编程

笔记仅供参考，查找方法更适合去[JavaAPI文档](https://docs.oracle.com/javase/8/docs/api/)，[中文文档下载（密码:chen）](https://wwxg.lanzoub.com/b02pzrdha) 

一些教程推荐：

- [XiaoChen/JavaStudyNotes](https://gitee.com/gitee-xiaochen/java-study-notes/blob/master/JavaNotes.md)

- [菜鸟Java教程](https://www.runoob.com/java/java-tutorial.html)

- [Quick Reference Java 备忘清单](http://bbs.laoleng.vip/reference/docs/java.html)

- [廖雪峰Java教程](https://www.liaoxuefeng.com/wiki/1252599548343744)

- [鱼皮Java学习路线](https://luxian.yupi.icu/#/roadmap/Java%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF)



# 泛型

## 泛型的好处

1. 编译时，检查添加元素的类型，提高了安全性

2. 减少了类型转换的次数，提高效率

   - 不使用泛型

     Dog -> 加入 -> Object -> 取出 -> Dog 放入到集合前会先转成 Object ，在取出时，还需要转换成Dog

   - 使用泛型

     Dog -> Dog -> Dog 放入时和取出时，不需要类型转换，提高效率

3. 不再提示编译警告



## 泛型介绍

1. 泛型又称为参数化类型，是JDK5.0出现的新特性，解决数据类型的安全性问题
2. 在类声明或实例化时只要指定好需要的具体类型即可
3. Java泛型可以保证如果程序在编译时没有发出警告，运行时就不会产生ClassCastException异常。同时，代码更加简洁、健壮。
4. 泛型的作用是：可以在类声明时通过一个标识表示类中某个属性的类型，或者是某个方法的返回值的类型，或者是参数类型



## 泛型的语法

**泛型的声明：**

`interface 接口<T>{}` 和 `class 类<K,v>{}`

说明：

1. 其中，T、K、V不代表值，而是表示类型
2. 任意字母都可以，常用T表示，是Type的缩写

**泛型的实例化：**

要在类名后指定类型参数的值(类型)，如：

1. `List<String> strList = new ArrayList<String>();`
2. `lterator<Customer> iterator = customers.iterator();`



## 注意事项和使用细节

1. 给泛型指向数据类型是，要求是引用类型，不能是基本数据类型

2. 在给泛型指定具体类型后，可以传入该类型或者其子类类型

3. 在实际开发中，我们往往简写

   `ArrayList<Integer> list = new ArrayList<Integer>();`

   `ArrayList<Integer> list = new ArrayList<>();`

4. `ArrayList arrayList = new ArrayList();`就等价`ArrayList<Object> arrayList = new ArrayList<Object>(); `



## 自定义泛型

### 自定义泛型类

**基本语法：**

```java
class 类名<T,R...>{//...表示可以有多个泛型
    成员
}
```

**注意细节：**

1. 普通成员可以使用泛型（属性、方法）

   ```java
   T t;
   R r;
   ```

2. 使用泛型的数组，不能初始化

   ```java
   //T[] ts = new T[]//错误
   //因为数组在 new 不能确定 T 的类型，就无法在内存开空间
   T[] ts;
   ```

3. 静态方法中不能使用类的泛型

   ```java
   //static void f(T t){}//错误
   //static T f();//错误
   //因为静态是和类相关的，在类加载时，对象还没有创建
   //所以，如果静态方法和静态属性使用了泛型，JVM 就无法完成初始化
   ```

4. 泛型类的类型，是在创建对象时确定的（因为创建对象时，需要指定确定类型）

5. 如果在创建对象时，没有指定类型，默认为Object

### 自定义泛型接口 

**基本语法：**

```java
interface 接口名<T,R...>{
}
```

**注意细节：**

1. 接口中，静态成员也不能使用泛型

   ```java
   //T t; 不能这样使用
   //因为接口中属性默认就是静态的，所以说接口属性不能使用泛型
   ```

2. 泛型接口的类型 ，在继承接口或者实现接口时确定

3. 没有指定类型，默认为Object

### 自定义泛型方法

**基本语法：**

```java
修饰符 <T,R...> 返回类型 方法名(参数列表){
}
```

**注意细节：**

1. 泛型方法中，可以定义在普通类中，也可以定义在泛型类中

2. 当泛型方法被调用时，类型会确定

3. `public void eat(E e){}`，修饰符后没有`<T,R...>`，因此eat方法不是泛型方法

4. 在泛型传入基本数据类型时，会进行自动装箱

   ```java
   f(10);//10自动装箱为Integer
   ```



## 泛型的继承和通配符

**基本介绍：**

1. 泛型不具备继承性

   `List<Object> list = new ArrayList<String>();`

2. `<?>`：支持任意泛型类型

3. `<? extends A>`：支持A类以及A类的子类，规定了泛型的上限

4. `<? super A>`：支持A类以及A类的父类，不限于直接父类，规定了泛型的下限

```java
import java.util.ArrayList;
import java.util.List;
public class GenericExtends {
    public static void main(String[] args) {

        Object o = new String("xx");

        //泛型没有继承性
        //List<Object> list = new ArrayList<String>();

        //举例说明下面三个方法的使用
        List<Object> list1 = new ArrayList<>();
        List<String> list2 = new ArrayList<>();
        List<AA> list3 = new ArrayList<>();
        List<BB> list4 = new ArrayList<>();
        List<CC> list5 = new ArrayList<>();

        //如果是 List<?> c ，可以接受任意的泛型类型
        printCollection1(list1);
        printCollection1(list2);
        printCollection1(list3);
        printCollection1(list4);
        printCollection1(list5);

        //List<? extends AA> c： 表示 上限，可以接受 AA或者AA子类
//        printCollection2(list1);//×
//        printCollection2(list2);//×
        printCollection2(list3);//√
        printCollection2(list4);//√
        printCollection2(list5);//√

        //List<? super AA> c: 支持AA类以及AA类的父类，不限于直接父类
        printCollection3(list1);//√
        //printCollection3(list2);//×
        printCollection3(list3);//√
        //printCollection3(list4);//×
        //printCollection3(list5);//×
    }
    // ? extends AA 表示 上限，可以接受 AA或者AA子类
    public static void printCollection2(List<? extends AA> c) {
        for (Object object : c) {
            System.out.println(object);
        }
    }
    //说明: List<?> 表示 任意的泛型类型都可以接受
    public static void printCollection1(List<?> c) {
        for (Object object : c) { // 通配符，取出时，就是Object
            System.out.println(object);
        }
    }
    // ? super 子类类名AA:支持AA类以及AA类的父类，不限于直接父类，
    //规定了泛型的下限
    public static void printCollection3(List<? super AA> c) {
        for (Object object : c) {
            System.out.println(object);
        }
    }
}
class AA {}
class BB extends AA {}
class CC extends BB {}
```



## JUnit

**为什么需要JUnit？**

1. 一个类有很多功能代码需要测试，为了测试，就需要写入到main方法中
2. 如果有多个功能代码测试，就需要来回注销，切换很麻烦
3. 如果可以直接运行一个方法，就方便很多，并且可以给出相关信息，就好了 -> JUnit

**基本介绍：**

1. JUnit是一个Java语言的单元测试框架
2. 多数Java的开发环境都已经集成可JUnit作为单元测试的工具

**使用方法：**

1. 导入JUnit包
2. 在方法上注释`@Test`



# 图形界面

> 因为在java中图形界面组件不重要，所以笔记较混乱

## JFrame

JFrame 是 Java 程序设计语言中用于建立窗口的类。它可以用来创建图形用户界面 (GUI) 应用程序，并且提供了用于显示和管理窗口元素的功能。 JFrame 类是在 Java Swing GUI 工具包中定义的，因此它只能在使用 Swing 的 Java 程序中使用。

**常用方法：**

1. this.setSize(603,680);//设置宽高
2. this.setTitle("拼图单机版 v1.0");//设置标题
3. this.setAlwaysOnTop(true);//设置一直显示在最上
4. setLocationRelativeTo(null);//设置界面居中
5. setDefaultCloseOperation(3);//设置默认的关闭方式 0-关不掉 1-默认 2-关闭所有窗口退出程序 3-关闭窗口退出程序
6. setVisible(true);//显示窗体，一般写在最后
7. setLayout(null);//取消默认的居中放置，只有取消了才会按照XY轴的形式添加组件



## jMenuBar JMenu JMenuItem

jMenuBar、JMenu 和 JMenuItem 是 Java Swing GUI 工具包中的类。jMenuBar 用于创建菜单栏，JMenu 用于创建菜单，而 JMenuItem 用于创建菜单项。通常，jMenuBar 包含多个 JMenu 对象，每个 JMenu 又包含多个 JMenuItem 对象，用户可以通过这些 JMenu 和 JMenuItem 来操作应用程序。

<img src="https://pb.nichi.co/aisle-food-ketchup" style="zoom: 50%;" /> 

**代码举例：**

```java
private void initJMenuBar() {
        JMenuBar jMenuBar = new JMenuBar();
        JMenu functionJMenu = new JMenu("功能");
        JMenu aboutJMenu = new JMenu("关于我们");
        JMenuItem againGameJMenu = new JMenuItem("重新游戏");
        JMenuItem againLoginJMenu = new JMenuItem("重新登录");
        JMenuItem exitJMenu = new JMenuItem("关闭游戏");
        JMenuItem numJMenu = new JMenuItem("公众号");

        jMenuBar.add(functionJMenu);
        jMenuBar.add(aboutJMenu);
        functionJMenu.add(againGameJMenu);
        functionJMenu.add(againLoginJMenu);
        functionJMenu.add(exitJMenu);
        aboutJMenu.add(numJMenu);

        this.setJMenuBar(jMenuBar);
    }
```

**常用方法：**

- jMenuBar 类：
  - add(JMenu menu)：用于向菜单栏添加菜单。
  - getMenu(int index)：用于获取菜单栏中指定位置的菜单。
  - setVisible(boolean visible)：用于设置菜单栏是否可见。
- JMenu 类：
  - add(JMenuItem menuItem)：用于向菜单添加菜单项。
  - getItem(int index)：用于获取菜单中指定位置的菜单项。
  - setText(String text)：用于设置菜单的标签。
- JMenuItem 类：
  - addActionListener(ActionListener listener)：用于为菜单项添加动作监听器。
  - setActionCommand(String command)：用于为菜单项设置动作命令。
  - setText(String text)：用于设置菜单项的标签。



## 添加图片

必须先在JFream中setLayout(null);//取消默认的居中放置，只有取消了才会按照XY轴的形式添加组件

```java
int num = 1;
for (int i = 0;i < 4;i++) {
	for (int j = 0; j < 4; j++) {
	//创建一个JLabel的对象(管理容器)
	JLabel jLabel1 = new JLabel(new ImageIcon("image/animal/animal3/" + num + ".jpg"));//创建一个图片ImageIcon的对象
	//指定图片位置
	jLabel1.setBounds(105 * j, 105 * i, 105, 105);
	//把管理容器添加到界面中
	//this.add(jLabel1);
	this.getContentPane().add(jLabel1);
    num++;
	}
}
```



## 事件

使用以下机制需要先继承这些接口，然后让要调用事件的部件去调用addActionListener()、addMouseListener(this)或addKeyListener(this)方法，this表示在此方法内

**ActionListener动作监听**

动作监听即点击鼠标或按下空格

**MouseListener鼠标监听机制**

| Modifier and Type | Method and Description                                       |
| ----------------- | ------------------------------------------------------------ |
| `void`            | `mouseClicked(MouseEvent e)`在组件上单击（按下并释放）鼠标按钮时调用。**单机** |
| `void`            | `mouseEntered(MouseEvent e)`当鼠标进入组件时调用。**划入**   |
| `void`            | `mouseExited(MouseEvent e)`当鼠标退出组件时调用。**划出**    |
| `void`            | `mousePressed(MouseEvent e)`在组件上按下鼠标按钮时调用。**按下不松** |
| `void`            | `mouseReleased(MouseEvent e)`在组件上释放鼠标按钮时调用。**松开** |

**KeyListener键盘监听机制**

| Modifier and Type | Method and Description                                       |
| :---------------- | :----------------------------------------------------------- |
| `void`            | `keyPressed(KeyEvent e)`按下键时调用。即**按下不松**时调用   |
| `void`            | `keyReleased(KeyEvent e)`当键已被释放时调用。即**松开**时调用 |
| `void`            | `keyTyped(KeyEvent e)`键入键时调用。一般不用                 |

```java
//给整个窗体添加键盘监听
//调用者this:本类对象，当前的界面对象，表示我要给整个界面添加监听
//addKeyListener: 表示要给本界面添加键盘监听
//参数this:当事件被触发之后，会执行本类中的对应代码
this.addKeyListener(this);
```

```java
@Override
public void keyReleased(KeyEvent e){
    System.out.printn("松开按键");
    //获取键盘上每一个按键的编号
    int code = e.getKeyCode();
    if(code == 65){
        System.out.println("A")
    }else if(code == 66){
        System.out.println("B")
    }
}
```



## Border

Border是一个边框

```
jLabel1.setBorder(new BevelBorder(1));//表示设置斜面边框，1为下凹，0为凸出
```



## 弹窗

JDialog是弹窗类

```java
System.out.println("公众号");
//创建一个弹框对象
JDialog jDialog = new JDialog();
//创建一个管理图片的容器对象JLabel
JLabel jLabel = new JLabel(new ImageIcon("image/about.png"));
//设置位置和宽高
jLabel.setBounds(0, 0, 430, 430);
//把图片添加到弹框中
jDialog.getContentPane().add(jLabel);
//设置弹框大小
jDialog.setSize(500,500);
//让弹框置顶
jDialog.setAlwaysOnTop(true);
//让弹框居中
jDialog.setLocationRelativeTo(null);
//弹框不关闭无法操作下面的界面
jDialog.setModal(true);
//让弹窗显示出来
jDialog.setVisible(true);
```



# 线程

## 线程相关概念

- 程序

  是为完成特定任务、用某种语言编写的一组指令的集合
  简单的说:就是我们写的代码

- 进程

  1. 进程是指运行中的程序，比如我们使用QQ，就启动了一个进程，操作系统就会为该进程分配内存空间。当我们使用迅雷，又启动了一个进程，操作系统将为迅雷分配新的内存空间
  2. 进程是程序的一次执行过程，或是正在运行的一个程序。是动态过程：有它自身的产生、存在和消亡的过程

- 线程

  1. 线程由进程创建的，是进程的一个实体
  2. 一个进程可以拥有多个线程

- 其他相关概念

  1. 单线程：同一个时刻，只允许执行一个线程
  2. 多线程：同一个时刻，可以执行多个线程，比如：一个qq进程，可以同时打开多个聊天窗口，一个迅雷进程，可以同时下载多个文件
  3. 并发：同一个时刻，多个任务交替执行，造成一种“貌似同时”的错觉，简单的说，单核cpu实现的多任务就是并发
  4. 并行：同一个时刻，多个任务同时执行，多核cpu可以实现并行



## 线程的基本使用

**创建线程的两种方式：**

1. 继承Thread 类，重写 run方法

   ```java
   public class Thread01 {
       public static void main(String[] args) throws InterruptedException {
   
           //创建Cat对象，可以当做线程使用
           Cat cat = new Cat();
   
           /*
               (1)
               public synchronized void start() {
                   start0();
               }
               (2)
               //start0() 是本地方法，是JVM调用, 底层是c/c++实现
               //真正实现多线程的效果， 是start0(), 而不是 run
               private native void start0();
   
            */
   
           cat.start();//启动线程-> 最终会执行cat的run方法
   
   
           //cat.run();//run方法就是一个普通的方法, 没有真正的启动一个线程，就会把run方法执行完毕，才向下执行
           //说明: 当main线程启动一个子线程 Thread-0, 主线程不会阻塞, 会继续执行
           //这时 主线程和子线程是交替执行..
           System.out.println("主线程继续执行" + Thread.currentThread().getName());//名字main
           for(int i = 0; i < 60; i++) {
               System.out.println("主线程 i=" + i);
               //让主线程休眠
               Thread.sleep(1000);
           }
   
       }
   }
   
   //1. 当一个类继承了 Thread 类， 该类就可以当做线程使用
   //2. 我们会重写 run方法，写上自己的业务代码
   //3. run Thread 类 实现了 Runnable 接口的run方法
   /*
       @Override
       public void run() {
           if (target != null) {
               target.run();
           }
       }
    */
   
   class Cat extends Thread {
   
       int times = 0;
       @Override
       public void run() {//重写run方法，写上自己的业务逻辑
   
           while (true) {
               //该线程每隔1秒。在控制台输出 “喵喵, 我是小猫咪”
               System.out.println("喵喵, 我是小猫咪" + (++times) + " 线程名=" + Thread.currentThread().getName());
               //让该线程休眠1秒 ctrl+alt+t
               try {
                   Thread.sleep(1000);
               } catch (InterruptedException e) {
                   e.printStackTrace();
               }
               if(times == 80) {
                   break;//当times 到80, 退出while, 这时线程也就退出..
               }
           }
       }
   }
   ```

   <img src="https://pb.nichi.co/caution-giraffe-setup" style="zoom:70%;" /> 

2. 实现Runnable接口，重写 run方法

   1. java是单继承的，在某些情况下一个类可能已经继承了某个父类，这时在用继承Thread类方法来创建线程显然不可能了
   2. java设计者们提供了另外一个方式创建线程，就是通过实现Runnable接口来创建线程

   ```java
   public class Thread02 {
       public static void main(String[] args) {
           Dog dog = new Dog();
           //dog.start(); 这里不能调用start
           //创建了Thread对象，把 dog对象(实现Runnable),放入Thread
           Thread thread = new Thread(dog);
           thread.start();
       }
   }
   class Dog implements Runnable { //通过实现Runnable接口，开发线程
       int count = 0;
       @Override
       public void run() { //普通方法
           while (true) {
               System.out.println("小狗汪汪叫..hi" + (++count) + Thread.currentThread().getName());
               //休眠1秒
               try {
                   Thread.sleep(1000);
               } catch (InterruptedException e) {
                   e.printStackTrace();
               }
               if (count == 10) {
                   break;
               }
           }
       }
   }
   ```

**多线程执行应用案例：**

请编写一个程序，创建两个线程，一个线程每隔1秒输出 “hello,world”，输出10次，退出，一个线程每隔1秒输出"hi”，输出5次退出

```java
public class Thread03 {
    public static void main(String[] args) {
        T1 t1 = new T1();
        T2 t2 = new T2();
        Thread thread1 = new Thread(t1);
        Thread thread2 = new Thread(t2);
        thread1.start();//启动第1个线程
        thread2.start();//启动第2个线程
        //...
    }
}
class T1 implements Runnable {
    int count = 0;
    @Override
    public void run() {
        while (true) {
            //每隔1秒输出 “hello,world”,输出10次
            System.out.println("hello,world " + (++count));
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if(count == 60) {
                break;
            }
        }
    }
}
class T2 implements Runnable {
    int count = 0;
    @Override
    public void run() {
        //每隔1秒输出 “hi”,输出5次
        while (true) {
            System.out.println("hi " + (++count));
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if(count == 50) {
                break;
            }
        }
    }
}
```

**继承Thread和实现Runnable的区别：**

1. 从java的设计来看，通过继承Thread或者实现Runnable接口来创建线程本质上没有区别，从jdk帮助文档我们可以看到Thread类本身就实现了Runnable接口
2. 实现Runnable接口方式更加适合多个线程共享一个资源的情况，并且避免了单继承的限制，建议使用Runnable



## 线程终止

1. 当线程完成任务后，会自动退出
2. 还可以通过使用变量来控制run方法退出的方式停止线程，即通知方式

```java
public class ThreadExit_ {
    public static void main(String[] args) throws InterruptedException {
        T t1 = new T();
        t1.start();
        //如果希望main线程去控制t1 线程的终止, 必须可以修改 loop
        //让t1 退出run方法，从而终止 t1线程 -> 通知方式
        //让主线程休眠 10 秒，再通知 t1线程退出
        System.out.println("main线程休眠10s...");
        Thread.sleep(10 * 1000);
        t1.setLoop(false);
    }
}
class T extends Thread {
    private int count = 0;
    //设置一个控制变量
    private boolean loop = true;
    @Override
    public void run() {
        while (loop) {
            try {
                Thread.sleep(50);// 让当前线程休眠50ms
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("T 运行中...." + (++count));
        }
    }
    public void setLoop(boolean loop) {
        this.loop = loop;
    }
}
```



## 线程常用方法

1. setName //设置线程名称，使之与参数 name 相同

2. getName //返回该线程的名称

3. start //使该线程开始执行，Java 虚拟机底层调用该线程的 start0 方法

4. run //调用线程对象 run 方法

5. setPriority //更改线程的优先级

6. getPriority //获取线程的优先级

   | 名称          | 优先级 |
   | ------------- | ------ |
   | MAX_PRIORITY  | 10     |
   | MIN_PRIORITY  | 1      |
   | NORM_PRIORITY | 5      |

7. sleep //在指定的毫秒数内让当前正在执行的线程休眠 (暂停执行)

8. interrupt //中断线程，但没有真正结束线程，所以一般用于中断正在休眠线程

9. yield //线程的礼让。让出cpu，让其他线程执行，但礼让的时间不确定，所以也不一定礼让成功

10. join //线程的插队。插队的线程一旦插队成功，则肯定先执行完插入的线程所有的任务

11. getState //查看线程状态

11. 用户线程和守护线程

    1. 用户线程：也叫工作线程，当线程的任务执行完或通知方式结束
    2. 守护线程：一般是为工作线程服务的，当所有的用户线程结束，守护线程自动结束
    3. 常见的守护线程：垃圾回收机

    ```java
    MyDaemonThread dt = new MyDaemonThread0;
    //将dt 设置为守护线程，当所有线程结束后，dt也就自动结束
    // 如果没有设置，那么 即使main线程执行完毕，dt也不退出，可以体验一下
    dt.setDaemon(true);
    dt.start();//守护线程必须放在start方法前
    ```



## 线程的生命周期

 **JDK 中用 Thread.State 枚举表示了线程的几种状态：**

- NEW
  尚未启动的线程处于此状态
- RUNNABLE
  在Java虚拟机中执行的线程处于此状态
- BLOCKED被阻塞等待监视器锁定的线程处于此状态
- WAITING
  正在等待另一个线程执行特定动作的线程处于此状态
- TIMED_WAITING
  正在等待另一个线程执行动作达到指定等待时间的线程处于此状态
- TERMINATED
  已退出的线程处于此状态

**线程状态转换图：**

<img src="https://pb.nichi.co/trial-shuffle-isolate" style="zoom: 30%;" /> 



## 线程的同步

**线程同步机制：**

1. 在多线程编程，一些敏感数据不允许被多个线程同时访问，此时就使用同步访问技术，保证数据在任何同一时刻，最多有一个线程访问，以保证数据的完整性
2. 也可以这里理解：线程同步，即当有一个线程在对内存进行操作时，其他线程都不可以对这个内存地址进行操作，直到该线程完成操作，其他线程才能对该内存地址进行操作

**synchronized的3种使用方式：**

- 修饰实例方法：作用于当前实例加锁

  ```java
  public synchronized void method(){
     // todo
  }
  ```

- 修饰静态方法：作用于当前类对象加锁

  ```java
  public synchronized static void method(){
     // todo
  }
  ```

- 修饰代码块：指定加锁对象，对给定对象加锁

  ```java
  public void method(){
     synchronized(this) {
        // todo
     }
  }
  ```

**互斥锁：**

1. Java语言中，引入了对象互斥锁的概念，来保证共享数据操作的完整性。
2. 每个对象都对应于一个可称为“互斥锁”的标记，这个标记用来保证在任一时刻，只能有一个线程访问该对象
3. 关键字synchronized 来与对象的互斥锁联系，当某个对象用synchronized修饰时表明该对象在任一时刻只能由一个线程访问
4. 同步的局限性：导致程序的执行效率要降低
5. 同步方法（非静态的）的锁可以是this，也可以是其他对象(要求是同一个对象)
6. 同步（方法静态的）的锁为当前类本身

**注意：**

- 同步方法如果没有使用static修饰：默认锁对象为this
- 如果方法使用static修饰，默认锁对象：当前类.class
- 实现的落地步骤
  - 需要先分析上锁的代码
  - 选择同步代码块或同步方法
  - 要求多个线程的锁对象为同一个即可

- 在定义接口方法时不能使用synchronized关键字
- 构造方法不能使用synchronized关键字，但可以使用synchronized代码块来进行同步

[synchronized详解_codedot的博客-CSDN博客_synchronized](https://blog.csdn.net/m0_53474063/article/details/112389756)

**线程的死锁：**

> 多个线程都占用了对方的锁资源，但不肯让，导致了死锁

```java
public class DeadLock_ {
    public static void main(String[] args) {
        //模拟死锁现象
        DeadLockDemo A = new DeadLockDemo(true);
        A.setName("A线程");
        DeadLockDemo B = new DeadLockDemo(false);
        B.setName("B线程");
        A.start();
        B.start();
    }
}
//线程
class DeadLockDemo extends Thread {
    static Object o1 = new Object();// 保证多线程，共享一个对象,这里使用static
    static Object o2 = new Object();
    boolean flag;
    public DeadLockDemo(boolean flag) {//构造器
        this.flag = flag;
    }
    @Override
    public void run() {
        //下面业务逻辑的分析
        //1. 如果flag 为 T, 线程A 就会先得到/持有 o1 对象锁, 然后尝试去获取 o2 对象锁
        //2. 如果线程A 得不到 o2 对象锁，就会Blocked
        //3. 如果flag 为 F, 线程B 就会先得到/持有 o2 对象锁, 然后尝试去获取 o1 对象锁
        //4. 如果线程B 得不到 o1 对象锁，就会Blocked
        if (flag) {
            synchronized (o1) {//对象互斥锁, 下面就是同步代码
                System.out.println(Thread.currentThread().getName() + " 进入1");
                synchronized (o2) { // 这里获得li对象的监视权
                    System.out.println(Thread.currentThread().getName() + " 进入2");
                }
            }
        } else {
            synchronized (o2) {
                System.out.println(Thread.currentThread().getName() + " 进入3");
                synchronized (o1) { // 这里获得li对象的监视权
                    System.out.println(Thread.currentThread().getName() + " 进入4");
                }
            }
        }
    }
}
```

**释放锁：**

1. 当前线程的同步方法、同步代码块执行结束
2. 当前线程在同步代码块、同步方法中遇到break、return
3. 当前线程在同步代码块同步方法中出现了未处理的Error或Exception，导致异常结束
4. 当前线程在同步代码块同步方法中执行了线程对象的wait()方法，当前线程暂停，并释放锁

**下面操作不会释放锁：**

1. 线程执行同步代码块或同步方法时，程序调用Thread.sleep()、Thread.yield()方法暂停当前线程的执行，不会释放锁

2. 线程执行同步代码块时，其他线程调用了该线程的suspend()方法将该线程挂起，该线程不会释放锁

   提示：应尽量避免使用suspend()和resume()来控制线程，方法不再推荐使用



# IO流

>  推荐文章：[万字长文+思维导图帮你梳理 Java IO 流](https://blog.csdn.net/a1405/article/details/116766237)

## 常用的文件操作 

**创建文件对象相关构造器和方法：**

- `new File(String pathname)`：根据路径构建一个File对象
- `new File(File parent,String child)`：根据父目录文件+子路径创建
- `new File(String parent,String child)`：根据父目录+子路径构建

- `createNewFile()`：创建新文件

**获取文件相关信息常用方法：**

- `getName()`：返回由此抽象路径名表示的文件或目录的名称。

- `getAbsolutePath()`：返回此抽象路径名的绝对路径名字符串
- `getParent()`：返回此抽象路径名的父 null的路径名字符串，如果此路径名未命名为父目录，则返回null
- `length()`：返回由此抽象路径名表示的文件的长度
- `exists()`：测试此抽象路径名表示的文件或目录是否存在
- `isFile()`：测试此抽象路径名表示的文件是否为普通文件
- `isDirectory()`：测试此抽象路径名表示的文件是否为目录

**目录的操作和文件删除：**

- `mkdir()`：创建一级目录
- `mkdirs()`：创建多级目录
- `delete()`：删除空目录或文件



##  IO流原理及流的分类

**Java IO 流原理：**

1. I/O是Input/Output的缩写，I/O技术是非常实用的技术，用于处理数据传输。如读/写文件，网络通讯等
2. Java程序中，对于数据的输入/输出操作以“流(stream)”的方式进行
3. java.io 包下提供了各种“流”类和接口，用以获取不同种类的数据，并通过方法输入或输出数据
4. 输入input：读取外部数据（磁盘、光盘等存储设备的数据）到程序（内存）中
5. 输出output：将程序（内存）数据输出到磁盘、光盘等存储设备中

**流的分类：**

- 按操作数据单位不同分为：字节流（8 bit）二进制文件，字符流（按字符）文本文件
- 按数据流的流向不同分为：输入流，输出流
- 按流的角色的不同分为：节点流，处理流/包装流

| 抽象基类 | 字节流       | 字符流 |
| -------- | ------------ | ------ |
| 输入流   | InputStream  | Reader |
| 输出流   | OutputStream | Writer |

- Java的IO流共涉及40多个类，实际上非常规则，都是从如上4个抽象基类派生的
- 由这四个类派生出来的子类名称都是以其父类名作为子类名后缀



## IO流常用类

### 体系图

<img src="https://pb.nichi.co/enhance-hurry-future" style="zoom:50%;" /> 

<img src="https://pb.nichi.co/million-perfect-fiscal" style="zoom: 40%;" /> 

### FileInputStream 和 FileOutputSteram

**文件拷贝：**

```java
import java.io.*;
public class FileCopy {
    public static void main(String[] args) {
        //完成 文件拷贝
        //思路分析
        //1. 创建文件的输入流 , 将文件读入到程序
        //2. 创建文件的输出流， 将读取到的文件数据，写入到指定的文件.
        String srcFilePath = "e:\\Koala.jpg";
        String destFilePath = "e:\\Koala1.jpg";
        FileInputStream fileInputStream = null;
        FileOutputStream fileOutputStream = null;
        try {
            fileInputStream = new FileInputStream(srcFilePath);
            fileOutputStream = new FileOutputStream(destFilePath);
            //定义一个字节数组,提高读取效果
            byte[] buf = new byte[1024];
            int readLen = 0;
            while ((readLen = fileInputStream.read(buf)) != -1) {
                //读取到后，就写入到文件 通过 fileOutputStream
                //即，是一边读，一边写
                fileOutputStream.write(buf, 0, readLen);//一定要使用这个方法
            }
            System.out.println("拷贝ok~");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                //关闭输入流和输出流，释放资源
                if (fileInputStream != null) {
                    fileInputStream.close();
                }
                if (fileOutputStream != null) {
                    fileOutputStream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

**常用方法：**

- FileInputStream：
  - 构造器：`FileInputStream(File file)` `FileInputStream(String name)`
  - 读取：`read()` `read(byte[]) ` `read(byte[] b, int off, int len)`
  - 关闭：`close()`
- FileOutputStream：
  - 构造器：`FileOutputStream(file, boolean append)`仅摘要一个，append为true表示将续页文件，false表覆盖
  - 写入：`write(byte[] b)` `write(byte[] b, int off, int len)` `write(int b)`
  - 关闭：`close()`

### FileReader 和 FileWriter

**常用方法：**

- FileReader：
  - new FileReader(File/String)
  - read:每次读取单个字符，返回该字符，如果到文件未尾返回
  - read(char[]):批量读取多个字符到数组，返回读取到的字符数，如果到文件未尾返回-1
  - 相关API:
    - new String(char[])：将char[]转换成String
    - new String(char[],off,len)：将char[]的指定部分转换成String
- FileWriter：
  - new FileWriter(File/String): 覆盖模式，相当于流的指针在首端
  - new FileWriter(File/String,true): 追加模式，相当于流的指针在尾端
  - write(int): 写入单个字符
  - write(char[]): 写入指定数组
  - write(char[],off,len): 写入指定数组的指定部分
  - write (string): 写入整个字符串
  - write(string,off,len): 写入字符串的指定部分
  - 相关API: String类: toCharArray:将String转换成char[]
  - **注意**:FileWriter使用后，**必须**要关闭(close)或刷新(flush)，否则写入不到指定的文件！



## 节点流和处理流

### 基本介绍

- 节点流可以从一个特定的数据源读写数据，如FileReader、FileWriter
- 处理流（也叫包装流）是“连接“在已存在的流（节点流或处理流）之上，为程序提供更为强大的读写功能，也更加灵活，如BufferedReader、BufferedWriter
- 关闭处理流时，只需要关闭外层流即可（关闭处理流时系统自动关闭节点流）

<img src="https://pb.nichi.co/relax-traffic-puppy" style="zoom: 33%;" /> 

**节点流和处理流的区别和联系：**

1. 节点流是底层流/低级流,直接跟数据源相接
2. 处理流（包装流）包装节点流，既可以消除不同节点流的实现差异，也可以提供更方便的方法来完成输入输出
3. 处理流（也叫包装流）对节点流进行包装，使用了修饰器设计模式，不会直接与数据源相连

**处理流的功能主要体现在以下两个方面：**

1. 性能的提高：主要以增加缓冲的方式来提高输入输出的效率

2. 操作的便捷：处理流提供了一系列便捷的方法来一次输入输出大批量的数据，使用更加灵活

### BufferedReader 和 BufferedWriter

- BufferedReader 和 BufferedWriter 属于字符流，是按照字符来读取数据的
- 关闭处理流时，只需要关闭外层流即可

**BufferedReader：**

```java
public class BufferedReader_ {
    public static void main(String[] args) throws Exception{
        String filePath = "d:\\hello.txt";
        BufferedReader bufferedReader = new BufferedReader(new FileReader(filePath));
        String line;
        //bufferedReader.readLine()按行读取
        while ((line = bufferedReader.readLine()) != null){//当返回 null 时，表示文件读取完毕
            System.out.println(line);
        }
        bufferedReader.close();//底层会调用FileReader.close()
    }
}
```

**BufferedWriter:**

```java
public class BufferedWriter_ {
    public static void main(String[] args) throws Exception {
        String filePath = "d:\\hello.txt";
        //如果想要追加，则在创建节点流处设置为true
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(filePath,true));
        bufferedWriter.write("hello");
        bufferedWriter.newLine();//插入一个和系统相关的换行
        bufferedWriter.write("hi");
        bufferedWriter.close();
    }
}
```

### 处理流-BufferedInputStream 和 BufferedOutputStream

- BufferedInputStream是字节流，在创建BufferedInputStream时，会创建一个内部缓冲区数组

- BufferedOutputStream是字节流，实现缓冲的输出流，可以将多个字节写入底层输出流中，而不必对每次字节写入调用底层系统

```java
public class Study {
    public static void main(String[] args) throws Exception {
        String srcPath = "D:\\abc.png";
        String destPath = "D:\\bcd.png";
        BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream(srcPath));
        BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(new FileOutputStream(destPath));
        byte[] readbuff = new byte[1024];
        int readLen;
        while ((readLen = bufferedInputStream.read(readbuff)) != -1){
            bufferedOutputStream.write(readbuff,0,readLen);
        }
        bufferedInputStream.close();
        bufferedOutputStream.close();
        System.out.println("拷贝完成~~");
    }
}
```

### 对象流-ObjectInputStream 和 ObjectOutputStream

**序列化和反序列化：**

1. 序列化就是在保存数据时，保存数据的值和数据类型
2. 反序列化就是在恢复数据时，恢复数据的值和数据类型
3. 需要让某个对象支持序列化机制，则必须让其类是可序列化的，为了让某个类是可序列化的，该类必须实现如下两个接口之一：
   - Serializable：这是一个标记接口，没有方法
   - Externalizable：该接口有方法需要实现，因此我们一般实现上面的 Serializable 接口

**对象流介绍：**

- 功能：提供了对基本类型或对象类型的序列化和反序列化的方法 
- ObjectOutputStream 提供**序列化**功能 
- ObjectInputStream 提供**反序列化**功能 

**ObjectOutStream：**

```java
public class ObjectOutStream_ {
    public static void main(String[] args) throws Exception {
        //序列化后，保存的文件格式，不是存文本，而是按照他的格式来保存
        String filePath = "e:\\data.dat";
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(filePath));
        //序列化数据到 e:\data.dat
        oos.writeInt(100);// int -> Integer (实现了 Serializable)
        oos.writeBoolean(true);// boolean -> Boolean (实现了 Serializable)
        oos.writeChar('a');// char -> Character (实现了 Serializable)
        oos.writeDouble(9.5);// double -> Double (实现了 Serializable)
        oos.writeUTF("你好世界");//String
        //保存一个dog对象
        oos.writeObject(new Dog("旺财", 10, "日本", "白色"));
        oos.close();
        System.out.println("数据保存完毕(序列化形式)");
    }
}
```

**ObjectInStream：**

```java
public class ObjectInputStream_ {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        //指定反序列化的文件
        String filePath = "e:\\data.dat";
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream(filePath));
        //1. 读取(反序列化)的顺序需要和你保存数据(序列化)的顺序一致
        //2. 否则会出现异常
        System.out.println(ois.readInt());
        System.out.println(ois.readBoolean());
        System.out.println(ois.readChar());
        System.out.println(ois.readDouble());
        System.out.println(ois.readUTF());
        //dog 的编译类型是 Object , dog 的运行类型是 Dog
        Object dog = ois.readObject();
        System.out.println("运行类型=" + dog.getClass());
        System.out.println("dog信息=" + dog);//底层 Object -> Dog
        //这里是特别重要的细节:
        //1. 如果我们希望调用Dog的方法, 需要向下转型
        //2. 需要我们将Dog类的定义，放在到可以引用的位置
        Dog dog2 = (Dog)dog;
        System.out.println(dog2.getName()); //旺财..
        //关闭流, 关闭外层流即可，底层会关闭 FileInputStream 流
        ois.close();
    }
}
```

**注意事项和细节说明：**

1. 读写顺序要一致
2. 要求序列化或反序列化对象需要 实现 Serializable
3. 序列化的类中建议添加SerialVersionUID，为了提高版本的兼容性
4. 序列化对象时，默认将里面所有属性都进行序列化，但除了static或transient修饰的成员
5. 序列化对象时，要求里面属性的类型也需要实现序列化接口
6. 序列化具备可继承性，也就是如果某类已经实现了序列化，则它的所有子类也已经默认实现了序列化

### 转换流-InputStreamReader 和 OutputStreamWriter

1. InputStreamReader：Reader的子类，可以将InputStream(字节流)包装成(转换)Reader(字符流)
2. OutputStreamWriter：Writer的子类，实现将OutputStream(字节流)包装成Writer(字符流)
3. 当处理纯文本数据时，如果使用字符流效率更高，并且可以有效解决中文问题，所以建议将字节流转换成字符流
4. 可以在使用时指定编码格式，比如：utf-8，gbk，gb2312，ISO8859-1等

**InputStreamReader：**

```java
public class InputStreamReader_ {
    public static void main(String[] args) throws IOException {
        String filePath = "e:\\a.txt";
        //1. 把 FileInputStream 转成 InputStreamReader
        //2. 指定编码 gbk
        //InputStreamReader isr = new InputStreamReader(new FileInputStream(filePath), "gbk");
        //3. 把 InputStreamReader 传入 BufferedReader
        //BufferedReader br = new BufferedReader(isr);
        //将2 和 3 合在一起
        BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream(filePath), "gbk"));
        //4. 读取
        String s = br.readLine();
        System.out.println("读取内容=" + s);
        //5. 关闭外层流
        br.close();
    }
}
```

**OutputStreamWriter：**

```java
// 1.创建流对象
OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("d:\\a.txt"), "gbk");
// 2.写入
osw.write("hello,韩顺平教育~");
// 3.关闭
osw.close();
System.out.println("保存成功~");
```

### 标准输入输出流

| 名称                | 类型        | 默认设备 |
| ------------------- | ----------- | -------- |
| System.in 标准输入  | InputStream | 键盘     |
| System.out 标准输出 | PrintStream | 显示器   |

```java
public class InputAndOutput {
    public static void main(String[] args) {
        //System 类 的 public final static InputStream in = null;
        // System.in 编译类型   InputStream
        // System.in 运行类型   BufferedInputStream
        // 表示的是标准输入 键盘
        System.out.println(System.in.getClass());

        //1. System.out public final static PrintStream out = null;
        //2. 编译类型 PrintStream
        //3. 运行类型 PrintStream
        //4. 表示标准输出 显示器
        System.out.println(System.out.getClass());

        System.out.println("hello, 世界");

        Scanner scanner = new Scanner(System.in);
        System.out.println("输入内容");
        String next = scanner.next();
        System.out.println("next=" + next);
        
    }
}
```

### 打印流-PrintStream 和 PrintWriter

**PrintStream：**

```java
public class PrintStream_ {
    public static void main(String[] args) throws IOException {
        PrintStream out = System.out;
        //在默认情况下，PrintStream 输出数据的位置是 标准输出，即显示器
        /*
             public void print(String s) {
                if (s == null) {
                    s = "null";
                }
                write(s);
            }
         */
        out.print("hello");
        //因为print底层使用的是write , 所以我们可以直接调用write进行打印/输出
        out.write("你好，世界".getBytes());
        out.close();
        //我们可以去修改打印流输出的位置/设备
        //1. 输出修改成到 "e:\\f1.txt"
        //2. "hello,你好世界" 就会输出到 e:\f1.txt
        //3. public static void setOut(PrintStream out) {
        //        checkIO();
        //        setOut0(out); // native 方法，修改了out
        //   }
        System.setOut(new PrintStream("e:\\f1.txt"));
        System.out.println("hello,你好世界");
    }
}
```

**PrintWriter：**

```java
public class PrintWriter_ {
    public static void main(String[] args) throws IOException {
        //PrintWriter printWriter = new PrintWriter(System.out);
        PrintWriter printWriter = new PrintWriter(new FileWriter("e:\\f2.txt"));
        printWriter.print("hi, 北京你好~~~~");
        printWriter.close();//flush + 关闭流, 才会将数据写入到文件..
    }
}
```



## Properties 类

**基本介绍：**

1. 专门用于读写配置文件的集合类

   配置文件格式：

   键=值

   键=值

2. 注意：键值对不需要有空格，值不需要用引号引起来，默认是String类型

3. Properties的常见方法

   - load：加载配置文件的键值对到Properties对象
   - list：将数据显示到指定设备
   - getProperty(key)：根据键获取值
   - setProperty(key,value)：设置键值对到Properties对象
   - store：将Properties中的键值对存储到配置文件，在idea中，保存信息到配置文件，如果含有中文，会存储为Unicode码

```java
public class Properties02 {
    public static void main(String[] args) throws IOException {
        //使用Properties 类来读取mysql.properties 文件
        //1. 创建Properties 对象
        Properties properties = new Properties();
        //2. 加载指定配置文件
        properties.load(new FileReader("src\\mysql.properties"));
        //3. 把k-v显示控制台
        properties.list(System.out);
        //4. 根据key 获取对应的值
        String user = properties.getProperty("user");
        String pwd = properties.getProperty("pwd");
        System.out.println("用户名=" + user);
        System.out.println("密码是=" + pwd);
        
        //创建
        //1.如果该文件没有key 就是创建
        //2.如果该文件有key ,就是修改
        properties.setProperty("charset", "utf8");
        properties.setProperty("user", "汤姆");//注意保存时，是中文的 unicode码值
        properties.setProperty("pwd", "888888");

        //将k-v 存储文件中即可
        properties.store(new FileOutputStream("src\\mysql2.properties"), null);
        System.out.println("保存配置文件成功~");
    }
}
```



# 网络编程

## 网络的相关概念

### 网络通信

1. 概念：两台设备之间通过网络实现数据传输
2. 网络通信：将数据通过网络从一台设备传输到另一台设备
3. java.net包下提供了一系列的类或接口，供程序员使用，完成网络通信

### 网络

1. 概念：两台或多台设备通过一定物理设备连接起来构成了网络
2. 根据网络的覆盖范围不同，对网络进行分类：
   - 局域网：覆盖范围最小，仅仅覆盖一个教室或一个机房
   - 城域网：覆盖范围较大，可以覆盖一个城市
   - 广域网：覆盖范围最大，可以覆盖全国，甚至全球，万维网是广域网的代表

### IP地址

1. 概念：用于唯一标识网络中的每台计算机/主机

2. 查看ip地址：ipconfig

3. ip地址的表示形式：点分十进制 xx.xx.xx.xx

4. 每一个十进制数的范围:0~255

5. ip地址的组成=网络地址+主机地址，比如：192.168.16.69

6. lPv6是互联网工程任务组设计的用于替代IPv4的下一代IP协议，其地址数量号称可以为全世界的每一粒沙子编上一个地址 

7. 由于IPv4最大的问题在于网络地址资源有限，严重制约了互联网的应用和发展。IPv6的使用，不仅能解决网络地址资源数量的问题，而且也解决了多种接入设备连入互联网的障碍

8. ipv4地址分类

   | 类型 | 范围                        |
   | ---- | --------------------------- |
   | A    | 0.0.0.0 - 127.255.255.255   |
   | B    | 128.0.0.0 - 191.255.255.255 |
   | C    | 192.0.0.0 - 223.255.255.255 |
   | D    | 224.0.0.0 - 239.255.255.255 |
   | E    | 240.0.0.0 - 247.255.255.255 |

   <img src="https://pb.nichi.co/blossom-solve-radio" style="zoom:50%;" /> 

### 域名

- 域名：
  1. 概念：将ip地址映射成域名，这里怎么映射上，HTTP协议
  2. 好处：为了方便记忆，解决记ip的困难
- 端口号：
  1. 概念：用于标识计算机上某个特定的网络程序
  2. 表示形式：以整数形式，端口范围0~65535 [2个字节表示端口 0~2^16-1]
  3. 0~1024已经被占用，比如 ssh 22，ftp 21，smtp 25，http 80
  4. 常见的网络程序端口号：
     - tomcat：8080
     - mysql：3306
     - oracle：1521
     - sqlserver：1433

### 网络通信协议

TCP/IP (Transmission Control Protocol/Internet Protocol) 的简写中文译名为传输控制协议/因特网互联协议，又叫网络通讯协议，这个协议是Internet最基本的协议、Internet国际互联网络的基础，简单地说，就是由网络层的IP协议和传输层的TCP协议组成的

<img src="https://pb.nichi.co/property-drive-unusual" style="zoom:50%;" /> 

### 网络通信协议

|  OIS模型   |   TCP/IP模型    |  TCP/IP模型各层对应协议   |
| :--------: | :-------------: | :-----------------------: |
|   应用层   |     应用层      | HTTP、ftp、telnet、DNS... |
|   表示层   |        ~        |             ~             |
|   会话层   |        ~        |             ~             |
|   传输层   |   传输层(TCP)   |        TCP、UDP...        |
|   网络层   |   网络层(IP)    |     IP、ICMP、ARP...      |
| 数据链路层 | 物理+数据链路层 |           Link            |
|   物理层   |        ~        |             ~             |

### TCP和UDP

- TCP协议：传输控制协议
  1. 使用TCP协议前，须先建立TCP连接，形成传输数据通道
  2. 传输前，采用“三次握手”方式，是**可靠的**
  3. TCP协议进行通信的两个应用进程：客户端、服务端在连接中可进行大数据量的传输
  4. 传输完毕，需释放已建立的连接，**效率低**
- UDP协议：用户数据协议
  1. 将数据、源、目的封装成数据包，不需要建立连接
  2. 每个数据报的大小限制在64K内，不适合传输大量数据
  3. 因无需连接，故是**不可靠的**
  4. 发送数据结束时无需释放资源（因为不是面向连接的），速度快



## InetAddress类

**相关方法：**

1. getLocalHost：获取本机InetAddress对象
2. getByName：根据指定主机名/域名获取ip地址对象
3. getHostName：获取InetAddress对象的主机名
4. getHostAddress：获取InetAddress对象的地址



## Socket

**基本介绍：**

1. 套接字(Socket)开发网络应用程序被广泛采用，以至于成为事实上的标准
2. 通信的两端都要有Socket，是两台机器间通信的端点
3. 网络通信其实就是Socket间的通信
4. Socket允许程序把网络连接当成一个流，数据在两个Socket间通过IO传输
5. 一般主动发起通信的应用程序属客户端，等待通信请求的为服务端

**常用方法：**

ServerSocket：

1. ServerSocker(int port) 构造器，创建绑定到指定端口的服务器套接字
2. accept() 侦听要连接到此套接字并接受它(即创建一个Socket对象)
3. close() 关闭

Socket：

1. Socket(InetAddress address, int port) 构造器，创建流套接字并将其连接到指定IP地址的指定端口号
2. getInputStream() 返回此套接字的输入流
3. getOutputStream() 返回此套接字的输出流
4. shutdownOutput() 禁用此套接字的输出流，即表示一个输出流传输完毕
5. close() 关闭

DatagramSocket：

1. DatagramSocket(int port) 构造器，构造数据报套接字并将其绑定到本地主机上的指定端口
2. receive(DatagramPacket p) 从此套接字接收数据报包
3. send(DatagramPacket p) 从此套接字发送数据报包
4. close() 关闭

DatagramPacket：

1. DatagramPacket(byte[] buf, int length) 构造器，构造一个 DatagramPacket用于接收长度的数据包 length
2. DatagramPacket(byte[] buf, int offset, int length, InetAddress address, int port) 构造器，构造用于发送长度的分组数据报包 length具有偏移 ioffset指定主机上到指定的端口号
3. getData() 返回数据缓冲区，即返回数据
4. getLength() 返回要发送的数据的长度或接收到的数据的长度



## TCP网络通信编程

**基本介绍：**

1. 基于客户端一服务端的网络通信
2. 底层使用的是TCP/IP协议
3. 应用场景举例：客户端发送数据，服务端接受并显示控制台
4. 基于Socket的TCP编程

**以文件传输演示使用方式：**

```java
//服务端
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
public class TCPFileUploadServer {
    public static void main(String[] args) throws Exception {

        //1. 服务端在本机监听8888端口
        ServerSocket serverSocket = new ServerSocket(8888);
        System.out.println("服务端在8888端口监听....");
        //2. 等待连接
        Socket socket = serverSocket.accept();

        //3. 读取客户端发送的数据
        //   通过Socket得到输入流
        BufferedInputStream bis = new BufferedInputStream(socket.getInputStream());
        byte[] bytes = StreamUtils.streamToByteArray(bis);
        //4. 将得到 bytes 数组，写入到指定的路径，就得到一个文件了
        String destFilePath = "src\\abc.mp4";
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(destFilePath));
        bos.write(bytes);
        bos.close();

        // 向客户端回复 "收到图片"
        // 通过socket 获取到输出流(字符)
        BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
        writer.write("收到图片");
        writer.flush();//把内容刷新到数据通道
        socket.shutdownOutput();//设置写入结束标记

        //关闭其他资源
        writer.close();
        bis.close();
        socket.close();
        serverSocket.close();
    }
}


//客户端
import java.io.*;
import java.net.InetAddress;
import java.net.Socket;
public class TCPFileUploadClient {
    public static void main(String[] args) throws Exception {

        //客户端连接服务端 8888，得到Socket对象
        Socket socket = new Socket(InetAddress.getLocalHost(), 8888);
        //创建读取磁盘文件的输入流
        String filePath = "e:\\abc.mp4";
        BufferedInputStream bis  = new BufferedInputStream(new FileInputStream(filePath));

        //bytes 就是filePath对应的字节数组
        byte[] bytes = StreamUtils.streamToByteArray(bis);

        //通过socket获取到输出流, 将bytes数据发送给服务端
        BufferedOutputStream bos = new BufferedOutputStream(socket.getOutputStream());
        bos.write(bytes);//将文件对应的字节数组的内容，写入到数据通道
        bis.close();
        socket.shutdownOutput();//设置写入数据的结束标记

        //=====接收从服务端回复的消息=====

        InputStream inputStream = socket.getInputStream();
        //使用StreamUtils 的方法，直接将 inputStream 读取到的内容 转成字符串
        String s = StreamUtils.streamToString(inputStream);
        System.out.println(s);

        //关闭相关的流
        inputStream.close();
        bos.close();
        socket.close();
    }
}


//引入一个StreamUtils工具包用于转换流成byte[]/String
import java.io.BufferedReader;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
/**
 * 此类用于演示关于流的读写方法
 *
 */
public class StreamUtils {
	/**
	 * 功能：将输入流转换成byte[]
	 * @param is
	 * @return
	 * @throws Exception
	 */
	public static byte[] streamToByteArray(InputStream is) throws Exception{
		ByteArrayOutputStream bos = new ByteArrayOutputStream();//创建输出流对象
		byte[] b = new byte[1024];
		int len;
		while((len=is.read(b))!=-1){
			bos.write(b, 0, len);	
		}
		byte[] array = bos.toByteArray();
		bos.close();
		return array;
	}
	/**
	 * 功能：将InputStream转换成String
	 * @param is
	 * @return
	 * @throws Exception
	 */
	public static String streamToString(InputStream is) throws Exception{
		BufferedReader reader = new BufferedReader(new InputStreamReader(is));
		StringBuilder builder= new StringBuilder();
		String line;
		while((line=reader.readLine())!=null){ //当读取到 null时，就表示结束
			builder.append(line+"\r\n");
		}
		return builder.toString();
	}
}
```

**netstat指令：**

1. netstat -an 可以查看当前主机网络情况，包括端口监听情况和网络连接情况
2. netstat - an | more 可以分页显示
3. netstat - anb  显示所有应用或进程名形式的地址和端口号
4. 状态LISTENING表示在监听，ESTABLISHED表示已建立连接



## UDP 网络通信编程

**基本介绍：**

1. 类 DatagramSocket 和 DatagramPacket [数据包/数据报] 实现了基于UDP协议网络程序
2. UDP数据报通过数据报套接字 DatagramSocket 发送和接收，系统不保证UDP数据报一定能够安全送到目的地，也不能确定什么时候可以抵达
3. DatagramPacket 对象封装了UDP数据报，在数据报中包含了发送端的IP地址和端口号以及接收端的IP地址和端口号
4. UDP协议中每个数据报都给出了完整的地址信息，因此无须建立发送方和接收方的连接

**基本流程：**

1. 核心的两个类/对象 DatagramSocket 与 DatagramPacket
2. 建立发送端，接收端（没有服务端和客户端概念）
3. 发送数据前，建立数据包/报 DatagramPacket对象
4. 调用DatagramSocket的发送、接收方法
5. 关闭DatagramSocket

**代码举例：**

```java
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.net.SocketException;
public class UDPReceiverA {
    public static void main(String[] args) throws IOException {
        //1. 创建一个 DatagramSocket 对象，准备在9999接收数据
        DatagramSocket socket = new DatagramSocket(9999);
        //2. 构建一个 DatagramPacket 对象，准备接收数据
        //   一个数据包最大 64k ,即 64 * 1024(byte)
        byte[] buf = new byte[1024];
        DatagramPacket packet = new DatagramPacket(buf, buf.length);
        //3. 调用 接收方法, 将通过网络传输的 DatagramPacket 对象
        //   填充到 packet对象
        //提示: 当有数据包发送到 本机的9999端口时，就会接收到数据
        //   如果没有数据包发送到 本机的9999端口, 就会阻塞等待
        System.out.println("接收端A 等待接收数据..");
        socket.receive(packet);

        //4. 可以把packet 进行拆包，取出数据，并显示.
        int length = packet.getLength();//实际接收到的数据字节长度
        byte[] data = packet.getData();//接收到数据
        String s = new String(data, 0, length);
        System.out.println(s);

        //===回复信息给B端
        //将需要发送的数据，封装到 DatagramPacket对象
        data = "好的, 明天见".getBytes();
        //说明: 封装的 DatagramPacket对象 data 内容字节数组 , data.length , 主机(IP) , 端口
        packet =
                new DatagramPacket(data, data.length, InetAddress.getByName("192.168.12.1"), 9998);

        socket.send(packet);//发送

        //5. 关闭资源
        socket.close();
        System.out.println("A端退出...");
    }
}

import java.io.IOException;
import java.net.*;
public class UDPSenderB {
    public static void main(String[] args) throws IOException {

        //1.创建 DatagramSocket 对象，准备在9998端口 接收数据
        DatagramSocket socket = new DatagramSocket(9998);

        //2. 将需要发送的数据，封装到 DatagramPacket对象
        byte[] data = "hello 明天吃火锅~".getBytes(); //

        //说明: 封装的 DatagramPacket对象 data 内容字节数组 , data.length , 主机(IP) , 端口
        DatagramPacket packet =
                new DatagramPacket(data, data.length, InetAddress.getByName("192.168.12.1"), 9999);
        
        socket.send(packet);

        //3.=== 接收从A端回复的信息
        //(1)   构建一个 DatagramPacket 对象，准备接收数据
        //   在前面讲解UDP 协议时，老师说过一个数据包最大 64k
        byte[] buf = new byte[1024];
        packet = new DatagramPacket(buf, buf.length);
        //(2)    调用 接收方法, 将通过网络传输的 DatagramPacket 对象
        //   填充到 packet对象
        //老师提示: 当有数据包发送到 本机的9998端口时，就会接收到数据
        //   如果没有数据包发送到 本机的9998端口, 就会阻塞等待.
        socket.receive(packet);

        //(3)  可以把packet 进行拆包，取出数据，并显示.
        int length = packet.getLength();//实际接收到的数据字节长度
        data = packet.getData();//接收到数据
        String s = new String(data, 0, length);
        System.out.println(s);

        //关闭资源
        socket.close();
        System.out.println("B端退出");
    }
}
```



# 反射

## Java Reflection

**简介：**

1. 反射机制允许程序在执行期借助于ReflectionAPI取得任何类的内部信息（比如成员变量，构造器，成员方法等等），并能操作对象的属性及方法，反射在设计模式和框架底层都会用到

2. 加载完类之后，在堆中就产生了一个Class类型的对象(一个类只有一个Class对象)，这个对象包含了类的完整结构信息。通过这个对象得到类的结构。这个Class对象就像一面镜子，透过这个镜子看到类的结构，所以，形象的称之为：反射

**Java 反射机制可以完成：**

1. 在运行时判断任意一个对象所属的类
2. 在运行时构造任意一个类的对象
3. 在运行时得到任意一个类所具有的成员变量和方法
4. 在运行时调用任意一个对象的成员变量和方法
5. 生成动态代理

**反射相关的主要类：**

1. java.lang.Class：代表一个类，Class对象表示某个类加载后在堆中的对象
2. java.lang.reflect.Method：代表类的方法，Method对象表示某个类的方法
3. java.lang.reflect.Field：代表类的成员变量，Field对象表示某个类的成员变量
4. java.lang.reflect.Constructor：代表类的构造方法，Constructor对象表示构造器

**反射优点和缺点：**

1. 优点：可以动态的创建和使用对象(也是框架底层核心)，使用灵活,没有反射制，框架技术就失去底层支撑
2. 缺点：使用反射基本是解释执行，对执行速度有影响

**反射调用优化（关闭访问检查）：**

1. Method和Field、Constructor对象都有setAccessible0方法
2. setAccessible作用是启动和禁用访问安全检查的开关
3. 参数值为true表示 反射的对象在使用时取消访问检查，提高反射的效率。参数值为false则表示反射的对象执行访问检查

## Class类

<img src="https://pb.nichi.co/glimpse-service-pear" style="zoom:50%;" /> 

1. Class也是类，因此也继承Object类
2. Class类对象不是new出来的，而是系统创建的
3. 对于某个类的Class类对象，在内存中只有一份，因为类只加载一次
4. 每个类的实例都会记得自己是由哪个 Class 实例所生成
5. 通过Class对象可以完整地得到一个类的完整结构，通过一系列API
6. Class对象是存放在堆的
7. 类的字节码二进制数据，是放在方法区的，有的地方称为类的元数据（包括 方法代码变量名，方法名，访问权限等等）

**常用方法：**

<img src="https://pb.nichi.co/tornado-craft-figure" style="zoom:50%;" /> 

**获取Class对象：**

1. 前提：已知一个类的全类名，且该类在类路径下，可通过Cass类的静态方法`forName()`获取，可能抛出`ClassNotFoundException`，实例：`Class cls1 = Class.forName("java.lang.Cat");`
   应用场景：多用于配置文件，读取类全路径，加载类

2. 前提：若已知具体的类，通过类的cass获取，该方式最为安全可靠，程序性能
   实例：`Class cls2 = Cat.class;`
   应用场景：多用于参数传递，比如通过反射得到对应构造器对象

3. 前提：已知某个类的实例，调用该实例的getClass0方法获取Class对象

   实例：`Class clazz=对象.getClass; //运行类型`
   应用场景：通过创建好的对象，获取Class对象

4. 其他方式
   `ClassLoader cl = 对象.getClass().getClassLoader();`
   `Class clazz4 = cl.loadClass("类的全类名”);`

5. 基本数据(int,char,boolean,float,double,byte,long,short)按如下方式得到Class类对象
   `Class cls = 基本数据类型.class;`

6. 基本数据类型对应的包装类，可以通过.TYPE得到Class类对象
   `Class cls = 包装类.TYPE;`

**哪些类型有 Class 对象：**

1. 外部类，成员内部类，静态内部类，局部内部类，匿名内部类
2. interface接口
3. 数组
4. enum枚举
5. annotation注解
6. 基本数据类型
7. void

## 类加载

反射机制是java实现动态语言的关键，也就是通过反射实现类动态加载。
1.静态加载：编译时加载相关的类，如果没有则报错，依赖性太强
2.动态加载：运行时加载需要的类，如果运行时不用该类，即使不存在该类，则不报错，降低了依赖性
**类加载时机：**

1. 当创建对象时(new) //静态加载
2. 当子类被加载时，父类也加载 //静态加载
3. 调用类中的静态成员时 //静态加载
4. 通过反射//动态加载`Class.forName("com.test.Cat");`

## 通过反射获取类的结构信息

**java.lang.Class 类：**

1. getName:获取全类名

2. getSimpleName:获取简单类名

3. getFields:获取所有public修饰的属性，包含本类以及父类的

4. getDeclaredFields:获取本类中所有属性

5. getMethods:获取所有public修饰的方法，包含本类以及父类的

6. getDeclaredMethods:获取本类中所有方法

7. getConstructors:获取本类所有public修饰的构造器

8. getDeclaredConstructors:获取本类中所有构造器

9. getPackage:以Package形式返包信息

10. getSuperClass:以Class形式返回父类信息

11. getInterfaces:以Class[]形式返回接口信息

12. getAnnotations:以Annotation[]形式返回注解信息

**java.lang.reflect.Field 类：**

1. getModifiers:以int形式返回**修饰符**

   默认修饰符是0,public是1,private是2,protected是4,static是8,final是16

2. getType:以Class形式**返回类型**

3. getName:返回**属性名**

**java.lang.reflect.Method 类：**

1. getModifiers:以int形式返回修**饰符**
2. getReturnType:以Class形式获取**返回类型**
3. getName:返回**方法名**
4. getParameterTypes:以Class[]返回**参数类型数组**

**java.lang.reflect.Constructor类：**

1. getModifiers:以int形式返回**修饰符**
2. getName:返回**构造器**名（全类名）
3. getParameterTypes:以Class[]返回**参数类型数组**

## 通过反射

### 通过反射创建对象

1. 方式一：调用类中的public修饰的无参构造器

2. 方式二：调用类中的指定构造器

3. Class类相关方法
   newlnstance：调用类中的无参构造器，获取对应类的对象
   getConstructor(Class...clazz)：根据参数列表，获取对应的public构造器对象
   getDecalaredConstructor(Class...clazz):根据参数列表，获取对应的所有构造器对象

4. Constructor类相关方法
   setAccessible：暴破
   newlnstance(Object...obj)：调用构造器

### 通过反射访问类中的成员

**访问属性：**

1. 根据属性名获取Field对象
   `Field f = clazz对象.getDeclaredField(属性名);`

2. 暴破：`f.setAccessible(true); //f是Field`

3. 访问
   `f.set(o,值); //o表示对象`
   `syso(f.get(o); //o表示对象`

4. 注意：如果是静态属性，则set和get中的参数o，可以写成null

**访问方法 ReflecAccessMethod.java：**

1. 根据方法名和参数列表获取Method方法对象：
   `Method m = clazz.getDeclaredMethod(方法名,XX.class); //得到本类的所有方法`

2. 获取对象：`Object o = clazz.newlnstance();`

3. 暴破：`m.setAccessible(true);`

4. 访问：`Object returnValue = m.invoke(o,实参列表); //o就是对象`

5. 注意：如果是静态方法，则invoke的参数o，可以写成null



# 正则表达式

**字符类(只匹配一个字符)：**

| 表达式          | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| `[abc]`         | 只能是abc                                                    |
| `[^abc]`        | 除了abc之外的任何字符                                        |
| `[a-zA-Z]`      | a到z A到Z，包括（范围）                                      |
| `[a-d[m-p]]`    | a到d，或m到p                                                 |
| `[a-z&&[def]]`  | a-z和def的交集，为def (如果写成了一个&，那么此时&表示就不是交集了，而是一个简简单单的&符号) |
| `[a-z&&[^bc]]`  | a-z和非bc的交集，等同于`[ad-z]`                              |
| `[a-z&&[^m-p]]` | a到z和除了m到p的交集，等同于`[a-lq-z]`                       |

**元字符-字符匹配符：**

| 符号  | 含义                                                         |
| ----- | ------------------------------------------------------------ |
| `[ ]` | 可接收的字符列表                                             |
| `[^]` | 不可接收的字符列表                                           |
| `-`   | 连字符                                                       |
| `.`   | 匹配除\n以外的任何字符                                       |
| `\\d` | 匹配单个数字字符，相当于`[0-9]`                              |
| `\\D` | 匹配单个非数字字符，相当于`[^0-9]`                           |
| `\\w` | 匹配单个数字、大小写字母字符和下划线，相当于`[0-9a-zA-Z_]`   |
| `\\W` | 匹配非单个数字、大小写字母字符和下划线，相当于`[^0-9a-zA-Z_]` |
| \s    | 一个空白字符：`[\t\n\c0B\f\r]`                               |
| \S    | 非空白字符：`[^\s]`                                          |

**元字符-选择匹配符：**

| 符号 | 含义                       |
| ---- | -------------------------- |
| `|`  | 匹配“\|”之前或之后的表达式 |

**元字符-限定符：**

| 符号    | 含义                               |
| ------- | ---------------------------------- |
| `*`     | 指字符重复0次或n次（无要求）零到多 |
| `+`     | 指字符重复1次或n次（至少1次）1到多 |
| `?`     | 指字符重复0次或1次（最多1次）0到1  |
| `{n}`   | 只能输入n个字符                    |
| `{n,}`  | 指定至少n个匹配                    |
| `{n,m}` | 指定至少n个但不多于m个匹配         |

**元字符-定位符：**

| 符号  | 含义                 |
| ----- | -------------------- |
| `^`   | 指定起始字符         |
| `$`   | 指定结束字符         |
| `\\b` | 匹配目标字符的边界   |
| `\\B` | 匹配目标字符的非边界 |

**分组：**

| 构造形式          | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| `(pattern)`       | 非命名捕获。捕获匹配的子字符串。编号为零的第一个捕获是由整个正则表达式模式匹配的文本，其它捕获结果则根据左括号的顺序从1开始自动编号 |
| `(<name>pattern)` | 命名捕获。将匹配的子字符串捕获到一个组名称回或编号名称中。用于name的字符串不能包含任何标点符号，并且不能以数字开头。可以使用单引号替代尖括号，例如(?'name') |
| `(?:pattern)`     | 匹配 pattern 但不捕获该匹配的子表达式，即它是一个非捕获匹配，不存储供以后使用的匹配。这对于用“or”字符（\|）组合模式部件的情况很有用。例如：`industr(?:y|ies)`是比`industry|industries`更经济的表达式 |
| `(?=pattern)`     | 它是一个非捕获匹配。例如：`Windows(?=95|98|NT|2000)`匹配"Windows 2000"中的"Windows"，但不匹配"Windows 3.1"中的"Windows" |
| `(?!pattern)`     | 该表达式匹配不处于匹配pattern的字符串的起始点的搜索字符串。它是一个非捕获匹配。例如：`Windows(?!95|98|NT|2000)'`匹配"Windows 3.1"中的"Windows"，但不匹配"Windows 2000"中的"Windows" |

**Java正则表达式默认是区分字母大小写的，如何实现不区分大小写？**

- (?i)abc 表示abc都不区分大小写
- a(?i)bc 表示bc不区分大小写
- a((?i)b)c 表示只有b不区分大小写
- `Pattern pat = Pattern.compile(regEx, Pattern.CASE INSENSITIVE);`、

**常用类：**

- Pattern类
  pattern对象是一个正则表达式对象。Pattern类没有公共构造方法。要创建一个Pattern对象，调用其公共静态方法，它返回一个Pattern对象。该方法接受一个正则表达式作为它的第一个参数，比如：`Pattern r = Pattern.compile(pattern);`

- Matcher类
  Matcher 对象是对输入字符串进行解释和匹配的引擎。与Pattern类一样，Matcher也没有公共构造方法。你需要调用Pattern对象的matcher方法来获得一个Matcher对象

- PatternSyntaxException
  PatternSyntaxException 是一个非强制异常类，它表示一个正则表达式模式中的语法错误

```java
String content = "要查验的字符串";
String regStr = "正则表达式";
//字符串方法：public boolean matches(String regex)：判断是否与正则表达式匹配
Pattern pattern = Pattern.compile(regStr);
Matcher matcher = pattern.matcher(content);
while (matcher.find()) {
    System.out.println("找到 " + matcher.group(0));//0代表全部 1代表第一组 2代表第二组
}
```

**分组、捕获、反向引用：**

- 分组
  我们可以用圆括号组成一个比较复杂的匹配模式，那么一个圆括号的部分我们可以看作是一个子表达式/一个分组

- 捕获
  把正则表达式中子表达式/分组匹配的内容，保存到内存中以数字编号或显式命名的组里，方便后面引用，从左向右，以分组的左括号为标志，第一个出现的分组的组号为1，第二个为2，以此类推，组0代表的是整个正则式

- 反向引用
  圆括号的内容被捕获后，可以在这个括号后被使用，从而写出一个比较实用的匹配模式，这个我们称为反向引用，这种引用既可以是在正则表达式内部，也可以是在正则表达式外部，内部反向引用`\\`分组号，外部反向引用`$`分组号

**String 类中使用正则表达式：**

- 替换功能：`public String replaceAll(String regex,String replacement)`
- 判断功能：`public boolean matches(String regex) //使用Pattern和Matcher类 `
- 分割功能：`public String[] split(String regex)`

**常用表达式：**

```
一、校验数字的表达式
1 数字：^[0-9]*$
2 n位的数字：^\d{n}$
3 至少n位的数字：^\d{n,}$
4 m-n位的数字：^\d{m,n}$
5 零和非零开头的数字：^(0|[1-9][0-9]*)$
6 非零开头的最多带两位小数的数字：^([1-9][0-9]*)+(.[0-9]{1,2})?$
7 带1-2位小数的正数或负数：^(\-)?\d+(\.\d{1,2})?$
8 正数、负数、和小数：^(\-|\+)?\d+(\.\d+)?$
9 有两位小数的正实数：^[0-9]+(.[0-9]{2})?$
10 有1~3位小数的正实数：^[0-9]+(.[0-9]{1,3})?$
11 非零的正整数：^[1-9]\d*$ 或 ^([1-9][0-9]*){1,3}$ 或 ^\+?[1-9][0-9]*$
12 非零的负整数：^\-[1-9][]0-9"*$ 或 ^-[1-9]\d*$
13 非负整数：^\d+$ 或 ^[1-9]\d*|0$
14 非正整数：^-[1-9]\d*|0$ 或 ^((-\d+)|(0+))$
15 非负浮点数：^\d+(\.\d+)?$ 或 ^[1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0$
16 非正浮点数：^((-\d+(\.\d+)?)|(0+(\.0+)?))$ 或 ^(-([1-9]\d*\.\d*|0\.\d*[1-9]\d*))|0?\.0+|0$
17 正浮点数：^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$ 或 ^(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*))$
18 负浮点数：^-([1-9]\d*\.\d*|0\.\d*[1-9]\d*)$ 或 ^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$
19 浮点数：^(-?\d+)(\.\d+)?$ 或 ^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$

二、校验字符的表达式
1 汉字：^[\u4e00-\u9fa5]{0,}$
2 英文和数字：^[A-Za-z0-9]+$ 或 ^[A-Za-z0-9]{4,40}$
3 长度为3-20的所有字符：^.{3,20}$
4 由26个英文字母组成的字符串：^[A-Za-z]+$
5 由26个大写英文字母组成的字符串：^[A-Z]+$
6 由26个小写英文字母组成的字符串：^[a-z]+$
7 由数字和26个英文字母组成的字符串：^[A-Za-z0-9]+$
8 由数字、26个英文字母或者下划线组成的字符串：^\w+$ 或 ^\w{3,20}$
9 中文、英文、数字包括下划线：^[\u4E00-\u9FA5A-Za-z0-9_]+$
10 中文、英文、数字但不包括下划线等符号：^[\u4E00-\u9FA5A-Za-z0-9]+$ 或 ^[\u4E00-\u9FA5A-Za-z0-9]{2,20}$
11 可以输入含有^%&',;=?$\"等字符：[^%&',;=?$\x22]+
12 禁止输入含有~的字符：[^~\x22]+

三、特殊需求表达式
1 Email地址：^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$
2 域名：[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(/.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+/.?
3 InternetURL：[a-zA-z]+://[^\s]* 或 ^https://([\w-]+\.)+[\w-]+(/[\w-./?%&=]*)?$
4 手机号码：^(13[0-9]|14[5|7]|15[0|1|2|3|5|6|7|8|9]|18[0|1|2|3|5|6|7|8|9])\d{8}$
5 电话号码("XXX-XXXXXXX"、"XXXX-XXXXXXXX"、"XXX-XXXXXXX"、"XXX-XXXXXXXX"、"XXXXXXX"和"XXXXXXXX)：^(\(\d{3,4}-)|\d{3.4}-)?\d{7,8}$ 
6 国内电话号码(0511-4405222、021-87888822)：\d{3}-\d{8}|\d{4}-\d{7}
7 身份证号：
	15或18位身份证：^\d{15}|\d{18}$
	15位身份证：^[1-9]\d{7}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{3}$
	18位身份证：^[1-9]\d{5}[1-9]\d{3}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{4}$
8 短身份证号码(数字、字母x结尾)：^([0-9]){7,18}(x|X)?$ 或 ^\d{8,18}|[0-9x]{8,18}|[0-9X]{8,18}?$
9 帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$
10 密码(以字母开头，长度在6~18之间，只能包含字母、数字和下划线)：^[a-zA-Z]\w{5,17}$
11 强密码(必须包含大小写字母和数字的组合，不能使用特殊字符，长度在8-10之间)：^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,10}$ 
12 日期格式：^\d{4}-\d{1,2}-\d{1,2}
13 一年的12个月(01～09和1～12)：^(0?[1-9]|1[0-2])$
14 一个月的31天(01～09和1～31)：^((0?[1-9])|((1|2)[0-9])|30|31)$ 
15 钱的输入格式：
16 1.有四种钱的表示形式我们可以接受:"10000.00" 和 "10,000.00", 和没有 "分" 的 "10000" 和 "10,000"：^[1-9][0-9]*$ 
17 2.这表示任意一个不以0开头的数字,但是,这也意味着一个字符"0"不通过,所以我们采用下面的形式：^(0|[1-9][0-9]*)$ 
18 3.一个0或者一个不以0开头的数字.我们还可以允许开头有一个负号：^(0|-?[1-9][0-9]*)$ 
19 4.这表示一个0或者一个可能为负的开头不为0的数字.让用户以0开头好了.把负号的也去掉,因为钱总不能是负的吧.下面我们要加的是说明可能的小数部分：^[0-9]+(.[0-9]+)?$ 
20 5.必须说明的是,小数点后面至少应该有1位数,所以"10."是不通过的,但是 "10" 和 "10.2" 是通过的：^[0-9]+(.[0-9]{2})?$ 
21 6.这样我们规定小数点后面必须有两位,如果你认为太苛刻了,可以这样：^[0-9]+(.[0-9]{1,2})?$ 
22 7.这样就允许用户只写一位小数.下面我们该考虑数字中的逗号了,我们可以这样：^[0-9]{1,3}(,[0-9]{3})*(.[0-9]{1,2})?$ 
23 8.1到3个数字,后面跟着任意个 逗号+3个数字,逗号成为可选,而不是必须：^([0-9]+|[0-9]{1,3}(,[0-9]{3})*)(.[0-9]{1,2})?$ 
24 备注：这就是最终结果了,别忘了"+"可以用"*"替代如果你觉得空字符串也可以接受的话(奇怪,为什么?)最后,别忘了在用函数时去掉去掉那个反斜杠,一般的错误都在这里
25 xml文件：^([a-zA-Z]+-?)+[a-zA-Z0-9]+\\.[x|X][m|M][l|L]$
26 中文字符的正则表达式：[\u4e00-\u9fa5]
27 双字节字符：[^\x00-\xff] (包括汉字在内，可以用来计算字符串的长度(一个双字节字符长度计2，ASCII字符计1))
28 空白行的正则表达式：\n\s*\r (可以用来删除空白行)
29 HTML标记的正则表达式：<(\S*?)[^>]*>.*?|<.*? /> (网上流传的版本太糟糕，上面这个也仅仅能部分，对于复杂的嵌套标记依旧无能为力)
30 首尾空白字符的正则表达式：^\s*|\s*$或(^\s*)|(\s*$) (可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式)
31 腾讯QQ号：[1-9][0-9]{4,} (腾讯QQ号从10000开始)
32 中国邮政编码：[1-9]\d{5}(?!\d) (中国邮政编码为6位数字)
33 IP地址：\d+\.\d+\.\d+\.\d+ (提取IP地址时有用)
```



# 数据库编程

暂无
