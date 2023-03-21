​	



# 使用React构建用户界面

rcc 自动补全类组件模板

rfc 自动补全无状态组件模板

## 1.JSX

React 是一个Facebook 开源的，用于构建用户界面的 JavaScript 库。官网为 https://reactjs.org/

在使用React时，需要引入相关的js文件如下：

```
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
```

然后在页面中，放入一个id叫root的div，作为我们项目的**顶级容器**

```
<div id="root"></div>
```

React推荐使用一种叫做JSX的语法，允许我们在JavaScript中嵌入HTML标签，例如我们可以把一个`<h1>`标签，赋值给一个js的变量：

```
let el = <h1>Hello React!</h1>
```

然后，使用React提供的一个叫做`ReactDOM`的对象，将 `el` 变量中的内容，渲染到`id`叫`root`的`div`容器中，完整代码如下：

```
<div id="root"></div>

<script type="text/babel">

  let el = <h1>Hello react!</h1>

  let root = document.getElementById('root');
  ReactDOM.render(el, root);

</script>
```

代码运行后，页面上将显示 `Hello React!`，等价于下面的HTML代码：

```
<div id="root">
    <h1>Hello React!</h1>
</div>
```

由于我们使用了 JSX语法，就不再是标准的JavaScript了，所以 `<script>`标签中的`type`属性，需要设置为`text/babel`。(注：Babel 是一个 JavaScript 编译器，可以解析JSX语法)

```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>Hello React</title>
<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>
<div id="root"></div>
<script type="text/babel">

  let el = <h1>Hello React!</h1>

  let root = document.getElementById('root');
  ReactDOM.render(el, root);

</script>
</body>
</html>

//输出结果Hello React!
```



## 2.组件化思想训练

浏览器提供了很多的**标签**给我们使用，例如 `<h1>、<img>、<input>`等等，那么，我们能自己创建标签吗？

在React中，我们把JSX代码放在一个函数中，就可以把函数名，当成标签来使用，看这这段代码：

```
function Demo(){
    return <div>Hello Demo!</div>
}
```

有了Demo函数，就相当于有了一个叫做Demo的标签 `<Demo>`，我们接下来，把这个Demo标签渲染到root节点上去

```
// let el = <h1>Hello React!</h1>
let el = <Demo></Demo>
```

我们将这样的函数，叫做**组件(Component)**，我们可以自由组合浏览器中提供的各种标签，来构建复杂的组件，例如下面这个搜索区域，我们就可以封装为一个叫做**Search**的组件，方便我们使用

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181152008.png!l)

```
function Search(){
   return (
        <div>
            <select>
                <option>网页</option>
                <option>图片</option>
            </select>
            <input type="text" />
            <button>搜索</button>
        </div>
   )
}

let el = <Search></Search>

let root = document.getElementById('root');
ReactDOM.render(el, root);
```

注意，**单标签**也需要**闭合**，例如`<input type="text" />`中的那条斜线不能省略。快去实验一下吧

当我们把页面上的功能块，都抽象为一个个的组件之后，我们的代码逻辑会更清晰。如果其它页面需要使用到相同的内容，也可以直接使用我们封装好的组件。下面，我们再来封装一个组件，`Nav`导航组件

```
function Nav(){
    return (
        <ul className="nav">
            <li><a>新闻</a></li>
            <li><a>视频</a></li>
            <li><a>图片</a></li>
        </ul>
    )
}
```

为了给这个组件写css样式，我在ul上给了一个类名，叫做**nav**。注意是**className=“nav”**，而不是**class=“nav”**，因为我们现在使用的是JSX语法，JSX是嵌入在JavaScript中的，class是JavaScript中的关键字，给标签添加类名时，就需要避开class这个关键字，而使用className。对应css如下：

```
<style>
    .nav{list-style: none; background-color: #1479d7; overflow: auto;}
    .nav li{float: left; margin: 10px;}
    .nav a{color: #fff; text-decoration: none;}
</style>
```

最后，将写好的Search和Nav组件，一起渲染到root节点中去：

```
let el = (
    <div>
        <Search></Search>
        <Nav></Nav>
    </div>
)

let root = document.getElementById('root');
ReactDOM.render(el, root);
```

需要注意的是，JSX中只支持一个根节点。这里我们有两个组件需要显示，就需要多加一个div容器，把`Nav`和`Search`组件装在一起来，最终得到如下的效果：

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181152009.png!l)

## 3.在Node环境中使用React

**npx nrm use taobao**  **切换淘宝镜像源**

**npx create-reate-app demo**

**创建成功后使用dir查看文件  再cd进入demo文件  使用npm start**



引入本地图片不能在src中直接写存储路径  否则会报错

**方法一 : 通过!important引入（推荐）**

```
import headset from "./imgs/耳机.png";

<img src={headset} alt="耳机" />
```

**方式二：require方法引入**

**require**中只能写字符串，不能写变量

在js中这样引入时,webpack只会把当前的src当作字符串,并不会当作资源文件去处理,这样当你的代码一旦打包到线上以后就会出现图片文件路径到不到的问题

```
<img src={require( "./imgs/耳机.png")} alt="耳机" />
```



在demo/src目录下创建index.js和index.css文件

**src中一定要有一个index.js文件**

代码运行时会和demo/public目录下的index.html一同运行

```
// let el = document.createElement("h1")
// el.innerHTML = "Hello React"
// document.getElementById("root").appendChild(el)

// $("#root").html("<h1 class='title'>Hello React</h1>")

//上下两种做法等价 但是上面的比较麻烦

import React from "react";
import { render } from "react-dom";
import "./index.css"; //导入css

//props 属性(例如class)  下面的{}就是props

// let el = React.createElement(
//     "h1",
//     {className:"title"},
//     "Hello React")

//JSX    更加简洁的表示  可以将代码转换为上面的代码 本质上是语法糖

//语法糖（Syntactic sugar），也译为糖衣语法，
// 指计算机语言中添加的某种语法，这种语法对语言的功能并没有影响，但是更方便程序员使用。
// 通常来说使用语法糖能够增加程序的可读性，从而减少程序代码出错的机会。

// let el = <h1 className="title"> Hello World!</h1>;

//el内容较复杂时,里面只能有一个根结点元素 即用一个div将其他标签包起来
let el = (
    <div>
        <h1 className="title"> Hello World!</h1>
        <div>abcdefg</div>
    </div>
    
);
//render 与 appendChild作用类似
render(el, document.getElementById("root"));
```

### 自定义组件

**以下操作均在demo/src下完成**

**组件写在index.js中** 

```
import React from "react";
import { render } from "react-dom";
import "./index.css"; //导入css

//JSX
//自定义组件

function Product(props) {
  console.log(props);
  return (
    <div>
      <div>{props.name}</div>
      <div>单价:{props.price}</div>
    </div>
  );
}
let product1 = {
  name: "商品一",
  price: "1988",
};

//商品一商品二通常来自数据库中的数据 不是像这样写死的
let el = (
  <div>
    <h1 className="title"> Hello World!</h1>
    <img
      alt="百度logo"
      src="https://www.baidu.com/img/PCtm_d9c8750bed0b3c7d089fa7d55720d6cf.png"
    />
    <Product name={product1.name} price={product1.price}></Product>
    <Product {...product1}></Product>
    <Product name="商品二" price="1688"></Product>
  </div>
);
render(el, document.getElementById("root"));
```

**当业务复杂时需要将组件放其他地方**

**index.js**

```
import React from "react";
import { render } from "react-dom";
import "./index.css"; //导入css
import Product  from "./product"

//JSX
//自定义组件

let product1 = {
  name: "商品一",
  price: "1988",
};

//商品一商品二通常来自数据库中的数据 不是向这样写死的
let el = (
  <div>
    <h1 className="title"> Hello World!</h1>
    {/*<Product {...product1}></Product>*/}
    <Product name={product1.name} price={product1.price}></Product> 
  </div>
);
render(el, document.getElementById("root"));

```

**product.js**

```
import React from "react";
import "./product.css"

function Product(props) {
    console.log(props);

    return (
      <div>
        <div className="procuct-name">{props.name}</div>
        <div>单价:{props.price}</div>
      </div>
    );
}

  //组件需要导出 否则会出现下面的报错
  //Attempted import error: './product' does not contain a default export (imported as 'Product').        oduct').
  export default Product;
```

**#product.css**

```
.procuct-name{
    background-color: #ccc;
}
```



## 4.React中的动态加载列表数据

```
import React from "react";
import { render } from "react-dom";

//自定义组件
import Article from "./components/article/index";
import Clock from "./components/clock/index";

let articles = [
  { id: "1", title: "援鄂专家口述: 如何让爆满重压中的定点医院上轨道" },
  { id: "2", title: "文章二" },
];

//map循环articles中的元素
// articles.map((item)=>{  //item就是articles[i]
//   console.log(item.title)
// })

let App = (
  <div>
    
    {/* 文章列表 */}
    {articles.map((item) => {
      return  <Article key={item.id} {...item}></Article>;
    })}
    
    {/* <Article {...articles[0]}></Article>
    <Article {...articles[1]}></Article> */}

	{/* 显示时间 */}
    <Clock></Clock>

  </div>
);

render(App, document.getElementById("root"));
import React, { Component } from "react";
import { render } from "react-dom";

//函数组件 没有属性  没有生命周期  调用就调用了  没有办法挂载与取消挂载

//类组件才有

class Clock extends Component {
  
  //组件的状态  state是固定写法
  state = {
    now: new Date(),
    count:0,
  };

  //组件被显示出来时,会自动执行  挂载
  componentDidMount() {
    console.log("componentDidMount");

    setInterval(()=>{
        this.setState({count:++this.state.count})
    },1000)

    this.timer = setInterval(() => {
      //   this.now = new Date();
      this.setState({ now: new Date() });  //setState是由react特殊处理的一个特殊的方法,它会去改变state的值,并在页面上动态显示出来. 
    }, 1000);
  }
  
  //组件被卸载时自动执行(跳转页面)  取消挂载
  componentWillUnmount() {
    console.log("componentWillUnmount");

    clearInterval(this.timer);
  }

  //react会自动调用组件的render方法

  render() {
    return (<div>
        count:{this.state.count}
        {this.state.now.toLocaleString()}
            </div>);
  }
}

export default Clock;

```

### axios动态生成文章内容

### ajax get请求

```
import React, { Component } from "react";
import axios from "axios";

//axios使用示例
// axios
//   .get("http://playground.it266.com/news")
//   .then((response) => {
//     //记得要使⽤箭头函数
//     console.log(response); //服务器响应的数据
//   })
//   .catch((error) => {
//     console.log(error);
//   });

class Article extends Component {
  state = {
    articles: [], //默认⽂章列表为空数组
  };
  componentDidMount() {
    axios
      .get("http://playground.it266.com/news")
      
      .then((response) => {
        // console.log(response);
        // console.log(response.data.articles[0].title)
        this.setState({
          articles: [...response.data.articles],
        });
        console.log([...response.data.articles])
        console.log(this.state.articles);
      })

      .catch((error) => {
        console.log(error);
      });
    // 在这⾥去做ajax请求，分析返回的数据，将⽂章列表数组找到
    // ajax获取到数据后，将服务器返回的⽂章数组，存放到状态中
    // 记得要使⽤ this.setState({articles: ⽂章列表数组})
  }

  render() {
    return (
      <div>
        {this.state.articles.map((item) => {
          return (
            <div key={item.id}>
             { item.title}
             </div>
          );
        })}
      </div>
    );
    // return <div>{/* 在这⾥，循环this.state.articles，输出⽂章列表 */}</div>;
  }
}

export default Article;

```

### ajax post请求

```
import axios from  "axios"
import qs from "qs"

axios({
    method: "post",
    url: 'http://playground.it266.com/register',
    headers: {'Content-Type': 'application/x-www-form-urlencoded'},
    data: qs.stringify({'username': this.state.username, 'password': this.state.password}),
}).then((response) => {
    console.log(response.data)
}).catch((error) => {
    alert("出错了")
})
```



## 5.React事件与表单

### 普通组件 添加事件

可以直接在标签里写函数

也可以将函数写在外面,再在标签里让onClick={函数名}

```
let App = (
    <div>
        <div onClick={()=>{  //js一样 区别在于onclick与onClick  
            alert(123456)
        }}>点击</div>
    </div>
)

//也可以用以下三种方式表示
let handleClick=()=>{
     alert(123456)
}

//let handleClick= function(){
    // alert(123456)
//}

//function handleClick(){
    // alert(123456)
//}

let App = (
    <div>           //handleClick后面不能加()  否则页面直接执行函数内容 跳出弹框"123456"
        <div onClick={handleClick}>点击</div>  
    </div>
)

//上面的情况当需要在函数里面传参时就没办法实现
//就可以在函数的外面套一个函数

function handleClick(num){
     alert(123456)
}

let App = (
    <div>    
        <div onClick={()=>{  //只有发生点击事件时才会执行里面的内容
            handleClick(1)
        }}>点击我!</div>
    </div>
)
```

### event事件

```
//在页面点哪个 控制台上打印哪个的innerHTML
function handleClick(e){
     console.log(e.target.innerHTML)
}

let App = (
    <div>    
        <div onClick={handleClick}>11</div>    
        <div onClick={handleClick}>22</div>

        //<input onClick={handleClick} value="11"></input>  上面应改为e.target.value
    </div>
)
```

### 动态选择导航中的任一项

```
import React,{Component} from 'react'

class Nav extend Component {
    state={
       activeIndex: 0, //当前被选中的项
    }
    
    handleClick(index){
       //console.log(12364)
        this.setState({activeIndex:index})  
    }
    
    render(){
        
        //let activeIndex = 4
        
        let categoryList=['首页','推荐','限免','金融','公司','宏观']  //index[0,5]
        let navDate=categoryList.map((item,index)=>{   //map函数的第二个参数  index索引
            return <li
                key={index}  //需要一个unique的key  否则会报错
                
                //下面就是逻辑运算的短路问题(前面条件成立才有后面) 
                //会产生一个boolean表达式的警告  此处不能使用
                //className={this.state.activeIndex===index && "active"}
            
                //应使用三元表达式
                className={this.state.activeIndex===index ? "active":""}
                
                //添加点击事件
                onClick={()=>{
                    this.handleClick(index)
                }}
            >{item}</li>
        })                       
        
        return(
        <div className="Nav">
            <ul>
                {navDate}
                //被选中的有选中效果
                //<li className="active"></li>
                //<li></li>
            </ul>
        </div>
    }   
}

export default Nav;
```

**点击事件的其他内容需要去查看官方文档**

### 表单写法

表单的作用是收集用户的信息

事件以及input表单取值的方法

出现undefined情况时 很可能是因为this作用域问题导致的  可以用箭头函数解决

```
import React, {Component} from 'react';

class Search extends React.Component{
    
    state{
        content:"React"      
    }

    componentDidMount(){
        //setTimeout(()=>{
            //this.setState({content:"javaScript"})
        //},3000)
    }
    
    //改变输入框内的值  注意this作用域问题  会出现can't read property 'setState' of undefined   可以使用箭头函数规避
    handleInput=(e)=>{
        console.log(e.target.value)
        this.setState({content:e.target.value})
    }

    render(){
        return(
            <div className={"Search"}>
            
            //react为单向数据流  数据由state里传出 并改变页面上的值
            <input value={this.state.content}
                className="keyword" 
                type="text" 
                pelachholder="请输入搜索内容"
                onChange={this.handleInput}
                onKeyPress={(e)=>{
                   console.log(e.charCode)
                    //如果用户按下的是回车键
                    if(e.charCode===13){
                        console.log("用户想要搜索的东西:"+this.state.content)
                        //ajax  实际需要通过ajax去数据库中搜索
                    }
                }}
            />
            <span className="icon"></span>
        );
    }  
}

export default Search;
```

### 注册页面

### ajax post请求

```
import axios from  "axios"
import qs from "qs"

axios({
    method: "post",
    url: 'http://playground.it266.com/register',
    headers: {'Content-Type': 'application/x-www-form-urlencoded'},
    data: qs.stringify({'username': this.state.username, 'password': this.state.password}),
}).then((response) => {
    console.log(response.data)
}).catch((error) => {
    alert("出错了")
})
```



## 6.注册功能讲解



## 7.React文章管理

通过登录得到一个token值,并将token储存在本地

带着token值访问接口

```
//存储token
window.localStorage.setItem("token", response.data.data.token)

//获取token
var token = window.localStorage.getItem("token")
```



**Link标签**

```
//在路由中使用Link标签  类似于a标签
import {Link} from "react-router-dom";

<Link to="/article"> </Link>
```

**跳转页面**   固定用法

```
this.props.history.push("路径")
```

### 路由管理

通常做项目时需要很多个页面,需要在多个页面中跳转和切换

这时候就需要用到路由

需要先安装

//npm install react-router-dom –save

没有exact时,会进入最开始的页面  

例如 ./ 和./article  会直接进入./页面

```
import {HashRouter,Switch,Route} from "react-router-dom";
<HashRouter>
    <Switch> //exact精确匹配
        <Route exact path="/" component={Home}></Route>   
        <Route  path="/article" component={Article}></Route>
    </Switch>
</HashRouter>
```

**src/app.js**

```
import React from "react";
import Loginpage from "./pages/login";
import Home from "./pages/home";
import Article from "./pages/article";

//npm install react-router-dom --save
import { HashRouter, Switch, Route } from "react-router-dom";

class App extends React.Component {
  render() {
    return (
      <HashRouter>
        <Switch>
          <Route exact path="/" component={Loginpage}></Route>
          <Route path="/home" component={Home}></Route>
          <Route path="/article" component={Article}></Route>
        </Switch>
      </HashRouter>
    );
  }
}
export default App;
```

**src/articles/index.js**

```
import React, { Component } from "react";
import { Switch, Route } from "react-router-dom";
import Index from "./components/index";
import Create from "./components/create";
import Edit from "./components/edit";
import Detail from "./components/detail";


class Article extends Component {
  render() {
    return (
      <Switch>
        <Route exact path="/article" component={Index}></Route>
        <Route path="/article/create" component={Create}></Route>
        <Route path="/article/edit/:id" component={Edit}></Route>
        <Route path="/article/detail/:id" component={Detail}></Route>
      </Switch>
    );
  }
}
export default Article;
```

### **axios post请求**

```
import axios from  "axios"
import qs from "qs"

state = {
    title: "",
    content: "",
  }; 

axios({
      method: "post",
      url: `http://playground.it266.com/article/create?token=${token}`,
      headers: { "Content-Type": "application/x-www-form-urlencoded" },
      data: qs.stringify({
        title: this.state.title,
        content: this.state.content,
      }),
    })
      .then((response) => {
        console.log(response);
        if (response.data.status) {
          this.props.history.push("/article");
        } else {
          alert(response.data.data);
          }
        }
      )
      .catch((error) => {
        alert("出错了");
      });
```

### 路由/:id  get请求

```
// this.props.match.params.id 固定用法 获取id  需要在路由处url的最后加上/:id

axios
      .get(`http://playground.it266.com/article/detail?token=${token}`, {
        params: {
          id: this.props.match.params.id,
        },
      })
      .then((response) => {
        console.log(response);
        this.setState({
          title: response.data.article.title,
          content: response.data.article.content,
        });
      })
      .catch((error) => {
        console.log(error);
      })
      .then(function () {});
```

## 8.React中的分页和搜索



/src/app.js

```
import Article from "./pages/article";
import Pegsearch from "./pages/Paging and searching";

//npm install react-router-dom --save
import { HashRouter, Switch, Route } from "react-router-dom";

class App extends React.Component {
  render() {
    return (
      <HashRouter>
        <Switch>
          <Route exact path="/" component={Loginpage}></Route>
          <Route path="/home" component={Home}></Route>
          <Route path="/article" component={Article}></Route>
          <Route path="/PagingAndSearch" component={Pegsearch}></Route>
        </Switch>
      </HashRouter>
    );
  }
}
export default App;

```

/src/pages/Paging and searching/index.js

```
import React, { Component } from "react";
import { Link } from "react-router-dom";
import axios from "axios";
import qs from "qs";
import "./index.css";

var token = window.localStorage.getItem("token");

class Pegsearch extends Component {
  state = {
    articleList: [],

    searchTitle: "",
    searchCreatedBegin: "",
    searchCreatedEnd: "",

    currentPage: 1,
    pageSize: 5, //每页条数
    itemCount: 0, //总记录条数
  };

  //计算分页数
  showPage = () => {
    let pageTotal = Math.ceil(this.state.itemCount / this.state.pageSize);

    let numbers = [];

    //循环生成span 跳转标签 并将它们装进numbers内  再放在下拉框后面
    for (let i = 1; i <= pageTotal; i++) {
      numbers.push(
        <span
          className={this.state.currentPage === i ? "active" : ""}
          key={i}
          onClick={() => {
            console.log(i);
            //setState没有生效 异步 改变时不会立即生效 需要一定的时间
            this.setState({ currentPage: i }, () => {
              this.getData();
            });

            // setTimeout(this.getData,1000)  上面情况可以用延时方法处理
            //也可以使用回调函数处理
          }}
        >
          {i}
        </span>
      );
    }

    return (
      <div>
        共{this.state.itemCount}条
        
        //下拉框添加事件 获取option内的值  并用setState改变state.itemCount(总记录条数)
        <select
          className="form-item"
          onChange={(e) => {
            console.log("this.state.itemCount" + this.state.itemCount);
            console.log("e.target.value" + e.target.value);
            this.setState(
              {
                pageSize: e.target.value,
                currentPage: 1,
              },
              this.getData
            );
          }}
        >
          <option value="5">5条/页</option>
          <option value="10">10条/页</option>
          <option value="15">15条/页</option>
        </select>

        {numbers}     //numbers

        跳至{" "}
        <input
          onKeyDown={(e) => {
            let pageTotal = Math.ceil(
              this.state.itemCount / this.state.pageSize
            );
            if (e.target.value > pageTotal) {
              e.target.value = "";
              alert("无");
            } else {
              if (e.keyCode === 13) {
                this.setState({ currentPage: e.target.value }, this.getData);
              }
            }
          }}
          size="3"
          className="form-item"
        />
        页
      </div>
    );
  };

    //拉取文章列表
  getData = () => {
    axios
      .get(`http://playground.it266.com/article?token=${token}`, {
        params: {
          page: this.state.currentPage,
          page_size: this.state.pageSize,

          title: this.state.searchTitle,
          created_begin: this.state.searchCreatedBegin,
          created_end: this.state.searchCreatedEnd,
        },
      })
      .then((response) => {
        console.log(response);
        let result = response.data;

        if (!result.status) {
          alert(result.data);
          return;
        }

        this.setState({
          articleList: result.data.articles,

          itemCount: result.data.page.itemCount,
          currentPage: result.data.page.currentPage,
          pageSize: result.data.page.pageSize,
        });
      });
  };
  componentDidMount() {
    this.getData();
  }
  //删除文章
  deleteArticle = (id) => {
    axios({
      method: "post",
      url: `http://playground.it266.com/article/delete?token=${token}`,
      headers: { "Content-Type": "application/x-www-form-urlencoded" },
      data: qs.stringify({
        id: id,
      }),
    })
      .then((response) => {
        console.log(response);
        if (response.data.status) {
          alert(response.data.data);

          //删除成功后 重新获取书籍信息
          this.getData();

          this.props.history.push("/PagingAndSearch");
        } else {
          alert(response.data.data);
        }
      })
      .catch((error) => {
        alert("出错了");
      });
  };

  render() {
    return (
      <div className="pegsearch">
        <h2>分⻚和搜索</h2>

        <div style={{ margin: "10px 0" }}>
          <input
            type="text"
            className="form-item"
            placeholder="标题"
            value={this.state.searchTitle}
            onChange={(e) => {
              this.setState({ searchTitle: e.target.value });
            }}
          />
          <input
            type="text"
            className="form-item"
            placeholder="开始时间"
            value={this.state.searchCreatedBegin}
            onChange={(e) => {
              this.setState({ searchCreatedBegin: e.target.value });
            }}
          />
          <input
            type="text"
            className="form-item"
            placeholder="结束时间"
            value={this.state.searchCreatedEnd}
            onChange={(e) => {
              this.setState({ searchCreatedEnd: e.target.value });
            }}
          />

          <button className="form-item" onClick={this.getData}>
            搜索
          </button>
          <button
            className="form-item"
            onClick={() => {
              this.setState(
                {
                  searchTitle: "",
                  searchCreatedBegin: "",
                  searchCreatedEnd: "",
                },
                this.getData
              );
            }}
          >
            重置
          </button>
        </div>

        <table border="1">
          <thead>
            <tr>
              <th width="60">ID</th>
              <th>标题</th>
              <th width="165">发表时间</th>
              <th width="120">操作</th>
            </tr>
          </thead>
          <tbody>
            {this.state.articleList.map((article) => {
              return (
                <tr key={article.id}>
                  <td>{article.id}</td>
                  <td>{article.title}</td>
                  <td>{article.created_at}</td>
                  <td>
                    <Link to={`/article/edit/${article.id}`}>编辑</Link>

                    <span
                      style={{ cursor: "pointer" }}
                      onClick={() => {
                        this.deleteArticle(article.id);
                      }}
                    >
                      <Link to={`/PagingAndSearch`}>删除</Link>
                    </span>
                  </td>
                </tr>
              );
            })}
          </tbody>
        </table>

        <div style={{ mariginTop: 10 }}>
          <div className="pagination">

            {this.showPage()}

          </div>
        </div>
      </div>
    );
  }
}
export default Pegsearch;

```



## 9.跨组件通讯

### 父传子 子传父

```
同级传值(父传子，子传父)
app组件传值top，login组件。通过公共组件app
app组件定义state，先传入top
父传子
app组件内 
state={
	nickName：""
}
<Top ninckName={this.state.nickname}></Top>在top中显示收到的值
this.props.nickName

子修改父
父组件定义一个函数，传给子组件
app组件内 
setNickname=(val)=>{
    this.setState({nickname:val})
}
rander(){
    <Routh path="/login" >//注意没有括号
        <login setNickname={this.setNickname}> </login>
    </Routh>
}子组件调用函数修改传值
login
<button onClick={()=>{
    this.props.setNickname(this.state.nickname)
}}>login
    </button>优点，反应迅速，不需要网页刷新  缺点，当面对嵌套较深的组件，需要层层传递，
父传子
在父组件里声明变量或者声明一个含有属性的状态,在子组件标签内写上属性名={this.state.属性或者this.变量}
子组件中用this.props.属性名获取传来的值

子传父
在父组件里定义一个接收参数的方法,方法内写this.setState({属性:传的参数}),在子组件标签内写上属性名={this.方法名}
子组件中用this.props.属性名(需要传递的实参)调用方法   传参的函数需要使用箭头函数包着

父传子
父组件声明一个变量  子组件标签内写属性名=this.变量
子组件内用this.props.属性名

子传父
父组件声明一个函数 在子组件标签里写属性名=this.方法
在子组件里用this.props.属性名(传递需要修改的参数)
```

**父传子   从父组件传递一个值到一个子组件中,又传一个方法到另一个子组件中用于改变传递的那个值**

**上述方法不适用于组件层级关系嵌套复杂的情况   过于繁琐  需要一直传递**

```
//父传子
//在父组件中定义状态(或者var一个变量,记得在前面加上this.)  在子组件标签中写上    "属性名={this.变量}"

//在子组件调用父组件传递的值
this.props.属性名
```



```
//子传父
//在父组件中定义方法和状态(或者var一个变量,记得在前面加上this.) 将方法写进子组件标签中  "属性名={this.方法}"
//在login子组件中用

//子组件也需要定义状态state={nickname:''}或者声明一个变量

this.state.nickname
this.setState({nickname:e.tatget.value}) //用于修改login组件中的state

this.props.setNickname(this.state.nickname) //将login组件中的this.state.nickname传到父组件中   调用setNickname修改父组件中的nickname
class App extends React.Component{
    state = {
        nickname:''
    }

	setNickname = (val) =>{
        this.setState({nickname:val})
    }
    
    render(){
        return(
        	<HashRouter>
            	<Top nickname={this.state.nickname}></Top>
				<Switch>
                    <Route path='/login' >
                        <Login setNickname={this.setNickname}></Login>
                    </Route>
            	</Switch>
            </HashRouter>
        )
    }
}
export default App
```



### Context上下文

**父组件**

导出一个React.createContext(不用加default,一个组件只有一个default),是provider,并在里面写上value

```
import React from "react";
import Login from "./bpp/login/index";
import Top from "./bpp/top/index";
import { HashRouter, Switch, Route } from "react-router-dom";

//Context上下文   导出AuthContext
export const AuthContext = React.createContext({
  user: null,
});

class Bpp extends React.Component {
  state = {
    user:null,
    // nickname: "jack", avatar: "http://example.com/jpg1"
  };

  setUser = (val) => {
    this.setState({ user: val });
  };
  render() {
    return (
                    //provider 
      <AuthContext.Provider value={{ user:this.state.user}}>
        
        //里面的组件只需导入context 并在组件内加上 <变量名＋consumer>  就可以获得父组件的数据
        <HashRouter>
          <Top></Top>
          <Switch>
            <Route path="/login">
              <Login setUser={this.setUser}></Login>     ///传方法到login组件,就可以修改user的值
            </Route>
          </Switch>
        </HashRouter>
      </AuthContext.Provider>
    );
  }
}
export default Bpp;
```

**top组件**

```
import React, { Component } from "react";
import { Link } from "react-router-dom";

import "./index.css";

//在需要传值的组件中导入context   该组件就是consumer

import { AuthContext } from "../../bpp";

class Top extends Component {
  render() {
    return (
      <AuthContext.Consumer>
        {/* 写一个函数接收provider提供的数据 */}
        {(value) => {
          console.log(value);}

          return (
            <div className="top">
              {value.user ? (<div className="login">{" "}当前用户:{value.user.nickname} 退出</div>
              ) : (<div className="login">{" "}<Link to="/login">请登录</Link></div>)}
              <div>
                <ul>
                  <li><Link to="/">首页</Link></li>
                  <li><Link to="/article">文章管理</Link></li>
                  <li><Link to="/">会员管理</Link></li>
                </ul>
                <div className="clear"></div>
              </div>
            </div>
          );
        }}
      </AuthContext.Consumer>
    );
  }
}
export default Top;
```

**Login组件**

```
import React, { Component } from "react";

class Login extends Component {

  state={
    nickname:'',
  }

  render() {
    return (
      <div className="login">
        <h3>登录</h3>
        <div className="username">name:
          <input
            type="text"
            value={this.state.nickname}
            onChange={(e) => {
              this.setState({ nickname: e.target.value });
            }}
          />
        </div>

        <div className="password">password:<input type="password" /></div>
        
        //从bpp组件获得的setUser方法
        <div><button onClick={()=>{this.props.setUser({nickname:this.state.nickname})}}>login</button></div>
            
      </div>
    );
  }
}
export default Login;

```

**对上面在子组件标签内传方法进行优化**  **不限层级嵌套** 

**不将方法写入到标签内,写在标签内时,其他组件使用时比较繁琐**

**将方法写进context内  可以跨组件进行传方法**

```
import React from "react";
import Login from "./bpp/login/index";
import Top from "./bpp/top/index";
import { HashRouter, Switch, Route } from "react-router-dom";

//持久化处理  页面刷新时用户名也不会变  将数据存在localStorage处
let nickname = window.localStorage.getItem('nickname')

//Context上下文   导出AuthContext
export const AuthContext = React.createContext({
  	user: null,
  	setUser = () => {
  	},
});

class Bpp extends React.Component {
  	constructor(props){
        super(props);
        
        this.setUser = (u)=>{
            this.setState({auth:{...this.state.auth,user:u}})
        }
   
    	//初始值
        this.state = {
            auth:{
                user:nickname ?{nickname:nickname}:null,
                setUser : this.setUser,
            }
        } 
    }
      
  render() {
    return (
       				//provider 
      <AuthContext.Provider value={{ this.state.auth}}>
        
        //里面的组件只需导入context 并在组件内加上 <变量名＋consumer>  就可以获得父组件的数据
        <HashRouter>
          <Top></Top>
          <Switch>
            <Route path="/login">
              <Login></Login> 
            </Route>
          </Switch>
        </HashRouter>
      </AuthContext.Provider>
    );
  }
}
export default Bpp;
```

**login组件**

```
import React, { Component } from "react";
import { AuthContext } from "../../bpp";

class Login extends Component {

  state={
    nickname:'',
  }

  render() {
    return (
      <AuthContext.Consumer>
        
        {(auth)=>{
        	console.log(auth)
    	}}
		return(){
        	 <div className="login">
            <h3>登录</h3>
            <div className="username">name:
              <input
                type="text"
                value={this.state.nickname}
                onChange={(e) => {
                  this.setState({ nickname: e.target.value });
                }}
              />
            </div>
            <div className="password">password:<input type="password" /></div>
            //从bpp组件获得的setUser方法
            <div><button onClick={()=>{
                
               	//将用户名存于loaclStorage中 
                window.localStorage.setItem('nickname',this.state.nickname)
                auth.setUser({nickname:this.state.nickname})
                
            }}>login</button>				</div>
          </div>    
        }
         
	</AuthContext.Consumer> 
    );
  }
}
export default Login;
```

**top组件**

```
import React, { Component } from "react";
import { Link } from "react-router-dom";

import "./index.css";

//在需要传值的组件中导入context   该组件就是consumer

import { AuthContext } from "../../bpp";

class Top extends Component {
  render() {
    return (
      <AuthContext.Consumer>
        {/* 写一个函数接收provider提供的数据 */}
        {(value) => {
          console.log(value);

          return (
            <div className="top">
              
              {value.user ? (<div className="login">{" "}当前用户:{value.user.nickname} 
      		<span onClick={()=>{value.setUser(null)}}
     		 >退出</span></div>
              ) : (<div className="login">{" "}<Link to="/login">请登录</Link></div>)}
              <div>
                <ul>
                  <li><Link to="/">首页</Link></li>
                  <li><Link to="/article">文章管理</Link></li>
                  <li><Link to="/">会员管理</Link></li>
                </ul>
                <div className="clear"></div>
              </div>
            </div>
          );
        }}
      </AuthContext.Consumer>
    );
  }
}
export default Top;
```

### 官方文档



### `React.createContext`

```
const MyContext = React.createContext(defaultValue);
```

**创建一个 Context 对象。当 React 渲染一个订阅了这个 Context 对象的组件，这个组件会从组件树中离自身最近的那个匹配的 `Provider` 中读取到当前的 context 值/////////////////.。**

**只有当组件所处的树中没有匹配到 Provider 时，其 `defaultValue` 参数才会生效。此默认值有助于在不使用 Provider 包装组件的情况下对组件进行测试。注意：将 `undefined` 传递给 Provider 的 value 时，消费组件的 `defaultValue` 不会生效。**

### `Context.Provider`

```
<MyContext.Provider value={/* 某个值 */}>
```

**每个 Context 对象都会返回一个 Provider React 组件，它允许消费组件订阅 context 的变化。**

**Provider 接收一个 `value` 属性，传递给消费组件。一个 Provider 可以和多个消费组件有对应关系。多个 Provider 也可以嵌套使用，里层的会覆盖外层的数据。**

**当 Provider 的 `value` 值发生变化时，它内部的所有消费组件都会重新渲染。从 Provider 到其内部 consumer 组件（包括 [.contextType](https://zh-hans.reactjs.org/docs/context.html#classcontexttype) 和 [useContext](https://zh-hans.reactjs.org/docs/hooks-reference.html#usecontext)）的传播不受制于 `shouldComponentUpdate` 函数，因此当 consumer 组件在其祖先组件跳过更新的情况下也能更新。**

**通过新旧值检测来确定变化，使用了与 [`Object.is`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is#Description) 相同的算法。**

### `Class.contextType`

```
class MyClass extends React.Component {
  componentDidMount() {
    let value = this.context;
    /* 在组件挂载完成后，使用 MyContext 组件的值来执行一些有副作用的操作 */
  }
  componentDidUpdate() {
    let value = this.context;
    /* ... */
  }
  componentWillUnmount() {
    let value = this.context;
    /* ... */
  }
  render() {
    let value = this.context;
    /* 基于 MyContext 组件的值进行渲染 */
  }
}
MyClass.contextType = MyContext;
```

**挂载在 class 上的 `contextType` 属性可以赋值为由 [`React.createContext()`](https://zh-hans.reactjs.org/docs/context.html#reactcreatecontext) 创建的 Context 对象。此属性可以让你使用 `this.context` 来获取最近 Context 上的值。你可以在任何生命周期中访问到它，包括 render 函数中。**

```
class MyClass extends React.Component {
  static contextType = MyContext;
  render() {
    let value = this.context;
    /* 基于这个值进行渲染工作 */
  }
}
```

### `Context.Consumer`

```
<MyContext.Consumer>
  {value => /* 基于 context 值进行渲染*/}
</MyContext.Consumer>
```

**一个 React 组件可以订阅 context 的变更，此组件可以让你在[函数式组件](https://zh-hans.reactjs.org/docs/components-and-props.html#function-and-class-components)中可以订阅 context。**

**这种方法需要一个[函数作为子元素（function as a child）](https://zh-hans.reactjs.org/docs/render-props.html#using-props-other-than-render)。这个函数接收当前的 context 值，并返回一个 React 节点。传递给函数的 `value` 值等价于组件树上方离这个 context 最近的 Provider 提供的 `value` 值。如果没有对应的 Provider，`value` 参数等同于传递给 `createContext()` 的 `defaultValue`。**

### `Context.displayName`

**context 对象接受一个名为 `displayName` 的 property，类型为字符串。React DevTools 使用该字符串来确定 context 要显示的内容。**

**示例，下述组件在 DevTools 中将显示为 MyDisplayName：**

```
const MyContext = React.createContext(/* some value */);
MyContext.displayName = 'MyDisplayName';
<MyContext.Provider> // "MyDisplayName.Provider" 在 DevTools 中
<MyContext.Consumer> // "MyDisplayName.Consumer" 在 DevTools 中
```

### 作用及特点

**在一个典型的 React 应用中，数据是通过 props 属性自上而下（由父及子）进行传递的，但此种用法对于某些类型的属性而言是极其繁琐的（例如：地区偏好，UI 主题），这些属性是应用程序中许多组件都需要的。Context 提供了一种在组件之间共享此类值的方式，而不必显式地通过组件树的逐层传递 props。**

**Context 设计目的是为了共享那些对于一个组件树而言是“全局”的数据，例如当前认证的用户、主题或首选语言。**

**Context 设计目的是为了共享那些对于一个组件树而言是“全局”的数据，例如当前认证的用户、主题或首选语言。举个例子，在下面的代码中，我们通过一个 “theme” 属性手动调整一个按钮组件的样式：**

```
class App extends React.Component {
  render() {
    return <Toolbar theme="dark" />;
  }
}

function Toolbar(props) {
  // Toolbar 组件接受一个额外的“theme”属性，然后传递给 ThemedButton 组件。
  // 如果应用中每一个单独的按钮都需要知道 theme 的值，这会是件很麻烦的事，
  // 因为必须将这个值层层传递所有组件。
  return (
    <div>
      <ThemedButton theme={props.theme} />
    </div>
  );
}

class ThemedButton extends React.Component {
  render() {
    return <Button theme={this.props.theme} />;
  }
}
```

**使用 context, 我们可以避免通过中间元素传递 props：**

```
// Context 可以让我们无须明确地传遍每一个组件，就能将值深入传递进组件树。
// 为当前的 theme 创建一个 context（“light”为默认值）。
const ThemeContext = React.createContext('light');
class App extends React.Component {
  render() {
    // 使用一个 Provider 来将当前的 theme 传递给以下的组件树。
    // 无论多深，任何组件都能读取这个值。
    // 在这个例子中，我们将 “dark” 作为当前的值传递下去。
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

// 中间的组件再也不必指明往下传递 theme 了。
function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  // 指定 contextType 读取当前的 theme context。
  // React 会往上找到最近的 theme Provider，然后使用它的值。
  // 在这个例子中，当前的 theme 值为 “dark”。
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;
  }
}
```



## 10.Hook!

### mockjs

Mock.js 是一款模拟数据生成器，旨在帮助前端攻城师独立于后端进行开发，帮助编写单元测试。提供了以下模拟功能：

- 根据数据模板生成模拟数据
- 模拟 Ajax 请求，生成并返回模拟数据
- 基于 HTML 模板生成模拟数据

```
安装   npm  install  mockjs  --save
//url
//参数
//返回数据
//文章列表
//page page_size
{
	statue:true,
	date:[
		{id:1,title:"标题一"}
		{id:2,title:"标题二"}
	]
}
import Mock from "mockjs"

Mock.mock('/api/article','get',{
    status:true,
    date:[
        {id:1,title:"标题一"}
		{id:2,title:"标题二"}
    ]
})
import Mock from "mockjs"
			//rurl路径			rtype类型  template模板
Mock.mock(/\/api\/article\/create/,'post',{
    status:true,
    data:"新增成功"
})

Mock.mock(/\/api\/article.*/,'get',{
    status:true,
    date:[
        {id:1,title:"标题一"}
		{id:2,title:"标题二"}
    ]
    
})
```

### hook

**Hook 是一些可以让你在函数组件里“钩入” React state 及生命周期等特性的函数。Hook 不能在 class 组件中使用 —— 这使得你不使用 class 也能使用 React。（我们[不推荐](https://zh-hans.reactjs.org/docs/hooks-intro.html#gradual-adoption-strategy)把你已有的组件全部重写，但是你可以在新组件里开始使用 Hook。）**

#### 声明多个 state 变量

将 state 变量声明为一对 `[something, setSomething]` 也很方便，因为如果我们想使用多个 state 变量，它允许我们给不同的 state 变量取不同的名称：

```
function ExampleWithManyStates() {
  // 声明多个 state 变量！
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}

//在以上组件中，我们有局部变量 age，fruit 和 todos，并且我们可以单独更新它们：

 function handleOrangeClick() {
    // 和 this.setState({ fruit: 'orange' }) 类似
    setFruit('orange');
  }
Hook 就是 JavaScript 函数，但是使用它们会有两个额外的规则：

只能在函数最外层调用 Hook。不要在循环、条件判断或者子函数中调用。
只能在 React 的函数组件中调用 Hook。不要在其他 JavaScript 函数中调用。（还有一个地方可以调用 Hook —— 就是自定义的 Hook 中，我们稍后会学习到。）
```

#### 总结

```
 1:  import React, { useState } from 'react'; 2:
 3:  function Example() {
 4:    const [count, setCount] = useState(0); 5:
 6:    return (
 7:      <div>
 8:        <p>You clicked {count} times</p>
 9:        <button onClick={() => setCount(count + 1)}>10:         Click me
11:        </button>
12:      </div>
13:    );
14:  }
第一行: 引入 React 中的 useState Hook。它让我们在函数组件中存储内部 state。
第四行: 在 Example 组件内部，我们通过调用 useState Hook 声明了一个新的 state 变量。它返回一对值给到我们命名的变量上。我们把变量命名为 count，因为它存储的是点击次数。我们通过传 0 作为 useState 唯一的参数来将其初始化为 0。第二个返回的值本身就是一个函数。它让我们可以更新 count 的值，所以我们叫它 setCount。
第九行: 当用户点击按钮后，我们传递一个新的值给 setCount。React 会重新渲染 Example 组件，并把最新的 count 传给它。
const [fruit, setFruit] = useState('banana');
```

这种 JavaScript 语法叫[数组解构](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring)。它意味着我们同时创建了 `fruit` 和 `setFruit` 两个变量，`fruit` 的值为 `useState` 返回的第一个值，`setFruit` 是返回的第二个值。它等价于下面的代码：

```
var fruitStateVariable = useState('banana'); // 返回一个有两个元素的数组
var fruit = fruitStateVariable[0]; // 数组里的第一个值
var setFruit = fruitStateVariable[1]; // 数组里的第二个值
```



### 类变函数式组件

```
import React,{useEffect,useState} from 'react';
import axios from "axios"

function Article(){
    //变量名类似state 用于修改变量的方法类似setState
    let [articleList,setArticleList] = useState([])
    
    //相当于挂载  当页面切走时触发
    useEffect (()=>{
        
        axios.get('/api/article',{
            params:{
                page:1,
            }
        }).then((res)=>{
            setArticleList(res.data.data)
        })
        
        //return()=>{                  相当于取消挂载 
           // console.log("成功切换页面")
        //}
        
    },[])   //deps:[]依赖  依赖里面的内容修改时 useEffect内的内容会重新执行
 
    return(
        <>
            <h3>文章管理页面</h3>
            <ul>
                {articleList.map(item =>{
                    return<li key={item.id}>{item.title}</li>
                })}
            </ul>
        </>
    )
}

export default Article
```



# react使用

## 常用方法

**浏览器缓存**

```
window.localStorage.setItem("token",token)
```

**获取缓存**

```
let  token=window.localStorage.token
```

**清除缓存**

```
window.localStorage.removeItem("token")
```

## 三元表达式的用法

在react中,三元表达式可以用变量动态更改各种数据,包括网页地址

```
 useEffect(() => {
        let token = window.localStorage.token
        axios({
            method: "GET",
            url: `http://xueba.it266.com:8081/api/post/${mypoststate === "one" ? "my" : "myFavorite"}?limit=${limitpage.limit}&page=${limitpage.page}&token=${token}`,
            headers: {'Content-Type': 'application/x-www-form-urlencoded'},
        }).then((response) => {
            response.data.code !== "SUCCESS" ? alert(response.data.message) :
                console.log("个人帖子获取成功：", response.data.data.postDtoList)
            setMypost(response.data.data.postDtoList)
        }).catch((error) => {
            console.log("个人帖子获取失败", error)
        })
        return () => {
        }
    }, [mypoststate])
```

在函数调用里需要return，只能用来赋值，调用只能return

```
return (
response.data.code === "SUCCESS" ?
(
alert("登录成功"),
props.history.push("./"),
window.localStorage.setItem("token", response.data.data.token)
)
:
alert(response.data.message)
)
```



## 头文件文件的导入

**样式导入**

> import  +  “路径名”

```
import "./product.css"
```

**组件导入**

> import  + 函数名/类名 +from +“路径名字”

```
import Search from "./components/search/"
```

**图片导入**

> import + 图片名   + from +“路径名”

```
import  Banner0 from "../imgs/banner/Banner0.png"
```

**class组件**

```
import React, { Component } from 'react';


class App extends React.Component {
    render() {
        return (
        <div>hello，jack</div>
        )
}
```

**插入axios**

```
import axios from "axios";
```

**插入路由各种信息**

```
//导入路由组件,切换组件，路径组件
import { HashRouter, Switch,Route} from "react-router-dom"
```

**插入Link信息**,切换展示状态

```
import {Link} from "react-router-dom"

<Link to="/home"></Link>

this.props.history.push("/home")
this.props.history.replace("/profile")
```

> **路由跳转出错**

```
import {withRouter} from 'react-router-dom'
  this.props.history.push("/home")
export default withRouter(Login)
```

input报错

```
<input autoComplete="on"/>
```

行内样式

```
 style={{backgroundImage: `url(${value.auth.avatar})`}}>
```

上传文件

```
<div class="row">
<input type="file" accept="image/*">
<input type="button" value="上传">
</div>
```



## **context格式**

**AuthContext（头部文件）**//导出  上下文 等于定义一个特殊的组件

```
export const AuthContext = React.createContext({
  user: null,
});
```

**Provider(生产者)**: 和他的名字一样。用于生产共享数据的地方。生产什么呢？ 那就看value定义的是什么了。value:放置共享的数据。

```
<Provider value={/*共享的数据*/}>
    /*里面可以渲染对应的内容*/
</Provider>
```

**Consumer(消费者)**:这个可以理解为消费者。 他是专门消费供应商(**Provider** 上面提到的)产生数据。Consumer需要嵌套在生产者下面。才能通过回调的方式拿到共享的数据源。当然也可以单独使用，那就只能消费到上文提到的defaultValue



```
<Consumer>
  {value => /*根据上下文  进行渲染相应内容*/}
</Consumer>
```

## 函数组件、类组件

**函数组件**

```
//导入react
import React from "react";
//导入样式
import "./product.css"

// 组件
function Product(props) {
    console.log(props)
    return (
        <div>
            <div className="product-name">{props.name}</div>
            <div>单价：{props.price}</div>
        </div>
    )
}
```

**类组件**

基础模板

```
import React ,{ Component }from "react"
// import {Switch,Route} from "react-router-dom"
// import Index from "./component"
// import Create from "./component/create"
// import Edit from "./component/edit"
// import Detail from "./component/detail"
// import Top from "../../components/top"



class Article extends Component{
    componentWillUnmount(){

    }

    render(){
        return(
            <div>
                <h1>文章管理</h1>
             </div>  
        )
    }
}
export default Article
```

**1.1.constructor()**

constructor()中完成了React数据的初始化，它接受两个参数：props和context，当想在函数内部使用这两个参数时，需使用super()传入这两个参数。 注意：只要使用了constructor()就必须写super(),否则会导致this指向错误。

```
import React from "react";
import { HashRouter, Switch, Route } from "react-router-dom";

import "./app.css"


// import Home from "./pages/home"
// import Top from "./components/top"
// import Member from "./pages/member"

import Login from "./pages/login"
import Register from "./pages/register"
import Profile from "./pages/profile"
import Article from "./pages/article"


let nickname = window.localStorage.getItem("nickname")


//导出数据
export const AuthContext = React.createContext({
    user: null,
    setUser: () => {},
})

class App extends React.Component {
    constructor(props) {//会在组件初始化的时候自动执行
        //props是自带得属性     
        //继承App这个方法
        super(props);
        this.setUser = (u) => {
            // this.setState({ auth: { user: u , setUser: this.setUser} })
            this.setState({ auth: { ...this.state.auth, user: u } })
        }
        this.state = {
            auth: {
                // eslint-disable-next-line eqeqeq
                user: {
                    id: '',
                    token: '',
                    mobile: '',
                    nickname: nickname ?   nickname  : '无',
                },

                setUser: this.setUser
            }
        }
    }
    render() {
        return (
            <AuthContext.Provider value={this.state.auth}>
                <HashRouter>
                    {/* <Top></Top> */}
                    <Switch>
                        {/* <Route exact path="/" component={Home} ></Route> */}
                        {/* 
                        <Route path="/member" component={Member}></Route> */}
                        {/* <Route path="/login" ><Login setUser={this.setUser}></Login></Route> */}
                        {/* <Route path="/login" ><Login setUser={this.setUser}></Login></Route> */}
                        <Route exact path="/" ><Login></Login></Route>
                        <Route path="/profile" ><Profile></Profile></Route>
                        <Route path="/register" ><Register></Register></Route>
                        <Route path="/article" component={Article}></Route>
                    </Switch>
                </HashRouter>
            </AuthContext.Provider>

        )
    }
}
export default App
```

**1.2.componentWillMount()**

componentWillMount()一般用的比较少，它更多的是在服务端渲染时使用。它代表的过程是组件已经经历了constructor()初始化数据后，但是还未渲染DOM时。

**1.3.componentDidMount()**

组件第一次渲染完成，此时dom节点已经生成，可以在这里调用ajax请求，返回数据setState后组件会重新渲染

**1.4.componentWillUnmount ()**

在此处完成组件的卸载和数据的销毁。

1. clear你在组建中所有的setTimeout,setInterval
2. 移除所有组建中的监听 removeEventListener
3. 有时候我们会碰到这个warning:

```
Can only update a mounted or mounting component. This usually      means you called setState() on an unmounted component. This is a   no-op. Please check the code for the undefined component.
```

原因：因为你在组件中的ajax请求返回setState,而你组件销毁的时候，请求还未完成，因此会报warning 解决方法：

**setInterval()的清除**

```
componentDidMount() {
    this.isMount === true
    axios.post().then((res) => {
    this.isMount && this.setState({   // 增加条件ismount为true时
      aaa:res
    })
})
}
componentWillUnmount() {
    this.isMount === false
}
```



```
                    let time = 5
                    let timer = setInterval(() => {
                        let registerVerify = document.getElementsByClassName("register-verify")[0]
                        if (registerVerify) {
                            // console.log("registerVerify", registerVerify)
                            registerVerify.disabled = true;
                            registerVerify.style.color = "grey"
                            registerVerify.innerHTML = time
                            time = time - 1
                            // console.log(time)
                            if (time === 0) {
                                clearInterval(timer)
                                registerVerify.disabled = false;
                                registerVerify.innerHTML = "获取验证码"
                                registerVerify.style.color = "rgb(0,152,208)"

                            }
                        }
                    }, 1000)
```

## map生成数组

> set是使用二叉搜索树维护集合的容器，map是维护键和键对应的的值的容器。

```
const newData = data.set("todos",data.get("todos").map(item=>{
    return item.get("id") == 2 ? item.set("title" , "吃鸡") : item;
}))
```



```
let articles = [
    { "id": 1, "title": "援鄂专家口述:如何让爆满重压中的定点医院上轨道" },
    { "id": 2, "title": "dwadwadawdwadawdawdawdwawdawdadwadwawda" },
    { "id": 3, "title": "23121432543435654673242345743757457477" },
]
let App = (
    <div>
        {
            articles.map((item) => {
                return <Article key={item.id} {...item}></Article>
            })
        }
        <Article {...articles[0]}></Article>
        <Article {...articles[1]}></Article>
        <Article {...articles[2]}></Article>
    </div>
)
render(App, document.getElementById("root"))
```

> key必须要等于一个不重复的数

```
let articles = [
    { "id": 1, "title": "援鄂专家口述:如何让爆满重压中的定点医院上轨道" },
    { "id": 2, "title": "dwadwadawdwadawdawdawdwawdawdadwadwawda" },
    { "id": 3, "title": "23121432543435654673242345743757457477" },
]
// articles.map((item)=>{
//     console.log(item)
// })

let App = (
    <div>
        {/*搜索*/}
        <Search></Search>
        {/*分类导航*/}
        <Nav></Nav>
        {/*幻灯⽚*/}
        <Banner></Banner>
        {/*⽂章列表*/}
        {
            articles.map((item) => {
                return <Article key={item.id} {...item}></Article>
            })
        }

        <Article {...articles[0]}></Article>
        <Article {...articles[1]}></Article>
        <Article {...articles[2]}></Article>
        {/*底部导航*/}
        <Tabbar></Tabbar>

        <Clock></Clock>
    </div>
)
render(App, document.getElementById("root"))
```

**map点击事件**修改类名

```
//导入react
import React,{Component}from 'react';
//导入样式
import "./style.css"


class Nav extends Component {
    state={
         //当前被选中的index
        activeIndex : 0,

    }


    handleClick(index) {
        console.log(index);
        this.setState({activeIndex:index})
    }
    // console.log(props)
    render() {
       
       

        let cateqoryList = ['首页', '推荐', '限免', '金融', '公司', '宏观']
        let navDate = cateqoryList.map((item, index) => {


            return <div
                key={index}
                className={this.state.activeIndex === index ? "nav-demo" : "" }
                onClick={()=>{this.handleClick(index)}}
                
                > {item}</div>
        })


        return (
            <div className="nav">
                <div className="nav-text">
                    {navDate}
                    {/* <div className="nav-demo">首页</div>
                <div className="nav-recommend">推荐</div>
                <div>限免</div>
                <div>金融</div>
                <div>公司</div>
                <div>宏观</div> */}
                </div>
                <div className="nav-symbol">+</div>

            </div>)
    }
}
//导出到App
export default Nav
```



```
得到Map对象的某一个键的值，要用get()方法

var immutable = require("immutable");
var fromJS = immutable.fromJS

const data = fromJS([
    {"id" : 1, "name" : "小明", "age" : 12},
    {"id" : 2, "name" : "小红", "age" : 12},
    {"id" : 3, "name" : "小强", "age" : 13},
])

const item = data.find(item=>item.get("id") == 2);
console.log(item.toJS())


删除用delete，删除下标为2的项

const list1 = fromJS([111,222,333,888,999]);
const list2 = list1.delete(2);
console.log(list1.toJS());
console.log(list2.toJS());
```

## map与set区别

### 一、set：

　　ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。类似python中的集合（set）

使用演示1：

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
const s = new Set();

[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));

for (let i of s) {
  console.log(i);
}
// 2 3 5 4
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

2: `Set`函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
// 例一
const set = new Set([1, 2, 3, 4, 4]);
[...set]
// [1, 2, 3, 4]

// 例二
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size // 5

// 例三
const set = new Set(document.querySelectorAll('div'));
set.size // 56
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

 

#### 用途1：去除数组重复成员或字符串里面的重复字符

```
// 去除数组的重复成员
[...new Set(array)]
```

　　注意：向 Set 加入值的时候，不会发生类型转换，所以`5`和`"5"`是两个不同的值。Set 内部判断两个值是否不同，NaN会认为等于自身。两个对象总是不相等的。

```

```

#### Set 实例的属性和方法

Set 结构的实例有以下属性。

- `Set.prototype.constructor`：构造函数，默认就是`Set`函数。
- `Set.prototype.size`：返回`Set`实例的成员总数。

Set 实例的方法分为两大类：操作方法（用于操作数据）和遍历方法（用于遍历成员）。下面先介绍四个操作方法。

- `Set.prototype.add(value)`：添加某个值，返回 Set 结构本身。
- `Set.prototype.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
- `Set.prototype.has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
- `Set.prototype.clear()`：清除所有成员，没有返回值。

Set 结构的实例有四个遍历方法，可以用于遍历成员。

- `Set.prototype.keys()`：返回键名的遍历器
- `Set.prototype.values()`：返回键值的遍历器
- `Set.prototype.entries()`：返回键值对的遍历器
- `Set.prototype.forEach()`：使用回调函数遍历每个成员

　　需要特别指出的是，`Set`的遍历顺序就是插入顺序。这个特性有时非常有用，比如使用 Set 保存一个回调函数列表，调用时就能保证按照添加顺序调用。

 

扩展运算符（`...`）内部使用`for...of`循环，所以也可以用于 Set 结构：

```
let set = new Set(['red', 'green', 'blue']);
let arr = [...set];
// ['red', 'green', 'blue']
```

 

#### 用途2: 使用 Set 可以很容易地实现并集（Union）、交集（Intersect）和差集（Difference）：

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// set {2, 3}

// 差集
let difference = new Set([...a].filter(x => !b.has(x)));
// Set {1}
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

 

#### 应用中的问题1：

　　如果想在遍历操作中，同步改变原来的 Set 结构，目前没有直接的方法，但有两种变通方法。一种是利用原 Set 结构映射（map）出一个新的结构，然后赋值给原来的 Set 结构；另一种是利用`Array.from`方法。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
// 方法一
let set = new Set([1, 2, 3]);
set = new Set([...set].map(val => val * 2));
// set的值是2, 4, 6

// 方法二
let set = new Set([1, 2, 3]);
set = new Set(Array.from(set, val => val * 2));
// set的值是2, 4, 6
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

 

 

### 二、WeakSet：

　　WeakSet 结构与 Set 类似，也是不重复的值的集合。但是，它与 Set 有两个区别。

　　首先，WeakSet 的成员只能是对象，而不能是其他类型的值。

　　其次，WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。

　　是因为垃圾回收机制依赖引用计数，如果一个值的引用次数不为`0`，垃圾回收机制就不会释放这块内存。结束使用该值之后，有时会忘记取消引用，导致内存无法释放，进而可能会引发内存泄漏。WeakSet 里面的引用，都不计入垃圾回收机制，所以就不存在这个问题。因此，WeakSet 适合临时存放一组对象，以及存放跟对象绑定的信息。只要这些对象在外部消失，它在 WeakSet 里面的引用就会自动消失。

　　由于上面这个特点，WeakSet 的成员是不适合引用的，因为它会随时消失。另外，由于 WeakSet 内部有多少个成员，取决于垃圾回收机制有没有运行，运行前后很可能成员个数是不一样的，而垃圾回收机制何时运行是不可预测的，因此 ES6 规定 WeakSet 不可遍历。

　　特点同样适用于本章后面要介绍的 WeakMap 结构。

 

#### 与set的区别：

　　（1）没有clear方法；（2）没有size属性； （3）没有遍历，所以没有那四个遍历方法。

 

 

### 三、Map：

　　JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

　　作为构造函数，Map 也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);

map.size // 2
map.has('name') // true
map.get('name') // "张三"
map.has('title') // true
map.get('title') // "Author"
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

　　不仅仅是数组，任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构（详见《Iterator》一章）都可以当作`Map`构造函数的参数。这就是说，`Set`和`Map`都可以用来生成新的 Map。

 

　　Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。这就解决了同名属性碰撞（clash）的问题，我们扩展别人的库的时候，如果使用对象作为键名，就不用担心自己的属性与原作者的属性同名。

　　如果 Map 的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map 将其视为一个键，比如`0`和`-0`就是一个键，布尔值`true`和字符串`true`则是两个不同的键。另外，`undefined`和`null`也是两个不同的键。虽然`NaN`不严格相等于自身，但 Map 将其视为同一个键。

 

#### 实例的属性和操作方法：

Map 结构的实例有以下属性和操作方法。

**（1）size 属性**

`size`属性返回 Map 结构的成员总数。

**（2）Map.prototype.set(key, value)**

`set`方法设置键名`key`对应的键值为`value`，然后返回整个 Map 结构。如果`key`已经有值，则键值会被更新，否则就新生成该键。

**（3）Map.prototype.get(key)**

`get`方法读取`key`对应的键值，如果找不到`key`，返回`undefined`。

**（4）Map.prototype.has(key)**

`has`方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。

**（5）Map.prototype.delete(key)**

`delete`方法删除某个键，返回`true`。如果删除失败，返回`false`。

**（6）Map.prototype.clear()**

`clear`方法清除所有成员，没有返回值。

 

#### 遍历方法：遍历的顺序就是插入的顺序

Map 结构原生提供三个遍历器生成函数和一个遍历方法。

- `Map.prototype.keys()`：返回键名的遍历器。
- `Map.prototype.values()`：返回键值的遍历器。
- `Map.prototype.entries()`：返回所有成员的遍历器。
- `Map.prototype.forEach()`：遍历 Map 的所有成员。

·Map 的`forEach`方法，与数组的`forEach`方法类似，也可以实现遍历。`forEach`方法还可以接受第二个参数，用来绑定`this`

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
map.forEach(function(value, key, map) {
  console.log("Key: %s, Value: %s", key, value);
});


const reporter = {
  report: function(key, value) {
    console.log("Key: %s, Value: %s", key, value);
  }
};

map.forEach(function(value, key, map) {
  this.report(key, value);
}, reporter);
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

 

#### 与其他数据结构的互相转换

**（1）Map 转为数组**

　　Map 转为数组最方便的方法，就是使用扩展运算符（`...`）。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
const map = new Map([
  [1, 'one'],
  [2, 'two'],
  [3, 'three'],
]);

[...map.keys()]
// [1, 2, 3]

[...map.values()]
// ['one', 'two', 'three']

[...map.entries()]
// [[1,'one'], [2, 'two'], [3, 'three']]

[...map]
// [[1,'one'], [2, 'two'], [3, 'three']]
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

**（2）数组 转为 Map**

　　将数组传入 Map 构造函数，就可以转为 Map。

**（3）Map 转为对象**

　　如果所有 Map 的键都是字符串，它可以无损地转为对象。如果有非字符串的键名，那么这个键名会被转成字符串，再作为对象的键名。

**🌟（4）Map 转为 JSON**

　　Map 转为 JSON 要区分两种情况。一种情况是，Map 的键名都是字符串，这时可以选择转为对象 JSON。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
function strMapToJson(strMap) {
  return JSON.stringify(strMapToObj(strMap));
}

let myMap = new Map().set('yes', true).set('no', false);
strMapToJson(myMap)
// '{"yes":true,"no":false}'
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

　　另一种情况是，Map 的键名有非字符串，这时可以选择转为数组 JSON。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
function mapToArrayJson(map) {
  return JSON.stringify([...map]);
}

let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']);
mapToArrayJson(myMap)
// '[[true,7],[{"foo":3},["abc"]]]'
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

**🌟（6）JSON 转为 Map**

　　JSON 转为 Map，正常情况下，所有键名都是字符串。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
function jsonToStrMap(jsonStr) {
  return objToStrMap(JSON.parse(jsonStr));
}

jsonToStrMap('{"yes": true, "no": false}')
// Map {'yes' => true, 'no' => false}
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

　　但是，有一种特殊情况，整个 JSON 就是一个数组，且每个数组成员本身，又是一个有两个成员的数组。这时，它可以一一对应地转为 Map。这往往是 Map 转为数组 JSON 的逆操作。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
function jsonToMap(jsonStr) {
  return new Map(JSON.parse(jsonStr));
}

jsonToMap('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

 

 

 

### 四、WeakMap：

#### `（1）WeakMap`与`Map`的区别有两点：

　　首先，`WeakMap`只接受对象作为键名（`null`除外），不接受其他类型的值作为键名。

　　其次，`WeakMap`的键名所指向的对象，不计入垃圾回收机制。

　　它的键名所引用的对象都是弱引用，即垃圾回收机制不将该引用考虑在内。因此，只要所引用的对象的其他引用都被清除，垃圾回收机制就会释放该对象所占用的内存。也就是说，一旦不再需要，WeakMap 里面的键名对象和所对应的键值对会自动消失，不用手动删除引用。

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

```
// 有时我们想在某个对象上面存放一些数据，但是这会形成对于这个对象的引用。最后必须删除，不然会引起内存泄漏：WeakMap可以避免

const e1 = document.getElementById('foo');
const e2 = document.getElementById('bar');
const arr = [
  [e1, 'foo 元素'],
  [e2, 'bar 元素'],
];


// 不需要 e1 和 e2 的时候
// 必须手动删除引用
arr [0] = null;
arr [1] = null;
```

[![复制代码](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181142794.gif)](javascript:void(0);)

　　注意，WeakMap 弱引用的只是键名，而不是键值。键值依然是正常引用。

 

#### （2）WeakMap 与 Map 在 API 上的区别主要是两个：

　　一是没有遍历操作（即没有`keys()`、`values()`和`entries()`方法），也没有`size`属性。因为没有办法列出所有键名，某个键名是否存在完全不可预测，跟垃圾回收机制是否运行相关。

　　二是无法清空，即不支持`clear`方法。

　　因此，`WeakMap`只有四个方法可用：`get()`、`set()`、`has()`、`delete()`。 

 

## axios请求

**插入axios类型转换**

```
import axios from "axios";
```

> params{}
>
> data: qs.stringify({  }),

```
 axios({
                method: "get",
                url: `http://playground.it266.com/api/user/profile`,
                headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
                params: { 'token': token }
               
            }).then((response) => {
                console.log(response) //服务器响应的数据
                if (response.data.status === false) {
                    console.log(response.data.data)
                    this.setState({
                        responseTips: response.data.data
                    })
                } else {
                    // window.localStorage.setItem("token", this.state.token)
                    window.localStorage.setItem("nickname", response.data.data.nickname)
                    //跳转到首页
                    // alert("登录成功")
                    let users = { ...response.data.data,token:token}
                    users.nickname = users.nickname ? users.nickname : '无'
                    auth.setUser(users)
                    console.log(users)
                    this.props.history.push("/profile")
                    // alert("登录成功")
    
                }
            }).catch((error) => {
                alert(error)
                console.log(error)
            })
```

## 动态生成文章列表

```
import "./style.css"
import axios from "axios";
import React, { Component } from 'react';


class Article extends Component {

    state = {
        articles: [], //默认⽂章列表为空数组
    }
    componentDidMount() {
        axios.get('http://playground.it266.com/news').then((response) => { //记得要使⽤箭头函数
            console.log(response) //服务器响应的数据
            this.setState({
                articles: [...response.data.articles],
            })
        }
        ).catch((error) => {
            console.log(error)
        })
    }
    render() {


        return (
            <div>
                {/* 在这⾥，循环this.state.articles，输出⽂章列表 */}
                {this.state.articles.map((item,index) => {
                    return (
                        <div  key={index} >
                            <div className="article">
                                <div className="article-text">

                                    <div  className="article-texts"> {item.title}</div>
                                    <div className="tip">
                                        <div className="tip-img">
                                        </div>
                                        <div className="tip-text">
                                            财经
                                        </div>
                                        <div className="tip-comment">
                                            108评论
                                        </div>
                                    </div>
                                </div>
                                <div className="article-bgimage"></div>
                            </div>
                        </div>
                    )

                })}
            </div>
        )
    }

}
export default Article
```

## 路由基础概念

安装路由

```
npm install react-router-dom --save
```

1.<BrowserRouter>组件：Router是BrowserRouter的别名，它表示BrowserRouter本身。而BrowserRouter使用了H5 Histroy API高阶路由组件；

2.<Switch>组件：它的作用是只渲染出第一个与当前访问地址匹配的<route>和<redireact>组件；

3.<Route/>组件：当地址URL和path属性设置的值匹配时，渲染出相应的UI组件界面；

4.<HashRouter>组件：它的作用主要利用Hash值的原理进行地址—UI匹配，在RR4中并没有抛弃，但是不建议使用；熟悉vue-router的可以知道，它跟vue-router匹配原理一样；

5.<NavLink>组件：主要用于导航拥有激活状态准备的；它和Link的路由匹配效果一致；不同的是NavLink有状态标记，Link无状态标记

## 路由基础作业

### src文件夹

> **index.js**

```
import React from "react";
import { render } from "react-dom";

import App from "./app";

render (<App/>,document.getElementById('root'))
```

> **app.js**首页路由

```
import React from "react"
// import React ,{ Component }from "react"
import Home from "./pages/home"
import Article from "./pages/article"

//安装路由
// npm install -S react-router-dom
// 导入路由组件,切换组件，路径组件
import { HashRouter, Switch,Route} from "react-router-dom"
import Login from "./pages/login"
//import {link} from "react-router-dom"



class App extends React.Component {
    render() {
        return (
            <HashRouter>            {/*HashRouter路由组件*/}
                <Switch>            {/*Switch切换组件*/}
                    
                    <Route exact path="/" component={Login}></Route>
                    <Route  path="/home" component={Home}></Route>
                    {/* exact：精确匹配,不会覆盖路径下的其他组件
                    path：路径，component：组成*/}
                    <Route path="/article" component={Article}></Route>
                </Switch>
            </HashRouter>

        )
    }
}
export default App
```

### pages文件夹

#### login文件夹

> **style.css**

```
*{
    margin: 0;
    padding: 0;
}
.login{
    font-size: 17px;
    opacity: 0.7;
    font-weight: 600;
}
.login-top{
    display: flex;
    height: 50px;
}
.login-back{
    width: 20px;
    height: 20px;
    background-image: url("./imgs/leftback.png");
    background-size: cover;
    margin-top: 15px;

}
.login-title{
    margin: 0 auto;
    line-height: 50px;
    font-weight: 800;
    font-size: 23px;
    opacity: 1;
}
.login-center{
    height: 40px;
    width: 100%;
    line-height: 40px;
    text-align: center;
    background-color: rgb(240, 240, 240);
}
.login-bottom{
    padding: 30px 40px 0px 30px;

}
.login-bottom input{
    width: 100%;
    height: 50px;
    font-size: 17px;
    outline: none;
    border: none;
    border-bottom: 2px solid rgb(240, 240, 240);
    padding-left: 10px;
}
.login-tip{
    color: red;
    padding-left: 10px;
    font-size: 12px;
    display: none;

}
.login-button{
    width: 85%;
    height: 50px;
    margin: 20px auto;

}
.login button{
    width: 100%;
    height: 100%;
    border: none;
    background-color: rgb(0,152,208);
    color: white;
    border-radius: 5px;
    font-size: 17px;


}
```

> **index.js**登录页

```
// 导入react
import React, { Component } from 'react';
//导入各种运行场景，浏览器
import Leftback from './imgs/leftback.png'
import "./style.css"
import axios from "axios"
import qs from "qs"
//⾃定义组件

class Login extends Component {

    state = {
        username: "",
        password: "",
        responseTips: "",
        tokenTip:"",

    }
    componentDidMount(){
        if(window.localStorage.token!==undefined){
            this.props.history.push("/home")
            console.log(window.localStorage.token);
        }
    }
    usernameInput = (e) => {
        console.log(e.target.value);
        this.setState({ username: e.target.value })
    }
    passwordInput = (e) => {
        console.log(e.target.value);
        this.setState({ password: e.target.value })
    }
    buttononClick = (e) => {
        let loginTip = document.getElementsByClassName("login-tip")
        console.log(e.target)

        axios({
            method: "post",
            url: 'http://playground.it266.com/login',
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            data: qs.stringify({ 'username': this.state.username, 'password': this.state.password }),
        }).then((response) => {
            console.log(response) //服务器响应的数据

            if (response.data.status === false) {
                console.log(response.data.data)
                this.setState({
                    responseTips: response.data.data
                })
                loginTip[0].style.display = "block"
                loginTip[1].style.display = "block"
            } else {
                this.setState({
                    tokenTip: response.data.data.token
                })
                window.localStorage.setItem("token", this.state.tokenTip)
                //跳转到首页
                
                alert("登录成功")
                this.props.history.push("/home")
                
            }

            console.log(response.data.data.token)
        }).catch((error) => {
            alert("出错了")
        })
    }


    render() {
        return (
            <div className="login">
                <div className="login-top">
                    <a href="www.baidu.com"><img className="login-back" src={Leftback} alt={Leftback} /> </a>
                    <div className="login-title">登录</div>
                </div>
                <div className="login-center">为了更好的体验，请登录</div>
                <div className="login-bottom">
                    <div>
                        <input value={this.state.username} className="username" type="text" placeholder="请输入账号"
                            onChange={this.usernameInput}


                        />
                        <div className="login-tip">{this.state.responseTips}</div>
                    </div>
                    <div>
                        <input value={this.state.password} className="password1" type="password" placeholder="请输入密码"
                            onChange={this.passwordInput}


                        />
                        <div className="login-tip">{this.state.responseTips}</div>
                    </div>


                </div>
                <div className="login-button">
                    <button
                        onClick={this.buttononClick}
                    >提交</button>
                </div>
            </div>
        )
    }
}


export default Login
```



#### home文件夹

> **index.css**

```
.home{
    border: 1px solid red;
    margin: 0 auto;
    width: 100px;
    
}
.home li{
    list-style-type:none;
}
.home a{
    text-decoration:none;
    color: blue;
}
```

> **index.js**首页

```
import React ,{ Component }from "react"
import {Link} from "react-router-dom"
import  "./index.css"


class Home extends Component{
    componentDidMount(){
        setInterval(() => {
            if(window.localStorage.token===undefined){
                this.props.history.push("/")
                console.log(window.localStorage.token);
            }
        }, 100);
    }
    exitClick(){
        localStorage.removeItem('token');
    }
    
    render(){
        return(
            <div className="home">
                <div style={{fontSize:'20px'}}>首页</div>
                <ul>
                    <li className="home-li" ><Link to="/article">文章管理</Link></li>
                    <li>会员管理</li>
                    <li><button onClick={this.exitClick}>退出登录</button></li>
                </ul>
            </div>
            
        )
    }
}
export default Home
```



#### article文件夹

> **index.js**列表路由

```
import React ,{ Component }from "react"
import {Switch,Route} from "react-router-dom"
import Index from "./component"
import Create from "./component/create"
import Edit from "./component/edit"
import Detail from "./component/detail"
class Article extends Component{
    render(){
        return(
            <div>

                <Switch>
                    <Route exact path="/article" component={Index}></Route>
                    <Route path="/article/create" component={Create}></Route>
                    <Route path="/article/edit/:id" component={Edit}></Route>
                    <Route path="/article/detail/:id" component={Detail}></Route>
                </Switch>
         
            </div>
            
        )
    }
}
export default Article
```

##### component文件夹

> **index.css**

```
.component-index table{
    border-collapse:collapse;
}
.component-index th,td{
    
    padding: 5px;
    border:2px solid black;
    
}
```

> **index.js**文章列表

```
import React, { Component } from "react"
import { Link } from "react-router-dom"
import axios from "axios"
import qs from "qs"
import "./index.css"


class Index extends Component {
    state = {
        page: "2",
        page_size: "6",
        articles: [], //默认⽂章列表为空数组
        deleteTip:''
    }

    componentDidMount() {
        let token = window.localStorage.getItem("token")
        axios({
            method: "get",
            url: `http://playground.it266.com/article?token=${token}`,
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            data: qs.stringify({ 'page': this.state.page, 'page_size': this.state.page_size }),
        }).then((response) => {
            console.log(response) //服务器响应的数据
            console.log("文章新增成功")
            this.setState({
                articles: response.data.data.articles
            })
            console.log(this.state.articles)

        }).catch((error) => {
            // alert("出错了")
        })
    }

    deleteClick = (e) => { 
        console.log(e);
        let token = window.localStorage.getItem("token")
        axios({
            method: "post",
            url: `http://playground.it266.com/article/delete?token=${token}`,
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            data: qs.stringify({ 'id': e,}),
        }).then((response) => {
            console.log(response) //服务器响应的数据
            if(response.data.status===true){
                alert("删除成功")
                this.componentDidMount()
            // this.props.history.push("/article")
            }else{
                this.setState({
                    deleteTip:response.data.data
                })
                console.log(this.state.deleteTip)
            }
            

        }).catch((error) => {
            console.log("出错了",this.state)
            alert("出错了")
        })
    }
    render() {
        return (
            <div className="component-index">
                <h2 >文章管理</h2>
                <Link to="/article/create">新增</Link>
                <table>
                    <tbody>
                        <tr>
                            <th style={{ color: 'red' }}>ID</th>
                            <th>标题</th>
                            <th>时间</th>
                            <th>操作</th>
                        </tr>
                        {/* 在这⾥，循环this.state.articles，输出⽂章列表 */}
                        {this.state.articles.map((item, index) => {
                            return (
                                <tr key={index}>
                                    <td>{item.id}</td>
                                    <td onClick={() => {
                                        console.log(item.id)
                                    }}><Link to={`/article/detail/${item.id}`}>{item.title}</Link></td>
                                    <td>{item.created_at}</td>
                                    <td><Link to={`/article/edit/${item.id}`}>编辑</Link>
                                        <button onClick={() => {this.deleteClick(item.id)}}>删除</button>
                                    </td>
                                </tr>
                            )
                        })}
                    </tbody>
                </table>

            </div>

        )
    }
}
export default Index
```

> **create.js** 新增文章

```
import React, { Component } from "react"
import qs from "qs"
import axios from "axios"
// import {Switch,Route} from "react-router-dom"


class Create extends Component {
    state = {
        title: '',
        content: '',
        createtips:''
    }
    handleClick = () => {
        let token = window.localStorage.getItem("token")

        axios({
            method: "post",
            url: `http://playground.it266.com/article/create?token=${token}`,
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            data: qs.stringify({ 'title': this.state.title, 'content': this.state.content}),
        }).then((response) => {
            console.log(response) //服务器响应的数据
            if (response.data.status===false) {
                this.setState({
                    createtips:response.data.data

                })
                return
            }else(
                window.alert("文章新增成功")
            )
            this.props.history.push("/article")
        }).catch((error) => {
            alert("出错了")
        })
     
    }
    titleChange = (e) => {
        this.setState({
            title: e.target.value,
        })
        console.log(e.target.value);
    }
    contentChange = (e) => {
        this.setState({
            content: e.target.value,
        })
        console.log(e.target.value);
    }
    render() {
        return (
            <div>
                <h2>新增文章</h2>
                <div className="create-tip">{this.state.createtips}</div>
                <div>标题：<input type="text" onChange={this.titleChange} /></div>
                <div>内容：<input type="text" onChange={this.contentChange} /></div>
                <button onClick={this.handleClick}>提交</button>
            </div>

        )
    }
}
export default Create
```

> **detail.js**文章详情

```
import React, { Component } from "react"
import axios from "axios"
// import {Switch,Route} from "react-router-dom"


class Detail extends Component {
    state = {
        title: '',
        content: '',
    }

    componentDidMount() {
        let id = this.props.match.params.id;
        console.log(id);
        let token = window.localStorage.getItem("token")
        axios({
            method: "get",
            url: `http://playground.it266.com/article/detail?token=${token}`,
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            params: { 'id': id },
        }).then((response) => {
            console.log(response) //服务器响应的数据
            console.log("获取成功")
            this.setState({
                title: response.data.article.title,
                content:response.data.article.content,
            })
            console.log(this.state)

        }).catch((error) => {
            console.log(this.state)
            // alert("出错了")
        })
    }
    titleChange=(e)=>{
        this.setState({
            title:e.target.value
        })

    }
    contentChange=(e)=>{
        this.setState({
            content:e.target.value
        })
    }
    handleClick = () => {
        console.log(this.state)
        this.props.history.push("/article")
    }

    render() {
        return (
            <div>
                <h2>文章详情</h2>
                <div>标题：<input type="text" value={`${this.state.title}`}
                onChange={(e)=>{this.titleChange(e)}}
                /></div>
                <div>内容：<input type="text" value={`${this.state.content}`}
                onChange={(e)=>{this.contentChange(e)}}
                /></div>
                <button onClick={this.handleClick}>返回</button>
            </div>

        )
    }
}
export default Detail
```

> **edit.js**文章编辑

```
import React, { Component } from "react"
import axios from "axios"
import qs from "qs"
// import {Switch,Route} from "react-router-dom"


class Edit extends Component {
    state = {
        title: '',
        content: '',
        editTip:'',
    }

    componentDidMount() {
        let id = this.props.match.params.id;
        console.log(id);
        let token = window.localStorage.getItem("token")
        axios({
            method: "get",
            url: `http://playground.it266.com/article/detail?token=${token}`,
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            params: { 'id': id },
        }).then((response) => {
            console.log(response) //服务器响应的数据
            console.log("获取成功")
            this.setState({
                title: response.data.article.title,
                content:response.data.article.content,
            })
            console.log(this.state)

        }).catch((error) => {
            console.log(this.state)
            // alert("出错了")
        })
    }
    titleChange=(e)=>{
        this.setState({
            title:e.target.value
        })

    }
    contentChange=(e)=>{
        this.setState({
            content:e.target.value
        })
    }
    handleClick = () => {
        console.log(this.state)
        
        let id = this.props.match.params.id;
        console.log(id);
        let token = window.localStorage.getItem("token")
        axios({
            method: "post",
            url: `http://playground.it266.com/article/update?token=${token}`,
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            data: qs.stringify({ 'id': id,'title':this.state.title,'content':this.state.content,}),
        }).then((response) => {
            console.log(response) //服务器响应的数据
            if(response.data.status===true){
            console.log("编辑成功")
            this.props.history.push("/article")
          
            }else{
                this.setState({
                    editTip:response.data.data
                })
                console.log(this.state.editTip)
            }
            

        }).catch((error) => {
            console.log("出错了",this.state)
            // alert()
        })
    }

    render() {
        return (
            <div>
                <h2>编辑</h2>
                <div>{this.state.editTip}</div>
                <div>标题：<input type="text" value={`${this.state.title}`}
                onChange={(e)=>{this.titleChange(e)}}
                /></div>
                <div>内容：<input type="text" value={`${this.state.content}`}
                onChange={(e)=>{this.contentChange(e)}}
                /></div>
                <button onClick={this.handleClick}>提交</button>
            </div>

        )
    }
}
export default Edit
```

## 路由分页与点击

```
import React, { Component } from "react"
import { Link } from "react-router-dom"
import axios from "axios"
import qs from "qs"
import "./index.css"


class Index extends Component {
    state = {
        articles: [], //默认⽂章列表为空数组
        page: "1",
        page_size: "5",
        deleteTip: '',//错误信息

        searchTitle: '',
        searchCreatedBegin: '',
        searchCreatedEnd: '',



        itemCount: '', //共有多少条数据
        currentPage: '', //当前是第⼏⻚
        pageSize: '', //每⻚多少条数据
    }
    showPage = () => {
        let pagetal = Math.ceil(this.state.itemCount / this.state.pageSize)
        let numbers = []
        for (let i = 1; i <= pagetal; i++) {
            numbers.push(<span
                key={i}
                className={this.state.currentPage === i ? 'numbers-demo' : "numbers"}

                onClick={() => {
                    this.setState({ page: i }
                        , this.getData)

                    console.log(this.state.page)
                }}
            >{i}</span>)
        }
        // console.log(numbers)
        return numbers
    }
    componentDidMount() {
        // if (maxpage > Math.ceil(this.state.itemCount / this.state.page_size)) {
        //     maxpage = Math.ceil(this.state.itemCount / this.state.page_size)
        //     this.setState({
        //         page: maxpage
        //     })
        // } else (
        //     maxpage = this.state.page
        // )
        this.getData()
    }
    getData = () => {

        let token = window.localStorage.getItem("token")
        axios({
            method: "get",
            url: `http://playground.it266.com/article?token=${token}`,
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            params: {
                'page': this.state.page,
                'page_size': this.state.page_size,

                'title': this.state.searchTitle,
                'created_begin': this.state.searchCreatedBegin,
                'created_end': this.state.searchCreatedEnd,
            },
        }).then((response) => {
            console.log(response) //服务器响应的数据
            console.log("文章新增成功")
            this.setState({
                articles: response.data.data.articles,
                itemCount: response.data.data.page.itemCount,
                currentPage: response.data.data.page.currentPage,
                pageSize: response.data.data.page.pageSize,
            })
            console.log(this.state.articles)
        }).catch((error) => {
            // alert("出错了")
        })
    }

    deleteClick = (e) => {
        console.log(e);
        let token = window.localStorage.getItem("token")
        axios({
            method: "post",
            url: `http://playground.it266.com/article/delete?token=${token}`,
            headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
            data: qs.stringify({ 'id': e, }),
        }).then((response) => {
             console.log(response) //服务器响应的数据
            if (response.data.status === true) {
                alert("删除成功")
                this.componentDidMount()
                // this.props.history.push("/article")
            } else {
                this.setState({
                    deleteTip: response.data.data
                })
                console.log(this.state.deleteTip)
            }


        }).catch((error) => {
            console.log("出错了", this.state)
            alert("出错了")
        })
    }
    pageChange = (e) => {
        // eslint-disable-next-line eqeqeq
        if (isNaN(e.target.value) == true) {
            return
        }
        let pagetal = Math.ceil(this.state.itemCount / this.state.page_size)
        if (e.target.value > pagetal) {
            e.target.value = pagetal
        }

        this.setState({
            page: e.target.value
        })
    }
    pageKeypress = (e) => {
        // eslint-disable-next-line eqeqeq
        if (isNaN(e.target.value) == true) {
            return
        }
        console.log(e.charCode)
        if (e.charCode === 13) {

            let pagetal = Math.ceil(this.state.itemCount / this.state.pageSize)
            if (e.target.value > pagetal) {
                e.target.value = pagetal

            }
            this.setState({
                page: e.target.value
            }, () => { this.componentDidMount() })

        }
    }
    pageSizeChange = (e) => {

        // eslint-disable-next-line eqeqeq
        if (isNaN(e.target.value) == true) {
            return
        }
        let pagetal = Math.ceil(this.state.itemCount / this.state.page)

        if (e.target.value > pagetal - 1) {
            e.target.value = pagetal
        }
        this.setState({
            page_size: e.target.value
        })
    }
    pageSizeKeypress = (e) => {
        // eslint-disable-next-line eqeqeq
        if (e.target.value == '') {
            return
        }
        // eslint-disable-next-line eqeqeq
        if (isNaN(e.target.value) == true) {
            return
        }
        if (e.target.value)
            // eslint-disable-next-line eqeqeq
            if (e.target.value == 0) {
                return
            }

        if (e.charCode === 13) {
            this.getData()
        }
    }

    render() {
        return (
            <div className="component-index">
                <h2 >文章管理</h2>
                <div style={{ display: 'flex', justifyContent: 'left', width: 'auto', }}>
                    <input type='text' className='search' placeholder='标题' value={this.state.searchTitle}
                        onChange={(e) => { this.setState({ searchTitle: e.target.value }) }} />
                    <input type='text' className='search' placeholder='开始时间' value={this.state.searchCreatedBegin}
                        onChange={(e) => { this.setState({ searchCreatedBegin: e.target.value }) }}
                    />
                    <input type='text' className='search' placeholder='结束时间' value={this.state.searchCreatedEnd}
                        onChange={(e) => { this.setState({ searchCreatedEnd: e.target.value }) }}
                    />
                    <button className='search searchbtn'
                        onClick={() => {
                            this.getData()
                            console.log(this.state.searchCreatedBegin)
                        }

                        }
                    >搜索</button><button className='search searchbtn'
                        onClick={() => {
                            this.setState({ searchTitle: '', searchCreatedBegin: '', searchCreatedEnd: '' }, this.getData)

                        }}

                    >重置</button>
                    <Link
                        style={{
                            padding: '5px 20px'
                            , color: 'blue', borderRadius: '5px'
                            , backgroundColor: "rgb(227,243,254)"
                        }}
                        to="/article/create">新增</Link>
                    <Link to="/home"
                        style={{
                            padding: '5px 20px'
                            , color: 'blue', borderRadius: '5px'
                            , backgroundColor: "rgb(227,243,254)"
                        }}>返回</Link>
                </div>
                <div>{this.state.deleteTip}</div>
                <table>
                    <tbody>
                        <tr>
                            <th style={{ color: 'red' }}>ID</th>
                            <th>标题</th>
                            <th>时间</th>
                            <th>操作</th>
                        </tr>
                        {/* 在这⾥，循环this.state.articles，输出⽂章列表 */}
                        {this.state.articles.map((item, index) => {
                            return (
                                <tr key={index}>
                                    <td>{item.id}</td>
                                    <td onClick={() => {
                                        console.log(item.id)
                                    }}><Link to={`/article/detail/${item.id}`}>{item.title}</Link></td>
                                    <td>{item.created_at}</td>
                                    <td><Link to={`/article/edit/${item.id}`} style={{
                                        padding: '5px 10px'
                                        , color: 'blue', borderRadius: '5px'
                                        , backgroundColor: "rgb(227,243,254)",
                                        border: 'none'
                                    }}>编辑</Link>
                                        <button onClick={() => { this.deleteClick(item.id) }}
                                            style={{
                                                padding: '5px 10px'
                                                , color: 'blue', borderRadius: '5px'
                                                , backgroundColor: "rgb(227,243,254)",
                                                border: 'none'
                                            }}>删除</button>
                                    </td>
                                </tr>
                            )
                        })}
                    </tbody>
                </table>
                <div>
                    <span style={{ margin: '10px' }}>跳转到<input value={this.state.page} style={{ width: '30px', }} type="text"
                        onChange={(e) => { this.pageChange(e) }}
                        onKeyPress={(e) => { this.pageKeypress(e) }}
                    />页</span>
                    <span style={{ margin: '10px' }}>每页<input value={this.state.page_size} style={{ width: '20px', }} type="text"
                        onChange={(e) => { this.pageSizeChange(e) }}
                        onKeyPress={(e) => { this.pageSizeKeypress(e) }}
                    />条</span>
                </div>
                <div>
                    <span style={{ margin: '10px' }}>共{this.state.itemCount}条</span>
                    <span style={{ margin: '10px' }}>现在{this.state.currentPage}页</span>
                    <span style={{ margin: '10px' }}>每⻚{this.state.pageSize}条</span>
                </div>
                <div>
                    {
                        this.showPage()

                    }<span className="numbers"
                        onClick={() => {
                            // eslint-disable-next-line eqeqeq
                            if (this.state.page == '' || this.state.page_size == '') {
                                this.setState({
                                    page:this.state.currentPage,page_size:this.state.pageSize
                                },this.getData)
                                return
                            }
                            let pagetal = parseInt(this.state.page) + 1
                            if (Math.ceil(this.state.itemCount / this.state.pageSize) < pagetal) {
                                pagetal = Math.ceil(this.state.itemCount / this.state.pageSize)
                            }
                            this.setState({ page: pagetal }, this.getData)
                            this.showPage()
                        }} >下一页 </span>
                    <span className="numbers"
                        onClick={() => {
                            // eslint-disable-next-line eqeqeq
                            if (this.state.page == '' || this.state.page_size == '') {
                                this.setState({
                                    page:this.state.currentPage,page_size:this.state.pageSize
                                },this.getData)
                                return
                            }
                            let pagetal = parseInt(this.state.page) - 1
                            if (1 > pagetal) {
                                pagetal = 1
                            }
                            this.setState({ page: pagetal }, this.getData)
                            this.showPage()
                        }
                        }


                    >上一页 </span>
                </div>
                <div>
                    <select onChange={(e) => {
                        if (this.state.itemCount < 15) {
                            this.setState({
                                page: 1
                            }, this.getData)

                        }
                        console.log(e.target.value)
                        this.setState({
                            page_size: e.target.value,
                            pageSize: e.target.value
                        }, this.getData)
                    }}>
                        <option value='5'>每页5条</option>
                        <option value='10'>每页10条</option>
                        <option value='15'>每页15条</option>
                    </select>
                </div>
            </div>

        )
    }
}
export default Index
```



## 跨组件通讯

### 父子组件示例

app组件

```
import React from "react";
import { HashRouter, Switch, Route } from "react-router-dom";

import "./app.css"


import Home from "./pages/home"
import Article from "./pages/article"
import Top from "./components/top"
import Login from "./pages/login"
import Member from "./pages/member"


class App extends React.Component {
    state={nickname:""}
    setNickname=(val)=>{
        this.setState({nickname:val})
    }

    render() {
        return (
            <HashRouter>
                <Top nickname={this.state.nickname} ></Top>
                <Switch>
                    <Route exact path="/" component={Home} ></Route>
                    <Route path="/article" component={Article}></Route>
                    <Route path="/member" component={Member}></Route>
                    <Route path="/login" ><Login setNickname={this.setNickname}></Login></Route>
                </Switch>
            </HashRouter>

        )
    }
}
export default App
```

top组件

```
import React from "react";
import "./index.css"
import { Link } from "react-router-dom";

class Top extends React.Component{
    state={nickname:""}
    componentDidMount=()=>{
        let val=window.localStorage.getItem("nickname")
        if(val){
            this.setState({
                nickname:val
            })

        }

     
    }


    render(){
        return(
            <div className="Nav">
                {this.props.nickname?
                <div>当前用户：{this.props.nickname} <span>退出</span></div>
                    :
                <div className="pleaseLogin"><Link to="/login" >请登录</Link></div>
                }
               
                <ul>
                    <li><Link to="/">首页展示</Link></li>
                    <li><Link to="/article">文章管理</Link></li>
                    <li><Link to="/member">会员管理</Link></li>
                </ul>
            </div>
        )
    }
}
export default Top
```

login组件

```
// 导入react
import React, { Component } from 'react';
//导入各种运行场景，浏览器
// import Leftback from './imgs/leftback.png'
import "./index.css"
// import axios from "axios"
// import qs from "qs"
//⾃定义组件
import {withRouter} from 'react-router-dom'


class Login extends Component {
    state = {
        nickname: '',
        password: ''
    }
    render() {
        return (
            <div className="login">
                <div className="loginTop"><span><h1>登录界面</h1></span>
                <span><button
                onClick={()=>{
                //ajax
                window.localStorage.setItem("nickname",this.state.nickname)
                this.props.setNickname(this.state.nickname)
                this.props.history.push("/")

                }}
                >提交</button></span></div>
               
                <div>账号:<input className="userInput"
                    value={this.state.nickname}
                    onChange={(e) => { this.setState({ nickname: e.target.value }) }} />
                </div>

                <div>密码:<input className="userInput" type="password"
                    value={this.state.password}
                    onChange={(e) => { this.setState({ password: e.target.value }) }} /></div>

            </div>
        )
    }
}






export default withRouter(Login)

```





### Context上下文

provider 提供者，Consumer消费者

provider 提供者

```
//导出  上下文 等于定义一个特殊的组件
export const AuthContext = React.createContext({
    user:null
    avatar:''
 })

class App extends React.Component {
    state={user:null}
        
    setUser=(val)=>{
        this.setState({user:val})
    }
    render() {
        return (
            
            <AuthContext.Provider value={{user:this.state.user}}>
                
                
            <HashRouter>            {/*HashRouter路由组件*/}
                <Switch>            {/*Switch切换组件*/}
                    <Route exact path="/" component={Login}></Route>
                    <Route  path="/home" component={Home}></Route>
                    <Route path="/article" component={Article}></Route>
                </Switch>
            </HashRouter>
                
                
            </AuthContext.Provider>
        )
    }
}


export default app 
```

Consumer消费者  top

```
import  {AuthContext} from "../app"//导入提供者

class top extends React.Component {
    render() {
       
            <AuthContext.Consume>
                {(value)=>{
                     return (
                         <div>
                             {value.user?<div>当前用户:{value.user.nikename}<span>退出</span> </div>
                                 :<div><Link to="/login">请登录</Link></div>
                                 
                             }
                         console.log(value)
                         </div>
                     )
                }}
            
            </AuthContext.Consumer>
    
    }
}

export default top
```

login

```
<button onClick={()=>{
    
    this.props.setNickname(this.state.nickname)
}}>login
    </button>优点，反应迅速，不需要网页刷新  缺点，当面对嵌套较深的组件，需要层层传递
```

### 上下文传递函数

```
import React from "react";
import { HashRouter, Switch, Route } from "react-router-dom";

import "./app.css"


// import Home from "./pages/home"
import Article from "./pages/article"
// import Top from "./components/top"

// import Member from "./pages/member"
import Login from "./pages/login"
import Register from "./pages/register"
import Profile from "./pages/profile"



let nickname = window.localStorage.getItem("nickname")


//导出数据
export const AuthContext = React.createContext({
    user: null,
   
    setUser: () => { },
})

class App extends React.Component {
    constructor(props) {//会在组件初始化的时候自动执行
        //props是自带得属性     
        //继承App这个方法
        super(props);
        this.setUser = (u) => {
            // this.setState({ auth: { user: u , setUser: this.setUser} })
            this.setState({ auth: { ...this.state.auth, user: u } })
        }
        this.state = {
            auth: {
                // eslint-disable-next-line eqeqeq
                user: {
                    id: '',
                    token: '',
                    mobile: '',
                    // eslint-disable-next-line eqeqeq
                    nickname: nickname ?   nickname  : '无',
                },

                setUser: this.setUser
            }
        }
    }


    render() {
        return (
            <AuthContext.Provider value={this.state.auth}>
                <HashRouter>
                    {/* <Top></Top> */}
                    <Switch>
                        {/* <Route exact path="/" component={Home} ></Route> */}
                        {/* 
                        <Route path="/member" component={Member}></Route> */}


                        {/* <Route path="/login" ><Login setUser={this.setUser}></Login></Route> */}
                        {/* <Route path="/login" ><Login setUser={this.setUser}></Login></Route> */}
                        <Route exact path="/" ><Login></Login></Route>
                        <Route path="/profile" ><Profile></Profile></Route>
                        <Route path="/register" ><Register></Register></Route>
                        <Route path="/article" component={Article}></Route>

                    </Switch>
                </HashRouter>
            </AuthContext.Provider>

        )
    }



}
export default App
```

[官方文档](https://links.jianshu.com/go?to=https%3A%2F%2Freact.docschina.org%2Fdocs%2Fcontext.html) 的demo已经很棒了。但我觉得我的描述会让你更容易理解。

##### 1.Context

Context 通过组件树提供了一个传递数据的方法，从而避免了在每一个层级手动的传递 props 属性。 有部分小伙伴应该使用props属性进行组件向下传值的操作。当多个组件嵌套时候。你就需要慢慢向上寻找最初的值是什么~(手动微笑,恶心吧 )

##### 2.API (个人大白话理解)

**React.createContext：**创建一个上下文的容器(组件), defaultValue可以设置共享的默认数据



```
const {Provider, Consumer} = React.createContext(defaultValue);
```

**Provider(生产者)**: 和他的名字一样。用于生产共享数据的地方。生产什么呢？ 那就看value定义的是什么了。value:放置共享的数据。



```
<Provider value={/*共享的数据*/}>
    /*里面可以渲染对应的内容*/
</Provider>
```

**Consumer(消费者)**:这个可以理解为消费者。 他是专门消费供应商(**Provider** 上面提到的)产生数据。Consumer需要嵌套在生产者下面。才能通过回调的方式拿到共享的数据源。当然也可以单独使用，那就只能消费到上文提到的defaultValue



```
<Consumer>
  {value => /*根据上下文  进行渲染相应内容*/}
</Consumer>
```

##### 3.react脚手架快速搭建

命令行按顺序执行以下代码：

```
npm install -g create-react-app`
 `create-react-app demo`
 `yarn start
```

##### 4.demo





在上面 脚手架添加 son.js 、grandson.js 并修改App.js内容。项目结构自行调整：

![img](https:////upload-images.jianshu.io/upload_images/7078301-ec199f70c77b42a1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/506/format/webp)

项目结构.jpg

代码效果图：

![img](https:////upload-images.jianshu.io/upload_images/7078301-a244e49439dd8f47.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/713/format/webp)

demo效果图.png

1. App.js 父组件

```
//App.js
import React from 'react';
import Son from './son';//引入子组件
// 创建一个 theme Context,
export const {Provider,Consumer} = React.createContext("默认名称");
export default class App extends React.Component {
    render() {
        let name ="小人头"
        return (
            //Provider共享容器 接收一个name属性
            <Provider value={name}>
                <div style={{border:'1px solid red',width:'30%',margin:'50px auto',textAlign:'center'}}>
                    <p>父组件定义的值:{name}</p>
                    <Son />
                </div>
            </Provider>
        );
    }
}
```

son.js 子组件

```
//son.js 子类
import React from 'react';
import { Consumer } from "./App.js";//引入父组件的Consumer容器
import Grandson from "./grandson.js";//引入子组件
function Son(props) {
    return (
        //Consumer容器,可以拿到上文传递下来的name属性,并可以展示对应的值
        <Consumer>
            {( name ) =>
                <div style={{ border: '1px solid blue', width: '60%', margin: '20px auto', textAlign: 'center' }}>
                    <p>子组件。获取父组件的值:{name}</p>
                    {/* 孙组件内容 */}
                    <Grandson />
               </div>
            }
        </Consumer>
    );
}
export default Son;
```

grandson.js 孙组件

```
//grandson.js 孙类
import React from 'react';
import { Consumer } from "./App.js";//引入父组件的Consumer容器
function Grandson(props) {
    return (
         //Consumer容器,可以拿到上文传递下来的name属性,并可以展示对应的值
        <Consumer>
            {(name ) =>
                   <div style={{border:'1px solid green',width:'60%',margin:'50px auto',textAlign:'center'}}>
                   <p>孙组件。获取传递下来的值:{name}</p>
               </div>
            }
        </Consumer>
    );
}
export default Grandson;
```

## mock.js与Hook!

https://github.com/nuysoft/Mock/wiki/Mock.mock()

https://zh-hans.reactjs.org/docs/hooks-state.html

### mockjs

https://github.com/nuysoft/Mock/wiki/Mock.mock()

Mock.js 是一款模拟数据生成器，旨在帮助前端攻城师独立于后端进行开发，帮助编写单元测试。提供了以下模拟功能：

- 根据数据模板生成模拟数据
- 模拟 Ajax 请求，生成并返回模拟数据
- 基于 HTML 模板生成模拟数据

```
安装   npm  install  mockjs  --save
//url
//参数
//返回数据
//文章列表
//page page_size
{
	statue:true,
	date:[
		{id:1,title:"标题一"}
		{id:2,title:"标题二"}
	]
}
import Mock from "mockjs"

Mock.mock('/api/article','get',{
    status:true,
    date:[
        {id:1,title:"标题一"}
		{id:2,title:"标题二"}
    ]
})
import Mock from "mockjs"
			//rurl路径			rtype类型  template模板
Mock.mock(/\/api\/article\/create/,'post',{
    status:true,
    data:"新增成功"
})

Mock.mock(/\/api\/article.*/,'get',{
    status:true,
    date:[
        {id:1,title:"标题一"}
		{id:2,title:"标题二"}
    ]
    
})
```

### hook

https://zh-hans.reactjs.org/docs/hooks-intro.html

**Hook 是一些可以让你在函数组件里“钩入” React state 及生命周期等特性的函数。Hook 不能在 class 组件中使用 —— 这使得你不使用 class 也能使用 React。（我们[不推荐](https://zh-hans.reactjs.org/docs/hooks-intro.html#gradual-adoption-strategy)把你已有的组件全部重写，但是你可以在新组件里开始使用 Hook。）**

#### 声明多个 state 变量

将 state 变量声明为一对 `[something, setSomething]` 也很方便，因为如果我们想使用多个 state 变量，它允许我们给不同的 state 变量取不同的名称：

```
function ExampleWithManyStates() {
  // 声明多个 state 变量！
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}

//在以上组件中，我们有局部变量 age，fruit 和 todos，并且我们可以单独更新它们：

 function handleOrangeClick() {
    // 和 this.setState({ fruit: 'orange' }) 类似
    setFruit('orange');
  }
Hook 就是 JavaScript 函数，但是使用它们会有两个额外的规则：

只能在函数最外层调用 Hook。不要在循环、条件判断或者子函数中调用。
只能在 React 的函数组件中调用 Hook。不要在其他 JavaScript 函数中调用。（还有一个地方可以调用 Hook —— 就是自定义的 Hook 中，我们稍后会学习到。）
```

#### 总结

```
 1:  import React, { useState } from 'react'; 2:
 3:  function Example() {
 4:    const [count, setCount] = useState(0); 5:
 6:    return (
 7:      <div>
 8:        <p>You clicked {count} times</p>
 9:        <button onClick={() => setCount(count + 1)}>10:         Click me
11:        </button>
12:      </div>
13:    );
14:  }
第一行: 引入 React 中的 useState Hook。它让我们在函数组件中存储内部 state。
第四行: 在 Example 组件内部，我们通过调用 useState Hook 声明了一个新的 state 变量。它返回一对值给到我们命名的变量上。我们把变量命名为 count，因为它存储的是点击次数。我们通过传 0 作为 useState 唯一的参数来将其初始化为 0。第二个返回的值本身就是一个函数。它让我们可以更新 count 的值，所以我们叫它 setCount。
第九行: 当用户点击按钮后，我们传递一个新的值给 setCount。React 会重新渲染 Example 组件，并把最新的 count 传给它。
const [fruit, setFruit] = useState('banana');
```

这种 JavaScript 语法叫[数组解构](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring)。它意味着我们同时创建了 `fruit` 和 `setFruit` 两个变量，`fruit` 的值为 `useState` 返回的第一个值，`setFruit` 是返回的第二个值。它等价于下面的代码：

```
var fruitStateVariable = useState('banana'); // 返回一个有两个元素的数组
var fruit = fruitStateVariable[0]; // 数组里的第一个值
var setFruit = fruitStateVariable[1]; // 数组里的第二个值
```

**hook更新对象**

与 class 组件中的 `setState` 方法不同，`useState` 不会自动合并更新对象。你可以用函数式的 `setState` 结合展开运算符来达到合并更新对象的效果。

```
const [state, setState] = useState({});
setState(prevState => {
  // 也可以使用 Object.assign
  return {...prevState, ...updatedValues};
});
```

`useReducer` 是另一种可选方案，它更适合用于管理包含多个子值的 state 对象。

**注意**

与 class 组件中的 `setState` 方法不同，`useState` 不会自动合并更新对象。你可以用函数式的 `setState` 结合展开运算符来达到合并更新对象的效果。

```
const [state, setState] = useState({});
setState(prevState => {
  // 也可以使用 Object.assign
  return {...prevState, ...updatedValues};
});
```

`useReducer` 是另一种可选方案，它更适合用于管理包含多个子值的 state 对象。

### 类变函数式组件

```
import React,{useEffect,useState} from 'react';
import axios from "axios"

function Article(){
    //变量名类似state 用于修改变量的方法类似setState
    let [articleList,setArticleList] = useState([])
    
    //相当于挂载  当页面切走时触发
    useEffect (()=>{
        
        axios.get('/api/article',{
            params:{
                page:1,
            }
        }).then((res)=>{
            setArticleList(res.data.data)
        })
        
        //return()=>{                  相当于取消挂载 
           // console.log("成功切换页面")
        //}
        
    },[])   //deps:[]依赖  依赖里面的内容修改时 useEffect内的内容会重新执行
 
    return(
        <>
            <h3>文章管理页面</h3>
            <ul>
                {articleList.map(item =>{
                    return<li key={item.id}>{item.title}</li>
                })}
            </ul>
        </>
    )
}

export default Article
```

## mock与hook示例

### Mock

> 生成随机数据，拦截Ajax请求

**创建mock**

> ./pages/mocks/aricle

```
//npm install mockjs --save   //安装mockjs

import Mock from "mockjs"


Mock.mock(/\/api\/article\/create/,'post',{
        state:true,
        data:"新增成功"
    })


// Mock.mock('/api/article?page=1','get',{
Mock.mock(/\/api\/article.*/,'get',{
    state:true,
    data:[
        {id:1,title:"标题1"},
        {id:2,title:"标题2"},
        {id:3,title:"标题3"},
    ]
})
```

**父组件导入**

> app.js

```
import "./pages/mocks/aricle"
```

**子组件内调用**

> ./pages/article

```
import React ,{ Component }from "react"
import "./index.css"
import {Link} from "react-router-dom"
import axios from "axios"

class Article extends Component{
    componentDidMount(){
        axios.get(
            '/api/article',
            {
                params:{
                    page:1
                }
            }).then((res)=>{
                console.log(res.data.data)
        })
        axios.post(
            '/api/article/create',
        ).then((res)=>{
            console.log(res.data.data)
        })
    }

    render(){
        return(
            <div className="page">
                <div> <h1>文章详情</h1><Link to="/profile">退出</Link></div>
                <div className="page-text">11月8日0—24时，31个省（自治区、直辖市）和新疆生产
                </div>
            
             </div>  
        )
    }
}
export default Article
```

### hook

```
import React, {useState,useEffect} from "react"

import "./index.css"

import { Link } from "react-router-dom"
import axios from "axios"

//hook可以简化代码让逻辑更加清晰
//1、类组件改造为函数组件，顶部{Component}换成{useState,useEffect}
function Article() {
    //2、用hook里面useState()的方法代state()，let[a,b]解构useState([])
    let [articleList, setArticleList] = useState([])

    useEffect(() => {
        axios.get(
            '/api/article',
            {
                params: {
                    page: 1
                }
            }).then((res) => {
                // console.log(res.data.data)
                setArticleList(res.data.data)
            })

            
            return()=>{
                console.log('切走了')
            }
            //离开的时候return

         }, [])//3、等于DidMount，空数组是它的依赖，必须给数组
         //依赖里面变量发生改变，代码会被执行执行，比如每页显示多少条的，会重新执行
    return (
        <div className="page">
            <div> <h1>文章管理页面</h1><Link to="/profile">退出</Link></div>
            <ul>
                {
                    articleList.map(item => {
                        return <li key={item.id}>{item.title}</li>
                    })
                }
            </ul>
        </div>
    )
}

export default Article
```

## Hook结合上下文

### 父组件

```
import "./app.css"

import { HashRouter, Switch, Route } from "react-router-dom";
import Head from "./compoents/Head";

import React, {useState,useEffect} from "react"
export const AuthContext = React.createContext()

//导入上下文组件

function App(props) {
    const [auth,setAuth]=useState([
        {id:1,name:"213213123"},
        {id:2,name:"1111111111"},
        {id:3,name:"33333333333"}
    ])
    useEffect(()=>{

        console.log(auth)
        return()=>{

        }

    },[auth])
    return (
        // 导出生产者方便组件之间的通信
        <AuthContext.Provider value={{auth,setAuth}}>
            <HashRouter>
                <Head></Head>
                <Switch>
                    <Route exact path="/" ><Head></Head></Route>
                    {/*<Head></Head>*/}
                    {/*<Head></Head>*/}
                </Switch>
            </HashRouter>
        </AuthContext.Provider>

    )
}
export default App;
```

### 子组件

```
import React from "react";
import "./index.css"
// import { Link } from "react-router-dom";
import {withRouter} from 'react-router-dom'
import { AuthContext } from "../../app"


 function Head(props) {

    return (

        <AuthContext.Consumer>
            {(value) => {
                console.log("head",value.auth)
                return (
                    // 顶部横幅样式
                    <div className="head">
                        Head
                    </div>
                )
            }}
        </AuthContext.Consumer>
    )
}
export default withRouter(Head)
```





# 安装基础环境

https://nodejs.org/en/

查询Node版本号

```
node --version
```

切换国内淘宝镜像源

```
npx nrm use taobao
```

创建项目

```
npx create-react-app demo
```

切换目录

```
cd demo
```

打开浏览器

```
npm start
```

安装路由

```
npm install react-router-dom --save
```

安装axios环境

```
npm install axios
```

安装mock

```
npm install mockjs --save
```

# 论坛前端笔记

浏览器信息

```
window.location
```

跳转页面

```
 props.history.push(`./detail/${item.post.id}`)
```

动画效果展开

```
transition: all .4s ease;
overflow:hidden;
transition-property:all; //要执行过渡的属性,如: width
transition-duration:.5s; //执行过渡的时间, 单位为s 秒
transition-timing-function:ease-in; //执行过渡的类型
transition-delay:.1s; //延迟执行过渡的类型
```

头像上传

```
let formData = new FormData()
formData.append('avatar', fileData); // 第一个参数file，由API决定
axios({
method: 'POST',
url: `http://xueba.it266.com:8081/api/upload/avatar?token=${value.token}`,
data: formData,
headers: {
'Content-Type': 'multipart/form-data'
},
timeout: 20000
}).then((res) => {
getData(value)
console.log("图片上传状态", res.data)

}).catch((error) => {
console.log("出错了", error)
// alert("出错了")
})
```

调用函数，生成div

```
let pageBtns=()=>{
        let el=[]
        for (let i=1;i<props.postSearchDto.total;i++){
            el.push(<div>dawdadwa</div>)
        }
        console.log(el)
        return el
    }
```

axios问题

axios是会有延迟，空对像会报错

要预留一个空的对象

```
   const [detail, setDetail] = useState({post:{}})
```

确认删除弹窗

```
 let bool = window.confirm("确认删除")
        if (bool) {
            let id = props.match.params.id;
            let token = window.localStorage.getItem("token")
            axios({
                method: "POST",
                url: `http://xueba.it266.com:8081/api/post/delete?token=${token}`,
                headers: {'Content-Type': 'application/x-www-form-urlencoded'},
                params: {"id": id}
            }).then((response) => {
                if (response.data.code === "SUCCESS") {
                    window.confirm("确认删除")
                    alert("删除成功", response.data)
                    props.history.replace("../")
                } else {
                    alert(response.data.message)
                }

            }).catch((error) => {
                alert("出错了")
            })
// eslint-disable-line
```



# ant-react项目构建

### **初始化项目**

```
#创建一个新的ant-react项目
$ rimraf node_modules
$ npm init react-app ant-react
#安装axios,路由
$ npm install axios react-router-dom --save
$ d install react-router@5 react-router-dom@5
```

**清理文件**

> src/

```
#删除src目录下的logo.svg,reportWebVitals.js和setuoTests.js
#app.js只留下最外层div
#清空所有样式 ---app.css,index.css
#index.html 
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

> public/留下favicon.ico—index.html—robots.txt三个文件
>
> public/index.html

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8"/>
    <!--头像信息-->
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
    <meta name="theme-color" content="#000000"/>

    <!--描述信息后面可以改-->
    <!--<meta-->
    <!--        name="description"-->
    <!--        content="Web site created using create-react-app"-->
    <!--/>-->
    <title>标题</title>
</head>
<body>
<noscript>You need to enable JavaScript to run this app.</noscript>
<div id="root"></div>
</body>
</html>
```

### normalize.css

> ant design中使用less.css

```
#安装normalize.css
npm install normalize.css
#index.js 加入 
#import 'normalize.css'
$ npm i -S craco-less --force
```

## [Ant Design配置](https://ant.design/index-cn)

```she
#安装Ant Design配置
$ npm install antd --save
```

修改 `src/App.js`，引入 antd 的按钮组件。

```shell
import React from 'react';
import { Button } from 'antd';
import './App.css';

const App = () => (
  <div className="App">
    <Button type="primary">Button</Button>
  </div>
);

export default App;
```

**安装sass**

```
$ npm install node-sass@npm:dart-sass  -–save
```

> 新建scss文件,并编辑

- 可以多层嵌套
- 可以定义变量

```json
.App {
  .demo {
    background: black;
  }
}
```

**引入less**

```
$ npm install @craco/craco craco-less --save
```

```shell
#如果报错
$ npm i -S craco-less --force
npm i @craco\craco@7.0.0-alpha.3
```

**修改 `package.json` 里的 `scripts` 属性。**

```shell
/* package.json */
"scripts": {
-   "start": "react-scripts start",
-   "build": "react-scripts build",
-   "test": "react-scripts test",
+   "start": "craco start",
+   "build": "craco build",
+   "test": "craco test",
}
```

**然后在项目根目录创建一个 `craco.config.js` 用于修改默认配置。**

```shell
/* craco.config.js */
module.exports = {
  // ...
};
```



### 自定义主题[#](https://ant.design/docs/react/use-with-create-react-app-cn#自定义主题)

按照 [配置主题](https://ant.design/docs/react/customize-theme-cn) 的要求，自定义主题需要用到类似 [less-loader](https://github.com/webpack-contrib/less-loader/) 提供的 less 变量覆盖功能。我们可以引入 [craco-less](https://github.com/DocSpring/craco-less) 来帮助加载 less 样式和修改变量。

首先把 `src/App.css` 文件修改为 `src/App.less`，然后修改样式引用为 less 文件。

```
/* src/App.js */
- import './App.css';
+ import './App.less';
/* src/App.less */
- @import '~antd/dist/antd.css';
+ @import '~antd/dist/antd.less';
```

**修改 `craco.config.js` 文件如下。**

```shell
const CracoLessPlugin = require('craco-less');


module.exports = {
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { '@primary-color': '#1DA57A' },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
};
```

## 精简教程

```shell
#创建一个新的ant-react项目,删除不需要文件
#$ npm init create-react-app cashier-frontend
$ npx create-react-app cashier-frontend
#安装axios,路由,antd
$ npm install  axios  --save
$ npm install  antd 
$ npm install  react-router-dom  --save
```

```shell
$ 不用
#安装normalize.css
#npm install normalize.css
#index.js 加入 
#import 'normalize.css'
#$ npm i -S craco-less --force
```

```shell
#配置全局less环境
$ npm install -g less
```

```shell
#引入less
$ npm install @craco/craco craco-less  --legacy-peer-deps --save
```

```shell	
/* package.json */
"scripts": {
-   "start": "react-scripts start",
-   "build": "react-scripts build",
-   "test": "react-scripts test",
   "start": "craco start",
   "build": "craco build",
   "test": "craco test",
}
```

```js
/* src/App.less */
- @import '~antd/dist/antd.css';
@import '~antd/dist/antd.less';
```

```js
/*App.js */
import React from 'react';
import { Button } from 'antd';
import './App.less';

const App = () => (
  <div className="App">
    <Button type="primary">Button</Button>
  </div>
);

export default App;
```

```js
/*craco.config.js*/
const CracoLessPlugin = require('craco-less');

module.exports = {
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { '@primary-color': '#1DA57A' },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
};
/*
@primary-color: #1890ff; // 全局主色
@link-color: #1890ff; // 链接色
@success-color: #52c41a; // 成功色
@warning-color: #faad14; // 警告色
@error-color: #f5222d; // 错误色
@font-size-base: 14px; // 主字号
@heading-color: rgba(0, 0, 0, 0.85); // 标题色
@text-color: rgba(0, 0, 0, 0.65); // 主文本色
@text-color-secondary: rgba(0, 0, 0, 0.45); // 次文本色
@disabled-color: rgba(0, 0, 0, 0.25); // 失效色
@border-radius-base: 2px; // 组件/浮层圆角
@border-color-base: #d9d9d9; // 边框色
@box-shadow-base: 0 3px 6px -4px rgba(0, 0, 0, 0.12), 0 6px 16px 0 rgba(0, 0, 0, 0.08),
  0 9px 28px 8px rgba(0, 0, 0, 0.05); // 浮层阴影
*/
```

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8"/>
    <!--头像信息-->
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico"/>
    <meta name="viewport" content="width=device-width, initial-scale=1"/>
    <meta name="theme-color" content="#000000"/>

    <!--描述信息后面可以改-->
    <!--<meta-->
    <!--        name="description"-->
    <!--        content="Web site created using create-react-app"-->
    <!--/>-->
    <title>标题</title>
</head>
<body>
<noscript>You need to enable JavaScript to run this app.</noscript>
<div id="root"></div>
</body>
</html>
```

```
使用npm时，报错：npm WARN config global `--global`, `--local` are deprecated. Use `--location=global` instead.

我找到了一篇帖子，他是对的，怕那个提问帖子过期，我抄下来了。如下：

将npm升级到最新版本即可
升级方法
1.在windows中以管理员身份打开cmd，然后执行命令
npm install -g npm-windows-upgrade
2.更改脚本策略
下载Windows Power Shell
然后以管理员身份运行，执行命令
set-ExecutionPolicy RemoteSigned
输入Y
成功更改脚本策略
3.在Windows Power Shell上运行命令
npm-windows-upgrade
```

