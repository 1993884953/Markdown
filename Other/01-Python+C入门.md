# Python语言基础

## 在程序中表示数据

### 声明变量

变量名 = 值

示例:

```javascript
book_name = "深入理解计算机系统"
print(book_name)
```

### 打印

print() 

### 模板变量

format()

```python
# 定义一个用于输出的模板变量
template = "书名: {}，价格: {}，出版年份: {}"
print(template.format(book_name, book_price, publish_year))
```



## 运算符变量

### +-*/ 

使用两个斜线 `//` 整除运算只返回商的整数部份。

示例:

```
7 // 3   # 结果为2
```

### %

 将余数部份，放在一个变量中

示例

```python
total = 7300
total % 3600 # 结果为100
```



## 分支流程控制训练

### datetime

```python
import datetime                     # 使用import关键字导入系统提供的datetime模块
h = datetime.datetime.now().hour    # 获取当前几点

print("当前时间是{}点".format(h))
```

datetime模块中，提供了获取当前是星期几的方法`datetime.datetime.now().isoweekday()`，返回数字1到7，分别是周一到周日

```python
import datetime                     # 导入datetime模块
w = datetime.datetime.now().isoweekday()    # 获取星期几，放入变量w中

print("今天是星期{}".format(w))
```

### if ... elif

```
if w == 1:
    print("今天是星期一")
elif w == 2:
    print("今天是星期二")
```

## 循环

### for  in 循环

示例

```
for i in range(10):
    print("我来刷屏了，哈哈哈")
```

### while 循环

```
示例1
i = 0
while i < 10:
    print("我来刷屏了，哈哈哈")
    i += 1
示例2
password = 391                               # 先设置一个密码，存放在这个变量中
    
for i in range(9999):                        # 最大尝试次数 9999
    if  i == password:
        print("破解成功，密码是{}".format(i))
        break                                # 已破解成功，跳出循环
    else:
        print("正在尝试破解{}".format(i))    
    
```

### random 随机整数

Python提供的`random`模块中，有一个`randint`可以生成随机的整数

```javascript
import random

num = random.randint(10, 99)   # 生成一个 10到99之间的随机数，存放到变量 num 中

print(num)
```

### input()函数

为了让用户能从键盘输入数字，还需要使用到`input`函数，代码如下

```javascript
print("请输入：", end="")
value = input()                              # 把键盘输入的内容存入变量 value中
print("你输入的内容是:{}".format(value))
```

input函数输入的内容是`字符串`，如果我们需要一个`整数`，用下面这种方式进行类型转换

```javascript
print("请输入一个整数，然后回车：", end="")
value = int(input())                  # 将输入的内容，转换为整数后，存入 value 变量中
print("你输入的数是:{}".format(value))
```

### 猜数游戏

```javascript
import random

print("=============")
print("   猜数游戏")
print("=============")

# 随机生成一个数字
num = random.randint(10, 99)

while True:
    
    print("请输入你猜的数字：", end="") 
    guess = int(input())
    
    if guess == num:

        print("恭喜猜对了")
        break              # 跳出循环
    else:
        
        # 没有猜对时，提示猜大了还是小了
        if guess > num:
            print("你猜大了")
        else:
            print("你猜小了")
```

## 函数

将代码封装到一个函数中,使用更加方便,关键字def

```javascript
def signature():
    print('╭⌒╮⌒╮ .\'\',,\',\'\', ╭⌒╮⌒╮,\'\',  ')
    print()
    print('\'\'╱◥████████◣\'\'最美的不是下雨天')
    print(' ︱ 田︱田田|, 是曾与你躲雨的屋檐 ')
    print('.\'\',,\',\'\', ')
    print('╭╭⌒╮⌒╮⌒.\'\',,\',\'\', ╭⌒╮⌒╮,\'\', ')
    print('╭╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╬╮')
```

有了这个函数之后，想使用时，直接使用函数名，就能调用函数中的那些代码，像下面这样

```javascript
print("邮件标题: 学习Python中的函数")
print("邮件正文: 我学会了自己封装函数")
signature()                # 调用我们自己写的函数，Python就会执行对应函数中的代码
```



```javascript
def hello(name):
    print("大家好，我是{}".format(name))
hello("小白")
hello("大白")
```

在定义函数的圆括号中，添加了一个参数，叫`name`，打招呼的代码中，也将`小白`替换为占位符了，使用name变量进行填充。接下来，我们调用这个函数的时候，就需要告诉Python，name这个参数对应的值是什么

总结一下，定义函数，使用`def`关键字，函数名后面写圆括号，如果需要有参数，参数名字写在圆括号中

## 内置函数

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142974.png!l)

常用  print()   input()   range()     int()

### abs() 决对值

```javascript
a = -5          # 变量a的值是 -5
b = abs(a)      # 对变量a的值，求绝对值，然后将结果，存入变量b中

print(b)        # 打印变量b
```

### max() 最大值

```javascript
n = max(3, 6)    # 向 max()函数传入两个参数，分别是 3 和 6，将函数返回的结果，放入变量n中

print(n)
```

### min() 最小值

```python
n = min(3, 6)    # 向 max()函数传入两个参数，分别是 3 和 6，将函数返回的结果，放入变量n中

print(n)
```



### round() 四舍五入到小数点后指定位数

```javascript
pi = 3.1415926

print(round(pi, 2))   # 保留2位小数
print(round(pi, 3))   # 保留3位小数
```

## 创建带返回值的函数

 max() 这个系统函数，功能是返回参数中，最大的一个值

```javascript
num = max(3, 5)

print(num)
```

如果不使用这个max()系统函数，我们自己该如何实现这个类似功能呢？其实也很容易，代码如下

```javascript
def my_max(a, b):
    if a > b:
        return a
    else:
        return b


num = my_max(3, 5)    # 调用我们自己实现的 my_max() 函数

print(num)
```

在调用 my_max 函数时，括号中的第一个参数 3 ，将被传递到函数的 a 形参中，第2二个参数 5 将被传递到函数的形参 b 中，函数中的return 关键字，就是返回指定的数据

请实现一个函数，函数名为 add，接收2个参数，功能是做加法运算，返回计算的结果

```javascript
def add(a, b):
    c = a + b
    return c

# 测试一下我们写的add函数
num = add(24, 4)  # 将函数返回结果存放变量num中
print(num)
```

## 列表

列表用来在程序中方便的存储一组相关的数据，例如有3个同学的成绩需要保存，就可以放到一个列表中

```javascript
scores = [98, 95, 100]
```

如果不使用列表，我们可能需要用3个变量，才能存放这些数据，像下面这样

```javascript
score1 = 98
score2 = 95
score3 = 100
```

使用列表还有一个好处，就是可以很方便的进行循环操作，例如，我们想输出所有的成绩，只需要一个循环就以完成

```javascript
scores = [98, 95, 100]

for i in scores:
    print(i)      # 每循环一次，i 的值就会按列表中的顺序改变
```

如果只想输出某一位同学的成绩，就要用到索引,也就是下标，注意，索引是从0开始的

```javascript
print(scores[0])   # 第一位同学的成绩
print(scores[1])   # 第二位同学的成绩
print(scores[2])   # 第三位同学的成绩
```

### len()函数

```javascript
scores = [98, 95, 100]
print(len(scores))      # 输出 列表 scores  当前的长度
```

上面代码输出为3

### append()动态扩容

Python提供的列表支持动态扩容，请看下面的代码

```javascript
scores = [98, 95, 100]

scores.append(88)   # 第四个同学的成绩

print(scores)
```

Python内置函数 max() min() sum() 可以直接传入列表，进行相应的计算并返回结果，请看代码

```javascript
scores = [98, 95, 100]

print("共有{}条数据".format(len(scores)))
print("最高分为{}".format(max(scores)))
print("最低分为{}".format(min(scores)))

total = sum(scores)   # 计算总成绩
avg = total / len(scores)   # 计算平均成绩

print("总分为{}".format(total))
print("平均分为{}".format(avg))
```

### 程序名称：比赛打分

需求描述

- 程序运行后，输出欢迎信息
- 循环提示用户从键盘录入成绩(整数)
- 如果录入 -1 表示结束录入
- 去掉一个最高分，去掉一个最低分
- 计算最后得分

运行效果如下：

================

欢迎进入比赛打分系统

================

请输入第1位的成绩:100
请输入第2位的成绩:455
请输入第3位的成绩:888
请输入第4位的成绩:777
请输入第5位的成绩:-1
去掉一个最高分888,去掉一个最低分100,最后得分616.0

代码如下:

```javascript
print("================")
print("欢迎进入比赛打分系统")
print("================")

scores = []                    # 声明一个空的列表，用来存放分值

while True:
    num = len(scores)          # 当前有已录入了几个成绩
    
    print("请输入第{}位的成绩:".format(num + 1), end="")
    val = int(input())
    
    if val == -1:
        break                  # 当输入的值是 -1 时，跳出 while 循环
    else:
        scores.append(val)     # 否则把输入的值存放到 scores 列表中

height = max(scores)           # 获取最高得分
low = min(scores)              # 最低得分
total = sum(scores)            # 总分
num = len(scores) - 2          # 有效分值数量

avg = (total - height - low) / num   # 去掉最高分和最低分，计算平均分
avg = round(avg, 1)                  # 保留1位小数

print("去掉一个最高分{},去掉一个最低分{},最后得分{}".format(height, low, avg))
```

## 基础强化

```python
3用循环统计出给定数据中，有多少个2
[3, 5, 2, 7, 2, 6, 4, 4, 2, 6, 7, 9, 2]

scores2=[]
scores=[3 ,5, 2, 7, 2, 6, 4, 4, 2, 6, 7, 9, 2]
for i in scores:
    if i ==2:
        scores2.append(i)
print(len(scores2))


k=0
scores=[3 ,5, 2, 7, 2, 6, 4, 4, 2, 6, 7, 9, 2]
for i in scores:
    if i ==2:
        k+= 1   
print(k)

4输出100以内，包含7的数字，以及7的倍数，例如7、14、17、...

for i in range(1,100):
    if (i%7==0  or i%10==7):
        print(i)

5将成绩转为等级，小于60分为E、60-70(不含)为D，70-80(不含)为C，80-90(不含)为B，90以上为A

print('请输入你的分数',end='')
i=int(input())
if i<60:
    print('成绩为E')
if i>=60 and i<70:
    print('成绩为D')
if i>=70 and i<80:
    print('成绩为C')
if i>=80 and i<90:
    print('成绩为B')
if i>=90 :
    print('成绩为A')


使用循环计算出平均值、最大值、最小值
[66, 80, 93, 88, 95, 75, 70]


scores=[66,80,93,88,95,75,70]
x=len(scores)
total=0
j=0
y=scores[0]
z=scores[0]
for i in scores: 
    total=total+i
    avg=round(total/x,1)
    if y<=i:
        y=i
    if  z>=i:
        z=i
print('数组中平均数为{} 最大值为{} 最小值为{}'.format(avg,y,z))

7.写一个函数，接收一个num参数，把传入的数字，转为中文星期的几，0为周日，1为周一，...

def num(i):
    if i==0 :
        print('周日')
    if i==1 :
        print('周一')
    if i==2 :
        print('周二')    
    if i==3 :
        print('周三')
    if i==4 :
        print('周四')
    if i==5 :
        print('周五')
    if i==6 :
        print('周六')
num(6) 

8.在同一行，输出指定数量的*号，列如num=5，则输出5个*号。提示print("*", end="")这样输出后不会自动换行

方法一:
print('输入行数num=',end='')
num=int(input())
y='' 
for i in range(num):
    y='*'+y 
print(y)

方法二:
print('输入行数num=',end='')
num=int(input())
for i in range(num):
    print('*',end="")

9用*号打印指定行和列的矩形，变量row表示行数，变量col表示列数，例如row=3; col=5;时，打印出如下效果：

*****

*****

*****

print('行数为',end='' )
row =int(input())
print('列数为',end='' )
col =int(input())
print('行数为{} 列数为{}'.format(row,col) )

col_=''
for i in range(col):
    col_=col_+'*'
for i in range(row):  
     print( col_)  

10根据row变量的值，打印出对应行数的三角形，如果row为5，则打印一个5行的三角形，如下所示
*
**

***

****

*****

print('行数为',end='' )
row =int(input())
y='' 
for i in range(row):  
    y='*'+y
    print(y)


11.写一个函数，根据传入的年份，判断是否闰年，是闰年返回true，不是则返回false。符合下面条件之一的，均为闰年：

能被4整除，但不能被100整除
能被4整除，又能被400整除

def year(x):
    if (x%4==0 and x%100!=0) or (x%4==0 and x%400==0):
        print('true')
    else:
        print('false')
year(400)  

12用循环统计出给定数据中，每种数字，分别出现了多少次
[3, 5, 2, 7, 2, 6, 4, 4, 2, 6, 7, 9, 2]

scores=[3, 5, 2, 7, 2, 6, 4, 4, 2, 6, 7, 9, 2]
a =[]
b =[]
for i in scores:
    if i in a:   # 判断数字i是否存在于数组a中
        for j in range(len(a)):
            if  a[j] == i:
                b[j] = b[j] +1
        continue
    a.append(i)   #将scores中不重复的数字生成到数组a
    b.append(1)
for i in range(len(a)):
    print("{}出现了{}次".format(a[i],b[i]))



def isExist(num,nums):   #自定义函数
    exist = False
    for i in nums:
        if i == num:
            exist = True
            break
    return exist
    

scores=[3, 5, 2, 7, 2, 6, 4, 4, 2, 6, 7, 9, 2]
a=[]
b=[]
for i in scores:
   #if i in a :
    if isExist(i,a) :
        for j in range(len(a)):
            if a[j]==i:
                b[j]=b[j]+1
        continue
    a.append(i)
    b.append(1)
for j in range(len(a)):
    print('{}出现了{}次'.format(a[j],b[j]))
    
    
方法二
scores_shuzi=[]
scores=[3, 5, 2, 7, 2, 6, 4, 4, 2, 6, 7, 9, 2]
for i in scores:                   #在scores这个数组中   从i=3开始输出
    if i in scores_shuzi:          #如果i=3在数字 scores_shuzi中包含  则
        continue                   #跳过当前循环，从头开始循环 不执行scores_shuzi.append(i)后面代码
    scores_shuzi.append(i)            #i的值加入到scores_shuzi中
    j=0                                   
    for a in range(len(scores)):      #a在0~11中循坏
        if i==scores[a]:                                                                            # 如果开始循环i的值等于scores中索引的值则执行下一行代码，否则返回上一行代码继续往下执行，必须执行完12次循环，才能print输出，不管是否符合条件  j是否加一都要循环12次
            j+=1
    print("数字{}一共出现了{}次".format(i,j))
    
    
自定义函数示例

def isExist(num,nums):
    exist=False
    for i in nums:
        if i == num:
            exist=True
            break
    return exist
scores=[3, 5, 2, 7, 2, 6, 4, 4, 2, 6, 7, 9, 2]
if  isExist(2,scores):
    print('ss')

示例    
import collections
a = [1,2,3,1,2,3,4,1,2,5,4,6,7,7,8,9,6,2,23,4,2,1,5,6,7,8,2]
b = collections.Counter(a)
for c in b:
    print  (c,b[c])
```

# C 数据类型训练



## 基本框架与编译

```c
#include <stdio.h> 

int main()  
{
	printf("");  				
	return 0;
}
```

touch hello.c		创建后缀为.c的文件夹

gcc hello.c			编译文件是否会出现警告与报错

​		gcc hello.c o data	命名编译后的文件

./a.out					运行编译后的文件

echo $?  	用于return的判断文件是否有无错误

```c
#include <stdio.h>              //standard input output
								//获取头文件，固定格式

int main()                       //int向终端传入	main()函数
{
    printf("hello world\n");    //printf格式化输出 print format
    return 0;					//返回一个整数用于判断echo $?能否输出数值
}
```

### 声明定义变量

int age=18；数据类型 变量名=值

%d 	整数	以十进制的方式输出

%f	浮点数，近似值

```c
#include <stdio.h> 

int main()  
{
    int age = 18;				//声明定义age这个变量
    printf("age: %d\n",age);	//  %d获取后方	\n换行
    age = 19					//重新赋值变量
	printf("age: %d\n",age);	//输出改变后的变量

	int year;					
    printf("%d\n",year);		//声明但不赋值会输出0

    float score = 98.5;			//浮点数数据类型
    printf("score: %f\n",score);	//%d获取后方浮点数
	return 0;
}

```

### 整数类型与浮点类型

| 整数类型    | 储存大小     | 最小值                     |          最大值           |
| ----------- | ------------ | -------------------------- | :-----------------------: |
| signed char | 1个字节      | -128                       |            127            |
| int         | 2个或4个字节 | -32 768 或 -2 147 483 648  |  32767 或 2 147 483 647   |
| short       | 2个字节      | -32 768                    |          32 767           |
| long        | 4个字节      | -2 147 483 648             |       2 147 483 647       |
| long long   | 8个字节      | -9 223 372 036 854 775 808 | 9 223 372 036 854 775 807 |

| 浮点类型    | 比特(位)数 | 有效数字 | 数值范围                      |
| ----------- | ---------- | -------- | ----------------------------- |
| float       | 32         | 6~7      | -3.4* 10^-38 ~ 3.4* 10^38     |
| double      | 64         | 15~16    | -1.7* 10^-308 ~ 1. 7* 10^308  |
| long double | 128        | 18 ~19   | -1.2* 10^-4932 ~ 1. 2* 104932 |



### 数组

> 从零开始数数

数组长度有限制，不是动态变化

```c
#include <stdio.h> 

int main()  
{
	int ages[3]={18,19,22}; 
	printf("ages: %d\n",ages[0]);  
	printf("ages: %d\n",ages[1]);  
	printf("ages: %d\n",ages[2]); 
    
    ages[1] = 21;
    printf("ages: %d\n",ages[1]);
	
	return 0;
}
```

长度不能越界，编译时不提示错误

```
	int nums[10];		
	nums[10] = 99;	
```

声明时赋值

```
	int	arr[] = {18,19,22};			//系统自动获取长度
```

## 使用键盘动态录入

### 获取键盘输入端

 printf("input a: ");		input用变量获取输入值
 scanf("%d",&a);			scanf将获取到的值储存到地址a里

```c
#include <stdio.h> 

int main()  
{
    int a,b;		//声明2个变量
        printf("input a: ");
        scanf("%d",&a);			//格式化扫描,扫描键盘输入，存到a里面

        printf("input b: ");
        scanf("%d",&b);
        
        int sum;
        sum = a + b;
        printf("%d\n",sum);
        printf("%d + %d = %d\n",a,b,sum);
        
		return 0;
}
```

### 简单运算	+-*/  %

> %取得是余数

```c
#include <stdio.h> 

int main()  
{
	int num;
    num=3+4*8-6/2;
    printf("%d\n", num);
    
    num=3+4*(8-6)/2;
    printf("%d\n", num);
    
    num=5%3;
    printf("%d\n", num) ;
    				
    return 0;
}
```

## man查看帮助

man 命令符或者操作符	 查阅官方手册 	例：

> man console_ codes	查找控制台#代码
> man ascti						查ascti码
>
> echo -e  "\033[31mHelLo\033[ 0m"

```c
#include <stdio.h> 

int main()  
{
	printf("\033[41;37m");
    printf("hello")
    printf("\033[0m\n")
	return 0;
}
```

## 表示字符%d %c %s %f

charr 字符是整数

%d 表示整数

%c 表示字符

%s 字符数组

%f 表示浮点数 %.1%f代表位小数

```c
#include <stdio.h> 

int main()  
{
	int c1 = 65;
	printf("%d\n",c1);
	printf("%c\n",c1);		//char
	
	char c2 = 'A'
	printf("%c\n",c2);		//char
	printf("%d\n",c2);
	
	char name[] = {'j','a','c','k'，'\0'};
	printf("%s\n",arr); 	//sting
	
	return 0;
}
```

打印汉字

```c
#include <stdio.h>

int main()
{    
	char zou[] = {233, 130, 185, 0};
	printf("%s\n", zou);

	return 0;
}
```

## 程序逻辑

### if条件

```
if(c >= 97 && c <=112){			//条件成立,输出花括号内容
		c = c -32;		
	}
```

### 字母转换程序

```c
#include <stdio.h>

int main()
{    
	char c;
	printf("input: ");
	scanf("%c",&c);
	if(c >= 97 && c <=112){			//如果条件成立输出内容
		c = c -32;		
	}
	printf("%c",&c);
	return 0;
}
```

> && 同时成立

## for 循环语句

```
 	for(int i = 0 ; i < 7; i++){ 
        printf("%d\n",i);
    }

```

### 循环输出输入的字符

```
#include <stdio.h> 

int main()  
{
    char str[7];

	printf("input: ");
    scanf("%s",&str[7]);
    printf("%s\n",str);
    //str = {'h','e','l','l','o','\0'}		
    printf("%c",str[0]);
    printf("%c",str[1]);
    printf("%c",str[2]);
    printf("%c",str[3]);
    printf("%c",str[4]);
    printf("%c",str[5]);
    printf("%c",str[6]);
    
    for(int i = 0 ; i < 7; i++){ 
        printf("%c",str[i]);
    }
	return 0;
}
```

### 加入转换程序

```
#include <stdio.h> 

int main()  
{
    char str[7];

	printf("input: ");
    scanf("%s",str);

    for(int i = 0 ; i < 7; i++){ 

        if( str[i] == '\0'){
            break;
            }else{
            printf("%c",str[i]-32;
        }
    }
	return 0;
}
```

整数0不等于

字符串的’0‘ 0是消失

### break ，continue，return

break 跳出循环

continue跳过本次循环

return不再执行本次函数

## 指针和数组



```
` int *p;
int arr[] = {100， 200， 300}; .
//p = &arr[0];
//p = (int *) &arr;
p = arr;

//p = &arr[0];
//p = (int *) &arr;
p = arr;
printf("%p\n" ,p);
printf("%d\n", *p) ;
int i=0;	//0
i++;	 	 //1
i++;		//2


```

```

```



数组的名字是一个地址

```
int main() {
int arr[] = {100， 200， 300};
int arr2[3];
for(inti=0;i<4;i++){
	arr2[i] = arr[i] ;
}
printf("%d\n"，arr2[1]);
return 0;
}

```

```
#include <string. h>
strcpy (name2，name) ;		数据源在后面
```



```
#include <stdio.h>
#include <string. h>
int main() {
char name[10] = "hello";
char name2 [10] ;
// name2 = name;
//strcpy(char *dest, char *src);
strcpy (name2，name) ;

```

## 结构体

### 基本结构

struct 调用结构体数组需要拷

\t 换行



```c
#include <stdio.h>
#include <strcpy.h>			
	
struct User{
    int age;
    char name [10] ;
};


int main() {
    
    struct User u;
    u.age = 18;
    strcpy(u.name,"jack");          //拷贝一个数组
    print_user(&u)			    	//&u寻找出地址
        
	return 0;
}
                                                                                         void print_user(struct User *u){				//*u取出地址里面的东西
                                                                                       		printf("age\tname\n") ;
    printf("-------------\n");
  //  printf("%d\t%s\n"，（*u）.age, (*u）. name);
    printf("%d\t%s\n"，u->age, u->name) ;	//指向结构体的可以用->
    printf("-------------\n");
                                                                                         }                                                                              
```

## 结构体存入数组

```c
#include <stdio.h>
#include <strcpy.h>
#define MAX 100
	
struct User{
    int age;
    char name [10] ;
};


int main() {
    
    struct User users[MAX];
	
    
    users[0].age=18;
    strcpy(users[0].name,"jack");
    
    users[1].age=18;
    strcpy(users[2].name,"mary");
    
    for(int i=0; i<3; i++){
        printf("%d %s\n",users[i].age,user[i].name);
    }
    
    
    
	return 0;
}
```

### 循环输入结构体数组

```c
#include <stdio.h>
#include <string.h>
#define MAX 100
	
struct User{
    int age;
    char name [10] ;
};



int main() {
    
    struct User users[MAX];
	int length=0;
	while(1){
   	
    printf("[%d]input age:",length+1);
    scanf("%d",&users[length].age);
    
    printf("[%d]input name:",length+1);
    scanf("%s",users[length].name);
    
    length++;
        
     printf(“请选择 [1]继续录入 [0]返回”)
     scanf("%d",&flag);
     
     if(flag ==0){
         break;
     }
  
    }
        
        
  /*  users[0].age=18;
    strcpy(users[0].name,"jack");
    
    users[1].age=18;
    strcpy(users[2].name,"mary");
  */
    
    for(int i=0; i<length; i++){
        printf("%d %s\n",users[i].age,user[i].name);
    }
}
```





