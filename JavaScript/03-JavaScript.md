# Js 基础

## 类，对象，函数的写法

> 类的属性和值中间是等于号，不用写逗号
>
> 对象的属性和值中间是冒号，需要写逗号

### let 对象 = {}

```
let Obj ={ 
	prop1 : "hello", 
	prop2 : "hello2", 
	prop3 : new Array("helloa",1,2)
} 
obj.prop1  ==> //hello


let Obj = function (){
	prop1 = "hello", 
	prop2 = "hello2", 
	prop3 = new Array("helloa",1,2)
}

obj().prop1  ==> //hello



let a = function (){
	console.log(1231)
	min - max 
	if (){
		fir 
	}
}
```

## 箭头函数

### function	函数

```
setTimeout( function(){console. log(11)}，1000)	  //1秒后打印11
function test(){
	console.log("test")
}

setTime(test,1000)
	
setTime("test()",1000)
```

>     传一个函数不能加（），传一个字符串的函数需要用（）

### 普通函数



```
var foo =function(){
	console.log("foo...")
}

// foo...

function foo (){}

```

###  箭头函数

 箭头函数不是普通函数的缩写

```
var bar=()=>{
	console.log("bar.....")
}
```

```
setTimeout(()=>{console.log("bar")},2000)
```

```
function run(){}
setrimeout (run ,1000 )
setT imeout("run( )"，1000)
setrimeout (function( ){}，1000)

setrimeout(()=>{console.1og(1)})	 //括号里面加参数
setTimeout(_=>{console.1og(1)})		//没有参数，用下划线占位
setTimeout(_=>console.1og(1))		//只有一句可以省略花括号
```

##

### class + 类名 + {}

```
class Player{
    name = null			//类中的属性默认值用等号，后面不加分号
	level = 1
    combat(){
        console. log(`${this .name}获胜了，等级++` )	//需要在变量前面加$符号
        this.level++ 
	}
}
user1 = new Player()
user1.name = "Jack"
console.log (user1)
user1. combat()
console.log (user1)
user2 = new Player()
console.log(user2)
```

#### class   扩展名	extends	类名	{	属性	}

```
let player = {
	isVip:true,
	combat:function(){
		this.level += 2			//vip战斗胜利等级加2
	}
}
 
 player = {
	...player,
	age:"awdad",
}

//具体的
let player = {
	isVip:true,
	age:awdad,
	combat:function(){
		this.level += 2			//vip战斗胜利等级加2
	}
}
player.age




class VipPlayer extends Player{
	isVip = true 
	 combat(){
		this.level += 2			//vip战斗胜利等级加2
	}
	constructor(name,level=20){
	 	super(name,level)
	}
}
let user3 = new VipPlayer("tom",20)
user3.combat			//level +2

user3.isVip
```

## jquery

### 创建元素

```
let h1 = $("<h1>world</h1>")
$("box1").append(h1)
```

### 改变标签属性

    $("#avatar").attr("src", result.data.avatar)		//attr语法添加标签
    $(".logo").attr("src","https//www.baidu.com")        

### 更改内容

```
$("#box1").html("hello")               		 //简写模式
$("#box1").html("")                    		 //清空内容
```

### 类名

```
   $(".logo").addClass("demo")         		//追加类名
$(".logo").removeClass("demo")        		 //删除类名
```

### 点击事件

```
$("#box1").click(function(){                   //简化
    console.log("被点击")
})
$(document).on("click","div",function(event){   
	console.log(event.target.innerHTML)
})


```

```
$(document).on("click","div",function(event){     //简化
console.log(event.target.innerHTML)
	$("div").removeClass("demo") 
event.target.classList.add("demo");
})
```

```
        $(document).on("click","div",function(event){     //简化

            $("div").removeClass("demo") 
            $(this).addClass('demo')
            console.log( $(this))
        })
```



# 客户端js

## windows控制台

### 弹出提示框

```
window.alert("hello")
```

### 发生跳转

```
window.location'http:www.baidu.com'
```

### 浏览器信息

```
window.location
```

### 刷新

```
window.location.reload()
```

### 后退

```
window.history.go(-1)  -1后退一步1进一步
```

### 获取当前浏览器环境

```
window.navigator.userAgent
```

###  获取屏幕信息

```
window.screen
```



## 定时器

### setTimeout()单次执行

```
window.setTimeout（）
window.setTimeout（functiom(){console.log('hello')},2000）
//2403   

//2s到了，执行函数输出hello
```

### setInterval()重复执行

```
var num = 1;  
var timer=setInterval(()=>{console.log(num);num++;},1000)

```

### clearTimeout()清除

### clearInterval()

```
var timer=window.setTimeout（functiom(){console.log('hello')},5000）
//var timer 获取到闹钟编号
clearTimeout(timer)
//取消这个编号的闹钟
```

## js操作网页内容

### getElementById()

> 括号里面跟着id名，id是唯一

```
// Element 	获取元素
var div1 =window.document.getElementById("demo")
console.log(div1)
//得到
```

### getElementsByClassName()

> 括号里面class类名，可以获得多个

```
var div1 =window.documentgetElementsByClassName("title")
var div1 =window.documentgetElementsByClassName("title").length
//class是一个数组，显示有多少个
var div1 =window.documentgetElementsByClassName("title")[0]
//后面加数组第一个元素
console.log(div1)
```

### getElementsByTagName()

> 获取标签

```
var div1 =window.documentgetElementsByTagname("title")[0]
//后面加数组第一个元素
```

### .innerHTML获取内容

>  获取到的属性名字直接赋值

> calssName

```
div1.title='hehe'
```

> 获取标签里面文本内容

```
console.log(div1.innerHtML)
div1.innerHtML="world"
//修改元素值

```

> ##### 在元素值内创建标签

```
var demo= document.getElementById("demo")

demo.innerHTML="<h1>word</h1>"
```

### .createElement()

> 创建元素

```
var el= document.creatElement("h1")
el.innerHTML='我是新来的'
```

### .appendChild()

> ##### 新创标签

```
var demo= document.getElementById("demo")

var el= document.creatElement("h1")
el.innerHTML='我是新来的'

demo.appendChild(el)
```

### .classList.add()

>   追加类名

```
dom.classList.add("className1");
```

### .classList.remove()

>   删除类名

```
dom.classList.remove("className1");
```

### .remove()

> 移除标签

```
el.remove()
```

 更改html的style

```
div1.style.backroundColor='#abcdef'
```

## 事件发生

### .onclick

> 当被点击开始执行

### .onmouseover

> 鼠标移入

### .onmouseout

> 鼠标移出

```
var div1 =window.document.getElementById("demo")

demo.onclick=function (event){
//demo.onmouseover=(){
//demo.onmouseout=(){
 console.log("div被点击/移入、移出")
}
```

### event 事件对象

> 获取和事件相关的一些信息

```
demo.onmouseover=function (event){
	console. log (event.offsetX)		
	console. log (event.offsetY)
    //console. log (event）

 console.log("鼠标移入")
}
```

### .onkeydown

> 键盘被按下

```
var div1 =window.document.getElementById("demo")

demo.onkeydown=function (event){
 	console.log(evet.keyCode)
}
```

## 表单事件

### .onsubmit

> 表单提交

```
<form action="" id="form1">
 	<div id="message"></div>
    <div>
   		Username<input type="text" id="username" value="jack">
    </div>
    <div>
	    <button type=" submit">提交</button>
    </div>
   
</ form>
<script>
	let form = document。getElementById("form1")
	form1.onsubmit=function(){					//表单提交
	
		let username=document.getElementById("username").value
		if (username.length<4){
		//	alert("用户名不能小于4个长度")		//弹框
			document.getElemenyById("message").innerHTML='用户名不能小于4个长度'
			return false
		}
	}
```

## input事件

### .onfocus 焦点光标

###  .onblur 失去焦点

### .onchange 发生改变

```
    let txtUsername = document.getELementById("username")
    
    txtUsername.onchange=function(event){
    	console.long(event.target.value)		//事件在哪一个对象上面发生了
    }
    
    let form1=documemt.getElementById("form1")
    txtUsername.onblur = function () {
        console. log ("onblur")
    }
```



# 《使用JavaScript入门编程语言》

> 作者: 邹义良  [http://www.itnova.top]
>
> 版权所有，未经授权禁止转载

 

JavaScript` (缩写: js) 是一门完备的动态编程语言，语法相当简洁，却非常灵活，应用场合极其广泛，网页开发、App开发、服务端编程、数据库查询等领域都有广泛的使用。如果你没有任何编程经验，使用`JavaScript`作为入门语言，将是不错的选择。文本主要讲解编程语言中一些较为通用的概念，这些知识绝大部份同样也适用于`C`、`Java`、`PHP`、`Python`、`Go`等主流开发语言。

 

## 一、基础语法

### 程序

程序是给计算机执行的一系列指令，使用 `分号` 表示一句指令结束。编程语言中，提供了很多内置指令，下面的代码被执行后将输出 `Hello World!`

```
console.log("Hello World!");
```

打开`Chrome`浏览器，按下键盘上的 `F12 键` (注意某些笔记本，可能是 `fn + F12` )，找到控制台 `Console`选项卡，将代码复制过去，并接下回车，观察代码运行效果。

在控制台输入的代码，不方便修改。建议使用文本编辑器(例如: [*Visual* Studio *Code*](https://code.visualstudio.com/))来写代码，在编辑器中新建一个文件 `hello.html`，内容如下

```
<script>
  console.log("Hello World!");
</script>
```

保存后，使用浏览器打开这个文件，你将会在控制台看到输出的`Hello World!`。

 

### 表示数据

- 数字
- 文本

在程序中经常要表示数字和文本，数字直接书写即可，表示文字则需要在内容的两端加上双引号，叫作`字符串`。

```
console.log(18);
console.log(98.5);
console.log("Hello World!");
```

 

### 转义字符

一些特殊的字符，需要用特殊的方式来表示。

例如：换行符要使用 `\n` 、表示`双引号`要使用 `\"` ，表示一条`反斜线`需要使用 `\\`

```
console.log("Hello\nWorld!");
console.log("\"Are you crazy?\" Jack called.");
```

 

### 注释

程序中加入注释，不会影响程序执行，是为了便于人们理解程序代码。 以 `/*` 开始到 `*/` 之间的内容就是注释，可以有多行，叫`多行注释`。 从 `//` 开始到该行末尾的这部份也是注释，叫`单行注释`。

```
/*
 这是一个示例程序
 示范如何在控制台打印出 Hello World!
*/
console.log("Hello World!");        // 打印字符串，需要加上双引号
```

 

## 二、变量

### 声明

变量(Variable)是用来在程序中存放数据的容器，使用`var`关键字声明变量。通常我们用一些有意义的英文单词作为变量名，例如想存放一个人的年龄，就可以声明一个叫`age`的变量。关键字 `var` 与变量名 `age` 之间，需要使用 `空格` 来进行分隔。

```
var age;                           // 声明一个叫age的变量
var name;                          // 声明一个叫name的变量
```

 

### 赋值

赋值 是向变量中存入指定的内容，使用符号 `=` 来操作。注意这不是数学方程中的等号，编程语言中的赋值是将 `=` 右边的数据，存入其左边的变量中。使用变量名的时候，不能加引号。

```
var age;                          // 声明一个叫age的变量
age = 18;                         // 将整数18存入变量age中
console.log(age);                 // 输出变量age中的内容，会输出18

age = 19;                         // 从新赋值后，变量中的内容被修改
console.log(age);                 // 此时变量age中的内容为19

var pi = 3.14;                    // 声明一个叫pi的变量，同时给变量赋值为3.14
console.log(pi);     
```

 

## 三、运算符

- 算术运算符
- 比较运算符
- 逻辑运算符
- 三元运算符

 

### 算术运算符

算术运算符与数学中的四则混合运算规则相同，使用小括号可改变优先级。

```
var num = 1 + 2 * (3 + 4) / 5 - 6;
console.log(num);               // 运算结果为 -2.2

// 如果变量存放的是字符串，加号将连接字符串，而不是做数学加法
var firstName = "Smith";
var lastName = "Tom";
var hello = "Hi, " + lastName + " " + firstName;
console.log(hello);    // Hi, Tom Smith
```

 

取模运算符 `%` 用于计算除法的余数。

```
var num = 7 % 3;
console.log(num);               // 输出1 (7÷3 = 2······1)
```

 

自增 `++` 表示将变量中的内容增加1

自减 `--` 表示将变量中的内容减少1

```
var age = 18;
age++;
console.log(age);                    //19

var num = 100;
num--;
console.log(num);                    //99
```

如果我们想让变量的值，在当前值基础上自增2，可以用如下方式

```
var num = 1;                        // 声明变量num，并赋值为1
num = num + 2;                      // 先计算 num + 2 的值，然后从新赋值给num变量
console.log(num);                   // 此时num变量中的值为3
```

可以写成如下的方式

```
var num = 1;
num += 2;                           // num变量自增2
console.log(num);                   // 此时num变量中的值为3
```

除了 `+=`，还有 `-=` 、 `*=`、  `/=`  分别表示在变量自身基础上，减去、乘以、除以一个数，再从新赋值给该变量。

 

### 比较运算符

`比较运算符`得到的结果是一种特殊的数据类型，叫`布尔类型`(boolean)。`布尔类型`有两个值，分别是 `true`、`false` 。我们用`true`来表示真，即条件成立，`false`表示假，即条件不成立。注意`true`和`false`两边没有引号。

| 运算符 | 描述     | 返回值                                                |
| ------ | -------- | ----------------------------------------------------- |
| `>`    | 大于     | 当左边大于右边时，返回 `true`，否则返回 `false`       |
| `<`    | 小于     | 当左边小于右边时，返回 `true`，否则返回 `false`       |
| `>=`   | 大于等于 | 当左边大于或等于右边时，返回 `true`，否则返回 `false` |
| `<=`   | 小于等于 | 当左边小于或等于右边时，返回 `true`，否则返回 `false` |
| `!=`   | 不等于   | 两边不相等时，返回 `true`，否则返回 `false`           |
| `==`   | 等于     | 两边相等时，返回 `true`，否则返回 `false`             |

 

```
var age = 18;
console.log(age > 18);                // false
console.log(age < 18);                // false
console.log(age >= 18);               // true
console.log(age <= 18);               // true
console.log(age != 18);               // false
console.log(age == 18);               // true
```

注意比较运算符 `==` ，不要误写为赋值符号 `=` 。

 

### 逻辑运算符

逻辑运算符用来表示 `并且`、`或者` 、`取反` 这样的逻辑关系。

| 运算符 | 描述         | 返回值                                                       |
| ------ | ------------ | ------------------------------------------------------------ |
| `&&`   | 逻辑与 (and) | 两边都为`true`时，才返回 `true`，否则返回 `false`            |
| `||`   | 逻辑或 (or)  | 任意一边(或两边)为true，返回 `true`，两边都是`false`，才返回 `false` |
| `!`    | 逻辑非       | 右边为`false`时，返回 `true`，否则返回 `false` (针对右边的表达式) |

 

```
console.log(true && true);         // true   两边都为true
console.log(true && false);        // false  两边都是true才会返回true，所以这里返回了false
console.log(true  || false);       // true   逻辑或 不需要两边为true，只要有一边true就会返回true
console.log(false || true);        // true   逻辑或
console.log(true  || true);        // true   逻辑或
console.log(false || false);       // false  逻辑或
```

 

```
var a = 95;
var b = 88;

console.log(a >= 90 && b >= 90);      // false
console.log(a >= 90 || b >= 90);      // true

var result = a < 90;                  // 比较结果不成立，得到false，存到变量result中
console.log(result);                  // false
console.log(!result);                 // 变量reuslt中的内容为false，所以逻辑非运算符返回true
```

 

### 三元运算符

三元运算符 `?:` 可以表示简单的逻辑判断，`问号`前面的条件如果成立，返回`冒号`前的内容，否则返回`冒号`后的内容。

```
var age = 17;
console.log(age >= 18 ? "我的世界我做主": "我还是个孩子");
```

 

## 四、流程控制

- 分支结构
- 循环结构
- 特殊关键字

 

### 分支结构

分支结构用于根据不同的条件，选择执行某些代码。

`if`关键字判断后面括号中的条件，如果括号中的结果为`true`，则执行后面花括号中的内容，如果括号中的结果为`false`，花括号中的内容将不会被执行。

```
var age = 17;

if(age >= 18){
    console.log("我的世界我做主");
}
```

上面代码中，条件不成立，运行程序将什么也不会输出。如果将变量的值改为18或更大的值，将会输出 `我的世界我做主`。

如果`if`中的条件不成立时，想让程序执行另一些代码，可以用 `if...else`结构

```
var age = 17;

if(age >= 18){
    console.log("我的世界我做主");
}else{
    console.log("我还是个孩子");
}
```

对于多条件分支的情况，例如想根据考试成绩来评级，可以用 `else if` 结构

```
var score = 82;

if(score >= 90){
    console.log("A");
}else if(score >= 80){
    console.log("B");
}else if(score >= 70){
    console.log("C");
}else if(score >= 60){
    console.log("D");
}else{
    console.log("E");
}
```

`else if`结构可以方便的进行范围判断，如果是单值判断，可以用`switch case`结构

```
var color = 2;          //用数字表示颜色 1:红灯、2:绿灯、3:黄灯

switch(color){
    case 1:
      console.log("当前是红灯");
      break;
    case 2:
      console.log("当前是绿灯");
      break;
    case 3:
      console.log("当前是黄灯");
      break;
    default:
       console.log("无法识别的颜色值");
}
```

`switch`关键字将根据后面小括号中的值，来决定选择某一个`case`中的代码块执行 。如果没有匹配的`case`块，将执行`default`块中的代码。

注意`case`块中不要漏掉`break`关键字，否则将会穿透到后面的`case`块中。下面的代码，没有`break`关键字，`switch`根据变量`color`中的值，选择执行`case 2`中的代码，但`case 2`中没有`break`，在执行完`case 2`中的代码后，将继续执行后面`case`块

```
var color = 2;           //用数字表示颜色 1:红灯、2:绿灯、3:黄灯

switch(color){
    case 1:
      console.log("当前是红灯");
    case 2:
      console.log("当前是绿灯");
    case 3:
      console.log("当前是黄灯");
    default:
      console.log("无法识别的颜色值");
}
```

 

### 循环结构

>   `for...in` 循环遍历的结果是数组元素的下标，而 `for...of` 遍历的结果是元素的值：

使用循环结构可以重复执行指定的代码块，经典的循环结构是`for`循环

下面通过一个变量 `i`，来控制`for`循环的次数，当变量 `i` 小于10的时候，将执行后面花括号中的代码，每执行1次，变量 `i`的值，将会自增 `1` 。直到 `i < 10`这个条件不成立才停止循环。

```
for(var i=0; i<10; i++){
    console.log("我将被重复", i);  // 变量i的值，从0到9变化
}
```

注意for循环小括号中，必须要有两个分号。

 

如果不使用for循环，也可以用while关键字进行循环，达到同样的效果。当while后面小括号中条件为true时，将重复执行后面花括号中的内容。

```
var i = 0;
while(i < 10){
    console.log("我将被重复", i);
    i++;
}
```

 

while循环还有一个变体，`do while`，这个结构，先执行do后面花括号中代码，然后判断while后小括号中的条件，如果条件成立，将重复执行花括号中的代码，然后再次判断……

```
var i = 0;
do{
    console.log("我将被重复", i);
    i++;
}while(i < 10);             // 注意最后有个分号
```

使用`do{}while();`结构时，花括号中的代码，至少会被执行1次。

使用`while(){}`结构时，如果while中的条件一开始就不成立，则花括号中的代码一次也不会被执行。

 

### 特殊关键字

使用`break`关键字，可以在循环的过程中提前结束循环

```
for(var i=0; i<10; i++){
  
    if(i==5){       // 当i等于5时，将进入if结构，执行里面的break
        break;      // 遇到break后，循环提前结束
    }
    console.log(i);
}
```

 

使用 `continue` 关键字，可以跳过本次循环中后面未执行的代码，下面的程序，将输出 `012346789`，中间`i`为5的那次循环，被`continue`跳过了。

```
for(var i=0; i<10; i++){
  
    if(i==5){      // 当i等于5时，将进入if结构，执行里面的continue
        continue;  // 遇到continue后，跳过本次循环后面未执行的所有代码
    }
    console.log(i);
}
```

 

```
break`、`continue` 关键字，同样适用于 `for`、 `while`、 `do ... while
```

 

## 五、函数

### 函数声明与调用

为了方便管理和复用程序中的代码片段，我们将相关的代码组织在一起，放在一对花括号中，这就是`函数`。通常还会为函数取一个有意义的名字，这个名字就叫`函数名`。声明函数，需要用一个`function`关键字，下面声明一个叫`welcome`的函数，函数名后面，需要有一对小括号，然后是一对花括号。

```
function welcome(){
  console.log("=================");
  console.log("|   欢迎学习编程  |");
  console.log("=================");
}
```

有了函数之后，通过函数名，就可以调用该函数，只需要写上函数名和圆括号，就能调用该函数，即执行该函数中的代码。如果函数不调用，函数体中的代码是不会被执行的。

```
welcome();        // 调用 welcome 函数
```

 

函数可以声明一个或多个参数，用于在调用函数时传入，以改变函数的行为，下面这个`hello`函数，接收一个`name`参数(形参)。调用该函数时，需要传入一个具体的值(实参)。

```
function hello(name){
  console.log("Hi, I'm", name);
}

hello("Jack");    // 将 "Jack"字符串，传入到函数中的name参数中，函数打印 Hi, I'm Jack

hello("Mary");    // 再次调用hello函数，这次传入 "Mary", 函数将打印 Hi, I'm Mary
```

 

函数中还可以返回数据，使用`return`关键字

```
function add(x, y){
   var z = x + y;
   return z;             // 将计算的结果返回
}

var sum = add(123, 456);  // 将123传入形参x中，将456传入形参y中，将函数返回的结果，赋值给sum变量
console.log(sum);         // 函数中返回的值是 579
```

 

### 作用域

- 局部变量
- 全局变量

在函数中声明的变量为`局部变量`，仅在函数中有效。下面的`1、2、3、4`为程序执行顺序，按这个顺序阅读代码

```
function demo(){
  var num = 123;             // 2. 在函数内部声明一个num局部变量，赋值为123
  console.log(num);          // 3. 这行代码，与num变量同在一个作用域内，可以访问到这个num变量
}

demo();                      // 1. 调用函数，进入到函数体中执行代码

console.log(num);            // 4. 不在num变量所在的作用域内，访问该变量将报错 num is not defined
```

 

在函数外声明的是全局变量，全局有效

```
function demo(){
   console.log(num);        // 3. 函数中，可以访问到全局变量，输出123
}

var num = 123;              // 1. num变量在函数外声明的，是全局变量

demo();                     // 2. 调用函数，进入到函数体中执行代码

console.log(num);           // 4. 与变量在同一个作用域，可以访问到该变量，输出123
```

 

## 六、数组

数组用来在程序中方便的存储一组相关的数据，使用中括号，将数据放在其中。下面我们用一个数组来表示3个姓名数据，给这3条数据编上序号(`索引、下标`)，从0开始， `0`对应Jack，`1`对应 Mary，  `2`对应Lily

```
['Jack', 'Mary', 'Lily']
```

把数组赋值给一个变量，就可以通过`变量名`和`索引`来访问数组中的`元素`

```
let names = ['Jack', 'Mary', 'Lily'];

console.log(names[0]);            // Jack
console.log(names[1]);            // Mary
console.log(names[2]);            // Lily

console.log(names.length);        // 数组名.length 可以动态获取数组的长度，这个数组长度为3

names[1] = 'Tom';                 // 通过索引，可以修改数组中指定元素的值
console.log(names);               // 修改后，数组就变成了 ["Jack", "Tom", "Lily"]
```

结合for循环，我们可以方便的遍历数组中所有元素

```
let names = ['Jack', 'Mary', 'Lily'];

// 数组长度为3，所以i在循环中的变化为 0, 1, 2 刚好对应数组的索引
for(var i=0; i<names.length; i++){ 
  console.log(names[i]);
}

// 第1次循环，i的值为0，names[i]，就是names[0]，输出 Jack
// 第2次循环，i的值为1，names[i]，就是names[1]，输出 Mary
// 第3次循环，i的值为2，names[i]，就是names[2]，输出 Lily
```

 

## 七、扩展

- 进制
- 浮点运算的精度
- 运算符优先级
- `i++`与`++i`的区别

 

### 进制

`十进制` 这是我们平常用于计数的方式，满十进位，用1位数最大可以表示10种不同的状态(0~9)

`八进制` 满八进位，用1位数最大可以表示8种不同的状态 （0~7）八进制只需要使用0~7这8个数字。

为了与十进制数区分，表示8进制，通常在数字前面加 `0o` (数字0后面跟一个字母o) 例如 `0o10` 就是十进制的`8`

```
console.log(0o7);                               // 将输出 7 (十进制)
console.log(0o10);                              // 将输出 8 (十进制)
```

`十六进制`  满十六进位，用1位数，最大可以表示16种不同的状态 (0~9, a-f)，为了区别于十进制，通常加`0x`前缀(数字0后面跟一个字母x)。

十六进制要满十六才进位，所以在表示十进制10的时候，仍然不用进位，用`0xa`表示，十制进的15，用`0xf`，十进制的16就需要用两位来表示了，即`0x10`

```
console.log(0x9);              // 将输出  9 (十进制)
console.log(0xa);              // 将输出 10 (十进制)
console.log(0xb);              // 将输出 11 (十进制)
console.log(0xc);              // 将输出 12 (十进制)
console.log(0xd);              // 将输出 13 (十进制)
console.log(0xe);              // 将输出 14 (十进制)
console.log(0xf);              // 将输出 15 (十进制)
console.log(0x10);             // 将输出 16 (十进制)
console.log(0x11);             // 将输出 17 (十进制)
```

 

`二进制`  满二进位，用1位数，最大可以表示2种不同的状态，即0和1这两种。表示二进制，以`0b`作为前缀

```
console.log(   0b0);             // 将输出 0 (十进制)
console.log(   0b1);             // 将输出 1 (十进制)
console.log(  0b10);             // 将输出 2 (十进制)
console.log(  0b11);             // 将输出 3 (十进制)
console.log( 0b100);             // 将输出 4 (十进制)
console.log( 0b101);             // 将输出 5 (十进制)
console.log( 0b110);             // 将输出 6 (十进制)
console.log( 0b111);             // 将输出 7 (十进制)
console.log(0b1000);             // 将输出 8 (十进制)
console.log(0b1001);             // 将输出 9 (十进制)
console.log(0b1010);             // 将输出10 (十进制)
console.log(0b1011);             // 将输出11 (十进制)
```

 

我们来算一下这个二进制数，转为十进制，是多少？

`0b01111111111111111111111111111111`     (共31个1)

即为`2^31-1`    十进制表示为：`2147483647` (21亿+)

在32位的系统中，这是带符号整数的最大取值范围，最前面那个0，是符号位，用来标记是正数还是负数。

如果不需要表示负数，32位全部为1时，就可以表示十进制的 `4294967295`  (42亿+)

 

可以使用如下方法，输出不同进制的字符串表示

```
var num = 12;                           // 十制制的12
console.log(num.toString(16));          // 输出num的十六进制   c
console.log(num.toString(8));           // 输出num的八进制    14
console.log(num.toString(2));           // 输出num的二进制    1100
```

 

手工将十进制数`11`转为二进制：

```
11 / 2  = 5 ...... 1
 5 / 2  = 2 ...... 1
 2 / 2  = 1 ...... 0
```

从最后一个商开始，连同所有的余数自下而上连起来，得到 `1011`，就是十进制数`11`的二进制表示方式

 

手工将二进制`1011`转为十进制，从右数第n位上的值乘以2的(n-1)次方，然后全部加起来

```
1       0       1       1
1*2^3 + 0*2^2 + 1*2^1 + 1*2^0  = 11
```

 

单位转换：

1个二进制位，叫`bit`

8个二进制位，叫做1个字节 `Byte`

1024字节 等于 1K

1024K      等于  1M

1024M     等于 1G

 

如果用32个二进制位来存放一个整数，那么一个整数就是占用4个字节

 

### 浮点运算的精度

 

先来看一个奇怪的bug

```
console.log(0.1 + 0.2 == 0.3);             // 结果是 false
```

 

这不是JavaScript的锅，其它主流编程语言，也一样存在这样的bug (下面的代码，不支持在浏览器中执行)

```
//C
printf("%d", 0.1 + 0.2 == 0.3);         // 0

//PHP
var_dump(0.1 + 0.2 == 0.3);             // false

//Python3
print(0.1 + 0.2 == 0.3);                // False

//Java
System.out.println(0.1 + 0.2 == 0.3);   // false
```

 

要弄清楚这个问题，需要了解浮点数在计算机中的表示方式

```
console.log((0.1).toString(2));    // 打印出0.1的二进制表示，结果如下
// 0.0001100110011001100110011001100110011001100110011001101
```

我们手工来转换一下，采用`乘2取整，顺序排列`法

用2乘十进制小数，可以得到积，将积的整数部分取出，再用2乘余下的小数部分，重复直到积中的小数部分为零

```
//连续乘以2     取出整数部分
0.1*2=0.2     0
0.2*2=0.4     0  //无限循环 0011
0.4*2=0.8     0
0.8*2=1.6     1
0.6*2=1.2     1
0.2*2=0.4     0  //无限循环 0011
0.4*2=0.8     0
0.8*2=1.6     1
0.6*2=1.2     1

//无限循环，计算机只能取一个近似值
0.0001100110011001100110011001100110011001100110011001101
```

原来计算机表示浮点数不精确，`0.1`不能被精确表示，那么浮点运算，自然就会有误差

```
console.log((0.1).toFixed(32))           // 0.10000000000000000555111512312578
console.log(0.1 + 0.2);                  // 0.30000000000000004
console.log((0.1 + 0.2).toFixed(32));    // 0.30000000000000004440892098500626
console.log((0.3).toFixed(32));          // 0.29999999999999998889776975374843
```

 

如果需要判断两个浮点是否相等，只需要将误差控制在一定范围就行。ECMA标准定义了`Number.EPSILON`这个精度值，大约是2.22e-16，两个相减得到的结果小于这个值，我们可以认为是相等的。

```
var num = 0.1 + 0.2;
console.log(num == 0.3);                    // false
console.log(num - 0.3 < Number.EPSILON);    // true
```

 

 

更多浮点相关知识可参考 IEEE 754标准：

https://standards.ieee.org/content/ieee-standards/en/standard/754-2019.html#Working

https://babbage.cs.qc.cuny.edu/IEEE-754.old/Decimal.html

[IEEE754计算器](http://weitz.de/ieee/)

 

### 运算符优先级

 

下表按照优先级从高到低列出了运算符。同一行中的运算符具有相同优先级，此时它们的结合方向决定求值顺序。

| **结合方向** | **运算符**            | **附加信息** |
| ------------ | --------------------- | ------------ |
| 右           | ++、 --               | 递增/递减    |
| 右           | !                     | 逻辑运算符   |
| 左           | *、 /、 %             | 算术运算符   |
| 左           | + 、 -                | 算术运算符   |
| 无           | < 、 <=、 > 、 >=     | 比较运算符   |
| 无           | == 、 !=              | 比较运算符   |
| 左           | ? :                   | 三元运算符   |
| 右           | =、+=、-=、*=、/=、%= | 赋值运算符   |

为了增加程序的可读性，建议合用小括号，明确指定优先级，不依靠运算符优先级和结合性来决定。

 

### i++ 与 ++i 的区别

`++`在后，先使用变量的值，然后再自增

```
var i = 0;
var j = i++;
console.log(j);   // 0
console.log(i);   // 1
```

`++`在前，先自增，然后再使用变量的值

```
var i = 0;
var j = ++i;
console.log(j);   // 1
console.log(i);   // 1
```

关于`++`在前与`++`在后，同样适用于`--`。

# 变量与数据类型

## typeof 类型

| 类型typeof | 含义                               | 例console.log(typeof 1==2);   |
| :--------- | ---------------------------------- | ----------------------------- |
| boolean    | 逻辑值 true or false  判断         | console.log(typeof 1==2);     |
| null       | 已知的变量表示空；                 | var foo =bull                 |
| undefined  | 未赋值；                           | console.log(foo);             |
| number     | 整数或者浮点数                     | console.log(typeof 1.222);    |
| bigint     | 很大的整数                         | console.log(1n +2n);          |
| string     | 表示字符串                         | console.log(typeof  “hello”); |
| Symbol（） | 符号类型；用于区分特殊且不可变的值 |                               |
| object     | 对向类型；属性和方法的集合         |                               |

> 前七个是原始不可变的类型

## 变量var let

var 变量名	或

var 变量名=值；

```
var age
var num=100;
console.log(num);
```

let 数据类型是自动转换,本能重复声明

let 只在作用域起作用

```
let x =100
console.log(typeof x)
let x = "hello world"
console.log(typeof x)
```

## 字符串

\ 	是转义字符		单引号和双引号没有任何区别

```
Let name =”jack"
Let msg='Hi,'+ name		//字符串会相互连接

let msg =`hi,${name}`	//`${}`另外一种方式
console. log (msg)		
```

## 对向

对向;提供一写函数

Math.abs	数学对向，绝对值

```
//   Math	方法 method
console.log(typeof Math)
console.log(Math.abs(-2))
console.log(Math.random())	随机小数
console.log(Math.ceil(2.14))向上取整
console.log(Math.floor(2.14))向下取整
console.log(Math.pow(2，20)) 2 的 20次幂

```

```
属性
console.log(Math.PI)
console.log(Math.E)
```



```
对象可以自定义
function add(a,b)
    let result =a+ b
	return result
}
console.log(add(1, 4))

let Cale = {
    add ;function(a, b) {let result=a+b
    }
    

```

方法

```
Let Cale = {
	version:"v1.0"
	author:
	add: function(a, b) {
 		Let	result=a+b
		return result
},
	multiply: function (a,b) {
        return a * b
    

}
console. log(Cale.add( a: 1，b: 4))
console. log(Cale.multiply( a: 2，b: 4))
console. log(Cale. author)

```

## 类型转换

```
console. log("1"+2)	自动换成字符串输出 12

console. log(parseInt(  "100px"))		字符串转化位整数处理	100

console. log(parseFloat(  "100.215px")  自动换为小数	100.215
```

```
NaN 		Not A  Number 	表示不是数字的一种值

console. log(parseInt( s: "ABCDEFG"))
console. log(isNaN(num))	用来判断变量是不是nan

let	n=null
console. log(n + 3)		输出3

let	n=undefined
console. log(n + 3)		输出NaN
```

== 自动转换

===不自动转换

## 流程控制

```
switch  不会转换类型

let num = "3"
switch (num) {
    case 2:
    console. log("星期二”)
    break
    case 3:
    console. log("星期三”)
    default :
    console. log ("未知")
}
```

函数

```
function add(a, b) {
return a + b
}
function sub(a, b) {
return a - b
}

function calc(a, b, cb) {	//回调函数
	return cb(a, b)
}
let	m=2
let	n=4
console. log(calc(m, n, sub))


console. log(calc(m, n,cb: function (a, b) {
return a * b
}))			//匿名函数


```

````
function calc(a, b, cb) {
return cb(a, b)
}
let m=2
let n=4
console. log(calc(m, n, cb: (C, d) => { 
return c + d
}))
箭头函数
````

## 数组	特殊对象

arr.push()  动态扩容

arr.length  数组长度

```
let arr = ['jack',mary' ]
console. log(arr[0] )
arr.push('lily')
console.log(arr. length)
console.log(arr)

```

arr.slice(1,2)	 截取不包含2

```
let arr = ['jack'，mary' ]
arr. push( 'lily')
console. log(arr.slice(0,2))

```

循环便利

```
let users =[
    {name: "jack",age: 18， sex:1},
    {name: "mary", age: 20，sex: 2},
    {name: "lily", age: 19， sex: 2},
]
for (let i = 0; i < users.length; i++) {
	console.log(users[i].name)
}

for ( let user of users) {
	console.log (user.name)
}

for (let i in users) {
	console.log(i, users[i].name)
}
```



## 常用内置对向

```
String Array Math Date JSON RegExp Promise
```

## string

### charAt()	

从一个字符串中返回指定的字符。

```
var anyString = "Brave new world";  

console.log("The character at index 0   is '" + anyString.charAt(0)+ "'");
//The character at index 0 is 'B' 
```

### includes()

判断一个数组是否可能包含一个指定的值，根据情况，如果可以返回真实，否则返回虚假。用于判断字符串是否包含指定的子字符串。

```
const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
//expected output: true
```

### endsWith()

判断当前字符串是否是另外一个给定的子字符串“结尾”的，根据判断结果返回`true`或`false`。

```
pconst str1 = 'Cats are the best!';

console.log(str1.endsWith('best', 17));
//expected output: true
```

### indexOf()

返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

```
const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

console.log(beasts.indexOf('bison'，2));
//expected output: 4 
```

### lastIndexOf()

 返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个索引，如果不存在则返回 -1 `fromIndex`。

```
const animals = ['Dodo', 'Tiger', 'Penguin', 'Dodo'];

console.log(animals.lastIndexOf('Dodo'));
//expected output: 3
```

### padEnd()

会用一个字符串填充动态字符串（如果需要的话则填充填充），返回填充后达到指定长度的字符串。从当前字符串的开始（方法）开始填充。

```
const str1 = 'Mushrooms';

console.log(str1.padEnd(25, '.'));
//expected output: "Mushrooms........"
```

### padStart()

方法用另一个字符串填充当前字符串（如果需要的话，会重复多次），以便产生的字符串达到定的长度。从当前字符串的起始开始填充。

```
const fullNumber ='2034399002125581'
const last4Digits = fullNumber.slice(-4);
const maskedNumber = last4Digits.padStart(fullNumber.length, '*');

console.log(maskedNumber);
// expected output: "************5581"
```

### repeat()

构造并返回一个新的字符串，该字符串包含被连接的指定数量的字符串的副本。包括指定字符串的指定数量副本的新字符串。

```
"abc".repeat(-1)     

// RangeError: repeat count must be positive and less than inifinity "abc".repeat(0)     
// "" 
"abc".repeat(1)     
// "abc" 
"abc".repeat(2)     
// "abcabc" 
"abc".repeat(3.5)    
// "abcabcabc" 参数count将会被自动转换成整数.
"abc".repeat(1/0)    
// RangeError: repeat count must be positive and less than inifinity

({toString : () => "abc", repeat : String.prototype.repeat}).repeat(2) 
//"abcabc",repeat是一个通用方法,也就是它的调用者可以不是一个字符串对象.
```

### replace()

方法返回一个由替换值（`replacement`）替换部分或所有的模式（`pattern`）匹配项后的新字符串。模式可以是一个字符串或者一个[正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)，替换值可以是一个字符串或者一个每次匹配都要调用的回调函数。**如果`pattern`是字符串，则仅替换第一个匹配项。**

```
const p = 'The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?';

console.log(p.replace('dog', 'monkey'));
// expected output: "The quick brown fox jumps over the lazy monkey. If the dog reacted, was it really lazy?"

const regex = /Dog/i;<br/>console.log(p.replace(regex, 'ferret'));
// expected output: "The quick brown fox jumps over the lazy ferret. If the dog reacted, was it really lazy?"

```



### search()

方法执行正则表达式和[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)对象之间的一个搜索匹配。

```
const paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';

// any character that is not a word character or whitespace
const regex = /[^\w\s]/g;

console.log(paragraph.search(regex));
// expected output: 43

console.log(paragraph[paragraph.search(regex)]);
// expected output: "."

```



### split()

使用指定的分隔符字符串将一个[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置。 

```
const str = 'The quick brown fox jumps over the lazy dog.';

const words = str.split(' ');
console.log(words[3]);
// expected output: "fox"

const chars = str.split('');
console.log(chars[8]);
// expected output: "k"

const strCopy = str.split();
console.log(strCopy);
// expected output: Array ["The quick brown fox jumps over the lazy dog."]

```



### startsWith()

判断当前字符串是否以另一个给定的子字符串开头，并根据判断结果返回`true`或`false`。

```
const str1 = 'Saturday night plans';

console.log(str1.startsWith('Sat'));
// expected output: true

console.log(str1.startsWith('Sat', 3));
// expected output: false
```



### substring() 

方法返回一个字符串在开始索引到结束索引之间的一个子集，或从开始索引直到结束的一个子集。

```
var anyString = "Mozilla";

// 输出 "Moz"
console.log(anyString.substring(0,3));
console.log(anyString.substring(3,0));
console.log(anyString.substring(3,-3));
console.log(anyString.substring(3,NaN));
console.log(anyString.substring(-2,3));
console.log(anyString.substring(NaN,3));

// 输出 "lla"
console.log(anyString.substring(4,7));
console.log(anyString.substring(7,4));

// 输出 ""
console.log(anyString.substring(4,4));

// 输出 "Mozill"
console.log(anyString.substring(0,6));

// 输出 "Mozilla"
console.log(anyString.substring(0,7));
console.log(anyString.substring(0,10));
```

### toLowerCase()

 调用该方法的字符串值转为小写形式，并返回

```
console.log('中文简体 zh-CN || zh-Hans'.toLowerCase());
// 中文简体 zh-cn || zh-hans

console.log( "ALPHABET".toLowerCase() );
// "alphabet"
```





### toUpperCase()

 将调用该方法的字符串转为大写形式并返回（如果调用该方法的值不是字符串类型会被强制转换）。

```
const sentence = 'The quick brown fox jumps over the lazy dog.';
a
console.log(sentence.toUpperCase());
// expected output: "THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG."

```



### trim()

方法会从一个字符串的终端删除空白字符。在这个上下文中的空白字符是所有的空白字符（空格、制表符、无中断空格等）以及所有行终止符字符（如LF，CR等）。

```
const greeting = '   Hello world!   ';

console.log(greeting);
// expected output: "   Hello world!   ";

console.log(greeting.trim());
// expected output: "Hello world!";
```





## Array数组



### pop() 

从数组中删除最后一个元素，并返回该元素的值。

```
const plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];

console.log(plants.pop());
// expected output: "tomato"
```

### push() 

将一个或多个元素添加到汇总的详细信息中，并返回该数组的新长度.

```
const animals = ['pigs', 'goats', 'sheep'];

const count = animals.push('cows');console.log(count);
// expected output: 4

console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows"]
```

### reverse() 

将数组中元素的位置颠倒，并返回该数组的第一个元素会变成最后一个，数组的最后一个元素会变成一个。

```
const array1 = ['one', 'two', 'three'];

console.log('array1:', array1);
// expected output: "array1:" Array ["one", "two", "three"]

const reversed = array1.reverse();
console.log('reversed:', reversed);
// expected output: "reversed:" Array ["three", "two", "one"]
```

### shift() 

从数组中删除**第一个**元素，并返回该元素的值。

```
const array1 = [1, 2, 3];
const firstElement = array1.shift();

console.log(array1);
// expected output: Array [2, 3]

console.log(firstElement);
// expected output: 1
```

### sort()

用[原地算法](https://en.wikipedia.org/wiki/In-place_algorithm)对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的UTF-16代码单元值序列时构建的

(由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。)

```
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]

const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// expected output: Array [1, 100000, 21, 30, 4]

```

### splice()

可以通过删除或替换现有元素或原地添加新的元素来修改数组，并以数组形式返回被修改的内容。此方法会改变原数组。

```
const months = ['Jan', 'March', 'April', 'June'];

months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "May"]

```

### unshift()

将方法或一个元素多个添加到数组的**开头和结尾**，报道查看并该数组的**新长度（该**方法修改原有数组**）**。

```
const array1 = [1, 2, 3];

console.log(array1.unshift(4, 5));
// expected output: 5

console.log(array1);
// expected output: Array [4, 5, 1, 2, 3]
```

### concat()

这种方法可以合并两个或多个数组。此方法不会改变现有数组，可组合返回一个新数组。

```
const array1 = ['a', 'b', 'c'];
const array2 = ['d', 'e', 'f'];
const array3 = array1.concat(array2);

console.log(array3);
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```

### includes()

判断一个数组是否可能包含一个指定的值，根据情况，如果可以返回真实，否则返回虚假。

```
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true

const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
// expected output: true

console.log(pets.includes('at'));
// expected output: false
```

### join()

方法将一个数组（或一个[类数组对象](https://developer.mozilla.org/zh-CN_docs/Web/JavaScript/Guide/Indexed_collections#working_with_array-like_objects)）的所有元素连接一个字符串并返回这个字符串。

```
const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"

```

### slice()

返回一个新的数组对象，这个对象是一个由 `begin`和`end`决定的原数组的**浅拷贝**（包括`begin`，不包括`end`）。原始数组不会被改变。

```
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]

console.log(animals.slice(-2));
// expected output: Array ["duck", "elephant"]

console.log(animals.slice(2, -1));
// expected output: Array ["camel", "duck"]

```

### indexOf()

返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

```
const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

console.log(beasts.indexOf('bison'));
// expected output: 1

// start from index 2
console.log(beasts.indexOf('bison', 2));
// expected output: 4

console.log(beasts.indexOf('giraffe'));
// expected output: -1

```

### lastIndexOf()

方法返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个索引，如果不存在则返回 -1 `fromIndex`。

```
const animals = ['Dodo', 'Tiger', 'Penguin', 'Dodo'];

console.log(animals.lastIndexOf('Dodo'));
// expected output: 3

console.log(animals.lastIndexOf('Tiger'));
// expected output: 1

```

### filter()数组函数

创建一个新数组，其包含通过所提供的函数实现的测试的所有元素。 

```
let arr=[1,4,2,7,2]
arr. filter( function( item){return item %2 == 0})

//(3) [4, 2, 2]
```



```
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]

```

### map()循环数组每一个值

创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。

```
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

```
letarr=[1,4,2,7,2]

ar.map( (item)=>{ return item + 1})
//(5) [2,5,3,8,3]
```

```
letarr=[1,4,2,7,2]

arr .map( (item)=>{return`[${item}]`})

//(5) ["[1]", "[4]", "[2]", "[7]", "[2]"]

```

### 三元表达式

```
letarr=[1,4,2,7,2]

Let arr = [64, 58，40, 90, 60]

art .map((n)=>{ if(n<60) {return n+2}else{return n} })
//(5) [64, 60, 42, 90, 60]

```

```
arr .map((n)=>{return n<60?n+2:n})
//(5)[64 ,60,42 ,90 ,60]

```

```
let res=[]

//for(let n of arr){ if (n<60) {res. push(n+2)}else{res. push(n)}}
```

## Date时间

### Date()构造函数的四种基本形式、

#### 一、new Date()

这是我们最常使用也最熟悉不过的Date对象的构造方法了，通过无参数的构造函数我们可以默认获取到一个代表实例化时的Date对象

```
var now = new Date();
console.log(now) //Thu Sep 19 2019 16:13:08 GMT+0800 (中国标准时间)
```

#### 二、new Date(value)

　这个构造方法的参数是一个Number型，表示自1970年1月1日00:00:00 UTC（the Unix epoch）以来的毫秒数，忽略了闰秒。这个方法中可以用整型，也可以用浮点型，不过浮点型后面的小数点后的尾数一般会被忽略就是了。虽然在node环境（v10.15.3）下参数的确是从00:00:00时分开始计数，但是，通过实测发现在部分浏览器环境（在Edge，Chrome下如此）下参数是却从08:00:00开始计数，如下代码所示：

```
var time1 = new Date(1000);
var time2 = new Date(2000.2);
var time3 = new Date(2000.8);
console.log(time1); //Thu Jan 01 1970 08:00:01 GMT+0800 (中国标准时间)
console.log(time2); //Thu Jan 01 1970 08:00:02 GMT+0800 (中国标准时间)
console.log(time3.getMilliseconds()); //0

//node
var time4 = new Date(1000);
console.log(time4); //1970-01-01T00:00:00.001Z
```

>　　　　原因分析：node中是严格遵守UTC时间标准的，所以是严格的1970年1月1日00:00:00 UTC（the Unix epoch）；而在浏览器中一般是以本地时间为准，例如：在中国是以北京时间为基准的，而北京在东八区，所以会比标准的格林尼治时间要多8个小时，将电脑时区设置成太平洋时区后测试
>
>　　//改成太平洋时间后
>　　var time5 = new Date(1000);
>　　console.log(time5); //Wed Dec 31 1969 16:00:01 GMT-0800 (Pacific Standard Time)
>　　　　看到太平洋时间发现时间被“减了”，就会想到参数为负数的时候，是不是也会从这个基准时间开始减，如下：
>
>　　//北京时间下
>　　var time6 = new Date(-1000);
>　　console.log(time6); //Thu Jan 01 1970 07:59:59 GMT+0800 (China Standard Time)

#### 三、new Date(dateString)

　　这个构造函数应该是最有用和最会出现一些问题的了。参数dateString，顾名思义，是一个String型的格式化date字符串。该字符串应该能被Date.parse()方法正确识别，即符合IETF-compliant RFC 2822 timestamps或version of IOS8601。那这个构造函数到底能解析哪些格式化字符串？又不能解析哪些字符串呢？

> 该构造函数在不同浏览器以及不同node版本之间有差异，不推荐使用，同理也不推荐使用Date.parse，可以使用自己定义的工具函数把字符串转成date哦！

```
var time1 = new Date('2019/9/9');
var time2 = new Date('2019/09/09');
var time3 = new Date('2019-9-9');
var time4 = new Date('2019-09-09');
var time5 = new Date('2019 9 9');
var time6 = new Date('2019/9/9 12:20:05');
var time7 = new Date('2019-9-9 12:70:100');
var time8 = new Date('2019 9 9 14 0 1');
var time9 = new Date('2019/09/09 -12:20:13');
var time10 =new Date("February 3,2009 12:30:15");
console.log(time1); //Mon Sep 09 2019 00:00:00 GMT+0800 (中国标准时间)
console.log(time2); //Mon Sep 09 2019 00:00:00 GMT+0800 (中国标准时间)
console.log(time3); //Mon Sep 09 2019 00:00:00 GMT+0800 (中国标准时间)
console.log(time4); //Mon Sep 09 2019 08:00:00 GMT+0800 (中国标准时间)
console.log(time5); //Mon Sep 09 2019 00:00:00 GMT+0800 (中国标准时间)
console.log(time6); //Mon Sep 09 2019 12:20:05 GMT+0800 (中国标准时间)
console.log(time7); //Invalid Date
console.log(time8); //Invalid Date
console.log(time9); //Invalid Date
console.log(time10); Tue Feb 03 2009 12:30:15 GMT+0800 (中国标准时间)
一般情况下，建议使用yyyy/MM/dd hh:mm:ss格式，其他格式可能会出现意想不到的错误
```

#### 四、new Date(year,monthIndex[,day[,hours[,minutes[,seconds[,milliseconds]]]]]

　　这个构造通过多个函数，指定年月日时分秒来构造日期对象。此方法参数至少为两个，表示年月，可选参数5个，因为参数只有1个的话，是number型会使用第二种构造方法，是string型会使用第三种构造方法。此方法的参数类型可以是整数，浮点数（浮点会被转化为整型），或是字符串（字符串会被转化为Number型），也可以是正数、负数（但是，注意不能超过日期所能表示的最大范围 -100,000,000 天至 100,000,000 天）。当参数只有2个的时候，除了day默认为1，其余参数默认为0（此时不受时区的影响）。另外，参数2的月份需要加1，因为它对应的是0-11（同getMonth()和setMonth()）

```
var time1 = new Date(2019,2);
var time2 = new Date(2019.3,'5');
var time3 = new Date(2019,4,-3);
var time4 = new Date(2019,5,10,13,70,100,50);
console.log(time1); //Fri Mar 01 2019 00:00:00 GMT+0800 (中国标准时间)
console.log(time2); //Sat Jun 01 2019 00:00:00 GMT+0800 (中国标准时间)
console.log(time3); //Sat Apr 27 2019 00:00:00 GMT+0800 (中国标准时间)
console.log(time4); //Mon Jun 10 2019 14:11:40 GMT+0800 (中国标准时间)
```

> 同之前的原因，在node环境下，时间会出现偏移，在原有”标准时间“下要减去时区的时间差，例如，北京时间为东八区，在浏览器中基本保持与传参一致，但是在node环境下会”减去”这八小时的时间差，相反，西八区会加上这八小时的时间差。

### getDate()

已知本地时间，返回一个指定的日期对象为目的地的哪一天（从1--31）

```
const birthday = new Date('August 19, 1975 23:15:30');
const date1 = birthday.getDate();

console.log(date1);
// expected output: 19

```

### getDay()

方法根据当地时间，返回一个具体日期中一周的第几天，0 表示星期天。对于某个月中的第几天

```
const birthday = new Date('August 19, 1975 23:15:30');
const day1 = birthday.getDay();
// Sunday - Saturday : 0 - 6

console.log(day1);
// expected output: 2


```

### getFullYear()

根据当地时间返回指定日期的日期。

```
const moonLanding = new Date('July 20, 69 00:20:18');

console.log(moonLanding.getFullYear());
// expected output: 1969

```

### getHours()

根据当地时间，返回一个指定的日期对象的时间。

```
const birthday = new Date('March 13, 08 04:20');

console.log(birthday.getHours());
// expected output: 4
```

### getMinutes()

方法根据当地时间，返回一个指定的日期对象的分钟数。

```
const birthday = new Date('March 13, 08 04:20');

console.log(birthday.getMinutes());
// expected output: 20
```

### getMonth()

 可知本地时间，返回一个指定的日期对象的月份，为基于0的值（0表示一年中的第一个月）。

```
const moonLanding = new Date('July 20, 69 00:20:18');

console.log(moonLanding.getMonth()); // (January gives 0)
// expected output: 6

```

### getSeconds()

根据本地时间，返回一个指定的日期对象的秒数。

```
const moonLanding = new Date('July 20, 69 00:20:18');

console.log(moonLanding.getSeconds());
// expected output: 18
```

### getTime()

方法返回一个时间的格林威治时间数值。

你可以用这个方法把一个日期时间提交给另一个[`Date`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date) 对象[`valueOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/valueOf)。

```
const moonLanding = new Date('July 20, 69 20:17:40 GMT+00:00');

// milliseconds since Jan 1, 1970, 00:00:00.000 GMT
console.log(moonLanding.getTime());
// expected output: -14182940000

```

## Math数字

### Math.abs(x)

函数返回指定数字“x”的绝对值。

>一个非数字形式的字符串或者未定义/空变量，将返回`NaN`。 null 将返回 0。

```
Math.abs('-1');     // 1
Math.abs(-2);       // 2
Math.abs(null);     // 0
Math.abs("string"); // NaN
Math.abs();         // NaN
```

### Math.ceil()

函数返回大于或等于一个给定数字的最小次数。

>返回整数 0 并且不会给出错误。`Math.ceil(null)`[`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)

```
console.log(Math.ceil(.95));
// expected output: 1

console.log(Math.ceil(4));
// expected output: 4

console.log(Math.ceil(7.004));
// expected output: 8

console.log(Math.ceil(-7.004));
// expected output: -7
```

### Math.floor()

返回小于或等于一个给定数字的最大次数。

```
Math.floor( 45.95);
// 45
Math.floor( 45.05);
// 45
Math.floor( 4 );
// 4
Math.floor(-45.05);
// -46
Math.floor(-45.95);
// -46
```

### Math.fround()

可以将任意的数字转换为离它最近的[单精度浮点数](https://en.wikipedia.org/wiki/Single-precision_floating-point_format)形式的数字

数字1.可以在二进制数字系统中表示，32位和64位的值相同：

```
Math.fround(1.5); // 1.5
Math.fround(1.5) === 1.5; // true
```

但是，数字1.337却无法在二进制数字系统中表示，所以32位和64位的值是不同的：

```
Math.fround(1.337); // 1.3370000123977661
Math.fround(1.337) === 1.337; // false
```

### Math.max() 

函数返回了许多中的曲线。

```
console.log(Math.max(1, 3, 2));
// expected output: 3

console.log(Math.max(-1, -3, -2));
// expected output: -1

const array1 = [1, 3, 2];

console.log(Math.max(...array1));
// expected output: 3
```

### Math.min()

返回零个不同的数值。

```
var x = 10, y = -20;
var z = Math.min(x, y);
```

使用 `Math.min()` 裁剪值（限幅的值）

`Math.min` 经常用于某个值，可能会小于或等于某个值。

```
var x = f(foo);

if (x > boundary) {
    x = boundary;
}
```

```
var x = Math.min(f(foo), boundary);
```



### Math.pow()

函数返回基数（`base`）的指数（`exponent`）次幂

```
console.log(Math.pow(7, 3));
// expected output: 343

console.log(Math.pow(4, 0.5));
// expected output: 2

console.log(Math.pow(7, -2));
// expected output: 0.02040816326530612
//                  (1/49)

console.log(Math.pow(-7, 0.5));
// expected output: NaN


```

### Math.random()

函数返回一个浮点数，伪随机数在范围从**0到**小于**1**，从0（包括0）往上，但不1（排除1），然后您可以缩放到需要的范围。将初始初始选择到随机数生成算法；它不能被选择或发生。

```
function getRandomInt(max) {
  return Math.floor(Math.random() * max);
}

console.log(getRandomInt(3));
// expected output: 0, 1 or 2

console.log(getRandomInt(1));
// expected output: 0

console.log(Math.random());
// expected output: a number from 0 to <1
```



# JS 高阶

## 从新认识js

JavaScript到底是什么?

>  JavaScript的核心语言叫ECMAScript ,是一种完备的动态编程语言(弱类型),是一种具有函数优先的解释型语言(即时编译),是一种基于原型、多范式的编程语言

js能做什么？

> Browser							浏览器
> NodeJs Chrome V8)		操作数据库，后端编程
> MongoDB						使用js操作数据库
> React Native (JavaScriptCore)	构建安卓ios   app

ECMAScript主要标准有哪些?

>ECMAScript 2009 (ES 5)				主要是es5，6
>ECMAScript 2015(ES 6)
>ECMAScript 2016 (ES 7)
>ECMAScript 2017 (ES 8)
>ECMAScript 2018 (ES 9)
>ECMAScript 2019 (ES 10)

### 如何学习JavaScript?

> 语法与数据类型
> 函数
> 控制流与错误处理
> 循环与迭代
> 表达式和运算符
> 字符串、数字和日期
> 对象与集合
> Promises

### var,let,const

>var	可以作用于花括号下面，不仅仅是同一个花括号。可以重复声明
>
>let	作用域小一些，只作用于同一花括号以内。不可以重复声明
>
>const	常量不可以修改值。不可以重复声明

```javascript
if (true){
vara=1;
letb=2;
}
console.log(a);			// 1
console.1og(b) ;		//b is not def ined
const PI = 3.14;
const PI = 3.14; 		// Identifier ' PI' has already been dec lared
PI = 3.14159 ;			// Ass ignment to constant variable.
```

## 8种数据类型

- Boolean	：布尔值。有2个值分别是：`true` 和 `false`.
- null            ：一个表明 null 值的特殊关键字。 `null` 与 `Null`、`NULL`或变体完全不同。
- undefined ：和 null 一样是一个特殊的关键字。undefined 表示变量未赋值时的属性。
- Number     ：数字。整数或浮点数，例如： `42` 或者 `3.14159`。
- BigInt         ：任意精度的整数 。可以安全地存储和操作大整数，可以超过数字的安全整数限制。
- String         ：字符串，字符串是一串表示文本值的字符序列，例如："Howdy" 。
- Symbol      ：代表 ( 在 ECMAScript 6 中新添加的类型).。一种实例是唯一且不可改变的数据类型。
- Object        ：对象。

## 对象中的属性和方法

>   当一个函数是一个对象的属性时，称之为**方法**

user:对向，name属性，jack值

声明属性的时候需要在后面加逗号

#### 对象里的方法

属性名 ：function(){}

```javascript
let user = {
    name :'Jack'，
}
console . log (user.name)

let value ='Jack'
let user =	{
    name: value,
}
    console.log (user.name)
```

```
let name =' Jack
let user = {
	name: name，		//后面的name是属性的值
}
console.log(user.name)
```

定义同名属性（缩写）

```
let name ='Jack'
let user = {
	name
}
console.log (user.name)
```

> 将name这个变量名当作属性，变量的值就是属性的值

[ ]寻找一个变量名对应的属性值

```
let key='name‘
let value = 'Jack’
let user = {
	[key]: value,
}
console . log (user . name)
```

## this关键字

> 方法的调用				在对像上面点一个具体的方法（）
>
> 普通函数的调用		直接写函数名字（）

this指代的是对象本身，必须在对象的方法里面，

```javascript
function say() {
    console.log('Hello World')
    let user ={
    name :'Jack'
    say: function() {
        console.log(`Hi,I'm ${this . name}~`)
    },
    hi: function() {
        say()
        this.say()
    }
}
console.log(user.say())
console.log(user.hi())
```

### 属性和方法缩写

```javascript
let name =‘Jack'
let user = {
	name，
	say( ){
	return	`Hi, I'm ${this.name}`
	}
}
console.log(user.name)
console.1og(user.say())
```

## 类和对象

### 游戏玩家类

<img src="https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142782.png" alt="image-20211013145646650" style="zoom:50%;" />例

class + 类名 + {}

> 类的属性和值中间是等于号，不用写逗号
>
> 对象的属性和值中间是冒号，需要写逗号



类是模板	实例化对象时通过类的模板来	new	一个对象

新建的对象是class具体的对象



this会随着对象的变化而变化

```javascript
class Player{
    name = null			//类中的属性默认值用等号，后面不加分号
	level = 1
    combat(){
        console. log(`${this .name}获胜了，等级++` )	//需要在变量前面加$符号
        this.level++ 
	}
}
user1 = new Player()
user1.name = "Jack"
console.log (user1)
user1. combat()
console.log (user1)
user2 = new Player()
console.log(user2)
```

## 构造方法

### constructor()

在实例化对象的时候被自动调用

```javascript
class Player{
    name=null
	level = 1
	constructor(name,level = 1){
        this.name = name
        this.level = level
	}
	combat(){
        console.log(`{this.name}获胜了，等级++` )
        this. leve 1++
	}
}
user1 =
    new Player(”Jack")
                console . log (user1 )
user2 =
    new Player("mary") 
               console. log (user2 )
```

## 继承：	子类继承父类

子类有父类所有属性和方法，可以有新属性，新方法

class   扩展名	extends	类名	{	属性	}

定义一个对象 	=	new	扩展名

```
class VipPlayer extends Player{
	isVip = true 
	combat(){
		this.level += 2			//vip战斗胜利等级加2
	}
	constructor(name,level=20){
	 	super(name,level)
	}
}
let user3 = new VipPlayer("tom",20)
user3.combat			//level +2
```

> 子类调用父类的构造方法时应该加上super关键字

## 箭头函数

### function	函数

```
setTimeout( function(){console. log(11)}，1000)	  //1秒后打印11
function test(){
	console.log("test")
}

setTime(test,1000)
	
setTime("test()",1000)
```

>     传一个函数不能加（），传一个字符串的函数需要用（）

### 普通函数



```
var foo =function(){
	console.log("foo...")
}

// foo...

function foo (){}

```

###  箭头函数

 箭头函数不是普通函数的缩写

```
var bar=()=>{
	console.log("bar.....")
}
```

```
setTimeout(()=>{console.log("bar")},2000)
```

```
function run(){}
setrimeout (run ,1000 )
setT imeout("run( )"，1000)
setrimeout (function( ){}，1000)

setrimeout(()=>{console.1og(1)})	 //括号里面加参数
setTimeout(_=>{console.1og(1)})		//没有参数，用下划线占位
setTimeout(_=>console.1og(1))		//只有一句可以省略花括号
```

## globalThis

>   顶层对象，提供全局环境(即全局作用域

●浏览器里面，顶层对象叫window 
●浏览器全局环境中，

window.alert('aaa')==this.alert('aaa')

●this会返回顶层对象
●普通函数里this指向顶层对象(严格模式undefined)

"use strict"	//启用严格模式

●函数作为方法运行，返回该对象自身
●Node.js里面，顶层对象叫global
●Node(ES6)模块中，this返回的是当前模块

```javascript
console. log(this)			//window
function test() {
	console .log(this 
}
test()						//window

function test2( ) {
	"use strict" ;			//开启严格模式
	console. log(this )		//undefined
}
test2( )

user = {
	name:"jack" ，
	say:function(){
		console log ( this name )
	}，
	test
}
user.say( )				//jack
user.test( )				//user对象

```

### This陷阱

```javascript
class Player{
    level = 1
	hp = 100
rest(){
    let timer = setInterval( function( ){
        if(this.hp < 100){
            console. log("hp++" )
            this . hp++
        }else{
            C lear Interval( timer )
        }
    }，1000)
    combat( ){
        console.log(获胜了， 等级++，血量减少、)
        this.hp = this.hp-20
        this. level++
        user1 = new Player( )
        user1. combat( ); user1.rest(); console . log (user1)
```

### 避免this陷阱

```javascript
class Player {
    level = 1
	hp=100
    rest(){
        let _this=this
        this = this
        let timer = setInterval( function() {
            if(_this.hp < 100) {
                this. hp++
            }else{
                clearInterval (timer)
            }
        }, 1000)
        combat( ) {
            console.log(获胜了，等级++,血量减少~ )
            this.hp = this.hp一20
            this . level++ 
        }
        
    }
    user1 = new Player( )
    user1. combat( ); user1.rest( ); console. log (user1 )

```

### 箭头函数解决this陷阱

​	箭头函数不会干扰this

```javascript
class Player{
    level = 1
	hp = 100
	rest(){
    	let timer = setInterval(() => {
            if(this.hp < 100) {
                this.hp++
            }else{
                clear Interval ( timer )
            },1000 )
        }
        combat(){
            console.log(`获胜了，等级++,血量减少` )
            this.hp = this.hp-20
          	this.level++
        }
}
user1 = new Player( )
user1. combat( )
user1.rest();		 console.log (user1)
```

## 对象是引用的

>   改变原版对象，第二个指向名也会改变

```javascript
var user1 = {name:"jack"}	
var user2 = {}				
user2.name = user1.name
"jack'
```

每new一个都是不同的对象

### {...object}语法

把一组对象的值单独赋给新的对象，2个对象无联系

```
var user2 = {... user1}
//undefined
user2
// {name: "jack"}
```

### 对象的扩展运算

三个没有引用关系

```
var user1 = {name:"jack"}
//undef ined
var user2 = {...user1, age:18}
//undefined
user2
//{name: "jack", age: 18}
var user3 = {.. .user2}
//undefined
user3
//{name: "jack", age: 18}
```

## 解构语法

```
age = 18
//18
user1 = {age}
//{age: 18}
name = "lily"
//"lily"
user1 = {name, age}
//{name: "lily", age:18}
```

### 对象的解构

```
var obj={name:"jack",age=18}
var	{name,age}=obj
name
//"jack"
age
//18
```

### 数组的解构

```
var[a,b]=[100,300]
a
//100
b
//100
```

# jquery 安装使用

到https://jquery.com/官网下载jquery.js文件，创建文件夹，把js文件放入新的文件夹里面

>   可以简化js的一些代码

使用scr="文件名"在script标签里面调用代码

### 1.选择器

```javascript
let box1=document.getElementById("box1")
	console.log(box1)
let arr=document.getElementsByClassName("box")
	console.log(arr[0])
	
	
//现在的方法
let box1 =jQuery("#box1")		//提供函数
    console.log(box1)       	 //id寻找
let box1 =jQuery(".box1")		//class寻找
    console.log(box1)
    
    

let box1=$(".box")  				//$取代jquery
	console.log(box1)

let res=$("div span:first-child")  	//$取代jquery
	console.log(box1)    

let box1=$("#box1")					//jquery寻找的是一个集合,不止一个数值，是多个并列的
	box1[0].innerHTML=$("#box1") 	//就算是只有一个，也要当作数组来使用

let res=$("div span:first-child")  //$取代jquery
	console.log(res.length)
for(let i=0;i<res.length;i++){
    res[i].style.color="blue"
}
```

### 2.属性选择

```javascript
$("#box1")[0].setAttribute("title","test")         //attr语法添加标签
$("#box1").attr("title","test") 
//> attr是一个集合体,会改变所有的集合下元素


let res=$("div span")                         //循环给一组标签添加元素
console.log(res)
for(let i=0;i<res.length;i++){
    res[i].setAttribute("title","test")
}
											//简化
$("div span").attr("title","test")          //给一组标签标签添加元素


$(".logo")[0].setAttribute("src","https//www.baidu.com")    //改图片地址
$(".logo").attr("src","https//www.baidu.com")        

$(".logo")[0].style.border="2px solid red"
$(".logo").css("border","2px solid red")        //简写style属性


$(".logo").addClass("demo")         		//追加类名

$(".logo").removeClass("demo")        		 //删除类名

$("#box1")[0].innerHTML="hello"        		 //标签内容赋值
$("#box1").html("hello")               		 //简写模式
$("#box1").html("")                    		 //清空内容
```

### 3.事件

```javascript
$("#box1")[0].onclick=function(e){          //点击事件
    console.log(e.target)
}

${"#box1"}.click(function(){                   //简化
    console.log("被点击")
})


${document}.on("click","#box1",function(){     //简化
    console.log("被点击")
})
```

### 4.文档

```javascript
let h1=document.createElement("h1")
h1.innerHTML="world"
$("#box1")[0].appendChild(h1)

let h1 = $("<h1>world</h1>")
$("box1").append(h1)
```



### 5.前端基础综合练习(ajax)

美工:设计效果图

前端:HTML+CSS +JavaScript

后端:数据库 + 接口
BS架构:浏览器 + 服务器
数据的传输:协议HTTP HTTP协议是无状态的,是指协议对于交互性场景没有记忆能力 请求的方法有GET、POST
GET把参数包含在URL中，POST通过request body传递参数
数据格式:JSON js Object Notation, js对象简谱 是一种轻量级的数据交换格式
AJXA 请求服务端的数据
无状态:token 浏览器带着数据如用户名、密码请求服务端,例如登录,服务端在数据库里查找有没有相应的用户名及密码,完成登录后, 客户端生成并返回一个长的字符串(token)给浏览器,浏览器再次访问时可以直接凭借token访问客户端

### JSON

json与js对象的关系以及如何转换
JSON是JS对象的字符串表示法,它使用文本表示一个JS对象的信息,本质是一个字符串

```
var obj = {a: 'Hello',b:'World'};  //这是一个对象,注意键名也是可以使用引导号包裹的
var json = '{"a":"Hello","b":"World"}' //这是一个json字符串,本质时一个字符串可以使用


JSON.parse()方法将JSON字符串转换为JS对象
var obj = JSON.parse('{"a":"Hello","b":"World"}') //{a: 'Hello',b:'World'}可以使用


JSON.stringify()方法将JS对象转换为JSON字符串
var json = JSON.stringify({a: 'Hello',b:'World'})  // '{"a":"Hello","b":"World"}'AJAX
```



```
                //jQuery.post( url [, data ] [, success ] [, dataType ] )
                //post请求
```

#### 首页

```
//获取windows的本地缓存
                var token = window.localStorage.getItem("token")
                //调试token是否存在
                console.log(token);
                if (token !== null) {

                    //对象data加属性
                    var data = {
                        //data.token存入token
                        "token": token
                    }
                    $.get("http://playground.it266.com/profile", data, function (result) {
                        if (result.status) {
                            //console.log(result.status);
                            //隐藏和展示登录

                            $(".login").show()
                            $(".nologin").hide()
                            //更改属性
                            //头像更改
                            $("#avatar").attr("src", result.data.avatar)
                            $("#username").html(result.data.username)
                            $("#balance").html(result.data.balance)
                            $("#point").html(result.data.point)
                        }
                    }, 'json')
```

#### 注册

```
        $(function () {
            $("#submit").click(function () {
                
                var data = {
                    username: $("#username").val(),
                    password: $("#password").val(),
                    password2: $("#password2").val(),
                   
            
                }
                console.log($("#password2").val());
                if( $("#password").val()!=$("#password2").val()){
                    $(".message").html("两次密码不一致，请重新输入")
                    console.log(password    );
                    console.log(password2);
                        return false
                    }
                
                $.post("http://playground.it266.com/register", data, function (result) {
                    if(!result.status){
                        console.log(result.status);
                        $(".message").html(result.data)
                    }else{
                        alert("注册成功，请登录")
                        window.location="login.html"
                    }
                }, 'json')
                //jQuery.post( url [, data ] [, success ] [, dataType ] )
                //post请求

                return false
            })
        }

        )
```

#### 登录

```
        $(function () {
            $("#submit").click(function () {
                var data = {
                    username: $("#username").val(),
                    password: $("#password").val(),
                }
                // console.log(data);
                $.post("http://playground.it266.com/login", data, function (result) {
                    //判断登录状态
                    if (!result.status) {
                        console.log(result.data)
                        $(".message").html(result.data)
                    } else {
                        console.log(result.data.token)
                        //windows存入token
                        window.localStorage.setItem("token", result.data.token)
                        //跳转到首页
                        alert("登录成功")
                        window.location = "index.html"
                    }
                }, 'json')
                //jQuery.post( url [, data ] [, success ] [, dataType ] )
                //post请求

                return false
            })
        }

        )
```



