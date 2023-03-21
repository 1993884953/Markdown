

# Java 基础

## 一、HELLOW WORLD！

强类型语言

学习Java之前，需要准备好Java开发环境，

什么是JDK？Java Development Kit (JDK) 是Sun公司（已被Oracle收购）针对Java开发员的软件开发工具包。现在去下载并安装JDK 8版本 https://www.oracle.com/cn/java/technologies/javase-downloads.html

什么是IDE？ 集成开发环境（IDE，Integrated Development Environment ）。开发Java程序时，我们一般会选择一款IDE，来帮我们更方便的编程。 Java常用的IDE有Eclipse 、IntelliJ IDEA等。这里推荐使用IntelliJ IDEA，Ultimate版本是收费的提供30天试用，Community版本免费开源，下载地址 https://www.jetbrains.com/idea/

查看版本

```
java -version
```



编译Hello文件

>   纯文本编辑器需要打开控制台 cd到demo目录下src/目录

```
javac Hello.java
```

>   代码没有错后输出Hello.class

执行Hello这个文件

```
java Hello
```

>   不需要加class后缀，



### 1.1新建项目

java，别的都不选![image-20211123164849830](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213044.png)

回到idea首页 新建项目create New project文件名路路径

### 1.2新建类名

```java
//在java里面所有的东西都要装到类里面
//public 公共的
public class Hello {
    //static是静态的
    //void返回值类型，main不返回东西，
    //(String[] args) 参数 不能省略
    public static void main(String[] args) {
        //main tab自动生成main方法
        //默认执行某一个类里面的main方法，入口方法
        //sout tab{打印字符到控制台，调用.out.println()这个方法}
        System.out.println("hello world");
    }
}
//类名必须大写，文件名与类名保持一致         文件后缀为 .java
```

>   println("test")相当于print("test\n")就是一般的输出字符串，会自动换行
>
>   System.out.printf("i的值为%d,j的值为%.2f", i,j);
>
>   这里的"%.2f"的意思是输出两位小数点。如果想输出三位那就"%.3f"。

### 1.3数据类型与程序逻辑

>   Java提供了8种基本数据类型

```
4种整型: byte 、short 、int 、long
2种浮点类型: float 、double
1种字符型: char (Unicode编码的字符)
1种表示真假的布尔型: boolean
```

>   原始数据类型占用内存空间情况

| 数据类型             | 占用字节 | 默认值 | 包装类    | 取值范围                 |      |      |
| -------------------- | -------- | ------ | --------- | ------------------------ | ---- | ---- |
| byte(字节型)         | 1        | 0      | Byte      | -128 ~ 127               |      |      |
| short(短整型)        | 2        | 0      | Short     | -32768 ~ 32767           | %o   | 八进 |
| int(整型)            | 4        | 0      | Integer   | -2147483648 ~ 2147483647 | %d   | 十进 |
| long(长整型)         | 8        | 0L     | Long      |                          | %x   | 十六 |
| float(浮点型)        | 4        | 0.0F   | Float     |                          | %f   | %.2f |
| double(双精度浮点型) | 8        | 0.0    | Double    |                          | %g   |      |
| char(字符型)         |          |        | Character |                          | %c%s |      |
| boolean(布尔型)      |          |        | Boolean   |                          | %b   | true |

这么多数据类型，编程时该如何选用合适的类型？

-   整数：一般使用int类型，如果取值范围超出int就用long，如果取值范围较小可考虑使用short或byte节省内存占用
-   小数：一般使用double，如果取值范围小可以使用float节省内存占用

### 1.4巩固数据类型

>   某款机械手表技术参数为每月误差不超过3分钟，请计算1年最大误差为多少分钟?

```java
int error = 3;           // 每月最大误差值 
int total = error * 12;  // 计算1年12个月的累计误差值
System.out.printf("每月误差%d分钟，一年误差%d分钟", error, total);
```

>   当pi取值3.14时，计算半径为5.2cm的圆周长?

```java
double pi = 3.14; 
double r = 5.2;
double c = 2 * pi * r;
System.out.printf("半径 %.2f cm的圆，周长为 %.2f cm", r, c);
```

### 1.5、int、float、double

```java
public class App {
    public static void main(String[] args) {
//    int a=5;
//    int b=3;
//    int c=a/b; //此时c只会取整数部分，余数被丢掉
//        System.out.println(c);
//

//        float a = 5.1;  //会提示报错，要使用双精度的写法
        float a = 5.1f;
        int b = 3;
        float c=a/b;
        System.out.printf("去啊%.2f呀%n",c); //此时会四舍五入


        double e = 5.1;
        int  f= 3;
        double g=e/f;
        System.out.printf("去啊%.2f呀",g);
    }
}
```

### 1.6逻辑与循环分支if,for,while

```java
public class App {
    public static void main(String[] args) {
    int a=3;
    if(a==3){
        System.out.println("twdawaue");
    }else {
        System.out.println("fawe");
    }
    for (int i=0;i<=10;i++){
        System.out.print(i);
        while(i==5){
            i=i+1;
            System.out.printf("收到%d%n",i);
        }}
    }

}
```

### 1.7、面向对象

Java语言号称一切都是对象(原始数据类型是例外)，面向对象知识，在Java中就变得特别重要了，接下来我们学习Java中的面向对象基础

​	Hello.class

```java
public class Hello{
    public int age;
    public String name;
    public void Say(){
        System.out.printf("大家好，我叫%s,我今年%d岁",this.name,this.age);
    }
}
```

app.java

```java
public class App {
    public static void main(String[] args) {
        Hello user=new Hello();
        user.name="华哥";
        user.age=19;
        user.Say();
    }
}
```

### 1.8、获取控制台输入

如果想在控制台从键盘读入内容，需要用到`Scanner`类

```
import java.util.Scanner;      //  导入Scanner类

public class App{
    public static void main(String[] args) {

        Scanner scan = new Scanner(System.in);   // 实例化一个Scanner类的对象
        int number = scan.nextInt();             // 从键盘读入一个整数
        String name = scan.next();               // 从键盘读入字符串

        System.out.println(number);
        System.out.println(name);
        scan.close();                            // 关闭Scanner对象
    }
}
```

如果需要一次读入多个整数，可以在一行中输入多个整数后回车(空格隔开)，例如输入`123 456` 然回车，下面的变量a中，值就是123，变量b中的值是456

```javascript
Scanner scan = new Scanner(System.in); 
int a = scan.nextInt();   // 123
int b = scan.nextInt();   // 456
```

学习过C语言的同学，对 printf 会很熟悉，Java中的 System.out.printf 与之类似：

```javascript
System.out.printf("名字%s, 年龄%d岁, 身高%.2f\n", "Jack", 25, 1.8);
```

如果你有更复杂的格式化需求，可参考 http://www.daimaku.net/post/view/12665

### 1.9、控制输入训练

```
#深入理解计算机系统#价格[139.50]出版年份[2016]
```

>   输出只有一行，书名前后有一个#号，价格保留2位小数，价格和年份前后有中括号

```java
import java.util.Scanner;

public class App{
    public static void main(String[] args){

        Scanner scan = new Scanner(System.in);
        System.out.print("输入价格");
        double a = scan.nextInt();   // 123
        System.out.print("输入年份");
        int b = scan.nextInt();   // 456

        System.out.printf("#深入理解计算机系统#价格[%.2f]出版年份[%d]",a,b);
    }
}
```

>   任务卡 #1001 求两数之和

```
import java.util.Scanner;

public class App{
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in); 
        int a = scan.nextInt();   // 123
        int b = scan.nextInt();   // 456
        int c=a+b;
   
        System.out.println(c);
        scan.close(); 
    }
}
```

>   输出一个 `3` 行 `5` 列的矩形，符号使用 `#`

```java
import java.util.Scanner;

public class App{
    public static void draw(int height, int width, String stock){
       for(int o =0;o<height;o++){
           for(int i =0;i<width;i++){
               System.out.print(stock);
           }
           System.out.print("\n");
       }
    }


    public static void main(String[] args){

        Scanner scan = new Scanner(System.in);
        System.out.print("输入宽");
        int width= scan.nextInt();   // 123
        System.out.print("输入高");
        int height = scan.nextInt();   // 456
        System.out.print("输入符号");
        String stock = scan.next();   // 456

        draw(width,height,stock);
    }
}
```



### 2.0、图形训练

>   app.java

```java
import java.util.Scanner;

public class App {
    public static void main(String[] args) {

        System.out.print("请输入宽：");
        Scanner sc=new Scanner(System.in);
        int width= sc.nextInt();
        System.out.print("请输入高：");
        int height= sc.nextInt();
        System.out.printf("宽度为%d%n",width);
        System.out.printf("高为%d%n",height);
        
        Rectangle user=new Rectangle();
        user.draw(width,height);
    }
}
```

>   Rectangle.java

```java
public class Rectangle {

    public String sym="*";
    public String spe=" ";

    public void draw(int width,int height){
        for (int o = 0; o<height;o++){
            if(o==0||o==height-1){
                for (int i = 0; i<width; i++){
                    System.out.print(sym);
                }
            }else {
                System.out.print(sym);
                for (int i = 0; i<width-2; i++){
                    System.out.print(spe);
                }
                System.out.print(sym);
            }
            System.out.print("\n");
        }
    }
}
```

### 2.1、冒泡排序法

```
int[] arr = {2, 5, 1, 7, 8, 4, 3, 9, 4};
```

```java
//import java.util.Arrays;

public class App {
    public static void main(String[] args) {
        int[] arr = {2, 5, 1, 7, 8, 4, 3, 9, 4};
        for (int i=0;i<arr.length-1;i++){
            for(int o=0;o<arr.length-1;o++){
                int x=arr[o];
                int y=arr[o+1];
                if(x>y){
                    arr[o]=y;
                    arr[o+1]=x;
                }

            }


        }
        for (int i=0;i<arr.length-1;i++){
            System.out.printf("%d,",arr[i]);
        }
        System.out.print("\n");
//        Arrays.sort(arr);					short数组排序
//        for (int i=0;i<arr.length-1;i++){
//            System.out.printf("%d,",arr[i]);
//        }

    }
}
```

>   ## 冒泡排序

| *输入:*           |
| ----------------- |
| `7 5 1 4 2 9 7 4` |
| *输出:*           |
| `9 7 5 4 4 2 1`   |

```java
import java.util.Scanner;


public class App {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int len = scan.nextInt();
        int[] arr = new int[len];
        for (int i = 0; i < len; i++) {
            int num = scan.nextInt();
            arr[i] = num;
        }
        for (int i = 0; i < arr.length - 1; i++) {
            for (int o = 0; o < arr.length - 1; o++) {
                int x = arr[o];
                int y = arr[o + 1];
                if (x < y) {
                    arr[o] = y;
                    arr[o + 1] = x;
                }
            }
        }
        for (int i = 0; i < arr.length; i++) {
            if (i == arr.length - 1) {
                System.out.printf("%d", arr[i]);
            } else {
                System.out.printf("%d ", arr[i]);
            }
        }
    }
}
```



### 2.2、个人所得税计算器

```java
import java.util.Scanner;

public class App {
    public static void main(String[] args) {
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入工资数：");
        int money= sc.nextInt();
        System.out.println("请输入抵扣款：");
        int onPay= sc.nextInt();

        double pay = 0;
        double payMoney = 0;
        money=money-onPay;
        if(money<=5000){
            pay=0;
            payMoney=0;

        }
        if(5000<money&&money<=8000){
            pay=0.03;
            payMoney=(money-5000)*pay+payMoney;
        }
        if(8000<money&&money<=17000){
            pay=0.10;
            payMoney=(money-8000)*pay+payMoney;
        }
        if(17000<money&&money<=30000){
            pay=0.20;
            payMoney=(money-17000)*pay+payMoney;
        }
        if(30000<money&&money<=40000){
            pay=0.25;
            payMoney=(money-30000)*pay+payMoney;
        }

        if(40000<money&&money<=60000){
            pay=0.30;
            payMoney=(money-40000)*pay+payMoney;
        }
        if(60000<money&&money<=85000){
            pay=0.35;
            payMoney=(money-60000)*pay+payMoney;
        }
        if(money>85000){
            pay=0.45;
            payMoney=(money-85000)*pay+payMoney;
        }


        System.out.println("税率为："+pay*100 +"%");
        System.out.println("个税扣除："+payMoney+"元");
        System.out.printf("税后输入：%.0f元",(money-payMoney));

    }
}
```

## 二、Java中的集合

>   直接声明

```
int[] arr = {2, 5, 1, 7, 8, 4, 3, 9, 4};
```

>   不可以动态改变

```
int[] arr=new int[3];   //里面是长度，数组是定长的
```



### 数组

>   java中数组是一个对象

不声明初始值的时候需要new一个对象

```java
public class App {
    public static void main(String[] args) {
//    int[] arr={1,2,2,3,3,4,4}
    int[] arr=new int[3];   //里面是长度，数组是定长的
    arr[0]=11;
    arr[1]=11;
//        for (int j : arr) {
//            System.out.println(j);
//        }
        for (int i=0;i<arr.length;i++){
            System.out.println(arr[i]);
        }
    }
}
//有特定的长度，如果未赋值，为0
```

判断数据类型

```java
System.out.println(arr instanceof Object); //true
```

>   数组是对象只有一份，是引用的
>
>   数组的长度不可以改变，数组的索引不能越界

```java
public class App {
    public static void main(String[] args) {
//    int[] arr={1,2,2,3,3,4,4}
    int[] arr=new int[3];
    arr[0]=11;
    arr[1]=11;


    test(arr);
        for (int i=0;i<arr.length;i++){
            System.out.println(arr[i]);
        }
    }


    public static void test(int[] arr){
            arr[0]=555;
    }
}
```

>   ##

### List集合

>   头文件

```
import java.util.List;
import java.util.ArrayList;
```

>   方法

```java
List list=new ArrayList();	//new一个空的列表
list.add(11)  				//list增加为11的数据
list.get(1)  				//list下标为1的数据
list.size()					//list的长度
list.set(1, 222); 			//修改list的第二项
list.remove()				//删除list数据
```

>   List强制转换类型

```
User u = (User) list.get(i);
System.out.println(((User) o).name);  
```

#### 1.1、**List数组**

```java
import java.util.List;
import java.util.ArrayList;

public class App {
    public static void main(String[] args) {

        List list=new ArrayList();
        //ArrayList是一种list，list是一种接口
        //列表， 长度是动态改变的
        list.add(11);
        list.add(22);
        list.add(33);

        
        System.out.println(list.size());
        System.out.println(list.get(1));
        list.set(1,222);
        for (int i=0;i< list.size();i++){
            System.out.println(list.get(i));
        }
    }
}
```

#### **1.2、List对象**

```java
import java.util.List;
import java.util.ArrayList;

public class App {
    public static void main(String[] args) {

        List list = new ArrayList();
        //ArrayList是一种list，list是一种接口

        User user1 = new User();
        user1.name = "jack";
        //new一个user1类

        list.add(user1);
        //添加一个object对象

        for (int i = 0; i < list.size(); i++) {
            //System.out.println(list.get(i).name);
            //直接点name时会报错找不到之前的User类，所以要转换类型
            User u = (User) list.get(i);
            //(User)表示强制转换类型，转换为User的类
            System.out.println(u.name);
        }
        for (Object o : list) {
            System.out.println(((User) o).name);
        }
    }
}
```

#### 1.3、构造方法

```
//java构造方法，直接public 同名变量
//java可以单独同名构造方法，传入单独变量
```

```java
public class User{
    public String name;
    public int age;

    //java构造方法，直接public 同名变量
    public User(String name,int age) {
        this.name=name;
        this.age=age;
    }
    //java可以单独同名构造方法，传入单一变量
    public User(String name) {
        this.name=name;
        this.age=age;
    }
    
    
    
    //方法
    public void Say(String name,int age){
        System.out.printf("大家好，我叫%s,我今年%d岁",this.name,this.age);
    }

    @Override
    public String toString() {
        return "User{" +
                "age=" + age +
                ", name='" + name + '\'' +
                '}';
    }


}
```

#### 1.4、List对象

```java
import java.util.ArrayList;
import java.util.List;

import java.util.HashMap;
import java.util.Map;

public class App {
    public static void main(String[] args) {
        User user1 = new User("jack", 14);
        User user2 = new User("marry", 13);

        List<User> userList = new ArrayList<>();
        //map也是一个接口，hashmap是一个集合
        userList.add(user1);
        userList.add(user2);
        for (User obj : userList) {
            System.out.println(obj);
        }
    }
}
```



```java
import java.util.ArrayList;

public class App {
    public static void main(String[] args) {
        //ArrayList userList = new ArrayList();
        ArrayList<User> userList = new ArrayList<>();
        //范型集合,可以改变具体类型，只能装User对象，和子对象

        //调用了构造方法
        User user1 = new User("jack", 22);
        userList.add(user1);
        userList.add(new User("marry", 12));


        //for (int i=0;i<userList.size();i++){
        //User u= (User) userList.get(i);//原生写法需要重复声明
        //System.out.println(u.name);
        //}
        //原生写法简写
        //for (Object user : userList) {
        //System.out.iprintln(((User) user).name);
        //}//原生写法需要重复声明

        for (int i=0;i<userList.size();i++){
            System.out.println(userList.get(i).name);
        }//麻烦版

        for (User user : userList) {
            System.out.println(user.name);//泛型不需要声明
        }
    }
}
```

#### 1.5、map键值对

>   头部文件

```
import java.util.HashMap;
import java.util.Map;

 //map也是一个接口，hashmap是一个集合
List<User> userList = new ArrayList<>();
Map<String, User> map = new HashMap<>();
```

>   调用方法

```
map.put("A0001", user1);		//map增加为11的数据
map.containsKey("A0001")  		//检测有没有同名key值，有就返回true

//map循环
for(String key:map.keySet()){
	System.out.println("map循环："+map.get(key).name);
}
```

示例

```java
import java.util.ArrayList;
import java.util.List;

import java.util.HashMap;
import java.util.Map;

public class App {
    public static void main(String[] args) {
        User user1 = new User("jack", 14);
        User user2 = new User("marry", 13);

        List<User> userList = new ArrayList<>();
        //map也是一个接口，hashmap是一个集合
        userList.add(user1);
        userList.add(user2);
        for (User obj : userList) {
            System.out.println(obj);
        }
        
        Map<String, User> map = new HashMap<>();
        //map也是一个接口，hashmap是一个集合
        map.put("A0001", user1);
        map.put("A0002", user1);
        System.out.println("获取map："+map.get("A0001").name);

        //后面put同名key会覆盖之前的key
        map.put("A0001", user2);
        System.out.println("同名key："+map.get("A0001").name);

        //检测有没有同名key值，有就返回true
        System.out.println("检测key："+map.containsKey("A0001"));

        //map循环
        for(String key:map.keySet()){
            System.out.println("map循环："+map.get(key).name);
        }
        
    }
}
```

#### 1.6、set不重复

>   导入头部

```java
import java.util.HashSet;
import java.util.Set;

 Set<String> names = new HashSet<>();
```

>   方法

```
names.add("jack");					//添加jack
names.contains("jack");				//判断是否纯在jack
```

>   示例

```java
import java.util.HashSet;
import java.util.Set;

public class App {
    public static void main(String[] args) {
        User user1 = new User("jack", 14);
        User user2 = new User("marry", 13);

        Set<String> names = new HashSet<>();
        names.add("jack");
        names.add("marry");
        //names.add("marry");//不可以放重复数据

        System.out.println(names.contains("jack"));
        //得到true

        names.remove("jack");

        System.out.println(names.size());
        for (String name:names){
            System.out.println(name);
        }
    }
}
```

#### 2.0、饭卡充值系统

```java
import java.util.*;

public class App {


    public static void main(String[] args) {
        //定义一个list类
        List<User> userList = new ArrayList<>();
        //map类
        Map<String, Integer> sexMap = new HashMap<>();
        sexMap.put("匿名卡", 0);
        sexMap.put("男", 0);
        sexMap.put("女", 0);
        //班级信息
        List<Class> classList = new ArrayList<>();
        Class class1=new Class(1,"一班");
        classList.add(class1);
        Class class2=new Class(2,"二班");
        classList.add(class2);
        //初始两条信息
        User user1 = new User(2019110101, 1, "张三", 18, 1, 88.88);
        userList.add(user1);
        sexMap.put("男", 1);
        User user2 = new User(2019110102, 2, "王舞", 19, 2, 66.66);
        userList.add(user2);
        sexMap.put("女", 1);


        //while循环会一直存在
        while (true) {

            //菜单栏
            System.out.println("----------------------------------");
            System.out.println("请选择所需要的服务:");
            System.out.println("1、新增学生信息");
            System.out.println("2、充值饭卡");
            System.out.println("3、查看男女人数");
            System.out.println("4、学号遍历学生信息");
            System.out.println("5、班级遍历学生信息");
            System.out.println("6、查看班级信息");
            System.out.println("7、新增班级信息");
            System.out.println("----------------------------------");
            Scanner sc = new Scanner(System.in); //创建一个变量用来接收类
            int index = sc.nextInt();
            switch (index) {
                case 1: {
                    boolean state = true;
                    System.out.println("请输入学号:");
                    int studentID = sc.nextInt();
                    //判断学号是否存在
                    for (User user : userList) {
                        if (user.studentID == studentID) {
                            System.out.println("此学号已经存在，确认更新信息吗？");
                            System.out.println("1、确认 2、取消");
                            int payState = sc.nextInt();
                            state = payState == 1;
                            break;
                        }
                    }
                    if (!state) {
                        break;
                    }
                    System.out.println("请输入班级:");
                    int classID = sc.nextInt();
                    System.out.println("请输入姓名:");
                    String name = sc.next();
                    System.out.println("请输入年龄:");
                    int age = sc.nextInt();
                    //map信息表加男女数据
                    int sex;
                    while (true) {
                        System.out.println("请输入性别:");
                        System.out.println("1、男 2、女");
                        sex = sc.nextInt();
                        if (sex == 1) {
                            sexMap.put("男", sexMap.get("男") + 1);
                            break;
                        } else if (sex == 2) {
                            sexMap.put("女", sexMap.get("女") + 1);
                            break;
                        } else {
                            System.out.println("没有此性别，请重新输入");
                        }
                    }
                    System.out.println("请输入饭卡金额:");
                    double amount = sc.nextDouble();

                    //用户表更新成功
                    User users = new User(studentID, classID, name, age, sex, amount);
                    userList.add(users);
                    System.out.println("新增成功");

                    break;
                }
                case 2: {
                    boolean state = true;
                    System.out.println("输入学号：");
                    int studentID = sc.nextInt();
                    System.out.println("输入金额：");
                    int amount = sc.nextInt();
                    /* 存在时 */
                    for (User user : userList) {
                        if (user.studentID == studentID) {
                            user.amount = amount;
                            System.out.println("充值成功");
                            state = false;
                            break;
                        }
                    }
                    if (!state) {
                        break;
                    }
                    System.out.println("并没有此卡号，确认创建匿名卡吗:");
                    System.out.println("1、确认，2、取消:");
                    int payState = sc.nextInt();
                    if (payState != 1) {
                        System.out.println("取消成功:");
                        break;
                    }
                    User user = new User(studentID, amount);
                    userList.add(user);
                    System.out.println(userList.get(userList.size() - 1));
                    System.out.println("充值成功:");
                    sexMap.put("匿名卡", sexMap.get("匿名卡") + 1);
                    break;
                }
                case 3: {
                    System.out.println("匿名卡：" + sexMap.get("匿名卡"));
                    System.out.println("男：" + sexMap.get("男"));
                    System.out.println("女：" + sexMap.get("女"));
                    break;
                }
                case 4: {
                    System.out.println("学号    班级    姓名    年龄    性别    饭卡金额");
                    for (User user : userList) {
                        String sexName;
                        if (user.sex == 1) {
                            sexName = "男";
                        } else if (user.sex == 2) {
                            sexName = "女";
                        } else {
                            sexName = "匿名卡";
                        }

                        System.out.println(user.studentID + "  " + user.classID + "  " + sexName + "  " + user.name + "  " + user.age + "  " + user.amount);
                    }
                    break;
                }
                case 5:{
                    for (Class obj:classList){
                        System.out.println("班级："+obj.className);
                        System.out.println("学号     姓名    年龄    性别    饭卡金额");
                        boolean state=true;
                       for (User user:userList){
                           if(obj.classId==user.classID){
                               String sexName;
                               if (user.sex == 1) {
                                   sexName = "男";
                               } else if (user.sex == 2) {
                                   sexName = "女";
                               } else {
                                   sexName = "匿名卡";
                               }
                               System.out.println(user.studentID  + "  " + sexName + "  " + user.name + "  " + user.age + "  " + user.amount);
                               state=false;
                           }
                       }
                       if (state){
                           System.out.println("该班无学生");
                       }
                    }
                    break;
                }
                case 6:{
                    System.out.println("班级Id      班级名称");
                    for (Class obj:classList){
                        System.out.println(obj.classId+"   "+obj.className);
                    }
                    break;
                }
                case 7:{
                    boolean state=true;
                    System.out.println("请输入班级Id:");
                    int classId= sc.nextInt();
                    for (Class obj:classList){
                        if (obj.classId==classId){
                            System.out.println("确认更新吗:");
                            System.out.println("1、确认  2、取消:");
                            int keyState= sc.nextInt();
                            if (keyState==1){
                                System.out.println("请输入班级名称:");
                                obj.className= sc.next();
                                state=false;
                            }
                        }
                    }
                    if (!state){
                        break;
                    }
                    System.out.println("请输入班级名称:");
                    String className=sc.next();
                    Class class0 =new  Class(classId,className);
                    classList.add(class0);
                    break;
                }
            }
        }
    }
}
```

//班级管理类

```
public class Class {
    public int classId;
    public String className;

    public Class(int classId, String className) {
        this.classId = classId;
        this.className = className;
    }
}

```

//学生信息类

```
public class User{
    public int studentID;
    public int classID;
    public String name;
    public int age;
    public int sex;
    public double amount;
    public User(int studentID, int classID, String name, int age, int sex, double amount){
        this.studentID=studentID;
        this.classID=classID;
        this.name=name;
        this.age=age;
        this.sex=sex;
        this.amount=amount;
    }
    public User(int studentID, double amount){
        this.studentID=studentID;
        this.amount=amount;
    }
    @Override
    public String toString() {
        return "User{" +
                "studentID=" + studentID +
                ", classID=" + classID +
                ", name='" + name + '\'' +
                ", age=" + age +
                ", sex=" + sex +
                ", amount=" + amount +
                '}';
    }
}
```

```
 任务卡 #1016 单词比较
题目描述
输入两个单词，如果相同，则将一个单词转为大写后输出，如果不相同，则将两个单词字母交替连在一起后，转为小写输出

输入
共2行，每行一个英文单词

输出
如果单词相同，例如输入单词为两个 book，则输出 BOOK
```

```java
import java.util.Scanner;


public class App {
    public static void main(String[] args) {
        Scanner scanner=new Scanner(System.in);
        String A=scanner.next();
        String B=scanner.next();
        if (A.equals(B)){
            System.out.println(B.toUpperCase());
        }else{
            A=A.toLowerCase();
            B=B.toLowerCase();
            int length=Math.max(A.length(), B.length());
            for(int i=0;i<length;i++){
                if(i<A.length()){
                    System.out.print(A.charAt(i));
                }
                if(i<B.length()){
                    System.out.print(B.charAt(i));
                }
            }
        }
    }
}
```



## 三、java面向对象

### 1.1、public、private、protected

```
public 公共的 谁都可以用，
private 私有的 只能在本类里面使用
protected 受到保护的,只能在有继承关系的类里面使用
```

>   return的时候不写void ，但必须要规定返回值类型

### 1.2、oop三大特征封装、继承、多态

**封装**：就是把一些相关联的方法（步骤）放到一个方法的内部，调用时直接调用这个方法

**继承**： 可以继承一个父类，生成新的子类，可以添加新的属性和方法

**多态**: ( **重载** ，**重写**)   一个相同的方法名，却有多种用法



>   main

```java
public class Example {
    public static void main(String[] args) {
        RobotV2 robot = new RobotV2();
//        robot.open();
//        robot.put("大象");
//        robot.close();
    robot.save("秀儿");
        //方法return的时候需要打印
        System.out.println( robot.toke("秀儿"));

    }

}
```

>   RobotV1

```java
public class Robot {
    //oop封装、继承、多态
    //封装就是把一些相关功能封装到类的内部
    //public 公共的 谁都可以用，
    //private 私有的 只能在本类里面使用
    //protected 受到保护的,只能在有继承关系的类里面使用
    //封装就是把一些相关联的方法（步骤）放到一个方法的内部，调用时直接调用这个方法
    protected void  open(){
        System.out.println("冰箱门已经打开");
    }
    private void put(String sth){
        System.out.println(sth+"已经放入");
    }
    protected void close(){
        System.out.println("冰箱门已经关闭");
    }
    public void save(String sth){
        open();
        put(sth);
        close();
    }
}
```

>   RobotV2

```java
//继承 可以继承一个父类，生成新的子类，可以添加新的属性和方法
public class RobotV2 extends Robot{
    //返回值需要加类型
    private String get(String value){
        System.out.println(value+"取出");

        return value;
    }
    public String toke(String value){
        open();
        //用来接收函数的返回值
        String sth=get(value);
//        System.out.println(get(value));
        close();
        return  sth;
    }
}

```

### 1.3、多态的重载和重写

**多态**：方法名相同，实现的功能不同

**重载** (overload)：方法名相同，但参数不同，参数的类型或数量不能相同，可以自动识别类型，来调用

```java
import java.util.List;

public class Robot {
    //oop封装、继承、多态
    //封装就是把一些相关联的方法（步骤）放到一个方法的内部，调用时直接调用这个方法
    protected void  open(){
        System.out.println("冰箱门已经打开");
    }
    private void put(String sth){
        System.out.println(sth+"已经放入");
    }
    protected void close(){
        System.out.println("冰箱门已经关闭");
    }
    public void save(String sth){
        open();
        put(sth);
        close();
    }
    //重载 方法名相同，但参数不同，参数的类型或数量不能相同
    public void save(List<String> list){
        open();
        for (String sth:list){
           put(sth);
        }
        close();
    }

}
```

>   main

```java
import java.util.ArrayList;
import java.util.List;

public class App {
    public static void main(String[] args) {
        List <String>list=new ArrayList<>();
        list.add("秀儿一");
        list.add("秀儿二");
        list.add("秀儿三");

        Robot robot=new Robot();
        robot.save(list);
        robot.save("秀儿");
    }

}
```

**重写**(override)：*(方法的覆盖)* 在有继承关系的类里面，可以把父类的方法重写

>   重写父类的方法时，参数和类型一定要相同
>
>   可以在get(){}里用super.get(){}继承父类的get(){}

```java
//继承 可以继承一个父类，生成新的子类，可以添加新的属性和方法
public class RobotV2 extends Robot {

    //覆盖 *(方法的覆盖)* 在有继承关系的类里面，可以把父类的方法重写
    protected void open() {
        super.open();          //继承父类的方法
        System.out.println("冰箱门已经打开，一会记得关门");
    }


    //返回值需要加类型
    private String get(String value) {
        System.out.println(value + "取出");

        return value;
    }

    public String toke(String value) {

        open();
        //用来接收函数的返回值
        String sth = get(value);
//        System.out.println(get(value));
        close();
        return sth;
    }
}
```

### 1.4、this、super、static、final、abstract

#### 一、this 关键字

```
//ALT+Insert快捷键，快速自动生成返回和改变
```

-   this关键字，this代表当前对象本身
-   创建一个私有的属性通过this关键字改变
-   ALT+Insert快捷键，快速自动生成返回和改变

```java
//this关键字，this代表当前对象本身
public class Robot{
    //创建一个私有的属性通过this关键字改变
    private String name;
    //ALT+Insert快捷键，快速自动生成返回和改变
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

```java
public class Example {
    public static void main(String[] args) {
        Robot robot=new Robot();
        //robot.name无法直接访问类类里面的属性
        robot.setName("大象");//setName改变类的属性
        System.out.println(robot.getName());//获取属性
    }
}
```

#### 二、super关键字

- java里面继承的的时候不会继承构造方法

- 在没有写构造方法的时候会提供一个无参的构造方法

- super可以覆盖父类的function,可以在子类里面调用父类的构造方法

  ```java
  //this关键字，this代表当前对象本身
  public class Robot{
      //创建一个私有的属性通过this关键字改变
      private String name;
  
      //在没有写构造方法的时候会提供一个无参的构造方法
      public Robot(){
      } //构造方法的重载
  
      //在父类创建一个构造方法
      public Robot(String name){
          this.name=name;
      }
  
      //ALT+Insert快捷键，快速自动生成返回和改变
      public String getName() {
          return name;
      }
      public void setName(String name) {
          this.name = name;
      }
  }
  ```

  ```java
  //java里面继承的时候是不会继承构造方法的
  //父类有构造方法子类没有构造方法
  public class RobotV2 extends Robot{
      //Alt+Insert快速生成构造方法
      public RobotV2(String name) {
          //super可以在子类里面调用父类的构造方法
          super(name);
      }
  }
  ```

  ```java
  public class Example {
      public static void main(String[] args) {
  
          Robot robot=new Robot();
          //robot.name无法直接访问类类里面的属性
          robot.setName("大象");//setName改变类的属性
          System.out.println(robot.getName());//获取属性
  
          //父类没有写空的构造方法的时候会报错
          //想要不输入可以创建一个空的构造方法
          //RobotV2 robotV2=new RobotV2();
      }
  }
  
  ```

#### 三、static静态的

-   方法加上static就不属于对象或者属性了

-   静态方法,构建出来的不属于一个对像或者一个属性
-   需要通过类名来调用

```
public static void version(){
System.out.println("version--1.0");
}
```

-   调用的时候直接类名.方法名

```
Robot.version();
RobotV2.version();
```

-   直接覆盖父类的版本号，否则会继承

```
public static void version(){
    System.out.println("version--v2");
}
```

#### 四、final 终极

-   不可扩展，不可重写

-   在父类加上final，不能被子类继承

```
public final class Robot{

}
```

-   在方法加上final，不能被子类重写

```
 public final void setName(String name) {
        this.name = name;
    }
```

![image-20211126160517144](C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20211126160517144.png)

#### 五、abstract 抽象的

- 可以放在方法上面或者类名

- 抽象类没有对象，不能被实例化，不能被new出来

  ```
  public abstract class Robot{
  
  }
  ```

>抽象类的子类可以被实例化

![image-20211126161836441](C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20211126161836441.png)

- 抽象方法必须在抽象类里面，抽象方法不能有花括号

  

  ```
  private String names;
  public abstract void age();
  ```

- 子类必须完成抽象方法，抽象方法里面不能有主体

  >   子类也可以继续抽象这个方法

  ![image-20211126162845180](C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20211126162845180.png)

>   抽象类可以没有抽象方法，抽象方法必须有抽象类

## 四、 Java常用类

#### java文档

http://www.daimaku.net/book/javasdk/

#### String、StringBuffer与StringBuilder之间区别

| String                                                       | StringBuffer                                                 | StringBuilder    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------- |
| String的值是不可变的,这就导致每次对String的操作都会生成新的String对象,不仅效率低下,而且浪费大量有限的内存空间. | StringBuffer是可变类和线程安全的字符串操作类,任何对它指向的字符串的操作都不会产生新的对象.每个StringBuffer对象都有一定的缓冲区容量,每当字符串大小没有超过容量时,不会分配新的容量,当字符串大小超过容量时,会自动增加容量 | 可变类,速度更快  |
| 不可变                                                       | 可变                                                         | 可变             |
|                                                              | 线程安全                                                     | 线程不安全       |
|                                                              | 多线程操作字符串                                             | 单线程操作字符串 |

**String字符串拼接应该使用哪种方式？**

>我们所知道的字符串String的拼接有： “+” 、 concat () 方式实现，或者使用StringBuilder、StringBuffer类实现。这几种方式性能的从低到高进行排序，则顺序为：“+” <  concat () < StringBuffer < StringBuilder 。使用"+"性能是最差的，应该避免使用！！！
>
>StringBuilder的性能是最高的，大家可能在StringBuffer和StringBuilder之间不知道怎么取舍要用哪个？两者的区别是：StringBuffer是线程安全的，而StringBuilder不是。在高并发的应用中，应该考虑使用StringBuffer! ！
>
>大家查看JDK源码就可以知道，StringBuffer和StringBuilder这两个类实现的接口都是一样的，只不过 StringBuffer的很多方法都加上了synchronized关键字修饰。

```java
package utils;
public class StringAddTest
{
    public static void main(String args[]) {
        int num = 100000;
        testAdd(num);
        testConcat(num);
        testStringBuffer(num);
        testStringBuilder(num);
    }
 
    public static void testAdd(int num){
        long start = System.currentTimeMillis();
        String str = "";
        for(int i = 0; i < num; i++){
            str += i;
        }
        System.out.println("字符串拼接使用 + 耗时：" + (System.currentTimeMillis() - start) + "ms");
    }
 
    public static void testConcat(int num){
        long start = System.currentTimeMillis();
        String str = "";
        for(int i = 0; i < num; i++){
            str.concat(String.valueOf(i));
        }
        System.out.println("字符串拼接使用 concat 耗时：" + (System.currentTimeMillis() - start) + "ms");
    }
 
    public static void testStringBuffer(int num){
        long start = System.currentTimeMillis();
        StringBuffer stringBuffer = new StringBuffer();
        for(int i = 0; i < num; i++){
            stringBuffer.append(String.valueOf(i));
        }
        stringBuffer.toString();
        System.out.println("字符串拼接使用 StringBuffer 耗时：" + (System.currentTimeMillis() - start) + "ms");
    }
 
    public static void testStringBuilder(int num){
        long start = System.currentTimeMillis();
        StringBuilder stringBuilder = new StringBuilder();
        for(int i = 0; i < num; i++){
            stringBuilder.append(String.valueOf(i));
        }
        stringBuilder.toString();
        System.out.println("字符串拼接使用 StringBuilder 耗时：" + (System.currentTimeMillis() - start) + "ms");
    }
}

//运行结果
//字符串拼接使用 + : 183485ms
//字符串拼接使用 concat  耗时:23ms
//字符串拼接使用 StringBuffer  耗时:19ms
//字符串拼接使用 StringBulider 耗时:12ms
```



#### String

```java
public final class String
extends Object
```

`String` 类代表字符串,被final修饰。Java 程序中的所有字符串字面值（如 `"abc"` ）都作为此类的实例实现。字符串缓冲区支持可变的字符串。因为 String 对象是不可变的，所以可以共享。例如：

```
     String str = "abc";
等效于：
     char data[] = {'a', 'b', 'c'};
     String str = new String(data);
```

`charAt(int index)`  返回指定索引处的 `char` 值。

`concat(String str)`  将指定字符串连接到此字符串的结尾。

`contains(CharSequence s) ` 当且仅当此字符串包含指定的 char 值序列时，返回 true。

`equals(Object anObject)` 将此字符串与指定的对象比较。

```ABAP
使用 == 和 equals() 比较字符串。
String 中 == 比较引用地址是否相同，equals() 比较字符串的内容是否相同：
```

`indexOf(String str)` 返回指定子字符串在此字符串中第一次出现处的索引。

`split()`根据匹配给定的正则表达式来拆分此字符串。

`isEmpty()` 当且仅当 length() 为 0 时返回 true。

`length()` 返回此字符串的长度。

`substring(int beginIndex,[int endIndex])`     返回一个新字符串，它是此字符串的一个子字符串

`toString()` 返回此对象本身（它已经是一个字符串！）。

`toLowerCase()`将此 `String` 中的所有字符都转换为小写

`toUpperCase()` 将此 `String` 中的所有字符都转换为大写

`trim()`  返回字符串的副本，忽略前导空白和尾部空白

>常量声明，少量的字符串拼接操作等

#### StringBuffer

线程安全的可变字符序列。一个类似于 `String`的字符串缓冲区，但不能修改。虽然在任意时间点上它都包含某种特定的字符序列，但通过某些方法调用可以改变该序列的长度和内容。

`append` 始终将这些字符添加到缓冲区的末端

`insert` 指定的点添加字符

> "通常用于xml解析，html参数解析与封装"

#### StringBuilder

可变的字符序列。此类提供一个与 `StringBuffer` 兼容的 API，但不保证同步。该类被设计用作 `StringBuffer` 的一个简易替换，用在字符串缓冲区被单个线程使用的时候（这种情况很普遍）。如果可能，建议优先采用该类，因为在大多数实现中，它比 `StringBuffer` 要快。

`append` 始终将这些字符添加到缓冲区的末端

`insert` 指定的点添加字符

> "通常用于sql语句拼接，JSON封装等"

#### Math

用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。

`abs() `  返回 绝对值。 

`max(int a, int b) `  返回两个 int值中较大的一个。

`min(int a, int b) `  返回两个 int值中较小的一个。

`random()`  返回一个[0.0,1.0)的小数的伪随机double值.

#### Date

一个包装了毫秒值的瘦包装器 (thin wrapper)，它允许 JDBC 将毫秒值标识为 SQL `DATE` 值

`getTime` 返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 `Date` 对象表示的毫秒数。

`setTime(long date)` 使用给定毫秒时间值设置现有 Date 对象。

`toString()` 使用给定毫秒时间值设置现有 Date 对象。

#### Pattern

正则表达式的编译表示形式。

指定为字符串的正则表达式必须首先被编译为此类的实例。然后，可将得到的模式用于创建 [`Matcher`](http://www.daimaku.net/book/javasdk/java/util/regex/Matcher.html) 对象，依照正则表达式，该对象可以与任意[``字符序列``](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html)匹配。执行匹配所涉及的所有状态都驻留在匹配器中，所以多个匹配器可以共享同一模式。

因此，典型的调用顺序是

```
 Pattern p = Pattern.compile("a*b");
 Matcher m = p.matcher("aaaaab");
 boolean b = m.matches();
```

在仅使用一次正则表达式时，可以方便地通过此类定义 [`matches`](http://www.daimaku.net/book/javasdk/java/util/regex/Pattern.html#matches(java.lang.String, java.lang.CharSequence)) 方法。此方法编译表达式并在单个调用中将输入序列与其匹配。语句

```
 boolean b = Pattern.matches("a*b", "aaaaab");
```

等效于上面的三个语句，尽管对于重复的匹配而言它效率不高，因为它不允许重用已编译的模式。

此类的实例是不可变的，可供多个并发线程安全使用。[`Matcher`](http://www.daimaku.net/book/javasdk/java/util/regex/Matcher.html) 类的实例用于此目的则不安全。

## 五、Java操作MySQL

### MySQL安装

Windows系统安装MySQL可参考：

>   http://www.daimaku.net/post/view/10706

Linux 系统MySQL，可参考：

>   http://www.daimaku.net/post/view/10863

macOS系统MySQL，可参考：

>   https://www.cnblogs.com/nickchen121/p/11145123.html

#### windows系统

##### 一、下载

通过如下链接从官方网站下载MySQL

https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.13-winx64.zip

##### 二、解压

解压`mysql-5.7.13-winx64.zip`到 `D:\MySQL`

##### 三、管理员身份打开命令提示符

在系统的开始菜单上，单击鼠标右键，选择命令提示符(管理员)

![管理员运行.png](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213045.png)

也可以这样操作：`所有应用`->`Windows系统`中找到`命令提示符`，然后这时候在`命令提示符`上单击鼠标`右键`，选择以`管理员身份打开命令提示符`

##### 四、初始化数据库目录并安装服务

初始化数据目录 (如果报错，先安装 `Microsoft Visual C++2013`)

```
D:\MySQL\bin\mysqld --initialize-insecure --console
```

安装服务(开机自启动)，最后一个mysql表示服务名，如果不指定默认就是mysql

```
D:\MySQL\bin\mysqld --install mysql
```

启动服务

```
net start mysql
```

##### 五、终端连接

进入MySQL终端，输密码时直接回车(默认密码为空)

```
D:\MySQL\bin\mysql -uroot -p
```

如果需要可视化客户端，Windows下可以下载 `SQLyog`

##### 六、卸载

如果我们不再需要MySQL或是想要更换其它版本，可通过下面的方法，删除MySQL的服务

```
net stop mysql
D:\MySQL\bin\mysqld -remove mysql
```

#### Ubuntu 20.4 安装

##### 一、准备环境

```
$ cat /etc/issue
Ubuntu 20.04.2 LTS

# 安装MySQL依赖包
$ apt install  -y libaio1 libncurses*
```

##### 二、下载软件

从MySQL官网下载编译好的Linux二进制包

```
$ wget https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.13-linux-glibc2.5-x86_64.tar.gz
```

你也可以在本地电脑中提前下载好，通过scp等方式，上传到Linux中

##### 三、解压

解压到 /usr/local/ 目录中

```
$ tar -zxvf mysql-5.7.13-linux-glibc2.5-x86_64.tar.gz -C /usr/local/
```

进入 `/usr/local/`目录，将 `mysql-5.7.13-linux-glibc2.5-x86_64` 重命名为 `mysql/`

```
$ cd /usr/local/
$ mv mysql-5.7.13-linux-glibc2.5-x86_64 mysql/
```

##### 四、初始化数据库目录

创建一个叫做`mysql`的系统帐号

```
$ useradd -s /bin/false -M mysql

# 删除系统中默认MySQL配置文件
$ rm -f /etc/my.cnf /etc/mysql/my.cnf /usr/local/mysql/etc/my.cnf ~/.my.cnf

# 初始化数据库目录，执行成功后，在/usr/local/mysql中，将新产生一个data目录
$ /usr/local/mysql/bin/mysqld --initialize-insecure --user=mysql

[Warning] Gtid table is not ready to be used. Table 'mysql.gtid_executed' cannot be opened.
[Warning] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
```

##### 五、启动服务

```
/usr/local/mysql/bin/mysqld_safe --user=mysql &
```

##### 六、测试连接

进入MySQL(默认空密码，直接回车)

```
$ /usr/local/mysql/bin/mysql -uroot -p

Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.7.13 MySQL Community Server (GPL)

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

建库建表

```
mysql> create database test;
Query OK, 1 row affected (0.00 sec)

mysql> use test;
Database changed

mysql> create table t1 (id int primary key auto_increment, name varchar(50)) engine=innodb default charset=utf8mb4;
Query OK, 0 rows affected (0.00 sec)
```

插入数据

```
mysql> insert into t1 (name) values ('jack');
Query OK, 1 row affected (0.01 sec)

#  查询数据
mysql> select * from t1;
+----+------+
| id | name |
+----+------+
|  1 | jack |
+----+------+
1 row in set (0.00 sec)
```

退出MySQL

```
mysql> exit
```

##### 七、常见错误解决

error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory

```
$ apt install -y libaio1
```

error while loading shared libraries: libncurses.so.5: cannot open shared object file: No such file or directory

```
$ apt install  -y libncurses*
```

#### macos安装

目录

-   [一、安装](https://www.cnblogs.com/nickchen121/p/11145123.html#一、安装)
-   二、环境变量
    -   [2.1 MySQL服务的启停和状态的查看](https://www.cnblogs.com/nickchen121/p/11145123.html#21-mysql服务的启停和状态的查看)
-   [三、启动](https://www.cnblogs.com/nickchen121/p/11145123.html#三、启动)
-   四、初始化设置
    -   [4.1 退出sql界面](https://www.cnblogs.com/nickchen121/p/11145123.html#41-退出sql界面)
-   五、配置
    -   [5.1 检测修改结果](https://www.cnblogs.com/nickchen121/p/11145123.html#51-检测修改结果)


MySQL完整教程目录：https://www.cnblogs.com/nickchen121/p/14709373.html



##### 一、安装

第一步：打开网址，[https://www.mysql.com](https://www.mysql.com/) ，点击downloads之后跳转到https://www.mysql.com/downloads 选择Community选项

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213046.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-01.png?x-oss-process=style/watermark)

第二步： 第一步结束后程序会跳转到https://dev.mysql.com/downloads/ 网址，点击MySQL Community Server进入下面的页面，再点击5.6版本的数据库

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213047.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-02.png?x-oss-process=style/watermark)

第三步：mac操作系统 点击5.6版本之后会跳转到https://dev.mysql.com/downloads/mysql/5.6.html#downloads 网址，页面如下，确认好要下载的版本和操作系统，点击Download

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213048.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-03.png?x-oss-process=style/watermark)

第四步：可以不用登陆或者注册，直接点击`No thanks,just start my download`就可以下载了。

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213049.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-04.png?x-oss-process=style/watermark)

第五步：双击下载好的dmg文件，会弹出pkg弹框，再双击pkg图标，进入安装界面

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213050.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-05.png?x-oss-process=style/watermark)

第六步：在安装界面上一路继续，最后就安装成功了。

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213051.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-06.png?x-oss-process=style/watermark)

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213052.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-07.png?x-oss-process=style/watermark)

##### 二、环境变量

第一步 ：在终端切换到根目录，编辑./.bash_profile文件



```shell
$ cd ~
$ vim ./.bash_profile
```

第二步 ：进入vim 编辑环境。 按下i 进入 insert 模式 ，输入



```shell
export PATH=$PATH:/usr/local/mysql/bin
export PATH=$PATH:/usr/local/mysql/support-files
```

第三步 ：按下esc 退出 insert 模式，输入:wq保存配置文件。



```shell
:wq
```

第四步 ：在终端界面下输入以下命令，让配置文件的修改生效，并查看环境变量是否设置成功



```shell
$ source ~/.bash_profile 
$ echo $PATH
```

###### 2.1 MySQL服务的启停和状态的查看



```shell
停止MySQL服务
sudo mysql.server stop

重启MySQL服务
sudo mysql.server restart

查看MySQL服务状态
sudo mysql.server status
```

##### 三、启动

第一步 ：终端界面下输入



```shell
sudo mysql.server start
```

第二步 ：启动mysql服务,启动成功后继续输入



```shell
mysql -u root -p
```

第三步 ：直接回车进入数据库，看到下列欢迎页面

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213053.jpeg)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-08.png?x-oss-process=style/watermark)

##### 四、初始化设置

设置初始化密码，进入数据库mysql数据库之后执行下面的语句，设置当前root用户的密码为root。



```sql
set password = password('root');
```

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213054.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-09.png?x-oss-process=style/watermark)

###### 4.1 退出sql界面



```shell
exit
```

##### 五、配置

进入到 /usr/local/mysql/support-files 目录。里面有个文件:my-default.cnf

将其复制到桌面上，改名为my.cnf，将内容替换为。



```default
[mysqld]
default-storage-engine=INNODB
character-set-server=utf8
port = 3306

[client]
default-character-set=utf8
```

将修改后的文件my.cnf复制到 /etc 目录下。

重启mysql

###### 5.1 检测修改结果

​    

```sql
$mysql>>>show variables like '%char%';
```

至此数据库就可以愉快的使用啦！

### Java使用JDBC操作MySQL数据库

##### 1. 下载Java语言操作MySQL的驱动jar包

   选择版本 `mysql-connector-java-5.1.48.jar`

   https://mvnrepository.com/artifact/mysql/mysql-connector-java

##### 2. 准备数据表

```SQL
CREATE TABLE `book` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(50) NOT NULL DEFAULT '' COMMENT '图书名称',
  `quantity` int(11) NOT NULL DEFAULT '0' COMMENT '库存数量',
  `price` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '单价',
  `isbn` varchar(20) DEFAULT NULL COMMENT '国际编号',
  PRIMARY KEY (`id`),
  UNIQUE KEY `isbn` (`isbn`),
  KEY `name` (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

##### 3. 将下载的MySQL驱动jar包移动到lib目录，编写`BookDao.java`类，目录结构如下

```
- BookDao.java
- lib/
 - mysql-connector-java-5.1.48.jar
```

##### 4. 插入数据

```java
import java.sql.*;

public class BookDao {
    public static void main(String arg[]) {

        // 操作数据库需要用到 java.sql 包中的三个类
        Connection conn = null;         // 连接对象
        PreparedStatement stmt = null;  // 预处理对象
        ResultSet rs = null;            // 结果集对象

        try {
            // 加载驱动类 (mysql-connector-java-5.x)
            Class.forName("com.mysql.jdbc.Driver");

            // 如果mysql-connector-java-8.x 则使用下面的驱动类，最低要求Java8+
            // Class.forName("com.mysql.cj.jdbc.Driver");

            // 连接到本机(127.0.0.1)的test数据库，使用Unicode字符集UTF-8编码，不使用SSL，时区为东8区
            String url = "jdbc:mysql://127.0.0.1:3306/test?useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai";
            conn = DriverManager.getConnection(url, "root", "your password");

            // 准备SQL语句
            String sql = "INSERT INTO book (name, quantity) VALUES (?, ?)";
            stmt = conn.prepareStatement(sql);

            // 绑定占位符的值
            stmt.setString(1, "book1");   // 新版本驱动直接支持MySQL中的utf8mb4字符集
            stmt.setInt(2, 100);

            // 执行SQL
            stmt.execute();

            // 获取MySQL自增id
            rs = stmt.executeQuery("SELECT LAST_INSERT_ID()");
            int id;
            if (rs.next()) {
                id = rs.getInt(1);
                System.out.println("ID:" + id);
            }

            // 释放资源，关闭连接
            if (rs != null) {
                rs.close();
            }
            if (stmt != null) {
                stmt.close();
            }
            if (conn != null) {
                conn.close();
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

##### 5. 编译运行

```shell
# Linux系统编译运行
$ javac BookDao.java
$ java -cp lib/mysql-connector-java-5.1.48.jar:. BookDao

# Windows系统编译运行
$ javac -encoding UTF-8 BookDao.java
$ java -cp lib/mysql-connector-java-5.1.48.jar;. BookDao
```

##### 6. 查询数据

```java
// 准备SQL语句
String sql = "SELECT * FROM book WHERE quantity > ? and name = ?";
stmt = conn.prepareStatement(sql);

// 绑定占位符的值
stmt.setInt(1, 10);
stmt.setString(2, "book1");

// 执行查询类型的SQL
rs = stmt.executeQuery();

System.out.println("id\tname\tquantity");

// 循环输出结果集，next是移动到下一条记录，如果后面没有记录则返回false
while (rs.next()) {
  int id = rs.getInt("id");
  String name = rs.getString("name");
  String email = rs.getString("quantity");
  System.out.println(id + "\t" + name + "\t" + email);
}

// 释放资源，关闭连接
```

##### 7. 更新数据

```java
// 准备SQL语句
String sql = "UPDATE book SET name = ? WHERE id = ?";
stmt = conn.prepareStatement(sql);

// 绑定占位符的值
stmt.setString(1, "new book");
stmt.setInt(2, 1);

// 执行SQL，返回受影响行数
int rows = stmt.executeUpdate();
System.out.println("更新了" + rows + "条记录");

// 释放资源，关闭连接
```

##### 8. 删除数据

```java
// 准备SQL语句
String sql = "DELETE FROM book WHERE id = ?";
stmt = conn.prepareStatement(sql);

// 绑定占位符的值
stmt.setInt(1, 3);

// 执行SQL，返回受影响行数
int rows = stmt.executeUpdate();
System.out.println("删除了" + rows + "条记录");

// 释放资源，关闭连接
```

##### 9. 思考 `execute` 、`executeQuery` 和 `executeUpdate` 的区别

executeQuery ：用于返回单个结果集，用来直接查询语句

>   用于产生单个结果集（ResultSet）的语句，例如 SELECT 语句。 被使用最多的执行 SQL 语句的方法。这个方法被用来执行 SELECT 语句，它几乎是使用最多的 SQL 语句。但也只能执行查询语句，执行后返回代表查询结果的ResultSet对象。

executeUpdate：用于执行 INSERT、UPDATE 、 DELETE 语句或 SQL DDL语，返回受影响的行数

>   用于执行 INSERT、UPDATE 或 DELETE 语句以及 SQL DDL（数据定义语言）语句，例如 CREATE TABLE 和 DROP TABLE。INSERT、UPDATE 或 DELETE 语句的效果是修改表中零行或多行中的一列或多列。executeUpdate 的返回值是一个整数（int），指示受影响的行数（即更新计数）。对于 CREATE TABLE 或 DROP TABLE 等不操作行的语句，executeUpdate 的返回值总为零。

execute：是executeQuery 和 executeUpdate ，用于返回多个结果集，即动态执行未知 SQL 字符串

>   可用于执行任何SQL语句，返回一个boolean值，表明执行该SQL语句是否返回了ResultSet。如果执行后第一个结果是ResultSet，则返回true，否则返回false。但它执行SQL语句时比较麻烦，通常我们没有必要使用execute方法来执行SQL语句，而是使用executeQuery或executeUpdate更适合，但如果在不清楚SQL语句的类型时则只能使用execute方法来执行该SQL语句了。

#### java操作数据库详情

```java
// 准备SQL语句
String sql = 
    "SELECT * FROM book WHERE name LIKE ? ORDER BY id DESC LIMIT ?";
stmt = conn.prepareStatement(sql);

// 绑定占位符的值
//%1%两个百分号表示模糊搜索
stmt.setString(1,"书");   // 新版本驱动直接支持MySQL中的utf8mb4字符集
stmt.setInt(2, 5);
```

```java
package com.example;

import com.example.entity.Book;
import com.example.dao.BookDao;

import java.util.List;

public class App {
    //1、建包、域名+项目名
    //架包如果找不到就把lib里的文件夹添加为库
    //dao 为数据访问对象
    //book 为数据结构
    public static void main(String[] args) {

        Book book =new Book("图书名11",1213,"22.22","1223");
        BookDao bookDao=new BookDao();
        bookDao.create(book);
//        BookDao bookDao=new BookDao();
//        List<Book>books =bookDao.findBooks("图书",3);
//       for (Book obj:books){
//           System.out.println(obj.getId()+"\t"+obj.getName()+"\t"+obj.getPrice()+"\t"+obj.getPrice()+"\t"+obj.getIsbn());
//       }


    }
}

```

```java
package com.example.dao;

import com.example.entity.Book;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;


//数据访问包
public class BookDao {
    //Connection：返回一个链接
    private Connection getConnection(){
        Connection conn=null;
        try {
            // 加载驱动类 (mysql-connector-java-5.x)
            Class.forName("com.mysql.jdbc.Driver");

            // 如果mysql-connector-java-8.x 则使用下面的驱动类，最低要求Java8+
            // Class.forName("com.mysql.cj.jdbc.Driver");

            // 连接到本机(127.0.0.1)的test数据库，使用Unicode字符集UTF-8编码，不使用SSL，时区为东8区
            String url = "jdbc:mysql://127.0.0.1:3306/book?useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai";
            conn = DriverManager.getConnection(url, "root", "");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return conn;
    }
    //创建book类，并且上传到MySql
    public void create(Book book) {

        // 操作数据库需要用到 java.sql 包中的三个类
        Connection conn = getConnection();         // 连接对象
        PreparedStatement stmt = null;  // 预处理对象
        ResultSet rs = null;            // 结果集对象

        try {
            // 准备SQL语句
            String sql = "INSERT INTO book (name, quantity) VALUES (?, ?)";
            stmt = conn.prepareStatement(sql);

            // 绑定占位符的值
            stmt.setString(1, book.getName());   // 新版本驱动直接支持MySQL中的utf8mb4字符集
            stmt.setInt(2, book.getQuantity());

            // 执行SQL
            stmt.execute();

            // 获取MySQL自增id
            rs = stmt.executeQuery("SELECT LAST_INSERT_ID()");
            int id;
            if (rs.next()) {
                id = rs.getInt(1);
                System.out.println("ID:" + id);
            }

            // 释放资源，关闭连接
            rs.close();
            stmt.close();
            conn.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //查找返回list类型数据
    public <list> List<Book> findBooks(String name, int size) {

        // 操作数据库需要用到 java.sql 包中的三个类
        Connection conn = getConnection();         // 连接对象
        PreparedStatement stmt = null;  // 预处理对象
        ResultSet rs = null;            // 结果集对象
        List<Book> bookList=new ArrayList<>();
        try {
            // 准备SQL语句
            String sql = "SELECT * FROM book WHERE name LIKE ? ORDER BY id DESC LIMIT ?";
            stmt = conn.prepareStatement(sql);

            // 绑定占位符的值
            //%1%两个百分号表示模糊搜索
            stmt.setString(1, "%"+name+"%");   // 新版本驱动直接支持MySQL中的utf8mb4字符集
            stmt.setInt(2, size);

            // 执行SQL
            stmt.execute();

            // 执行查询类型的SQL
            rs = stmt.executeQuery();

            System.out.println("id\tname\tquantity");

            // 循环输出结果集，next是移动到下一条记录，如果后面没有记录则返回false
            while (rs.next()) {
                Book book =new Book(rs.getInt("id"),rs.getString("name"),rs.getInt("quantity"),rs.getString("price"),rs.getString("isbn"));
//                book.setId(rs.getInt("id"));
//                book.setName(rs.getString("name"));
//                book.setQuantity(rs.getInt("quantity"));
//                book.setPrice(r s.getString("price"));
//                book.setIsbn(rs.getString("isbn"));
                bookList.add(book);
            }


            // 释放资源，关闭连接
            rs.close();
            stmt.close();
            conn.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
        return bookList;
    }
}
```

```java
package com.example.entity;

//建一个类储存可以被new出来的数据
public class Book {
    //创建与表相同的数据
    private  int id;
    private String name;
    private int quantity;
    private String price;
    private String isbn;

    public Book() {
    }

    public Book(String name, int quantity) {
        this.name = name;
        this.quantity = quantity;
    }

    public Book(int id, String name, int quantity, String price, String isbn) {
        this.id = id;
        this.name = name;
        this.quantity = quantity;
        this.price = price;
        this.isbn = isbn;
    }

    public Book(String name, int quantity, String price, String isbn) {
        this.name = name;
        this.quantity = quantity;
        this.price = price;
        this.isbn = isbn;
    }

    @Override
    public String toString() {
        return "Book{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", quantity=" + quantity +
                ", price='" + price + '\'' +
                ", isbn='" + isbn + '\'' +
                '}';
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public String getPrice() {
        return price;
    }

    public void setPrice(String price) {
        this.price = price;
    }

    public String getIsbn() {
        return isbn;
    }

    public void setIsbn(String isbn) {
        this.isbn = isbn;
    }
}

```



## 六、 Java中的接口

接口就是用来规范代码的

创建一个接口

```java
public interface UserBiz {
	User register(String username,String password);
	User login(String username,String password);
}
```

实现接口

```java
public class UserService implements UserBiz {
    @Override
	User register(String username,String password) {
        // jdbc 连接mysql
        // insert into ...
        User user = new User();
        user.username = username;
        user.password = password;
        
        return user;
    }
}
```

接口和抽象类的区别

```
相同点
（1）都不能被实例化 （2）接口的实现类或抽象类的子类都只有实现了接口或抽象类中的方法后才能实例化。
（1）接口只有定义，不能有方法的实现，java 1.8中可以定义default方法体，而抽象类可以有定义与实现，方法可在抽象类中实现。

（2）实现接口的关键字为implements，继承抽象类的关键字为extends。一个类可以实现多个接口，但一个类只能继承一个抽象类。所以，使用接口可以间接地实现多重继承。

（3）接口强调特定功能的实现，而抽象类强调所属关系。

（4）接口成员变量默认为public static final，必须赋初值，不能被修改；其所有的成员方法都是public、abstract的。抽象类中成员变量默认default，可在子类中被重新定义，也可被重新赋值；抽象方法被abstract修饰，不能被private、static、synchronized和native等修饰，必须以分号结尾，不带花括号。

```



#### 目录结构的含义

##### dao

数据访问对象，用来访问数据库，不进行业务逻辑

##### entity

实体类，就是属性类，就是一个数据库表生成一个类

##### serivce

服务类，处理业务逻辑

## 七、枚举类

```java
package com.example.demo.controller;

enum ApiEnum { // 此处的枚举值必须调用对应的构造器来创建
    CART("/api/goods/favorite/list")
    , FEMALE("女");
    public final String name ;// 枚举值的构造器只能使用 private 修饰

    private ApiEnum(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }


}

 System.out.println(ApiEnum.CART.getName());
```



## Java类

### String

|                                                              | ***\*方法摘要\****                                           |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| char                                                         | **[charAt](#charAt(int))**(int index)      返回指定索引处的 char 值。 |
| int                                                          | **[codePointAt](#codePointAt(int))**(int index)      返回指定索引处的字符（Unicode 代码点）。 |
| int                                                          | **[codePointBefore](#codePointBefore(int))**(int index)      返回指定索引之前的字符（Unicode 代码点）。 |
| int                                                          | **[codePointCount](#codePointCount(int, int))**(int beginIndex, int endIndex)      返回此 String 的指定文本范围中的 Unicode 代码点数。 |
| int                                                          | **[compareTo](#compareTo(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) anotherString)      按字典顺序比较两个字符串。 |
| int                                                          | **[compareToIgnoreCase](#compareToIgnoreCase(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      按字典顺序比较两个字符串，不考虑大小写。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[concat](#concat(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      将指定字符串连接到此字符串的结尾。 |
| boolean                                                      | **[contains](#contains(java.lang.CharSequence))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s)      当且仅当此字符串包含指定的 char 值序列时，返回 true。 |
| boolean                                                      | **[contentEquals](#contentEquals(java.lang.CharSequence))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) cs)      将此字符串与指定的 CharSequence 比较。 |
| boolean                                                      | **[contentEquals](#contentEquals(java.lang.StringBuffer))**([StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) sb)      将此字符串与指定的 StringBuffer 比较。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[copyValueOf](#copyValueOf(char[]))**(char[] data)      返回指定数组中表示该字符序列的 String。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[copyValueOf](#copyValueOf(char[], int, int))**(char[] data, int offset, int count)      返回指定数组中表示该字符序列的 String。 |
| boolean                                                      | **[endsWith](#endsWith(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) suffix)      测试此字符串是否以指定的后缀结束。 |
| boolean                                                      | **[equals](#equals(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) anObject)      将此字符串与指定的对象比较。 |
| boolean                                                      | **[equalsIgnoreCase](#equalsIgnoreCase(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) anotherString)      将此 String 与另一个 String 比较，不考虑大小写。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[format](#format(java.util.Locale, java.lang.String, java.lang.Object...))**([Locale](http://www.daimaku.net/book/javasdk/java/util/Locale.html) l, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) format, [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html)... args)      使用指定的语言环境、格式字符串和参数返回一个格式化字符串。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[format](#format(java.lang.String, java.lang.Object...))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) format, [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html)... args)      使用指定的格式字符串和参数返回一个格式化字符串。 |
| byte[]                                                       | **[getBytes](#getBytes())**()      使用平台的默认字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。 |
| byte[]                                                       | **[getBytes](#getBytes(java.nio.charset.Charset))**([Charset](http://www.daimaku.net/book/javasdk/java/nio/charset/Charset.html) charset)      使用给定的 [charset](http://www.daimaku.net/book/javasdk/java/nio/charset/Charset.html) 将此 String 编码到 byte 序列，并将结果存储到新的 byte 数组。 |
| void                                                         | **[getBytes](#getBytes(int, int, byte[], int))**(int srcBegin, int srcEnd, byte[] dst, int dstBegin)      ***\*已过时。\**** **该方法无法将字符正确转换为字节。从 JDK 1.1 起，完成该转换的首选方法是通过** *[getBytes()](#getBytes())* 方法，该方法使用平台的默认字符集。 |
| byte[]                                                       | **[getBytes](#getBytes(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) charsetName)      使用指定的字符集将此 String 编码为 byte 序列，并将结果存储到一个新的 byte 数组中。 |
| void                                                         | **[getChars](#getChars(int, int, char[], int))**(int srcBegin, int srcEnd, char[] dst, int dstBegin)      将字符从此字符串复制到目标字符数组。 |
| int                                                          | **[hashCode](#hashCode())**()      返回此字符串的哈希码。    |
| int                                                          | **[indexOf](#indexOf(int))**(int ch)      返回指定字符在此字符串中第一次出现处的索引。 |
| int                                                          | **[indexOf](#indexOf(int, int))**(int ch, int fromIndex)      返回在此字符串中第一次出现指定字符处的索引，从指定的索引开始搜索。 |
| int                                                          | **[indexOf](#indexOf(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      返回指定子字符串在此字符串中第一次出现处的索引。 |
| int                                                          | **[indexOf](#indexOf(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str, int fromIndex)      返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[intern](#intern())**()      返回字符串对象的规范化表示形式。 |
| boolean                                                      | **[isEmpty](#isEmpty())**()      当且仅当 [length()](#length()) 为 0 时返回 true。 |
| int                                                          | **[lastIndexOf](#lastIndexOf(int))**(int ch)      返回指定字符在此字符串中最后一次出现处的索引。 |
| int                                                          | **[lastIndexOf](#lastIndexOf(int, int))**(int ch, int fromIndex)      返回指定字符在此字符串中最后一次出现处的索引，从指定的索引处开始进行反向搜索。 |
| int                                                          | **[lastIndexOf](#lastIndexOf(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      返回指定子字符串在此字符串中最右边出现处的索引。 |
| int                                                          | **[lastIndexOf](#lastIndexOf(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str, int fromIndex)      返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索。 |
| int                                                          | **[length](#length())**()      返回此字符串的长度。          |
| boolean                                                      | **[matches](#matches(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) regex)      告知此字符串是否匹配给定的[正则表达式](#sum)。 |
| int                                                          | **[offsetByCodePoints](#offsetByCodePoints(int, int))**(int index, int codePointOffset)      返回此 String 中从给定的 index 处偏移 codePointOffset 个代码点的索引。 |
| boolean                                                      | **[regionMatches](#regionMatches(boolean, int, java.lang.String, int, int))**(boolean ignoreCase, int toffset, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) other, int ooffset, int len)      测试两个字符串区域是否相等。 |
| boolean                                                      | **[regionMatches](#regionMatches(int, java.lang.String, int, int))**(int toffset, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) other, int ooffset, int len)      测试两个字符串区域是否相等。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[replace](#replace(char, char))**(char oldChar, char newChar)      返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[replace](#replace(java.lang.CharSequence, java.lang.CharSequence))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) target, [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) replacement)      使用指定的字面值替换序列替换此字符串所有匹配字面值目标序列的子字符串。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[replaceAll](#replaceAll(java.lang.String, java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) regex, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) replacement)      使用给定的 replacement 替换此字符串所有匹配给定的[正则表达式](#sum)的子字符串。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[replaceFirst](#replaceFirst(java.lang.String, java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) regex, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) replacement)      使用给定的 replacement 替换此字符串匹配给定的[正则表达式](#sum)的第一个子字符串。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html)[] | **[split](#split(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) regex)      根据给定[正则表达式](#sum)的匹配拆分此字符串。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html)[] | **[split](#split(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) regex, int limit)      根据匹配给定的[正则表达式](#sum)来拆分此字符串。 |
| boolean                                                      | **[startsWith](#startsWith(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) prefix)      测试此字符串是否以指定的前缀开始。 |
| boolean                                                      | **[startsWith](#startsWith(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) prefix, int toffset)      测试此字符串从指定索引开始的子字符串是否以指定前缀开始。 |
| [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) | **[subSequence](#subSequence(int, int))**(int beginIndex, int endIndex)      返回一个新的字符序列，它是此序列的一个子序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[substring](#substring(int))**(int beginIndex)      返回一个新的字符串，它是此字符串的一个子字符串。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[substring](#substring(int, int))**(int beginIndex, int endIndex)      返回一个新字符串，它是此字符串的一个子字符串。 |
| char[]                                                       | **[toCharArray](#toCharArray())**()      将此字符串转换为一个新的字符数组。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toLowerCase](#toLowerCase())**()      使用默认语言环境的规则将此 String 中的所有字符都转换为小写。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toLowerCase](#toLowerCase(java.util.Locale))**([Locale](http://www.daimaku.net/book/javasdk/java/util/Locale.html) locale)      使用给定 Locale 的规则将此 String 中的所有字符都转换为小写。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toString](#toString())**()      返回此对象本身（它已经是一个字符串！）。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toUpperCase](#toUpperCase())**()      使用默认语言环境的规则将此 String 中的所有字符都转换为大写。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toUpperCase](#toUpperCase(java.util.Locale))**([Locale](http://www.daimaku.net/book/javasdk/java/util/Locale.html) locale)      使用给定 Locale 的规则将此 String 中的所有字符都转换为大写。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[trim](#trim())**()      返回字符串的副本，忽略前导空白和尾部空白。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(boolean))**(boolean b)      返回 boolean 参数的字符串表示形式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(char))**(char c)      返回 char 参数的字符串表示形式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(char[]))**(char[] data)      返回 char 数组参数的字符串表示形式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(char[], int, int))**(char[] data, int offset, int count)      返回 char 数组参数的特定子数组的字符串表示形式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(double))**(double d)      返回 double 参数的字符串表示形式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(float))**(float f)      返回 float 参数的字符串表示形式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(int))**(int i)      返回 int 参数的字符串表示形式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(long))**(long l)      返回 long 参数的字符串表示形式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[valueOf](#valueOf(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      返回 Object 参数的字符串表示形式。 |

###  math

|               | ***\*方法摘要\****                                           |
| ------------- | ------------------------------------------------------------ |
| static double | **[abs](#abs(double))**(double a)      返回 double 值的绝对值。 |
| static float  | **[abs](#abs(float))**(float a)      返回 float 值的绝对值。 |
| static int    | **[abs](#abs(int))**(int a)      返回 int 值的绝对值。       |
| static long   | **[abs](#abs(long))**(long a)      返回 long 值的绝对值。    |
| static double | **[acos](#acos(double))**(double a)      返回一个值的反余弦；返回的角度范围在 0.0 到 **pi** 之间。 |
| static double | **[asin](#asin(double))**(double a)      返回一个值的反正弦；返回的角度范围在 -**pi**/2 到 **pi**/2 之间。 |
| static double | **[atan](#atan(double))**(double a)      返回一个值的反正切；返回的角度范围在 -**pi**/2 到 **pi**/2 之间。 |
| static double | **[atan2](#atan2(double, double))**(double y, double x)      将矩形坐标 (x, y) 转换成极坐标 (r, **theta**)，返回所得角 **theta**。 |
| static double | **[cbrt](#cbrt(double))**(double a)      返回 double 值的立方根。 |
| static double | **[ceil](#ceil(double))**(double a)      返回最小的（最接近负无穷大）double 值，该值大于等于参数，并等于某个整数。 |
| static double | **[copySign](#copySign(double, double))**(double magnitude, double sign)      返回带有第二个浮点参数符号的第一个浮点参数。 |
| static float  | **[copySign](#copySign(float, float))**(float magnitude, float sign)      返回带有第二个浮点参数符号的第一个浮点参数。 |
| static double | **[cos](#cos(double))**(double a)      返回角的三角余弦。    |
| static double | **[cosh](#cosh(double))**(double x)      返回 double 值的双曲线余弦。 |
| static double | **[exp](#exp(double))**(double a)      返回欧拉数 **e** 的 double 次幂的值。 |
| static double | **[expm1](#expm1(double))**(double x)      返回 **e**x -1。  |
| static double | **[floor](#floor(double))**(double a)      返回最大的（最接近正无穷大）double 值，该值小于等于参数，并等于某个整数。 |
| static int    | **[getExponent](#getExponent(double))**(double d)      返回 double 表示形式中使用的无偏指数。 |
| static int    | **[getExponent](#getExponent(float))**(float f)      返回 float 表示形式中使用的无偏指数。 |
| static double | **[hypot](#hypot(double, double))**(double x, double y)      返回 sqrt(**x**2 +**y**2)，没有中间溢出或下溢。 |
| static double | **[IEEEremainder](#IEEEremainder(double, double))**(double f1, double f2)      按照 IEEE 754 标准的规定，对两个参数进行余数运算。 |
| static double | **[log](#log(double))**(double a)      返回 double 值的自然对数（底数是 **e**）。 |
| static double | **[log10](#log10(double))**(double a)      返回 double 值的底数为 10 的对数。 |
| static double | **[log1p](#log1p(double))**(double x)      返回参数与 1 之和的自然对数。 |
| static double | **[max](#max(double, double))**(double a, double b)      返回两个 double 值中较大的一个。 |
| static float  | **[max](#max(float, float))**(float a, float b)      返回两个 float 值中较大的一个。 |
| static int    | **[max](#max(int, int))**(int a, int b)      返回两个 int 值中较大的一个。 |
| static long   | **[max](#max(long, long))**(long a, long b)      返回两个 long 值中较大的一个。 |
| static double | **[min](#min(double, double))**(double a, double b)      返回两个 double 值中较小的一个。 |
| static float  | **[min](#min(float, float))**(float a, float b)      返回两个 float 值中较小的一个。 |
| static int    | **[min](#min(int, int))**(int a, int b)      返回两个 int 值中较小的一个。 |
| static long   | **[min](#min(long, long))**(long a, long b)      返回两个 long 值中较小的一个。 |
| static double | **[nextAfter](#nextAfter(double, double))**(double start, double direction)      返回第一个参数和第二个参数之间与第一个参数相邻的浮点数。 |
| static float  | **[nextAfter](#nextAfter(float, double))**(float start, double direction)      返回第一个参数和第二个参数之间与第一个参数相邻的浮点数。 |
| static double | **[nextUp](#nextUp(double))**(double d)      返回 d 和正无穷大之间与 d 相邻的浮点值。 |
| static float  | **[nextUp](#nextUp(float))**(float f)      返回 f 和正无穷大之间与 f 相邻的浮点值。 |
| static double | **[pow](#pow(double, double))**(double a, double b)      返回第一个参数的第二个参数次幂的值。 |
| static double | **[random](#random())**()      返回带正号的 double 值，该值大于等于 0.0 且小于 1.0。 |
| static double | **[rint](#rint(double))**(double a)      返回最接近参数并等于某一整数的 double 值。 |
| static long   | **[round](#round(double))**(double a)      返回最接近参数的 long。 |
| static int    | **[round](#round(float))**(float a)      返回最接近参数的 int。 |
| static double | **[scalb](#scalb(double, int))**(double d, int scaleFactor)      返回 d × 2scaleFactor，其舍入方式如同将一个正确舍入的浮点值乘以 double 值集合中的一个值。 |
| static float  | **[scalb](#scalb(float, int))**(float f, int scaleFactor)      返回 f × 2scaleFactor，其舍入方式如同将一个正确舍入的浮点值乘以 float 值集合中的一个值。 |
| static double | **[signum](#signum(double))**(double d)      返回参数的符号函数；如果参数为 0，则返回 0；如果参数大于 0，则返回 1.0；如果参数小于 0，则返回 -1.0。 |
| static float  | **[signum](#signum(float))**(float f)      返回参数的符号函数；如果参数为 0，则返回 0；如果参数大于 0，则返回 1.0；如果参数小于 0，则返回 -1.0。 |
| static double | **[sin](#sin(double))**(double a)      返回角的三角正弦。    |
| static double | **[sinh](#sinh(double))**(double x)      返回 double 值的双曲线正弦。 |
| static double | **[sqrt](#sqrt(double))**(double a)      返回正确舍入的 double 值的正平方根。 |
| static double | **[tan](#tan(double))**(double a)      返回角的三角正切。    |
| static double | **[tanh](#tanh(double))**(double x)      返回 double 值的双曲线余弦。 |
| static double | **[toDegrees](#toDegrees(double))**(double angrad)      将用弧度表示的角转换为近似相等的用角度表示的角。 |
| static double | **[toRadians](#toRadians(double))**(double angdeg)      将用角度表示的角转换为近似相等的用弧度表示的角。 |
| static double | **[ulp](#ulp(double))**(double d)      返回参数的 ulp 大小。 |
| static float  | **[ulp](#ulp(float))**(float f)      返回参数的 ulp 大小。   |

### Date

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| boolean                                                      | **[after](#after(java.util.Date))**([Date](http://www.daimaku.net/book/javasdk/java/util/Date.html) when)      测试此日期是否在指定日期之后。 |
| boolean                                                      | **[before](#before(java.util.Date))**([Date](http://www.daimaku.net/book/javasdk/java/util/Date.html) when)      测试此日期是否在指定日期之前。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[clone](#clone())**()      返回此对象的副本。              |
| int                                                          | **[compareTo](#compareTo(java.util.Date))**([Date](http://www.daimaku.net/book/javasdk/java/util/Date.html) anotherDate)      比较两个日期的顺序。 |
| boolean                                                      | **[equals](#equals(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      比较两个日期的相等性。 |
| int                                                          | **[getDate](#getDate())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.DAY_OF_MONTH)** **取代。** |
| int                                                          | **[getDay](#getDay())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.DAY_OF_WEEK)** **取代。** |
| int                                                          | **[getHours](#getHours())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.HOUR_OF_DAY)** **取代。** |
| int                                                          | **[getMinutes](#getMinutes())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.MINUTE)** **取代。** |
| int                                                          | **[getMonth](#getMonth())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.MONTH)** **取代。** |
| int                                                          | **[getSeconds](#getSeconds())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.SECOND)** **取代。** |
| long                                                         | **[getTime](#getTime())**()      返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。 |
| int                                                          | **[getTimezoneOffset](#getTimezoneOffset())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **-(Calendar.get(Calendar.ZONE_OFFSET) + Calendar.get(Calendar.DST_OFFSET)) / (60 \* 1000)** **取代。** |
| int                                                          | **[getYear](#getYear())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.YEAR) - 1900** **取代。** |
| int                                                          | **[hashCode](#hashCode())**()      返回此对象的哈希码值。    |
| static long                                                  | **[parse](#parse(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) s)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **DateFormat.parse(String s)** **取代。** |
| void                                                         | **[setDate](#setDate(int))**(int date)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.DAY_OF_MONTH, int date)** **取代。** |
| void                                                         | **[setHours](#setHours(int))**(int hours)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.HOUR_OF_DAY, int hours)** **取代。** |
| void                                                         | **[setMinutes](#setMinutes(int))**(int minutes)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.MINUTE, int minutes)** **取代。** |
| void                                                         | **[setMonth](#setMonth(int))**(int month)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.MONTH, int month)** **取代。** |
| void                                                         | **[setSeconds](#setSeconds(int))**(int seconds)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.SECOND, int seconds)** **取代。** |
| void                                                         | **[setTime](#setTime(long))**(long time)      设置此 Date 对象，以表示 1970 年 1 月 1 日 00:00:00 GMT 以后 time 毫秒的时间点。 |
| void                                                         | **[setYear](#setYear(int))**(int year)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.YEAR, year + 1900)** **取代。** |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toGMTString](#toGMTString())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **DateFormat.format(Date date)** **取代，使用 GMT** **TimeZone****。** |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toLocaleString](#toLocaleString())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **DateFormat.format(Date date)** **取代。** |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toString](#toString())**()      把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)。 |
| static long                                                  | **[UTC](#UTC(int, int, int, int, int, int))**(int year, int month, int date, int hrs, int min, int sec)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(year + 1900, month, date, hrs, min, sec)** **或** **GregorianCalendar(year + 1900, month, date, hrs, min, sec)** **取代，使用 UTC** **TimeZone****，后跟** **Calendar.getTime().getTime()****。** |
| ***\*方法摘要\****                                           |                                                              |
| boolean                                                      | **[after](#after(java.util.Date))**([Date](http://www.daimaku.net/book/javasdk/java/util/Date.html) when)      测试此日期是否在指定日期之后。 |
| boolean                                                      | **[before](#before(java.util.Date))**([Date](http://www.daimaku.net/book/javasdk/java/util/Date.html) when)      测试此日期是否在指定日期之前。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[clone](#clone())**()      返回此对象的副本。              |
| int                                                          | **[compareTo](#compareTo(java.util.Date))**([Date](http://www.daimaku.net/book/javasdk/java/util/Date.html) anotherDate)      比较两个日期的顺序。 |
| boolean                                                      | **[equals](#equals(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      比较两个日期的相等性。 |
| int                                                          | **[getDate](#getDate())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.DAY_OF_MONTH)** **取代。** |
| int                                                          | **[getDay](#getDay())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.DAY_OF_WEEK)** **取代。** |
| int                                                          | **[getHours](#getHours())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.HOUR_OF_DAY)** **取代。** |
| int                                                          | **[getMinutes](#getMinutes())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.MINUTE)** **取代。** |
| int                                                          | **[getMonth](#getMonth())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.MONTH)** **取代。** |
| int                                                          | **[getSeconds](#getSeconds())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.SECOND)** **取代。** |
| long                                                         | **[getTime](#getTime())**()      返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。 |
| int                                                          | **[getTimezoneOffset](#getTimezoneOffset())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **-(Calendar.get(Calendar.ZONE_OFFSET) + Calendar.get(Calendar.DST_OFFSET)) / (60 \* 1000)** **取代。** |
| int                                                          | **[getYear](#getYear())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.get(Calendar.YEAR) - 1900** **取代。** |
| int                                                          | **[hashCode](#hashCode())**()      返回此对象的哈希码值。    |
| static long                                                  | **[parse](#parse(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) s)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **DateFormat.parse(String s)** **取代。** |
| void                                                         | **[setDate](#setDate(int))**(int date)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.DAY_OF_MONTH, int date)** **取代。** |
| void                                                         | **[setHours](#setHours(int))**(int hours)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.HOUR_OF_DAY, int hours)** **取代。** |
| void                                                         | **[setMinutes](#setMinutes(int))**(int minutes)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.MINUTE, int minutes)** **取代。** |
| void                                                         | **[setMonth](#setMonth(int))**(int month)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.MONTH, int month)** **取代。** |
| void                                                         | **[setSeconds](#setSeconds(int))**(int seconds)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.SECOND, int seconds)** **取代。** |
| void                                                         | **[setTime](#setTime(long))**(long time)      设置此 Date 对象，以表示 1970 年 1 月 1 日 00:00:00 GMT 以后 time 毫秒的时间点。 |
| void                                                         | **[setYear](#setYear(int))**(int year)      ***\*已过时。\**** **从 JDK 1.1 开始，由** **Calendar.set(Calendar.YEAR, year + 1900)** **取代。** |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toGMTString](#toGMTString())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **DateFormat.format(Date date)** **取代，使用 GMT** **TimeZone****。** |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toLocaleString](#toLocaleString())**()      ***\*已过时。\**** **从 JDK 1.1 开始，由** **DateFormat.format(Date date)** **取代。** |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toString](#toString())**()      把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)。 |

### Pattern

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| static [Pattern](http://www.daimaku.net/book/javasdk/java/util/regex/Pattern.html) | **[compile](#compile(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) regex)      将给定的正则表达式编译到模式中。 |
| static [Pattern](http://www.daimaku.net/book/javasdk/java/util/regex/Pattern.html) | **[compile](#compile(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) regex, int flags)      将给定的正则表达式编译到具有给定标志的模式中。 |
| int                                                          | **[flags](#flags())**()      返回此模式的匹配标志。          |
| [Matcher](http://www.daimaku.net/book/javasdk/java/util/regex/Matcher.html) | **[matcher](#matcher(java.lang.CharSequence))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) input)      创建匹配给定输入与此模式的匹配器。 |
| static boolean                                               | **[matches](#matches(java.lang.String, java.lang.CharSequence))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) regex, [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) input)      编译给定正则表达式并尝试将给定输入与其匹配。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[pattern](#pattern())**()      返回在其中编译过此模式的正则表达式。 |
| static [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[quote](#quote(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) s)      返回指定 String 的字面值模式 String。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html)[] | **[split](#split(java.lang.CharSequence))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) input)      围绕此模式的匹配拆分给定输入序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html)[] | **[split](#split(java.lang.CharSequence, int))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) input, int limit)      围绕此模式的匹配拆分给定输入序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toString](#toString())**()      返回此模式的字符串表示形式。 |

### StringBuffer

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(boolean))**(boolean b)      将 boolean 参数的字符串表示形式追加到序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(char))**(char c)      将 char 参数的字符串表示形式追加到此序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(char[]))**(char[] str)      将 char 数组参数的字符串表示形式追加到此序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(char[], int, int))**(char[] str, int offset, int len)      将 char 数组参数的子数组的字符串表示形式追加到此序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(java.lang.CharSequence))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s)      将指定的 CharSequence 追加到该序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(java.lang.CharSequence, int, int))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s, int start, int end)      将指定 CharSequence 的子序列追加到此序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(double))**(double d)      将 double 参数的字符串表示形式追加到此序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(float))**(float f)      将 float 参数的字符串表示形式追加到此序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(int))**(int i)      将 int 参数的字符串表示形式追加到此序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(long))**(long lng)      将 long 参数的字符串表示形式追加到此序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      追加 Object 参数的字符串表示形式。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      将指定的字符串追加到此字符序列。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[append](#append(java.lang.StringBuffer))**([StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) sb)      将指定的 StringBuffer 追加到此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[appendCodePoint](#appendCodePoint(int))**(int codePoint)      将 codePoint 参数的字符串表示形式追加到此序列。 |
| int                                                          | **[capacity](#capacity())**()      返回当前容量。            |
| char                                                         | **[charAt](#charAt(int))**(int index)      返回此序列中指定索引处的 char 值。 |
| int                                                          | **[codePointAt](#codePointAt(int))**(int index)      返回指定索引处的字符（统一代码点）。 |
| int                                                          | **[codePointBefore](#codePointBefore(int))**(int index)      返回指定索引前的字符（统一代码点）。 |
| int                                                          | **[codePointCount](#codePointCount(int, int))**(int beginIndex, int endIndex)      返回此序列指定文本范围内的统一代码点。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[delete](#delete(int, int))**(int start, int end)      移除此序列的子字符串中的字符。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[deleteCharAt](#deleteCharAt(int))**(int index)      移除此序列指定位置的 char。 |
| void                                                         | **[ensureCapacity](#ensureCapacity(int))**(int minimumCapacity)      确保容量至少等于指定的最小值。 |
| void                                                         | **[getChars](#getChars(int, int, char[], int))**(int srcBegin, int srcEnd, char[] dst, int dstBegin)      将字符从此序列复制到目标字符数组 dst。 |
| int                                                          | **[indexOf](#indexOf(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      返回第一次出现的指定子字符串在该字符串中的索引。 |
| int                                                          | **[indexOf](#indexOf(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str, int fromIndex)      从指定的索引处开始，返回第一次出现的指定子字符串在该字符串中的索引。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, boolean))**(int offset, boolean b)      将 boolean 参数的字符串表示形式插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, char))**(int offset, char c)      将 char 参数的字符串表示形式插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, char[]))**(int offset, char[] str)      将 char 数组参数的字符串表示形式插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, char[], int, int))**(int index, char[] str, int offset, int len)      将数组参数 str 的子数组的字符串表示形式插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, java.lang.CharSequence))**(int dstOffset, [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s)      将指定 CharSequence 插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, java.lang.CharSequence, int, int))**(int dstOffset, [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s, int start, int end)      将指定 CharSequence 的子序列插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, double))**(int offset, double d)      将 double 参数的字符串表示形式插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, float))**(int offset, float f)      将 float 参数的字符串表示形式插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, int))**(int offset, int i)      将 int 参数的字符串表示形式插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, long))**(int offset, long l)      将 long 参数的字符串表示形式插入此序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, java.lang.Object))**(int offset, [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      将 Object 参数的字符串表示形式插入此字符序列中。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[insert](#insert(int, java.lang.String))**(int offset, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      将字符串插入此字符序列中。 |
| int                                                          | **[lastIndexOf](#lastIndexOf(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      返回最右边出现的指定子字符串在此字符串中的索引。 |
| int                                                          | **[lastIndexOf](#lastIndexOf(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str, int fromIndex)      返回最后一次出现的指定子字符串在此字符串中的索引。 |
| int                                                          | **[length](#length())**()      返回长度（字符数）。          |
| int                                                          | **[offsetByCodePoints](#offsetByCodePoints(int, int))**(int index, int codePointOffset)      返回此序列中的一个索引，该索引是从给定 index 偏移 codePointOffset 个代码点后得到的。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[replace](#replace(int, int, java.lang.String))**(int start, int end, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      使用给定 String 中的字符替换此序列的子字符串中的字符。 |
| [StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) | **[reverse](#reverse())**()      将此字符序列用其反转形式取代。 |
| void                                                         | **[setCharAt](#setCharAt(int, char))**(int index, char ch)      将给定索引处的字符设置为 ch。 |
| void                                                         | **[setLength](#setLength(int))**(int newLength)      设置字符序列的长度。 |
| [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) | **[subSequence](#subSequence(int, int))**(int start, int end)      返回一个新的字符序列，该字符序列是此序列的子序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[substring](#substring(int))**(int start)      返回一个新的 String，它包含此字符序列当前所包含的字符子序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[substring](#substring(int, int))**(int start, int end)      返回一个新的 String，它包含此序列当前所包含的字符子序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toString](#toString())**()      返回此序列中数据的字符串表示形式。 |
| void                                                         | **[trimToSize](#trimToSize())**()      尝试减少用于字符序列的存储空间。 |

### StringBuilder

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(boolean))**(boolean b)      将 boolean 参数的字符串表示形式追加到序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(char))**(char c)      将 char 参数的字符串表示形式追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(char[]))**(char[] str)      将 char 数组参数的字符串表示形式追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(char[], int, int))**(char[] str, int offset, int len)      将 char 数组参数的子数组的字符串表示形式追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(java.lang.CharSequence))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s)      向此 Appendable 追加到指定的字符序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(java.lang.CharSequence, int, int))**([CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s, int start, int end)      将指定 CharSequence 的子序列追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(double))**(double d)      将 double 参数的字符串表示形式追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(float))**(float f)      将 float 参数的字符串表示形式追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(int))**(int i)      将 int 参数的字符串表示形式追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(long))**(long lng)      将 long 参数的字符串表示形式追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      追加 Object 参数的字符串表示形式。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      将指定的字符串追加到此字符序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[append](#append(java.lang.StringBuffer))**([StringBuffer](http://www.daimaku.net/book/javasdk/java/lang/StringBuffer.html) sb)      将指定的 StringBuffer 追加到此序列。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[appendCodePoint](#appendCodePoint(int))**(int codePoint)      将 codePoint 参数的字符串表示形式追加到此序列。 |
| int                                                          | **[capacity](#capacity())**()      返回当前容量。            |
| char                                                         | **[charAt](#charAt(int))**(int index)      返回此序列中指定索引处的 char 值。 |
| int                                                          | **[codePointAt](#codePointAt(int))**(int index)      返回指定索引处的字符（统一代码点）。 |
| int                                                          | **[codePointBefore](#codePointBefore(int))**(int index)      返回指定索引前的字符（统一代码点）。 |
| int                                                          | **[codePointCount](#codePointCount(int, int))**(int beginIndex, int endIndex)      返回此序列指定文本范围内的统一代码点。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[delete](#delete(int, int))**(int start, int end)      移除此序列的子字符串中的字符。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[deleteCharAt](#deleteCharAt(int))**(int index)      移除此序列指定位置上的 char。 |
| void                                                         | **[ensureCapacity](#ensureCapacity(int))**(int minimumCapacity)      确保容量至少等于指定的最小值。 |
| void                                                         | **[getChars](#getChars(int, int, char[], int))**(int srcBegin, int srcEnd, char[] dst, int dstBegin)      将字符从此序列复制到目标字符数组 dst。 |
| int                                                          | **[indexOf](#indexOf(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      返回第一次出现的指定子字符串在该字符串中的索引。 |
| int                                                          | **[indexOf](#indexOf(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str, int fromIndex)      从指定的索引处开始，返回第一次出现的指定子字符串在该字符串中的索引。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, boolean))**(int offset, boolean b)      将 boolean 参数的字符串表示形式插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, char))**(int offset, char c)      将 char 参数的字符串表示形式插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, char[]))**(int offset, char[] str)      将 char 数组参数的字符串表示形式插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, char[], int, int))**(int index, char[] str, int offset, int len)      将数组参数 str 子数组的字符串表示形式插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, java.lang.CharSequence))**(int dstOffset, [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s)      将指定 CharSequence 插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, java.lang.CharSequence, int, int))**(int dstOffset, [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) s, int start, int end)      将指定 CharSequence 的子序列插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, double))**(int offset, double d)      将 double 参数的字符串表示形式插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, float))**(int offset, float f)      将 float 参数的字符串表示形式插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, int))**(int offset, int i)      将 int 参数的字符串表示形式插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, long))**(int offset, long l)      将 long 参数的字符串表示形式插入此序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, java.lang.Object))**(int offset, [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      将 Object 参数的字符串表示形式插入此字符序列中。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[insert](#insert(int, java.lang.String))**(int offset, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      将字符串插入此字符序列中。 |
| int                                                          | **[lastIndexOf](#lastIndexOf(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      返回最右边出现的指定子字符串在此字符串中的索引。 |
| int                                                          | **[lastIndexOf](#lastIndexOf(java.lang.String, int))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str, int fromIndex)      返回最后一次出现的指定子字符串在此字符串中的索引。 |
| int                                                          | **[length](#length())**()      返回长度（字符数）。          |
| int                                                          | **[offsetByCodePoints](#offsetByCodePoints(int, int))**(int index, int codePointOffset)      返回此序列中的一个索引，该索引是从给定 index 偏移 codePointOffset 个代码点后得到的。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[replace](#replace(int, int, java.lang.String))**(int start, int end, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) str)      使用给定 String 中的字符替换此序列的子字符串中的字符。 |
| [StringBuilder](http://www.daimaku.net/book/javasdk/java/lang/StringBuilder.html) | **[reverse](#reverse())**()      将此字符序列用其反转形式取代。 |
| void                                                         | **[setCharAt](#setCharAt(int, char))**(int index, char ch)      将给定索引处的字符设置为 ch。 |
| void                                                         | **[setLength](#setLength(int))**(int newLength)      设置字符序列的长度。 |
| [CharSequence](http://www.daimaku.net/book/javasdk/java/lang/CharSequence.html) | **[subSequence](#subSequence(int, int))**(int start, int end)      返回一个新字符序列，该字符序列是此序列的子序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[substring](#substring(int))**(int start)      返回一个新的 String，它包含此字符序列当前所包含字符的子序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[substring](#substring(int, int))**(int start, int end)      返回一个新的 String，它包含此序列当前所包含字符的子序列。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toString](#toString())**()      返回此序列中数据的字符串表示形式。 |
| void                                                         | **[trimToSize](#trimToSize())**()      尝试减少用于字符序列的存储空间。 |



## tips

### Java 基本数据类型

>变量就是申请内存来存储值。也就是说，当创建变量的时候，需要在内存中申请空间。
>
>内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据。
>
>通过以下方法获取 ,二进制位数 和值的范围
>
>Integer.SIZE
>
>"包装类：java.lang.Integer"
>
>Integer.MIN_VALUE
>
>Integer.MAX_VALUE
>
>```java
>public class Test {
>static boolean bool;
>static byte by;
>static char ch;
>static double d;
>static float f;
>static int i;
>static long l;
>static short sh;
>static String str;
>
>public static void main(String[] args) {
>System.out.println("Bool :" + bool);
>System.out.println("Byte :" + by);
>System.out.println("Character:" + ch);
>System.out.println("Double :" + d);
>System.out.println("Float :" + f);
>System.out.println("Integer :" + i);
>System.out.println("Long :" + l);
>System.out.println("Short :" + sh);
>System.out.println("String :" + str);
>}
>}
>//输出结果
>//Bool     :false
>//Byte     :0
>//Character:
>//Double   :0.0
>//Float    :0.0
>//Integer  :0
>//Long     :0
>//Short    :0
>//String   :null
>```
>
>#### 自动类型转换
>
>**整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。**
>
>转换从低级到高级。  
>
>```
>低  ------------------------------------>  高
>byte,short,char—> int —> long—> float —> double 
>```
>
>数据类型转换必须满足如下规则：
>
>- \1. 不能对boolean类型进行类型转换。
>
>- \2. 不能把对象类型转换成不相关类的对象。
>
>- \3. 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。
>
>- \4. 转换过程中可能导致溢出或损失精度，例如：
>
>- ```
>  int i =128;   
>   byte b = (byte)i;
>  ```
>
>  ```
>因为 byte 类型是 8 位，最大值为127，所以当 int 强制转换为 byte 类型时，值 128 时候就会导致溢出。
>
>\5. 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：
>
>```
>
>(int)23.7 == 23;        
>(int)-45.89f == -45
>
>```
>
>```

### Java 局部变量

>- 局部变量声明在方法、构造方法或者语句块中；
>- 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
>- 访问修饰符不能用于局部变量；
>- 局部变量只在声明它的方法、构造方法或者语句块中可见；
>- 局部变量是在栈上分配的。
>- 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。
>- 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。

### 输出

System.out.println();

>- println() 是一个方法。
>- System 是系统类。
>- out 是标准输出对象。 

### 时间

>获取当前时间  格式为2021-10-30 16:58
>
>```java
>Date dNow = new Date( );
>SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd hh:mm:ss");
>System.out.println("当前时间为: " + ft.format(dNow));  
>```

### 正则表达式

```java
//username要求 输入长度2-10中文、数字与字母
String regExp1 = "[\\u4e00-\\u9fa5  a-zA-Z0-9]{2,10}";
boolean rs1 = username.matches(regExp1);
//符合要求 rs1==true

//password要求 输入长度4-10数字与字母
String regExp2 = "[A-Za-z0-9]{4,10}";
boolean rs2 = password.matches(regExp2);
//符合要求 rs2==true
```

```java
 String regex = "^[A-Za-z0-9\u4e00-\u9fa5]{2,10}+$";
        if(!username.matches(regex)){
            System.out.println("注册失败");
            System.out.println("账号只能由汉字，数字，字母组成");
            return null;
        }
```

>   文本格式

```java
 String regex="^[\\u4e00-\\u9fa5]{1,7}$|^[\\dA-Za-z_]{1,14}$";
        if (!message.getContent().matches(regex)){
            System.out.println("文本长度不规范");
            return ;
        }
```

## 逻辑练习

### ASCLL的转换

```java
public class App{
    public static void main(String[] args) {
        Scanner sc=new Scanner(System.in);
        int num=sc.nextInt();
        String stringList= sc.next();
        char[] list=stringList.toCharArray();

        for(char obj :list) {
            int num2=num;
            byte byteAscii = (byte) ((byte) obj);
            while (byteAscii+num2>122){
                num2=num2-26;
            }
            System.out.print((char) ((char) byteAscii+num2));
        }
    }
}
```

### 倒序输出数组合

```
import java.util.*;

public class App {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int nums = scan.nextInt();
        List<Integer> list = new ArrayList<>();
        //长度为0时进入循环，和num相同则不进入徐明华
        while (list.size() < nums) {
            int num = scan.nextInt();
            list.add(num);
        }
        List<Integer>listRes = new ArrayList<>();
        for (int i=0;i<list.size();i++){
            for (int j=i+1;j<list.size();j++){
                for (int k=j+1;k<list.size();k++){
                    int x=list.get(i);
                    int y=list.get(j);
                    int z=list.get(k);
                    listRes.add(x+y+z);
                    System.out.print(x+","+y+","+z);
                }
            }
        }
        Collections.sort(listRes);
        Collections.reverse(listRes);
        for (Integer listRe : listRes) {
            System.out.println(listRe);
        }
    }
}                           
```

```
set转成list可以解决

List <A> list = new ArrayList<A>(B);//B是set型的
```

```
取的时候只要这样

list.get(0);
```

>   斐波那契数列

```
import java.util.Scanner;

public class App {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        long M =scanner.nextInt();

        long f1 = 0, f2 = 1, f;
        for (int i = 2; i <= M; i++) {
            f = f2;
            f2 = f1 + f2;
            f1 = f;
//            System.out.println("第" + i + "个月的兔子对数: " + f2);
        }
        System.out.println(f2);
    }
}
```

# Java Web开发基础

##  一、jsp技术

### 一、idea配置环境

**下载**

https://tomcat.apache.org/download-90.cgi

**新建项目什么都不点**

添加框架支持

![image-20211206172618372](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213055.png)

![image-20211206172758610](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213056.png)

添加配置场景

![image-20211206173151207](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213058.png)

![image-20211206173358357](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213059.png)

再次选择已经调试好的配置环境

点击设置里面的项目库，添加架包

![image-20211206175210412](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213060.png)

### 二、编写网页

JSP全称Java Server Pages，是一种动态网页开发技术。它使用JSP标签在HTML网页中插入Java代码。标签通常以<%开头以%>结束。

JSP是一种Java servlet，主要用于实现Java web应用程序的用户界面部分。网页开发者们通过结合HTML代码、XHTML代码、XML元素以及嵌入JSP操作和命令来编写JSP。

#### 常用代码

##### 1.1、指令

**page指令**

用于设置当前页面的信息，导入包，其他网页

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
```

**include指令**

```jsp
 <%@ include file="menu.jsp" %>
```

>   例： ① Hello.txt 文本文件的代码如下：

```
<%@ page contentType="text/html;charset=utf-8" %>很高兴认识你!Nice to meet you.
```

>   ② 创建 2-19.jsp 页面，具体代码如下：

```jsp
纯文本复制
<%@ page contentType="text/html;charset=utf-8" %>
<html><body bgcolor=cyan><H3>
<% include file="Hello.txt" %></H3></body></html>
```

![](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213061.png)

##### 1.2、常用内置对象

在JSP中一共预先定义了9个这样的对象，分别为request、response、session、application、out、pageContext、config、page和exception。

https://blog.csdn.net/pan_junbiao/article/details/87916435

###### 1.2.1、out

**out(输出):**对象一个最基本的应用就是向客户端浏览器输出信息,会自动转换为字符串进行输出。

```html
<% out.print("您好，pan_junbiao的博客");%>

<%= "您好，华华的博客" %>
```


println()方法也可以用于向客户端浏览器输出信息，该方法输出内容后，还输出一个换行符。

```html
<pre>
<%
    out.println("<b>使用println()方法向客户端浏览器输出文字：</b>");
    out.println("您好！");
    out.println("欢迎访问 pan_junbiao的博客");
    out.println("博客地址：https://blog.csdn.net/pan_junbiao");
%>
</pre>
```

>   使用print()方法输出内容要有换行的效果，需要使用HTML的<pre>标记括起来，否则无法显示换行效果。

###### 1.2.2、request

**request(请求):**对象用于处理HTTP请求中（获取get,post响应里面的参数）的各项参数。(封装一些浏览器的请求信息)

>   这可以通过在超链接的后面加上问号“?”来实现。同时指定多个参数使用与符号“&”分隔即可。

示例：在页面中定义超链接。	

```jsp
<a href="delete.jsp?id=1">删除</a>
```

>   获取当前路径

```
<%
    String url = request.getServletPath();
    System.out.println(url);
%>
```

>   在delete.jsp页面中，可以通过request对象的getParameter()方法获取传递的参数值。

```html
<%
    String id = request.getParameter("id");  //获取id参数的值
   
   //获取请求获得的参数
	request.getParameter("username");

	//获取请求的url地址  如index.jsp
	String servletPath = request.getServletPath();
%>
```

###### 1.2.3、response

**response(响应):**对象用于响应客户请求，向客户端输出信息。它封装了JSP产生的响应，并发送到客户端以响应客户端的请求。请求的数据可以是各种数据类型，甚至是文件。response对象在JSP页面内有效。

>   request对象的常用方法：

| 方法                                 | 说明                                         |
| :----------------------------------- | :------------------------------------------- |
| getWriter(String value)              | 输出向浏览器输出信息                         |
| sendRedirect(String path)            | 将网页重定向到另一个页面。path(指定目标路径) |
| setHeader(String name, String value) | 设置HTTP响应报头信息。                       |

**重定向：**使用response对象提供的sendRedirect()方法重定向到登录页面。

```html
<%
	response.sendRedirect("login.jsp");  //重定向跳转到登录页面
%>
```

**禁用缓存**(对于一些安全性要求比较高的网站，通常需要禁用缓存)

>   在默认情况下，浏览器将会对显示的网页内容进行缓存，这样可以提高网页的显示速度

```html
<%
	response.setHeader("Cache-Control", "no-store");
	response.setDateHeader("Expires", 0);
%>
```

**设置页面自动刷新**（使页面每隔10秒自动刷新一次。）

```html
<%
	response.setHeader("refresh", "10");
%>
```

 **定时跳转网页**（使页面5秒后自动跳转到指定的网页）

```html
<%
	response.setHeader("refresh", "5;URL=login.jsp");
%>
```

###### 1.2.4、session

**session(会话保存):**可以在应用程序的Web页面间进行跳转时，保存用户的状态，使整个用户会话一直存在下去，直到关闭浏览器

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213062.png)

**保存与获取**:session对象信息。

```java
<%
	session.setAttribute("UserName", "pan_junbiao的博客");           //保存session对象
	String userName = session.getAttribute("UserName").toString();  //获取session对象
%>
```

###### 1.2.5、application

application对象提供了两种访问应用程序初始化参数的方法。

**getInitParameter(String name)**方法：（用于获取已命名的应用程序初始化参数值。）

示例：获取上面web.xml文件中配置的url参数的值。

```
<%
	String url = application.getInitParameter("url");
%>
```

**getInitParameterNames()**方法：（获取所有已定义的应用程序初始化参数名的枚举）

示例：使用getInitParameterNames()方法获取web.xml文件中定义的全部应用程序初始化参数，并通过循环输出。

```jsp
<%@ page import="java.util.*" %>
<%
	Enumeration<String> enume = application.getInitParameterNames();   //获取全部初始化参数
	while(enume.hasMoreElements())
	{
		String name = enume.nextElement();                  //获取参数名
		String value = application.getInitParameter(name);  //获取参数值
		out.println(name + "：");  //输出参数名
		out.println(value);        //输出参数值
	}
%>
```


 **管理应用程序环境属性**: 	与session对象相同，也可以**在application对象中设置属性**。

与session对象不同的是，session只是在当前客户的会话范围内有效，当超过保存时间，session对象就被收回；

而application对象在整个应用区域中都有效。

```jsp
<%
	application.setAttribute("UserName", "pan_junbiao的博客");           //保存application对象
	String userName = application.getAttribute("UserName").toString();  //获取application对象
%>
```

### 三、循环生成文章

>   for循环花括号在最外面分开包裹元素

```java
<%
    BookService bookService=new BookService();
    List<Book> books= bookService.findBooks("",100);
%>
<ul>
    <%for (Book obj:books){%>
    <li><%=obj.getName()%></li>//表达式后面没有分号
    <li>图书2</li>
    <%}%>
</ul>

```

### 四、jsp制作博客笔记

>   获取url

```mysql
String url = request.getServletPath();
```

>   获取请求的参数

```
pages = Integer.parseInt(request.getParameter("page"));

String username=request.getParameter("username");
String password=request.getParameter("password");
```

>   重定向

```mysql
response.sendRedirect("index.jsp"); 
```

>   session的设置、获取、销毁

```mysql
session.setAttribute("authUser",user);
User user = (User) session.getAttribute("authUser");
String error = (String) session.getAttribute("error");
session.removeAttribute("error");
session.removeAttribute("authUser");
```

盒子阴影

```
box-shadow: 2px 2px 10px #909090;
```

jsp使用js

```jsp
<script type="text/javascript">
    //在首页时
    <%
    System.out.println(url);
    if((url.equals("/index.jsp"))){%>
    document.getElementById("homeBtn").setAttribute("class", "active")
    <%}%>
    //新建文章时
    <%if(url.equals("/create.jsp")){%>
    document.getElementById("createBtn").setAttribute("class", "active")
    <%}%>
    //在个人中心时
    <%if(url.equals("/myPage.jsp")){%>
    document.getElementById("myPageBtn").setAttribute("class", "active")
    <%}%>

    function selectClick() {
        let el=document.getElementById("selected")
        if (el.style.visibility !== "visible") {
            el.style.visibility = "visible"
        } else {
            el.style.visibility = "hidden"
        }
    }
</script>
```

>   **分页逻辑判断** Html

```
<ul id="btns">

        <li class=""><a href="">&laquo;</a></li>

       

    <li class="active"><a href="">1</a></li>



    <li class="active><a href="">2</a></li>

        <li class=""><a href="">&raquo;</a></li>
</ul>
```

```

```



```html
<ul id="btns">
    <%--    最小页数判断--%>

        <li class=""><a href="?page=<%=pages>1?pages-1:1%>">&laquo;</a></li>

    <%--    分页判断--%>
    <%

        for (int i = 1; i < maxPage; i++) {
            if (i < 8 && pages < 5) {
    %>

    <li class="<%out.write(pages==i?"active":"");%>"><a href="?page=<%=i%>"><%=i%>
    </a></li>

    <%} else if (i > maxPage - 8 && pages > maxPage - 4) {%>

    <li class="<%out.write(pages==i?"active":"");%>"><a href="?page=<%=i%>"><%=i%>
    </a></li>

    <%} else if (i > pages - 4 && i < pages + 4) {%>

    <li class="<%out.write(pages==i?"active":"");%>"><a href="?page=<%=i%>"><%=i%>
    </a></li>

    <%
            }
        }
    %>
        <li class=""><a href="?page=<%=pages<maxPage-1?pages+1:pages%>">&raquo;</a></li>
</ul>
```

>   **分页样式** css

```css
#btns {
    margin-left: 50px;
}

#btns li {
    border: 0;
    margin: 0;
    padding: 0;
    font-size: 11px;
    list-style: none; /* savers */
    float: left;
}

#btns a {
    border: solid 1px #9aafe5;
    margin-right: 2px;
}

#btns .btn-off, #btns .next-off {
    border: solid 1px #DEDEDE;
    color: #888888;
    display: block;
    float: left;
    font-weight: bold;
    margin-right: 2px;
    padding: 3px 4px;
}

#btns .next a, #btns .btn-off a {
    font-weight: bold;
}

#btns .active {
    background: lavender;
    color: azure;
    display: block;
}

#btns a:link, #btns a:visited {
    color: #0e509e;
    display: block;
    float: left;
    padding: 3px 6px;
    text-decoration: none;
}

#btns a:hover {
    border: solid 1px #0e509e;
}

```

## 二、SpringBoot框架

SpringBoot是java里面主流开发框架，可以简化javaweb开发，提高开发效率

官网：https://spring.io/projects/spring-boot

### 一、配置环境

#### 1.1、打开官网

https://start.spring.io/配置基础环境

>   Project:Maven Project
>
>   Language:java
>
>   SpringBoot2.5.7

![image-20211211142521341](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213063.png)

#### 1.2、添加依赖

**Spring Web**  

**Spring Boot DevTools**：开发工具包		

**MySQL Driver**	：mysql驱动，mysql架包

**MyBatis Framework**：简化MySQL的操作

**Lombok** ：在项目库下载Lombok

**Thymeleaf**：模板引擎 加载Html

>   添加完点击generate自动创建项目，查看项目是否为jdk1.8，java.8

#### 1.3、文件夹用法

```
MVC: 

Controller控制器（映射url，model传入数据，控制return到不同html）,
view 视图（显示模板与数据，用户界面），
model模型（传递数据）
```

**编写代码目录为**：**src/main/ **     下同级目录

**templates**:模板

浏览器先访问**controller**文件夹，把**templates**下的html显示出来

**创建java文件**：**src/main/java/com.example.demo/controller/HellController.java**

**创建html文件**：**src/main/resources/templates/home.html**



### 二、写法

新建demo文件

#### /resources/(sql引入)

修改src/resources/application.properties配置文件

```python
## 应用名称
spring.application.name=demo
## 端口号
server.port=8080
## 当前环境为开发环境
spring.profiles.active=dev
## MySQL连接字符串
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/article?useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai
## 数据库连接的用户名和密码
spring.datasource.username=root
spring.datasource.password=
## 数据库驱动
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

## 列名下划线转驼峰
mybatis.configuration.map-underscore-to-camel-case=true
## 控制台打印sql
mybatis.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl

```

#### /mapper/(接口)

```java
@Select    //ibatis的简化写法

@Select("SELECT * FROM article WHERE id=#{id}")//#{id}占位符
Book findBookById(@Param("id")int id);//获取参数id的参数
```

```java
package com.example.demo.mapper;
import com.example.demo.entity.Book;
import org.apache.ibatis.annotations.Param;
import org.apache.ibatis.annotations.Select;
import java.util.List;

public interface BookMapper {

    @Select("SELECT * FROM article")//sql简化语句
    List<Book> findBook();

    @Select("SELECT * FROM article WHERE id=#{id}")//#{id}占位符
    Book findBookById(@Param("id")int id);//获取参数id的参数
}

```

#### /controller/(控制器)

**src/main/java/com.example.demo/controller/HellController.java**

```java
@Controller //告诉框架这个类一个控制器

@GetMapping("/") //告诉框架这个方法是要映射url的

@Resource //自动连接接口
@Autowired //自动连接接口
BookMapper bookMapper;
```

```java
@GetMapping("/detail") //是url的映射，告诉框架这个方法是要映射url的
public String detail(Model model, HttpServletRequest request) {
    //获取响应中的参数，并把参数转化为整数
    int id= Integer.parseInt(request.getParameter("id"));
    Book book = bookMapper.findBookById(id);
    model.addAttribute("book",book);
    return "detail";//会被浏览器请求，detail.html模板文件
}
```

```java
package com.example.demo.controller;
import com.example.demo.entity.Book;
import com.example.demo.mapper.BookMapper;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

import javax.annotation.Resource;
import javax.servlet.http.HttpServletRequest;
import java.util.List;

//MVC Controller View Model
//Controller控制（控制return模板）,view 视图（显示模板与数据），model模型（传递数据）


@Controller  //告诉框架这个类一个控制器
public class HelloController {
//    @Autowired //自动连接接口
    @Resource //自动连接接口
    BookMapper bookMapper;

    @GetMapping("/detail") //是url的映射，告诉框架这个方法是要映射url的
    public String detail(Model model, HttpServletRequest request) {

        //获取响应中的参数，并把参数转化为整数
        int id= Integer.parseInt(request.getParameter("id"));
        Book book = bookMapper.findBookById(id);
        model.addAttribute("book",book);
        return "detail";//会被浏览器请求，home.html模板文件
    }

    @GetMapping("/") //是url的映射，告诉框架这个方法是要映射url的
    public String home(Model model) {

        List<Book>books=bookMapper.findBook();

        model.addAttribute("books",books);
        return "home";//会被浏览器请求，home.html模板文件
    }
}

```

#### /entity/(实体类)

**com.example.demo/entity/Book.java(实体类)** 

>   lombok插件

```java
@Data   //get、set访问器
@AllArgsConstructor //全参构造方法
@NoArgsConstructor //无参构造方法
```

```java
package com.example.demo.entity;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data   //get、set访问器
@AllArgsConstructor //全参构造方法
@NoArgsConstructor //无参构造方法
public class Book {

    private int id;
    private String name;
    private String price;
    private String isbn;
}

```

#### /templates/(模板)

```html
<html lang="zh-CN" xmlns:th="http://www.thymeleaf.org/">

<ul>
<!--each循环-->
<li th:each="book:${books}">
<!--跳转网页,显示变量-->
<a th:href="@{'/detail?id='+${book.id}}"th:text="${book.name}"></a>
</li></ul>
```

**home.html**

```html
<!DOCTYPE html>
<html lang="zh-CN" xmlns:th="http://www.thymeleaf.org/">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<ul>
    <!--each循环-->
    <li th:each="book:${books}">
        <!--跳转网页,显示变量-->
        <a th:href="@{'/detail?id='+${book.id}}"   th:text="${book.name}"></a>
    </li>
</ul>

</body>
</html>
```

**detail.html**

```html
<!DOCTYPE html>
<html lang="zh-CN"  xmlns:th="http://www.thymeleaf.org/">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div id="" th:text="${book}"></div>
</body>
</html>
```

## 三、Api开发

在pom. xml里是下载的框架和版本号可以手动添加

.m2文件夹下面有下载的所有依赖

**@RestController**

**返回的东西是用于json数据的**

>相当于@Controller+@ResponseBody两个注解的结合，
>返回json数据不需要在方法前面加@ResponseBody注解了，
>但使用@RestController这个注解，
>就不能返回jsp,html页面，视图解析器无法解析jsp,html页面

**@Constroller**

>在对应的方法上，视图解析器可以解析return 的jsp,html页面，并且跳转到相应页面
>
>若返回json等内容到页面，则需要加@ResponseBody**注解**

**RESTful**风格API设计

**统一响应格式**:

```
{"code": "SUCCESS", "message": null, "data": null}
```

>   code 为 SUCCESS 代表请求成功，data 中存放具体的业务数据。

```
{"code":"ERROR","message":"失败原因","data":null}
```

>   code 不为 SUCCESS 代表请求失败,message 中是失败原因。

#### 1、响应 JSON

##### 1、单个对象

```java
@RestController
public class DemoController {
    @GetMapping("/demo/hi")
    public  String h1(){
        return "hi";
    }
    @GetMapping("/demo/getBook")
    public Book getBook(){
       Book book=Book.builder().id(1).name("java编程思想").build();
        return book;
    }
}
```

```java
@Builder //静态方法builder，链式的调用
Book book=Book.builder().id(1).name("java编程思想").build();
```

##### 2、集合

```java
@RestController
public class DemoController {
    @GetMapping("/demo/getBooks")
    public List<Book> getBooks(){
        List <Book> books=new ArrayList<Book>();
        books.add(Book.builder().id(1).name("java编程语言").build());
        books.add(Book.builder().id(2).name("天才在左，疯子在右").build());
        return books;
    }
}
```

##### 3、状态码和数据

```java
//RestController
//会将return的数据理解为字符串,转换类
@RestController
public class DemoController {
    @GetMapping("/demo/getResult")
    public Result getResult(){
        Result result=new Result("SUCESS",null,"hello");
        return result;
    }
}
```

>建一个/util/Result.java结果模板

```java
package com.example.demo.util;
import lombok.AllArgsConstructor;
import lombok.Getter;

@Getter
@AllArgsConstructor
//结果的模板类
public class Result {
    private final String code;
    private final String message;
    private final String date;
}
```

##### 4、泛型信息

>   单个结果集

```java
//RestController
//会将return的数据理解为字符串,转换类
@RestController
public class DemoController {
    @GetMapping("/demo/getResult")
    public Result<Book> getResult(){
        Book book=Book.builder().id(1).name("java编程语言").build();
        Result result=new Result("SUCESS",null,book);
        return result;
    }
}
```

>   多个结果集

```java
@GetMapping("/demo/getResults")
public Result<List <Book>> getResults(){
List <Book> books=new ArrayList<Book>();
    books.add(Book.builder().id(1).name("java编程语言").build());
    books.add(Book.builder().id(2).name("天才在左，疯子在右").build());

    Result result=new Result("SUCCESS",null,books);
    return result;
}
```

>建一个/util/Result.java结果模板

```java
package com.example.demo.util;
import lombok.AllArgsConstructor;
import lombok.Getter;

@Getter
@AllArgsConstructor
//结果的模板类
public class Result<T> {
    private final String code;
    private final String message;
    private final T date;
}
```

#### 2、接收参数

**新建一个/dto/文件夹 获取请求内容**

```java
package com.example.demo.dto;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;
//请求参数的模板
@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class DemoRequest {
    private String name;
    private int page;
    private int limit;
}
```

##### Query Params

>   传递参数的时候需要在URL地址中指定传递参数的形式参数：

```java
//获取url的get传参
@GetMapping("/demo/params1")
public String params(HttpServletRequest request){
    System.out.println(request.getParameter("name"));
    return request.getParameter("name");
}
//SpringBoot会自动从get找到name，并且注入到参数列表里面
@GetMapping("/demo/params2")
public String paramsGet(String name,int page,int limit){
    System.out.println(name);
    System.out.println(page);
    System.out.println(limit);
    return name+" "+page+" "+limit;
}
//在dto文件夹下创建一个类接收对应的参数
//get传参，参数模板为对象
@GetMapping("/demo/params3")
public DemoRequest paramsGet(DemoRequest demoRequest){
    System.out.println(demoRequest);
    return demoRequest;
}
```

##### PathParam(post请求)

>传递参数的时候直接就是将参数写到后面

```java
//路径传参
@PostMapping("/demo/book/{bookId}/user/{userId}")
public String paramsPost3(@PathVariable String bookId,@PathVariable String userId){
   System.out.println(bookId+""+userId);

   return bookId+userId;
}
@DeleteMapping("/demo/book2/{bookId}/user/{userId}")
public String paramsPost4(@PathVariable String bookId,@PathVariable String userId){
    System.out.println(bookId+""+userId);
	return bookId+userId;
}

```

##### **from表单**(post请求)：

>**application/x-www-form-urlencoded**
>
>post>body>x-www-form-urlencoded>key,value 

```java
@PostMapping("/demo/params4")
    public DemoRequest paramsPost(DemoRequest demoRequest){
    System.out.println(demoRequest);
    return demoRequest;
}
```

##### **json**(post请求)：

>**application/json**
>
>post>body>raw>json{"name":jack,"age":16} 

```java
//json传参
@PostMapping("/demo/paramsPost2")
public DemoRequest paramsPost2(@RequestBody DemoRequest demoRequest){
    System.out.println(demoRequest);
    return demoRequest;
}
```

#### 3、mybatis Script语法

```
public interface BookMapper {

    @Select("SELECT * FROM article")//sql简化语句
    List<Book> findBook();

	//#{id}占位符参数传递，注解后面是什么，占位符就代表i的是什么，与变量无关
    @Select("SELECT * FROM article WHERE id=#{id}")
    Book findBookById(@Param("id")int id);//获取参数id的参数
}
```

##### 流程分支

```java
@Select(
"<script>" +
"SELECT * FROM book" +
"<where>" +
"<if test='book.name != null'> AND name LIKE CONCAT ('%',#{book.name},'%') </if>" +
"<if test='book.id != 0'> AND id=#{book.id}</if>" +
"</where>"+
"ORDER BY id DESC" +
"LIMIT #{pagination.offset}, #{pagination.limit}"+
"</script>" +
)
```

##### 循环插入

```java
@Insert("<script>" +
        "INSERT INTO plan_item " +
        "(tenant_id,plan_id,product_id,service_type,type,price,percentage,status) VALUES " +
        "<foreach collection='planItems' item='item' separator=','>" +
        "(#{item.tenantId},#{item.planId},#{item.productId},#{item.serviceType},#{item.type},#{item.price},#{item.percentage},#{item.status})" +
        "</foreach>" +
        "</script>")
@Options(useGeneratedKeys = true, keyProperty = "id")
void createPlanItems(@Param("planItems") List<PlanItem> planItems);
```

```
@Insert("<script>" +
        "INSERT INTO tag " +
        "(name,post_id) VALUES " +
        "<foreach collection='tagList' item='item' separator=','>" +
        "(#{item.name},#{item.postId})" +
        "</foreach>" +
        "</script>")
@Options(useGeneratedKeys = true, keyProperty = "id")
int create(@Param("tagList") List<Tag> tagList);
```

##### 循环查询

```java
@Select(
      "<script>" +
            "SELECT * FROM book WHERE id in" +
            " <foreach collection='books' item='item' index='index' open='(' separator=',' close=')'> #{item}</foreach>" +
      "</script>"
)
List<Book> findBookByids(@Param("ids")List<Interger>ids);
```

```java
@Select(
"<script>" +
"SELECT * FROM book WHERE id in" +
" <foreach collection='books' item='item' index='index' open='(' separator=',' close=')'> #{item.id} </foreach>" +
"</script>" +
)
List<Book> findBookList(List<Book> books);
```

![image-20211231104832716](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213064.png)

#### 4、图书管理后端

###### /controller/

**BookController.java**

```java
package com.example.books.controller;
import com.example.books.dto.BookRequest;
import com.example.books.dto.Pagination;
import com.example.books.entity.Book;
import com.example.books.mapper.BookMapper;
import com.example.books.util.Result;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.web.bind.annotation.*;

import javax.annotation.Resource;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

@CrossOrigin
@RestController
public class BookController {
    //@Autowired //自动连接接口
    @Resource //自动连接接口
    BookMapper bookMapper;


    //复杂查询图书
    @GetMapping("/books")
    //返回泛型Map集合，传入书籍参数，分页信息
    public Result<Map<String, Object>> getAllBooks(Book book, Pagination pagination){
        //查询数量
        pagination.setTotal(bookMapper.count(book));
        //为0时报错
        if(pagination.getTotal()==0){
            return new Result<>("ERROR","未查寻到图书",null);
        }
        //获取所有信息
        List<Book> books = bookMapper.findBooks(book,pagination);

        //设置返回模板
        Result<Map<String, Object>> result;
        //设置返回参数data，并且添加数据
        Map<String, Object> data=new HashMap<>();
        data.put("pagination",pagination);
        data.put("books",books);

        result=new Result<>("SUCCESS","查找成功",data);
        return result;

    }

    //获取所有图书
//    @GetMapping("/books")
//    public Result<List <Book>> getResults(){
//        List<Book> books=bookMapper.findAllBook();
//        Result<List<Book>> result=new Result<>("SUCCESS",null,books);
//        return result;
//    }
    //获取单本图书
    @GetMapping("/books/{bookId}")
    public Result<Book> paramsGet(@PathVariable String bookId){
        Book book=bookMapper.findIdBook(bookId);
        Result<Book> result;

        if (book!=null){
            result=new Result<>("SUCCESS","查找成功",book);
        }else{
            result=new Result<>("ERROR","查无此书",null);
        }

        System.out.println(result);
        return result;
    }
    //新增图书
    @PostMapping("/books")
    public Result<Book> paramsPost(BookRequest bookRequest){
        //创建book类接收参数
        Book book=Book.builder().name(bookRequest.getName()).describe(bookRequest.getDescribe()).price(bookRequest.getPrice()).build();
        //创建返回结果
        Result<Book> result;
        //判断是否为空
        if(book.getName()==null||book.getDescribe()==null || book.getName().equals("") || book.getDescribe().equals("")){
            result=new Result<>("ERROR","描述和书名不能为空",null);
            return result;
        }
        //传入参数，插入mysql
        bookMapper.insertBook(book);
        if(book.getId()!=0){
            result= new Result<>("SUCCESS", "新增成功", book);
        }else {
            result=new Result<>("ERROR","新增失败",null);
        }
    return result;
    }
    //更改图书信息
    @PostMapping("/books/{bookId}")
    public Result<String> paramsUpdate(@PathVariable String bookId,@RequestBody BookRequest bookRequest){
        //创建book类接收参数
        Book book=Book.builder().name(bookRequest.getName()).describe(bookRequest.getDescribe()).price(bookRequest.getPrice()).build();
        //创建返回结果
        Result<String> result;
        //判断是否为空
        if(book.getName()==null||book.getDescribe()==null|| book.getName().equals("") || book.getDescribe().equals("")){
            result=new Result<>("ERROR","描述和书名不能为空",null);
            return result;
        }
        //传入参数，插入mysql
        int update=bookMapper.update(bookId,book);
        if(update==1){
            result=new Result<>("SUCCESS","更新成功",null);
        }else{
            result=new Result<>("ERROR","更新失败,未查到书籍信息",null);
        }
        return result;

    }
    //删除图书Delete
    @DeleteMapping("/books/{bookId}")
    public Result<String> paramsDelete(@PathVariable String bookId){
        //接收删除数量信息
        int delete=bookMapper.delete(bookId);
        //创建返回结果
        Result<String> result;
        //逻辑判断
        if (delete==1){
            result=new Result<>("SUCCESS","删除成功",null);
        }else{
            result=new Result<>("ERROR","删除失败,图书不存在",null);
        }
        return result;
    }

}

```

###### /mapper/

```java
package com.example.books.mapper;

import com.example.books.dto.Pagination;
import com.example.books.entity.Book;
import org.apache.ibatis.annotations.*;

import java.util.List;

public interface BookMapper {

    //    //复杂查询
    @Select("<script>" +
            "SELECT * FROM books " +
            "<where>" +
            "<if test='book.name !=null'> AND name LIKE CONCAT('%',#{book.name},'%') </if>" +
            "<if test='book.id !=0'>AND id=#{book.id}</if>" +
            "</where>" +
            "ORDER BY id DESC " +
            "LIMIT #{pagination.offset},#{pagination.limit}" +
            "</script>")
    List<Book> findBooks(@Param("book") Book book, @Param("pagination") Pagination pagination);

    //统计条数
    @Select("<script>" +
            "SELECT COUNT(*) FROM books" +
            "<where>" +
            "<if test='book.name !=null'> AND name LIKE CONCAT('%',#{book.name},'%') </if>" +
            "<if test='book.id !=0'>AND id=#{book.id}</if>" +
            "</where>" +
            "</script>")
    long count(@Param("book") Book book);
    
    //查找所有图书
    @Select("SELECT * FROM books")
    List<Book> findAllBook();

    //查询一本图书信息
    @Select("SELECT * FROM books WHERE id=#{id} ")
    Book findIdBook(@Param("id") String id);

    //新增图书,自主获取并且更改主键
    @Insert("INSERT INTO books (name,`describe`,`price`)VALUES (#{name},#{describe},#{price})")
    @Options(useGeneratedKeys = true, keyProperty = "id", keyColumn = "id")
    void insertBook(Book book);

    //更改图书，返回受影响行数
    @Update("UPDATE books SET name=#{book.name},`describe`=#{book.describe},price=#{book.price} WHERE id =#{id}")
    int update(@Param("id") String id, @Param("book") Book book);

    //删除图书，返回受影响行数
    @Delete("DELETE FROM books WHERE id=#{id}")
    int delete(@Param("id") String id);
}
```

###### /dto/

**BookRequset.java**

```java
package com.example.books.dto;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

//接收类
@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class BookRequest {
private String name;
private String describe;
private String price;
}

```

**Pagination.java**

```java
package com.example.books.dto;

import com.fasterxml.jackson.annotation.JsonIgnoreProperties;
import lombok.ToString;

@ToString
@JsonIgnoreProperties(value = {"offset"})
public class Pagination {

    protected int page;
    protected int limit;
    protected long total;

    public Pagination() {
        limit = 5;
        page = 1;
    }

    public Pagination(int page, int limit) {
        setPage(page);
        setLimit(limit);
    }

    public Pagination(int page, int limit,long total) {
        setPage(page);
        setLimit(limit);
        setTotal(total);
    }

    public long getTotal() {
        return total;
    }

    public void setTotal(long total) {
        this.total = total;
    }

    public int getPage() {
        return page;
    }

    public void setPage(int page) {
        this.page = page > 0 ? page : 1;
    }

    public int getOffset() {
        return (page - 1) * limit;
    }

    public void setLimit(int limit) {
        if (limit > 0) {
            this.limit = limit;
        }
    }

    public int getLimit() {
        return limit;
    }
}
```

###### /util/

**Result.java**

```java
package com.example.books.util;


import lombok.AllArgsConstructor;
import lombok.Getter;


@Getter
@AllArgsConstructor
//结果的模板类
public class Result<T> {
    private final String code;
    private final String message;
    private final T data;
}
```

###### /com.example.books/

BooksApplication.java

```
package com.example.books;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;


@SpringBootApplication
@MapperScan("com.example.books.mapper") //配置接口目录文件，方便框架查询接口@MapperScan("com.example.books.mapper") //配置接口目录文件，方便框架查询接口
public class BooksApplication {

    public static void main(String[] args) {
        SpringApplication.run(com.example.books.BooksApplication.class, args);
    }

}
```

#### 5、图书管理前端

###### /src/

**index.js**

```
import React from "react";
import { render } from "react-dom";

import App from "./app";

render (<App/>,document.getElementById('root'))
```

**app.js**

```
import React from "react"
import Article from "./pages/article"
import { Layout, Menu, Breadcrumb } from 'antd';
import { UserOutlined, LaptopOutlined, NotificationOutlined } from '@ant-design/icons';
import 'antd/dist/antd.css';
//安装路由
// npm install -S react-router-dom
// 导入路由组件,切换组件，路径组件
import { HashRouter, Switch, Route } from "react-router-dom"
import Home from "./pages/home"
//import {link} from "react-router-dom"
export default function App(params) {
    const { Header, Content, Footer, Sider } = Layout;
    const { SubMenu } = Menu;
    return (
        <Layout>
    <Header className="header">
      <div className="logo" />
      <Menu theme="dark" mode="horizontal" defaultSelectedKeys={['2']}>
        <Menu.Item key="1">nav 1</Menu.Item>
        <Menu.Item key="2">nav 2</Menu.Item>
        <Menu.Item key="3">nav 3</Menu.Item>
      </Menu>
    </Header>
    <Content style={{ padding: '0 50px' }}>
      <Breadcrumb style={{ margin: '16px 0' }}>
        <Breadcrumb.Item>Home</Breadcrumb.Item>
        <Breadcrumb.Item>List</Breadcrumb.Item>
        <Breadcrumb.Item>App</Breadcrumb.Item>
      </Breadcrumb>
      <Layout className="site-layout-background" style={{ padding: '24px 0' }}>
        <Sider className="site-layout-background" width={200}>
          <Menu
            mode="inline"
            defaultSelectedKeys={['1']}
            defaultOpenKeys={['sub1']}
            style={{ height: '100%' }}
          >
            <SubMenu key="sub1" icon={<UserOutlined />} title="subnav 1">
              <Menu.Item key="1">option1</Menu.Item>
              <Menu.Item key="2">option2</Menu.Item>
              <Menu.Item key="3">option3</Menu.Item>
              <Menu.Item key="4">option4</Menu.Item>
            </SubMenu>
            <SubMenu key="sub2" icon={<LaptopOutlined />} title="subnav 2">
              <Menu.Item key="5">option5</Menu.Item>
              <Menu.Item key="6">option6</Menu.Item>
              <Menu.Item key="7">option7</Menu.Item>
              <Menu.Item key="8">option8</Menu.Item>
            </SubMenu>
            <SubMenu key="sub3" icon={<NotificationOutlined  />} title="subnav 3">
              <Menu.Item key="9">option9</Menu.Item>
              <Menu.Item key="10">option10</Menu.Item>
              <Menu.Item key="11">option11</Menu.Item>
              <Menu.Item key="12">option12</Menu.Item>
            </SubMenu>
          </Menu>
        </Sider>
        <Content style={{ padding: '0 24px', minHeight: 280 }}>
        <HashRouter>            {/*HashRouter路由组件*/}
            <Switch>            {/*Switch切换组件*/}
                {/* <Route exact path="/" component={Login}></Route>  */}
                <Route exact path="/home" component={Home}></Route>
                {/* exact：精确匹配,不会覆盖路径下的其他组件
                    path：路径，component：组成*/}
                <Route  path="/article" component={Article}></Route>
            </Switch>
        </HashRouter>
        </Content>
      </Layout>
    </Content>
    <Footer style={{ textAlign: 'center' }}>Ant Design ©2018 Created by Ant UED</Footer>
  </Layout>
        
    )
}
```

###### /page/article/

**index.js**

```
import React from "react"
import Create from "./compoents/create"
import Articles from "./compoents/index"
import Edit from "./compoents/edit"


//安装路由
// npm install -S react-router-dom
// 导入路由组件,切换组件，路径组件
import { HashRouter, Switch, Route } from "react-router-dom"

//import {link} from "react-router-dom"
export default function Article(params) {



    return (

        <HashRouter>
            awdawdaadwada
            <Switch>            {/*Switch切换组件*/}
                <Route path="/article/create" component={Create}></Route>
                <Route path="/article/edit/:id" component={Edit}></Route>
                <Route  path="/article" component={Articles}></Route>
            </Switch>
            3243423432
        </HashRouter>
    )
}
```

###### /page/article/compoents

**index.js**

```
import React, { useEffect, useState } from "react"
import { Link } from "react-router-dom"
import axios from "axios"

import "./index.css"


export default function Index(props) {
    const [bookName, setBookName] = useState("")
    const [articles, setArticles] = useState([])
    const [pagination, setPagination] = useState({})
    const [pageLimit, setPageLimit] = useState({
        page: 1,
        limit: 2,
    })
    const outBtn = () => {
        let maxPage = Math.ceil(pagination.total / pagination.limit)
        let el = []
        console.log(pagination);
        for (let i = 1; i < maxPage + 1; i++) {
            if (i < 8 && pagination.page < 5) {
                el.push(<li className={pagination.page === i ? "active" : ""}
                    onClick={() => {
                        setPageLimit({ ...pageLimit, page: i })
                    }}
                    key={i}><span>{i}</span></li>)

            } else if (i > maxPage - 8 && pagination.page > maxPage - 4) {
                el.push(<li className={pagination.page === i ? "active" : ""}
                    onClick={() => {
                        setPageLimit({ ...pageLimit, page: i })
                    }}
                    key={i}><span>{i}</span></li>)

            } else if (i > pagination.page - 4 && i < pagination.page + 4) {
                el.push(<li className={pagination.page === i ? "active" : ""}
                    onClick={() => {
                        setPageLimit({ ...pageLimit, page: i })
                    }}
                    key={i} ><span>{i}</span></li>)

            }
        }
        return el
    }
    const getData = () => {
        axios({
            method: "Get",
            url: `http://localhost:8080/books`,
            headers: { 'Content-Type': 'application/json' },
            params: {
                "name": bookName,
                "page": pageLimit.page,
                "limit": pageLimit.limit,
            }
        }).then((res) => {
            if (res.data.code === "SUCCESS") {
                setArticles(res.data.data.books)
                setPagination(res.data.data.pagination)
      

            } else {
                setBookName("")
                alert(res.data.message)
                setPageLimit({...pageLimit,page:1})
               
            }
         
        }).catch((error) => {
            alert("出错了")
        })
    }
    useEffect(() => {
        getData()
        return () => {
        }
        // eslint-disable-next-line react-hooks/exhaustive-deps
    }, [pageLimit])
    const deleteArticle = (id) => {
        axios({
            method: "DELETE",
            url: `http://localhost:8080/books/${id}`,
            // headers: { 'Content-Type': 'application/json' },

        }).then((res) => {
            if (res.data.code === "SUCCESS") {
                console.log(res.data.data);
            } else {
                console.log(res.data.message)
            }
            alert(res.data.message)
            setPageLimit({...pageLimit,page:1})
        }).catch((error) => {
            alert("出错了")
        })
    }
    return (
        <div className="books">
            <div className="top">
                <div><h2>图书管理</h2></div>
                <Link to="/article/create" className="right"
                
                
                >+ 新增</Link>
            </div>
            <div className="top2">
                书名<input placeholder="请输入书名"
                    onChange={(e) => { setBookName(e.target.value) }}
                    value={bookName}
                /><input type="button" value="搜索" 
                
                onClick={()=>{getData()}}
                /><input type="button" value="清空" 
                
                onClick={()=>{
                    setBookName("")
                    setPageLimit({...pageLimit,page:1})
                }}
                />
            </div>
            <div className="table">
                <div className="border" >
                    <div>编号</div><div>书名</div><div>单价</div><div>状态</div><div>新增时间</div><div>操作</div>
                </div>
                {
                    articles.map((item) => {
                        return (
                            <div className="border" key={item.id}>
                                <div>{item.isbn}</div>
                                <div>{item.name}</div>
                                <div>{item.price}</div>
                                <div>{item.status === "1" ? "启用" : "禁用"}</div>
                                <div>{item.createdAt}</div>
                                <div>
                                    <span
                                    onClick={()=>{
                                   
                                  
                                        props.history.push(`/article/edit/${item.id}`)
                                    }}
                                    
                                    
                                    >编辑</span>
                                    <span onClick={() => {
                                        deleteArticle(item.id)
                                       
                                    }}>删除</span>
                                </div>
                            </div>
                        )
                    })
                }


            </div>
           
            <div id="btn">
                <ul id="btns">

                    <li className=""


                        onClick={() => {
                            setPageLimit({
                                ...pageLimit, page: pagination.page - 1 > 1 ? pagination.page - 1 : 1
                            })
                        }}
                    ><span>&laquo;</span></li>
                    {outBtn()}
                    <li className=""

                        onClick={() => {
                            setPageLimit({
                                ...pageLimit, page: pagination.page < Math.ceil(pagination.total / pagination.limit) ? pagination.page + 1 : Math.ceil(pagination.total / pagination.limit)
                            })
                        }}
                    ><span>&raquo;</span></li>
                </ul>
            </div >
            <span>共{pagination.total}条</span>
            <select onChange={(e) => {
                setPageLimit({
                    page: 1,
                    limit: e.target.value
                })
            }}>
                <option value='5'>每页5条</option>
                <option value='10'>每页10条</option>
                <option value='15'>每页15条</option>
            </select>
         
            <span >跳转到
                <input type="number"
                    onKeyDown={(e) => {
                        if (e.keyCode === 13) {
                            if (e.target.value < 1) {
                                e.target.value = 1
                            }
                            else if (e.target.value > Math.ceil(pagination.total / pagination.limit)) {
                                e.target.value = Math.ceil(pagination.total / pagination.limit)
                            }

                            setPageLimit({ ...pageLimit, page: e.target.value })

                        }

                    }}
                    className="jumpPage" />页</span>

        </div>
    )
}
```

edit.js

```
import React, { useEffect, useState } from "react"
import axios from "axios"
import "./edit.css"
import qs from "qs"
// import {Switch,Route} from "react-router-dom"


export default function Edit(props) {
   const [ name , setName] = useState("")
   const [ describe  , setDescribe ] = useState("")
    const getData=()=>{
        let id = props.match.params.id;
        
        axios({
            method: "GET",
            url: `http://localhost:8080/books/${id}`,
            headers: { 'Content-Type': 'x-www-form-urlencoded' },
        
        }).then((res) => {
            console.log(res.data)
            // alert(res.data.message);
            if(res.data.code==="SUCCESS"){
                setName(res.data.data.name)
                setDescribe(res.data.data.describe)
            }
         
        }).catch((error) => {
            alert("出错了")
        })
        
    }
    useEffect(()=>{
        getData()
    // eslint-disable-next-line react-hooks/exhaustive-deps
    },[])
    const updateData = () => {
        let id = props.match.params.id;
        axios({
            method: "POST",
            url: `http://localhost:8080/books/37`,
            headers: { 'Content-Type': 'application/json' },
            data: { 
                "name":name,
                "describe":describe
             }
        }).then((res) => {
            if (res.data.code === "SUCCESS") {
                props.history.push("/article")
            } 
            alert(res.data.message);
         
        }).catch((error) => {
            alert("出错了")
        })
    }
    return (
            <div className="edit">
                <h2>更新文章</h2>
                <div className="tip">{}</div>
                <div>标题:<br/>
                <input type="text" 
                onChange={(e)=>{
                    setName(e.target.value)

                }}
                value={name}
                /></div>
                <div>内容:<br/>
                <textarea type="text"
                   onChange={(e)=>{
                    setDescribe(e.target.value)

                }}
                value={describe}
                ></textarea></div>
                <button 
                
                onClick={()=>{
                    updateData()
                }}
                
                >提交</button><br/>
                <button>返回</button>
            </div>

        )
    
}
```

**create.js**

```
import React, { useState } from "react"
import axios from "axios"
import "./edit.css"
// import {Switch,Route} from "react-router-dom"


export default function Create(props) {
   const [ name , setName] = useState("")
   const [ describe  , setDescribe ] = useState("")
 
    const createData = () => {
        axios({
            method: "POST",
            url: `http://localhost:8080/books`,
            headers: { 'Content-Type': 'x-www-form-urlencoded' },
            params: {
               "name":name,
               "describe":describe
            }
        }).then((res) => {
            if (res.data.code === "SUCCESS") {
                props.history.push("/article")
            } 
            alert(res.data.message);
         
        }).catch((error) => {
            alert("出错了")
        })
    }
    return (
            <div className="edit">
                <h2>新增文章</h2>
                <div className="tip">{}</div>
                <div>标题:<br/>
                <input type="text" 
                onChange={(e)=>{
                    setName(e.target.value)

                }}
                value={name}
                /></div>
                <div>内容:<br/>
                <textarea type="text"
                   onChange={(e)=>{
                    setDescribe(e.target.value)

                }}
                value={describe}
                ></textarea></div>
                <button 
                
                onClick={()=>{
                    createData()
                }}
                
                >提交</button><br/>
                <button>返回</button>
            </div>

        )
}
```

## 四、登录和token拦截

### 参数校验

**添加依赖@Valid**

>   在pom.xml处手动导入javax.validation.Valid依赖  或者alt+enter 再右击点搜索依赖向
>
>   ```java
>   //导入javax.validation.Valid依赖
>   <dependency>
>     <groupId>javax.validation</groupId>
>     <artifactId>validation-api</artifactId>
>     <scope>compile</scope>
>   </dependency>
>   ```
>
>   @高版本解决方案
>
>   ```
>    <dependency>
>              <groupId>org.springframework.boot</groupId>
>              <artifactId>spring-boot-starter-validation</artifactId>
>          </dependency>
>   ```
>
>   **@Valid无效时** 
>
>   ```java
>   <dependency>
>     <groupId>jakarta.validation</groupId>
>     <artifactId>jakarta.validation-api</artifactId>
>     <version>2.0.2</version>
>     </dependency>
>   
>     <dependency>
>     <groupId>org.hibernate.validator</groupId>
>     <artifactId>hibernate-validator</artifactId>
>     <version>6.1.1.Final</version>
>     <!--<version>7.0.1Final</version>-->
>     </dependency>
>   ```

#### 验证器

| 限制                      | 说明                                                         |
| :------------------------ | :----------------------------------------------------------- |
| @Null                     | 限制只能为null                                               |
| @NotNull                  | 限制必须不为null                                             |
| @AssertFalse              | 限制必须为false                                              |
| @AssertTrue               | 限制必须为true                                               |
| @DecimalMax(value)        | 限制必须为一个不大于指定值的数字                             |
| @DecimalMin(value)        | 限制必须为一个不小于指定值的数字                             |
| @Digits(integer,fraction) | 限制必须为一个小数，且整数部分的位数不能超过integer，小数部分的位数不能超过fraction |
| @Future                   | 限制必须是一个将来的日期                                     |
| @Max(value)               | 限制必须为一个不大于指定值的数字                             |
| @Min(value)               | 限制必须为一个不小于指定值的数字                             |
| @Past                     | 限制必须是一个过去的日期                                     |
| @Pattern(value)           | 限制必须符合指定的正则表达式                                 |
| @Size(max,min)            | 限制字符长度必须在min到max之间                               |
| @Past                     | 验证注解的元素值（日期类型）比当前时间早                     |
| @NotEmpty                 | 验证注解的元素值不为null且不为空（字符串长度不为0、集合大小不为0） |
| @NotBlank                 | 验证注解的元素值不为空（不为null、去除首位空格后长度为0），不同于@NotEmpty，@NotBlank只应用于字符串且在比较时会去除字符串的空格 |
| @Email                    | 验证注解的元素值是Email，也可以通过正则表达式和flag指定自定义的email格式 |

### 1、验证器示例

#### /dto/(接收参数)

**/UserCreateRequest.java**

```java
package com.example.demo.dto;

import lombok.Data;

import javax.validation.constraints.*;


@Data
//接收用户创建信息
public class UserCreateRequest {
    //在字段上面加一些规则
    //@NotNull//不能为空
    //@NotEmpty//不能为空和字符串
    @NotBlank//不能传空格
    private String username;
    private String password;

    @NotEmpty(message = "邮箱地址不能为空")
    @Email//验证邮箱地址
    private String email;

    @NotNull(message = "年龄不能为空")
    @Max(value = 100,message = "年龄不能大于一百")
    @Min(value = 10,message = "年龄不能小于十")
    private int age;
}
```

#### /entity/(实体类)

```java
package com.example.demo.entity;


import lombok.Builder;
import lombok.Data;

@Data
@Builder
public class User {
    private int id;
    private String username;
    private String password;
}

```



#### /exception/(绑定异常，返回错误信息)

```java
package com.example.demo.exception;

import org.springframework.validation.BindException;
import org.springframework.web.bind.annotation.ControllerAdvice;

import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.ResponseBody;


import java.util.HashMap;
import java.util.Map;

//全局公共异常处理类,接收错误异常
@ControllerAdvice //处理异常
public class CommonExceptionHandler {


    //异常处理程序，指定处理通用错误
    @ExceptionHandler(Throwable.class)
    @ResponseBody//响应数据到前端
    public Map<String, String> exceptionHandler(Throwable e) {
        e.printStackTrace();//错误打印控制台
        Map<String, String> result = new HashMap<>();
        result.put("code", "ERROR");
        result.put("message", e.getMessage());


        result.put("data", null);
        return result;//拿到错误消息并返回给浏览器
    }

    //绑定异常处理程序，指定处理绑定错误
    @ExceptionHandler(BindException.class)
    @ResponseBody//响应数据到前端
    public Map<String, String> exceptionHandler(BindException e) {
        e.printStackTrace();//错误打印控制台
        Map<String, String> result = new HashMap<>();
        result.put("code", "ERROR");
        //向浏览器响应具体错误字段
        result.put("message", e.getBindingResult().getAllErrors().get(0).getDefaultMessage());
        result.put("data", null);
        return result;//拿到错误消息并返回给浏览器
    }
}

```

#### /controller/(控制台)

```java
package com.example.demo.controller;

import com.example.demo.dto.UserCreateRequest;
import com.example.demo.entity.User;
import com.example.demo.interceptor.UserContext;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.validation.Valid;

@RestController
public class UserController {
    //监听路由
    @PostMapping("/api/user/create")
    //将用户传入数据绑定到对象里面，request绑定验证器 ,BindingResult类,绑定错误消息(添加后全局绑定失效)
    public String create(@Valid UserCreateRequest userCreateRequest) {
//        if(bindingResult.hasErrors()){
//            //输出错误消息
//            return bindingResult.getFieldError().getDefaultMessage();
//        }
        System.out.println(userCreateRequest);

        return userCreateRequest.toString();
    }

    @GetMapping("/api/user/whoami")
    public String findToken(String token) {
        //查token  得到一个userId
        User user= UserContext.getUser();
        return user.getUsername();
    }

}

```



### 2、token拦截

#### **/controller/(控制器)**

**TokenController.java（注册登录获取token）**

```java
package com.example.demo.controller;


import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.HashMap;
import java.util.Map;

@RestController
public class TokenController {
    //登录流程
    @PostMapping("/api/token/create")
    public Map<String, String> create(String username, String password) {
        //查username表 ，验证密码，得到userId

        //验证成功 生成一个随机的字符串，存到token表

        Map<String, String> result = new HashMap<>();
        result.put("code", "SUCCESS");
        result.put("message", "获取token成功");
        result.put("data","token123");
        return result;
    }
}
```

**OrderController.java(通过token获取userID)**

```java
package com.example.demo.controller;

import com.example.demo.entity.User;
import com.example.demo.interceptor.UserContext;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class OrderController {
    @GetMapping("/api/order/find")
    public String order(){
        //查用户Id，userId不能在浏览器传
        User user= UserContext.getUser();
        return  user.toString();
    }
}

```

#### /interceptor/（拦截器）

**TokenInterceptor.java(拦截器组件)**

```java
package com.example.demo.interceptor;

import com.example.demo.entity.User;
import org.springframework.stereotype.Component;
import org.springframework.web.servlet.HandlerInterceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

//告诉框架这个是token拦截起的组件
@Component
//创建一个全局拦截的类，实现HandlerInterceptor这个接口
public class TokenInterceptor implements HandlerInterceptor {
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        String token = request.getParameter("token");
        System.out.println("拦截器生效,token:" + token);
        if (token == null) {
            throw new RuntimeException("无token信息");
        }

        //去token表查，得到userId
        User user = User.builder().id(12).build();
        if (user.getId() == 0) {
            //查不 到抛出异常
            throw new RuntimeException("token无效");
        }

        //查到则储存User信息
        user = User.builder().id(1).username("jaAck").build();
        UserContext.setUser(user);
        return true;
    }
}
```

**UserContext.java(线程传输数据)**

```java
package com.example.demo.interceptor;

import com.example.demo.entity.User;

//安全线程存放user信息，线程不安全
public class UserContext {

    //创建一个本地线程存放user信息
    private static final ThreadLocal<User> current = new ThreadLocal<User>();
    public static void setUser(User user) {
        current.set(user);
    }
    public static User getUser(){
        return current.get();
    }
}

```

#### /config/(导入数据)

**WebMvcConfiguration.java(将拦截器注入框架),**

```java
5package com.example.demo.config;

import com.example.demo.interceptor.TokenInterceptor;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

//配置文件导入
@Configuration
public class WebMvcConfiguration implements WebMvcConfigurer {
    //将拦截器注入框架,
    @Autowired
    TokenInterceptor tokenInterceptor;

    public void addInterceptors(InterceptorRegistry registry) {
        InterceptorRegistration interceptorRegistration = registry.addInterceptor(tokenInterceptor);

        //对单独路径生效
        interceptorRegistration.addPathPatterns("/api/**")
                //排除特殊路径
                .excludePathPatterns("/error", "/api/user/create", "/api/token/create");
    }
}
```

## 五、SpringBoot文件上传

**做项目时经常需要上传文件,如电商项目上传图片**

**controller/UploadController**

```java
package com.example.demo.controller;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.multipart.MultipartFile;

import java.io.File;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.UUID;

@RestController
public class UploadController {

    @Value("${upload.path}")
    private  String uploadPath;
    //上面的uploadPath属性的值会由框架自动从配置文件里面 读出upload.path=${user.dir}/uploads/ 并注入到uploadPath属性内
    //控制器会动态的把图片放到uploads目录底下  想要修改存储路径时 可以直接修改配置文件内相应的内容

    //将提交过来的的文件 先取一个文件名 如何new一个file对象
    //通过file里的transferTo 保存到指定文件的绝对地址上去
    @PostMapping("/upload/image")
    public String image(@RequestParam("file") MultipartFile file) throws IOException {
        //判断文件是否上传
        if(file.isEmpty()){
            return  "没有上传文件";
        }

        //获取原始文件名  上传之前的名字(8.jpg(汤姆头像))
        System.out.println(file.getOriginalFilename());

        //从 MultipartFile file 中取到文件拓展名
        int index = file.getOriginalFilename().lastIndexOf(".");

        String extname = file.getOriginalFilename().substring(index + 1).toLowerCase();

        //再uploads内添加子目录管理上传的文件
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy/MM/");

        String subPath = simpleDateFormat.format(new Date());
        String saveName = subPath + UUID.randomUUID().toString().replaceAll("-", "") + "." + extname;

        //判断上传文件是否合法
        String allowImgFormat = "png,jpg,jpeg,gif";
        if (!allowImgFormat.contains(extname)) {
            return "文件类型不被允许";
        }
//        String uploadPath = "uploads/";


        File dir = new File(uploadPath + subPath);

        //如果dir目录不存在 则创建一个
        if (!dir.exists()) {
            dir.mkdirs();
        }


        //文件名需要随机 不能重复 拓展名为.jpg .jpeg .png等
        File save = new File(uploadPath + saveName);

        file.transferTo(save.getAbsoluteFile());

        System.out.println(file);


        //将 savaName 保存到数据库内  注意不要把uploads目录存进去 只需存储动态生成的部分
        return saveName;

        //需要在src/../application.properties配置环境才能在url里访问到上传的图片
    }
}
//前端访问图片  域名再拼接从数据库中获取的2021/11/2e1e16b07a7246efb868319194856aed.jpg信息
// http://localhost:8080/static/uploads/2021/11/2e1e16b07a7246efb868319194856aed.jpg

```

**resources/application.properties**

**配置环境**

```java
#upload file environment

upload.path=${user.dir}/uploads/

#static resource
spring.mvc.static-path-pattern=/static/uploads/**
#find static resource from this dir
spring.web.resources.static-locations=file:${upload.path}

#limit upload file's size
#spring.servlet.multipart.maxFileSize=8MB
```



### 知识点

#### application/json

**application/json 和application/x-www-form-urlencoded的区别**

application/json和application/x-www-form-urlencoded都是表单数据发送时的编码类型。

**EncType：**

enctype 属性规定在发送到服务器之前应该如何对表单数据进行编码。

默认地，表单数据会编码为 "application/x-www-form-urlencoded"。就是说，在发送到服务器之前，所有字符都会进行编码。

如Headers/Request Headers

内的Content-Type：application/x-www-form-urlencoded

**application/x-www-form-urlencoded的编码类型的发送和接收**

窗体数据被编码为名称/值对

客户端:

发送"test= I ' m Jack'",F12,NetWork中查看发送的数据

```
Form Data 
	test: I 'm Jack
```

服务端:

接收test数据

```
echo $_POST["test"]:
```

 **application/json的发送和接收**

序列化后的 JSON 字符串

客户端:

发送JSON格式字符串'{"test":"I'm Client."}'

```
Request Payload
	{test:"I'm Client."}
```

```ABAP
application/json

ajax请求中content-type：application/json代表参数以json字符串传递给后台，controller接收需要@RequestBody 接收参数 例如：@RequestBody Map<String, Object> map，也可以使用类接收@RequestBody User user

application/x-www-form-urlencoded

ajax请求中content-type：application/x-www-form-urlencoded代表参数以键值对传递给后台，controller接收可以单个参数接收，如
@RequestParam("param") String param；也可以用类接收User user，参数名需要一一对应
```



# Java Web开发练习

##  JSP技术

### 搭建jsp开发环境

需要下载服务端软件来运行java web项目

https://www.tomcat.apache.org  下载tomcat 9

创建项目  点击项目名,添加框架支持 Add Frameworks Support

点击Web Application 

项目中多了个web目录

点击web文件夹中的index.jsp文件  

点击在绿色锤子旁的Add Configuration...来配置环境

找到Tomcat Server/Local 并点击

在Server下在Application server出添加tomcat存储路径

切换到部署处 Deployment 点击加号 点击Artifact...

将Application context:处的地址删为 "/" 方便之后以一个根目录的形式访问

完成上述操作后  点击启动键  idea会将tomcat启动 自动打开一个网页(localhost:8080)并显示$END$



在Project Structure/Project Setting/Libraries处将tomcat/lib下的jsp-api.jar和servlet-api.jar两个架包添加到项目中

这就是如何在idea里面把一个普通的jsp项目部署到tomcat里面进行开发测试

### JSP技术

#### **include**

导入其他的jsp文件

```java
<%@  include file="menu.jsp" %>
```

#### **page**

导入包和信息

```java
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```

#### 内置对象

```
共有九个内置对象
常用的五个内置对象
    out          向浏览器输出信息
    request      封装来自浏览器的一些请求信息 如通过http协议带过来的一些信息
    response     响应 给浏览器回复响应
    session      用来做会话保持的 区分不同的用户
    application  所有用户都共享的对象 相当于系统级别的全局变量
```



```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>demo</title>
</head>
<body>
<%@  include file="menu.jsp" %>
<% out.write("hello JSP");%>

<%--五个内置对象
    out          向浏览器输出信息
    request      封装来自浏览器的一些请求信息 如通过http协议带过来的一些信息
    response     响应 给浏览器回复响应
    session      用来做会话保持的 区分不同的用户
    application  所有用户都共享的对象 相当于系统级别的全局变量
--%>

<%
//    可以在页面连接数据库 但是大量的业务逻辑代码使得比较乱 不利于代码的维护  不建议
//    在src目录底下操作
//    String name = request.getParameter("name");
//    System.out.println(name);
//
//    response.getWriter().print(name.toUpperCase());
//    跳转页面
//    response.sendRedirect("login.jsp");
%>
</body>
</html>
```

**不想让浏览器请求的东西可以放在web/WEB-INF内**

例如mysql架包

```ABAP
<%@ page import="com.example.BookService" %>
<%@ page import="com.example.Book" %>
<%@ page import="java.util.List" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>demo</title>
</head>
<body>
<%@  include file="menu.jsp" %>
<% out.write("hello JSP");%>
<%
    BookService bookService = new BookService();
    List<Book> bookList = bookService.findBooks();
%>

<ul>
    <%for (Book book : bookList) {%>
<%--    <li><%out.print(book.getName());%></li>--%>

<%--    jsp表达式  相当与把得到的东西转成字符串--%>
    <li>
        <%=book.getName()%>
    </li>d
    <%}%>
</ul>

</body>
</html>
```

#### session

```java
//在浏览器内存入一个类似与token的session对象 浏览器不共用这个对象 用于识别用户
//session与Cookies的关系
//session需要依赖Cookies里面的SESSIONID
//存取session
session.setAttribute("authUser",user);   //attribute 属性
session.getAttribute("authUser")
session.removeAttribute("authUser");
```

#### 重定向

```java
response.sendRedirect("index.jsp");
```

#### request

```
//获取请求获得的参数
request.getParameter("username");

//获取请求的url地址  如index.jsp
String servletPath = request.getServletPath();
```

## SpringBoot基础

官网 https://spring.io/projects/spring-boot/

快速开始https://start.spring.io

**项目结构**

![image-20211117123202157](C:\Users\LIN\AppData\Roaming\Typora\typora-user-images\image-20211117123202157.png)

### Dependencies

**模板引擎可以在pom.xml文件内修改**

添加依赖Dependencies

>Spring Web    					 web项目需要
>
>MySQL Driver  		 		  MySQL架包
>
>MyBatis Framework   	   简化mysql操作
>
>Lombok							   插件   添加注释 
>
>Thymeleaf   					    模板引擎  加载html
>
>Spring Boot DevTools     开发工具包

使用快速开始或者在IDEA内(`New Project`)创建项目时,选择Spring Initilaizr

### application.properties

**修改默认设置**

**resources\application.properties文件内**

```java
	#修改配置文件
spring.application.name=demo
server.port=8080

    #开发环境
spring.profiles.active=dev

    #mysql连接字符串
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/user(库名)?useUnicode=true&characterEncoding=utf8&useSSL=false&zeroDateTimeBehavior=convertToNull&&serverTimezone=Asia/Shanghai
spring.datasource.username=root
spring.datasource.password=

    #mysql驱动包
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

	# 列名下划线转驼峰
mybatis.configuration.map-underscore-to-camel-case=true

    #控制台打印sql
mybatis.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
```

### **controller**

**控制器**

**MVC  model(数据模型) view(就是templates 模板) controller(控制器)**

**model用法**

**HelloController类**

```java
 model.addAttribute("book", book);
```

```java
package com.example.demo.controller;

import com.example.demo.entity.Book;
import com.example.demo.mapper.BookMapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

import javax.servlet.http.HttpServletRequest;
import java.util.ArrayList;
import java.util.List;

//由控制器(Controller)决定显示哪个模板
@Controller
public class HelloController {

    //让框架帮我们自动注入一个mapper实现的一个对象进来 划红线不用管
    @Autowired
    // @Autowired等价于@Resource
    BookMapper bookMapper;

    //url的映射
    @GetMapping("/")
    public String home(Model model) {

//        model.addAttribute("name","Java编程思想");

//        List <Book> books = new ArrayList<>();
//        books.add(new Book(1,"Java编程思想","100",null));
//        books.add(new Book(2,"计算机原理","90",null));

       
        List<Book> books = bookMapper.findBooks();
        model.addAttribute("bookList", books);
        return "home";         //return的home是templates模板内的html文件
    }

    @GetMapping("/detail")
    public String detail(Model model, HttpServletRequest request) {

        int id = Integer.parseInt(request.getParameter("id"));
        Book book =bookMapper.findBookById(id);
//        Book  book = new Book(id,"example","99",null);

        model.addAttribute("book", book);
        return "detail";
    }
}
//MVC  model(数据模型) view(就是templates 模板) controller(控制器)
```



### DemoApplication

**/com.example.demo/DemoApplication**

**main方法**

```java
package com.example.demo;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

//修改过java类时需要点击绿色的锤子进行重新编译

@SpringBootApplication
@MapperScan("com.example.demo.mapper")  //扫描mapper内容

public class DemoApplication {
    
//	main方法启动SpringBoot框架   框架会去controller包内查找@Controller控制器(内含一个url的映射)
	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

}
```

### templates

>**<html lang="en" xmlns:th="http://www.thymeleaf.org">**
>
>结点内的数据存放在th:text内 直接在标签内写数据会报错
>
>th:each 用于循环
>
>th:href
>
>th:text

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>detail</title>
</head>
<body>
<div th:text="${name}"></div>
    
<!-- 循环输出由model传来的bookList-->
<ul>
    <li th:each="book : ${bookList}">
        <a th:href="@{'/detail?id='+${book.id}}" th:text="${book.name}"></a>
    </li>
</ul>
    
</body>
</html>
```

### 注解

**entity类 实体类** 

##### **lombok注解**

>@Data  			   //getter setter toString hashCode equals
>@Builder   		   //Book book = Book.builder().id(i).name("Java编程思想").build();   可以方便的生成指定参数的对象
>@AllArgsConstructor //全参构造方法
>@NoArgsConstructor	//无参构造方法
>@Slf4j    自动生成该类的 log 静态常量，要打日志就可以直接打，不用再手动 new log 静态常量了
>
>![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213065.png)

 **@NoArgsConstructor, @AllArgsConstructor, @RequiredArgsConstructor**

>**@NoArgsConstructor** : 生成一个没有参数的构造器
>
>**@AllArgsConstructor** : 生成一个包含所有参数的构造器
>
>**@RequiredArgsConstructor** : 生成一个包含 "特定参数" 的构造器，特定参数指的是那些有加上 final 修饰词的变量们
>
>```java
>@RequiredArgsConstructor
>public class User{
>	private final Integer id;
>	private String name;
>}
>//等价于下面的写法
>public class User{
>	private final Integer id;
>	private String name;
>
>	public User(Integer id ){
>		this.id = id;
>	}
>}
>```
>

**@Data** 

```java
@Data
public class User{
	private Integer id;
	private String name;
}
```

**上下等价**

```java
public class User{
	private Integer id;
	private String name;
	
	//@RequiredArgsConstructor
	public User(){
	}
	//@Getter/@Setter
	public void setId (Integer id){
		this.id  =id;
	}
    
    public String GetName(String name){
		return name;
    }
    public void SetName(String name){
		this.name=name;
    }
    
    //@EqualsAndHashCode
    public boolean equals (Object obj){
        if (this == obj) return true;
       	if(obj==null||getClass() !=obj.getClass()) return false;
    	User user =(User) obj;
        return Objects.equals(id,user.id)&&Objects.equals(name,user.name);
    }
    
    public int hashCode (){
        return Objects.hash(id,name);
    }
    
    //@ToString
    public String toString(){
        return "User(id=)"+this.getId()+",name"+this.getName()+")"
    }
	
}
```

 	

整合包，只要加了 @Data 这个注解，等于同时加了以下注解

- @Getter/@Setter
- @ToString
- @EqualsAndHashCode
- @RequiredArgsConstructor

@Data 是使用频率最高的 lombok 注解，通常 @Data 会加在一个值可以被更新的对象上，像是日常使用的 DTO 们、或是 JPA 裡的 Entity 们，就很适合加上 @Data 注解，也就是 @Data for mutable class

 **@Value**

也是整合包，但是他会把所有的变量都设成 final 的，其他的就跟 @Data 一样，等于同时加了以下注解

- @Getter (注意没有setter)
- @ToString
- @EqualsAndHashCode
- @RequiredArgsConstructor

```java
package com.example.demo.entity;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data  			   //getter setter toString hashCode equals
@Build   		   //Book book = Book.builder().id(i).name("Java编程思想").build();   可以方便的生成指定参数的对象
@AllArgsConstructor //全参构造方法
@NoArgsConstructor	//无参构造方法
public class Book {
    private int id;
    private  String name;
    private  String price;
    private String isbn;
}

```

##### **SpringBoot注解**

**1、@SpringBootApplication**

包含@Configuration、@EnableAutoConfiguration、@ComponentScan

通常用在主类上

**2、@Repository**

用于标注数据访问组件，即DAO组件。

**3、@Service**

用于标注业务层组件。

**4、@RestController**

用于标注控制层组件(如struts中的action)，包含@Controller和@ResponseBody

**5、@ResponseBody**

表示该方法的返回结果直接写入HTTP response body中

一般在异步获取数据时使用，在使用@RequestMapping后，返回值通常解析为跳转路径，加上@responsebody后返回结果不会被解析

为跳转路径，而是直接写入HTTP response body中。比如异步获取json数据，加上@responsebody后，会直接返回json数据。

**6、@RequestMapping**

@RequestMapping=@GetMapping +@PostMapping

RequestMapping是一个用来处理请求地址映射的注解，可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径。

**7.@RequestParam**

用在方法的参数前面。

```java
@RequestParam String a =request.getParameter("a");
```

**8.@PathVariable**

路径变量。参数与大括号里的名字一样要相同。

```java
RequestMapping("user/get/mac/{macAddress}")

public String getByMacAddress(@PathVariable String macAddress){
　　//do something;
　　}
```



### Mapper

**用于做数据库与entity之间的映射  把数据库中的记录全部映射到entity内,变成一个一个的对象**

**内含接口  写数据库查询语句 将符合条件的数据 返回**

**id=#{id} 与JDBC的问号占位符区分开**

```java
//mapper 

package com.example.demo.mapper;
//mapper 用于做数据库与entity之间的映射  把数据库中的记录全部映射到entity内,变成一个一个的对象
import com.example.demo.entity.Book;
import org.apache.ibatis.annotations.Param;
import org.apache.ibatis.annotations.Select;
import java.util.List;


//接口时没有具体的方法实现的 写名字就可以了 接口无法被new出来 可以依赖注入
public interface BookMapper {

    @Select("SELECT * FROM book")
    List<Book> findBooks();

    @Select("SELECT * FROM book WHERE id=#{id}")
    Book findBookById(@Param("id") int id);
}
```

## SpringBoot API开发

### RESTful风格API设计

#### @RestController

**返回的东西是用于json数据的**

>相当于@Controller+@ResponseBody两个注解的结合，
>返回json数据不需要在方法前面加@ResponseBody注解了，
>但使用@RestController这个注解，
>就不能返回jsp,html页面，视图解析器无法解析jsp,html页面

**@Constroller**

>在对应的方法上，视图解析器可以解析return 的jsp,html页面，并且跳转到相应页面
>
>若返回json等内容到页面，则需要加@ResponseBody注解

#### 响应JSON

>单个对象
>
>```java
>@GetMapping("/demo/getBook")
>public Book getBook(){
>	Book book = book.add(Book.builder().id(1).name("Java编程思想").build());
>		return book;
>}
>```
>
>集合
>
>```java
>@GetMapping("/demo/getBooks")
>public List<Book> getBooks(){
>	List<Book> books = new ArrayList<Book>;
>
>//调用@Builder中的静态方法  可以去代替生成任意参数的构造方法
>	books.add(Book.builder().id(1).name("Java编程思想").build());
>	books.add(Book.builder().id(2).name("计算机基础").build());
>
>		return books;
>}
>```
>
>状态码和错误信息
>
>在util内新建一个Result来装响应的数据
>
>```java
>package com.example.demo.util;
>
>import lombok.AllArgsConstructor;
>import lombok.Getter;
>
>@Getter
>@AllArgsConstructor
>
>//<T>泛型集合 可以放多种类型数据
>public class Result<T> {
>private String code;
>   private String message;
>   private T data;
>}
>```
>
>**在controller内**
>
>**data为单个对象**
>
>```java
>@GetMapping("/demo/getResult")
>public Result<Book> getResult(){
>Book book =Book.builder().id(1).name("Java编程思想").build();
>
>  Result result = new Result<Book>("SUCCESS",null,book);
>	return result;
>}
>```
>
>**data为一个数组**
>
>```java
>@GetMapping("/demo/getResult2")
>public Result<List<Book>> getResult2(){
>
>	List<Book> books = new ArrayList<Book>;
>
>	//调用@Builder中的静态方法  可以去代替生成任意参数的构造方法
>	books.add(Book.builder().id(1).name("Java编程思想").build());
>	books.add(Book.builder().id(2).name("计算机基础").build());
>
>	Result result = new Result<List<Book>>("SUCCSEE",null,books);
>	return result;
>}
>```

统一响应格式:

{"code":"SUCCSEE","message":null,"data":"数据"}

code 为SUCCESS代表请求成功,data中存放具体的业务数据.

{"code":"ERROR","message":"失败原因","data":null}

#### 接收参数

>Query Params 
>
>application/x-www-form-urlencoded
>
>application/json
>
>URI中的参数

```java
//可以获取get请求中的name  /demo/params?name=jack&page=1&limit=5

@GetMapping("/demo/params")
public String params(HttpServletRequest request){
	System.out.println(request.grtParameter("name"));
	
	return "hi";
}

//上面等价于下面  SpringBoot会自动去get里面找到name 帮我们注入到参数列表内
@GetMapping("/demo/params")
public String params(String name){
	
    System.out.println(name);

	return "hi";
}

//传递多个参数
@GetMapping("/demo/params")
public String params(String name,int page,int limit){
	
    System.out.println(name);
    System.out.println(page);
	System.out.println(limit);
    
	return "hi";
}

//(String name,int page,int limit)
//当传递的参数过多时 写进括号内会比较麻烦
//可以新建一个数据传输对象dto包 用于封装那些参数

//get请求 将传递的参数放在url或者query params内
@GetMapping("/demo/params")
public String params(DemoRequest demoRequest){	
    System.out.println(demoRequest);   // DemoRequest(name=java,page=2,limit=5)
	return "hi";
}

//post请求  传递的参数放在body内
@PostMapping("/demo/paramsPost")
public String paramsPost(DemoRequest demoRequest){	
    System.out.println(demoRequest);   // DemoRequest(name=java,page=2,limit=5)
	return "hi";
}
```

**dto包内新建DemoRequest类**

```java
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class DemoRequest{
	private String name;
	private int page;
	private int limit;
}
```

上面为Application/x-www-form-urlencoded传参

Application/json传参

**选择单选框 raw  右边选择 JSON**

![image-20211116150855110](C:\Users\LIN\AppData\Roaming\Typora\typora-user-images\image-20211116150855110.png)

```java
@PostMapping("/demo/paramsPost2")

//底下的@RequestBody注解 是表示请求内容content-type不是Application/x-www-form-urlencoded

public String paramsPost2(@RequestBody DemoRequest demoRequest){	
    System.out.println(demoRequest);   // DemoRequest(name=java,page=2,limit=5)
	return "hi";
}
```

**通过url内的一部分接收参数**

```java
@PostMapping("/demo/book/{bookId}")
public String paramsPost3(@PathVariable String bookId){	
    System.out.println(bookId);   // 
	return "hi";
}
```

#### 图书管理系统

**目录结构**

![image-20211120104635876](C:\Users\LIN\AppData\Roaming\Typora\typora-user-images\image-20211120104635876.png)

**DemoApplication**

```java
package com.example.demo;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

//修改过java类时需要点击绿色的锤子进行重新编译
@SpringBootApplication
@MapperScan("com.example.demo.mapper")
public class DemoApplication {
//	main方法启动SpringBoot框架   框架会去controller包内查找@Controller控制器(内含一个url的映射)
	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}
}
```

**entity/book对象**

```java
package com.example.demo.entity;
import java.sql.Date;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Builder
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Book {
    private int id;
    private String name;
    private String price;
    private String describe;
    private String isbn;
    private Date createAt;
}
```

记得在util/DemoApplication内写上@MapperScan注解

例如@Mapper

在mapper包内进行mybatis流程操作

**mapper/BookMapper**

```java
package com.example.demo.mapper;
//mapper 用于做数据库与entity之间的映射  把数据库中的记录全部映射到entity内,变成一个一个的对象
import com.example.demo.entity.Book;
import com.example.demo.util.Pagination;
import org.apache.ibatis.annotations.*;

import java.util.List;

//接口时没有具体的方法实现的 写名字就可以了 接口无法被new出来 可以依赖注入
public interface BookMapper {

    //全查
    @Select("SELECT * FROM book2")
    List<Book> findAllBooks();

    //查一本
    @Select("SELECT * FROM book2 WHERE id=#{id}")
    Book findBookById(@Param("id") int id);

    //改
    @Update("UPDATE book2 SET name=#{book.name},isbn=#{book.isbn},price=#{book.price},`describe`=#{book.describe} WHERE id=#{id}")
    int update(@Param("id") int bookId,@Param("book") Book book);

    //增
    @Insert("INSERT INTO book2 (name,`describe`,price,ISBN) VALUE(#{name},#{describe},#{price},#{isbn})")
    @Options(useGeneratedKeys = true,keyProperty = "id")
    void insert(Book book);

    //删
    @Delete("DELETE FROM book2 WHERE id = #{id}")
    int delete(@Param("id") int id);

	//复杂查询
    @ ("<script>"+
            "SELECT * FROM book2 " +
            "<where>"+
            "<if test='book.name !=null'> AND name LIKE CONCAT('%',#{book.name},'%') </if>"+
            "<if test='book.id !=0'>AND id=#{book.id}</if>"+
            "</where>"+
            "ORDER BY id DESC "+
            "LIMIT #{pagination.offset},#{pagination.limit}"+
            "</script>")
    List<Book> findBooks(@Param("book") Book book,@Param("pagination") Pagination pagination);

    //统计条数
    @Select("<script>" +
            "SELECT COUNT(*) FROM book2"+
            "<where>"+
            "<if test='book.name !=null'> AND name LIKE CONCAT('%',#{book.name},'%') </if>"+
            "<if test='book.id !=0'>AND id=#{book.id}</if>"+
            "</where>"+
            "</script>")
    long count (@Param("book") Book book);
}
```

**controller/bookcontroller**

```java
package com.example.demo.controller;

import com.example.demo.entity.Book;
import com.example.demo.mapper.BookMapper;
import com.example.demo.util.JsonResult;
import com.example.demo.util.Pagination;
import org.springframework.web.bind.annotation.*;

import javax.annotation.Resource;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
@CrossOrigin
@RestController
public class BookController {
    @Resource
    BookMapper bookMapper;

    //新增一本课本 已完成
    @PostMapping("/books")
    public JsonResult<Book> createBook(Book book) {
        bookMapper.insert(book);
        return new   JsonResult<Book>(book);
    }

    //删除书本  已完成
    @DeleteMapping("/books/{bookId}")
    public JsonResult deleteBook(@PathVariable(name="bookId") int bookId) {

        int rows = bookMapper.delete(bookId);
        if (rows ==1){
            return new JsonResult("SUCCESS","删除成功");
        }
        return new JsonResult("ERROR","删除失败");
    }

    //查看单书本的内容  已完成
    @GetMapping("/books/{bookId}")
    public JsonResult detail(@PathVariable int bookId) {

        Book book = bookMapper.findBookById(bookId);

        if(book==null){
            return new JsonResult(false,"查找失败");
        }
        return new JsonResult(book);
    }

    //编辑书本信息  (先获取到这本书的详情 再原有内容上进行编辑)  已完成
    @PostMapping("/books/{bookId}")
    public  JsonResult updateBook (@RequestBody Book book,@PathVariable(name="bookId") int bookId){

        //PostMan body row json {"name":"new name","describe":"haha"}

        int rows = bookMapper.update(bookId,book);
        if(rows==1){
            return new JsonResult("SUCCESS","更新成功");
        }
        return  new JsonResult("ERROR","更新失败");
    }

    //复杂查询
    @GetMapping("/books")
    public JsonResult books(String name, Pagination pagination) {
        //用一个对象存放搜索条件
        Book condition = Book.builder()
                .name(name)
                .build();

        //获取符合条件的总记录数，用于分页
        pagination.setTotal(bookMapper.count(condition));

        //分页查询数据
        List<Book> books = bookMapper.findBooks(condition , pagination);

        System.out.println(books);
        //组装JSON需要的格式
        Map<String,Object> data= new HashMap<>();
        data.put("pagination",pagination);
        data.put("books",books);
        return new JsonResult(data);
    }

    //查找所有的书
    @GetMapping("/allBooks")
    public List<Book> books() {
        List<Book> books = bookMapper.findAllBooks();
        System.out.println(books);
        return  books;
    }
}
```

**util/Pagination**

```java
package com.example.demo.util;

import com.fasterxml.jackson.annotation.JsonIgnoreProperties;
import lombok.ToString;

@ToString
@JsonIgnoreProperties(value = {"offset"})
public class Pagination {

    protected int page;
    protected int limit;
    protected long total;

    public Pagination() {
        limit = 5;
        page = 1;
    }

    public Pagination(int page, int limit) {
        setPage(page);
        setLimit(limit);
    }

    public Pagination(int page, int limit,long total) {
        setPage(page);
        setLimit(limit);
        setTotal(total);
    }

    public long getTotal() {
        return total;
    }

    public void setTotal(long total) {
        this.total = total;
    }

    public int getPage() {
        return page;
    }

    public void setPage(int page) {
        this.page = page > 0 ? page : 1;
    }

    public int getOffset() {
        return (page - 1) * limit;
    }

    public void setLimit(int limit) {
        if (limit > 0) {
            this.limit = limit;
        }
    }

    public int getLimit() {
        return limit;
    }
}
```

**jsonresult**

```java
package com.example.demo.util;

import lombok.Data;

@Data
public class JsonResult<T> {
    private String code;
    private String message;
    private T data;

    //默认code为SUCCESS
    public JsonResult() {
        this.code = "SUCCESS";
    }

    //只传如data时 code为SUCCESS
    public JsonResult(T data) {
        this.code = "SUCCESS";
        this.data = data;
    }

    //手动传入SUCCESS||ERROR 和 请求是否成功文字信息
    public JsonResult(String code, String message) {
        this.message = message;
        this.code = code;
    }

    //传入false与true
    public JsonResult(boolean status, String message) {
        this.message = message;
        this.code = status ? "SUCCESS" : "ERROR";
    }
}
```

## 登录注册API

### 添加依赖

在pom.xml处手动导入javax.validation.Valid依赖  或者alt+enter 再右击点搜索依赖向

```java
//导入javax.validation.Valid依赖
<dependency>
    <groupId>javax.validation</groupId>
    <artifactId>validation-api</artifactId>
    <scope>compile</scope>
</dependency>
```

**@Valid无效时** 

```java
<dependency>
    <groupId>jakarta.validation</groupId>
    <artifactId>jakarta.validation-api</artifactId>
    <version>2.0.2</version>
    </dependency>
    	
    <dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.1.1.Final</version>
    <!--<version>7.0.1Final</version>-->
    </dependency>
```



### 验证器

#### 参数校验

| 限制                      | 说明                                                         |
| :------------------------ | :----------------------------------------------------------- |
| @Null                     | 限制只能为null                                               |
| @NotNull                  | 限制必须不为null                                             |
| @AssertFalse              | 限制必须为false                                              |
| @AssertTrue               | 限制必须为true                                               |
| @DecimalMax(value)        | 限制必须为一个不大于指定值的数字                             |
| @DecimalMin(value)        | 限制必须为一个不小于指定值的数字                             |
| @Digits(integer,fraction) | 限制必须为一个小数，且整数部分的位数不能超过integer，小数部分的位数不能超过fraction |
| @Future                   | 限制必须是一个将来的日期                                     |
| @Max(value)               | 限制必须为一个不大于指定值的数字                             |
| @Min(value)               | 限制必须为一个不小于指定值的数字                             |
| @Past                     | 限制必须是一个过去的日期                                     |
| @Pattern(value)           | 限制必须符合指定的正则表达式                                 |
| @Size(max,min)            | 限制字符长度必须在min到max之间                               |
| @Past                     | 验证注解的元素值（日期类型）比当前时间早                     |
| @NotEmpty                 | 验证注解的元素值不为null且不为空（字符串长度不为0、集合大小不为0） |
| @NotBlank                 | 验证注解的元素值不为空（不为null、去除首位空格后长度为0），不同于@NotEmpty，@NotBlank只应用于字符串且在比较时会去除字符串的空格 |
| @Email                    | 验证注解的元素值是Email，也可以通过正则表达式和flag指定自定义的email格式 |

```ABAP
@NotEmpty
The annotated element must not be {@code null} nor empty. Supported types are:
不能是null
不能是空字符
集合框架中的元素不能为空

@NotNul
被修饰元素不能为null,可以为空的字符串

@NotBlank
The annotated element must not be {@code null} and must contain at least one
non-whitespace character.

@Size(min = 6, max = 11, message = "密码长度必须是6-16个字符")
```

```java
package com.example.demo.dto;
import lombok.Data;
import javax.validation.constraints.*;
@Data
public class UserCreateRequest {
//    @NotNull   可以为空的字符串 ""
    @NotEmpty(message="用户名不能为空")
    private  String username;
    private  String password;
    @Email
    private  String email;
    @Max(value = 120,message = "不能超过120")
    @Min(value = 1,message = "不能低于1")
    private  int age;
}
```

#### 错误处理

```
@Valid
数据校验
```

```java
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;
//验证器
import javax.validation.Valid;

@RestController
public class UserController {
    @PostMapping("/api/user/create")
                        //数据校验                                      //校验返回的结果
    public  String create(@Valid UserCreateRequest userCreateRequest, BindingResult bindingResult){

        //获取校验结果
        //绑定信息失败时 获取框架提供的默认错误信息 也可以再相应的注解( @Min(value = 1,message = "不能低于1"))内添加message属性
        if(bindingResult.hasErrors()){
            return  bindingResult.getFieldError().getDefaultMessage();
        }

        System.out.println(userCreateRequest);
        return  "返回成功";
    }
}
```

### 全局异常统一处理

**优化上面的错误处理**

**新建exception包内含一个CommonExceptionHandler**

>```
>@ControllerAdvice
>这个注解意味着这个类是用于错误处理的  控制器内发生异常 程序就会进入这个类
>```
>
>```
>@ExceptionHandler(Throwable.class)
>指定这个类处理的错误类型 Throwable.class是所有错误的基类 顶层类 所有的异常都继承自这个类
>```
>
>```
>@ResponseBody  
>会将底下的map编译成一个json的字符串
>```
>
>```
>@ExceptionHandler(BindException.class)
>参数绑定异常,可以单独处理 org.springframework.validation.BindException  程序先执行绑定异常 后进行全局异常
>e.getBindingResult().getAllErrors().get(0).getDefaultMessage()
>```

```java
package com.example.demo.exception;

import org.springframework.validation.BindException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.ResponseBody;

import java.util.HashMap;
import java.util.Map;

//这个注解意味着这个类是用于错误处理的  控制器内发生异常 程序就会进入这个类
@ControllerAdvice
public class CommonExceptionHandler {
   //指定这个类处理的错误类型 Throwable.class是所有错误的基类 顶层类 所有的异常都继承自这个类
    @ExceptionHandler(Throwable.class)

    //拿到异常结果后返回到前端 因为不是在@RestController 所以需要加这个注解
    @ResponseBody  //会将底下的map编译成一个json的字符串
    public Map<String,String> exceptionHandler(Throwable e){
        e.printStackTrace();
        Map<String,String>  result=new HashMap<String,String>();
        result.put("code","ERROR");
        result.put("message",e.getMessage());
        result.put("data",null);
        return result;
    }

    //参数绑定异常,可以单独处理 org.springframework.validation.BindException  程序先执行绑定异常 后进行全局异常
    @ExceptionHandler(BindException.class)
    @ResponseBody
    public Map<String,String> exceptionHandler(BindException e){
        e.printStackTrace();
        Map<String,String>  result=new HashMap<String,String>();
        result.put("code","ERROR");
        result.put("message",e.getBindingResult().getAllErrors().get(0).getDefaultMessage());
        result.put("data",null);
        return result;
    }
}
```

**controller包下的UserController**

```java
package com.example.demo.controller;

import com.example.demo.dto.UserCreateRequest;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;
//验证器
import javax.validation.Valid;

@RestController
public class UserController {
    @PostMapping("/api/user/create")
    //数据校验
    public  String create(@Valid UserCreateRequest userCreateRequest){
        System.out.println(userCreateRequest);
        return  "返回成功";
    }
}
```

### 拦截器(Token机制)

流程为先建一个拦截类,再配置这个拦截类

#### 拦截器

**interceptor包/TokenInterceptor类**

>@Component  //@Component注解作用是将这个类告诉框架 这是一个token拦截的组件
>全局token拦截器 用于判断token是否存在  需要在config包内注册token
>
>重写了系统HandlerInterceptor接口的方法
>
>通过HttpServletRequest request获取到url中token的值

```java
package com.example.demo.interceptor;

import com.example.demo.entity.User;
import org.springframework.stereotype.Component;
import org.springframework.web.servlet.HandlerInterceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@Component  //@Component注解作用是将这个类告诉框架 这是一个token拦截的组件
//全局token拦截器 用于判断token是否存在  需要在config包内注册token
public class TokenInterceptor implements HandlerInterceptor {
    //下面是重写了系统HandlerInterceptor接口的方法
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

        //可以通过HttpServletRequest request获取到url中token的值

        String token = request.getParameter("token");
        System.out.println(token);

        //去token表查,得到userId

        //RuntimeException 运行时候的异常
        //throw new RuntimeException("token无效");
        User user = User.builder().id(1).username("jack").build();
        return true;
    }
}
```

**controller包/TokenController类**

```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.HashMap;
import java.util.Map;

@RestController
public class TokenController {

    @PostMapping("/api/token/create")
    public Map<String ,String> create(String username,String password){

        // 查 user表 验证密码,得到userId

        //验证成功 生成一个随机的字符串,存到token表内
        Map<String,String>  result=new HashMap<String,String>();
        result.put("code","SUCCESS");
        result.put("message",null);
        result.put("data","token");

        return result;
    }
}
```

#### 配置文件

config包/WebMvcConfiguration接口

```java
package com.example.demo.config;

import com.example.demo.interceptor.TokenInterceptor;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

//Mvc配置文件 实现一个WebMvc配置文件的接口
@Configuration  //  这个WebMvcConfiguration类是配置文件 需要加@Configuration注解
public class WebMvcConfiguration implements WebMvcConfigurer {

//    把写好的拦截器TokenInterceptor 注入进来 并加入到框架内 registry.addInterceptor(tokenInterceptor)
    @Autowired
    TokenInterceptor tokenInterceptor;
//    输入add选择Interceptors自动生成拦截器
    public void addInterceptors(InterceptorRegistry registry){
        InterceptorRegistration interceptorRegistration=registry.addInterceptor(tokenInterceptor);
        //以下路径通通需要经过这个拦截器过滤 **代表所有
          interceptorRegistration.addPathPatterns("/api/**")
                //排除掉 错误信息 用户创建 token生成
                .excludePathPatterns("/error", "/api/user/create", "/api/token/create");
    }
}
```

#### entity/User

```java
package com.example.demo.entity;

import lombok.Builder;
import lombok.Data;

@Data
@Builder
public class User {
    private  int id;
    private  String username;
    private  String password;
}
```

### 线程安全传递数据

**interceptor包/UserContext**

```java
package com.example.demo.interceptor;

import com.example.demo.entity.User;

//这个类用于存放用户登录登录后的消息
public class UserContext {
    public static User current;  //static 静态变量线程不安全 ,再所有的线程共享数据

    public  static  void setUser(User user){
        current = user;
    }

    public  static User  getUser(){
        return  current;
    }
}
//上面的线程不安全 需要改造成线程安全的静态变量  下面是改造后的
//-------------------------------------分界线------------------------------------//

package com.example.demo.interceptor;
import com.example.demo.entity.User;
//这个类用于存放用户登录登录后的消息
public class UserContext {
    public static final ThreadLocal<User> current=new ThreadLocal<>();

    public  static  void setUser(User user){
        current.set(user);
    }

    public  static User  getUser(){
        return  current.get();
    }
}
```

```ABAP
　　ThreadLocal简介
　　多线程访问同一个共享变量的时候容易出现并发问题，特别是多个线程对一个变量进行写入的时候，为了保证线程安全，一般使用者在访问共享变量的时候需要进行额外的同步措施才能保证线程安全性。ThreadLocal是除了加锁这种同步方式之外的一种保证一种规避多线程访问出现线程不安全的方法，当我们在创建一个变量后，如果每个线程对其进行访问的时候访问的都是线程自己的变量这样就不会存在线程不安全问题。

　　ThreadLocal是JDK包提供的，它提供线程本地变量，如果创建一乐ThreadLocal变量，那么访问这个变量的每个线程都会有这个变量的一个副本，在实际多线程操作的时候，操作的是自己本地内存中的变量，从而规避了线程安全问题，如下图所示
```

## SpringBoot文件上传

**做项目时经常需要上传文件,如电商项目上传图片**

**controller/UploadController**

```java
package com.example.demo.controller;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.multipart.MultipartFile;

import java.io.File;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.UUID;

@RestController
public class UploadController {

    @Value("${upload.path}")
    private  String uploadPath;
    //上面的uploadPath属性的值会由框架自动从配置文件里面 读出upload.path=${user.dir}/uploads/ 并注入到uploadPath属性内
    //控制器会动态的把图片放到uploads目录底下  想要修改存储路径时 可以直接修改配置文件内相应的内容

    //将提交过来的的文件 先取一个文件名 如何new一个file对象
    //通过file里的transferTo 保存到指定文件的绝对地址上去
    @PostMapping("/upload/image")
    public String image(@RequestParam("file") MultipartFile file) throws IOException {
        //判断文件是否上传
        if(file.isEmpty()){
            return  "没有上传文件";
        }

        //获取原始文件名  上传之前的名字(8.jpg(汤姆头像))
        System.out.println(file.getOriginalFilename());

        //从 MultipartFile file 中取到文件拓展名
        int index = file.getOriginalFilename().lastIndexOf(".");

        String extname = file.getOriginalFilename().substring(index + 1).toLowerCase();

        //再uploads内添加子目录管理上传的文件
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy/MM/");

        String subPath = simpleDateFormat.format(new Date());
        String saveName = subPath + UUID.randomUUID().toString().replaceAll("-", "") + "." + extname;

        //判断上传文件是否合法
        String allowImgFormat = "png,jpg,jpeg,gif";
        if (!allowImgFormat.contains(extname)) {
            return "文件类型不被允许";
        }
//        String uploadPath = "uploads/";


        File dir = new File(uploadPath + subPath);

        //如果dir目录不存在 则创建一个
        if (!dir.exists()) {
            dir.mkdirs();
        }


        //文件名需要随机 不能重复 拓展名为.jpg .jpeg .png等
        File save = new File(uploadPath + saveName);

        file.transferTo(save.getAbsoluteFile());

        System.out.println(file);


        //将 savaName 保存到数据库内  注意不要把uploads目录存进去 只需存储动态生成的部分
        return saveName;

        //需要在src/../application.properties配置环境才能在url里访问到上传的图片
    }
}
//前端访问图片  域名再拼接从数据库中获取的2021/11/2e1e16b07a7246efb868319194856aed.jpg信息
// http://localhost:8080/static/uploads/2021/11/2e1e16b07a7246efb868319194856aed.jpg

```

**resources/application.properties**

**配置环境**

```java
#upload file environment

upload.path=${user.dir}/uploads/

#static resource
spring.mvc.static-path-pattern=/static/uploads/**
#find static resource from this dir
spring.web.resources.static-locations=file:${upload.path}

#limit upload file's size
#spring.servlet.multipart.maxFileSize=8MB
```



## 知识点

### application/json

**application/json 和application/x-www-form-urlencoded的区别**

application/json和application/x-www-form-urlencoded都是表单数据发送时的编码类型。

**EncType：**

enctype 属性规定在发送到服务器之前应该如何对表单数据进行编码。

默认地，表单数据会编码为 "application/x-www-form-urlencoded"。就是说，在发送到服务器之前，所有字符都会进行编码。

如Headers/Request Headers

内的Content-Type：application/x-www-form-urlencoded

**application/x-www-form-urlencoded的编码类型的发送和接收**

窗体数据被编码为名称/值对

客户端:

发送"test= I ' m Jack'",F12,NetWork中查看发送的数据

```
Form Data 
	test: I 'm Jack
```

服务端:

接收test数据

```
echo $_POST["test"]:
```

 **application/json的发送和接收**

序列化后的 JSON 字符串

客户端:

发送JSON格式字符串'{"test":"I'm Client."}'

```
Request Payload
	{test:"I'm Client."}
```

```ABAP
application/json

ajax请求中content-type：application/json代表参数以json字符串传递给后台，controller接收需要@RequestBody 接收参数 例如：@RequestBody Map<String, Object> map，也可以使用类接收@RequestBody User user

application/x-www-form-urlencoded

ajax请求中content-type：application/x-www-form-urlencoded代表参数以键值对传递给后台，controller接收可以单个参数接收，如@RequestParam("param") String param；也可以用类接收User user，参数名需要一一对应
```





# Java网络编程

## 一、java中的IO流

### 1、什么是IO？

>   即输入和输出(Input/Output) 简称IO

什么是流? 即 (Stream) ， Java 中将数据的输入输出抽象为流，流是一组有顺序的，单向的，有起点和终点的数据集合，就像水流。

#### 输入流 `InputStream` 

此抽象类是表示字节输入流的所有类的超类。

需要定义 `InputStream` 子类的应用程序必须总是提供返回下一个输入字节的方法。

 

| ***\*方法摘要\**** |                                                              |
| ------------------ | ------------------------------------------------------------ |
| int                | **[available](#available())**()      返回此输入流下一个方法调用可以不受阻塞地从此输入流读取（或跳过）的估计字节数。 |
| void               | **[close](#close())**()      关闭此输入流并释放与该流关联的所有系统资源。 |
| void               | **[mark](#mark(int))**(int readlimit)      在此输入流中标记当前的位置。 |
| boolean            | **[markSupported](#markSupported())**()      测试此输入流是否支持 mark 和 reset 方法。 |
| abstract  int      | **[read](#read())**()      从输入流中读取数据的下一个字节。  |
| int                | **[read](#read(byte[]))**(byte[] b)      从输入流中读取一定数量的字节，并将其存储在缓冲区数组 b 中。 |
| int                | **[read](#read(byte[], int, int))**(byte[] b, int off, int len)      将输入流中最多 len 个数据字节读入 byte 数组。 |
| void               | **[reset](#reset())**()      将此流重新定位到最后一次对此输入流调用 mark 方法时的位置。 |
| long               | **[skip](#skip(long))**(long n)      跳过和丢弃此输入流中数据的 n 个字节。 |

 

#### 输出流 `OutputStream`


此抽象类是表示输出字节流的所有类的超类。输出流接受输出字节并将这些字节发送到某个接收器。

需要定义 `OutputStream` 子类的应用程序必须始终提供至少一种可写入一个输出字节的方法。

| void           | **[close](#close())**()      关闭此输出流并释放与此流有关的所有系统资源。 |
| -------------- | ------------------------------------------------------------ |
| void           | **[flush](#flush())**()      刷新此输出流并强制写出所有缓冲的输出字节。 |
| void           | **[write](#write(byte[]))**(byte[] b)      将 b.length 个字节从指定的 byte 数组写入此输出流。 |
| void           | **[write](#write(byte[], int, int))**(byte[] b, int off, int len)      将指定 byte 数组中从偏移量 off 开始的 len 个字节写入此输出流。 |
| abstract  void | **[write](#write(int))**(int b)      将指定的字节写入此输出流。 |

 	



我们可以从一个**输入流**中，读取数据`read()`，也可以向一个**输出流**，写入数据`write()`。

IO流相关的类，在`java.io`包中，请到Java SDK文档中，找到相关类 http://www.daimaku.net/book/javasdk/

接下来，我们创建创建一个叫做 hello.txt的文件，文件内容为字符串ab并保存：

![img](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/110-Java%25E7%25BD%2591%25E7%25BB%259C%25E7%25BC%2596%25E7%25A8%258B%25E7%25AC%2594%25E8%25AE%25B0/30340e77c72acdd75816eb25d01916f3.png!l)

预览

通过File对象，实例化一个 `FileInputStream` 文件输入流：

```javascript
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;

public class Demo {
    public static void main(String[] args) throws IOException {

        File file = new File("hello.txt");  // Java中，使用File类，来表示文件或目录
      
        FileInputStream stream = new FileInputStream(file);

        System.out.println(stream.read());   // 97
        System.out.println(stream.read());   // 98
        System.out.println(stream.read());   // -1
        System.out.println(stream.read());   // -1
      
    }
}
```

第一次读取，得到一个97，就是hello.txt文件中的第一个字符`a`对应的ASCII码，接下来读到得到98是`b`的ASCII码。当读到文件末尾，就会返回 `-1`

### 2、File类

>   File是Java中对文件或目录的抽象，提供了很多文件相关操作的方法：

-   exists()                 	boolean      测试此抽象路径名表示的文件或目录是否存在。

-   delete()				    boolean      删除此抽象路径名表示的文件或目录。

-   isDirectory()            boolean      测试此抽象路径名表示的文件是否是一个目录。
-   length()                    long             返回由此抽象路径名表示的文件的长度。
-   listFiles()                  File[]            返回一个抽象路径名数组，这些路径名表示此抽象路径名表示的目录中的文件
-   mkdir()                    boolean       创建此抽象路径名指定的目录。
-   renameTo()            boolean       重新命名此抽象路径名表示的文件。

 

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[File](#File(java.io.File, java.lang.String))**([File](http://www.daimaku.net/book/javasdk/java/io/File.html) parent, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) child)      根据 parent 抽象路径名和 child 路径名字符串创建一个新 File 实例。 |      |
| **[File](#File(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) pathname)      通过将给定路径名字符串转换为抽象路径名来创建一个新 File 实例。 |      |
| **[File](#File(java.lang.String, java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) parent, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) child)      根据 parent 路径名字符串和 child 路径名字符串创建一个新 File 实例。 |      |
| **[File](#File(java.net.URI))**([URI](http://www.daimaku.net/book/javasdk/java/net/URI.html) uri)      通过将给定的 file: URI 转换为一个抽象路径名来创建一个新的 File 实例。 |      |

 

| 方法摘                                                       |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| boolean                                                      | **[canExecute](#canExecute())**()      测试应用程序是否可以执行此抽象路径名表示的文件。 |
| boolean                                                      | **[canRead](#canRead())**()      测试应用程序是否可以读取此抽象路径名表示的文件。 |
| boolean                                                      | **[canWrite](#canWrite())**()      测试应用程序是否可以修改此抽象路径名表示的文件。 |
| int                                                          | **[compareTo](#compareTo(java.io.File))**([File](http://www.daimaku.net/book/javasdk/java/io/File.html) pathname)      按字母顺序比较两个抽象路径名。 |
| boolean                                                      | **[createNewFile](#createNewFile())**()      当且仅当不存在具有此抽象路径名指定名称的文件时，不可分地创建一个新的空文件。 |
| static [File](http://www.daimaku.net/book/javasdk/java/io/File.html) | **[createTempFile](#createTempFile(java.lang.String, java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) prefix, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) suffix)      在默认临时文件目录中创建一个空文件，使用给定前缀和后缀生成其名称。 |
| static [File](http://www.daimaku.net/book/javasdk/java/io/File.html) | **[createTempFile](#createTempFile(java.lang.String, java.lang.String, java.io.File))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) prefix, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) suffix, [File](http://www.daimaku.net/book/javasdk/java/io/File.html) directory)       在指定目录中创建一个新的空文件，使用给定的前缀和后缀字符串生成其名称。 |
| boolean                                                      | **[delete](#delete())**()      删除此抽象路径名表示的文件或目录。 |
| void                                                         | **[deleteOnExit](#deleteOnExit())**()      在虚拟机终止时，请求删除此抽象路径名表示的文件或目录。 |
| boolean                                                      | **[equals](#equals(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      测试此抽象路径名与给定对象是否相等。 |
| boolean                                                      | **[exists](#exists())**()      测试此抽象路径名表示的文件或目录是否存在。 |
| [File](http://www.daimaku.net/book/javasdk/java/io/File.html) | **[getAbsoluteFile](#getAbsoluteFile())**()      返回此抽象路径名的绝对路径名形式。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getAbsolutePath](#getAbsolutePath())**()      返回此抽象路径名的绝对路径名字符串。 |
| [File](http://www.daimaku.net/book/javasdk/java/io/File.html) | **[getCanonicalFile](#getCanonicalFile())**()      返回此抽象路径名的规范形式。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getCanonicalPath](#getCanonicalPath())**()      返回此抽象路径名的规范路径名字符串。 |
| long                                                         | **[getFreeSpace](#getFreeSpace())**()      返回此抽象路径名[指定的](#partName)分区中未分配的字节数。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getName](#getName())**()      返回由此抽象路径名表示的文件或目录的名称。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getParent](#getParent())**()      返回此抽象路径名父目录的路径名字符串；如果此路径名没有指定父目录，则返回 null。 |
| [File](http://www.daimaku.net/book/javasdk/java/io/File.html) | **[getParentFile](#getParentFile())**()      返回此抽象路径名父目录的抽象路径名；如果此路径名没有指定父目录，则返回 null。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getPath](#getPath())**()      将此抽象路径名转换为一个路径名字符串。 |
| long                                                         | **[getTotalSpace](#getTotalSpace())**()      返回此抽象路径名[指定的](#partName)分区大小。 |
| long                                                         | **[getUsableSpace](#getUsableSpace())**()      返回此抽象路径名[指定的](#partName)分区上可用于此虚拟机的字节数。 |
| int                                                          | **[hashCode](#hashCode())**()      计算此抽象路径名的哈希码。 |
| boolean                                                      | **[isAbsolute](#isAbsolute())**()      测试此抽象路径名是否为绝对路径名。 |
| boolean                                                      | **[isDirectory](#isDirectory())**()      测试此抽象路径名表示的文件是否是一个目录。 |
| boolean                                                      | **[isFile](#isFile())**()      测试此抽象路径名表示的文件是否是一个标准文件。 |
| boolean                                                      | **[isHidden](#isHidden())**()      测试此抽象路径名指定的文件是否是一个隐藏文件。 |
| long                                                         | **[lastModified](#lastModified())**()      返回此抽象路径名表示的文件最后一次被修改的时间。 |
| long                                                         | **[length](#length())**()      返回由此抽象路径名表示的文件的长度。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html)[] | **[list](#list())**()      返回一个字符串数组，这些字符串指定此抽象路径名表示的目录中的文件和目录。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html)[] | **[list](#list(java.io.FilenameFilter))**([FilenameFilter](http://www.daimaku.net/book/javasdk/java/io/FilenameFilter.html) filter)      返回一个字符串数组，这些字符串指定此抽象路径名表示的目录中满足指定过滤器的文件和目录。 |
| [File](http://www.daimaku.net/book/javasdk/java/io/File.html)[] | **[listFiles](#listFiles())**()      返回一个抽象路径名数组，这些路径名表示此抽象路径名表示的目录中的文件。 |
| [File](http://www.daimaku.net/book/javasdk/java/io/File.html)[] | **[listFiles](#listFiles(java.io.FileFilter))**([FileFilter](http://www.daimaku.net/book/javasdk/java/io/FileFilter.html) filter)      返回抽象路径名数组，这些路径名表示此抽象路径名表示的目录中满足指定过滤器的文件和目录。 |
| [File](http://www.daimaku.net/book/javasdk/java/io/File.html)[] | **[listFiles](#listFiles(java.io.FilenameFilter))**([FilenameFilter](http://www.daimaku.net/book/javasdk/java/io/FilenameFilter.html) filter)      返回抽象路径名数组，这些路径名表示此抽象路径名表示的目录中满足指定过滤器的文件和目录。 |
| static [File](http://www.daimaku.net/book/javasdk/java/io/File.html)[] | **[listRoots](#listRoots())**()      列出可用的文件系统根。  |
| boolean                                                      | **[mkdir](#mkdir())**()      创建此抽象路径名指定的目录。    |
| boolean                                                      | **[mkdirs](#mkdirs())**()      创建此抽象路径名指定的目录，包括所有必需但不存在的父目录。 |
| boolean                                                      | **[renameTo](#renameTo(java.io.File))**([File](http://www.daimaku.net/book/javasdk/java/io/File.html) dest)      重新命名此抽象路径名表示的文件。 |
| boolean                                                      | **[setExecutable](#setExecutable(boolean))**(boolean executable)      设置此抽象路径名所有者执行权限的一个便捷方法。 |
| boolean                                                      | **[setExecutable](#setExecutable(boolean, boolean))**(boolean executable, boolean ownerOnly)      设置此抽象路径名的所有者或所有用户的执行权限。 |
| boolean                                                      | **[setLastModified](#setLastModified(long))**(long time)      设置此抽象路径名指定的文件或目录的最后一次修改时间。 |
| boolean                                                      | **[setReadable](#setReadable(boolean))**(boolean readable)      设置此抽象路径名所有者读权限的一个便捷方法。 |
| boolean                                                      | **[setReadable](#setReadable(boolean, boolean))**(boolean readable, boolean ownerOnly)      设置此抽象路径名的所有者或所有用户的读权限。 |
| boolean                                                      | **[setReadOnly](#setReadOnly())**()      标记此抽象路径名指定的文件或目录，从而只能对其进行读操作。 |
| boolean                                                      | **[setWritable](#setWritable(boolean))**(boolean writable)      设置此抽象路径名所有者写权限的一个便捷方法。 |
| boolean                                                      | **[setWritable](#setWritable(boolean, boolean))**(boolean writable, boolean ownerOnly)      设置此抽象路径名的所有者或所有用户的写权限。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toString](#toString())**()      返回此抽象路径名的路径名字符串。 |
| [URI](http://www.daimaku.net/book/javasdk/java/net/URI.html) | **[toURI](#toURI())**()      构造一个表示此抽象路径名的 file: URI。 |
| [URL](http://www.daimaku.net/book/javasdk/java/net/URL.html) | **[toURL](#toURL())**()      ***\*已过时。\**** **此方法不会自动转义 URL 中的非法字符。建议新的代码使用以下方式将抽象路径名转换为 URL：首先通过** *[toURI](#toURI())* 方法将其转换为 URI，然后通过 *[URI.toURL](#toURL())* 方法将 URI 装换为 URL。 |

 

### 3、 向文件写入字符

>    向`hello.txt`文件中，写入字符`Hello World`

```javascript
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

public class Demo {
    public static void main(String[] args) throws IOException {

        File file = new File("hello.txt");
        FileOutputStream stream = new FileOutputStream(file);
        stream.write("Hello World".getBytes());
    }
}
```

去实验一下

重 做

刚才我们练习的，都是字节流，以字节为最小单位进行操作。除了字节流，Java还提供了字符流，用于操作纯文本文件。

-   字节流：以 8 位（即 1 byte，8 bit）作为一个数据单元，数据流中最小的数据单元是字节
-   字符流：以 16 位（即 1 char，2 byte，16 bit）作为一个数据单元，数据流中最小的数据单元是字符， Java 中的字符是 Unicode 编码，一个字符占用两个字节

Java流类图结构：

![img](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/110-Java%25E7%25BD%2591%25E7%25BB%259C%25E7%25BC%2596%25E7%25A8%258B%25E7%25AC%2594%25E8%25AE%25B0/59de4715fdd960fe9a34a9ad0616c874.jpg!l)

### **4、字节流**

注意：**字符流只能处理纯文本数据，字节流可以处理二进制文件，例如图片音乐等文件**

>   主要用到以下几个类，请先到Java SDK手册中查阅相关类

##### InputStreamReader

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[InputStreamReader](#InputStreamReader(java.io.InputStream))**([InputStream](http://www.daimaku.net/book/javasdk/java/io/InputStream.html) in)      创建一个使用默认字符集的 InputStreamReader。 |      |
| **[InputStreamReader](#InputStreamReader(java.io.InputStream, java.nio.charset.Charset))**([InputStream](http://www.daimaku.net/book/javasdk/java/io/InputStream.html) in, [Charset](http://www.daimaku.net/book/javasdk/java/nio/charset/Charset.html) cs)      创建使用给定字符集的 InputStreamReader。 |      |
| **[InputStreamReader](#InputStreamReader(java.io.InputStream, java.nio.charset.CharsetDecoder))**([InputStream](http://www.daimaku.net/book/javasdk/java/io/InputStream.html) in, [CharsetDecoder](http://www.daimaku.net/book/javasdk/java/nio/charset/CharsetDecoder.html) dec)      创建使用给定字符集解码器的 InputStreamReader。 |      |
| **[InputStreamReader](#InputStreamReader(java.io.InputStream, java.lang.String))**([InputStream](http://www.daimaku.net/book/javasdk/java/io/InputStream.html) in, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) charsetName)      创建使用指定字符集的 InputStreamReader。 |      |

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| void                                                         | **[close](#close())**()      关闭该流并释放与之关联的所有资源。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getEncoding](#getEncoding())**()      返回此流使用的字符编码的名称。 |
| int                                                          | **[read](#read())**()      读取单个字符。                    |
| int                                                          | **[read](#read(char[], int, int))**(char[] cbuf, int offset, int length)      将字符读入数组中的某一部分。 |
| boolean                                                      | **[ready](#ready())**()      判断此流是否已经准备好用于读取。 |

#####  OutputStream

| ***\*方法摘要\**** |                                                              |
| ------------------ | ------------------------------------------------------------ |
| void               | **[close](#close())**()      关闭此输出流并释放与此流有关的所有系统资源。 |
| void               | **[flush](#flush())**()      刷新此输出流并强制写出所有缓冲的输出字节。 |
| void               | **[write](#write(byte[]))**(byte[] b)      将 b.length 个字节从指定的 byte 数组写入此输出流。 |
| void               | **[write](#write(byte[], int, int))**(byte[] b, int off, int len)      将指定 byte 数组中从偏移量 off 开始的 len 个字节写入此输出流。 |
| abstract  void     | **[write](#write(int))**(int b)      将指定的字节写入此输出流。 |

  

##### BufferedReader

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[BufferedReader](#BufferedReader(java.io.Reader))**([Reader](http://www.daimaku.net/book/javasdk/java/io/Reader.html) in)      创建一个使用默认大小输入缓冲区的缓冲字符输入流。 |      |
| **[BufferedReader](#BufferedReader(java.io.Reader, int))**([Reader](http://www.daimaku.net/book/javasdk/java/io/Reader.html) in, int sz)      创建一个使用指定大小输入缓冲区的缓冲字符输入流。 |      |

 	

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| void                                                         | **[close](#close())**()      关闭该流并释放与之关联的所有资源。 |
| void                                                         | **[mark](#mark(int))**(int readAheadLimit)      标记流中的当前位置。 |
| boolean                                                      | **[markSupported](#markSupported())**()      判断此流是否支持 mark() 操作（它一定支持）。 |
| int                                                          | **[read](#read())**()      读取单个字符。                    |
| int                                                          | **[read](#read(char[], int, int))**(char[] cbuf, int off, int len)      将字符读入数组的某一部分。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[readLine](#readLine())**()      读取一个文本行。          |
| boolean                                                      | **[ready](#ready())**()      判断此流是否已准备好被读取。    |
| void                                                         | **[reset](#reset())**()      将流重置到最新的标记。          |
| long                                                         | **[skip](#skip(long))**(long n)      跳过字符。              |

#####  处理二进制文件

然后编写如下代码：

```javascript
import java.io.*;

public class Demo {
    public static void main(String[] args) throws IOException {

        File file = new File("hello.txt");

      	// 文件输入流(字节流)
        FileInputStream inputStream = new FileInputStream(file);

        // 转换为字符流，可以按字符读取
        InputStreamReader reader = new InputStreamReader(inputStream);

        // 转为带缓冲的Reader
        BufferedReader bufferedReader = new BufferedReader(reader);

        // 可以方便的从缓冲区，一次读取一行数据
        System.out.println(bufferedReader.readLine());

    }
}
```

注意：**字符流只能处理纯文本数据，字节流可以处理二进制文件，例如图片音乐等文件**

### 5、文件流

##### 文件输入流

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[FileInputStream](#FileInputStream(java.io.File))**([File](http://www.daimaku.net/book/javasdk/java/io/File.html) file)      通过打开一个到实际文件的连接来创建一个 FileInputStream，该文件通过文件系统中的 File 对象 file 指定。 |      |
| **[FileInputStream](#FileInputStream(java.io.FileDescriptor))**([FileDescriptor](http://www.daimaku.net/book/javasdk/java/io/FileDescriptor.html) fdObj)      通过使用文件描述符 fdObj 创建一个 FileInputStream，该文件描述符表示到文件系统中某个实际文件的现有连接。 |      |
| **[FileInputStream](#FileInputStream(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) name)      通过打开一个到实际文件的连接来创建一个 FileInputStream，该文件通过文件系统中的路径名 name 指定。 |      |

 

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| int                                                          | **[available](#available())**()      返回下一次对此输入流调用的方法可以不受阻塞地从此输入流读取（或跳过）的估计剩余字节数。 |
| void                                                         | **[close](#close())**()      关闭此文件输入流并释放与此流有关的所有系统资源。 |
| protected  void                                              | **[finalize](#finalize())**()      确保在不再引用文件输入流时调用其 close 方法。 |
| [FileChannel](http://www.daimaku.net/book/javasdk/java/nio/channels/FileChannel.html) | **[getChannel](#getChannel())**()      返回与此文件输入流有关的唯一 [FileChannel](http://www.daimaku.net/book/javasdk/java/nio/channels/FileChannel.html) 对象。 |
| [FileDescriptor](http://www.daimaku.net/book/javasdk/java/io/FileDescriptor.html) | **[getFD](#getFD())**()      返回表示到文件系统中实际文件的连接的 FileDescriptor 对象，该文件系统正被此 FileInputStream 使用。 |
| int                                                          | **[read](#read())**()      从此输入流中读取一个数据字节。    |
| int                                                          | **[read](#read(byte[]))**(byte[] b)      从此输入流中将最多 b.length 个字节的数据读入一个 byte 数组中。 |
| int                                                          | **[read](#read(byte[], int, int))**(byte[] b, int off, int len)      从此输入流中将最多 len 个字节的数据读入一个 byte 数组中。 |
| long                                                         | **[skip](#skip(long))**(long n)      从输入流中跳过并丢弃 n 个字节的数据。 |

#####  文件输出流

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[FileOutputStream](#FileOutputStream(java.io.File))**([File](http://www.daimaku.net/book/javasdk/java/io/File.html) file)      创建一个向指定 File 对象表示的文件中写入数据的文件输出流。 |      |
| **[FileOutputStream](#FileOutputStream(java.io.File, boolean))**([File](http://www.daimaku.net/book/javasdk/java/io/File.html) file, boolean append)      创建一个向指定 File 对象表示的文件中写入数据的文件输出流。 |      |
| **[FileOutputStream](#FileOutputStream(java.io.FileDescriptor))**([FileDescriptor](http://www.daimaku.net/book/javasdk/java/io/FileDescriptor.html) fdObj)      创建一个向指定文件描述符处写入数据的输出文件流，该文件描述符表示一个到文件系统中的某个实际文件的现有连接。 |      |
| **[FileOutputStream](#FileOutputStream(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) name)      创建一个向具有指定名称的文件中写入数据的输出文件流。 |      |
| **[FileOutputStream](#FileOutputStream(java.lang.String, boolean))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) name, boolean append)      创建一个向具有指定 name 的文件中写入数据的输出文件流。 |      |

 

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| void                                                         | **[close](#close())**()      关闭此文件输出流并释放与此流有关的所有系统资源。 |
| protected  void                                              | **[finalize](#finalize())**()      清理到文件的连接，并确保在不再引用此文件输出流时调用此流的 close 方法。 |
| [FileChannel](http://www.daimaku.net/book/javasdk/java/nio/channels/FileChannel.html) | **[getChannel](#getChannel())**()      返回与此文件输出流有关的唯一 [FileChannel](http://www.daimaku.net/book/javasdk/java/nio/channels/FileChannel.html) 对象。 |
| [FileDescriptor](http://www.daimaku.net/book/javasdk/java/io/FileDescriptor.html) | **[getFD](#getFD())**()      返回与此流有关的文件描述符。    |
| void                                                         | **[write](#write(byte[]))**(byte[] b)      将 b.length 个字节从指定 byte 数组写入此文件输出流中。 |
| void                                                         | **[write](#write(byte[], int, int))**(byte[] b, int off, int len)      将指定 byte 数组中从偏移量 off 开始的 len 个字节写入此文件输出流。 |
| void                                                         | **[write](#write(int))**(int b)      将指定字节写入此文件输出流。 |

 

 

## 二、Java网络编程基础

Java语言提供了java.net包，用于网络编程，请到Java SDK文档中，找到如下类：

#### URL 类，代表一个统一资源定位符，例如一个网址

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[URL](#URL(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) spec)      根据 String 表示形式创建 URL 对象。 |      |
| **[URL](#URL(java.lang.String, java.lang.String, int, java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) protocol, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) host, int port, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) file)      根据指定 protocol、host、port 号和 file 创建 URL 对象。 |      |
| **[URL](#URL(java.lang.String, java.lang.String, int, java.lang.String, java.net.URLStreamHandler))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) protocol, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) host, int port, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) file, [URLStreamHandler](http://www.daimaku.net/book/javasdk/java/net/URLStreamHandler.html) handler)      根据指定的 protocol、host、port 号、file 和 handler 创建 URL 对象。 |      |
| **[URL](#URL(java.lang.String, java.lang.String, java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) protocol, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) host, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) file)      根据指定的 protocol 名称、host 名称和 file 名称创建 URL。 |      |
| **[URL](#URL(java.net.URL, java.lang.String))**([URL](http://www.daimaku.net/book/javasdk/java/net/URL.html) context, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) spec)      通过在指定的上下文中对给定的 spec 进行解析创建 URL。 |      |
| **[URL](#URL(java.net.URL, java.lang.String, java.net.URLStreamHandler))**([URL](http://www.daimaku.net/book/javasdk/java/net/URL.html) context, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) spec, [URLStreamHandler](http://www.daimaku.net/book/javasdk/java/net/URLStreamHandler.html) handler)      通过在指定的上下文中用指定的处理程序对给定的 spec 进行解析来创建 URL。 |      |

 

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| boolean                                                      | **[equals](#equals(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) obj)      比较此 URL 是否等于另一个对象。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getAuthority](#getAuthority())**()      获取此 URL 的授权部分。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[getContent](#getContent())**()      获取此 URL 的内容。   |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[getContent](#getContent(java.lang.Class[]))**([Class](http://www.daimaku.net/book/javasdk/java/lang/Class.html)[] classes)      获取此 URL 的内容。 |
| int                                                          | **[getDefaultPort](#getDefaultPort())**()      获取与此 URL 关联协议的默认端口号。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getFile](#getFile())**()      获取此 URL 的文件名。       |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getHost](#getHost())**()      获取此 URL 的主机名（如果适用）。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getPath](#getPath())**()      获取此 URL 的路径部分。     |
| int                                                          | **[getPort](#getPort())**()      获取此 URL 的端口号。       |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getProtocol](#getProtocol())**()      获取此 URL 的协议名称。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getQuery](#getQuery())**()      获取此 URL 的查询部分。   |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getRef](#getRef())**()      获取此 URL 的锚点（也称为“引用”）。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getUserInfo](#getUserInfo())**()      获取此 URL 的 userInfo 部分。 |
| int                                                          | **[hashCode](#hashCode())**()      创建一个适合哈希表索引的整数。 |
| [URLConnection](http://www.daimaku.net/book/javasdk/java/net/URLConnection.html) | **[openConnection](#openConnection())**()      返回一个 URLConnection 对象，它表示到 URL 所引用的远程对象的连接。 |
| [URLConnection](http://www.daimaku.net/book/javasdk/java/net/URLConnection.html) | **[openConnection](#openConnection(java.net.Proxy))**([Proxy](http://www.daimaku.net/book/javasdk/java/net/Proxy.html) proxy)      与 openConnection() 类似，所不同是连接通过指定的代理建立；不支持代理方式的协议处理程序将忽略该代理参数并建立正常的连接。 |
| [InputStream](http://www.daimaku.net/book/javasdk/java/io/InputStream.html) | **[openStream](#openStream())**()      打开到此 URL 的连接并返回一个用于从该连接读入的 InputStream。 |
| boolean                                                      | **[sameFile](#sameFile(java.net.URL))**([URL](http://www.daimaku.net/book/javasdk/java/net/URL.html) other)      比较两个 URL，不包括片段部分。 |
| protected  void                                              | **[set](#set(java.lang.String, java.lang.String, int, java.lang.String, java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) protocol, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) host, int port, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) file, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) ref)      设置 URL 的字段。 |
| protected  void                                              | **[set](#set(java.lang.String, java.lang.String, int, java.lang.String, java.lang.String, java.lang.String, java.lang.String, java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) protocol, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) host, int port, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) authority, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) userInfo, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) path, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) query, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) ref)      设置 URL 的指定的 8 个字段。 |
| static void                                                  | **[setURLStreamHandlerFactory](#setURLStreamHandlerFactory(java.net.URLStreamHandlerFactory))**([URLStreamHandlerFactory](http://www.daimaku.net/book/javasdk/java/net/URLStreamHandlerFactory.html) fac)      设置应用程序的 URLStreamHandlerFactory。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toExternalForm](#toExternalForm())**()      构造此 URL 的字符串表示形式。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[toString](#toString())**()      构造此 URL 的字符串表示形式。 |
| [URI](http://www.daimaku.net/book/javasdk/java/net/URI.html) | **[toURI](#toURI())**()      返回与此 URL 等效的 [URI](http://www.daimaku.net/book/javasdk/java/net/URI.html)。 |



http://www.daimaku.net/book/javasdk/

重 做

接下来，我们使用Java，连接到 `playground.it266.com` 的服务器，并读取数据，输出到控制台

```javascript
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class Demo {
    public static void main(String[] args) throws IOException {

        // 统一资源定位符对象
        URL url = new URL("http://playground.it266.com/news");

        // 打开一个连接对象，强转成httpURLConnection类
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();

        // 设置请求方法为 GET
        conn.setRequestMethod("GET");

        // 通过连接对象，获取一个输入流
        InputStream inputStream = conn.getInputStream();

        // 将输入流转为 BufferedReader对象，以字符行的方式读据数据
        BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream, "UTF-8"));

        // 循环读取数据
        while (true) {

            String row = reader.readLine();

            if (row == null) {  // 没有数据了
                break;
            }

            System.out.println(row);

        }


        // 关闭相关资源
        reader.close();
        inputStream.close();
        conn.disconnect();

    }
}
```

去实验一下吧

重 做

如果我们需要以POST方式，进行HTTP请求，使用如下方式：

```javascript
import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;

public class Demo {
    public static void main(String[] args) throws IOException {

        // 统一资源定位符对象
        URL url = new URL("http://playground.it266.com/login");

        // 打开一个连接对象，强转成httpURLConnection类
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();

        // 设置请求方法为 POST
        conn.setRequestMethod("POST");

        // 需要向流中写入数据时，设置为true
        conn.setDoOutput(true);

        // 设置Content-Type
        conn.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");

        OutputStream outputStream = conn.getOutputStream();

        // 需要发送的数据
        String data = "username=jack&password=jack123";

        outputStream.write(data.getBytes());

        // 服务端返回的HTTP状态码
        System.out.println(conn.getResponseCode());

        // 通过连接对象，获取一个输入流
        InputStream inputStream = conn.getInputStream();

        // 将输入流转为 BufferedReader对象，以字符行的方式读据数据
        BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream, "UTF-8"));

        // 循环读取数据
        while (true) {

            String row = reader.readLine();

            if (row == null) {  // 没有数据了
                break;
            }

            System.out.println(row);

        }

        // 关闭相关资源
        outputStream.close();
        reader.close();
        inputStream.close();
        conn.disconnect();
    }
}
```

#### HttpURLConnection 发起HTTP连接

| ***\*字段摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| protected  int                                               | **[chunkLength](#chunkLength)**      使用存储块编码流模式进行输出时的存储块长度。 |
| protected  int                                               | **[fixedContentLength](#fixedContentLength)**      使用固定长度流模式时的固定内容长度。 |
| static int                                                   | **[HTTP_ACCEPTED](#HTTP_ACCEPTED)**      HTTP 状态码 202：Accepted。 |
| static int                                                   | **[HTTP_BAD_GATEWAY](#HTTP_BAD_GATEWAY)**      HTTP 状态码 502：Bad Gateway。 |
| static int                                                   | **[HTTP_BAD_METHOD](#HTTP_BAD_METHOD)**      HTTP 状态码 405：Method Not Allowed。 |
| static int                                                   | **[HTTP_BAD_REQUEST](#HTTP_BAD_REQUEST)**      HTTP 状态码 400：Bad Request。 |
| static int                                                   | **[HTTP_CLIENT_TIMEOUT](#HTTP_CLIENT_TIMEOUT)**      HTTP 状态码 408：Request Time-Out。 |
| static int                                                   | **[HTTP_CONFLICT](#HTTP_CONFLICT)**      HTTP 状态码 409：Conflict。 |
| static int                                                   | **[HTTP_CREATED](#HTTP_CREATED)**      HTTP 状态码 201：Created。 |
| static int                                                   | **[HTTP_ENTITY_TOO_LARGE](#HTTP_ENTITY_TOO_LARGE)**      HTTP 状态码 413：Request Entity Too Large。 |
| static int                                                   | **[HTTP_FORBIDDEN](#HTTP_FORBIDDEN)**      HTTP 状态码 403：Forbidden。 |
| static int                                                   | **[HTTP_GATEWAY_TIMEOUT](#HTTP_GATEWAY_TIMEOUT)**      HTTP 状态码 504：Gateway Timeout。 |
| static int                                                   | **[HTTP_GONE](#HTTP_GONE)**      HTTP 状态码 410：Gone。     |
| static int                                                   | **[HTTP_INTERNAL_ERROR](#HTTP_INTERNAL_ERROR)**      HTTP 状态码 500：Internal Server Error。 |
| static int                                                   | **[HTTP_LENGTH_REQUIRED](#HTTP_LENGTH_REQUIRED)**      HTTP 状态码 411：Length Required。 |
| static int                                                   | **[HTTP_MOVED_PERM](#HTTP_MOVED_PERM)**      HTTP 状态码 301：Moved Permanently。 |
| static int                                                   | **[HTTP_MOVED_TEMP](#HTTP_MOVED_TEMP)**      HTTP 状态码 302：Temporary Redirect。 |
| static int                                                   | **[HTTP_MULT_CHOICE](#HTTP_MULT_CHOICE)**      HTTP 状态码 300：Multiple Choices。 |
| static int                                                   | **[HTTP_NO_CONTENT](#HTTP_NO_CONTENT)**      HTTP 状态码 204：No Content。 |
| static int                                                   | **[HTTP_NOT_ACCEPTABLE](#HTTP_NOT_ACCEPTABLE)**      HTTP 状态码 406：Not Acceptable。 |
| static int                                                   | **[HTTP_NOT_AUTHORITATIVE](#HTTP_NOT_AUTHORITATIVE)**      HTTP 状态码 203：Non-Authoritative Information。 |
| static int                                                   | **[HTTP_NOT_FOUND](#HTTP_NOT_FOUND)**      HTTP 状态码 404：Not Found。 |
| static int                                                   | **[HTTP_NOT_IMPLEMENTED](#HTTP_NOT_IMPLEMENTED)**      HTTP 状态码 501：Not Implemented。 |
| static int                                                   | **[HTTP_NOT_MODIFIED](#HTTP_NOT_MODIFIED)**      HTTP 状态码 304：Not Modified。 |
| static int                                                   | **[HTTP_OK](#HTTP_OK)**      HTTP 状态码 200：OK。           |
| static int                                                   | **[HTTP_PARTIAL](#HTTP_PARTIAL)**      HTTP 状态码 206：Partial Content。 |
| static int                                                   | **[HTTP_PAYMENT_REQUIRED](#HTTP_PAYMENT_REQUIRED)**      HTTP 状态码 402：Payment Required。 |
| static int                                                   | **[HTTP_PRECON_FAILED](#HTTP_PRECON_FAILED)**      HTTP 状态码 412：Precondition Failed。 |
| static int                                                   | **[HTTP_PROXY_AUTH](#HTTP_PROXY_AUTH)**      HTTP 状态码 407：Proxy Authentication Required。 |
| static int                                                   | **[HTTP_REQ_TOO_LONG](#HTTP_REQ_TOO_LONG)**      HTTP 状态码 414：Request-URI Too Large。 |
| static int                                                   | **[HTTP_RESET](#HTTP_RESET)**      HTTP 状态码 205：Reset Content。 |
| static int                                                   | **[HTTP_SEE_OTHER](#HTTP_SEE_OTHER)**      HTTP 状态码 303：See Other。 |
| static int                                                   | **[HTTP_SERVER_ERROR](#HTTP_SERVER_ERROR)**      ***\*已过时。\**** **放错了位置，它不应该存在。** |
| static int                                                   | **[HTTP_UNAUTHORIZED](#HTTP_UNAUTHORIZED)**      HTTP 状态码 401：Unauthorized。 |
| static int                                                   | **[HTTP_UNAVAILABLE](#HTTP_UNAVAILABLE)**      HTTP 状态码 503：Service Unavailable。 |
| static int                                                   | **[HTTP_UNSUPPORTED_TYPE](#HTTP_UNSUPPORTED_TYPE)**      HTTP 状态码 415：Unsupported Media Type。 |
| static int                                                   | **[HTTP_USE_PROXY](#HTTP_USE_PROXY)**      HTTP 状态码 305：Use Proxy。 |
| static int                                                   | **[HTTP_VERSION](#HTTP_VERSION)**      HTTP 状态码 505：HTTP Version Not Supported。 |
| protected  boolean                                           | **[instanceFollowRedirects](#instanceFollowRedirects)**      如果为 true，则协议自动执行重定向。 |
| protected  [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[method](#method)**      HTTP 方法（GET、POST、PUT 等）。  |
| protected  int                                               | **[responseCode](#responseCode)**      表示三位字数的 HTTP 状态码 (Status-Code) 的 int。 |
| protected  [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[responseMessage](#responseMessage)**      HTTP 响应消息。 |

 

| ***\*从类 java.net.\******[URLConnection](http://www.daimaku.net/book/javasdk/java/net/URLConnection.html)** 继承的字段 |
| ------------------------------------------------------------ |
| [allowUserInteraction](#allowUserInteraction), [connected](#connected), [doInput](#doInput), [doOutput](#doOutput), [ifModifiedSince](#ifModifiedSince), [url](#url), [useCaches](#useCaches) |

 

| ***\*构造方法摘要\**** |                                                              |
| ---------------------- | ------------------------------------------------------------ |
| protected              | **[HttpURLConnection](#HttpURLConnection(java.net.URL))**([URL](http://www.daimaku.net/book/javasdk/java/net/URL.html) u)      HttpURLConnection 的构造方法。 |

 

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| abstract  void                                               | **[disconnect](#disconnect())**()      指示近期服务器不太可能有其他请求。 |
| [InputStream](http://www.daimaku.net/book/javasdk/java/io/InputStream.html) | **[getErrorStream](#getErrorStream())**()      如果连接失败但服务器仍然发送了有用数据，则返回错误流。 |
| static boolean                                               | **[getFollowRedirects](#getFollowRedirects())**()      返回指示是否应该自动执行 HTTP 重定向 (3xx) 的 boolean 值。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getHeaderField](#getHeaderField(int))**(int n)      返回 nth 头字段的值。 |
| long                                                         | **[getHeaderFieldDate](#getHeaderFieldDate(java.lang.String, long))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) name, long Default)      返回解析为日期的指定字段的值。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getHeaderFieldKey](#getHeaderFieldKey(int))**(int n)      返回 nth 头字段的键。 |
| boolean                                                      | **[getInstanceFollowRedirects](#getInstanceFollowRedirects())**()      返回此 HttpURLConnection 的 instanceFollowRedirects 字段的值。 |
| [Permission](http://www.daimaku.net/book/javasdk/java/security/Permission.html) | **[getPermission](#getPermission())**()      返回一个权限对象，其代表建立此对象表示的连接所需的权限。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getRequestMethod](#getRequestMethod())**()      获取请求方法。 |
| int                                                          | **[getResponseCode](#getResponseCode())**()      从 HTTP 响应消息获取状态码。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getResponseMessage](#getResponseMessage())**()      获取与来自服务器的响应代码一起返回的 HTTP 响应消息（如果有）。 |
| void                                                         | **[setChunkedStreamingMode](#setChunkedStreamingMode(int))**(int chunklen)      此方法用于在预先***\*不\****知道内容长度时启用没有进行内部缓冲的 HTTP 请求正文的流。 |
| void                                                         | **[setFixedLengthStreamingMode](#setFixedLengthStreamingMode(int))**(int contentLength)      此方法用于在预先已知内容长度时启用没有进行内部缓冲的 HTTP 请求正文的流。 |
| static void                                                  | **[setFollowRedirects](#setFollowRedirects(boolean))**(boolean set)      设置此类是否应该自动执行 HTTP 重定向（响应代码为 3xx 的请求）。 |
| void                                                         | **[setInstanceFollowRedirects](#setInstanceFollowRedirects(boolean))**(boolean followRedirects)      设置此 HttpURLConnection 实例是否应该自动执行 HTTP 重定向（响应代码为 3xx 的请求）。 |
| void                                                         | **[setRequestMethod](#setRequestMethod(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) method)      设置 URL 请求的方法， GET POST HEAD OPTIONS PUT DELETE TRACE 以上方法之一是合法的，具体取决于协议的限制。 |
| abstract  boolean                                            | **[usingProxy](#usingProxy())**()      指示连接是否通过代理。 |

 

## 三、GUI编程基础

### gui基础

什么是GUI? 图形用户界面（Graphical User Interface，简称GUI，又称图形用户接口）。Java语言提供了一个叫做Swing的工具包，用于GUI编程

学习GUI编程，先来认识一下窗体 (JFrame)，下图就是一个窗体，通常有标题、还有最大化、最小化、关闭按扭

![img](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/110-Java%25E7%25BD%2591%25E7%25BB%259C%25E7%25BC%2596%25E7%25A8%258B%25E7%25AC%2594%25E8%25AE%25B0/f0bf3b750b2ee735f00bba66f65053df.png!l)

预览

一个JFrame对象，就是一个窗体，代码如下：

```javascript
import javax.swing.*;

public class Hello {
    public static void main(String[] args) {
      
        JFrame frame = new JFrame();
        frame.setTitle("Hello");       // 设置标题
        frame.setSize(300, 200);       // 设置宽高
        frame.setVisible(true);        // 窗体默认不显示，需要设置visible属性为true，才会显示
    }
}
```

关闭按扭默认行为是隐藏窗体，并不是销毁窗体，如果我们希望点关闭按扭时销毁窗体，需要将关闭按扭的默认行为设置为`销毁`，代码如下：

```javascript
// 关闭按扭的默认行为设置为销毁窗口
frame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);

// 如果我们希望在在窗口关闭时，得到通知：
frame.addWindowListener(new WindowAdapter() {
    public void windowClosed(WindowEvent e) {
        System.out.println(" 窗口关闭");
    }
});

// 如果希望点击窗口时退出整个应用程序，可以使用：
// frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```

去实验一下

重 做

接下来学习按扭(JButton)的使用，按扭是我们常用的组件，下面我们创建一个按扭，并添加到窗体中：

```javascript
import javax.swing.*;

public class Hello {
    public static void main(String[] args) {
        JFrame frame = new JFrame();
        frame.setTitle("Hello");
        frame.setSize(300, 200);

        frame.setLayout(null);                // 取消窗体的默认布局

        JButton button = new JButton("点我");
        button.setBounds(80, 80, 60, 30);     // x, y, width, height
      
        button.addActionListener(event -> {   // 点击事件
            System.out.println("被点了");
        });
      
        frame.add(button);                    // 将按扭添加到窗体中

        frame.setVisible(true);               // 放在最后面，组件都添加完成之后，才显示主窗体
    }
}
```

窗体属于容器组件，有自己的默认布局管理器，在这个示例中，我们需要手动管理组件的位置，所以设置为layout属性为null

去实验一下吧

重 做 

常用组件，还有标签(JLabel)和文本域(JTextField)

```javascript
JLabel label1 = new JLabel("姓名");
label1.setBounds(20, 20, 60, 30);
frame.add(label1);

JTextField field1 = new JTextField(20);
field1.setBounds(80, 20, 200, 30);
frame.add(field1);
```

获取文本域中，用户输入的内容，可以用 `field1.getText()`

请在按扭的点击事件中，获取用户输入的内容

重 做

对话框组件，也是我们常用的：

```javascript
int res = JOptionPane.showConfirmDialog(frame, "确定要删除吗？", "删除提示", 0);
```

更多组件参考Java API 文档` javax.swing` http://www.daimaku.net/book/javasdk

### gui登录练习

```java
package com.example.demo.gui;

import javax.swing.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class Hello {
    //设置主窗口的宽高
    public static int frameWidth=400;
    public static int frameHeight=500;



    public static void main(String[] args) {
        JFrame frame = new JFrame();
        frame.setTitle("Hello");
        frame.setSize(frameWidth, frameHeight);



        // 关闭按扭的默认行为设置为销毁窗口
        frame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);

        // 如果我们希望在在窗口关闭时，得到通知：
        frame.addWindowListener(new WindowAdapter() {
            public void windowClosed(WindowEvent e) {
                System.out.println(" 窗口关闭");
            }
        });

        // 如果希望点击窗口时退出整个应用程序，可以使用：
        // frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)

        frame.setLayout(null);                // 取消窗体的默认布局

        JButton button = new JButton("点我登录");
        int buttonWitch=200;
        int buttonHeight=50;
        button.setBounds((frameWidth-buttonWitch)/2, frameHeight-frameWidth/2, buttonWitch, buttonHeight);     // x, y, width, height

        frame.add(button);                    // 将按扭添加到窗体中


        int fieldWidth=frameWidth*3/5;
        int fieldHeight=fieldWidth/5;

        int labelWidth=frameWidth/5;
        int labelX=25;
        int labelY=60;
        int space=100;

        //账号输入框
        JLabel label1 = new JLabel("用户名:");
        label1.setBounds(labelX, labelY, labelWidth, fieldHeight);
        frame.add(label1);


        JTextField field1 = new JTextField(20);
        field1.setBounds(labelX+labelY, labelY, fieldWidth, fieldHeight);
        frame.add(field1);
        String info1 = "";
        field1.setText(info1);
        //密码输入框
        JLabel label2 = new JLabel("密码:");
        label2.setBounds(labelX, labelY+space, labelWidth, fieldHeight);
        frame.add(label2);


        JTextField field2 = new JTextField(20);
        field2.setBounds(labelX+labelY, labelY+space, fieldWidth, fieldHeight);
        frame.add(field2);
        String info2 = "";
        field2.setText(info2);
/////////////////////////////////////////////////////
        button.addActionListener(event -> {   // 点击事件
            System.out.println("被点了");
            if(field1.getText().length()==0||field2.getText().length()==0){
                int res = JOptionPane.showConfirmDialog(frame, "未输入用户名或密码", "登录提示", 0);
            }else {
                int res = JOptionPane.showConfirmDialog(frame, "登陆成功", "登录提示", 0);
            }
        });

        frame.setVisible(true);               // 放在最后面，组件都添加完成之后，才显示主窗体
    }
}
```



### 常用类

#### JComboBox：下拉列表组件

>   将按钮或可编辑字段与下拉列表组合的组件。用户可以从下拉列表中选择值，下拉列表在用户请求时显示。如果使组合框处于可编辑状态，则组合框将包括用户可在其中键入值的可编辑字段。

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[JComboBox](#JComboBox())**()      创建具有默认数据模型的 JComboBox。 |      |
| **[JComboBox](#JComboBox(javax.swing.ComboBoxModel))**([ComboBoxModel](http://www.daimaku.net/book/javasdk/javax/swing/ComboBoxModel.html) aModel)      创建一个 JComboBox，其项取自现有的 ComboBoxModel。 |      |
| **[JComboBox](#JComboBox(java.lang.Object[]))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html)[] items)      创建包含指定数组中的元素的 JComboBox。 |      |
| **[JComboBox](#JComboBox(java.util.Vector))**([Vector](http://www.daimaku.net/book/javasdk/java/util/Vector.html)<?> items)      创建包含指定 Vector 中的元素的 JComboBox。 |      |

 

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| void                                                         | **[actionPerformed](#actionPerformed(java.awt.event.ActionEvent))**([ActionEvent](http://www.daimaku.net/book/javasdk/java/awt/event/ActionEvent.html) e)      此方法由于实现的副作用而存在的公共方法。 |
| protected  void                                              | **[actionPropertyChanged](#actionPropertyChanged(javax.swing.Action, java.lang.String))**([Action](http://www.daimaku.net/book/javasdk/javax/swing/Action.html) action, [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) propertyName)      更新组合框的状态以响应关联动作中的属性更改。 |
| void                                                         | **[addActionListener](#addActionListener(java.awt.event.ActionListener))**([ActionListener](http://www.daimaku.net/book/javasdk/java/awt/event/ActionListener.html) l)      添加 ActionListener。 |
| void                                                         | **[addItem](#addItem(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) anObject)      为项列表添加项。 |
| void                                                         | **[addItemListener](#addItemListener(java.awt.event.ItemListener))**([ItemListener](http://www.daimaku.net/book/javasdk/java/awt/event/ItemListener.html) aListener)      添加 ItemListener。 |
| void                                                         | **[addPopupMenuListener](#addPopupMenuListener(javax.swing.event.PopupMenuListener))**([PopupMenuListener](http://www.daimaku.net/book/javasdk/javax/swing/event/PopupMenuListener.html) l)      添加 PopupMenu 侦听器，该侦听器将侦听取自组合框弹出部分的通知消息。 |
| void                                                         | **[configureEditor](#configureEditor(javax.swing.ComboBoxEditor, java.lang.Object))**([ComboBoxEditor](http://www.daimaku.net/book/javasdk/javax/swing/ComboBoxEditor.html) anEditor, [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) anItem)      利用指定项初始化编辑器。 |
| protected  void                                              | **[configurePropertiesFromAction](#configurePropertiesFromAction(javax.swing.Action))**([Action](http://www.daimaku.net/book/javasdk/javax/swing/Action.html) a)      在此组合框上设置属性以匹配指定 Action 中的属性。 |
| void                                                         | **[contentsChanged](#contentsChanged(javax.swing.event.ListDataEvent))**([ListDataEvent](http://www.daimaku.net/book/javasdk/javax/swing/event/ListDataEvent.html) e)      此方法作为实现的副作用存在的公共方法。 |
| protected  [PropertyChangeListener](http://www.daimaku.net/book/javasdk/java/beans/PropertyChangeListener.html) | **[createActionPropertyChangeListener](#createActionPropertyChangeListener(javax.swing.Action))**([Action](http://www.daimaku.net/book/javasdk/javax/swing/Action.html) a)      创建并返回一个 PropertyChangeListener，它负责侦听指定 Action 的更改并更新适当属性。 |
| protected  [JComboBox.KeySelectionManager](http://www.daimaku.net/book/javasdk/javax/swing/JComboBox.KeySelectionManager.html) | **[createDefaultKeySelectionManager](#createDefaultKeySelectionManager())**()      返回默认键选择管理器的实例。 |
| protected  void                                              | **[fireActionEvent](#fireActionEvent())**()      通知所有需要此事件类型的通知的已注册侦听器。 |
| protected  void                                              | **[fireItemStateChanged](#fireItemStateChanged(java.awt.event.ItemEvent))**([ItemEvent](http://www.daimaku.net/book/javasdk/java/awt/event/ItemEvent.html) e)      通知所有需要此事件类型的通知的已注册侦听器。 |
| void                                                         | **[firePopupMenuCanceled](#firePopupMenuCanceled())**()      通知 PopupMenuListener 组合框的弹出部分已被取消。 |
| void                                                         | **[firePopupMenuWillBecomeInvisible](#firePopupMenuWillBecomeInvisible())**()      通知 PopupMenuListener 组合框的弹出部分已变得不可见。 |
| void                                                         | **[firePopupMenuWillBecomeVisible](#firePopupMenuWillBecomeVisible())**()      通知 PopupMenuListener 组合框的弹出部分将变得可见。 |
| [AccessibleContext](http://www.daimaku.net/book/javasdk/javax/accessibility/AccessibleContext.html) | **[getAccessibleContext](#getAccessibleContext())**()      获取与此 JComboBox 关联的 AccessibleContext。 |
| [Action](http://www.daimaku.net/book/javasdk/javax/swing/Action.html) | **[getAction](#getAction())**()      返回此 ActionEvent 源当前设置的 Action，如果没有设置任何 Action，则返回 null。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getActionCommand](#getActionCommand())**()      返回发送到动作侦听器的事件中包括的动作命令。 |
| [ActionListener](http://www.daimaku.net/book/javasdk/java/awt/event/ActionListener.html)[] | **[getActionListeners](#getActionListeners())**()      返回使用 addActionListener() 添加到此 JComboBox 的所有 ActionListener 组成的数组。 |
| [ComboBoxEditor](http://www.daimaku.net/book/javasdk/javax/swing/ComboBoxEditor.html) | **[getEditor](#getEditor())**()      返回用于绘制和编辑 JComboBox 字段中所选项的编辑器。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[getItemAt](#getItemAt(int))**(int index)      返回指定索引处的列表项。 |
| int                                                          | **[getItemCount](#getItemCount())**()      返回列表中的项数。 |
| [ItemListener](http://www.daimaku.net/book/javasdk/java/awt/event/ItemListener.html)[] | **[getItemListeners](#getItemListeners())**()      返回使用 addItemListener() 添加到此 JComboBox 中的所有 ItemListener 组成的数组。 |
| [JComboBox.KeySelectionManager](http://www.daimaku.net/book/javasdk/javax/swing/JComboBox.KeySelectionManager.html) | **[getKeySelectionManager](#getKeySelectionManager())**()      返回列表的键选择管理器。 |
| int                                                          | **[getMaximumRowCount](#getMaximumRowCount())**()      返回组合框不使用滚动条可以显示的最大项数 |
| [ComboBoxModel](http://www.daimaku.net/book/javasdk/javax/swing/ComboBoxModel.html) | **[getModel](#getModel())**()      返回 JComboBox 当前使用的数据模型。 |
| [PopupMenuListener](http://www.daimaku.net/book/javasdk/javax/swing/event/PopupMenuListener.html)[] | **[getPopupMenuListeners](#getPopupMenuListeners())**()      返回利用 addPopupMenuListener() 添加到此 JComboBox 的所有 PopupMenuListener 组成的数组。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[getPrototypeDisplayValue](#getPrototypeDisplayValue())**()      返回“原型显示”值，即用于计算显示高度和宽度的 Object。 |
| [ListCellRenderer](http://www.daimaku.net/book/javasdk/javax/swing/ListCellRenderer.html) | **[getRenderer](#getRenderer())**()      返回用于显示 JComboBox 字段中所选项的渲染器。 |
| int                                                          | **[getSelectedIndex](#getSelectedIndex())**()      返回列表中与给定项匹配的第一个选项。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[getSelectedItem](#getSelectedItem())**()      返回当前所选项。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html)[] | **[getSelectedObjects](#getSelectedObjects())**()      返回包含所选项的数组。 |
| [ComboBoxUI](http://www.daimaku.net/book/javasdk/javax/swing/plaf/ComboBoxUI.html) | **[getUI](#getUI())**()      返回呈现此组件的 L&F 对象。     |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getUIClassID](#getUIClassID())**()      返回呈现此组件的 L&F 类的名称。 |
| void                                                         | **[hidePopup](#hidePopup())**()      促使组合框关闭其弹出窗口。 |
| void                                                         | **[insertItemAt](#insertItemAt(java.lang.Object, int))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) anObject, int index)      在项列表中的给定索引处插入项。 |
| protected  void                                              | **[installAncestorListener](#installAncestorListener())**()  |
| void                                                         | **[intervalAdded](#intervalAdded(javax.swing.event.ListDataEvent))**([ListDataEvent](http://www.daimaku.net/book/javasdk/javax/swing/event/ListDataEvent.html) e)      此方法作为实现的副作用存在的公共方法。 |
| void                                                         | **[intervalRemoved](#intervalRemoved(javax.swing.event.ListDataEvent))**([ListDataEvent](http://www.daimaku.net/book/javasdk/javax/swing/event/ListDataEvent.html) e)      此方法作为实现的副作用存在的公共方法。 |
| boolean                                                      | **[isEditable](#isEditable())**()      如果 JComboBox 可编辑，则返回 true。 |
| boolean                                                      | **[isLightWeightPopupEnabled](#isLightWeightPopupEnabled())**()      获取 lightWeightPopupEnabled 属性的值。 |
| boolean                                                      | **[isPopupVisible](#isPopupVisible())**()      确定弹出窗口的可见性。 |
| protected  [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[paramString](#paramString())**()      返回此 JComboBox 的字符串表示形式。 |
| void                                                         | **[processKeyEvent](#processKeyEvent(java.awt.event.KeyEvent))**([KeyEvent](http://www.daimaku.net/book/javasdk/java/awt/event/KeyEvent.html) e)      处理 KeyEvent，查找 Tab 键。 |
| void                                                         | **[removeActionListener](#removeActionListener(java.awt.event.ActionListener))**([ActionListener](http://www.daimaku.net/book/javasdk/java/awt/event/ActionListener.html) l)      移除 ActionListener。 |
| void                                                         | **[removeAllItems](#removeAllItems())**()      从项列表中移除所有项。 |
| void                                                         | **[removeItem](#removeItem(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) anObject)      从项列表中移除项。 |
| void                                                         | **[removeItemAt](#removeItemAt(int))**(int anIndex)      移除 anIndex 处的项。 |
| void                                                         | **[removeItemListener](#removeItemListener(java.awt.event.ItemListener))**([ItemListener](http://www.daimaku.net/book/javasdk/java/awt/event/ItemListener.html) aListener)      移除 ItemListener。 |
| void                                                         | **[removePopupMenuListener](#removePopupMenuListener(javax.swing.event.PopupMenuListener))**([PopupMenuListener](http://www.daimaku.net/book/javasdk/javax/swing/event/PopupMenuListener.html) l)      移除 PopupMenuListener。 |
| protected  void                                              | **[selectedItemChanged](#selectedItemChanged())**()      此受保护方法是特定于实现的。 |
| boolean                                                      | **[selectWithKeyChar](#selectWithKeyChar(char))**(char keyChar)      如果存在与指定键盘字符相对应的项，则选择该列表项并返回 true。 |
| void                                                         | **[setAction](#setAction(javax.swing.Action))**([Action](http://www.daimaku.net/book/javasdk/javax/swing/Action.html) a)      设置 ActionEvent 源的 Action。 |
| void                                                         | **[setActionCommand](#setActionCommand(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) aCommand)      设置发送到动作侦听器的事件中应该包括的动作命令。 |
| void                                                         | **[setEditable](#setEditable(boolean))**(boolean aFlag)      确定 JComboBox 字段是否可编辑。 |
| void                                                         | **[setEditor](#setEditor(javax.swing.ComboBoxEditor))**([ComboBoxEditor](http://www.daimaku.net/book/javasdk/javax/swing/ComboBoxEditor.html) anEditor)      设置用于绘制和编辑 JComboBox 字段中所选项的编辑器。 |
| void                                                         | **[setEnabled](#setEnabled(boolean))**(boolean b)      启用组合框以便可以选择项。 |
| void                                                         | **[setKeySelectionManager](#setKeySelectionManager(javax.swing.JComboBox.KeySelectionManager))**([JComboBox.KeySelectionManager](http://www.daimaku.net/book/javasdk/javax/swing/JComboBox.KeySelectionManager.html) aManager)      设置将键盘字符转换为列表选择的对象。 |
| void                                                         | **[setLightWeightPopupEnabled](#setLightWeightPopupEnabled(boolean))**(boolean aFlag)      设置 lightWeightPopupEnabled 属性，该属性提供一个提示：是应该使用重量级 Component（如 Panel 或 Window）还是轻量级 Component 来包含 JComboBox。 |
| void                                                         | **[setMaximumRowCount](#setMaximumRowCount(int))**(int count)      设置 JComboBox 显示的最大行数。 |
| void                                                         | **[setModel](#setModel(javax.swing.ComboBoxModel))**([ComboBoxModel](http://www.daimaku.net/book/javasdk/javax/swing/ComboBoxModel.html) aModel)      设置 JComboBox 用于获取项列表的数据模型。 |
| void                                                         | **[setPopupVisible](#setPopupVisible(boolean))**(boolean v)      设置弹出窗口的可见性。 |
| void                                                         | **[setPrototypeDisplayValue](#setPrototypeDisplayValue(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) prototypeDisplayValue)      设置用于计算 UI 部分的显示大小的原型显示值。 |
| void                                                         | **[setRenderer](#setRenderer(javax.swing.ListCellRenderer))**([ListCellRenderer](http://www.daimaku.net/book/javasdk/javax/swing/ListCellRenderer.html) aRenderer)      设置渲染器，该渲染器用于绘制列表项和从 JComboBox 字段的列表中选择的项。 |
| void                                                         | **[setSelectedIndex](#setSelectedIndex(int))**(int anIndex)      选择索引 anIndex 处的项。 |
| void                                                         | **[setSelectedItem](#setSelectedItem(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) anObject)      将组合框显示区域中所选项设置为参数中的对象。 |
| void                                                         | **[setUI](#setUI(javax.swing.plaf.ComboBoxUI))**([ComboBoxUI](http://www.daimaku.net/book/javasdk/javax/swing/plaf/ComboBoxUI.html) ui)      设置呈现此组件的 L&F 对象。 |
| void                                                         | **[showPopup](#showPopup())**()      促使组合框显示其弹出窗口。 |
| void                                                         | **[updateUI](#updateUI())**()      将 UI 属性重置为当前外观的值。 |

#### JRadioButton：单选按钮组件

>实现一个单选按钮，此按钮项可被选择或取消选择，并可为用户显示其状态。与 [`ButtonGroup`](http://www.daimaku.net/book/javasdk/javax/swing/ButtonGroup.html) 对象配合使用可创建一组按钮，一次只能选择其中的一个按钮。（创建一个 ButtonGroup 对象并用其 `add` 方法将 JRadioButton 对象包含在此组中。）

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[JRadioButton](#JRadioButton())**()      创建一个初始化为未选择的单选按钮，其文本未设定。 |      |
| **[JRadioButton](#JRadioButton(javax.swing.Action))**([Action](http://www.daimaku.net/book/javasdk/javax/swing/Action.html) a)      创建一个单选按钮，其属性来自提供的 Action。 |      |
| **[JRadioButton](#JRadioButton(javax.swing.Icon))**([Icon](http://www.daimaku.net/book/javasdk/javax/swing/Icon.html) icon)      创建一个初始化为未选择的单选按钮，其具有指定的图像但无文本。 |      |
| **[JRadioButton](#JRadioButton(javax.swing.Icon, boolean))**([Icon](http://www.daimaku.net/book/javasdk/javax/swing/Icon.html) icon, boolean selected)      创建一个具有指定图像和选择状态的单选按钮，但无文本。 |      |
| **[JRadioButton](#JRadioButton(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) text)      创建一个具有指定文本的状态为未选择的单选按钮。 |      |
| **[JRadioButton](#JRadioButton(java.lang.String, boolean))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) text, boolean selected)      创建一个具有指定文本和选择状态的单选按钮。 |      |
| **[JRadioButton](#JRadioButton(java.lang.String, javax.swing.Icon))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) text, [Icon](http://www.daimaku.net/book/javasdk/javax/swing/Icon.html) icon)      创建一个具有指定的文本和图像并初始化为未选择的单选按钮。 |      |
| **[JRadioButton](#JRadioButton(java.lang.String, javax.swing.Icon, boolean))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) text, [Icon](http://www.daimaku.net/book/javasdk/javax/swing/Icon.html) icon, boolean selected)      创建一个具有指定的文本、图像和选择状态的单选按钮。 |      |

 

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [AccessibleContext](http://www.daimaku.net/book/javasdk/javax/accessibility/AccessibleContext.html) | **[getAccessibleContext](#getAccessibleContext())**()      获取与此 JRadioButton 相关联的 AccessibleContext。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getUIClassID](#getUIClassID())**()      返回呈现此组件的 L&F 类的名称。 |
| protected  [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[paramString](#paramString())**()      返回此 JRadioButton 的字符串表示形式。 |
| void                                                         | **[updateUI](#updateUI())**()      将 UI 属性重置为当前外观对应的值。 |

 

#### JList：列表框组件

>    显示对象列表并且允许用户选择一个或多个项的组件。单独的模型 `ListModel` 维护列表的内容。
>
>    使用能自动构建只读 `ListModel` 实例的 `JList` 构造方法，可以方便地显示对象数组或对象 Vector：

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[JList](#JList())**()      构造一个具有空的、只读模型的 JList。 |      |
| **[JList](#JList(javax.swing.ListModel))**([ListModel](http://www.daimaku.net/book/javasdk/javax/swing/ListModel.html) dataModel)      根据指定的非 null 模型构造一个显示元素的 JList。 |      |
| **[JList](#JList(java.lang.Object[]))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html)[] listData)      构造一个 JList，使其显示指定数组中的元素。 |      |
| **[JList](#JList(java.util.Vector))**([Vector](http://www.daimaku.net/book/javasdk/java/util/Vector.html)<?> listData)      构造一个 JList，使其显示指定 Vector 中的元素。 |      |

 

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| void                                                         | **[addListSelectionListener](#addListSelectionListener(javax.swing.event.ListSelectionListener))**([ListSelectionListener](http://www.daimaku.net/book/javasdk/javax/swing/event/ListSelectionListener.html) listener)      将侦听器添加到列表，每次选择发生更改时将获得通知；这是侦听选择状态更改的首选方式。 |
| void                                                         | **[addSelectionInterval](#addSelectionInterval(int, int))**(int anchor, int lead)      将选择设置为指定间隔与当前选择的并集。 |
| void                                                         | **[clearSelection](#clearSelection())**()      清除选择；调用此方法后，isSelectionEmpty 将返回 true。 |
| protected  [ListSelectionModel](http://www.daimaku.net/book/javasdk/javax/swing/ListSelectionModel.html) | **[createSelectionModel](#createSelectionModel())**()      返回一个 DefaultListSelectionModel 实例；在构造期间调用此方法初始化列表的选择模型属性。 |
| void                                                         | **[ensureIndexIsVisible](#ensureIndexIsVisible(int))**(int index)      滚动封闭视口中的列表，使指定单元完全可见。 |
| protected  void                                              | **[fireSelectionValueChanged](#fireSelectionValueChanged(int, int, boolean))**(int firstIndex, int lastIndex, boolean isAdjusting)      通知直接添加到列表的 ListSelectionListener 对列表模型做出了选择更改。 |
| [AccessibleContext](http://www.daimaku.net/book/javasdk/javax/accessibility/AccessibleContext.html) | **[getAccessibleContext](#getAccessibleContext())**()      获取与此 JList 关联的 AccessibleContext。 |
| int                                                          | **[getAnchorSelectionIndex](#getAnchorSelectionIndex())**()      返回定位选择索引。 |
| [Rectangle](http://www.daimaku.net/book/javasdk/java/awt/Rectangle.html) | **[getCellBounds](#getCellBounds(int, int))**(int index0, int index1)      返回列表的坐标系统中两个索引所指定单元范围内的边界矩形。 |
| [ListCellRenderer](http://www.daimaku.net/book/javasdk/javax/swing/ListCellRenderer.html) | **[getCellRenderer](#getCellRenderer())**()      返回负责绘制列表项的对象。 |
| boolean                                                      | **[getDragEnabled](#getDragEnabled())**()      返回是否启用自动拖动处理。 |
| [JList.DropLocation](http://www.daimaku.net/book/javasdk/javax/swing/JList.DropLocation.html) | **[getDropLocation](#getDropLocation())**()      返回在该组件上执行 DnD 操作期间此组件应该视觉上指示为放置位置的位置；如果当前没有任何显示的位置，则返回 null。 |
| [DropMode](http://www.daimaku.net/book/javasdk/javax/swing/DropMode.html) | **[getDropMode](#getDropMode())**()      返回此组件的放置模式。 |
| int                                                          | **[getFirstVisibleIndex](#getFirstVisibleIndex())**()      返回当前可见的最小的列表索引。 |
| int                                                          | **[getFixedCellHeight](#getFixedCellHeight())**()      返回 fixedCellHeight 属性的值。 |
| int                                                          | **[getFixedCellWidth](#getFixedCellWidth())**()      返回 fixedCellWidth 属性的值。 |
| int                                                          | **[getLastVisibleIndex](#getLastVisibleIndex())**()      返回当前可见的最大列表索引。 |
| int                                                          | **[getLayoutOrientation](#getLayoutOrientation())**()      返回列表的布局方向属性：如果布局是单列单元，则返回 VERTICAL；如果布局是“报纸样式”并且内容按先垂直后水平排列， 则返回 VERTICAL_WRAP；如果布局是“报纸样式”并且内容按先水平后垂直排列，则返回 HORIZONTAL_WRAP。 |
| int                                                          | **[getLeadSelectionIndex](#getLeadSelectionIndex())**()      返回前导选择索引。 |
| [ListSelectionListener](http://www.daimaku.net/book/javasdk/javax/swing/event/ListSelectionListener.html)[] | **[getListSelectionListeners](#getListSelectionListeners())**()      返回通过 addListSelectionListener 添加到此 JList 中的所有 ListSelectionListener 所组成的数组。 |
| int                                                          | **[getMaxSelectionIndex](#getMaxSelectionIndex())**()      返回选择的最大单元索引；如果选择为空，则返回 -1。 |
| int                                                          | **[getMinSelectionIndex](#getMinSelectionIndex())**()      返回选择的最小单元索引；如果选择为空，则返回 -1。 |
| [ListModel](http://www.daimaku.net/book/javasdk/javax/swing/ListModel.html) | **[getModel](#getModel())**()      返回保存由 JList 组件显示的项列表的数据模型。 |
| int                                                          | **[getNextMatch](#getNextMatch(java.lang.String, int, javax.swing.text.Position.Bias))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) prefix, int startIndex, [Position.Bias](http://www.daimaku.net/book/javasdk/javax/swing/text/Position.Bias.html) bias)      返回其 toString 值以给定前缀开头的下一个列表元素。 |
| [Dimension](http://www.daimaku.net/book/javasdk/java/awt/Dimension.html) | **[getPreferredScrollableViewportSize](#getPreferredScrollableViewportSize())**()      计算显示 visibleRowCount 行所需的视口的大小。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[getPrototypeCellValue](#getPrototypeCellValue())**()      返回“原型的”单元值，即用于计算单元的固定宽度和高度的值。 |
| int                                                          | **[getScrollableBlockIncrement](#getScrollableBlockIncrement(java.awt.Rectangle, int, int))**([Rectangle](http://www.daimaku.net/book/javasdk/java/awt/Rectangle.html) visibleRect, int orientation, int direction)      返回为显露上一个或下一个块而滚动的距离。 |
| boolean                                                      | **[getScrollableTracksViewportHeight](#getScrollableTracksViewportHeight())**()      如果此 JList 在 JViewport 中显示并且视口的高度大于列表的首选高度，或者布局方向为 VERTICAL_WRAP 或 visibleRowCount <= 0，则返回 true；否则返回 false。 |
| boolean                                                      | **[getScrollableTracksViewportWidth](#getScrollableTracksViewportWidth())**()      如果此 JList 在 JViewport 中显示并且视口的宽度大于列表的首选宽度，或者布局方向为 HORIZONTAL_WRAP 和 visibleRowCount <= 0，则返回 true；否则返回 false。 |
| int                                                          | **[getScrollableUnitIncrement](#getScrollableUnitIncrement(java.awt.Rectangle, int, int))**([Rectangle](http://www.daimaku.net/book/javasdk/java/awt/Rectangle.html) visibleRect, int orientation, int direction)      返回为显露上一个或下一个行（垂直滚动）或列（水平滚动）而滚动的距离。 |
| int                                                          | **[getSelectedIndex](#getSelectedIndex())**()      返回最小的选择单元索引；只选择了列表中单个项时，返回**该选择**。 |
| int[]                                                        | **[getSelectedIndices](#getSelectedIndices())**()      返回所选的全部索引的数组（按升序排列）。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) | **[getSelectedValue](#getSelectedValue())**()      返回最小的选择单元索引的值；只选择了列表中单个项时，返回**所选值**。 |
| [Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html)[] | **[getSelectedValues](#getSelectedValues())**()      返回所有选择值的数组，根据其列表中的索引顺序按升序排序。 |
| [Color](http://www.daimaku.net/book/javasdk/java/awt/Color.html) | **[getSelectionBackground](#getSelectionBackground())**()      返回用于绘制选定项的背景的颜色。 |
| [Color](http://www.daimaku.net/book/javasdk/java/awt/Color.html) | **[getSelectionForeground](#getSelectionForeground())**()      返回用于绘制选定项的前景的颜色。 |
| int                                                          | **[getSelectionMode](#getSelectionMode())**()      返回列表的当前选择模式。 |
| [ListSelectionModel](http://www.daimaku.net/book/javasdk/javax/swing/ListSelectionModel.html) | **[getSelectionModel](#getSelectionModel())**()      返回当前选择模型。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getToolTipText](#getToolTipText(java.awt.event.MouseEvent))**([MouseEvent](http://www.daimaku.net/book/javasdk/java/awt/event/MouseEvent.html) event)      返回用于给定事件的工具提示文本。 |
| [ListUI](http://www.daimaku.net/book/javasdk/javax/swing/plaf/ListUI.html) | **[getUI](#getUI())**()      返回呈现此组件的外观对象 ListUI。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getUIClassID](#getUIClassID())**()      返回 "ListUI"，它是用于查找定义此组件外观的 javax.swing.plaf.ListUI 类名称的 UIDefaults 键。 |
| boolean                                                      | **[getValueIsAdjusting](#getValueIsAdjusting())**()      返回选择模型的 isAdjusting 属性的值。 |
| int                                                          | **[getVisibleRowCount](#getVisibleRowCount())**()      返回 visibleRowCount 属性的值。 |
| [Point](http://www.daimaku.net/book/javasdk/java/awt/Point.html) | **[indexToLocation](#indexToLocation(int))**(int index)      返回列表的坐标系统中指定项的原点。 |
| boolean                                                      | **[isSelectedIndex](#isSelectedIndex(int))**(int index)      如果选择了指定的索引，则返回 true；否则返回 false。 |
| boolean                                                      | **[isSelectionEmpty](#isSelectionEmpty())**()      如果什么也没有选择，则返回 true；否则返回 false。 |
| int                                                          | **[locationToIndex](#locationToIndex(java.awt.Point))**([Point](http://www.daimaku.net/book/javasdk/java/awt/Point.html) location)      返回最接近列表的坐标系统中给定位置的单元索引。 |
| protected  [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[paramString](#paramString())**()      返回此 JList 的 String 表示形式。 |
| void                                                         | **[removeListSelectionListener](#removeListSelectionListener(javax.swing.event.ListSelectionListener))**([ListSelectionListener](http://www.daimaku.net/book/javasdk/javax/swing/event/ListSelectionListener.html) listener)      从列表中移除一个选择侦听器。 |
| void                                                         | **[removeSelectionInterval](#removeSelectionInterval(int, int))**(int index0, int index1)      将选择设置为指定间隔和当前选择的差集。 |
| void                                                         | **[setCellRenderer](#setCellRenderer(javax.swing.ListCellRenderer))**([ListCellRenderer](http://www.daimaku.net/book/javasdk/javax/swing/ListCellRenderer.html) cellRenderer)      设置用于绘制列表中每个单元的委托。 |
| void                                                         | **[setDragEnabled](#setDragEnabled(boolean))**(boolean b)      打开或关闭自动拖动处理。 |
| void                                                         | **[setDropMode](#setDropMode(javax.swing.DropMode))**([DropMode](http://www.daimaku.net/book/javasdk/javax/swing/DropMode.html) dropMode)      设置此组件的放置模式。 |
| void                                                         | **[setFixedCellHeight](#setFixedCellHeight(int))**(int height)      设置一个固定值，将用于列表中每个单元的高度。 |
| void                                                         | **[setFixedCellWidth](#setFixedCellWidth(int))**(int width)      设置一个固定值，将用于列表中每个单元的宽度。 |
| void                                                         | **[setLayoutOrientation](#setLayoutOrientation(int))**(int layoutOrientation)      定义布置列表单元的方式。 |
| void                                                         | **[setListData](#setListData(java.lang.Object[]))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html)[] listData)      根据一个对象数组构造只读 ListModel，然后对此模型调用 setModel。 |
| void                                                         | **[setListData](#setListData(java.util.Vector))**([Vector](http://www.daimaku.net/book/javasdk/java/util/Vector.html)<?> listData)      根据一个 Vector 构造只读 ListModel，然后对此模型调用 setModel。 |
| void                                                         | **[setModel](#setModel(javax.swing.ListModel))**([ListModel](http://www.daimaku.net/book/javasdk/javax/swing/ListModel.html) model)      设置表示列表内容或列表“值”的模型，通知属性更改侦听器，然后清除列表选择。 |
| void                                                         | **[setPrototypeCellValue](#setPrototypeCellValue(java.lang.Object))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) prototypeCellValue)      设置 prototypeCellValue 属性，然后（如果新值为非 null）计算 fixedCellWidth 和 fixedCellHeight 属性：请求单元渲染器组件提供单元渲染器的给定值（及索引 0），并使用该组件的首选大小。 |
| void                                                         | **[setSelectedIndex](#setSelectedIndex(int))**(int index)      选择单个单元。 |
| void                                                         | **[setSelectedIndices](#setSelectedIndices(int[]))**(int[] indices)      将选择更改为给定数组所指定的索引的集合。 |
| void                                                         | **[setSelectedValue](#setSelectedValue(java.lang.Object, boolean))**([Object](http://www.daimaku.net/book/javasdk/java/lang/Object.html) anObject, boolean shouldScroll)      从列表中选择指定的对象。 |
| void                                                         | **[setSelectionBackground](#setSelectionBackground(java.awt.Color))**([Color](http://www.daimaku.net/book/javasdk/java/awt/Color.html) selectionBackground)      设置用于绘制选定项的背景的颜色，单元渲染器可以使用此颜色填充所选单元。 |
| void                                                         | **[setSelectionForeground](#setSelectionForeground(java.awt.Color))**([Color](http://www.daimaku.net/book/javasdk/java/awt/Color.html) selectionForeground)      设置用于绘制选定项的前景的颜色，单元渲染器可以使用此颜色呈现文本和图形。 |
| void                                                         | **[setSelectionInterval](#setSelectionInterval(int, int))**(int anchor, int lead)      选择指定的间隔。 |
| void                                                         | **[setSelectionMode](#setSelectionMode(int))**(int selectionMode)      设置列表的选择模式。 |
| void                                                         | **[setSelectionModel](#setSelectionModel(javax.swing.ListSelectionModel))**([ListSelectionModel](http://www.daimaku.net/book/javasdk/javax/swing/ListSelectionModel.html) selectionModel)      将列表的 selectionModel 设置为非 null 的 ListSelectionModel 实现。 |
| void                                                         | **[setUI](#setUI(javax.swing.plaf.ListUI))**([ListUI](http://www.daimaku.net/book/javasdk/javax/swing/plaf/ListUI.html) ui)      设置呈现此组件的外观对象 ListUI。 |
| void                                                         | **[setValueIsAdjusting](#setValueIsAdjusting(boolean))**(boolean b)      设置选择模型的 valueIsAdjusting 属性。 |
| void                                                         | **[setVisibleRowCount](#setVisibleRowCount(int))**(int visibleRowCount)      设置 visibleRowCount 属性，对于不同的布局方向，此方法有不同的含义：对于 VERTICAL 布局方向，此方法设置要显示的首选行数（不要求滚动）；对于其他方向，它影响单元的包装。 |
| void                                                         | **[updateUI](#updateUI())**()      重置 ListUI 属性，将其设置为当前外观所提供的值。 |

 

#### JCheckBox：复选框组件

>   复选框的实现，复选框是一个可以被选定和取消选定的项，它将其状态显示给用户。按照惯例，可以选定组中任意数量的复选框。有关使用复选框的示例和信息，请参阅 *The Java Tutorial* 中的 [How to Use Buttons, Check Boxes, and Radio Buttons](http://java.sun.com/docs/books/tutorial/uiswing/components/button.html)。
>
>   通过 `Action` 可配置按钮，并进行某种程度的控制。将 `Action` 用于按钮具有许多直接配置按钮所不及的优点。有关更多详细信息，请参阅[支持 `Action`](http://www.daimaku.net/book/javasdk/javax/swing/Action.html#buttonActions) 的 Swing 组件，可在 *The Java Tutorial* 中的 [How to Use Actions](http://java.sun.com/docs/books/tutorial/uiswing/misc/action.html) 一节找到更多信息。

| ***\*构造方法摘要\****                                       |      |
| ------------------------------------------------------------ | ---- |
| **[JCheckBox](#JCheckBox())**()      创建一个没有文本、没有图标并且最初未被选定的复选框。 |      |
| **[JCheckBox](#JCheckBox(javax.swing.Action))**([Action](http://www.daimaku.net/book/javasdk/javax/swing/Action.html) a)      创建一个复选框，其属性从所提供的 Action 获取。 |      |
| **[JCheckBox](#JCheckBox(javax.swing.Icon))**([Icon](http://www.daimaku.net/book/javasdk/javax/swing/Icon.html) icon)      创建有一个图标、最初未被选定的复选框。 |      |
| **[JCheckBox](#JCheckBox(javax.swing.Icon, boolean))**([Icon](http://www.daimaku.net/book/javasdk/javax/swing/Icon.html) icon, boolean selected)      创建一个带图标的复选框，并指定其最初是否处于选定状态。 |      |
| **[JCheckBox](#JCheckBox(java.lang.String))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) text)      创建一个带文本的、最初未被选定的复选框。 |      |
| **[JCheckBox](#JCheckBox(java.lang.String, boolean))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) text, boolean selected)      创建一个带文本的复选框，并指定其最初是否处于选定状态。 |      |
| **[JCheckBox](#JCheckBox(java.lang.String, javax.swing.Icon))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) text, [Icon](http://www.daimaku.net/book/javasdk/javax/swing/Icon.html) icon)      创建带有指定文本和图标的、最初未选定的复选框。 |      |
| **[JCheckBox](#JCheckBox(java.lang.String, javax.swing.Icon, boolean))**([String](http://www.daimaku.net/book/javasdk/java/lang/String.html) text, [Icon](http://www.daimaku.net/book/javasdk/javax/swing/Icon.html) icon, boolean selected)      创建一个带文本和图标的复选框，并指定其最初是否处于选定状态。 |      |

 

| ***\*方法摘要\****                                           |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [AccessibleContext](http://www.daimaku.net/book/javasdk/javax/accessibility/AccessibleContext.html) | **[getAccessibleContext](#getAccessibleContext())**()      获取与此 JCheckBox 关联的 AccessibleContext。 |
| [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[getUIClassID](#getUIClassID())**()      返回指定呈现此组件的 L&F 类名的字符串。 |
| boolean                                                      | **[isBorderPaintedFlat](#isBorderPaintedFlat())**()      获取 borderPaintedFlat 属性的值。 |
| protected  [String](http://www.daimaku.net/book/javasdk/java/lang/String.html) | **[paramString](#paramString())**()      返回此 JCheckBox 的字符串表示形式。 |
| void                                                         | **[setBorderPaintedFlat](#setBorderPaintedFlat(boolean))**(boolean b)      设置 borderPaintedFlat 属性，该属性为外观提供了关于复选框边框外观的提示。 |
| void                                                         | **[updateUI](#updateUI())**()      根据当前外观重置 UI 属性值。 |

##  四、Java中解析JSON

Java中，我们经常需要将JSON字符串，转为Java对象，或是将Java对象转为JSON字符串，这一节，我们学习使用`Jackson`库，来完成这个功能

`Jackson` 是当前用的比较广泛的，用来序列化和反序列化 json 的 Java 的开源框架。Jackson 社区相对比较活跃，更新速度也比较快， 从 Github 中的统计来看，Jackson 是最流行的 json 解析器之一 。 Spring MVC 的默认 json 解析器便是 Jackson。

在pom.xml中添加依赖：

```
<dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.8.3</version>
</dependency>
```

接下来，我们将Foo类的对象，转为JSON字符串

```javascript
class Foo {
    private int id;
    private String name;

    public Foo() {
    }

    public Foo(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
Foo foo = new Foo(1,"jack");

ObjectMapper mapper = new ObjectMapper();
String json= mapper.writeValueAsString(foo);
System.out.println(json);
```

这样，我们就得到了JSON字符串 `{"id":1,"name":"jack"}`

如果我们有一个JSON字符串，需要转为Java对象，使用下面的方法：

```javascript
// json是一个String变量，值为 {"id":1,"name":"jack"}
String json = "{\"id\":1,\"name\":\"jack\"}";

ObjectMapper mapper = new ObjectMapper();

Foo foo =  mapper.readValue(json, Foo.class); 
```

## 五、开发桌面聊天软件

接下来，我们利用本章所学的知识，开发图形界面的聊天软件(类似QQ)

### 1、登录接口如下：

HTTP POST (application/x-www-form-urlencoded)

https://www.it266.com/teamboard-backend/api/user/token

字段：

```
username
password
```

### 2、登录成功后，获取个人信息  

HTTP GET

https://www.it266.com/teamboard-backend/api/user/profile?token=XXX

### 3、联系人数据

HTTP GET

https://www.it266.com/teamboard-backend/api/chat/contact?token=XXX

### 4、给指定好友发消息

HTTP POST (application/x-www-form-urlencoded)

https://www.it266.com/teamboard-backend/api/chat/message/create?token=XXX

字段：

```
type                  消息类型，1表示文本消息
content               消息内容
receiver_type         接收方类型，1表示发给好友
receiver_id           接收方id(好友的id，不是uid)
```



## 六、MQTT协议

MQTT（Message Queuing Telemetry Transport，消息队列遥测传输协议）是一种低开销、低带宽占用的即时通讯协议，使其在物联网、小型设备、移动应用等方面有较广泛的应用

扩展阅读了解： MQTT 协议 3.1.1 中文版

http://www.daimaku.net/book/mqtt/

调试MQTT可以使用`mqtt.fx`，下载该软件，并连下面的MQTT服务器，让好友发消息给你，测试是否能收到消息

聊天功能服务端地址: mqtt.it266.com

端口: 1883

用户名: 调用`https://www.it266.com/teamboard-backend/api/user/profile`获取的`id`

密码： 调用登录API获取的token

订阅聊天消息: `/msg/u/<用户id>`

例如，你的id为123，订阅 `/msg/u/123` 之后，有新消息时，你将能及时获取到消息内容

订阅群聊消息: `/msg/g/<群id>`

消息格式为JSON字符串：

![img](https://static.daimaku.net/material/202104/09/11c2c58946c4f7f152712e8b9296de23.png!l)

预览

Java客户端使用 `mqtt-client`，使用方法 ：

https://github.com/fusesource/mqtt-client

如果你还看不懂官方文档，可以参考： http://www.daimaku.net/post/view/10736

请完成聊天软件中的消息接收功能

重 做

## 七、线程

`线程`是操作系统能够进行运算调度的最小单位，Java中，将线程管理封装到了Thread类中

```javascript
Thread thread1 = new Thread(() -> {
     // 这里面的代码，将在单独的线程中运行
});

thread1.start();
```

## 八、线程

设计模式

教学资料

先学习 `单例模式`，核心思想参考： http://www.daimaku.net/post/view/10963

接下来学习 `发布订阅模式`，优化我们聊天系统中的消息传递，从资料中下载源码学习

再往下：工厂模式、抽象工厂模式、观察者模式、装饰器模式，每天掌握一个 https://www.runoob.com/design-pattern/design-pattern-tutorial.html

## [GUI](https://so.csdn.net/so/search?q=GUI)编程

[狂神视频学习笔记](https://space.bilibili.com/95256449)

### 1.简介

GUI核心技术：[Swing](https://so.csdn.net/so/search?q=Swing) AWT

#### 缺点：

-   不美观
-   需要jre环境

#### 为什么要学习

-   可以写出一些自己用的小工具
-   可能会涉及到swing的维护工作 -> 破解
-   了解MVC架构，了解监听

### 2.AWT

#### 2.1.AWT介绍

-   AWT：抽象的窗口工具，包含了很多的类和接口
-   元素：窗口、按钮、文本框
-   java.awt包下

#### 2.2.组件和容器

##### [frame](https://so.csdn.net/so/search?q=frame)

```java
import java.awt.*;

//GUI的第一个界面
public class TestFrame {
    public static void main(String[] args) {
        Frame frame = new Frame("frame标题");
//        设置窗口可见
        frame.setVisible(true);
//        设置大小
        frame.setSize(400,400);
//        设置背景颜色
        frame.setBackground(Color.BLACK);
//        设置初始位置
        frame.setLocation(400,400);
//        设置大小固定
        frame.setResizable(false);


    }
}

123456789101112131415161718192021
```

-   封装打开多个实现

```java
import java.awt.*;

public class TestFrame2 {
    public static void main(String[] args) {
        new MyFrame(100,100,200,200,Color.BLACK);
        new MyFrame(300,100,200,200,Color.BLUE);
        new MyFrame(100,300,200,200,Color.YELLOW);
        new MyFrame(300,300,200,200,Color.WHITE);
    }

}
class MyFrame extends Frame{
    //        计数器
    private static int id = 0;
    public MyFrame(int x,int y,int w,int h,Color color){
        super("MyFrame+"+id++);
        this.setBounds(x,y,w,h);
        this.setBackground(color);
        this.setVisible(true);
    }
}

12345678910111213141516171819202122
```

##### Panel

```java
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestPanel {
    public static void main(String[] args) {
        Frame frame = new Frame("带面板的Frame");
        Panel panel = new Panel();
        frame.setBounds(400,400,500,500);
        frame.setBackground(Color.BLACK);
        frame.setLayout(null);

        panel.setBounds(100,100,300,300);
        panel.setBackground(Color.YELLOW);
//        将面板放入frame中
        frame.add(panel);
        frame.setVisible(true);
//        添加监听
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

123456789101112131415161718192021222324252627
```

#### 2.3.布局管理器

-   流式布局 FlowLayout

```java
import java.awt.*;

//流式布局
public class TestFlowLayout {
    public static void main(String[] args) {
        Frame frame = new Frame();
        frame.setVisible(true);
        frame.setBounds(400,400,500,500);
        Button button1 = new Button("按钮1");
        Button button2 = new Button("按钮2");
        Button button3 = new Button("按钮3");

        frame.add(button1);
        frame.add(button2);
        frame.add(button3);
        frame.setLayout(new FlowLayout(FlowLayout.RIGHT));
    }
}

12345678910111213141516171819
```

-   东西南北中 BorderLayout

```java
import java.awt.*;

public class TestBorderLayout {
    public static void main(String[] args) {
        Frame frame = new Frame();
        frame.setVisible(true);
        frame.setBounds(400,400,500,500);
        Button east = new Button("East");
        Button west = new Button("West");
        Button south = new Button("South");
        Button north = new Button("North");
        Button center = new Button("Center");

        frame.add(east,BorderLayout.EAST);
        frame.add(west,BorderLayout.WEST);
        frame.add(south,BorderLayout.SOUTH);
        frame.add(north,BorderLayout.NORTH);
//        frame.add(center,BorderLayout.CENTER);

    }

}

1234567891011121314151617181920212223
```

-   表格式布局 GridLayout

```java
import java.awt.*;

public class TestGridLayout {
    public static void main(String[] args) {
        Frame frame = new Frame();
        frame.setVisible(true);
//        frame.setBounds(400,400,500,500);

        Button button1 = new Button("but1");
        Button button2 = new Button("but2");
        Button button3 = new Button("but3");
        Button button4 = new Button("but4");
        Button button5 = new Button("but5");
        Button button6 = new Button("but6");
        frame.add(button1);
        frame.add(button2);
        frame.add(button3);
        frame.add(button4);
        frame.add(button5);
        frame.add(button6);
        frame.setLayout(new GridLayout(3,2));
        //        自动布局大小,测试过程中发现不能在第一行写这个，需要在添加完毕后增加会分配默认size
        frame.pack();
    }
}

1234567891011121314151617181920212223242526
```

-   练习

```java
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

/**
 * 分析：分四部分写
 */
public class ExDemo {
    public static void main(String[] args) {
        //总frame
        Frame frame = new Frame();
        frame.setLocation(400, 400);
        frame.setSize(300, 300);
        frame.setBackground(Color.blue);
        frame.setVisible(true);
        frame.setLayout(new GridLayout(2, 1));
        //四个面板
        Panel p1 = new Panel(new BorderLayout());
        Panel p2 = new Panel(new GridLayout(2, 1));
        Panel p3 = new Panel(new BorderLayout());
        Panel p4 = new Panel(new GridLayout(2, 2));
        //上面
        p1.add(new Button("Eset-1"), BorderLayout.EAST);
        p1.add(new Button("West"), BorderLayout.WEST);
        p2.add(new Button("p2-btn-1"));
        p2.add(new Button("p2-btn-2"));
        p1.add(p2, BorderLayout.CENTER);
        //下面
        p3.add(new Button("Eset-1"), BorderLayout.EAST);
        p3.add(new Button("West"), BorderLayout.WEST);
        for (int i = 0; i < 4; i++) {
            p4.add(new Button("btn-" + i));
        }
        p3.add(p4, BorderLayout.CENTER);
        frame.add(p1);
        frame.add(p3);
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });

    }
}
123456789101112131415161718192021222324252627282930313233343536373839404142434445
```

#### 2.4.监听器

-   一个按钮可以添加多个监听

```java
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestActionEvent1 {
    public static void main(String[] args) {
        Frame frame = new Frame();
        frame.setVisible(true);
        frame.setBounds(100,100,500,500);
//        一个按钮可以同时添加多个监听
        Button button = new Button();
        button.addActionListener((actionEvent) -> System.out.println("1"));
        button.addActionListener((actionEvent) -> System.out.println("2"));
        frame.add(button,BorderLayout.NORTH);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

123456789101112131415161718192021222324
```

-   一个监听可以给多个按钮共同使用

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestActionEvent2 {
    public static void main(String[] args) {
        Frame frame = new Frame();
        frame.setVisible(true);
        frame.setBounds(100,100,500,500);
//        顶一个一个监听可以多个按钮共同使用
        ActionListener actionListener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println(e.getActionCommand());
            }
        };
        Button button1 = new Button("1");
//        可以为按钮带参数来控制同一个监听执行不同按钮的方法
        button1.setActionCommand("11111111111111");
        button1.addActionListener(actionListener);
        Button button2 = new Button("2");
        button2.addActionListener(actionListener);
        frame.add(button1,BorderLayout.NORTH);
        frame.add(button2,BorderLayout.SOUTH);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

123456789101112131415161718192021222324252627282930313233343536
```

#### 总结

frame是一个顶级容器

-   panel面板不能单独存在，需要放到容器中使用
-   布局管理器

1.  流式布局
2.  东西南北中
3.  表格布局
4.  监听器

#### 2.5.输入框监听

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestActionEvent3 {
    public static void main(String[] args) {
        new MyFrame();
    }
}
class MyFrame extends Frame{
    public MyFrame(){
        TextField textArea = new TextField();
        textArea.addActionListener((event)-> {
            System.out.println(textArea.getText());
            textArea.setText("");
        });
        this.setVisible(true);
        this.setBounds(100,100,500,500);
        add(textArea);
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

123456789101112131415161718192021222324252627282930
```

#### 2.6.简易计算器

```java
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestCalc {
    public static void main(String[] args) {
        Calc calc = new Calc();
    }
}
class Calc extends Frame{
    public Calc(){
        TextField jia1 = new TextField("10");
        TextField jia2 = new TextField("10");
        TextField rest = new TextField("20");
        setLayout(new FlowLayout());
        add(jia1);
        add(new Label("+"));
        add(jia2);
        Button button = new Button("=");
        button.addActionListener(e -> {
            int jia = Integer.parseInt(jia1.getText());
            int beijia = Integer.parseInt(jia2.getText());
            rest.setText(jia+beijia+"");
            jia1.setText("");
            jia2.setText("");
        });
        add(button);
        add(rest);
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
        setVisible(true);
        pack();

    }
}

12345678910111213141516171819202122232425262728293031323334353637383940
```

#### 2.7.画笔

```java
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestPaint {
    public static void main(String[] args) {
        new MyPaint().loadMyPaint();
    }
}
class MyPaint extends Frame{
    public void loadMyPaint(){
        setVisible(true);
        setBounds(100,100,800,600);
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

    @Override
    public void paint(Graphics g) {
//        super.paint(g);
        g.setColor(Color.blue);
        g.drawOval(100,100,100,100);
        g.fillOval(100,200,100,100);
        g.fillRect(100,300,200,100);
    }
}

12345678910111213141516171819202122232425262728293031
```

#### 2.8.鼠标监听

>   [转载自人生若只如初代码优化](https://blog.csdn.net/u011412779/article/details/106629686/)

-   思路分析
    ![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/110-Java%25E7%25BD%2591%25E7%25BB%259C%25E7%25BC%2596%25E7%25A8%258B%25E7%25AC%2594%25E8%25AE%25B0/20201201104317526.jpg)

```java
import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

//测试鼠标监听
public class TestMouseListenter {
    public static void main(String[] args) {
        new Paint("画图").loadMyPaint();
    }
}
class Paint extends Frame {
    private List<Point> pointList;
    private Paint cuttorPaint;
    public Paint(String title){
        super(title);
        cuttorPaint = this;
        pointList = new ArrayList<>();
    }
    public void loadMyPaint(){
        setVisible(true);
        setBounds(100,100,800,600);
        addMouseListener(new MyMouseListenter());
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

    @Override
    public void paint(Graphics g) {
        Iterator<Point> iterator = pointList.iterator();
        while (iterator.hasNext()){
            Point point = iterator.next();
            //循环画列表的点坐标
            g.fillOval(point.x,point.y,10,10);
        }
    }
    private class MyMouseListenter extends MouseAdapter{
//        按下鼠标时触发
        @Override
        public void mousePressed(MouseEvent e) {
            pointList.add(new Point(e.getX(),e.getY()));
            //画笔重新画点
            cuttorPaint.repaint();
        }
    }
}

12345678910111213141516171819202122232425262728293031323334353637383940414243444546474849505152535455
```

#### 2.9.窗口监听

```java
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestWindow {
    public static void main(String[] args) {
        new MyWindow().loadMyPaint();
    }
}
class MyWindow extends Frame{
    public MyWindow(){
        super("默认窗口名称");
    }
    public void loadMyPaint(){
        setVisible(true);
        setBounds(100,100,800,600);
        addWindowListener(new WindowAdapter() {
//            点击窗口关闭按钮
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }

            @Override
            public void windowDeactivated(WindowEvent e) {
                System.out.println("窗口失去焦点");
            }

            //            打开窗口时执行
            @Override
            public void windowOpened(WindowEvent e) {
                System.out.println("windowOpened");
            }

            @Override
            public void windowClosed(WindowEvent e) {
                System.out.println("windowClosed");
            }

            @Override
            public void windowIconified(WindowEvent e) {
                System.out.println("缩小");
            }

            @Override
            public void windowDeiconified(WindowEvent e) {
                System.out.println("缩小对应的弹出窗口");
            }

            @Override
            public void windowActivated(WindowEvent e) {
                setTitle("被激活了窗口");
            }


            @Override
            public void windowStateChanged(WindowEvent e) {
                System.out.println("windowStateChanged");
            }

            @Override
            public void windowGainedFocus(WindowEvent e) {
                System.out.println("windowGainedFocus");
            }

            @Override
            public void windowLostFocus(WindowEvent e) {
                System.out.println("windowLostFocus");
            }
        });

    }
}

1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950515253545556575859606162636465666768697071727374
```

#### 2.10.键盘监听

```java
import java.awt.*;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestKeyListener {
    public static void main(String[] args) {
        new MyKeyFrame().loadMyPaint();
    }
}

class MyKeyFrame extends Frame{
    public MyKeyFrame(){
        super("默认窗口名称");
    }
    public void loadMyPaint(){
        setVisible(true);
        setBounds(100,100,800,600);
        addKeyListener(new KeyAdapter() {
//            按下键时执行
            @Override
            public void keyPressed(KeyEvent e) {
                int keyCode = e.getKeyCode();
                System.out.println(keyCode);
                if(keyCode == KeyEvent.VK_ENTER){
                    System.out.println("按了回车");
                }
            }
        });
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }
}

123456789101112131415161718192021222324252627282930313233343536373839
```

### 3.Swing

#### 3.1.窗口JFrame

```java
import javax.swing.*;
import java.awt.Container;
import static java.awt.Color.YELLOW;

public class TestJFrame1 {
    public static void main(String[] args) {
        JFrame jFrame = new JFrame();
        jFrame.setBounds(10,10,400,400);
        jFrame.setVisible(true);

        JLabel jLabel = new JLabel("测试标签");
//        jFrame.setBackground(Color.BLACK);
        Container contentPane = jFrame.getContentPane();
        contentPane.setBackground(YELLOW);
        //标签居中
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);
        jFrame.add(jLabel);
//        不设置，默认是隐藏窗口
        jFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}

12345678910111213141516171819202122
```

#### 3.2.弹窗JDialog

```java
import javax.swing.*;
import java.awt.*;

import static java.awt.Color.YELLOW;

public class TestJFrame2 {
    public static void main(String[] args) {
        JFrame jFrame = new JFrame();
        jFrame.setBounds(10,10,400,400);
        jFrame.setVisible(true);

        JButton jLabel = new JButton("测试按钮");
//        jFrame.setBackground(Color.BLACK);
        Container contentPane = jFrame.getContentPane();
        contentPane.setBackground(YELLOW);
//        设置居中
        jLabel.setHorizontalAlignment(SwingConstants.CENTER);
        jLabel.addActionListener(e ->
            new Mydiglog()
        );
        contentPane.setLayout(null);
        jLabel.setLocation(50,50);
        jLabel.setSize(200,50);
        contentPane.add(jLabel);
//        不设置，默认是隐藏窗口
        jFrame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }
}
class Mydiglog extends JDialog{
    public Mydiglog(){
        setVisible(true);
        setBounds(10,10,500,500);
//        弹窗默认带了关闭，不需要写
//        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        JLabel jLabel = new JLabel("测试弹窗标签2 ");
        Container container = getContentPane();
        container.setLayout(null);
        jLabel.setLocation(10,10);
        jLabel.setSize(100,20);
        container.add(jLabel);
    }
}

1234567891011121314151617181920212223242526272829303132333435363738394041424344
```

#### 图标Icon

```java
package com.duan.lesson03;

import javax.swing.*;
import java.awt.*;

public class IconFrame1 {
    public static void main(String[] args) {
        JFrame jFrame = new JFrame();
        jFrame.setBounds(10,10,400,400);
        jFrame.setVisible(true);
        JLabel jButton = new JLabel(" 标签",new MyIconDemo(10,10),SwingConstants.CENTER);
//        不设置，默认是隐藏窗口
        jFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jButton.setSize(100,100);
        jFrame.add(jButton);
    }
}
class MyIconDemo implements Icon{
    private int iconWiddth;
    private int iconHeight;

    public MyIconDemo(int iconWiddth,int iconHeight){
        this.iconWiddth = iconWiddth;
        this.iconHeight = iconHeight;
    }
    @Override
    public void paintIcon(Component c, Graphics g, int x, int y) {
        g.fillOval(x,y,iconWiddth,iconHeight);
    }

    @Override
    public int getIconWidth() {
        return iconWiddth;
    }

    @Override
    public int getIconHeight() {
        return iconHeight;
    }
}

1234567891011121314151617181920212223242526272829303132333435363738394041
```

#### 滚动条面板

```java
import javax.swing.*;
import java.awt.*;
import java.io.File;
import java.net.MalformedURLException;

public class TestPanle4 {
    public static void main(String[] args)  {
        JFrame jFrame = new JFrame();
        jFrame.setBounds(10,10,400,400);
        jFrame.setVisible(true);
        JTextArea jTextArea = new JTextArea(50,50);
//        滚动条面板
        JScrollPane jButton = new JScrollPane(jTextArea);
        jFrame.add(jButton);
    }
}

1234567891011121314151617
```

### 4.贪吃蛇

-   帧，如果时间片足够小，就是动画 一秒三石帧，连起来是动画 拆开就是图片
-   键盘监听 addKeyListener
-   需要注意，如果是面板添加监听需要设置当前面板获取焦点setFocusable(true);

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import java.io.File;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.Random;

public class StartGame  {
    public static void main(String[] args) {
        JFrame jFrame = new JFrame("贪吃蛇");

        jFrame.add(new GamePanel());
//        设置窗口不可拉伸
        jFrame.setResizable(false);
//        固定大小
        jFrame.setBounds(100,100,900,750);
        jFrame.setVisible(true);
        jFrame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
    }

}
//游戏面板
class GamePanel extends JPanel{
    private int length = 3;
    private int fx;
    private int[][] zuobiao = new int[2][850];
    private boolean isStart = false;
    private boolean isError = false;
    private int[] foot = new int[2];
    Random random = new Random();
    private Timer timer = new Timer(100,e -> {
        if(isStart && !isError){
            if(zuobiao[0][0] == foot[0] && zuobiao[1][0] == foot[1]){
                length++;
                setRandomFoot();
            }
            for (int i = length - 1; i > 0; i--) {
                zuobiao[0][i] =  zuobiao[0][i-1];
                zuobiao[1][i] =  zuobiao[1][i-1];
            }
            switch (fx){
                case KeyEvent.VK_RIGHT:
                    zuobiao[0][0] = zuobiao[0][0]+25;
                    if(zuobiao[0][0] >= 875)zuobiao[0][0]=25;
                    break;
                case KeyEvent.VK_LEFT:
                    zuobiao[0][0] = zuobiao[0][0]-25;
                    if(zuobiao[0][0] < 25)zuobiao[0][0]=850;
                    break;
                case KeyEvent.VK_UP:
                    zuobiao[1][0] = zuobiao[1][0]-25;
                    if(zuobiao[1][0] <= 70)zuobiao[1][0]=675;
                    break;
                case KeyEvent.VK_DOWN:
                    zuobiao[1][0] = zuobiao[1][0]+25;
                    if(zuobiao[1][0] >= 675)zuobiao[1][0]=70;
                    break;
            }
//            失败条件
            for (int i = 1; i < length; i++) {
                if(zuobiao[0][0] == zuobiao[0][i] && zuobiao[1][0] == zuobiao[1][i]){
                    isError = true;
                }
            }
            repaint();
        }
    });
    public GamePanel(){
        addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                switch (e.getKeyCode()){
                    case KeyEvent.VK_ENTER:
                        isError = false;
                        timer.stop();
                        init();
                        break;
                    case KeyEvent.VK_SPACE:
                        if(!isError){
                            isStart = !isStart;
                            repaint();
                        }
                        break;
                    case KeyEvent.VK_UP:
                        if(fx != KeyEvent.VK_DOWN)fx = KeyEvent.VK_UP;
                        break;
                    case KeyEvent.VK_DOWN:
                        if(fx != KeyEvent.VK_UP)fx = KeyEvent.VK_DOWN;
                        break;
                    case KeyEvent.VK_LEFT:
                        if(fx != KeyEvent.VK_RIGHT)fx = KeyEvent.VK_LEFT;
                        break;
                    case KeyEvent.VK_RIGHT:
                        if(fx != KeyEvent.VK_LEFT)fx = KeyEvent.VK_RIGHT;
                        break;
                }
            }
        });
        init();
    }
    public void init(){
        length = 3;
        zuobiao[0][0] = 100;
        zuobiao[1][0] = 95;
        for (int i = 1; i < length; i++) {
            zuobiao[0][i] = zuobiao[0][0]-i*25;
            zuobiao[1][i] = zuobiao[1][0];
        }
        setRandomFoot();
//        默认向右
        fx = KeyEvent.VK_RIGHT;
        setFocusable(true);
//        timer.setDelay(1);
        timer.start();
    }
//设置事物随机坐标
    private void setRandomFoot() {
        foot[0] = 25 + 25*random.nextInt(34);
        foot[1] = 70 + 25*random.nextInt(24);
        for (int i = 0; i < length; i++) {
            if(zuobiao[0][i] == foot[0] && zuobiao[1][i] == foot[1]){
                setRandomFoot();
            }
        }
    }

    //    画板
    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        setBackground(Color.white);
        GameData.header.paintIcon(this,g ,25,0);
        g.fillRect(25,70,850,625);
        GameData.food.paintIcon(this,g ,foot[0],foot[1]);
        switch (fx){
            case KeyEvent.VK_RIGHT:
                GameData.right.paintIcon(this,g,zuobiao[0][0],zuobiao[1][0]);
                break;
            case KeyEvent.VK_LEFT:
                GameData.left.paintIcon(this,g,zuobiao[0][0],zuobiao[1][0]);
                break;
            case KeyEvent.VK_UP:
                GameData.up.paintIcon(this,g,zuobiao[0][0],zuobiao[1][0]);
                break;
            case KeyEvent.VK_DOWN:
                GameData.dowm.paintIcon(this,g,zuobiao[0][0],zuobiao[1][0]);
                break;
        }
        for (int i = 1; i < length; i++) {
            GameData.body.paintIcon(this,g,zuobiao[0][i],zuobiao[1][i]);
        }

        if(!isStart){
            g.setColor(Color.YELLOW);
            g.setFont(new Font("微软雅黑",Font.BOLD,48));
            g.drawString("按空格开启游戏",250,500);
        }
        if(isError){
            g.setColor(Color.RED);
            g.setFont(new Font("微软雅黑",Font.BOLD,48));
            g.drawString("游戏失败,按回车开启游戏",250,500);
        }
    }
}
//游戏图标类
class GameData{
    private static URL bodyurl;
    private static URL downurl;
    private static URL foodurl;
    private static URL headerurl;
    private static URL lefturl;
    private static URL righturl;
    private static URL upurl;
    static {
        try {
            bodyurl = new File("D:\\xuexi\\img\\statics\\body.png").toURL();
            foodurl = new File("D:\\xuexi\\img\\statics\\food.png").toURL();
            headerurl = new File("D:\\xuexi\\img\\statics\\header.png").toURL();
            upurl = new File("D:\\xuexi\\img\\statics\\up.png").toURL();
            downurl = new File("D:\\xuexi\\img\\statics\\down.png").toURL();
            lefturl = new File("D:\\xuexi\\img\\statics\\left.png").toURL();
            righturl = new File("D:\\xuexi\\img\\statics\\right.png").toURL();
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
    }
    public static ImageIcon header = new ImageIcon(headerurl);
    public static ImageIcon body = new ImageIcon(bodyurl);
    public static ImageIcon food = new ImageIcon(foodurl);
    public static ImageIcon up = new ImageIcon(upurl);
    public static ImageIcon dowm = new ImageIcon(downurl);
    public static ImageIcon left = new ImageIcon(lefturl);
    public static ImageIcon right = new ImageIcon(righturl);
}
\\img\\statics\\body.png").toURL();
            foodurl = new File("D:\\xuexi\\img\\statics\\food.png").toURL();
            headerurl = new File("D:\\xuexi\\img\\statics\\header.png").toURL();
            upurl = new File("D:\\xuexi\\img\\statics\\up.png").toURL();
            downurl = new File("D:\\xuexi\\img\\statics\\down.png").toURL();
            lefturl = new File("D:\\xuexi\\img\\statics\\left.png").toURL();
            righturl = new File("D:\\xuexi\\img\\statics\\right.png").toURL();
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
    }
    public static ImageIcon header = new ImageIcon(headerurl);
    public static ImageIcon body = new ImageIcon(bodyurl);
    public static ImageIcon food = new ImageIcon(foodurl);
    public static ImageIcon up = new ImageIcon(upurl);
    public static ImageIcon dowm = new ImageIcon(downurl);
    public static ImageIcon left = new ImageIcon(lefturl);
    public static ImageIcon right = new ImageIcon(righturl);
}

```

# Java并发编程

## 一、Java中的线程

### 1、用户线程与守护线程

*   查看当前进程

```
jps -l
```

示例

```json
PS C:\Users\十六夜咲夜\Desktop\thread\thread> jps -l
6948 com.example.Foo
4120 sun.tools.jps.Jps
8440 org.jetbrains.idea.maven.server.RemoteMavenServer36
1196 
```

*   打印1196进程中更多的信息

```json
 jstack 1196  /*里面有多个线程信息*/
```

*   用户线程

```
自己写的mian函数
主要跑我们自己写的业务逻辑
```

*   守护线程

```
其他的线程
底层所依赖的系统级别的工作
```



* jvm 会等其他用户线程**(自己的业务逻辑)** 结束再结束

```json
/*设置为守护线程*/
t1.setDaemon( true );
```

* 对于无关紧要的线程可以设置为守护线程(jvm不会等待守护线程结束)

```json
package com.example.demo;

public class Foo {
    public static void main ( String[] args ) {

       Thread t1= new Thread(()->{
            try {
                System.out.println( "sleep start" );
                Thread.sleep( 5000 );

                System.out.println("thread end");
            } catch ( InterruptedException e ) {
                e.printStackTrace();
            }
        });

/*设置为守护线程*/
t1.setDaemon( true );
       t1.start();
        System.out.println( "main end" );
    }
}

```

### 当前线程



```json
/*获取当前线程*/
Thread thread = Thread.currentThread();
/*获取线程id*/
System.out.println( thread.getId() );
```

> 结果

```json
分线程的id:12
主线程id:1
分线程id:12
______________
睡眠后的id12
______________
```

```java
package com.example.demo;

public class Foo {
    public static void main ( String[] args ) {

        Thread t1 = new Thread( () -> {
            System.out.println("分线程id:"+ Thread.currentThread().getId() );
            try {
                /*获取当前线程*/
                Thread thread = Thread.currentThread();
                /*获取线程id*/
                System.out.println("______________");
                Thread.sleep( 1000 );
                System.out.println("睡眠后的id" + thread.getId() );
                System.out.println("______________");
            } catch ( InterruptedException e ) {
                e.printStackTrace();
            }
        } );
        System.out.println("分线程的id:"+t1.getId());
        System.out.println("主线程id:"+ Thread.currentThread().getId() );

        t1.start();
    }
}
```

## 二、线程安全



### 多线程的问题

> 当多个现成的数据对同一个数据主线程的数据进行修改的时候 会产生数据紊乱(与预期结不同)

```java
package com.example.demo;

class Bar {
    public int count = 0;
}

public class Foo {
    public final static Bar bar = new Bar();

    public static void main ( String[] args ) throws InterruptedException {
        Thread t1 = new Thread( () -> {
            for ( int i = 0; i < 10000; i++ ) {
                bar.count++;
            }
        } );
        Thread.sleep( 1000 );

        Thread t2 = new Thread( () -> {
            for ( int i = 0; i < 10000; i++ ) {
                bar.count++;
            }
        } );
//        同时执行2个线程
        t1.start();
        t2.start();

        Thread.sleep( 5000 );
        System.out.println( bar.count );
    }
}
/*结果不为20000*/
```

### synchronoized(){}(同步化)

**原子性**

由于2个线程同时对一个变量查询然后修改的时候会导致查询的数据不同步(高并发下来的一些问题)

* 数据库查询时应当使用count=count+1



> 解决线程不安全的问题

```json
/*加锁(同步化[让能执行的线程只有一个]) 加锁的时候其他线程会等待*/
synchronoized(bar){bar.count++}
```



```java
package com.example.demo;

class Bar {
    public int count = 0;
}

public class Foo {
    public final static Bar bar = new Bar();

    public static void main(String[] args) throws InterruptedException {
        //原子性
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 10000; i++) {
                synchronized (bar) {
                    bar.count++;
                }
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 10000; i++) {
                synchronized (bar) {
                    bar.count++;
                }
            }
        }); 
        t1.start();
        t2.start();


        /*等待查询完毕*/
        t1.join();
        t2.join();
        System.out.println(bar.count);
    }

}
```

### volatile(可见的)关键字

**可见性**

cpu有三级缓存 

*  不同线程之间,不一定感知到对共享变量的修改

> 如果在主线程中设置条件并修改条件,依赖这个条件的其他线程会先去找三级缓存,之后才会去查找内存,内存里面的条件发生改变的时候,缓存并没有做出相应改变

* 可以设置为禁止缓存

`join()`方法是`Thread`类中的一个方法，该方法的定义是等待该线程终止。其实就是`join()`方法将挂起**调用线程**的执行，直到**被调用的对象**完成它的执行。这段话难理解，后面我会用实例做讲解。

**注意**

```
要想在多线程环境下保证原子性，则可以通过锁、synchronized来确保。volatile是无法保证复合操作的原子性。
```

```java
package com.example.demo;

import java.net.InetAddress;
import java.net.UnknownHostException;
import java.util.Arrays;



public class Foo {
    public final static Bar bar = new Bar();
    /** 禁止缓存 (解决内存与缓存之间的数据不一致的问题) */z
    static volatile boolean isRun = true;

    public static void main(String[] args) throws InterruptedException, UnknownHostException {
        new Thread(() -> {
            long i = 0;
            while (Foo.isRun) {
                i++;
            }
            System.out.println(i);
        }).start();

//        Thread.sleep(1000);
        isRun = false;
        System.out.println("main end");
    }

}

```

### 练习demo

```java
package com.example.demo;

import lombok.Synchronized;

import java.net.InetAddress;
import java.net.UnknownHostException;
import java.util.*;


class Bar {
    public  long val = 0;



}

public class Foo {
    public volatile static boolean isRun = true;


    public static void main(String[] args) throws InterruptedException, UnknownHostException {
        Bar bar = new Bar();
        Thread t3 = new Thread(() -> {
            Foo.isRun=false;
        });

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000000; i++) {
                synchronized (bar) {
                    if (Foo.isRun) {
                        bar.val++;
                    }
                if (bar.val==15000)t3.start();
                }
            }
        });
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000000; i++) {
                synchronized (bar) {
                    if (Foo.isRun) {
                        bar.val++;
                    }

                    if (bar.val==15000)t3.start();

                }
            }
        });

        t1.start();
        t2.start();


        t1.join();
        t2.join();
        System.out.println(bar.val);
    }

}

```



### 线程安全问题

JVM之原子性、可见性、有序性（指令重排）
一、原子性
    原子性操作指相应的操作是单一不可分割的操作。在我们学化学这门课程的时候，对于里面讲到的原子性相信大家都非常明白，原子是微观世界中最小的不可再进行分割的单元，原子是最小的粒子。java里面的原子性操作也是如此，它代表着一个操作不能再进行分割是最小的执行单元，或者一系列操作要么全部成功执行，要么全部执行失败，不允许中间某一些成功失败，类比如事物控制，要么全部提交要么全部回滚。
    下面根据几个粒子来分析下原子性操作：

```
i = 0;       //1
j = i ;      //2
i++;         //3
i = j + 1;   //4
```

上面四个操作，有哪个几个是原子操作，那几个不是？如果不是很理解，可能会认为都是原子性操作，其实只有1才是原子操作，其余均不是。

```
1在Java中，对基本数据类型的变量和赋值操作都是原子性操作； 
2中包含了两个操作：读取i，将i值赋值给j 
3中包含了三个操作：读取i值、i + 1 、将+1结果赋值给i； 
4中同三一样
```

在单线程环境下我们可以认为整个步骤都是原子性操作，但是在多线程环境下则不同，Java只保证了基本数据类型的变量和赋值操作才是原子性的（注：在32位的JDK环境下，对64位数据的读取不是原子性操作*，如long、double）。在多线程环境中，非原子操作可能会受其他线程的干扰，例如第3个操作，i在加1之后将结果赋值给i，在赋值给i回写主内存的时候可能会被其他线程抢先回写，导致此次执行失败丢失了本次计算结果（这里会涉及到原子性操作，下面会进行讲解）。



    public class AtomicTest {
    private int i = 0;
    
    public void add() {
        i++;
    }
    
    public static void main(String[] args) {
        for (int t = 0; t < 10; t++) {
            AtomicTest test = new AtomicTest();
            Thread[] threads = new Thread[10];
            for (int i = 0; i < threads.length; i++) {
                threads[i] = new Thread(() -> {
                    for (int k = 0; k < 1000; k++) {
                        test.add();
                    }
                });
                threads[i].start();
            }
            Arrays.stream(threads).forEach(th -> {
                try {
                    th.join();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            });
            System.out.println("第" + (t + 1) + "次执行结果:" + test.i);
        }
    }
    }


```
第1次执行结果:8987
第2次执行结果:8970
第3次执行结果:6820
第4次执行结果:9841
第5次执行结果:10000
第6次执行结果:7766
第7次执行结果:8105
第8次执行结果:10000
第9次执行结果:10000
第10次执行结果:10000
```

最终的执行结果会是小于等于10000，在某些情况下与我们所期望的结果10000不符合，并发的情况下导致bug的产生。



二、可见性
    可见性是指当多个线程访问同一个变量时，一个线程修改了这个变量的值，其他线程能够立即看得到修改的值。CPU在执行代码的时候，为了减少变量访问的时间消耗可能将代码中访问的变量的值缓存到该CPU缓存区中，因此，相应的代码再次访问该变量的时候，相应的值可能从CPU缓存中而不是主内存中读取的。同样的，代码对这些被缓存过的变量的值的修改也可能仅是被写入CPU缓存区，而没有写入主内存。由于每个CPU都有自己的缓存区，因此一个CPU缓存区中的内容对于其他CPU而言是不可见的。这就导致了在其他CPU上运行的其他线程可能无法看到其他线程对某个变量值的修改。



    对于可见性，Java提供了volatile关键字来保证可见性。当一个共享变量被volatile修饰时，它会保证修改的值会立即被更新到主存，当有其他线程需要读取时，它会去内存中读取新值。而普通的共享变量不能保证可见性，因为普通共享变量被修改之后，什么时候被写入主存是不确定的，当其他线程去读取时，此时内存中可能还是原来的旧值，因此无法保证可见性。另外，通过synchronized和Lock也能够保证可见性，synchronized和Lock能保证同一时刻只有一个线程获取锁然后执行同步代码，并且在释放锁之前会将对变量的修改刷新到主存当中。因此可以保证可见性。

三、有序性（指令重排）
    有序性最终表述的现象是CPU是否按照既定代码顺序执行依次执行指令。编译器和CPU为了提高指令的执行效率可能会进行指令重排序，这使得代码的实际执行方式可能不是按照我们所认为的方式进行，在单线程的情况下只要保证最终执行结果正确即可。如下：

int i = 0;            //语句1  
boolean flag = false; //语句2
i = 1;                //语句3  
flag = true;          //语句4
上面代码最终执行结果是i=1、flag=true，在不影响这个结果的情况下语句2可能比语句1先执行，语句4可能比语句3先执行。此种指令重排之后单线程下不会有问题，单如果是在多线程的情况下呢？



```java
public class SerialTest {
    static SerialTest serialTest;
    static boolean isInit = false;
    public static void main(String[] args) {
        for(int i=0; i< 200;i++) {
            serialTest = null;
            isInit = false;
            new Thread(()->{
                serialTest = new SerialTest();//语句1
                isInit = true;                //语句2
            }).start();
            new Thread(()->{
                if(isInit) {
                    serialTest.doSomething();
                }
            }).start();
        }
    }

    public void doSomething() {
        System.out.println("doSomething");
    }
}
```



运行上面代码执行的结果如下：

```java
Exception in thread "Thread-283" java.lang.NullPointerException
	at com.cd.concurrent.SerialTest.lambda$main$1(SerialTest.java:25)
	at java.lang.Thread.run(Thread.java:748)
......
doSomething
doSomething
doSomething
doSomething
doSomething
Exception in thread "Thread-283" java.lang.NullPointerException
	at com.cd.concurrent.SerialTest.lambda$main$1(SerialTest.java:25)
	at java.lang.Thread.run(Thread.java:748)
```

我们所期望的结果应该是每次都会打印doSOmething，可是这里会报空指针异常，出现这种情况的原因就是因为指令重排导致，上面语句1和语句2最终执行顺序可能会变为语句2先执行，语句1还未执行，此时刚有有一个线程独到了isInit的值为true，此时通过对象取调用方法就报空指针，因为此时SerialTest对象还未被实例化。

指令重排序不会影响单个线程的执行，但是会影响到线程并发执行的正确性。也就是说，要想并发程序正确地执行，必须要保证原子性、可见性以及有序性。只要有一个没有被保证，就有可能会导致程序运行不正确。

在Java里面，可以通过volatile关键字来保证一定的“有序性”。另外可以通过synchronized和Lock来保证有序性，很显然，synchronized和Lock保证每个时刻是有一个线程执行同步代码，相当于是让线程顺序执行同步代码，自然就保证了有序性。另外，Java内存模型具备一些先天的“有序性”，即不需要通过任何手段就能够得到保证的有序性，这个通常也称为 happens-before 原则。如果两个操作的执行次序无法从happens-before原则推导出来，那么它们就不能保证它们的有序性，虚拟机可以随意地对它们进行重排序。

happens-before原则
程序次序规则：一个线程内，按照代码顺序，书写在前面的操作先行发生于书写在后面的操作。
锁定规则：一个unLock操作先行发生于后面对同一个锁额lock操作。
volatile变量规则：对一个变量的写操作先行发生于后面对这个变量的读操作。
传递规则：如果操作A先行发生于操作B，而操作B又先行发生于操作C，则可以得出操作A先行发生于操作C。
线程启动规则：Thread对象的start()方法先行发生于此线程的每个一个动作。
线程中断规则：对线程interrupt()方法的调用先行发生于被中断线程的代码检测到中断事件的发生。
线程终结规则：线程中所有的操作都先行发生于线程的终止检测，我们可以通过Thread.join()方法结束、Thread.isAlive()的返回值手段检测到线程已经终止执行。
对象终结规则：一个对象的初始化完成先行发生于他的finalize()方法的开始。

## 三、原子类与CAS

```shell
javap -c Demo.class
```

java里面++操作不是原子的

### AtomicLong

*  incrementAbdGet()先获取再自增;
*  如果只是自增操作没有必要用到锁锁很消耗性能
*  既安全性能又高不用加锁  

```java
package com.example.demo;

import lombok.Synchronized;

import java.net.InetAddress;
import java.net.UnknownHostException;
import java.util.*;
import java.util.concurrent.atomic.AtomicBoolean;
import java.util.concurrent.atomic.AtomicLong;

import static com.example.demo.Bar.value;


class Bar {
    public long val = 0;
    static AtomicLong value = new AtomicLong();
}

public class Foo {
    public volatile static boolean isRun = true;


    public static void main(String[] args) throws InterruptedException, UnknownHostException {
        Bar bar = new Bar();


        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000000; i++) {
                if (Foo.isRun) {
                    bar.val++;
                    if (value.incrementAndGet()==150000) {
                        Foo.isRun=false;
                    }
                }
            }
        });
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000000; i++) {
                if (Foo.isRun) {
                    bar.val++;
                    value.incrementAndGet();
                    if (value.incrementAndGet()==150000) {
                        Foo.isRun=false;
                    }
                }
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();
        System.out.println(bar.val);
        System.out.println(value);
    }

}

```











### CAS (比较并且交换cpu硬件级别的保证,原子性操作)

*  不能直接set,需要调用compareAndSet
*  

```
foo.val.compareAndSet(current, next)
```

*  用原子对象

```
//Master Slava Slave Slave Slave 荷载均衡 计数然后分别查询对应数据库

```

* 自旋

```java
package com.example.demo;

import java.util.concurrent.atomic.AtomicInteger;

public class Foo {
//    static  long val=0;//这个会有线程安全问题


    //调用次数
    private AtomicInteger val = new AtomicInteger();

    public static void main(String[] args) {
        //Master Slava Slave Slave Slave 荷载均衡 计数然后分别查询对应数据库
        Foo foo = new Foo();
        
        int current;
        int next;
         do {
             //获取的次数
             current = foo.val.incrementAndGet();
             //初始化数值,
             next=current>=Integer.MAX_VALUE?0:current+1;
             /*原子操作改变值,如果产生并发冲突会作废掉,并且重新执行*/
        }while(!foo.val.compareAndSet(current, next));
        /* 调用次数取余 */
        int db = current % 4;
    }
}

```



java自带

### 原子类有哪些



![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213066.png)



## 四、线程协作

* synchronized(){}同步锁中尽量少写代码提高速度
* orders.notify();//开启被等待的线程
* orders.wait();//等待通知



```java
package com.example.线程协作;

import java.util.Date;
import java.util.LinkedList;
import java.util.List;

import static cn.hutool.core.thread.ThreadUtil.sleep;

public class Example {
    static final List<String> orders = new LinkedList<>();

    public static void main(String[] args) {
        new Thread(() -> {
            while (true) {
                /*完成的时间越短冲突的几率越高*/
                synchronized (orders) {
                    orders.add(new Date().toString());
                    orders.notify();//开启被等待的线程
                }
                sleep(200);
            }
        }).start();
        new Thread(new Handle()).start();
        new Thread(new Handle()).start();
        new Thread(new Handle()).start();
        new Thread(new Handle()).start();
        new Thread(new Handle()).start();

    }

    public static void sleep(long t) {

        try {
            Thread.sleep(t);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    //在线程开始的时候直接调用run方法
    static class Handle implements Runnable {
        @Override
        public void run() {

            String order = null;
            while (true){

                synchronized (orders) {
                    if (orders.size() > 0) {
                        System.out.println("剩余数量"+orders.size());
                        // 删除并返回取到的订单
                        order = orders.remove(0);
                    }else {
                        System.out.println(Thread.currentThread().getId()+"没活干");
                        try {
                            orders.wait();//等待通知
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }

                //假设完成订单的时间为1秒
                if (order != null) {
                    sleep(1000);
                    //打印被处理掉的id
                    System.out.println(Thread.currentThread().getId()+ "处理完成"+order );
                    order = null;
                }
            }
        }
    }

}
```



## 五、锁

### 悲观锁(只能自己修改,修改完之后开开锁)

```
//开启事务
//select * from xxx where xxx for update 给符合条件的数据加锁
```

### 乐观锁(使用自旋,判断中途有没有被别人修改)

```
//select * from xxx where xx
//???
//version  2

//update xxx  set version=version+1  where xxx and version =2 //更新的时候如果被别人修改,使用自旋CAS
```

### synchronized 非公平锁(随机调用线程)

### ReentrantLock 公平锁(几乎一样)

*  lock.lock();加锁
*  lock.unlock;解锁
*  new ReentrantLock(true);设置公平状态

```java
package com.example.锁;

import java.util.Date;
import java.util.LinkedList;
import java.util.List;
import java.util.concurrent.locks.ReentrantLock;

public class Example {
    //设置为公平锁
    static  ReentrantLock lock =new ReentrantLock(true);
    static  int value=0;

    public static void main(String[] args) {
        new Thread(()->{
           lock.lock();
           //无论try里面成不成功都解锁
           try {
               //加锁
               value++;
           }finally {
               //解锁
               lock.unlock();
           }
        }).start();

        new Thread(()->{
           lock.lock();
           //无论try里面成不成功都解锁
           try {
               //加锁
               value++;
           }finally {
               //解锁
               lock.unlock();
           }
        }).start();
    }
}

```

### ReentrantLock可重入锁 (独占锁)

```java
//可重入锁 (独占锁)
static ReentrantLock myLock = new ReentrantLock(true);
static int value = 0;

public static void main(String[] args) throws InterruptedException {

    //cas不是锁,但是可以完成锁的一些功能
    //可重入锁
    myLock.lock();
    myLock.lock();

    new Thread(()->{
        System.out.println(1);
        myLock.lock();//会等待myLock的其他锁解锁
        System.out.println(2);
    });



    System.out.println("end" + value);
}
```

### ReadWriteLock(共享锁,独占锁)

```java
 //共享锁(ReadWriteLock)
 // readLock 共享锁 writeLock独占锁
static ReadWriteLock myLock=new ReentrantReadWriteLock();


 public static void main(String[] args) {
     //读锁只能读,(解锁之前)不能写
     //写锁只能写,(解锁之前)不能读,独占锁
     myLock.writeLock().lock();
     new Thread(()->{
         System.out.println("1");
         myLock.writeLock().lock();
         System.out.println("2");
     }).start();
     System.out.println("end");
     
     
     myLock.readLock().unlock();
 }
```



## 六、Java线程的创建方式

大A2022-02-28 18:16:02标签:文章110

一、继承Thread类，重写run()方法，实例化对象后调用start()方法

```java
public class Demo {
    public static void main(String[] args) {

        class Foo extends Thread {
            @Override
            public void run() {
                System.out.println("hello");
            }
        }

        Foo foo = new Foo();
        foo.start();
    }
}
```

二、实现 Runnable 接口，实现run() 方法。Thread类的构造方法可以接收一个实现了Runnable接口的对象

```java
public class Demo {
    public static void main(String[] args) {


        class Foo implements Runnable {

            @Override
            public void run() {
                System.out.println("hello");
            }
        }

        Foo foo = new Foo();

        Thread thread = new Thread(foo);
        thread.start();
    }
}
```

三、实现Callable接口实现call方法，配合FutureTask，能获取到线程中返回的值

```java
import java.util.concurrent.Callable;
import java.util.concurrent.FutureTask;

public class Demo {
    public static void main(String[] args) {


        class Foo implements Callable<String> {
            @Override
            public String call() throws Exception {
                System.out.println("hello");
                return "hi";
            }
        }

        Foo foo = new Foo();

        FutureTask<String> futureTask = new FutureTask<>(foo);

        Thread thread = new Thread(futureTask);
        thread.start();

        try {
            String res = futureTask.get();
            System.out.println(res);

        } catch (Exception e) {
            e.printStackTrace();
        }

    }
}
```

四、线程池

```java
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

public class Demo {
    public static void main(String[] args) {

        ThreadPoolExecutor poolExecutor = new ThreadPoolExecutor(
                3,   //corePoolSize 核心线程池大小
                5,   //maximumPoolSize 线程池最大数量 (如果使用了无界的任务队列这个参数就没什么效果)
                30,  //keepAliveTime 空闲存活的时间
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<Runnable>(5), // 任务队列(阻塞队列)
                new ThreadPoolExecutor.AbortPolicy()); //饱和策略

        poolExecutor.execute(new Runnable() {
            @Override
            public void run() {
                System.out.println("hello");
            }
        });
    }
}
```

比较

1、继承Thread类方式：

（1）优点：编写简单，任务类中访问当前线程时，可以直接使用this关键字。

（2）缺点：任务类即线程类已经继承了Thread类，所以不能再继承其他父类。

2、实现Runnable接口的方式：

（1）优点：任务类只实现了Runnable接口，还可以继承其他类。这种方式，可以多个线程对象共享一个任务类对象，即多线程共享一份资源的情况，如下：

```java
TestThread tt1 = new TestThread();
Thread t1 = new Thread(tt1);
Thread t2 = new Thread(tt1);
t1.start();
t2.start();
```

（2）缺点：编写稍微复杂，任务类中访问当前线程时，必须使用Thread.currentThread()方法。

3、通过Callable和Future的方式：

（1）优点：任务类只实现了Callable接口，还可以继承其他类，同样多线程下可共享同一份资源，这种方式还有返回值，并且可以抛出返回值的异常。

（2）缺点：编写稍微复杂，任务类中访问当前线程时，必须使用Thread.currentThread()方法。

3、线程池方式：

（1）优点：避免每次都创建和销毁线程的开销

（2）缺点：编写复杂，要考虑的因数较多







## 锁的原理

1. ### jvm 在对象中是否有三个区域 对象布局

```
//64bit jvm byte 在六十四位虚拟机
//1、至少需要对象属性 实例数据 不固定
//2.对象头                固定
//3.数据对齐     8字节的倍数 
```

![image-20220302144323313](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213067.png)

2. ### 什么是java的对象头  —-对象的第一个部分 公共部分

   

   书上java 对象头mark word =32bit=4byte  32/位虚拟机

   自己96bit =12byte   64位虚拟机

![image-20220302145625667](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213068.png)

3. ###   java对象头由什么组成

```
96bit  12byte
128bit 16byte




Mark word
class Metadata Address----
		1.Mark word?  	  64bit
		
		2.klass pointer/class metadata address 32bit
		指针压缩开启时32bit 不开启64bit
```



#### 什么是jvm ? 什么是hotpost?

当前使用的虚拟机是什么?

```
jvm(java虚拟机)--------规范/标准---规定了类由什么组成
hotspot--------产品实现 --- 实现了这个规范
```

规范:

![image-20220302152744012](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213069.png)

```
object.hashcode
```

![image-20220302155300444](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213070.png)

## 对象状态

1.无状态 new出来的时候   1111

2.偏向锁    1000

3.轻量缩     1100

4.重量锁  	0011

5.gc标记  	0000

![image-20220302160328229](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213071.png)

 

Java对象

分类专栏： JVM 文章标签： java jvm
版权

JVM
专栏收录该内容
12 篇文章1 订阅
订阅专栏
文章目录
对象实例化
对象的创建方式
对象的创建步骤
对象的创建过程
对象组成
查看对象的组成
对象头
实例数据
对齐填充数据
对象的访问定位
句柄访问
直接访问
对象的终止机制
对象实例化
对象的创建方式
使用new关键字创建：最常见的方式、单例类中调用getInstance的静态类方法，XXXFactory的静态方法；
使用反射方式创建：
使用Class的newInstance方法：在JDK9里面被标记为过时的方法，因为只能调用空参构造器；
使用Constructor的newInstance(XXX)：反射的方式，可以调用空参的，或者带参的构造器；
使用clone()：不调用任何的构造器，要求当前的类需要实现Cloneable接口中的clone接口；
使用序列化：序列化一般用于Socket的网络传输；
使用第三方库 Objenesis；
对象的创建步骤
创建对象代码演示及字节码指令

public class MainTest {
    public static void main(String[] args) {
        Object obj = new Object();
    }
}
1
2
3
4
5


创建对象步骤：

加载类元信息
为对象分配内存
处理并发问题
属性的默认初始化（零值初始化）
设置对象头信息
属性的显示初始化、代码块中初始化、构造器中初始化
对象的创建过程
判断对象对应的类是否加载、链接、初始化

虚拟机遇到一条new指令，首先去检查这个指令的参数能否在 Metaspace 的常量池中定位到一个类的符号引用，并且检查这个符号引用代表的类是否已经被加载，解析和初始化。（即判断类元信息是否存在）。

如果没有，那么在双亲委派模式下，使用当前类加载器以 ClassLoader + 包名 + 类名 为key进行查找对应的 .class文件，如果没有找到文件，则抛出 ClassNotFoundException 异常，如果找到，则进行类加载，并生成对应的Class对象。

为对象分配内存

首先计算对象占用空间的大小，接着在堆中划分一块内存给新对象。如果实例成员变量是引用类型，仅分配引用变量空间即可，即4个字节大小.

如果内存规整：指针碰撞；如果内存不规整：虚拟表需要维护一个列表，即空闲列表分配

指针碰撞:
所有用过的内存在一边，空闲的内存放另外一边，中间放着一个指针作为分界点的指示器，分配内存就仅仅是把指针指向空闲那边挪动一段与对象大小相等的距离罢了。
如果垃圾收集器选择的是Serial ，ParNew这种基于压缩算法的，虚拟机采用这种分配方式。一般使用带Compact（整理）过程的收集器时，使用指针碰撞。

空闲列表分配:
虚拟机维护了一个列表，记录上那些内存块是可用的，再分配的时候从列表中找到一块足够大的空间划分给对象实例，并更新列表上的内容。
这种分配方式成为了 “空闲列表（Free List）”。

选择哪种分配方式由Java堆是否规整所决定，而Java堆是否规整又由所采用的垃圾收集器是否带有压缩整理功能决定。

处理并发问题

采用CAS配上失败重试保证更新的原子性
每个线程预先分配TLAB - 通过设置 -XX:+UseTLAB参数来设置,在Java8是默认开启的
初始化分配到的内存

就是给对象属性赋值的操作

属性的默认初始化
显示初始化
代码块中的初始化
构造器初始化
给所有属性设置默认值，保证对象实例字段在不赋值时可以直接使用。

设置对象的对象头

将对象的所属类（即类的元数据信息）、对象的 HashCode 和对象的GC信息、锁信息等数据存储在对象的对象头中。这个过程的具体设置方式取决于JVM实现。

执行init方法进行初始化

初始化成员变量，执行实例化代码块，调用类的构造方法，并把堆内对象的首地址赋值给引用变量。
因此一般来说（由字节码中跟随 invokespecial 指令所决定），new指令之后会接着执行方法，把对象按照程序员的意愿进行初始化，这样一个真正可用的对象才算完成创建出来。

对象组成


查看对象的组成
引入依赖

<!-- 引入查看对象布局的依赖 -->
<dependency>
    <groupId>org.openjdk.jol</groupId>
    <artifactId>jol-core</artifactId>
    <version>0.9</version>
</dependency>
1
2
3
4
5
6
测试代码

public class MainTest {
    public static void main(String[] args) {
        //这个对象里面是空的什么都没有
        T t = new T();
        System.out.println(ClassLayout.parseInstance(t).toPrintable());
    }
}
class T{}
1
2
3
4
5
6
7
8
测试结果

 OFFSET  SIZE   TYPE DESCRIPTION                               VALUE
      0     4        (object header)                           01 00 00 00 (00000001 00000000 00000000 00000000) (1)
      4     4        (object header)                           00 00 00 00 (00000000 00000000 00000000 00000000) (0)
      8     4        (object header)                           a1 2c 01 20 (10100001 00101100 00000001 00100000) (536947873)
     12     4        (loss due to the next object alignment)
Instance size: 16 bytes
Space losses: 0 bytes internal + 4 bytes external = 4 bytes total
1
2
3
4
5
6
7
在64位JVM下,通过测试的结果我们可以看到Java对象的布局对象头占12byte,因为Jvm规定内存分配的字节必须是8的倍数,否则无法分配内存，所以就出现了，4byte的对齐数据。

通过测试发现，Java的对象布局包括：

必定存在一个对象头
如果分配的JVM分配的字节不是8的倍数的话，还要存在对齐数据
当该类里边有变量时,还包含实例变量
对象头
官方文档对于对象头的解释

object header
Common structure at the beginning of every GC-managed heap object.
(Every oop points to an object header.) Includes fundamental information about the heap object’s layout, type, GC state, synchronization state, and identity hash code.
Consists of two words. In arrays it is immediately followed by a length field.
Note that both Java objects and VM-internal objects have a common object header format.

大意：每个GC管理堆对象开始处的公共结构。(每个oop都指向一个对象头。)包括关于堆对象布局、类型、GC状态、同步状态和标识散列代码的基本信息。
由两个词组成。在数组中，它后面紧跟着一个长度字段。注意，Java对象和vm内部对象都有一个共同的对象头格式。

其中上面的两个词指的是

mark word
The first word of every object header. Usually a set of bitfields including synchronization state and identity hash code.
May also be a pointer (with characteristic low bit encoding) to synchronization related information.
During GC, may contain GC state bits.

大意：每个对象头文件的第一个字。通常是一组位域，包括同步状态和身份散列码。也可以是一个用于同步相关信息的指针(具有特征的低位编码)。在GC期间，可能包含GC状态位。

klass pointer
The second word of every object header. Points to another object (a metaobject) which describes the layout and behavior of the original object.
For Java objects, the “klass” contains a C++ style “vtable”.

大意：每个对象头文件的第二个字。指向另一个对象(元对象)，它描述了原始对象的布局和行为。对于Java对象，“klass”包含一个c++风格的“vtable”。

简单来说，对象头包含了包括两部分，分别是标志词(mark word)和类型指针(klass pointer)；如果是数组，还需要记录数组的长度。

引用上面在64位虚拟机下的测试结果，对象头中的这些二进制数字代表什么呢？

 OFFSET  SIZE   TYPE DESCRIPTION                               VALUE
      0     4        (object header)                           01 00 00 00 (00000001 00000000 00000000 00000000) (1)
      4     4        (object header)                           00 00 00 00 (00000000 00000000 00000000 00000000) (0)
      8     4        (object header)                           a1 2c 01 20 (10100001 00101100 00000001 00100000) (536947873)
1
2
3
4
在openjdk8-master中markOop.hpp，有对mark word的描述

//  32 bits:
//  --------
//             hash:25 ------------>| age:4    biased_lock:1 lock:2 (normal object)
//             JavaThread*:23 epoch:2 age:4    biased_lock:1 lock:2 (biased object)
//             size:32 ------------------------------------------>| (CMS free block)
//             PromotedObject*:29 ---------->| promo_bits:3 ----->| (CMS promoted object)
//
//  64 bits:
//  --------
//  unused:25 hash:31 -->| unused:1   age:4    biased_lock:1 lock:2 (normal object)
//  JavaThread*:54 epoch:2 unused:1   age:4    biased_lock:1 lock:2 (biased object)
//  PromotedObject*:61 --------------------->| promo_bits:3 ----->| (CMS promoted object)
//  size:64 ----------------------------------------------------->| (CMS free block)

在32位虚拟机下，正常的对象对象头的mark word，从前到后的顺序，25个位表示hash值，4位表示GC分代的年龄，1位偏向锁的信息，2位锁的状态；
在64位虚拟机下，正常的对象对象头的mark word，从前到后的顺序，25个未使用，31个位表示hash值，未使用1位，4位表示GC分代的年龄，1位偏向锁的信息，2位锁的状态；
64位虚拟机下对象头共12个字节(96bit)，mark word占8字节(64位)，所以klass pointer占4字节(32位)；

有些资料上显示: mark word占8字节(64位)，klass pointer也占8字节(64位)；
其实这种说法也正确，因为虚拟机默认开启了指针压缩，所以默认情况下klass pointer占4字节(32位)。

那么mark word64位中存放什么呢？

从上面可以看出，标志词（mark word）主要存放:

哈希值
GC分代年龄
锁状态标志
线程持有的锁
mark word会根据对象的不同状态存放的也不相同；

对象的状态

无状态：对象刚被new出来
偏向锁状态: 一个线程持有对象
轻量级锁状态
重量级锁状态
被垃圾回收器标记的状态


因为对象的状态是5种，而lock却是两位，两位最多能表示5种状态，那么对象的5种状态是怎么表示的？

对象的状态是联合用biased_lock: 1 和 lock: 2 表示的；例如：

biased_lock ：1 lock： 00： 表示无状态
biased_lock ：1 lock： 01： 表示偏向锁状态
biased_lock ：1 lock： 10： 表示轻量级锁状态
biased_lock ：1 lock： 11： 表示重量级锁状态
biased_lock ：0 lock： 00： 表示被垃圾回收器标记的状态
mark word在对象的不同状态下会有不同的表现形式，主要有三种状态，无锁状态、加锁状态、gc标记状态。

那么可以理解为Java当中的取锁其实可以理解是给对象上锁，也就是改变对象头的状态，如果上锁成功则进入同步代码块。但是Java当中的锁有分为很多种，从上图可以看出大体分为偏向锁、轻量锁、重量锁三种锁状态.

实例数据
独立于方法之外的变量,在类里定义的变量无 static 修饰；包括从父类继承下来的变量和本身拥有的字段。

一些规则：

相同宽度的字段总是被分配到一起（比如都是8个字节的，会放到一起）；
父类中定义的变量会出现在子类之前；
如果JVM参数CompactFields设置为true，子类的窄变量可能插入到父类的间隙；
对齐填充数据
不是必须的，也没有特别的含义，仅仅起到占位符的作用。
因为Jvm规定内存分配的字节必须是8的倍数,否则无法分配内存.如果对象头占得字节 + 实例变量占得字节刚好为8的倍数,对齐填充数据则不存在。

对象的访问定位
JVM是如何通过栈帧中的对象引用访问到其内部的对象实例呢？



hotspot使用的是直接访问。因为句柄访问开辟了句柄池，所以直接访问相较于句柄访问效率稍高一点。

句柄访问
句柄访问是在栈的局部变量表中，记录的对象的引用，然后在堆空间中开辟了一块空间，也就是句柄池。指向的是方法区中的对象类型数据。

优点：reference 中存储稳定句柄地址，对象被移动（垃圾收集时移动对象很普遍）时只会改变句柄中实例数据指针即可，reference 本身不需要被修改



直接访问
直接指针是局部变量表中的引用，直接指向堆中的实例，在对象实例中有类型指针，指向的是方法区中的对象类型数据。



对象的终止机制
Java语言提供了对象终止（finalization）机制来允许开发人员提供对象被销毁之前的自定义处理逻辑。
当垃圾回收器发现没有引用指向一个对象，即：垃圾回收此对象之前，总会先调用这个对象的finalize()方法。

finalize() 方法允许在子类中被重写，用于在对象被回收时进行资源释放。
通常在这个方法中进行一些资源释放和清理的工作，比如关闭文件、套接字和数据库连接等。

文档注释大意：当GC确定不再有对对象的引用时，由垃圾收集器在对象上调用。子类重写finalize方法来释放系统资源或执行其他清理。

   /**
     * Called by the garbage collector on an object when garbage collection
          * determines that there are no more references to the object.
          * A subclass overrides the {@code finalize} method to dispose of
               * system resources or to perform other cleanup.
               */
            protected void finalize() throws Throwable { }

永远不要主动调用某个对象的finalize方法应该交给垃圾回收机制调用原因

在调用finalize方法时时可能会导致对象复活；
finalize方法的执行时间是没有保障的，它完全由GC线程决定，极端情况下，若不发生GC，则finalize方法将没有执行机会;
因为优先级比较低，即使主动调用该方法，也不会因此就直接进行回收
一个糟糕的finalize方法会严重影响GC的性能;
由于finalize方法的存在,虚拟机中的对象一般处于三种可能的状态

如果从所有的根节点都无法访问到某个对象，说明对象己经不再使用了。一般来说，此对象需要被回收。
但事实上，也并非是“非死不可”的，这时候它们暂时处于“缓刑”阶段。一个无法触及的对象有可能在某一个条件下“复活”自己，如果这样，那么对它的回收就是不合理的，为此，虚拟机中定义了的对象可能的三种状态：

可触及的：从根节点开始，可以到达这个对象；对象存活被使用；
可复活的：对象的所有引用都被释放，但是对象有可能在finalize中复活；对象被复活，对象在finalize方法中被重新使用；
不可触及的：对象的finalize方法被调用，并且没有复活，那么就会进入不可触及状态；对象死亡，对象没有被使用；
只有在对象不可触及时才可以被回收。不可触及的对象不可能被复活，因为finalize()只会被调用一次。

finalize机制判定一个对象能否被回收过程

判定一个对象是否可回收，至少要经历两次标记过程：

如果对象没有没有引用链，则进行第一次标记
进行筛选，判断此对象是否有必要执行finalize方法
如果对象没有重写finalize方法，或者finalize方法已经被虚拟机调用过，则虚拟机视为“没有必要执行”，对象被判定为不可触及的。
如果对象重写了finalize方法，且还未执行过，那么会被插入到F-Queue队列中，由一个虚拟机自动创建的、低优先级的Finalizer线程触发其finalize方法执行。
finalize方法是对象逃脱死亡的最后机会，稍后GC会对F-Queue队列中的对象进行第二次标记。如果对象在finalize方法中与引用链上的任何一个对象建立了联系，那么在第二次标记时，该对象会被移出“即将回收”集合。
之后，对象会再次出现没有引用存在的情况。在这个情况下，finalize方法不会被再次调用，对象会直接变成不可触及的状态，也就是说，一个对象的finalize方法只会被调用一次。
代码演示对象能否被回收过程



    public class MainTest {
    public static MainTest var;
    
    /**
     * 此方法只能被调用一次
     * 可对该方法进行注释，来测试finalize方法是否能复活对象
     */
    @Override
    protected void finalize() throws Throwable {
        System.out.println("调用当前类重写的finalize()方法");
        // 复活对象 让当前带回收对象重新与引用链中的对象建立联系
        var = this;
    }
    
    public static void main(String[] args) throws InterruptedException {
        var = new MainTest();
        var = null;
        System.gc();
        System.out.println("-----------------第一次gc操作------------");
        // 因为Finalizer线程的优先级比较低，暂停2秒，以等待它
        Thread.sleep(2000);
        if (var == null) {
            System.out.println("对象已经死了");
            // 如果第一次对象就死亡了 就终止
            return;
        } else {
            System.out.println("对象还活着");
        }
    
        System.out.println("-----------------第二次gc操作------------");
        var = null;
        System.gc();
        // 下面代码和上面代码是一样的，但是 对象却自救失败了
        Thread.sleep(2000);
        if (var == null) {
            System.out.println("对象已经死了");
        } else {
            System.out.println("对象还活着");
        }
    }
    }

# Spring Framework

## 一、 Spring IOC

This chapter covers Spring’s Inversion of Control (IoC) container.

本章涵盖了Spring的控制（IOC）容器的反转。

*   通过依赖注入实现控制反转(DI)

*   POJO（Plain Ordinary Java Object）简单的Java对象，实际就是普通JavaBeans，
*   EJB  企业级的javabean

```
JavaBean 只是一个标准

所有属性都是私有的（使用getters/setters）
公共无参数构造函数
实现Serializable。(可以被序列化)
```

*   BeanFactory

```
BeanFactory API为Spring的IOC功能提供了基础。 其特定合同主要用于与Spring和相关的第三方框架的其他部分集成，其DefaultLableBeanFactory实现是高级泛级普通件内容容器中的密钥委托。
```

*   `ApplicationContext`

```
ApplicationContext(应用上下文)是beanFactory 创建的 bean工厂
```

.16.1. `BeanFactory` or `ApplicationContext`?

```json
You should use an `ApplicationContext` unless you have a good reason for not doing so, with `GenericApplicationContext` and its subclass `AnnotationConfigApplicationContext` as the common implementations for custom bootstrapping. These are the primary entry points to Spring’s core container for all common purposes: loading of configuration files, triggering a classpath scan, programmatically registering bean definitions and annotated classes, and (as of 5.0) registering functional bean definitions.
/*您应该使用“ApplicationContext`”，除非您有一个不错的原因，否则使用“genericApplicationContext`”和“子类”“注释”ConfigApplicationContext`为自定义引导的公共实现。这些是Spring的核心容器的主要条目点，用于所有常规目的：加载配置文件，触发类路径扫描，以编程方式注册Bean定义和注释类，以及（5.0）注册功能bean定义。*/
Because an `ApplicationContext` includes all the functionality of a `BeanFactory`, it is generally recommended over a plain `BeanFactory`, except for scenarios where full control over bean processing is needed. Within an `ApplicationContext` (such as the `GenericApplicationContext` implementation), several kinds of beans are detected by convention (that is, by bean name or by bean type — in particular, post-processors), while a plain `DefaultListableBeanFactory` is agnostic about any special beans.
/*因为`applicationContext在“ApplicationContext`中”（例如`GenericApplicationContext`），常规检测几种bean（即bean名称或bean类型 - 特别是处理器），而普通的`defaultListablebeactory`是关于任何特殊豆的不可知论。*/


For many extended container features, such as annotation processing and AOP proxying, the [`BeanPostProcessor` extension point](`https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-extension-bpp`) is essential. If you use only a plain `DefaultListableBeanFactory`, such post-processors do not get detected and activated by default. This situation could be confusing, because nothing is actually wrong with your bean configuration. Rather, in such a scenario, the container needs to be fully bootstrapped through additional setup.
/*对于许多扩展的容器功能，如注释处理和AOP代理，[`beanpost processor`扩展点]（https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans -  Factory-Extension-BPP）至关重要。如果您只使用普通的“defaultListableBeanFactory”，则默认情况下不会检测到此类后处理器并激活。这种情况可能会令人困惑，因为你的bean配置的东西实际上是错误的。相反，在这样的场景中，需要通过额外的设置完全启动容器。*/
```

The following table lists features provided by the `BeanFactory` and `ApplicationContext` interfaces and implementations.

| Feature                                                      | `BeanFactory` | `ApplicationContext` |
| :----------------------------------------------------------- | :------------ | :------------------- |
| Bean instantiation/wiring                                    | Yes           | Yes                  |
| Integrated lifecycle management                              | No            | Yes                  |
| Automatic `BeanPostProcessor` registration                   | No            | Yes                  |
| Automatic `BeanFactoryPostProcessor` registration            | No            | Yes                  |
| Convenient `MessageSource` access (for internationalization) | No            | Yes                  |
| Built-in `ApplicationEvent` publication mechanism            | No            | Yes                  |

To explicitly register a bean post-processor with a `DefaultListableBeanFactory`, you need to programmatically call `addBeanPostProcessor`, as the following example shows:

### 1、创建一个新的项目

**pom.xml**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.15</version>
    </dependency>
</dependencies>
```

**配置/src/main/resources/beans.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean name="fooService" class="com.example.FooService">
        <!--    不用改源代码 ，初始化类的属性值-->
        <property name="num" value="9999"></property>
        <!--    引用下面bean定义的barService的值 ref引用-->
        <property name="barService" ref="barService"></property>
        <!--    如果无参构造方法被顶用,可以使用这个来替换初始的null-->
        <constructor-arg ref="barService"></constructor-arg>  
    </bean>
    <bean id="barService" class="com.example.BarService"></bean>
</beans>
```

![image-20220223134040933](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213072.png)

```java
package com.example;

public class BarService {
}
```

```java
package com.example;

public class FooService {
    private   BarService barService;

    public BarService getBarService () {
        return barService;
    }

    public void setBarService ( BarService barService ) {
        this.barService = barService;
    }

    public FooService ( BarService barService ) {
        this.barService = barService;
    }

    private int num;

    public int getNum () {
        return num;
    }

    public void setNum ( int num ) {
        this.num = num;
    }

    public void test(){
        System.out.println(barService);
        System.out.println("foo-test"+num);
    }
}
```

```java
package com.example;

import org.springframework.beans.factory.BeanFactory;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Demo {
    public static void main ( String[] args ) {
//       一、配置文件应用上下文（到资源目录寻找上下文文件）
        FileSystemXmlApplicationContext /*BeanFactory*/ /*（应用上下文等于bean工厂）*/
                context = new FileSystemXmlApplicationContext("classpath:beans.xml");

//        二、类路径上下文
//        ClassPathXmlApplicationContext  context = new ClassPathXmlApplicationContext("beans.xml");

//         三、注解应用上下文
//        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext("beans.xml");

        FooService fooService = (FooService) context.getBean("fooService");
        System.out.println(fooService);
        fooService.test();
//        new FooService();
    }
}
```

### 2、注解应用上下文

```java
package com.example;

public class Foo {
}

```

```java
package com.example;

import org.springframework.context.annotation.Configuration;

@Configuration
public class Config {

}
```

```java
package com.example;

import org.springframework.beans.factory.BeanFactory;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Scope;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;
import org.springframework.stereotype.Component;

@Component
public class Demo {
    public static void main ( String  [] args ) {
//       一、配置文件应用上下文（到资源目录寻找上下文文件）
//        FileSystemXmlApplicationContext /*BeanFactory*/ /*（应用上下文等于bean工厂）*/
//                context = new FileSystemXmlApplicationContext("classpath:beans.xml");

//        二、类路径上下文
//        ClassPathXmlApplicationContext  context = new ClassPathXmlApplicationContext("beans.xml");

//         三、注解应用上下文    (配置扫描路径)
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext("com.example");

        FooService fooService = (FooService) context.getBean("fooService");
        System.out.println(fooService);
        fooService.test();
//        new FooService();
        //多次配置为同一个bean ，（bean是引用的、单例的(只有一个对象)、）
        System.out.println(context.getBean("foo")==context.getBean("foo"));
    }
    @Bean
    //加上prototype，则有多个例
    @Scope(value = "prototype")
    public  Foo foo(){
        return new Foo();
    }
}

```

```java
package com.example;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class FooService {
    @Autowired
    private   BarService barService;

    public BarService getBarService () {
        return barService;
    }

    public void setBarService ( BarService barService ) {
        this.barService = barService;
    }

//    public FooService ( BarService barService ) {
//        this.barService = barService;
//    }

    private int num;

    public int getNum () {
        return num;
    }

    public void setNum ( int num ) {
        this.num = num;
    }

    public void test(){
        System.out.println(barService);
        System.out.println("foo-test"+num);
    }
}

```



###  3、	bean的生命周期

| Scope                                                        | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [singleton](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-singleton) | (Default) Scopes a single bean definition to a single object instance for each Spring IoC container.（将单个bean定义视为每个Spring IoC容器的单个对象实例。） |
| [prototype](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-prototype) | Scopes a single bean definition to any number of object instances.（对任何数量的对象实例处理单个bean定义） |
| [request](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-request) | Scopes a single bean definition to the lifecycle of a single HTTP request. That is, each HTTP request has its own instance of a bean created off the back of a single bean definition. Only valid in the context of a web-aware Spring `ApplicationContext`.（将单个bean定义视为单个HTTP请求的生命周期。 也就是说，每个HTTP请求都有自己的bean的实例，从单个bean定义的背面创建。 仅在Web感知春季的上下文中有效地是ApplicationContext`的。） |
| [session](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-session) | Scopes a single bean definition to the lifecycle of an HTTP `Session`. Only valid in the context of a web-aware Spring `ApplicationContext`.（在http`会话的生命周期中缩放一个bean定义 。 仅在Web感知春季的上下文中有效地是ApplicationContext`的。） |
| [application](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#beans-factory-scopes-application) | Scopes a single bean definition to the lifecycle of a `ServletContext`. Only valid in the context of a web-aware Spring `ApplicationContext`.（在“servletContext”的生命周期中，将单个Bean定义。 仅在Web感知春季的上下文中有效地是ApplicationContext`的。） |
| [websocket](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#websocket-stomp-websocket-scope) | Scopes a single bean definition to the lifecycle of a `WebSocket`. Only valid in the context of a web-aware Spring `ApplicationContext`.(将单个bean定义划分为`websocket`的生命周期。 仅在Web感知春季的上下文中有效地是ApplicationContext`的。)da |

![组合设计模式](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213073.png)

### 4、动态代理

**sms(interface)**

```java
package com.example;

public interface Sms {
    boolean send(String mobile,String text);
}
```

**SmsTencentService**

```java
package com.example;

import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Service;

@Service
@Primary//优先运行这个代理
public class SmsTencentService implements  Sms {
    public boolean send (String mobile,String text){
        //post aliyun send
        System.out.println("post tencent send.......");
        return true;
    }
}
```

**SmsAliyunService**

```java
package com.example;

import org.springframework.stereotype.Service;

@Service
public class SmsAliyunService implements  Sms {
    public boolean send (String mobile,String text){
        //post aliyun send
        System.out.println("post aliyun send.......");
        return true;
    }
}
```

**Demo**

```java
package com.example;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.stereotype.Component;

@Component
public class Demo {
    public static void main ( String[] args ) {
//       一、配置文件应用上下文（到资源目录寻找上下文文件）
//        FileSystemXmlApplicationContext /*BeanFactory*/ /*（应用上下文等于bean工厂）*/
//                context = new FileSystemXmlApplicationContext("classpath:beans.xml");

//        二、类路径上下文
//        ClassPathXmlApplicationContext  context = new ClassPathXmlApplicationContext("beans.xml");

//         三、注解应用上下文    (配置扫描路径)
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext("com.example");

        FooService fooService = (FooService) context.getBean("fooService");
        System.out.println(fooService);
        fooService.test();
//        new FooService();
        //多次配置为同一个bean ，（bean是引用的、单例的(只有一个对象)、）
        System.out.println(context.getBean("foo") == context.getBean("foo"));

        Foo bean = context.getBean(Foo.class);
        System.out.println();

//可以调用代理来实现方法
//        SmsAliyunService smsAliyunService = context.getBean(SmsAliyunService.class);
//        System.out.println(smsAliyunService.send("1888888888", "短信内容"));

//动态代理 可以实现不同代理，只需要让所有代理实现一个共同的接口
        //@Primary//优先运行这个代理
        Sms sms = context.getBean(Sms.class);
        System.out.println(sms.send("1888888888" , "短信内容"));


        context.close();
        //java -jar xxx.jar
        //pid 2345
        //kill -9 2345


        //1、new
        //2、属性注入
        //3、实现接口(BeanNameAware) 应用上下文不是自己实现bean工厂接口
    }

    @Bean
    //加上prototype，则有多个例
//    @Scope(value = "prototype")
    public Foo foo () { 
        return new Foo();
    }
}
```

## 二、Spring AOP

**面向切面的编程**（对面向对象的一种增强）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>ioc</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.13</version>
        </dependency>
		
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>5.2.0.RELEASE</version>
        </dependency>

    </dependencies>


</project>
```

```java
package com.example;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;
import org.springframework.stereotype.Component;

@Configuration
@EnableAspectJAutoProxy//开启自动代理
public class Demo {
    public static void main ( String[] args ) {
//       一、配置文件应用上下文（到资源目录寻找上下文文件）
//        FileSystemXmlApplicationContext /*BeanFactory*/ /*（应用上下文等于bean工厂）*/
//                context = new FileSystemXmlApplicationContext("classpath:beans.xml");

//        二、类路径上下文
//        ClassPathXmlApplicationContext  context = new ClassPathXmlApplicationContext("beans.xml");

//         三、注解应用上下文    (配置扫描路径)
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext("com.example");

        FooService fooService = (FooService) context.getBean("fooService");
        System.out.println(fooService);
        fooService.test();
//        new FooService();
        //多次配置为同一个bean ，（bean是引用的、单例的(只有一个对象)、）
        System.out.println(context.getBean("foo") == context.getBean("foo"));

        Foo bean = context.getBean(Foo.class);
        System.out.println(bean);

//可以调用代理来实现方法
//        SmsAliyunService smsAliyunService = context.getBean(SmsAliyunService.class);
//        System.out.println(smsAliyunService.send("1888888888", "短信内容"));

//动态代理 可以实现不同代理，只需要让所有代理实现一个共同的接口
        //@Primary//优先运行这个代理
//        SMS sms = context.getBean(SMS.class);
        SMS sms =(SMS)context.getBean("smsAliyunService");
        System.out.println(sms.send("1888888888" , "短信内容"));
        //spring boot 用 JDK proxy 和 CGLIB 实现代理
        //用接口是 JDK proxy
        //不用接口是CGLIB 字节码增强
        context.close();
        //java -jar xxx.jar
        //pid 2345
        //kill -9 2345



        //1、new
        //2、属性注入
        //3、实现接口(BeanNameAware) 应用上下文不是自己实现bean工厂接口
      
    }

    @Bean
    //加上prototype，则有多个例
//    @Scope(value = "prototype")
    public Foo foo () {
        return new Foo();
    }
}
```

**动态代理**

```java
package com.example;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Service;

@Service
@Aspect/*切面 不生效则打开切面的自动代理*/
public class Log {
    //*不管返回什么都可以
    //send 方法名
    //..不管参数是什么都无所谓


    //    @Pointcut ("execution(* com.example.SMS.send(..)))")//拦截接口的send方法
    @Pointcut ("execution(public *  send(..)))") /*@Pointcut切入点*///拦截所有接口的send方法
    public void send () {

    }

//        @Before ("send()")//前置
//        @After ("send()") //后置
    @Around ("send()")//环绕
    public Object addLog ( ProceedingJoinPoint joinPoint ) throws Throwable {

        System.out.println("发短信开始");
        Object[] args = joinPoint.getArgs();
        for (Object o : args) {
            System.out.println(o);
        }
        Object proceed = joinPoint.proceed();
        System.out.println("发短信完毕");
        return proceed;
    }
}

```

## 三、Spring MVC Tomcat原理

D:\code\apache-tomcat-9.0.55\webapps\demo\WEB-INF

```java
import javax.servlet.Servlet;
import javax.servlet.http.HttpServletRequest;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class MyServer {
    public static void main ( String[] args ) throws IOException {
        int port = 8080;//开了一个8080的端口
        ServerSocket serverSocket = new ServerSocket(8080);
        System.out.println("MyServer port :" + port);
        while (true) {
            //接收的客户端，嵌套字
            Socket clientSocket = serverSocket.accept();
            try {
                handle(clientSocket);
            } catch (Exception e) {
                System.out.println(e.getMessage());
            }
        }

    }

    public static void handle ( Socket clientSocket ) throws IOException {
        InputStream inputStream = clientSocket.getInputStream();
        byte[] buffer = new byte[1024];//缓存区

        inputStream.read(buffer);
        String requestContent = new String(buffer);
        String firstLine = requestContent.substring(0 , requestContent.indexOf("\r\n"));
        System.out.println(firstLine);

        OutputStream outputStream = clientSocket.getOutputStream();
        outputStream.write("HTTP/1.0 200 OK\r\nCONTENT-Length:5\r\n\r\nhello".getBytes());
        clientSocket.close();
    }

    public static void handle2 ( Socket clientSocket ) throws IOException, ClassNotFoundException, InstantiationException, IllegalAccessException {
        InputStream inputStream = clientSocket.getInputStream();
        byte[] buffer = new byte[1024];//缓存区

        inputStream.read(buffer);//请求内容

        String requestContent = new String(buffer);
        String firstLine = requestContent.substring(0 ,  requestContent.indexOf("\r\n"));

//        System.out.println(requestContent);
        String[] arr = firstLine.split(" ");
        String method = arr[0];
        String path = arr[1];// /hi /hello servlet

        String className =path.substring(1,2).toUpperCase()+path.substring(2)+"Servlet";
    Servlet servlet=(Servlet)Class.forName(className).newInstance();
//    servlet.service(new HttpRequest(requestContent),new HttpResponse(clientSocket) );


        clientSocket.close();
    }


}

```

```java
public class HelloServlet implements Servlet{

    @Override
    public void service ( HttpRequest request , HttpResponse response ) {
        response.write("hello");
    }
}

```



### 一. 什么是 tomcat

优点

* 免费的、开放源代码的 web 应用服务器，属于轻量级应用服务器

  

  


tomcat 是一个符合 javaee web 标准的最小的 web 容器，所有的 jsp 程序一定要有 web 容器的支持才能运行，而且在给定的 web 容器里面都会支持事务处理操作。

 

tomcat 是由 apache 提供的（www.apache.org）提供的可以用安装版和解压版，安装版可以在服务中出现一个 tomcat 的服务，免安装没有，开发中使用免安装版。 tomcat 简单的说就是一个运行 java 的网络服务器，底层是 socket 的一个程序，它也是 jsp 和 servlet 的一个容器。 tomcat 是 apache 软件基金会（apache software foundation）的 jakarta 项目中的一个核心项目，由 apache、sun和其他一些公司及个人共同开发而成。

 

由于有了 sun 的参与和支持，最新的 servlet 和 jsp 规范总是能在 tomcat 中得到体现。因为 tomcat 技术先进、性能稳定，而且免费，因而深受 java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的 web 应用服务器。

 

 

tomcat 服务器是一个免费的开放源代码的 web 应用服务器，属于轻量级应用服务器， 在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试 jsp 程序的首选。 对于一个初学者来说，可以这样认为，当在一台机器上配置好 apache 服务器，可利用它响应 html（标准通用标记语言下的一个应用）页面的访问请求。实际上 tomcat 部分是 apache 服务器的扩展，但它是独立运行的，所以当你运行 tomcat 时，它实际上作为一个与 apache 独立的进程单独运行的。

 

 

当配置正确时，apache 为 html 页面服务，而 tomcat 实际上是在运行 jsp 页面和 servlet。另外，tomcat 和 iis 等 web 服务器一样，具有处理 html 页面的功能，另外它还是 一个 servlet 和 jsp 容器，独立的 servlet 容器是 tomcat 的默认模式。不过，tomcat 处理静态 html 的能力不如 apache 服务器。目前 tomcat 最新版本为 9.0。

 

### 二. 安装 tomcat

运行 tomcat 需要 jdk 的支持【tomcat 会通过 java_home 找到所需要的 jdk】。 安装就是解压缩过程。启动 tomcat，能访问则算安装好了

 

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213074.jpg)

 

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213075.jpg)

 

2、root 目录中查看 index.html 或 index.jsp 文件

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213076.jpg)

 

tomcat8 中自带了页面，而 tomcat7 免安装下没有，如果直接访问会出 404 tomcat7.xxx 则需要查看 webapps->root 目录中是否有 index.html 或者 index.jsp，如果没有则自己手动添 加一个 html 文件或者到其他地方拷贝一份 jsp，此时能访问该页面则是配置成功。

 x

3、启动 tomcat (在 tomcat 的安装目录下的 bin 目录 使用命令行启动 tomcat)

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213077.jpg)

 

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213078.jpg)

启动后该启动窗口不能关

 

4、打开浏览器输入 http://localhost:8080/访问

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213079.jpg)

 

ok tomcat 安装成功。

 

5、调用shutdown命令关闭 tomcat

 

### 三. tomcat 目录结构

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213080.jpg)

 

\1. bin：启动和关闭 tomcat 的 bat 文件

\2. conf：配置文件server.xml 该文件用于配置 server 相关的信息，比如 tomcat 启动的端口号，配置主机(host) web.xml 文件配置与 web 应用（web 应用相当于一个 web 站点）tomcat-user.xml 配置用户名密码和相关权限.

\3. lib：该目录放置运行 tomcat 运行需要的 jar 包

\4. logs：存放日志，当我们需要查看日志的时候，可以查询信息

\5. webapps：放置我们的 web 应用

\6. work 工作目录：该目录用于存放 jsp 被访问后生成对应的 server 文件和.class 文件

### 四. eclipse 关联 tomcat

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213081.jpg)

感谢阅读乐字节技术文章，请继续关注乐字节，更多java技术文章奉上，下篇将给大家带来http协议的详细介绍。

##  四、构建mvc项目

（https://i.csdn.net/#/user-center/collection-list?type=1)

###  一、使用idea基于maven创建SpringMVC项目

（创建太慢可能是下载速度的原因可以添加属性`name: archetypeCatalog ,value: internal`可以加快下载速度）

首先我们可以创建[maven](https://so.csdn.net/so/search?q=maven&spm=1001.2101.3001.7020)项目，`file-> new ->project->maven`
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610144105145.png)
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213082.png)
如果下载不较慢，可以添加属性`name: archetypeCatalog ,value: internal`可以加快下载速度
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610144903544.png)
在选择自己的maven时。默认的下载存储位置是在C盘，可以打开配置文件更改为自己的下载位置：`<localRepository>E:\Program Files\apache-maven-3.6.1\repository_file</localRepository>`
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610145441194.png)

![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610145420325.png)
项目创建完成后你会看到，其中java、resources和test文件夹没有就自己创建，
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213083.png)
创建好了之后是灰色的,需要`选中相应的文件夹右键 选择Mark Directory as 点击相应的颜色即可`
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610150136852.png)
打开pom.xml文件，添加各类依赖，将下面的代码复制到标签中（这些是我添加的依赖，做个参考)，添加完成之后，等待maven将这些jar下载完毕，下载完成后，可以看到External Library下多了很多文件

```
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.7</maven.compiler.source>
        <maven.compiler.target>1.7</maven.compiler.target>

        <!--spring 版本号-->
        <spring.version>5.1.6.RELEASE</spring.version>

        <!--mybatis 版本号-->
        <mybatis.version>3.2.4</mybatis.version>
    </properties>
    <!--上边介绍的的版本号等等 将下面的代码放到dependencies标签中即可-->

        <!--spring 核心包-->
        <!-- spring start -->
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-core</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-web</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-oxm</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-tx</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-jdbc</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-aop</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context-support</artifactId>
          <version>${spring.version}</version>
        </dependency>
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-test</artifactId>
          <version>${spring.version}</version>
        </dependency>

        <!-- spring end -->

        <!--mybatis核心包-->
        <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis</artifactId>
          <version>${mybatis.version}</version>
        </dependency>

        <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.11</version>
          <scope>test</scope>
        </dependency>
        <!--日志-->
        <!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-log4j12 -->
        <dependency>
          <groupId>org.slf4j</groupId>
          <artifactId>slf4j-log4j12</artifactId>
          <version>1.8.0-alpha0</version>
          <scope>test</scope>
        </dependency>


        <!--j2ee相关包 servlet、jsp、jstl-->
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>4.0.0</version>
          <scope>provided</scope>
        </dependency>
        <dependency>
          <groupId>javax.servlet.jsp</groupId>
          <artifactId>jsp-api</artifactId>
          <version>2.2</version>
        </dependency>
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>jstl</artifactId>
          <version>1.2</version>
        </dependency>

        <!--mybatis/spring 包-->
        <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis-spring</artifactId>
          <version>1.2.2</version>
        </dependency>

        <!--MySQL 驱动包-->
        <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>5.1.39</version>
        </dependency>


        <dependency>
          <groupId>org.apache.maven</groupId>
          <artifactId>maven-model</artifactId>
          <version>3.0</version>
        </dependency>

        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>3.1.0</version>
        </dependency>

    123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899100101102103104105106107108109110111112113114115116117118119120121122123124125126127128129130131
```

之后添加springMVC框架，右击项目文件夹Demo，选择Add framework support
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213084.png)
将下图中的[Spring](https://so.csdn.net/so/search?q=Spring&spm=1001.2101.3001.7020)和Spring下的Spring MVC都勾上，之前配置pom.xml文件时，已经自动下载了spring相关文件，所以这里就直接用之前下载好的就可以了，OK。（注意：点了Add framework support之后，在下图中有可能会找不到Spring，解决办法在下图的下方）
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213085.png)
如果在Add framework support中找不到Spring，那是因为项目中可能已经存在Spring相关文件，但不一定是完善的。因此我们要将已经存在的Spring给删掉，重新添加，方法如下：

点击File，选择[Project](https://so.csdn.net/so/search?q=Project&spm=1001.2101.3001.7020) Structure，（**快捷键ctrl+shift+alt+s**）选择Facets，就会看到有一个Spring啦，右击它，点删除就行啦，然后再回到上面第3步重新Add framework support，Spring就会出现啦。
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610151339783.png)
Spring框架添加完之后，会看到目录下多了两个xml文件，我还创建了static文件夹用来存放静态资源css、js、images（图片等），和views文件夹用来存放映射文件（例如[JSP](https://so.csdn.net/so/search?q=JSP&spm=1001.2101.3001.7020)）
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213086.png)
其中java文件是用来建包的，现在可以对SpringMVC进行设置了，首先配置web.xml 。他自己自动生成的可能不是这种，直接用下面的替换就可以了

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">

    <display-name>Archetype Created Web Application</display-name>
    <!--welcome pages-->
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <!--配置springmvc DispatcherServlet-->
    <servlet>
        <servlet-name>springMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <!--配置dispatcher.xml作为mvc的配置文件-->
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/dispatcher-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
        <async-supported>true</async-supported>
    </servlet>

    <!--<servlet>-->
        <!--<servlet-name>EmpServlet</servlet-name>-->
        <!--<servlet-class>com.gx.filter.EmpServlet</servlet-class>-->
    <!--</servlet>-->

    <servlet-mapping>
        <servlet-name>springMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    <!--把applicationContext.xml加入到配置文件中-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/applicationContext.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
</web-app>
12345678910111213141516171819202122232425262728293031323334353637383940414243
```

配置dispatcher-servlet.xml，负责[mvc](https://so.csdn.net/so/search?q=mvc&spm=1001.2101.3001.7020)的配置

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:mvc="http://www.springframework.org/schema/mvc"
      xmlns:context="http://www.springframework.org/schema/context"
      xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

   <!--此文件负责整个mvc中的配置-->

   <!--启用spring的一些annotation -->
   <context:annotation-config/>

   <!-- 配置注解驱动 可以将request参数与绑定到controller参数上 -->
   <mvc:annotation-driven/>

   <!--静态资源映射-->
   <!--本项目把静态资源放在了webapp的statics目录下，资源映射如下-->
   <mvc:resources mapping="/css/**" location="/static/css/"/>
   <mvc:resources mapping="/js/**" location="/static/js/"/>
   <mvc:resources mapping="/image/**" location="/static/images/"/>
   <mvc:default-servlet-handler />  <!--这句要加上，要不然可能会访问不到静态资源，具体作用自行百度-->

   <!-- 对模型视图名称的解析，即在模型视图名称添加前后缀(如果最后一个还是表示文件夹,则最后的斜杠不要漏了) 使用JSP-->
   <!-- 默认的视图解析器 在上边的解析错误时使用 (默认使用html)- -->
   <bean id="defaultViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
       <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
       <property name="prefix" value="/WEB-INF/views/"/><!--设置JSP文件的目录位置-->
       <property name="suffix" value=".jsp"/>
       <property name="exposeContextBeansAsAttributes" value="true"/>
   </bean>

   <!-- 自动扫描装配 -->
   <context:component-scan base-package="com.gx.controller"/>

</beans>
12345678910111213141516171819202122232425262728293031323334
```

配置applicationContext.xml，负责一些非MVC组件的配置，暂时没有所以是空的，但也可以扫描一下

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="com.gx"/>

</beans>
123456789
```

以上就是配置好了 可以创建文件使用了哦！亲测可用



选择tomcat 选择工件 之后选第二个

![image-20220225112536332](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213087.png)

### 二、运行servIce nactive

### 0、参考资料

首先我们可以创建[maven](https://so.csdn.net/so/search?q=maven&spm=1001.2101.3001.7020)项目，`file-> new ->project->maven`
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610144105145.png)
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213082.png)
如果下载不较慢，可以添加属性`name: archetypeCatalog ,value: internal`可以加快下载速度
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610144903544.png)
在选择自己的maven时。默认的下载存储位置是在C盘，可以打开配置文件更改为自己的下载位置：`<localRepository>E:\Program Files\apache-maven-3.6.1\repository_file</localRepository>`
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610145441194.png)

![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610145420325.png)
项目创建完成后你会看到，其中java、resources和test文件夹没有就自己创建，
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213083.png)
创建好了之后是灰色的,需要`选中相应的文件夹右键 选择Mark Directory as 点击相应的颜色即可`
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610150136852.png)
打开pom.xml文件，添加各类依赖，将下面的代码复制到标签中（这些是我添加的依赖，做个参考)，添加完成之后，等待maven将这些jar下载完毕，下载完成后，可以看到External Library下多了很多文件

```
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>

    <!--spring 版本号-->
    <spring.version>5.1.6.RELEASE</spring.version>

    <!--mybatis 版本号-->
    <mybatis.version>3.2.4</mybatis.version>
</properties>
<!--上边介绍的的版本号等等 将下面的代码放到dependencies标签中即可-->

    <!--spring 核心包-->
    <!-- spring start -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-oxm</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <!-- spring end -->

    <!--mybatis核心包-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>${mybatis.version}</version>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
    <!--日志-->
    <!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-log4j12 -->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
      <version>1.8.0-alpha0</version>
      <scope>test</scope>
    </dependency>


    <!--j2ee相关包 servlet、jsp、jstl-->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.0</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.2</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>

    <!--mybatis/spring 包-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.2.2</version>
    </dependency>

    <!--MySQL 驱动包-->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.39</version>
    </dependency>


    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-model</artifactId>
      <version>3.0</version>
    </dependency>

    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
    </dependency>


```

之后添加springMVC框架，右击项目文件夹Demo，选择Add framework support
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213084.png)
将下图中的[Spring](https://so.csdn.net/so/search?q=Spring&spm=1001.2101.3001.7020)和Spring下的Spring MVC都勾上，之前配置pom.xml文件时，已经自动下载了spring相关文件，所以这里就直接用之前下载好的就可以了，OK。（注意：点了Add framework support之后，在下图中有可能会找不到Spring，解决办法在下图的下方）
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213085.png)
如果在Add framework support中找不到Spring，那是因为项目中可能已经存在Spring相关文件，但不一定是完善的。因此我们要将已经存在的Spring给删掉，重新添加，方法如下：

点击File，选择[Project](https://so.csdn.net/so/search?q=Project&spm=1001.2101.3001.7020) Structure，（**快捷键ctrl+shift+alt+s**）选择Facets，就会看到有一个Spring啦，右击它，点删除就行啦，然后再回到上面第3步重新Add framework support，Spring就会出现啦。
![在这里插入图片描述](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/150-Spring%2520Framework/20190610151339783.png)
Spring框架添加完之后，会看到目录下多了两个xml文件，我还创建了static文件夹用来存放静态资源css、js、images（图片等），和views文件夹用来存放映射文件（例如[JSP](https://so.csdn.net/so/search?q=JSP&spm=1001.2101.3001.7020)）
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213086.png)
其中java文件是用来建包的，现在可以对SpringMVC进行设置了，首先配置web.xml 。他自己自动生成的可能不是这种，直接用下面的替换就可以了

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">

    <display-name>Archetype Created Web Application</display-name>
    <!--welcome pages-->
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <!--配置springmvc DispatcherServlet-->
    <servlet>
        <servlet-name>springMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <!--配置dispatcher.xml作为mvc的配置文件-->
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/dispatcher-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
        <async-supported>true</async-supported>
    </servlet>

    <!--<servlet>-->
        <!--<servlet-name>EmpServlet</servlet-name>-->
        <!--<servlet-class>com.gx.filter.EmpServlet</servlet-class>-->
    <!--</servlet>-->

    <servlet-mapping>
        <servlet-name>springMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    <!--把applicationContext.xml加入到配置文件中-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/applicationContext.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
</web-app>
12345678910111213141516171819202122232425262728293031323334353637383940414243
```

配置dispatcher-servlet.xml，负责[mvc](https://so.csdn.net/so/search?q=mvc&spm=1001.2101.3001.7020)的配置

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:mvc="http://www.springframework.org/schema/mvc"
      xmlns:context="http://www.springframework.org/schema/context"
      xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

   <!--此文件负责整个mvc中的配置-->

   <!--启用spring的一些annotation -->
   <context:annotation-config/>

   <!-- 配置注解驱动 可以将request参数与绑定到controller参数上 -->
   <mvc:annotation-driven/>

   <!--静态资源映射-->
   <!--本项目把静态资源放在了webapp的statics目录下，资源映射如下-->
   <mvc:resources mapping="/css/**" location="/static/css/"/>
   <mvc:resources mapping="/js/**" location="/static/js/"/>
   <mvc:resources mapping="/image/**" location="/static/images/"/>
   <mvc:default-servlet-handler />  <!--这句要加上，要不然可能会访问不到静态资源，具体作用自行百度-->

   <!-- 对模型视图名称的解析，即在模型视图名称添加前后缀(如果最后一个还是表示文件夹,则最后的斜杠不要漏了) 使用JSP-->
   <!-- 默认的视图解析器 在上边的解析错误时使用 (默认使用html)- -->
   <bean id="defaultViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
       <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
       <property name="prefix" value="/WEB-INF/views/"/><!--设置JSP文件的目录位置-->
       <property name="suffix" value=".jsp"/>
       <property name="exposeContextBeansAsAttributes" value="true"/>
   </bean>

   <!-- 自动扫描装配 -->
   <context:component-scan base-package="com.gx.controller"/>

</beans>
12345678910111213141516171819202122232425262728293031323334
```

配置applicationContext.xml，负责一些非MVC组件的配置，暂时没有所以是空的，但也可以扫描一下

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="com.gx"/>

</beans>
123456789
```

以上就是配置好了 可以创建文件使用了哦！亲测可用



###  1、引入依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.example</groupId>
  <artifactId>untitled1</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <name>untitled1 Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>

    <!--spring 版本号-->
    <spring.version>5.3.15</spring.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13.2</version>
      <scope>test</scope>
    </dependency>
    <!--spring 核心包-->
    <!-- spring start -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-oxm</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <!-- spring end -->
  </dependencies>

  <build>
    <finalName>untitled1</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

### 2、运行spring mvc

![image-20220225140046490](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213088.png)

![image-20220225153843142](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213089.png)



# 高并发架构

## 一.缓存Cache

### 常见的使用缓存方式有：

- 文件缓存
- 堆内缓存（Caffeine 、Ehcache、Guava Cache）
- 堆外缓存（Ehcache、MapDB）
- 分布式缓存（Redis、 Memcached)

### StringBoot中使用Caffeine/Redis缓存

Caffeine 是基于Java 8的一个高性能本地缓存库

http://www.daimaku.net/post/view/11304

#### 添加依赖

`pom.xml` 中添加

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-cache</artifactId>
</dependency>

<!-- https://github.com/ben-manes/caffeine -->
<dependency>
  <groupId>com.github.ben-manes.caffeine</groupId>
  <artifactId>caffeine</artifactId>
  <version>2.8.8</version>
</dependency>
```



#### 配置缓存

配置缓存类型`application.properties`

```
# 缓存类型
spring.cache.type=caffeine

# 初始缓存空间大小, 缓存的最大条数, 过期时间
# 这种方式不方便针对每个cache配置不同的参数，推荐使用下面的CacheConfig类来配置
# spring.cache.caffeine.spec=initialCapacity=50,maximumSize=500,expireAfterWrite=30s
```

添加一个CacheConfig类，配置缓存空间名称和过期时间，示例中配置了两种缓存(bookCache、findUserByToken)

```
import com.github.benmanes.caffeine.cache.Caffeine;
import org.springframework.cache.CacheManager;
import org.springframework.cache.caffeine.CaffeineCache;
import org.springframework.cache.support.SimpleCacheManager;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Primary;

import java.util.ArrayList;
import java.util.concurrent.TimeUnit;

@Configuration
public class CacheConfig {
    private static final int DEFAULT_MAXSIZE = 50000;  // 缺省最大容量50000
    private static final int DEFAULT_TTL = 10;         // 缺省10秒

    /**
     * 定义cache名称、过期时间（秒）、最大容量
     * 每个cache缺省：10秒超时、最多缓存50000条数据，需要修改可以在构造方法的参数中指定
     */
    public enum Caches {
        bookCache(60, 50),           // 图书缓存(60秒，最大缓存条数50)
        findUserByToken(30, 100),    // 通过token查用户，缓存30秒，最大容量100条
        ;


        Caches() {
        }

        Caches(int ttl) {
            this.ttl = ttl;
        }

        Caches(int ttl, int maxSize) {
            this.ttl = ttl;
            this.maxSize = maxSize;
        }

        private int maxSize = DEFAULT_MAXSIZE;    // 最大數量
        private int ttl = DEFAULT_TTL;            // 过期时间（秒）

        public int getMaxSize() {
            return maxSize;
        }

        public int getTtl() {
            return ttl;
        }
    }

    /**
     * 创建基于 Caffeine 的 Cache Manager
     */
    @Bean
    @Primary
    public CacheManager caffeineCacheManager() {
        SimpleCacheManager cacheManager = new SimpleCacheManager();

        ArrayList<CaffeineCache> caches = new ArrayList<>();

        for (Caches c : Caches.values()) {
            caches.add(new CaffeineCache(c.name(),
                    Caffeine.newBuilder().recordStats()
                            .expireAfterWrite(c.getTtl(), TimeUnit.SECONDS)
                            .maximumSize(c.getMaxSize())
                            .build())
            );
        }

        cacheManager.setCaches(caches);

        return cacheManager;
    }
}
```

#### 开启缓存

```
import org.springframework.cache.annotation.EnableCaching;

@SpringBootApplication
@EnableCaching
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

#### 编码方式使用缓存

```
import org.springframework.cache.CacheManager;

@Autowired
CacheManager cacheManager;

Cache cache = cacheManager.getCache("bookCache");

// 把book对象放入缓存，key为book:1
cache.put("book:1",  new Book(1, "Java语言规范"));

// 从缓存中获取数据
Cache.ValueWrapper value = cache.get("book:1");
```



#### 注解方式使用缓存

在Service的方法中开启缓存

```java
@Cacheable(cacheNames = "bookCache", key = "'bookId:' + #id")
public Book findBookById(int id) {
  System.out.println("query book from db");
  return bookMapper.findById(id);
}

@Cacheable(cacheNames = "findUserByToken", key = "targetClass + #token")
public User findUserByToken(String token) {
  System.out.println("query user from db");
  return userMapper.findByToken(token);
}
```

`@Cacheable`的`cacheNames`(也可以用别名`value`)表示在配置中定义的缓存空间名称，`key`为缓存的标识，用于区分不同的缓存数据(缺省按照方法的`所有参数进行组合`)，可以使用`targetClass`、`method`分别代表当前类名和方法名

缓存对象需要可序列化

```java
public class Book implements Serializable {}

public class User implements Serializable {}
```

### 切换为Reids缓存

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

### application.properties

```
spring.cache.type=redis
```

### CacheConfig

```java
import org.springframework.cache.CacheManager;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Primary;
import org.springframework.data.redis.cache.RedisCacheConfiguration;
import org.springframework.data.redis.cache.RedisCacheManager;
import org.springframework.data.redis.cache.RedisCacheWriter;
import org.springframework.data.redis.connection.RedisConnectionFactory;

import java.time.Duration;


@Configuration
public class CacheConfig {
    private static final int DEFAULT_MAXSIZE = 50000;  // 缺省最大容量50000
    private static final int DEFAULT_TTL = 10;         // 缺省10秒

    /**
     * 定义cache名称、过期时间（秒）、最大容量
     * 每个cache缺省：10秒超时、最多缓存50000条数据，需要修改可以在构造方法的参数中指定
     */
    public enum Caches {
        bookCache(60, 50),           // 图书缓存(60秒，最大缓存条数50)
        findUserByToken(30, 100),    // 通过token查用户，缓存30秒，最大容量100条
        ;


        Caches() {
        }

        Caches(int ttl) {
            this.ttl = ttl;
        }

        Caches(int ttl, int maxSize) {
            this.ttl = ttl;
            this.maxSize = maxSize;
        }

        private int maxSize = DEFAULT_MAXSIZE;    // 最大數量
        private int ttl = DEFAULT_TTL;            // 过期时间（秒）

        public int getMaxSize() {
            return maxSize;
        }

        public int getTtl() {
            return ttl;
        }
    }

    /**
     * 创建基于 Redis 的 Cache Manager
     */
    @Bean
    @Primary
    public CacheManager caffeineCacheManager(RedisConnectionFactory connectionFactory) {
        RedisCacheManager.RedisCacheManagerBuilder builder = RedisCacheManager
                .builder(RedisCacheWriter.nonLockingRedisCacheWriter(connectionFactory))
                .cacheDefaults(RedisCacheConfiguration.defaultCacheConfig().entryTtl(Duration.ofSeconds(DEFAULT_TTL)));

        for (Caches c : Caches.values()) {
            builder.withCacheConfiguration(c.name(), RedisCacheConfiguration.defaultCacheConfig()
                    .entryTtl(Duration.ofSeconds(c.getTtl())));
        }

        return builder.build();
    }


}
```



如果使用Redis后，报错：

```xml
java.lang.ClassCastException: Book  cannot be cast to Book
```

pom.xml 中 删除 `spring-boot-devtools` 试试。原因是类加载器不相同

```xml
org.springframework.boot.devtools.restart.classloader.RestartClassLoader

sun.misc.Launcher$AppClassLoader
```





















## 二.消息队列MQ

### 常见的消息队列有：

**注意** :线程如果存在就不需要new ,

- ActiveMQ
- RabbitMQ
- Kafka
- RocketMQ



### Ubuntu下安装步骤如下：

重新安装虚拟机推荐安装在d盘,出现跳过则跳过

接下来，我们主要掌握 RabbitMQ，官方文档 https://www.rabbitmq.com/

```cmd
# 更新源
$ sudo apt-get update

# 安装 RabbitMQ
$ sudo apt-get install rabbitmq-server

# 添加 admin 用户， 密码设置为 admin123
$ sudo rabbitmqctl add_user admin admin123

# 将 admin 用户设置为管理员角色
$ sudo rabbitmqctl set_user_tags admin administrator

# 设置 admin 赋权
$ sudo rabbitmqctl set_permissions -p / admin '.*' '.*' '.*'

# 启用图形管理界面
$ sudo rabbitmq-plugins enable rabbitmq_management
```



![image-20220304152552413](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213090.png)

安装完成后，管理界面在15672端口，浏览器访问

[http://your-rabbitmq-server-ip:15672](http://your-rabbitmq-server-ip:15672/)

```
ifconfig -a  -查看ip
http://192.168.19.129:15672/#/
```

服务管理命令

```
sudo service rabbitmq-server stop
sudo service rabbitmq-server start
sudo service rabbitmq-server restart
```



![](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213091.png)



```java
package com.example.demo.service;

import com.rabbitmq.client.*;
import lombok.Data;

import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.util.concurrent.TimeoutException;
@Data
public class Demo {
    static  final  String host="192.168.19.129";
    static  final  int port=5672;
    static final String username= "admin";
    static final String password= "admin123";

    private static String ranks="msg";//消息队伍类型
    private static String  message="hello,jack";//消息内容

    public static void main(String[] args) throws IOException, TimeoutException {
//        for (int i = 0; i < 100; i++) {
//            publish1();
//        publish2();
//        }


        consume();
    }


    private static void publish1() throws IOException, TimeoutException {
        //创建连接工厂
        ConnectionFactory factory = new ConnectionFactory();

        factory.setUsername(username);
        factory.setPassword(password);

        //设置 RabbitMQ 地址
        factory.setHost(host);
        factory.setPort(port);

        //建立到代理服务器到连接
        Connection conn = factory.newConnection();

        //获得信道
        Channel channel = conn.createChannel();

        //声明队列。
        //参数1：队列名
        //参数2：持久化 （true表示是，队列将在服务器重启时依旧存在）
        //参数3：独占队列（创建者可以使用的私有队列，断开后自动删除）
        //参数4：当所有消费者客户端连接断开时是否自动删除队列
        //参数5：队列的其他参数
        channel.queueDeclare(ranks, true, false, false, null);

        //发布消息
//        String message = "hello";

        // 基本发布消息
        // 第一个参数为交换机名称(空)
        // 第二个参数为队列映射的路由key(直接使用队列名)
        // 第三个参数为消息的其他属性、
        // 第四个参数为发送信息的主体
        channel.basicPublish("", ranks, MessageProperties.MINIMAL_PERSISTENT_BASIC, message.getBytes(StandardCharsets.UTF_8));

        channel.close();
        conn.close();
    }

    private static void publish2() throws IOException, TimeoutException {
        //创建连接工厂
        ConnectionFactory factory = new ConnectionFactory();


        factory.setUsername(username);
        factory.setPassword(password);
        //设置 RabbitMQ 地址
        factory.setHost(host);
        factory.setPort(port);

        //建立到代理服务器到连接
        Connection conn = factory.newConnection();

        //获得信道
        Channel channel = conn.createChannel();

        //声明交换器
        String exchangeName = "/chat";
        channel.exchangeDeclare(exchangeName, "direct", true);


        //声明队列。
        //参数1：队列名
        //参数2：持久化 （true表示是，队列将在服务器重启时依旧存在）
        //参数3：独占队列（创建者可以使用的私有队列，断开后自动删除）
        //参数4：当所有消费者客户端连接断开时是否自动删除队列
        //参数5：队列的其他参数
        channel.queueDeclare(ranks, true, false, false, null);

        //队列绑定到交换机
        String routingKey = "tag1";
        channel.queueBind(ranks, "/chat", routingKey);


        //发布消息
//        String message = "hello";


        // 基本发布消息
        // 第一个参数为交换机名称、
        // 第二个参数为队列映射的路由key、
        // 第三个参数为消息的其他属性 指定持久化 (创建队列也需要配置持久化)
        // 第四个参数为发送信息的主体
        channel.basicPublish("/chat", "tag1", MessageProperties.MINIMAL_PERSISTENT_BASIC, message.getBytes(StandardCharsets.UTF_8));


        channel.close();
        conn.close();
    }

    private static void consume() throws IOException, TimeoutException {
        ConnectionFactory factory = new ConnectionFactory();

        factory.setUsername(username);
        factory.setPassword(password);

        //设置 RabbitMQ 地址
        factory.setHost(host);
        factory.setPort(port);

        //建立到代理服务器到连接
        Connection conn = factory.newConnection();

        //获得信道
        Channel channel = conn.createChannel();

        //声明队列
        channel.queueDeclare(ranks, true, false, false, null);

        while (true) {
            //消费消息
            boolean autoAck = false;
            String consumerTag = "";
            channel.basicConsume(ranks, autoAck, consumerTag, new DefaultConsumer(channel) {
                @Override
                public void handleDelivery(String consumerTag,
                                           Envelope envelope,
                                           AMQP.BasicProperties properties,
                                           byte[] body) throws IOException {

                    String routingKey = envelope.getRoutingKey();
                    String contentType = properties.getContentType();

                    System.out.println("消费的路由键：" + routingKey);
                    System.out.println("消费的内容类型：" + contentType);

                    System.out.println("消费的消息体内容：");
                    String bodyStr = new String(body, StandardCharsets.UTF_8);
                    System.out.println(bodyStr);

                    sleep(1000);

                    //确认消息
                    long deliveryTag = envelope.getDeliveryTag();
                    channel.basicAck(deliveryTag, false);

                }
            });
        }
    }

    private static void sleep(long t) {
        try {
            Thread.sleep(t);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```



## 三.数据库主从架构



### 主从同步笔记

**环境**

```
主数据库 192.168.88.88
从数据库 192.168.88.99
```

**服务控制**

```cmd
/usr/local/mysql/support-files/mysql.server start|stop|restart
```

```
/usr/local/mysql/bin/mysql -uroot -p
```



**查询用户**

> 查询环境下的用户

```sql
mysql>select user,host from mysql.user;
mysql>select user,host from mysql.user\G;
```

ip

> localhost代表只能在本机访问

![image-20220308140645028](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213092.png)



**删除用户**

```sql
mysql>delete from mysql.user where user='jack'
```

**新增用户**

```sql
mysql>grant all on *.* to jack@"%" identified by "123";
```



| 字段  | 功能                          |                |
| ----- | ----------------------------- | -------------- |
| all   | 权限                          | select,updata  |
| \*.*  | 某个数据库的某个表            | test.book      |
| jack  | 登录用户名                    |                |
| “%”   | 从哪台服务器登录,可以是ip地址 | 192.168.19.129 |
| “123” | 密码                          |                |

**远连 接**

```sql
mysql -ujack -p -h 192.168.19.1
```

**开启binlog  ,记录所有的数据库变化操作(数据增删改,创建表等)**

vi my.cnf

> vi /usr/local/mysql/my.cnf

```sql
[mysqld]
basedir = /usr/local/mysql
datadir=/usr/local/mysql/data
user = mysql
default_storage_engine = InnoDB
port = 3306
socket=/tmp/mysql.sock
log_error=/usr/local/mysql/data/mysqld.log
pid_file=/use/local/mysql/data/mysqld.pid
character_set_server=utf8

server_id = 1
log_bin = mysql-bin

sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES

[client]
port    =3306
socket  =/tmp/mysql.sock
default_character_set=utf8
```

```sql
[mysqld]
datadir=/usr/local/mysql/data
log-bin=mysql-bin
binlog_format=row		#mysql 5.7默认为row 格式
```

**在datadir目录中,查看binlog文件**

```
mysql-bin.000001
mysql-bin.000002
```

**在binlog常规操作**

```cmd
mysql>show master status;	#查看当前binlog日志
mysql>reset master;			#清空所有的binlog文件
mysql>flush logs; 			#启用一个新的binlog日志
```

**创建测试表**

```mysql
create database test 
use test;
create table user(id omt,name varchar(10));
insert into user values (1,"jack")
insert into user values (2,"Lily")
```

**查看日志内容**

```cmd
/usr/local/mysql/bin/mysqlbinlog -v data/mysql-bin.000001
/user/local/mysql/bin/mysqlbinlog -v --base64-output=decode0rows mysql-bin.000001
```



### 主从服务器配置

####  主服务器配置

**1.授权一个用户,在从服务器上可以通过这个用户来连接主服务器**

```cmd
grant all on *.* to jack@192.168.88.99 identified by "123";
```

**2.修改主数据库服务器的配置文件,开启bin-log并设置server-id的值**

vi /usr/local/mysql/my.cnf

```sql
[mysqld]
log-bin=mysql-bin
server-id=1
```

**3.清空所有的bin-log日志**

```cmd
reset master;
show master status;	
```

**4.备份主服务器的test 数据库**

```sql
#如果主服务器在使用中,可以锁定数据库禁止写入配好后再解锁
mysql>flush tables with read lock;
mysql>unlock tables;
#备份
/usr/local/mysql/bin/mysqldump -uroot -p -lF test >'/tmp/db.test.20210603.sql'
```

```sql
D:\code\MySQl\bin\mysqldump -uroot -p forum -lF >D:\code\db.forum.20220308.sql
```



#### 从服务器配置

**1.把服务器上的备份文件,拷贝到从服务器上**

```sql
 scp root@192.168.88.88:/tmp/test.sql /tmp/db.test.sql 
```

**2.从备份文件,恢复数据库**

```sql
mysql>create database if not exists test;
[root@localhost ~]# mysql -uroot -p test -f<'/tmp/db.test.sql'
```

**3.清空所有bin-log**

```sql
mysql>reset master
mysql>show master status;ignore
```

**4.备份从服务器的test 数据库**

```
#如果从服务器在使用中,可以锁定数据库禁止写入配好后再解锁
mysql>flush tables with read lock;
mysql>unlock tables;

/usr/local/mysql/bin/mysqldump -uroot -p -IF test >'/tmp/db.test.sql'
```

**5.重启Mysql**

```sql
ps -le | grep mysqld
plill mysqld
```

**6.连接主服务器**

```sql
change master to master_user='jack',master_password='123',master_host='192,168.88.88',master_port=3306;

start slave;
# stop salve;
show slave status\G;
show processlist 
```

#### **报错处理**



![image-20220307225057853](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213093.png)



### 主从架构定义与使用

#### 什么是 MySQL 的主从复制？

指一台服务器充当`主数据库`服务器，另一台或多台服务器充当`从数据库`服务器，主服务器中的数据自动复制到从服务器之中

主从复制工作原理：

1. Master 数据库只要发生变化，立马记录到 Binary log 日志文件中
2. Slave数据库启动一个 I/O thread 连接 Master 数据库，请求 Master 变化的二进制日志
3. Slave I/O 获取到的二进制日志，保存到自己的 Relay log 日志文件中
4. Slave 有一个 SQL thread 定时检查 Realy log 是否变化，变化了就更新数据到数据库中

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213094.jpg!l)

预览

#### 为什么要用 MySQL 的主从？

##### 1.实现服务器负载均衡

​    即可以通过在主服务器和从服务器之间切分处理客户查询的负荷，从而得到更好的客户相应时间。通常情况下，数据库管理员会有两种思路。

​    一是在主服务器上只实现数据的更新操作。包括数据记录的更新、删除、新建等等作业。而不关心数据的查询作业。数据库管理员将数据的查询请求全部 转发到从服务器中。这在某些应用中会比较有用。如某些应用，像基金净值预测的网站。其数据的更新都是有管理员更新的，即更新的用户比较少。而查询的用户数 量会非常的多。此时就可以设置一台主服务器，专门用来数据的更新。同时设置多台从服务器，用来负责用户信息的查询

​    二是在主服务器上与从服务器切分查询的作业。在这种思路下，主服务器不单单要完成数据的更新、删除、插入等作业，同时也需要负担一部分查询作业。而从服务器的话，只负责数据的查询。当主服务器比较忙时，部分查询请求会自动发送到从服务器重，以降低主服务器的工作负荷。

##### 2.通过复制实现数据的异地备份

​    可以定期的将数据从主服务器上复制到从服务器上，这无疑是先了数据的异地备份。在传统的备份体制下，是将数据备份在本地。此时备份 作业与数据库服务器运行在同一台设备上，当备份作业运行时就会影响到服务器的正常运行。有时候会明显的降低服务器的性能。同时，将备份数据存放在本地，也 不是很安全。如硬盘因为电压等原因被损坏或者服务器被失窃，此时由于备份文件仍然存放在硬盘上，数据库管理员无法使用备份文件来恢复数据。这显然会给企业 带来比较大的损失。

##### 3.提高数据库系统的可用性

​    数据库复制功能实现了主服务器与从服务器之间数据的同步，增加了数据库系统的可用性。当主服务器出现问题时，数据库管理员可以马上让从服务器作为主服务器，用来数据的更新与查询服务。然后回过头来再仔细的检查主服务器的问题。此时一般数据库管理员也会采用两种手段。

​    一是主服务器故障之后，虽然从服务器取代了主服务器的位置，但是对于主服务器可以采取的操作仍然做了一些限制。如仍然只能够进行数据的查询，而 不能够进行数据的更新、删除等操作。这主要是从数据的安全性考虑。如现在一些银行系统的升级，在升级的过程中，只能够查询余额而不能够取钱。这是同样的道 理。

​    二是从服务器真正变成了主服务器。当从服务器切换为主服务器之后，其地位完全与原先的主服务器相同。此时可以实现对数据的查询、更新、删除等操 作。为此就需要做好数据的安全性工作。即数据的安全策略，要与原先的主服务器完全相同。否则的话，就可能会留下一定的安全隐患。

#### 怎么配置 MySQL 主从复制？

![image-20220307202109436](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213095.png)

实验时注意注意 MySQL 版本，目前不建议使用 MySQL 8.x，推荐使用 MySQL 5.7.13，安装教程：https://www.daimaku.net/post/view/10863

### Ubuntu 20.4 安装 MySQL 5.7

#### 一、准备环境

```
$ cat /etc/issue
Ubuntu 20.04.2 LTS

# 安装MySQL依赖包
$ apt install  -y libaio1 libncurses*
```

#### 二、下载软件

从MySQL官网下载编译好的Linux二进制包

```
$ wget https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.13-linux-glibc2.5-x86_64.tar.gz
```

你也可以在本地电脑中提前下载好，通过scp等方式，上传到Linux中

#### 三、解压

解压到 /usr/local/ 目录中

```
$ tar -zxvf mysql-5.7.13-linux-glibc2.5-x86_64.tar.gz -C /usr/local/
```

进入 `/usr/local/`目录，将 `mysql-5.7.13-linux-glibc2.5-x86_64` 重命名为 `mysql/`

```
$ cd /usr/local/
$ mv mysql-5.7.13-linux-glibc2.5-x86_64 mysql/
```

#### 四、初始化数据库目录

创建一个叫做`mysql`的系统帐号

```
$ useradd -s /bin/false -M mysql

# 删除系统中默认MySQL配置文件
$ rm -f /etc/my.cnf /etc/mysql/my.cnf /usr/local/mysql/etc/my.cnf ~/.my.cnf

# 初始化数据库目录，执行成功后，在/usr/local/mysql中，将新产生一个data目录
$ /usr/local/mysql/bin/mysqld --initialize-insecure --user=mysql

[Warning] Gtid table is not ready to be used. Table 'mysql.gtid_executed' cannot be opened.
[Warning] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
```

#### 五、启动服务

```
/usr/local/mysql/bin/mysqld_safe --user=mysql &
```

#### 六、测试连接

进入MySQL(默认空密码，直接回车)

```
$ /usr/local/mysql/bin/mysql -uroot -p

Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.7.13 MySQL Community Server (GPL)

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

建库建表

```
mysql> create database test;
Query OK, 1 row affected (0.00 sec)

mysql> use test;
Database changed

mysql> create table t1 (id int primary key auto_increment, name varchar(50)) engine=innodb default charset=utf8mb4;
Query OK, 0 rows affected (0.00 sec)
```

插入数据

```
mysql> insert into t1 (name) values ('jack');
Query OK, 1 row affected (0.01 sec)

#  查询数据
mysql> select * from t1;
+----+------+
| id | name |
+----+------+
|  1 | jack |
+----+------+
1 row in set (0.00 sec)
```

退出MySQL

```
mysql> exit
```

#### 七、常见错误解决

error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory

```
$ apt install -y libaio1
```

error while loading shared libraries: libncurses.so.5: cannot open shared object file: No such file or directory

```
$ apt install  -y libncurses*
```



### ShardingSphere-JDBC(读写分离)

Java 中，例用 ShardingSphere-JDBC 基于 MyBatis 做 MySQL 读写分离，教程 https://www.daimaku.net/post/view/12624

#### 引入依赖 pom.xml

```
<dependency>
    <groupId>org.apache.shardingsphere</groupId>
    <artifactId>shardingsphere-jdbc-core-spring-boot-starter</artifactId>
    <version>5.0.0</version>
</dependency>
```

#### 配置数据源

```
#spring.datasource.url=jdbc:mysql://127.0.0.1:3306/test?useUnicode=true&characterEncoding=utf8&useSSL=false&zeroDateTimeBehavior=convertToNull&serverTimezone=Asia/Shanghai
#spring.datasource.username=root
#spring.datasource.password=root
#spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
#mybatis.configuration.map-underscore-to-camel-case=true
#mybatis.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl

# 所有数据源名称
spring.shardingsphere.datasource.names=ds1,ds2,ds3

# 数据源1
spring.shardingsphere.datasource.ds1.jdbc-url=jdbc:mysql://127.0.0.1:3306/test?useUnicode=true&characterEncoding=utf8&useSSL=false&zeroDateTimeBehavior=convertToNull&serverTimezone=Asia/Shanghai
spring.shardingsphere.datasource.ds1.username=root
spring.shardingsphere.datasource.ds1.password=root
spring.shardingsphere.datasource.ds1.type=com.zaxxer.hikari.HikariDataSource
spring.shardingsphere.datasource.ds1.driver-class-name=com.mysql.cj.jdbc.Driver


# 数据源2
spring.shardingsphere.datasource.ds2.jdbc-url=jdbc:mysql://127.0.0.1:3306/test?useUnicode=true&characterEncoding=utf8&useSSL=false&zeroDateTimeBehavior=convertToNull&serverTimezone=Asia/Shanghai
spring.shardingsphere.datasource.ds2.username=root
spring.shardingsphere.datasource.ds2.password=root
spring.shardingsphere.datasource.ds2.type=com.zaxxer.hikari.HikariDataSource
spring.shardingsphere.datasource.ds2.driver-class-name=com.mysql.cj.jdbc.Driver

# 数据源3
spring.shardingsphere.datasource.ds3.jdbc-url=jdbc:mysql://127.0.0.1:3306/test?useUnicode=true&characterEncoding=utf8&useSSL=false&zeroDateTimeBehavior=convertToNull&serverTimezone=Asia/Shanghai
spring.shardingsphere.datasource.ds3.username=root
spring.shardingsphere.datasource.ds3.password=root
spring.shardingsphere.datasource.ds3.type=com.zaxxer.hikari.HikariDataSource
spring.shardingsphere.datasource.ds3.driver-class-name=com.mysql.cj.jdbc.Driver

# 负载均衡 ROUND_ROBIN/RANDOM
spring.shardingsphere.rules.readwrite-splitting.load-balancers.demo.type=ROUND_ROBIN
#spring.shardingsphere.rules.readwrite-splitting.load-balancers.demo.props.key1=val1
#spring.shardingsphere.rules.readwrite-splitting.load-balancers.demo.props.key2=val2

# 读写配置 ds1是主库，增删改走ds1，查询走ds2和ds3
spring.shardingsphere.rules.readwrite-splitting.data-sources.demo.load-balancer-name=demo
spring.shardingsphere.rules.readwrite-splitting.data-sources.demo.write-data-source-name=ds1
spring.shardingsphere.rules.readwrite-splitting.data-sources.demo.read-data-source-names=ds2,ds3



# 打印 sql
spring.shardingsphere.props.sql-show=true
```

可以看到，INSERT语句，使用ds1数据源，查询语句使用ds2、ds3。

![WX20211026-174526@2x.png](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213096.png)



### Ubuntu上海时区

#### 使用`date`命令查看系统时间

```
date
```

#### 设置市区

```
tzselect
```

#### 从出现的菜单中依次选择`4`、`9`、`1`、`1`

```
root@ubuntu:/etc/apt# tzselect
Please identify a location so that time zone rules can be set correctly.
Please select a continent, ocean, "coord", or "TZ".
 1) Africa
 2) Americas
 3) Antarctica
 4) Asia
 5) Atlantic Ocean
 6) Australia
 7) Europe
 8) Indian Ocean
 9) Pacific Ocean
10) coord - I want to use geographical coordinates.
11) TZ - I want to specify the timezone using the Posix TZ format.
#? 4
Please select a country whose clocks agree with yours.
 1) Afghanistan          18) Israel            35) Palestine
 2) Armenia          19) Japan            36) Philippines
 3) Azerbaijan          20) Jordan            37) Qatar
 4) Bahrain          21) Kazakhstan        38) Russia
 5) Bangladesh          22) Korea (North)        39) Saudi Arabia
 6) Bhutan          23) Korea (South)        40) Singapore
 7) Brunei          24) Kuwait            41) Sri Lanka
 8) Cambodia          25) Kyrgyzstan        42) Syria
 9) China          26) Laos            43) Taiwan
10) Cyprus          27) Lebanon            44) Tajikistan
11) East Timor          28) Macau            45) Thailand
12) Georgia          29) Malaysia            46) Turkmenistan
13) Hong Kong          30) Mongolia            47) United Arab Emirates
14) India          31) Myanmar (Burma)        48) Uzbekistan
15) Indonesia          32) Nepal            49) Vietnam
16) Iran          33) Oman            50) Yemen
17) Iraq          34) Pakistan
#? 9
Please select one of the following timezones.
1) Beijing Time
2) Xinjiang Time
#? 1

The following information has been given:

    China
    Beijing Time

Therefore TZ='Asia/Shanghai' will be used.
Selected time is now:    Thu Mar  3 15:57:13 CST 2022.
Universal Time is now:    Thu Mar  3 07:57:13 UTC 2022.
Is the above information OK?
1) Yes
2) No
#? 1
```

#### 改变localtime文件

```
sudo cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

#### 再打印时间就同步了

```
date
```



### linux配置全局环境变量

mysql全局环境变量

Linux 配置

 jdk mysql 环境变量

1.[vim](https://so.csdn.net/so/search?q=vim&spm=1001.2101.3001.7020) /etc/profile 命令进入编辑

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213097.png)

![L3Byb3h5L2h0dHAvaW1hZ2UubWFtaWNvZGUuY29tL2luZm8vMjAyMDAxLzIwMjAwMTEyMTMxMzE0ODcyNjU4LnBuZw==.jpg](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213098.jpg)

g 到最后一行  i 开始插入  在最后一行加上下面的内容

export JAVA_HOME=/usr/local/jdk1.8.0_231

export MYSQL_HOME=/usr/local/mysql

export PATH=$JAVA_HOME/bin:$MYSQL_HOME/bin:$PATH

Esc  shift+冒号  wq 保存退出

tail /etc/profile 查看修改是否正确   不想查看可以跳过

![L3Byb3h5L2h0dHAvaW1hZ2UubWFtaWNvZGUuY29tL2luZm8vMjAyMDAxLzIwMjAwMTEyMTMxMzE0OTY2NDExLnBuZw==.jpg](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213099.jpg)

2.source /etc/profile  重新加载配置文件

3.任意路径 msql -u root -p 登录 记得输入正确的密码

4.show databases; 显示数据库 说明配置成功  (记得加上分号)

![L3Byb3h5L2h0dHAvaW1hZ2UubWFtaWNvZGUuY29tL2luZm8vMjAyMDAxLzIwMjAwMTEyMTMxMzE1MDkyMzkzLnBuZw==.jpg](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213100.jpg)





## 四.反向代理与负载均衡

这一节，我们实验 `反向代理`（Reverse Proxy） 和 `负载均衡`（Load Balance）

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213101.png!l)

官方文档：

http://nginx.org/en/docs/http/ngx_http_proxy_module.html



修改 Nginx 配置文件 `nginx.conf` 如下，然后让 Nginx 加载新的配置文件，命令是 `nginx -s reload`，就实现了反向代理和负载均衡

```javascript
http {
    
    # 配置两台上游服务器，例如是 Java 启动的 Spring Boot 服务
    upstream backend {
        server 172.19.13.56:8080 weight=1 max_fails=0;
        server 172.19.13.57:8080 weight=1 max_fails=0;
    }

    server {
    
        listen       80;
        server_name  _;

        location / {
            proxy_pass   http://backend;        # 将请求转发到上游服务器
            proxy_set_header    X-Real-IP  $remote_addr;
            proxy_set_header    HTTP_X_FORWARDED_FOR $remote_addr;
            proxy_set_header    X-Forwarded-For  $proxy_add_x_forwarded_for;
            proxy_set_header    X-Forwarded-Proto $scheme;
            proxy_set_header    Host    $host;
        }
    }
}
```



将`社区(论坛)`项目后端，部署到 2 台机器中，使用 Nginx 做反向代理，实现负载均衡

****

#   java虚拟机

## 类加载器ClassLoader

[类加载器-博客园](https://www.cnblogs.com/secbro/p/11759046.html)


Java中有三种

- 启动类加载器  BootstrapClassLoader  核心加载器
- 扩展类加载器  ExtClassLoader  相对核心
-    应用类加载器  AppClassLoader  处理业务代码

>启动类加载器：这个加载器不是一个Java类，而是由底层的c++实现，负责将存放在JAVA_HOME下lib目录中的类库，比如rt.jar。因此，启动类加载器不属于Java类库，无法被Java程序直接引用，用户在编写自定义类加载器时，如果需要把加载请求委派给引导类加载器，那直接使用null代替即可。
>
>扩展类加载器：由sun.misc.Launcher$ExtClassLoader实现，负责加载JAVA_HOME下lib\ext目录下的，或者被java.ext.dirs系统变量所指定的路径中的所有类库，开发者可以直接使用扩展类加载器。
>
>应用类加载器：由sun.misc.Launcher$AppClassLoader实现的。由于这个类加载器是ClassLoader中的getSystemClassLoader方法的返回值，所以也叫系统类加载器。它负责加载用户类路径上所指定的类库，可以被直接使用。如果未自定义类加载器，默认为该类加载器

### BootstrapClassLoader

最底层的类加载器,Java核心的类的加载器
lib/
如: rt.jar

```java
ClassLoader classLoader = 
ArrayList.class.getClassLoader();
System.out.println(classLoader);
```

打印结果为null,因为启动加载类器对于Java层面是不可见的

### ExtClassLoader

Java里的扩展包里的类的加载器
lib/ext/*.jar

```java
ClassLoader classLoader1 =
ZipFileSystem.class.getClassLoader();
System.out.println(classLoader1);
```

打印结果为

```java
sun.misc.Launcher$ExtClassLoader@677327b6
```

### AppClassLoader

用户建的类 如Foo
classpath

```java
ClassLoader classLoader2 = Foo.class.getClassLoader();
System.out.println(classLoader2);
```

### 怎么协作加载？

#### 双亲委派模型

Parent Delegation Model

双亲委派模型：当一个类加载器接收到类加载请求时，会先请求其父类加载器加载，依次递归，当父类加载器无法找到该类时（根据类的全限定名称），子类加载器才会尝试去加载。

![image](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213102.jpg)

双亲委派中的父子关系一般不会以继承的方式来实现，而都是使用组合的关系来复用父加载器的代码。

#### 作用

为了: 防止核心类被替换

双亲委派模型是为了保证Java核心库的类型安全。所有Java应用都至少需要引用java.lang.Object类，在运行时这个类需要被加载到Java虚拟机中。如果该加载过程由自定义类加载器来完成，可能就会存在多个版本的java.lang.Object类，而且这些类之间是不兼容的。

通过双亲委派模型，对于Java核心库的类的加载工作由启动类加载器来统一完成，保证了Java应用所使用的都是同一个版本的Java核心库的类，是互相兼容的。

## 字节码文件

编译之后的.class文件用16进制工具显示

hexdump工具[HEXDUMP for Windows (di-mgt.com.au)](https://www.di-mgt.com.au/hexdump-for-windows.html)
JVM官方手册[Chapter 4. The class File Format (oracle.com)](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html)

```java
ClassFile {
	u4 	magic;
	u2 	minor_version;
	u2 	major_version;
	u2 	constant_pool_count;
	cp_info constant_pool[constant_pool_count-1];
	u2 	access_flags;
	u2 	this_class;
	u2 	super_class;
	u2 	interfaces_count;
	u2 	interfaces[interfaces_count];
	u2 	fields_count;
	field_info fields[fields_count];
	u2 	methods_count;
	method_info methods[methods_count];
	u2 	attributes_count;
	attribute_info attributes[attributes_count];
}
```

第一个魔数（magic），必须是 cafe babo
第二三版本号，0034表示Java1.8
idea 插件jclasslib Bytecoed Viewer

![image-20220310212022225](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213103.png)

默认的，无参的构造方法

## JVM类加载过程

类加载分为三个阶段
**加载**
**链接**
**初始化**

### 加载

把字节码文件读到内存里,生成java.lang.Class

```java
Class clazz = Demo.class;
```

## 链接

### 验证

验证字节码是否符合规范

### 准备

申请内存空间,变量初始化

### 解析

解析字节码

### 初始化	

**将变量复制**

### 静态属性

```java
public class Demo {
	public static int a = 5;
	static {
		a = 6;
	}
}
```

![image-20220310212518079](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213105.png)

先将5赋给变量a,然后将6赋给a

```java
public class Demo {
	static {
		a = 6;
	}
	public static int a = 5;
}

```

![image-20220310212628794](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213106.png)

### 构造方法

```java
public class Demo {
	static int a = 1;
	public Demo() {
		a++;
	}
}
```

![image-20220310212715803](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213107.png)

## 汇编指令

寄存器的指令集

![image-20220310213031595](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213108.png)

Java用栈来表示数据

```java
0 iconst_5
1 putstatic #2 <com/example/Demo.num : I>
4 return
```

### 常用前缀

```java
i-------int
f-------float
c-------char
d-------double
b-------byte
s-------short
l-------long
a-------引用
iconst_4：把4放到栈顶
` istore_1：把栈定元素存到局部变量表1`里
```

### 数字计算

```java
public static void main(String[] args) {
	int x = 2;
	int y = 3;
	int z = x + y;
}

```

```java
0 iconst_2
1 istore_1
2 iconst_3
3 istore_2
4 iload_1
5 iload_2
6 iadd
7 istore_3
8 return
```

### 对象

```java
public class Demo {
	public void add(){
	}
	public static void main(String[] args) {
		Demo demo = new Demo();
		demo.add();
	}
}
```

```java
0 new #2 <com/example/Demo>
3 dup
4 invokespecial #3 <com/example/Demo.<init> : ()V>
7 astore_1
8 aload_1
9 invokevirtual #4 <com/example/Demo.add : ()V>
12 return
```

0 实例化一个对象 
3 复制对象在栈顶 
4 调用3的init方法 
7 把栈顶元素存到局部变量表1里 
8 加载局部变量表1到栈顶 
9 调用这个变量的add方法

## 字符串相加底层原理

### 两个字符串常量

```java
public static void main(String[] args) {
	String str = "xx" + "yy";
}
```

```java
0 ldc #2 <xxyy>
2 astore_1
3 return
```

0：lac：Path item from run-time constant pool 
从运行时常量池推送项目； 
把这个xxyy从常量池里push到局部变量表2中， 
局部变量表2

```
字符串字面量:cp info #21 <xxyy>
```

即：在初始化时，str的值就是xxyy 数字计算时：把结果放在变量中。结果是在javac编译就算好了

### 变量与常量

```java
public static void main(String[] args) {
	String str = "xx" ;
	String str1 = str + "yy";
}
```

0：从常量池里拿一个xx，是2号常量 
2：保存到局部变量表1 
3：new一个三号常量-StringBuilder 
6：推到栈顶 
7：调用StringBuilder的init构造方法 
10：加载局部变量的xx到栈里 
11：调用StringBuilder的append方法 
14：从常量池拿一个yy，6号常量

```java
0 ldc #2 <xx>
2 astore_1
3 new #3 <java/lang/StringBuilder>
6 dup
7 invokespecial #4 <java/lang/StringBuilder.<init> : ()V>
10 aload_1
11 invokevirtual #5 <java/lang/StringBuilder.append :
(Ljava/lang/String;)Ljava/lang/StringBuilder;>
14 ldc #6 <yy>
16 invokevirtual #5 <java/lang/StringBuilder.append :
(Ljava/lang/String;)Ljava/lang/StringBuilder;>
19 invokevirtual #7 <java/lang/StringBuilder.toString :
()Ljava/lang/String;>
22 astore_2
23 return
```

**直接return对象，不需要先引用再return了**

## 运行时数据区

![image-20220310214130492](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213109.png)

黄色是线程隔离数据区 
单个线程私有，每个线程都有这些区； 
即：每个线程都有自己的栈 
绿色是线程共享的数据区
所有线程公用的

### 执行引擎

java命令后开始运行

### Java接口

#### 堆

- 堆里存放对象 
- 由局部变量引用对象 
- 栈里存放局部变量
- 当栈里的局部变量不引用对象之后，对象就会被垃圾回收机制收回

#### 方法区

保存class消息的区
类加载器产生的类都放在这里
new对象时,在方法区内找到类的消息

**本地方法栈**

### 程序计数器

线程之间的切换
存储当前执行的位置

### 栈

- 局部变量表 
- 当前操作树栈-----汇编指令中的栈 
- 运行时常量池的符号引用，要转成直接引用----“动态链接”

### 爆栈

栈的大小一般为512M-2MB
超过就会爆栈,考虑并发架构



#  深入Java并发

## 1.引用类型与ThreadLocal

java四种引用类型：强、软、弱、虚

```javascript
// 强引用，就是普通的赋值
Object obj = new Object();   // 这就是一个强引用
obj = null;                  // 解除引用
// 软引用
Object obj = new Object(); 

// ref这就是一个软引用
SoftReference<Object> ref =  new SoftReference<>(obj);

Object obj2 = ref.get();

System.out.println( obj == obj2); 

```

* 强、
  * 就算发生OOM(内存溢出),也不会被清楚
* 软 **(SoftReference)** 不推荐
  * 内存不足,垃圾回收才会干掉,   用于  缓存
* 弱 **(WeakReference)**
  * 只要发生垃圾回收,就会被回收
* 虚

![image-20220606191416563](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213110.png)



```java
public class Demo{

    private ThreadLocal<String> local = new ThreadLocal<>();

    public void test(String val){
        local.set(val);
        // local.remove();
    }

    public void test2(){
        System.out.println(local.get());
    }

    public static void main(String[] args){
        Demo demo = new Demo();
        Thread thread1 = new Thread(() -> {
            demo.test("jack");//1
            sleep(1000);
            demo.test2();//4
        });
        Thread thread2 = new Thread(() -> {
            sleep(50);
            demo.test("marry");//2
            sleep(500);
            demo.test2();//3
        });
        thread1.start();
        thread2.start();
        System.out.println(demo.local.get());
    }
    private static void sleep(long val){
        try {
            Thread.sleep(val);
        }catch (InterruptedException e){
            e.printStackTrace();
        }
    }
}

```

## 2.线程池

### ThreadPoolExecutor

线程创建是非常消耗性能的,所以提前准备核心线程

```java
public class Test{
    public static void main(String[] args){
        ThreadPoolExecutor poolExecutor=new ThreadPoolExecutor(
                3,//核心线程数量
                5,//最大数量
                30,//空闲存活时间
                TimeUnit.SECONDS,
                // new ArrayBlockingQueue<>(5),//阻塞队列
                new LinkedBlockingQueue<>(5),//阻塞队列
                new ThreadPoolExecutor.AbortPolicy()//直接抛出异常
                // new ThreadPoolExecutor.CallerRunsPolicy()//只使用调用者所在的线程
                // new ThreadPoolExecutor.DiscardOldestPolicy()//把最近的任务丢弃掉
                // new ThreadPoolExecutor.DiscardPolicy()//线程池满了就丢弃掉
        );
        for (int i = 0 ; i <4 ; i++) {
            poolExecutor.execute(new Runnable(){
                @Override
                public void run(){
                    System.out.println(Thread.currentThread().getId());
                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            });
        }
        System.out.println(poolExecutor.getCorePoolSize());
    }
}
```



### BlockingQueue

BlockingQueue接口定义了一种阻塞的FIFO queue，每一个BlockingQueue都有一个容量，让容量满时往BlockingQueue中添加数据时会造成阻塞，当容量为空时取元素操作会阻塞。

* ArrayBlockingQueue

* LinkedBlockingQueue

#### ArrayBlockingQueue

ArrayBlockingQueue是一个由数组支持的有界阻塞队列。在读写操作上都需要锁住整个容器，因此吞吐量与一般的实现是相似的，适合于实现“生产者消费者”模式。

#### LinkedBlockingQueue

* LinkedBlockingQueue是基于链表的阻塞队列，同ArrayListBlockingQueue类似，其内部也维持着一个数据缓冲队列（该队列由一个链表构成），当生产者往队列中放入一个数据时，队列会从生产者手中获取数据，并缓存在队列内部，而生产者立即返回；

* 只有当队列缓冲区达到最大值缓存容量时（LinkedBlockingQueue可以通过构造函数指定该值），才会阻塞生产者队列，直到消费者从队列中消费掉一份数据，生产者线程会被唤醒，反之对于消费者这端的处理也基于同样的原理。
* 而LinkedBlockingQueue之所以能够高效的处理并发数据，还因为其对于生产者端和消费者端分别采用了独立的锁来控制数据同步，这也意味着在高并发的情况下生产者和消费者可以并行地操作队列中的数据，以此来提高整个队列的并发性能。

#### SynchronousQueue

```
private static ExecutorService cachedThreadPool = new ThreadPoolExecutor(4, Runtime.getRuntime().availableProcessors() * 2, 0, TimeUnit.MILLISECONDS, new SynchronousQueue<>(), r -> new Thread(r, "ThreadTest"));
```

 

SynchronousQueue没有容量，是无缓冲等待队列，是一个不存储元素的阻塞队列，会直接将任务交给消费者，必须等队列中的添加元素被消费后才能继续添加新的元素。

拥有公平（FIFO）和非公平(LIFO)策略，非公平侧罗会导致一些数据永远无法被消费的情况？

使用SynchronousQueue阻塞队列一般要求maximumPoolSizes为无界(Integer.MAX_VALUE)，避免线程拒绝执行操作。

#### 二者区别：

1. **队列中锁的实现不同**

  ArrayBlockingQueue实现的队列中的锁是没有分离的，即生产和消费用的是同一个锁；

  LinkedBlockingQueue实现的队列中的锁是分离的，即生产用的是putLock，消费是takeLock

2. **在生产或消费时操作不同**

  ArrayBlockingQueue实现的队列中在生产和消费的时候，是直接将枚举对象插入或移除的；

  LinkedBlockingQueue实现的队列中在生产和消费的时候，需要把枚举对象转换为Node<E>进行插入或移除，会影响性能

3. **队列大小初始化方式不同**

  ArrayBlockingQueue实现的队列中必须指定队列的大小；

  LinkedBlockingQueue实现的队列中可以不指定队列的大小，但是默认是Integer.MAX_VALUE



#### 常用API：



offer

将元素插入队列，成功返回true，如果当前没有可用的空间，则返回false

offer(E e, long timeout, TimeUnit unit) 

将元素插入队列，在到达指定的等待时间前等待可用的空间

E poll(long timeout, TimeUnit unit) 

获取并移除队列的头部，在指定的等待时间前等待可用的元素

void put(E e) 

将元素插入队列，将等待可用的空间（堵塞）

take() 

获取并移除队列的头部，在元素变得可用之前一直等待（堵塞）



```java
public class BlockingQueueTest {
	private static ArrayBlockingQueue<Integer> queue = new ArrayBlockingQueue<Integer>(5, true); //最大容量为5的数组堵塞队列
	//private static LinkedBlockingQueue<Integer> queue = new LinkedBlockingQueue<Integer>(5);

	private static CountDownLatch producerLatch; //倒计时计数器
	private static CountDownLatch consumerLatch;

	public static void main(String[] args) {
		BlockingQueueTest queueTest = new BlockingQueueTest();
		queueTest.test();
	}

	private void test(){
		producerLatch = new CountDownLatch(10); //state值为10
		consumerLatch = new CountDownLatch(10); //state值为10

		Thread t1 = new Thread(new ProducerTask());
		Thread t2 = new Thread(new ConsumerTask());

		//启动线程
		t1.start();
		t2.start();

		try {
			System.out.println("producer waiting...");
			producerLatch.await(); //进入等待状态，直到state值为0，再继续往下执行
			System.out.println("producer end");
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

		try {
			System.out.println("consumer waiting...");
			consumerLatch.await(); //进入等待状态，直到state值为0，再继续往下执行
			System.out.println("consumer end");
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

		//结束线程
		t1.interrupt();
		t2.interrupt();

		System.out.println("end");
	}

	//生产者
	class ProducerTask implements Runnable{
		private Random rnd = new Random();

		@Override
		public void run() {
			try {
				while(true){
					queue.put(rnd.nextInt(100)); //如果queue容量已满，则当前线程会堵塞，直到有空间再继续

					//offer方法为非堵塞的
					//queue.offer(rnd.nextInt(100), 1, TimeUnit.SECONDS); //等待1秒后还不能加入队列则返回失败，放弃加入
					//queue.offer(rnd.nextInt(100));

					producerLatch.countDown(); //state值减1
					//TimeUnit.SECONDS.sleep(2); //线程休眠2秒
				}
			} catch (InterruptedException e) {
				//e.printStackTrace();
			}  catch (Exception ex){
				ex.printStackTrace();
			}
		}
	}

	//消费者
	class ConsumerTask implements Runnable{
		@Override
		public void run() {
			try {
				while(true){
					Integer value = queue.take(); //如果queue为空，则当前线程会堵塞，直到有新数据加入

					//poll方法为非堵塞的
					//Integer value = queue.poll(1, TimeUnit.SECONDS); //等待1秒后还没有数据可取则返回失败，放弃获取
					//Integer value = queue.poll();

					System.out.println("value = " + value);

					consumerLatch.countDown(); //state值减1
					TimeUnit.SECONDS.sleep(2); //线程休眠2秒
				}
			} catch (InterruptedException e) {
				//e.printStackTrace();
			} catch (Exception ex){
				ex.printStackTrace();
			}
		}
	}

}
```

## 3.CopyOnWriteArrayList

### Concurrent包下的常用并发类和普通类之间的区别

#### 1. [ConcurrentHashMap](https://so.csdn.net/so/search?q=ConcurrentHashMap&spm=1001.2101.3001.7020)和HashMap以及Hashtable之间的区别

**1.1 HashMap不是线程安全的，key和value都可为null；而Hashtable是线程安全的，代码中要求\**value不为null\**，但是在计算key的hashcode是直接调用，所以key也不能为null。**

**1.2 但Hashtable是锁住整个hash表，而ConcurrentHashMap是将hash表分为多个segment，每次操作先将映射到相应的segment，因为\**segment继承了ReentrantLock\**，所以segment操作可以保证线程安全，这样锁的粒度变细，并发性能提升明显。key和value都不能为null，因为value为null无法判断数据不存在还是数据存在但为null，\**存在歧义\**；而对于HashMap在get(key)获得null时，可以在不并发的情况调用contains(key)来解决歧义。**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213111.png)



#### 2. ConcurrenLinkedQueue和LinkedBlockingQueue之间的区别

**2.1 ConcuLinkedQueue是非阻塞队列，采用CAS+自旋保证并发的数据安全。对于写操作较多的场景，会增加自旋的次数；但是对于多个读操作，并不影响性能。**

**2.2 LinkedBlockingQueue是阻塞队列，通过锁机制保证数据安全。如果队列为空，那么消费者线程被阻塞。所以适合\**生产者多于消费者的场景\**。**



#### 3. CopyOnWriteArrayList和ArrayList

**3.1 CopyOnWriteArrayList在实现ArrayList的基础上，又实现了线程安全。但不是通过加锁来实现线程安全，因为这样性能太低；而且对于读操作是不更改数据的，所以多个读操作之间不需要加锁，只有读写、写写之间需要考虑线程安全。但是，CopyOnWriteArrayList最关键的是在读写操作并发也不阻塞读操作，只会对多个写操作之间进行加锁。如果存在写操作，那么先复制一份数据，然后更改，最终再覆盖原始的数据，这样在并发场景下可以高效地处理数据。**

**3.2 CopyOnWriteArrayList读取数据的源码分析——没有加锁操作**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213112.png)

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213113.png)![img](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/230-%25E6%25B7%25B1%25E5%2585%25A5Java%25E5%25B9%25B6%25E5%258F%2591/20210601150919131.png)

**3.3 CopyOnWriteArrayList写数据的源码分析——只会进行写操作的同步**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213114.png)



#### 4. CopyOnWriteArraySet

**4.1 内部就是CopyOnWriteArrayList**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213115.png)

**4.2 CopyOnWriteArrayList怎么满足CopyOnWriteArraySet的元素不重复性质**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213116.png)



## 4.@Transactional

```
    @Transactional(isolation = Isolation.REPEATABLE_READ,rollbackFor = Exception.class ,propagation = Propagation.REQUIRED)
```

### Isolation 隔离级别

* DEFAULT  
  * MySQL默认
* READ_COMMITTED
  * 读已提交 
* READ_UNCOMMITTED
  * 读未提交 
* REPEATABLE_READ
  * 可重复读

> 一个对照关系表：
>                  Dirty reads     non-repeatable reads      phantom reads
> Serializable             不会            不会                      不会
> REPEATABLE READ       不会            不会                       会
> READ COMMITTED       不会            会                        会
> Read Uncommitted       会              会                        会

### propagation传播

> @Transactional(isolation = Isolation.REPEATABLE_READ,rollbackFor = Exception.class ,propagation = Propagation.REQUIRED)

```shell
REQUIRED
SUPPORTS
MANDATORY  	  	 必须开事务才能调用
REQUIRES_NEW
NOT_SUPPORTED
NEVER 
NESTED
```

* PROPAGATION_REQUIRED 如果存在一个事务，则支持当前事务。如果没有事务则开启一个新的事务。 

* PROPAGATION_REQUIRES_NEW 总是开启一个新的事务。如果一个事务已经存在，则将这个存在的事务挂起。

* PROPAGATION_NESTED如果一个活动的事务存在，则运行在一个嵌套的事务中. 如果没有活动事务, 则按REQUIRED 属性执行

  

* PROPAGATION_SUPPORTS 如果存在一个事务，支持当前事务。如果没有，则非事务的执行。但是对于事务同步的事务管理器，与不使用事务有少许不同。

* PROPAGATION_NOT_SUPPORTED 总是非事务地执行，并挂起任何存在的事务。



* PROPAGATION_MANDATORY 如果已经存在一个事务，支持当前事务。如果没有一个活动的事务，则抛出异常。
* PROPAGATION_NEVER 总是非事务地执行，如果存在一个活动事务，则抛出异常

所以最安全的，是Serializable，但是伴随而来也是高昂的性能开销。
另外，事务常用的两个属性：readonly和timeout
一个是设置事务为只读以提升性能。
另一个是设置事务的超时时间，一般用于防止大事务的发生。还是那句话，事务要尽可能的小！

最后引入一个问题：
***\*一个逻辑操作需要检查的条件有20条，能否为了减小事务而将检查性的内容放到事务之外呢？\**** 

很多系统都是在DAO的内部开始启动事务，然后进行操作，最后提交或者回滚。这其中涉及到代码设计的问题。小一些的系统可以采用这种方式来做，但是在一些比较大的系统，
逻辑较为复杂的系统中，势必会将过多的业务逻辑嵌入到DAO中，导致DAO的复用性下降。所以这不是一个好的实践。

来回答这个问题：能否为了缩小事务，而将一些业务逻辑检查放到事务外面？答案是：对于核心的业务检查逻辑，不能放到事务之外，而且必须要作为分布式下的并发控制！
一旦在事务之外做检查，那么势必会造成事务A已经检查过的数据被事务B所修改，导致事务A徒劳无功而且出现并发问题，直接导致业务控制失败。
所以，在分布式的高并发环境下，对于核心业务逻辑的检查，要采用加锁机制。
比如事务开启需要读取一条数据进行验证，然后逻辑操作中需要对这条数据进行修改，最后提交。
这样的一个过程，如果读取并验证的代码放到事务之外，那么读取的数据极有可能已经被其他的事务修改，当前事务一旦提交，又会重新覆盖掉其他事务的数据，导致数据异常。
所以在进入当前事务的时候，必须要将这条数据锁住，使用for update就是一个很好的在分布式环境下的控制手段。

一种好的实践方式是使用编程式事务而非生命式，尤其是在较为规模的项目中。对于事务的配置，在代码量非常大的情况下，将是一种折磨，而且人肉的方式，绝对不能避免这种问题。
将DAO保持针对一张表的最基本操作，然后业务逻辑的处理放入manager和service中进行，同时使用编程式事务更精确的控制事务范围。
特别注意的，对于事务内部一些可能抛出异常的情况，捕获要谨慎，不能随便的catch Exception 导致事务的异常被吃掉而不能正常回滚。

### 事务的使用

> 直接调用一个事务,是一个类的内部调用,切面并不会生效,
>
> 调用代理对象才能使用切面

 

```java
@Autowired // 自己注入自己
TransactionalTest transactionalTest;
@Autowired // 上下文注入
ApplicationContext context;
```

> 这样就可以避免事务未启动

```java
@GetMapping("/test1") // Isolation.DEFAULT READ_COMMITTED READ_UNCOMMITTED REPEATABLE_READ
// @Transactional(isolation = Isolation.REPEATABLE_READ,rollbackFor = Exception.class ,propagation = Propagation.REQUIRED)
public void test1() throws InterruptedException{
    // REQUIRED
    // SUPPORTS
    // MANDATORY
    // REQUIRES_NEW
    // NOT_SUPPORTED
    // NEVER
    // NESTED
    TransactionalTest test =context.getBean(TransactionalTest.class);
    test.test1();

}

@GetMapping("/test2") // Isolation.DEFAULT READ_COMMITTED READ_UNCOMMITTED REPEATABLE_READ
@Transactional(isolation = Isolation.REPEATABLE_READ,rollbackFor = Exception.class ,propagation = Propagation.REQUIRED)
public void test2() throws InterruptedException{

}
```









## [5.MyBatis一 二级缓存 ](https://www.cnblogs.com/ysocean/p/7342498.html)



**目录**

- [1、一级Qq缓存](https://www.cnblogs.com/ysocean/p/7342498.html#_label0)
- [2、二级缓存](https://www.cnblogs.com/ysocean/p/7342498.html#_label1)
- [3、二级缓存整合ehcache](https://www.cnblogs.com/ysocean/p/7342498.html#_label2)
- [4、二级缓存的应用场景](https://www.cnblogs.com/ysocean/p/7342498.html#_label3)

 

------

　　上一章节，我们讲解了通过mybatis的懒加载来提高查询效率，那么除了懒加载，还有什么方法能提高查询效率呢？这就是我们本章讲的缓存。

　　本篇源码下载链接：http://pan.baidu.com/s/1eRHTsIm 密码：a5wn

　　mybatis 为我们提供了一级缓存和二级缓存，可以通过下图来理解：

　　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213117.png)

　　①、一级缓存是SqlSession级别的缓存。在操作数据库时需要构造sqlSession对象，在对象中有一个数据结构（HashMap）用于存储缓存数据。不同的sqlSession之间的缓存数据区域（HashMap）是互相不影响的。

　　②、二级缓存是mapper级别的缓存，多个SqlSession去操作同一个Mapper的sql语句，多个SqlSession可以共用二级缓存，二级缓存是跨SqlSession的。

 

[回到顶部](https://www.cnblogs.com/ysocean/p/7342498.html#_labelTop)

### 1、一级缓存

　　**①、我们在一个 sqlSession 中，对 User 表根据id进行两次查询，查看他们发出sql语句的情况。**

```
@Test``public` `void` `testSelectOrderAndUserByOrderId(){``  ``//根据 sqlSessionFactory 产生 session``  ``SqlSession sqlSession = sessionFactory.openSession();``  ``String statement = ``"one.to.one.mapper.OrdersMapper.selectOrderAndUserByOrderID"``;``  ``UserMapper userMapper = sqlSession.getMapper(UserMapper.``class``);``  ``//第一次查询，发出sql语句，并将查询的结果放入缓存中``  ``User u1 = userMapper.selectUserByUserId(``1``);``  ``System.out.println(u1);``  ` `  ``//第二次查询，由于是同一个sqlSession,会在缓存中查找查询结果``  ``//如果有，则直接从缓存中取出来，不和数据库进行交互``  ``User u2 = userMapper.selectUserByUserId(``1``);``  ``System.out.println(u2);``  ` `  ``sqlSession.close();``}
```

　　查看控制台打印情况：

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213118.png)

 

　　**②、 同样是对user表进行两次查询，只不过两次查询之间进行了一次update操作。**

```
@Test``public` `void` `testSelectOrderAndUserByOrderId(){``  ``//根据 sqlSessionFactory 产生 session``  ``SqlSession sqlSession = sessionFactory.openSession();``  ``String statement = ``"one.to.one.mapper.OrdersMapper.selectOrderAndUserByOrderID"``;``  ``UserMapper userMapper = sqlSession.getMapper(UserMapper.``class``);``  ``//第一次查询，发出sql语句，并将查询的结果放入缓存中``  ``User u1 = userMapper.selectUserByUserId(``1``);``  ``System.out.println(u1);``  ` `  ``//第二步进行了一次更新操作，sqlSession.commit()``  ``u1.setSex(``"女"``);``  ``userMapper.updateUserByUserId(u1);``  ``sqlSession.commit();``  ` `  ``//第二次查询，由于是同一个sqlSession.commit(),会清空缓存信息``  ``//则此次查询也会发出 sql 语句``  ``User u2 = userMapper.selectUserByUserId(``1``);``  ``System.out.println(u2);``  ` `  ``sqlSession.close();``}
```

　　控制台打印情况：

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213119.png)

　　

　　**③、总结**

　　1、第一次发起查询用户id为1的用户信息，先去找缓存中是否有id为1的用户信息，如果没有，从数据库查询用户信息。得到用户信息，将用户信息存储到一级缓存中。 

　　2、如果中间sqlSession去执行commit操作（执行插入、更新、删除），则会清空SqlSession中的一级缓存，这样做的目的为了让缓存中存储的是最新的信息，避免脏读。

　　3、第二次发起查询用户id为1的用户信息，先去找缓存中是否有id为1的用户信息，缓存中有，直接从缓存中获取用户信息。

 　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213120.png)

 

 

 

 

[回到顶部](https://www.cnblogs.com/ysocean/p/7342498.html#_labelTop)

### 2、二级缓存

　　二级缓存的原理和一级缓存原理一样，第一次查询，会将数据放入缓存中，然后第二次查询则会直接去缓存中取。但是一级缓存是基于 sqlSession 的，而 二级缓存是基于 mapper文件的namespace的，也就是说多个sqlSession可以共享一个mapper中的二级缓存区域，并且如果两个mapper的namespace相同，即使是两个mapper，那么这两个mapper中执行sql查询到的数据也将存在相同的二级缓存区域中。

 　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213121.png)

　　那么二级缓存是如何使用的呢？

　　**①、开启二级缓存**

　　和一级缓存默认开启不一样，二级缓存需要我们手动开启

　　首先在全局配置文件 mybatis-configuration.xml 文件中加入如下代码：

```
<!--开启二级缓存 -->``<settings>``  ``<setting name=``"cacheEnabled"` `value=``"true"``/>``</settings>
```

　　其次在 UserMapper.xml 文件中开启缓存

```
<!-- 开启二级缓存 -->``<cache></cache>
```

　　我们可以看到 mapper.xml 文件中就这么一个空标签<cache/>，其实这里可以配置<cache type="org.apache.ibatis.cache.impl.PerpetualCache"/>,PerpetualCache这个类是mybatis默认实现缓存功能的类。我们不写type就使用mybatis默认的缓存，也可以去实现 Cache 接口来自定义缓存。

　　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213122.png)

　　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213123.png)

　　我们可以看到 二级缓存 底层还是 HashMap 架构。

 

 

 　**②、po 类实现** **Serializable** **序列化接口**

 　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213124.png)

 

 　开启了二级缓存后，还需要将要缓存的pojo实现Serializable接口，为了将缓存数据取出执行反序列化操作，因为二级缓存数据存储介质多种多样，不一定只存在内存中，有可能存在硬盘中，如果我们要再取这个缓存的话，就需要反序列化了。所以mybatis中的pojo都去实现Serializable接口。

 　

 　**③、测试**

 　一、测试二级缓存和sqlSession 无关

```
@Test``public` `void` `testTwoCache(){``  ``//根据 sqlSessionFactory 产生 session``  ``SqlSession sqlSession1 = sessionFactory.openSession();``  ``SqlSession sqlSession2 = sessionFactory.openSession();``  ` `  ``String statement = ``"com.ys.twocache.UserMapper.selectUserByUserId"``;``  ``UserMapper userMapper1 = sqlSession1.getMapper(UserMapper.``class``);``  ``UserMapper userMapper2 = sqlSession2.getMapper(UserMapper.``class``);``  ``//第一次查询，发出sql语句，并将查询的结果放入缓存中``  ``User u1 = userMapper1.selectUserByUserId(``1``);``  ``System.out.println(u1);``  ``sqlSession1.close();``//第一次查询完后关闭sqlSession``  ` `  ``//第二次查询，即使sqlSession1已经关闭了，这次查询依然不发出sql语句``  ``User u2 = userMapper2.selectUserByUserId(``1``);``  ``System.out.println(u2);``  ``sqlSession2.close();``}
```

　　可以看出上面两个不同的sqlSession,第一个关闭了，第二次查询依然不发出sql查询语句。

 

　　二、测试执行 commit() 操作，二级缓存数据清空

```
@Test``public` `void` `testTwoCache(){``  ``//根据 sqlSessionFactory 产生 session``  ``SqlSession sqlSession1 = sessionFactory.openSession();``  ``SqlSession sqlSession2 = sessionFactory.openSession();``  ``SqlSession sqlSession3 = sessionFactory.openSession();``  ` `  ``String statement = ``"com.ys.twocache.UserMapper.selectUserByUserId"``;``  ``UserMapper userMapper1 = sqlSession1.getMapper(UserMapper.``class``);``  ``UserMapper userMapper2 = sqlSession2.getMapper(UserMapper.``class``);``  ``UserMapper userMapper3 = sqlSession2.getMapper(UserMapper.``class``);``  ``//第一次查询，发出sql语句，并将查询的结果放入缓存中``  ``User u1 = userMapper1.selectUserByUserId(``1``);``  ``System.out.println(u1);``  ``sqlSession1.close();``//第一次查询完后关闭sqlSession``  ` `  ``//执行更新操作，commit()``  ``u1.setUsername(``"aaa"``);``  ``userMapper3.updateUserByUserId(u1);``  ``sqlSession3.commit();``  ` `  ``//第二次查询，由于上次更新操作，缓存数据已经清空（防止数据脏读），这里必须再次发出sql语句``  ``User u2 = userMapper2.selectUserByUserId(``1``);``  ``System.out.println(u2);``  ``sqlSession2.close();``}
```

　　查看控制台情况：

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213125.png)

 

 　**④、useCache和flushCache**

　　mybatis中还可以配置userCache和flushCache等配置项，userCache是用来设置是否禁用二级缓存的，在statement中设置useCache=false可以禁用当前select语句的二级缓存，即每次查询都会发出sql去查询，默认情况是true，即该sql使用二级缓存。

```
<select id=``"selectUserByUserId"` `useCache=``"false"` `resultType=``"com.ys.twocache.User"` `parameterType=``"int"``>``  ``select * from user where id=#{id}``</select>
```

　　这种情况是针对每次查询都需要最新的数据sql，要设置成useCache=false，禁用二级缓存，直接从数据库中获取。 

　　在mapper的同一个namespace中，如果有其它insert、update、delete操作数据后需要刷新缓存，如果不执行刷新缓存会出现脏读。

   设置statement配置中的flushCache=”true” 属性，默认情况下为true，即刷新缓存，如果改成false则不会刷新。使用缓存时如果手动修改数据库表中的查询数据会出现脏读。

```
<select id=``"selectUserByUserId"` `flushCache=``"true"` `useCache=``"false"` `resultType=``"com.ys.twocache.User"` `parameterType=``"int"``>``  ``select * from user where id=#{id}``</select>
```

　　一般下执行完commit操作都需要刷新缓存，flushCache=true表示刷新缓存，这样可以避免数据库脏读。所以我们不用设置，默认即可。

 

 

[回到顶部](https://www.cnblogs.com/ysocean/p/7342498.html#_labelTop)

### 3、二级缓存整合ehcache

　　上面我们介绍了mybatis自带的二级缓存，但是这个缓存是单服务器工作，无法实现分布式缓存。那么什么是分布式缓存呢？假设现在有两个服务器1和2，用户访问的时候访问了1服务器，查询后的缓存就会放在1服务器上，假设现在有个用户访问的是2服务器，那么他在2服务器上就无法获取刚刚那个缓存，如下图所示：

　　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213126.png)

　　为了解决这个问题，就得找一个分布式的缓存，专门用来存储缓存数据的，这样不同的服务器要缓存数据都往它那里存，取缓存数据也从它那里取，如下图所示：

　　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213127.png)

 

 　如上图所示，在几个不同的服务器之间，我们使用第三方缓存框架，将缓存都放在这个第三方框架中，然后无论有多少台服务器，我们都能从缓存中获取数据。

　　这里我们介绍mybatis与第三方框架ehcache的整合。

　　上文一开始提到过，mybatis提供了一个cache接口，如果要实现自己的缓存逻辑，实现cache接口开发即可。mybatis本身默认实现了一个，但是这个缓存的实现无法实现分布式缓存，所以我们要自己来实现。ehcache分布式缓存就可以，mybatis提供了一个针对cache接口的ehcache实现类，这个类在mybatis和ehcache的整合包中。

　　**①、导入 mybatis-ehcache 整合包（最上面的源代码中包含有）**

　　![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181213128.png)

 

 　**②、在全局配置文件 mybatis-configuration.xml 开启缓存**

```
<!--开启二级缓存 -->``<settings>``  ``<setting name=``"cacheEnabled"` `value=``"true"``/>``</settings>
```

　　

 　**③、在 xxxMapper.xml 文件中整合 ehcache 缓存**

　　将如下的类的全类名写入<cache type="" ></cache>的type属性中

```
<!-- 开启本mapper的namespace下的二级缓存``  ``type:指定cache接口的实现类的类型，不写type属性，mybatis默认使用PerpetualCache``  ``要和ehcache整合，需要配置type为ehcache实现cache接口的类型``-->``<cache type=``"org.mybatis.caches.ehcache.EhcacheCache"``></cache>
```

　　

　　**④、配置缓存参数**

　　在 classpath 目录下新建一个 ehcache.xml 文件，并增加如下配置：

```
<?xml version=``"1.0"` `encoding=``"UTF-8"``?>``<ehcache xmlns:xsi=``"http://www.w3.org/2001/XMLSchema-instance"``  ``xsi:noNamespaceSchemaLocation=``"../config/ehcache.xsd"``>` `  ``<diskStore path=``"F:\develop\ehcache"``/>` `  ``<defaultCache``      ``maxElementsInMemory=``"10000"``      ``eternal=``"false"``      ``timeToIdleSeconds=``"120"``      ``timeToLiveSeconds=``"120"``      ``maxElementsOnDisk=``"10000000"``      ``diskExpiryThreadIntervalSeconds=``"120"``      ``memoryStoreEvictionPolicy=``"LRU"``>``    ``<persistence strategy=``"localTempSwap"``/>``  ``</defaultCache>``  ` `</ehcache>
```

　　

 diskStore：指定数据在磁盘中的存储位置。
 defaultCache：当借助CacheManager.add("demoCache")创建Cache时，EhCache便会采用<defalutCache/>指定的的管理策略
以下属性是必须的：
 maxElementsInMemory - 在内存中缓存的element的最大数目
 maxElementsOnDisk - 在磁盘上缓存的element的最大数目，若是0表示无穷大
 eternal - 设定缓存的elements是否永远不过期。如果为true，则缓存的数据始终有效，如果为false那么还要根据timeToIdleSeconds，timeToLiveSeconds判断
 overflowToDisk - 设定当内存缓存溢出的时候是否将过期的element缓存到磁盘上
以下属性是可选的：
 timeToIdleSeconds - 当缓存在EhCache中的数据前后两次访问的时间超过timeToIdleSeconds的属性取值时，这些数据便会删除，默认值是0,也就是可闲置时间无穷大
 timeToLiveSeconds - 缓存element的有效生命期，默认是0.,也就是element存活时间无穷大
 diskSpoolBufferSizeMB 这个参数设置DiskStore(磁盘缓存)的缓存区大小.默认是30MB.每个Cache都应该有自己的一个缓冲区.
 diskPersistent - 在VM重启的时候是否启用磁盘保存EhCache中的数据，默认是false。
 diskExpiryThreadIntervalSeconds - 磁盘缓存的清理线程运行间隔，默认是120秒。每个120s，相应的线程会进行一次EhCache中数据的清理工作
 memoryStoreEvictionPolicy - 当内存缓存达到最大，有新的element加入的时候， 移除缓存中element的策略。默认是LRU（最近最少使用），可选的有LFU（最不常使用）和FIFO（先进先出）

 
