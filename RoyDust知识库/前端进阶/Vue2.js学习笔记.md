# Vue.js学习笔记

![92846013_p0](https://s2.loli.net/2021/12/04/7ucKgHiGzsnDSZp.jpg)

Vue 的核心库只关注视图层，方便与第三方库或既有项目整合。

HTML + CSS + JS : 视图 ： `给用户看，刷新后台给的数据`

网络通信 ： axios

页面跳转 ： vue-router

状态管理：vuex

Vue-UI : ICE , Element UI

1. VUE 概述
    Vue (读音/vju/, 类似于view)是一套用于构建用户界面的渐进式框架，发布于2014年2月。与其它大型框架不同的是，Vue被设计为可以自底向上逐层应用。Vue的核心库只关注视图层，不仅易于上手，还便于与第三方库(如: vue-router: 跳转，vue-resource: 通信，vuex:管理)或既有项目整合
2. 前端三要素
    HTML (结构) :超文本标记语言(Hyper Text Markup Language) ，决定网页的结构和内容
    CSS (表现) :层叠样式表(Cascading Style sheets) ，设定网页的表现样式
    JavaScript (行为) :是一种弱类型脚本语言，其源代码不需经过编译，而是由浏览器解释运行,用于控制网页的行为
3. JavaScript框架
    jQuery: 大家熟知的JavaScript框架，优点是简化了DOM操作，缺点是DOM操作太频繁,影响前端性能;在前端眼里使用它仅仅是为了兼容IE6、7、8;

**Angular:** Google收购的前端框架，由一群Java程序员开发，其特点是将后台的MVC模式搬到了前端并增加了模块化开发的理念，与微软合作，采用TypeScript语法开发;对后台程序员友好，对前端程序员不太友好;最大的缺点是版本迭代不合理(如: 1代-> 2代，除了名字，基本就是两个东西;截止发表博客时已推出了Angular6)

**React:** Facebook出品，一款高性能的JS前端框架;特点是提出了新概念[虚拟DOM]用于减少真实DOM操作，在内存中模拟DOM操作，有效的提升了前端渲染效率;缺点是使用复杂，因为需要额外学习一门[JSX] 语言;

**Vue:**一款渐进式JavaScript框架，所谓渐进式就是逐步实现新特性的意思，如实现模块化开发、路由、状态管理等新特性。其特点是综合了Angular (模块化)和React (虚拟DOM)的优点;

**Axios :**前端通信框架;因为Vue 的边界很明确，就是为了处理DOM,所以并不具备通信能力，此时就需要额外使用一个通信框架与服务器交互;当然也可以直接选择使用jQuery提供的AJAX通信功能;

前端三大框架：Angular、React、Vue

# ES6语法

#### 1.不一样的变量声明：const和let

ES6推荐使用let声明局部变量，相比之前的var（无论声明在何处，都会被视为声明在函数的最顶部）
 let和var声明的区别：

```jsx
var x = '全局变量';
{
  let x = '局部变量';
  console.log(x); // 局部变量
}
console.log(x); // 全局变量
```

```html
<body>
  <button>按钮1</button>
  <button>按钮2</button>
  <button>按钮3</button>
  <button>按钮4</button>
  <button>按钮5</button>
  <script>
    // 变量作用域:变量在什么位置内是可用的
    // ES5之前因为if和for都没有块级作用域的概念，所以在很多时候，我们都必须借助于function的作月域来解决应用外面变量的问题
    // 闭包可以解决这个问题: 函数是一个作用域
    // ES6中加入了let,let它是有if和for块级作用域

    // ES5语法
    // var btns = document.getElementsByTagName('button');
    // for(var i = 0; i<btns.length; i++){
    //   (function(num){
    //     bnts[num].addEventListener('click',function(){
    //       console.log('第'+num+'个按钮被点击');
    //     })
    //   })(i)
    // }

    // ES6语法
    const btns = document.getElementsByTagName('button')
    for (let i = 1; i < btns.length; i++) {
      btns[i].addEventListener('click', function () {
        console.log('第' + i + '个按钮被点击');
      })
    }
  </script>
</body>
```

let表示声明变量，而const表示声明常量，两者都为块级作用域；

const 声明的变量都会被认为是常量，意思就是它的值被设置完成后就不能再修改了，且const定义标识符时，必须赋值：

**建议:**在ES6开发中,优先使用const,只有需要改变某一个标识符的时候才使用let。

```cpp
const a = 1
a = 0 //报错
```

如果const的是一个对象，对象所包含的值（内部属性）是可以被修改的。抽象一点儿说，就是对象所指向的地址没有变就行：

```csharp
const student = { name: 'cc' }

student.name = 'yy';// 不报错
student  = { name: 'yy' };// 报错
```

有几个点需要注意：

> - let 关键词声明的变量不具备变量提升（hoisting）特性
> - let 和 const 声明只在最靠近的一个块中（花括号内）有效
> - 当使用常量 const 声明时，请使用大写变量，如：CAPITAL_CASING
> - const 在声明时必须被赋值

#### 2.模板字符串

在ES6之前，我们往往这么处理模板字符串：
 通过“\”和“+”来构建模板

```jsx
$("body").html("This demonstrates the output of HTML \
content to the page, including student's\
" + name + ", " + seatNumber + ", " + sex + " and so on.");
```

而对ES6来说

1. 基本的字符串格式化。将表达式嵌入字符串中进行拼接。用${}来界定；
2. ES6反引号(``)直接搞定；

```jsx
$("body").html(`This demonstrates the output of HTML content to the page, 
including student's ${name}, ${seatNumber}, ${sex} and so on.`);
```

#### 3.箭头函数（Arrow Functions）

> ES6 中，箭头函数就是函数的一种简写形式，使用括号包裹参数，跟随一个 =>，紧接着是函数体；

箭头函数最直观的三个特点。

> - 不需要 function 关键字来创建函数
> - 省略 return 关键字
> - 继承当前上下文的 this 关键字

```jsx
// ES5
var add = function (a, b) {
    return a + b;
};
// 使用箭头函数
var add = (a, b) => a + b;

// ES5
[1,2,3].map((function(x){
    return x + 1;
}).bind(this));
    
// 使用箭头函数
[1,2,3].map(x => x + 1);
```

> 细节：当你的函数有且仅有一个参数的时候，是可以省略掉括号的。当你函数返回有且仅有一个表达式的时候可以省略{} 和 return；

#### 4. 函数的参数默认值

在ES6之前，我们往往这样定义参数的默认值：

```jsx
// ES6之前，当未传入参数时，text = 'default'；
function printText(text) {
    text = text || 'default';
    console.log(text);
}

// ES6；
function printText(text = 'default') {
    console.log(text);
}

printText('hello'); // hello
printText();// default
```

#### 5.Spread / Rest 操作符

> Spread / Rest 操作符指的是 ...，具体是 Spread 还是 Rest 需要看上下文语境。

当被用于迭代器中时，它是一个 Spread 操作符：

```jsx
function foo(x,y,z) {
  console.log(x,y,z);
}
 
let arr = [1,2,3];
foo(...arr); // 1 2 3
```

当被用于函数传参时，是一个 Rest 操作符：当被用于函数传参时，是一个 Rest 操作符：

```jsx
function foo(...args) {
  console.log(args);
}
foo( 1, 2, 3, 4, 5); // [1, 2, 3, 4, 5]
```

#### 6.二进制和八进制字面量

> ES6 支持二进制和八进制的字面量，通过在数字前面添加 0o 或者0O 即可将其转换为八进制值：

```jsx
let oValue = 0o10;
console.log(oValue); // 8
 
let bValue = 0b10; // 二进制使用 `0b` 或者 `0B`
console.log(bValue); // 2
```

#### 7.对象和数组解构

```jsx
// 对象
const student = {
    name: 'Sam',
    age: 22,
    sex: '男'
}
// 数组
// const student = ['Sam', 22, '男'];

// ES5；
const name = student.name;
const age = student.age;
const sex = student.sex;
console.log(name + ' --- ' + age + ' --- ' + sex);

// ES6
const { name, age, sex } = student;
console.log(name + ' --- ' + age + ' --- ' + sex);
```

#### 8.对象超类

ES6 允许在对象中使用 super 方法：

```jsx
var parent = {
  foo() {
    console.log("Hello from the Parent");
  }
}
 
var child = {
  foo() {
    super.foo();
    console.log("Hello from the Child");
  }
}
 
Object.setPrototypeOf(child, parent);
child.foo(); // Hello from the Parent
             // Hello from the Child
```

#### 9.for...of 和 for...in

for...of 用于遍历一个迭代器，如数组：

```jsx
let letters = ['a', 'b', 'c'];
letters.size = 3;
for (let letter of letters) {
  console.log(letter);
}
// 结果: a, b, c
```

for...in 用来遍历对象中的属性：

```jsx
 let stus = ["Sam", "22", "男"];
 for (let stu in stus) {
   console.log(stus[stu]);
  }
// 结果: Sam, 22, 男
```

#### 10.ES6中的类

ES6 中支持 class 语法，不过，ES6的class不是新的对象继承模型，它只是原型链的语法糖表现形式。

函数中使用 static 关键词定义构造函数的的方法和属性：

```jsx
class Student {
  constructor() {
    console.log("I'm a student.");
  }
 
  study() {
    console.log('study!');
  }
 
  static read() {
    console.log("Reading Now.");
  }
}
 
console.log(typeof Student); // function
let stu = new Student(); // "I'm a student."
stu.study(); // "study!"
stu.read(); // "Reading Now."
```

类中的继承和超集：

```jsx
class Phone {
  constructor() {
    console.log("I'm a phone.");
  }
}
 
class MI extends Phone {
  constructor() {
    super();
    console.log("I'm a phone designed by xiaomi");
  }
}
 
let mi8 = new MI();
```

> extends 允许一个子类继承父类，需要注意的是，子类的constructor 函数中需要执行 super() 函数。
>  当然，你也可以在子类方法中调用父类的方法，如super.parentMethodName()。
>  在 这里 阅读更多关于类的介绍。

> 有几点值得注意的是：
>
> - 类的声明不会提升（hoisting)，如果你要使用某个 Class，那你必须在使用之前定义它，否则会抛出一个 ReferenceError 的错误
> - 在类中定义函数不需要使用 function 关键词

# 1、基本认识vue

- 轻量级，体积小是一个重要指标。Vue.js 压缩后有只有 20多kb （Angular 压缩后 56kb+，React 压缩后 44kb+）
- 移动优先。更适合移动端，比如移动端的 Touch 事件
- 易上手，学习曲线平稳，文档齐全
- 吸取了 Angular（模块化）和 React（虚拟 DOM）的长处，并拥有自己独特的功能，如：计算属性
- Vue是一个渐进式的框架可以将Vue作为你应用的一 部分嵌入其中,带来更丰富的交互体验。
- 开源，社区活跃度高
- Vue有很多特点和Web开发中常见的高级功能
  - 解耦视图和数据.
  - 可复用的组件
  - 前端路由技术
  - 状态管理
  - 虚拟DOM

**下载地址**：

- 开发版本
  包含完整的警告和调试模式：https://vuejs.org/js/vue.js
  删除了警告，30.96KB min + gzip：https://vuejs.org/js/vue.min.js
- CDN

```html
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
```

- NPM安装

 **初识vue.js**

```html
<body>
    
    <div id="app">{{message}}</div> //执行到这里显然出对应的HTML

    <script src="../js/vue.js"></script>
    <script>
        //执行这里创建Vue实例,并且对原HTML进行解析和修改。
        //编程范式：声明式编程
        const app = new Vue({   //创建Vue实例
            el:'#app',   //用于指定要挂载的元素
            data:{       //定义数据
                message:"洛依尘！"
            }
        })
        //元素js的做法(编程范式:命令式编程)
        // 1.创建div元素,设置id属性
        // 2.定义一个变量叫message
        // 3.将message变量放在前面的div元素中显示
    </script>
</body>
```

## **MVVM 模式**

MVVM 源自于经典的 Model–View–Controller（MVC）模式（期间还演化出了 Model-View-Presenter（MVP）模式，可忽略不计）。MVVM 的出现促进了 GUI 前端开发与后端业务逻辑的分离，极大地提高了前端开发效率。MVVM 的核心是 ViewModel 层，它就像是一个中转站（value converter），负责转换 Model 中的数据对象来让数据变得更容易管理和使用，该层向上与视图层进行双向数据绑定，向下与 Model 层通过接口请求进行数据交互，起呈上启下作用。

如下图所示：

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/882926-20171115175942921-775941263.png)

简单画了一张图来说明 MVVM 的各个组成部分：

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/882926-20171115175958671-1955710845.png)

分层设计一直是软件架构的主流设计思想之一，MVVM 也不例外。

### View 层

View 是视图层，也就是用户界面。前端主要由 HTML 和 CSS 来构建，为了更方便地展现 ViewModel 或者 Model 层的数据，已经产生了各种各样的前后端模板语言，比如 FreeMarker、Marko、Pug、Jinja2等等，各大 MVVM 框架如 KnockoutJS，Vue，Angular 等也都有自己用来构建用户界面的内置模板语言。

### Model 层

Model 是指数据模型，泛指后端进行的各种业务逻辑处理和数据操控，主要围绕数据库系统展开。后端的处理通常会非常复杂

###  ViewModel 层

ViewModel 是由前端开发人员组织生成和维护的视图数据层。在这一层，前端开发者对从后端获取的 Model 数据进行转换处理，做二次封装，以生成符合 View 层使用预期的视图数据模型。**需要注意的是 ViewModel 所封装出来的数据模型包括视图的状态和行为两部分，而 Model 层的数据模型是只包含状态的，比如页面的这一块展示什么，那一块展示什么这些都属于视图状态（展示），而页面加载进来时发生什么，点击这一块发生什么，这一块滚动时发生什么这些都属于视图行为（交互），视图状态和行为都封装在了 ViewModel 里。这样的封装使得 ViewModel 可以完整地去描述 View 层。**由于实现了双向绑定，ViewModel 的内容会实时展现在 View 层，这是激动人心的，因为前端开发者再也不必低效又麻烦地通过操纵 DOM 去更新视图，MVVM 框架已经把最脏最累的一块做好了，我们开发者只需要处理和维护 ViewModel，更新数据视图就会自动得到相应更新，真正实现数据驱动开发。看到了吧，View 层展现的不是 Model 层的数据，而是 ViewModel 的数据，由 ViewModel 负责与 Model 层交互，这就完全解耦了 View 层和 Model 层，这个解耦是至关重要的，它是前后端分离方案实施的重要一环。

![image-20210508173816636](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210508173816636.png)

## Vue实例的options

- **el:**
  类型 : string | HTMLElement
  作用 : 决定之后Vue实例会管理哪一个DOM。
- data:
  类型 : Object | Function (组件当中data必须是一个函数)
  作用 : Vue实例对应的数据对象。
- **methods:**
  类型 : { [key: string]: Function }
  作用 : 定义属于Vue的一 些方法，可以在其他地方调用,也可以在指令中使用。

## vue实例的生命周期

**一、解析**

**1、什么是生命周期：从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期！**

 

**2、生命周期钩子 = 生命周期函数 = 生命周期事件**

 

**3、主要的生命周期函数分类：**

\- 创建期间的生命周期函数：

  \+ beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性

  \+ created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板

  \+ beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中

  \+ mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示

 

 \- 运行期间的生命周期函数：

 \+ beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点

 \+ updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！

 

 \- 销毁期间的生命周期函数：

 \+ beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。

 \+ destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

```html
<body>
  <div id="app">
    <input type="button" value="修改msg" @click="msg='No'">
    <h3 id="h3">{{ msg }}</h3>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        msg: 'ok'
      },
      methods: {
        show() {
          console.log('执行了show方法')
        }
      },
      beforeCreate() { // 这是我们遇到的第一个生命周期函数，表示实例完全被创建出来之前，会执行它
        console.log(this.msg)
        this.show()
        // 注意： 在 beforeCreate 生命周期函数执行的时候，data 和 methods 中的 数据都还没有没初始化
      },
      created() { // 这是遇到的第二个生命周期函数
        console.log(this.msg)
        this.show()
        //  在 created 中，data 和 methods 都已经被初始化好了！
        // 如果要调用 methods 中的方法，或者操作 data 中的数据，最早，只能在 created 中操作
      },
      beforeMount() { // 这是遇到的第3个生命周期函数，表示 模板已经在内存中编辑完成了，但是尚未把 模板渲染到 页面中
        console.log(document.getElementById('h3').innerText)
        // 在 beforeMount 执行的时候，页面中的元素，还没有被真正替换过来，只是之前写的一些模板字符串
      },
      mounted() { // 这是遇到的第4个生命周期函数，表示，内存中的模板，已经真实的挂载到了页面中，用户已经可以看到渲染好的页面了
        console.log(document.getElementById('h3').innerText)
        // 注意： mounted 是 实例创建期间的最后一个生命周期函数，当执行完 mounted 就表示，实例已经被完全创建好了，此时，如果没有其它操作的话，这个实例，就静静的 躺在我们的内存中，一动不动
      },


      // 接下来的是运行中的两个事件
      beforeUpdate() { // 这时候，表示 我们的界面还没有被更新【数据被更新了吗？  数据肯定被更新了】
        console.log('界面上元素的内容：' + document.getElementById('h3').innerText)
        console.log('data 中的 msg 数据是：' + this.msg) 
        // 得出结论： 当执行 beforeUpdate 的时候，页面中的显示的数据，还是旧的，此时 data 数据是最新的，页面尚未和 最新的数据保持同步
      },
      updated() {
        console.log('界面上元素的内容：' + document.getElementById('h3').innerText)
        console.log('data 中的 msg 数据是：' + this.msg)
        // updated 事件执行的时候，页面和 data 数据已经保持同步了，都是最新的
      }
    });
  </script>
</body>
```

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/20200815191941397.png)

# 2、基本语法

## 1、插值操作

**Mustache语法**

```html
<div id="app">
	<h2>{{massage}}</h2>
  <h2>{{massage}},洛依尘</h2>
  <h2>{{firstName+lastName}}</h2>
  <h2>{{firstName+' '+lastName}}</h2>
  <h2>{{counter*2}}</h2>
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好",
        firstName:"kobe",
        lastName:"bryant",
        counter:200
			}
		})
	</script>
</body>
```

**v-once指令**

> 该指令后面不需要跟任何表达式(比如之前的v-for后面是由跟表达式的
>
> 该指令表示元素和组件(组件后面才会学习)只渲染- 次,不会随着数据的改变而改变

```html
<h2 v-once>{{massage}}</h2>
```

**v-html**

> 该指令后面往往会跟上一个string类型
> 会将string的html解析出来并且进行渲染

```html
	<h2>{{url}}</h2>  <!-- <a href="www.baidu.com">百度一下</a> -->
	<h2 v-html="url"></h2>  <!-- 百度一下 -->
```

**v-text**

> 都是用于将数据显示在界面中，但是通常只接受一个string类型

```html
	<h2 v-text="massage">,洛依尘</h2>	<!--你好-->
```

**v-pre**

> 用于跳过这个元素和它子元素的编译过程,用于显示原本的Mustache语法

```html
	<h2 v-pre>{{massage}}</h2> <!-- {{massage}} -->
```

**v-cloak**

> 在某些情况下,f防止浏览器可能会直接显然出未编译的Mustache标签。

```html
<style>
		[v-cloak] {
			display: none;
		}
	</style>
</head>

<div id="app" v-cloak>
	<h2>{{massage}}</h2>
	<h2 v-once>{{massage}}</h2>
	<h2>{{url}}</h2> <!-- <a href="www.baidu.com">百度一下</a> -->
	<h2 v-html="url"></h2> <!-- 	百度一下 -->
	<h2 v-text="massage">,洛依尘</h2>
	<!--你好-->
	<h2 v-pre>{{massage}}</h2> <!-- {{massage}} -->
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		//在vue解析之前，div里有一个属性c-cloak
		//在vue解析之后，div里没有一个属性c-cloak
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好",
				url: '<a href="www.baidu.com">百度一下</a>'
			}
		})
	</script>
</body>
```

## 2、绑定属性

**v-bind**

> v-bind用于绑定一个或多个属性值,或者向另-一个组件传递props值

```html
<div id="app">
    
  <!-- <img src="{{imgURL}}" alt=""> -->
  <!--  错误的用法:这里不可以使用mustache语法-->
    
  <!-- 正确用法：使用v-band指令 -->
  <a v-bind:href="aHref">百度</a>
  <img v-bind:src='imgURL' alt="" >

  <!-- 语法糖的写法 -->
  <a :href="aHref">百度</a>
  <img :src='imgURL' alt="" >
    
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好",
        imgURL:'https://www.baidu.com/img/PCtm_d9c8750bed0b3c7d089fa7d55720d6cf.png',
        aHref:"https://www.baidu.com/"
			}
		})
	</script>
</body>
```

**v-bind 动态绑定class（对象语法）**

- 可以通过{ }绑定一个类
- 也可以通过判断，传入多个值
- 和普通类同时存在，并不冲突
- 如果过于复杂，可以放在一个methods或者computed中

```html
<style>
    .active{
      color: red;
    }
  </style>
</head>

<div id="app">
	<!-- <h2 class="active">{{massage}}</h2>
  <h2 :class="active">{{massage}}</h2> -->
  
  <!-- <h2 :class="{类名1:ture,类名2:boolean}">{{massage}}</h2> 对class对象进行选择-->
  <h2 v-bind:class="{active: isActive , line: isLine}">{{massage}}</h2>   
  <!-- 将内容放在一个methods里，并调用 -->
  <h2 v-bind:class="getClasses()">{{massage}}</h2>   
  <button v-on:click="bntClick">按钮</button>
  <!-- 监听按钮，使用bntClick方法 -->
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好",
        active:'active',
        isActive:true,  //设置boolean值决定是否启用
        isLine:true
			},
      methods:{
        bntClick: function(){
          this.isActive=!this.isActive
        },
        getClasses:function(){
          return {active: this.isActive, line: this.isLine}
        }
      }
		})
	</script>
</body>
```

**v-bind 动态绑定class（数组语法）**

```html

<div id="app">
  <!-- 如果在[]数组里的元素加了引号，代表他是一个字符串，而不是引用一个变量 -->
  <h2 :class="[active,line]">{{massage}}</h2>
  <h2 :class="['active','line']">{{massage}}</h2>
  <h2 :class="getClasses()">{{massage}}</h2>
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好",
        active:"aaa",
        line:"bbb"
			},
      methods:{
        getClasses:function(){
          return [this.active,this.line]
        }
      }
		})
	</script>
</body>
```

**小作业：**点击列表中的哪一项, 那么该项的文字变成红色

```html
<style>
		.active {
			color: red;
		}
	</style>
</head>

<div id="app">
	<ul>
		<li v-for="(item, index) in movies" :class="{active: currentIndex === index}" @click="liClick(index)">
            <!-- {active: currentIndex === index}当currentIndex === index为true时，改变颜色  -->
			{{index}}.{{item}}
		</li>
	</ul>
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				movies: ['海王', '火影忍者', '进击的巨人', '死神'],
				currentIndex: 0
			},
			methods: {
				liClick(index) {
					this.currentIndex = index
				}
			}
		})
	</script>
</body>
```

**v-bind 绑定style**

```html
<div id="app">
	<!-- <h2 :style="{key(属性名):value(属性值)}">{{massage}}</h2> -->

  <!-- 这里要加' '要不然vue会去解析50px这个变量然后报错 -->
  <h2 :style="{fontSize: '50px'}">{{massage}}</h2>
  
  <!-- finalSize当成一个变量在使用 -->
  <h2 :style="{fontSize: finalSize}">{{massage}}</h2>

  <!-- 也可以拼接 -->
  <h2 :style="{fontSize: finalSize + 'px',color:finalColor}">{{massage}}</h2>

  <!-- 数组语法 -->
  <h2 :style="[baseStyle,baseStyle1]">{{massage}}</h2>
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好",
        finalSize: 100,
        finalColor: 'red',
        baseStyle:{color:'red'},
        baseStyle1:{fontSize:'75px'}
			}
		})
	</script>
</body>
```

## 3、计算属性

**一、什么是计算属性**

　　模板内的表达式非常便利，但是设计它们的初衷是用于**简单运算的**。在模板中放入太多的逻辑会让模板过重且难以维护。

**二、计算属性的用法**

　　在一个计算属性里可以完成各种复杂的逻辑，包括运算、函数调用等，只要最终返回一个结果就可以。

```html
<div id="app">
	<h2>{{firstName+' '+lastName}}</h2>
  <h2>{{fullName}}</h2>
  <h2>总价格:{{totalPrice}}</h2>
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				firstName:"luo",
        lastName:"yichen",
        books:[
          {id:100, name: 'java核心技术' , price:100},
          {id:101, name: 'c核心技术' , price:100},
          {id:102, name: 'php核心技术' , price:100},
          {id:103, name: 'python核心技术' , price:100}
        ]
			},
      // computed: 计算属性()
      computed:{
        fullName:function(){
          return this.firstName+' '+this.lastName
        },
        totalPrice:function(){
          let result =0
          for (let i=0;i < this.books.length; i++){
            result += this.books[i].price
          }
          return result;
        }
      }
		})
	</script>
```

**计算属性的getter和setter**

每个计算属性都包含一个getter和一个setter

- 在上面的例子中,我们只是使用getter来读取。
- 在某些情况下,你也可以提供一个setter方法 (不常用)。
- 在需要写setter的时候,代码如下: .

 ```HTML
<div id="app">
  <h2>{{fullName}}</h2>
</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        firstName: "luo",
        lastName: "yichen",
      },
      computed: {
        // fullName: function () {
        //   return this.firstName + ' ' + this.lastName
        // }
        // 计算属性一般没有set值，只读属性。
        fullName:{
          set: function(newValue){
            const names = newValue.split(" ");
            this.firstName = names[0];
            this.lastName = names[1];
          }, 
          get: function(){
            return this.firstName + ' ' + this.lastName
          }
        },
        // 简洁写法
        // fullName:function(){
        //   return this.firstName+' '+this.lastName
        // }
      }
    })
  </script>
</body>
 ```

**计算属性与methods对比**

```html
<div id="app">
  <!-- 通过拼接：语法过于繁琐 -->
  <h2>{{firstName}} {{lastName}}</h2>
  <!-- 通过定义methods 每次都要调用-->
  <h2>{{getFullName()}}</h2>
  <!-- 通过computed 如果没有发生改变只需要调用一次-->
  <h2>{{fullName}}</h2>
</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        firstName: "luo",
        lastName: "yichen"
      },
      methods: {
        getFullName: function () {
          return this.firstName + ' ' + this.lastName
        }
      },
      computed: {
        fullName: function () {
          return this.firstName + ' ' + this.lastName
        }
      }
    })
  </script>
</body>
```

## 4、事件监听

> 可以用 `v-on` 指令监听 DOM 事件，并在触发时运行一些 JavaScript 代码。
>
> 获取到浏览器参数的event对象: $event

```html
<div id="app">
	<h2>{{counter}}</h2>
  <button v-on:click="increment">+</button>
  <button v-on:click="decrement">-</button>
  <!-- 语法糖 当没参数时（）可以不用写 -->
  <button @click="increment">+</button>
  <button @click="decrement">-</button>

  <!-- 事件调用时没有参数 -->
  <button @click="bnt1Click()">按钮1</button>
  <button @click="bnt1Click">按钮1</button>

  <!-- 在事件定义前，写函数省略了小括号，但是方法本身需要一个参数,这个时候
  Vue会将浏览器默认生成的event事件对象作为参数传入方法中 -->
  <button @click="bnt2Click(123)">按钮2</button> 
  <button @click="bnt2Click()">按钮2</button>
  <button @click="bnt2Click">按钮2</button>

  <!-- 定义方法时，我们需要event对象，同时又需要其他参数 -->
  <!-- 在调用方式时，如何手动的获取到浏览器参数的event对象: $event -->
  <button @click="bnt3Click('abc',$event)">按钮3</button>
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				counter: 0
			},
      methods:{
        increment(){
          this.counter++
        },
        decrement(){
          this.counter--
        },
        bnt1Click(){
          console.log("bnt1Click");
        },
        bnt2Click(abc){
          console.log("--------------",abc);
        },
        bnt3Click(abc,event){
          console.log("++++++++++++++", abc,event);
        }
      }
		})

    // 如果我们函数需要参数，但是没有传入参数，那么函数的形参为undefined
    function abc(name){
      console.log(name);
    }
    abc()
	</script>
</body>
```

### **v-on的修饰符**

> 1. **.stop修饰符的使用**
>
>    当多对标签进行重叠的时候, 你点击最上面的一层标签的时候, 会自动的冒泡到他下面的所有标签上面
>    而`.stop`就是阻止冒泡使用的
>
> 2. **.prevent修饰符的使用**
>
>    在`form`表单提交时候或者在点击`a`标签的时候, 会阻止提交或跳转
>
> 3. **.keyup监听某个键盘的键帽**
>
>    监听某个键盘的键位
>
> 4. **.once修饰符的使用**
>
>    绑定后只会触发一次

```html
<div id="app">
  <!-- 1. .stop -->
  <div @click='divClick'>
    aaaaa
    <button @click.stop='bntClick'>按钮</button>
  </div>

  <!-- 2. .prevent  -->
  <form action="baidu">
    <input type="submit" value="提交" @click.prevent='submitClick'>
  </form>

  <!-- 3. 监听某个键盘的键位 -->
  <input type="text" @keyup.enter="keyUp">

  <!-- 4. once修饰符的使用 -->
  <button @click.once='bnt2Click'>按钮</button>
</div>



<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好"
      },
      methods: {
        bntClick() {
          console.log('bnt')
        },
        divClick() {
          console.log('div')
        },
        submitClick() {
          console.log("submitClick")
        },
        keyUp() {
          console.log("up")
        },
        bnt2Click() {
          console.log('bnt2');
        }
      }
    })
  </script>
</body>
```

## 5、条件判断

> v-if的原理：
> 	v-if后面的条件为false时,对应的元素以及其子元素不会渲染。
> 	也就是根本没有不会有对应的标签出现在DOM中。

```html
<div id="app">
  <h2 v-if="score>90">优秀</h2>
  <h2 v-else-if="score>80">良好</h2>
  <h2 v-else-if="score>60">及格</h2>
  <h2 v-else>不及格</h2>

  <h1>{{result}}</h1>

  <h2 v-if="isShow">{{massage}}</h2>
  <h1 v-else>当isShow为false时显示我</h1>

</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好",
        isShow: true,
        score: 99
      },
      computed: {
        result() {
          let showMessage = '';
          if (this.score >= 90) {
            showMessage = "优秀"
          } else if (this.score >= 80) {
            showMessage = "良好"
          }
          // ...
          return showMessage
        }
      }
    })
  </script>
</body>
```

**用户切换的小案例**

```html
<div id="app">
	<span v-if="isUser">
    <label for="username">用户账号</label>
    <input type="text" id="username" placeholder="用户账号" key='username'>
  </span>
  <span v-else>
    <label for="emailname">用户邮箱</label>
    <input type="text" id="emailname" placeholder="用户邮箱" key='emailname'>
  </span>
  <button @click="isUser = !isUser">切换类型</button>
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				isUser:true
			}
		})
	</script>
</body>
```

**小问题:**

- 如果我们在有输入内容的情况下,切换了类型,我们会发现文字依然显示之前的输入的内容。
- 但是按道理讲,我们应该切换到另外一个input元素中了。
- 在另一个input元素中,我们并没有输入内容。
- 为什么会出现这个问题呢?

**问题解答:**

- 这是因为Vue在进行DOM渲染时,出于性能考虑,会尽可能的复用已经存在的元素,而不是重新创建新的元素。
- 在上面的案例中, Vue内部会发现原来的input元素不再使用,直接作为else中的input来使用了.

**解决方案:**

- 如果我们不希望Vue出现类似重复利用的问题,可以给对应的input添加key
- 并且我们需要保证key的不同

### Virtual DOM 是什么？

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/2019-06-26-01.png)

Virtual DOM 其实就是一棵以 JavaScript 对象( VNode 节点)作为基础的树，用对象属性来描述节点，实际上它只是一层对真实 DOM 的抽象。最终可以通过一系列操作使这棵树映射到真实环境上。

简单来说，可以把Virtual DOM 理解为一个简单的JS对象，并且最少包含标签名( tag)、属性(attrs)和子元素对象( children)三个属性。不同的框架对这三个属性的命名会有点差别。

对于虚拟DOM，咱们来看一个简单的实例，就是下图所示的这个，详细的阐述了`模板 → 渲染函数 → 虚拟DOM树 → 真实DOM`的一个过程

![img](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/2019-06-26-02.png)

### Virtual DOM 作用是什么？

**虚拟DOM的最终目标是将虚拟节点渲染到视图上**。但是如果直接使用虚拟节点覆盖旧节点的话，会有很多不必要的DOM操作。例如，一个ul标签下很多个li标签，其中只有一个li有变化，这种情况下如果使用新的ul去替代旧的ul,因为这些不必要的DOM操作而造成了性能上的浪费。

为了避免不必要的DOM操作，虚拟DOM在虚拟节点映射到视图的过程中，将虚拟节点与上一次渲染视图所使用的旧虚拟节点（oldVnode）做对比，找出真正需要更新的节点来进行DOM操作，从而避免操作其他无需改动的DOM。

其实虚拟DOM在Vue.js主要做了两件事：

- 提供与真实DOM节点所对应的虚拟节点vnode
- 将虚拟节点vnode和旧虚拟节点oldVnode进行对比，然后更新视图

### **v-if和v-show的区别**

> v-show控制的是节点的display属性 v-if是将节点删除了 如果节点需要频繁显示隐藏 使用v-show性能更佳！

```html
<div id="app">
  <!-- v-if: 当条件为false时，包含v-if指令的元素，根本就不会存在dom中 -->
  <h2 v-if='isShow' id="aaa">{{massage}}</h2>
  <!-- V- show:当条件为false时，v-show只是给我们的元素添加一个行内样式: display: none -->
  <h2 v-show='isShow' id="bbb">{{massage}}</h2>
</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好",
        isShow: true
      }
    })
  </script>
</body>
```

6、循环遍历

>当我们有一组数据需 要进行渲染时,我们就可以使用v-for来完成。
>	v-for的语法类似于JavaScript中的for循环。
>	格式如下: item in items的形式。

```html
<div id="app">
  <!-- 1.在遍历的过程中，没有使用索引值（下标值） -->
  <ul>
    <li v-for='item in names'>{{item}}</li>
  </ul>

  <!-- 2.在遍历过程中,获取索引值 -->
  <ul>
    <li v-for='(item,index) in names'>
      {{index+1}}.{{item}}
    </li>
  </ul>

  <!-- 1.在遍历对象的过程中，如果只是获取一个值，那么获取到的是value -->
  <ul>
    <li v-for="item in info">{{item}}</li>
  </ul>
  <!-- 2.， 获取key和value 格式(value,key) -->
  <ul>
    <li v-for="(value,key) in info">{{value}}-{{key}}</li>
  </ul>
  <!-- 3. 获取key和value和index 格式(value,key,index)-->
  <ul>
    <li v-for="(value,key,index) in info">{{value}}-{{key}}-{{index}}</li>
  </ul>
</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        names: ['why', 'who', 'what', 'where']	//遍历数组
      },
      info: {									//遍历对象
        name: 'lyc',
        age: 18,
        height: 1.88
      }
    })
  </script>
</body>
```

### **v-for加key属性**

- 为什么需要这个key属性呢(了解) ?
  - 这个其实和Vue的虚拟DOM的Diff算法有关系。	
  - 这里我们借用React' S diff algorithm中的一张图来简单说明一下:

- 当某一层有很多相同的节点时,也就是列表节点时,我们希望插入一一个新
  的节点
  - 我们希望可以在B和C之间加一一个F , Diff算法默认执行起来是这样的。
  - 即把C更新成F , D更新成C , E更新成D ,最后再插入E ,是不是很没有
    效率?

- 所以我们需要使用key来给每个节点做一个唯一标识

  - Diff算法就可以正确的识别此节点

  - 0找到正确的位置区插入新的节点。

**所以一句话, key的作用主要是为了高效的更新虚拟DOM。**

![image-20210517163534869](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210517163534869.png)

![image-20210517163043021](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210517163043021.png)

### **哪些数组方法是响应式的**

```html
<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        letters: ['A', 'C', 'B', 'D', 'E']
      },
      methods: {
        btnClick() {
          // 1.push()   在数组最后添加元素
          this.letters.push('aaa','bbb')

          // 2.pop()      在数组最后删除一个元素
          this.letters.pop();

          // 3.shift()   删除在数组第一个元素
          this.letters.shift();

          // 4.unshift() 在数组最前面添加元素
          this.letters.unshift('ddd','ddd');

          // 5.splice()   删除/插入/替换元素
          // 删除元素: 第一参数传入你从第几个元素开始删除，第二参数传入你要删除的几个元素(如果没有传,就删除后面所有元素)
          // 插入元素: 第二个传入0，后面跟上要添加的值
          // 替换元素: 第二参数传入你要删除元素，后面追加你要写入的元素完成替换
          this.letters.splice(1,3,'m','n','l')

          // 6.sort()     排序
          this.letters.sort()

          // 7.reverse()  反转
          this.letters.reverse()

          // 注意：通过索引值直接来修改数组中的元素 不是响应式
          // this.letters[0]='bbbbbbbbbbbb'
          // set(要修改的对象，索引值，修改后的值)
          Vue.set(this.letters,0,'bbbbbb')
        }
      }
    })

    // 扩展知识：可变参数
    // function sum(...sum){
    //   console.log(sum);
    // }
    // sum(11,223,44,56,77,889,9,1)
  </script>
</body>
```

## 6、表单绑定

- 表单控件在实际开发中是非常常见的。特别是对于用户信息的提交,需要大量的表单。
- Vue中使用v-model指令来实现表单元素和数据的双向绑定。

```html
<body>

  <div id="app">
    <input type="text" v-model="massage">
    {{massage}}
  </div>

  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好"
      }
    })
  </script>
</body>
```

- 当我们在输入框输入内容时
- 因为input中的v-model绑定了message ,所以会实时将输入的内容传递给message , message发生改变。
- 当message发生改变时,因为上面我们使用Mustache语法,将message的值插入到DOM中,所以DOM会发生响应的改变。
- 所以,通过v-model实现了双向的绑定。

原理：

```html
  <div id="app">
    <!-- <input type="text" v-model="massage"> -->
    <!-- <input type="text" :value="massage" @input="valueChange"> -->
    <input type="text" :value="massage" @input="massage = $event.target.value">
    {{massage}}
  </div>

  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好"
      },
      methods: {
        valueChange(event) {
          this.massage = event.target.value;
        }
      }
    })
  </script>

</body>
```

### v-model结合radio类型

```html
<div id="app">
  <label for="">
    <input type="radio" id="male" value="男" v-model="sex">男
  </label>
  <label for="">
    <input type="radio" id="female" value="女" v-model="sex">女
  </label>
  <h2>{{sex}}</h2>
</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        message: "你好",
        sex:'男'
      }
    })
  </script>
</body>
```

v-model结合checkbox类型

单个勾选框: .

- v-modelI即为布尔值。
- 此时input的value并不影响v-model的值。

多个复选框:

- 多个复选框时,因为可以选中多个,所以对应的data中属性是一个数组。
- 当选中某一个时 ,就会将input的value添加到数组中。

```html
<div id="app">
  <!-- 单选框 -->
  <!-- <label for="agree">
    <input type="checkbox" id="agree" v-model="isAgree">同意协议
  </label>
  <h2>{{isAgree}}</h2>
  <button :disabled="!isAgree">下一步</button> -->

  <!-- 多选框 -->
    <!-- <input type="checkbox" value="篮球" v-model="hobbies">篮球
    <input type="checkbox" value="足球" v-model="hobbies">足球
    <input type="checkbox" value="排球" v-model="hobbies">排球
    <input type="checkbox" value="手球" v-model="hobbies">手球
    <h2>{{hobbies}}</h2> -->

    <label v-for="item in originHobbies" :for="item">
      <input type="checkbox" :value="item" :id="item" v-model="hobbies">{{item}}
    </label>
  </div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        message: "你好",
        isAgree: false,//单选框
        hobbies:[],//多选框 
        originHobbies:['篮球','足球','乒乓球','台球','高尔夫球']
          //也可以通过值绑定来从服务器获取值
      }
    })
  </script>
</body>
```

### v-model结合select

单选:只能选中一个值。

- v-model绑定的是一个值。
- 当我们选中option中的一个时,会将它对应的value赋值到mySelect中

多选:可以选中多个值。

- v-model绑定的是一个数组。
- 当选中多个值时,就会将选中的option对应的value添加到数组mySelects中

```html
<body>

  <div id="app">
    <!-- 1、选择一个 -->
    <select name="abc" id=""  v-model="fruit">
      <option value="苹果">苹果</option>
      <option value="香蕉">香蕉</option>
      <option value="榴莲">榴莲</option>
      <option value="西瓜">西瓜</option>
    </select>
    <h2>{{fruit}}</h2>

    <!-- 2、选择多个 -->
    <select name="abc" id=""  v-model="fruits" multiple>
      <option value="苹果">苹果</option>
      <option value="香蕉">香蕉</option>
      <option value="榴莲">榴莲</option>
      <option value="西瓜">西瓜</option>
    </select>
    <h2>{{fruits}}</h2>
  </div>

    <script src="../js/vue.js"></script>
    <script>
      const app = new Vue({
        el: "#app", 
        data: {
          message: "你好",
          fruit:"香蕉",
          fruits:[]
        }
      })
    </script>

</body>
```

### v-model的修饰符

lazy修饰符:

- 默认情况下, v- model默认是在input事件中同步输入框的数据的。
- 也就是说, 一旦有数据发生改变对应的data中的数据就会自动发生
  改变。
- lazy修饰符可以让数据在失去焦点或者回车时才会更新:

number修饰符:

- 默认情况下,在输入框中无论我们输入的是字母还是数字,都会被
  当做字符串类型进行处理。
- 但是如果我们希望处理的是数字类型,那么最好直接将内容当做数
  字处理。
- number修饰符可以让在输入框中输入的内容自动转成数字类型:

trim修饰符:

- 如果输入的内容首尾有很多空格,通常我们希望将其去除
- trim修饰符可以过滤内容左右两边的空格

```html
<div id="app">
  <!-- 1.修饰符：lazy -->
  <input type="text" v-model.lazy="message">
  <h2>{{message}}</h2>

  <!-- 2.修饰符：number -->
  <input type="number" v-model.number="age">
  <h2>{{typeof age}}</h2>

  <!-- 3.修饰符：trim -->
  <input type="text" v-model.trim="name">
  <h2>{{name}}</h2>
</div>

<body> 
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        message: "你好",
        age:12,
        name:''
      }
    })
  </script>
</body>
```

## 综合-书籍购物车案例

- **HTML**

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="./style.css">

</head>

<body>

  <div id="app">
    <div v-if="books.length">
      <table>
        <thead>
          <tr>
            <th></th>
            <th>书籍名称</th>
            <th> 出版日期</th>
            <th> 价格</th>
            <th> 购买数量</th>
            <th> 操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item,index) in books">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.date}}</td>
            <td>{{item.price | showPrice}}</td>
            <td>
              <button @click="decrement(index)" v-bind:disabled="item.count <= 1">-</button>
              {{item.count}}
              <button @click="increment(index)">+</button>
            </td>
            <td><button @click="removeHandler(index)">移除</button></td>
          </tr>
        </tbody>
      </table>
      <h2>
        总价格: {{totalPrice | showPrice}}
      </h2>
    </div>
    <div v-else>
      <h1>购物车为空</h1>
    </div>
  </div>
  <script src="../js/vue.js"></script>
  <script src="./main.js"></script>
</body>

</html>
```

- **CSS**

```CSS
table{
  border: 1px solid #000;
  border-collapse: collapse;
  border-spacing: 0;
}
th,td{
  padding: 8px 16px;
  border: 1px solid #000;
  text-align: left;
}

th{
  background-color: #f7f7f7;
  color: #5c6b77;
  font-weight: 600;
}
```

- JS

```js
const app = new Vue({
  el: "#app",
  data: {
    books: [{
        id: 1,
        name: '《算法导论》',
        date: "2006-9",
        price: 85.00,
        count: 1
      },
      {
        id: 2,
        name: '《算法导论》',
        date: "2006-9",
        price: 85.00,
        count: 1
      },
      {
        id: 3,
        name: '《算法导论》',
        date: "2006-9",
        price: 85.00,
        count: 1
      },
      {
        id: 4,
        name: '《算法导论》',
        date: "2006-9",
        price: 85.00,
        count: 1
      }
    ]
  },
  methods: {
    // getFinalPrice(price){
    //   return '￥'+price.toFixed(2) //toFixed(2)保留两位小数
    // }
    increment(index) {
      this.books[index].count++
    },
    decrement(index) {
      this.books[index].count--
    },
    removeHandler(index) {
      this.books.splice(index, 1)
    }
  },
  filters: { //过滤器
    showPrice(price) {
      return '￥' + price.toFixed(2)
    }
  },
  computed: {
    totalPrice() {
      let totalPrice = 0;
      for (let i = 0; i < this.books.length; i++) {
        totalPrice += this.books[i].price * this.books[i].count;
      }
      return totalPrice;
    }
  }
})
```

## JS高阶函数

编程范式：命令式编程/声明式编程

编程范式：面向对象编程(第一公民:对象)/函数式编程（第一公民:函数)

**filter/map/reduce**

filter中的回调函数有一个要求：必须返回一个 boolean值

true:当返回true时，函数内部会自动将这次回调的n加入到新的数组中

false:当返回false时，函数内部会过滤掉这次的n

- 基本写法

```js
const nums = [10,20,111,222,444,40,50]

// 1.需求:取出小于100的数字
let newNums = []
for(let n of nums){
  if(n > 100){
    newNums.push(n)
  }
}

// 2.需求：将所有小于160的数字进行转化：全部*2
let new2Nums = []
for(let n of newNums){
  new2Nums.push(n*2)
}

// 3.需求：将所有new2Nums数字相加，得到最终的记过
let total = 0
for(let n of new2Nums){
  total +=n
}
console.log(total)
```

- 高阶写法

```js
const nums = [10,20,111,222,444,40,50]
// 1.filter函数的使用
let newNums = nums.filter(function(n){
  return n<100
})
console.log(newNums)

// 2.map函数的使用
let new2Nums = newNums.map(function(n){
  return n*2
})
console.log(new2Nums)

// 3.reduce函数的使用
// reduce作用对数组中所有的内容进行汇总
let total = new2Nums.reduce(function(preValue,n){
  return preValue + n;
},0)
console.log(total)
// 第一次： revalue 0  n 20
// 第二次： revalue 20 n 40
// 第二次： revalue 60 n 80
// 第二次： revalue 140 n 100
// 240
```

- 高阶综合写法

```js
const nums = [10,20,111,222,444,40,50]

// 综合
let total = nums.filter(function(n){
  return n<100
}).map(function(n){
  return n*2
}).reduce(function(preValue,n){
  return preValue + n;
},0) //初始化
console.log(total)

//使用箭头函数进一步简化
let total = nums.filter(n => n<100).map(n => n*2).reduce((pre,n) => pre+n)
console.log(total)
```

# 3、组件化开发

## 一、什么是组件化开发

人面对复杂问题的处理方式：
 任何一个人处理信息的逻辑能力都是有限的
 所以，当面对一个非常复杂的问题时，我们不太可能一次性搞定一大堆的内容。
 但是，我们人有一种天生的能力，就是将问题进行拆解。
 如果将一个复杂的问题，拆分成很多个可以处理的小问题，再将其放在整体当中，你会发现大的问题也会迎刃而解。
 组件化也是类似的思想：
 如果我们将一个页面中所有的处理逻辑全部放在一起，处理起来就会变得非常复杂，而且不利于后续的管理以及扩展。
 但如果，我们讲一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能，那么之后整个页面的管理和维护就变得非常容易了。

![img](https:////upload-images.jianshu.io/upload_images/15616626-2469fe9444ce60b9.png?imageMogr2/auto-orient/strip|imageView2/2/w/525/format/webp)

![img](https:////upload-images.jianshu.io/upload_images/15616626-fd069d4c1e180695.png?imageMogr2/auto-orient/strip|imageView2/2/w/172/format/webp)

我们将一个完整的页面分成很多个组件。
 每个组件都用于实现页面的一个功能块。
 而每一个组件又可以进行细分。

## 二、Vue组件化思想

组件化是Vue.js中的重要思想
 它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用。
 任何的应用都会被抽象成一颗组件树。

![img](https:////upload-images.jianshu.io/upload_images/15616626-dcbc0473dbebdba2.png?imageMogr2/auto-orient/strip|imageView2/2/w/630/format/webp)

组件化思想的应用：
 有了组件化的思想，我们在之后的开发中就要充分的利用它。
 尽可能的将页面拆分成一个个小的、可复用的组件。
 这样让我们的代码更加方便组织和管理，并且扩展性也更强。
 所以，组件是Vue开发中，非常重要的一个篇章，要认真学习。

## 三、注册组件的基本步骤

组件的使用分成三个步骤：
 创建组件构造器
 注册组件
 使用组件。
 我们来看看通过代码如何注册组件
 查看运行结果：
 和直接使用一个div看起来并没有什么区别。
 但是我们可以设想，如果很多地方都要显示这样的信息，我们是不是就可以直接使用<my-cpn></my-cpn>来完成呢？

![img](https:////upload-images.jianshu.io/upload_images/15616626-dd7ec5935bc97d63.png?imageMogr2/auto-orient/strip|imageView2/2/w/284/format/webp)

![img](https:////upload-images.jianshu.io/upload_images/15616626-055ae2789a0771c4.png?imageMogr2/auto-orient/strip|imageView2/2/w/427/format/webp)



![img](https:////upload-images.jianshu.io/upload_images/15616626-7983029e8bab5bc1.png?imageMogr2/auto-orient/strip|imageView2/2/w/287/format/webp)

## 四、注册组件步骤解析

这里的步骤都代表什么含义呢？
 1.Vue.extend()：
 调用Vue.extend()创建的是一个组件构造器。
 通常在创建组件构造器时，传入template代表我们自定义组件的模板。
 该模板就是在使用到组件的地方，要显示的HTML代码。
 事实上，这种写法在Vue2.x的文档中几乎已经看不到了，它会直接使用下面我们会讲到的语法糖，但是在很多资料还是会提到这种方式，而且这种方式是学习后面方式的基础。
 2.Vue.component()：
 调用Vue.component()是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称。
 所以需要传递两个参数：1、注册组件的标签名 2、组件构造器
 3.组件必须挂载在某个Vue实例下，否则它不会生效。
 我们来看下面我使用了三次<my-cpn></my-cpn>
 而第三次其实并没有生效：
 第三步的解析

![img](https:////upload-images.jianshu.io/upload_images/15616626-ac35f35e02771f96.png?imageMogr2/auto-orient/strip|imageView2/2/w/1122/format/webp)

```html
<div id="app">
    <my-cpn></my-cpn>
</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    //1.创建组件构造器对象
    const cpnC = Vue.extend({
      template: `
        <div>
          <h2>我是标题</h2>
          <p>我是内容，红红火火恍恍惚惚</p>
          <p>我是内容，红红火火恍恍惚惚</p>
        </div>`
    })

    // 2.注册组件
    Vue.component('my-cpn',cpnC)

    const app = new Vue({
      el: "#app",
      data: {
        message: "你好"
      }
    })
  </script>
</body>
```



## 五、全局组件和局部组件

当我们通过调用Vue.component()注册组件时，组件的注册是全局的
 这意味着该组件可以在任意Vue示例下使用。
 如果我们注册的组件是挂载在某个实例中, 那么就是一个局部组件



![img](https:////upload-images.jianshu.io/upload_images/15616626-0a60523efad51327.png?imageMogr2/auto-orient/strip|imageView2/2/w/486/format/webp)

![img](https:////upload-images.jianshu.io/upload_images/15616626-b5748d756fe3a380.png?imageMogr2/auto-orient/strip|imageView2/2/w/452/format/webp)

```html
<div id="app">
    <cpn></cpn>
</div>
<div id="app2">
  <cpn></cpn>
</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    //1.创建组件构造器对象
    const cpnC = Vue.extend({
      template: `
        <div>
          <h2>我是标题</h2>
          <p>我是内容，红红火火恍恍惚惚</p>
          <p>我是内容，红红火火恍恍惚惚</p>
        </div>`
    })

    // 2.注册组件(全局组件，意味着可以在多个Vue的实力下面使用)
    Vue.component('my-cpn',cpnC)

    const app = new Vue({
      el: "#app",
      data: {
        message: "你好"
      },
      //在Vue实例内注册组件就是局部组件
      components:{
        //cpn使用组件时的标签名
        cpn:cpnC
      }
    })
    
    const app2 = new Vue({
      el: "#app2",
      data: {
        message: "你好"
      }
    })
  </script>
</body>
```

## 六、父子组件

父子组件错误用法:以子标签的形式在Vue实例中使用

- 因为当子组件注册到父组件的components时, Vue会编译好父组件的模块
- 该模板的内容已经决定了父组件将要渲染的HTML (相当于父组件中已经有了子组件中的内容了)
- <child-cpn> </child-cpn>是只能在父组件中被识别的。
- 类似这种用法, <child-cpn> </child-cpn>是会被浏览器忽略的。

```html
<div id="app">
	<cpn1></cpn1>
  <cpn2></cpn2>
</div>

<body>
	<script src="../js/vue.js"></script>
	<script>
    // 1.创建第一个组件构造器(子组件)
    const cpnC1 = Vue.extend({
      template:`
      <div>
      <h2>我是标题</h2>
      <p>我是内容，红红火火恍恍惚惚</p>
      </div>
      `
    })

    // 2.创建第二个组件构造器(父组件)
    const cpnC2 = Vue.extend({
      template:`
      <div>
      <h2>我是标题</h2>
      <p>我是内容，呵呵呵呵呵呵呵呵</p>
      <cpn1></cpn1>
      </div>
      `,
      components:{  //在父组件中注册子组件
        cpn1:cpnC1
      }
    })

    //  可以把Vue当成一个root组件
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好"
			},
      components:{
        cpn2:cpnC2
      }
		})
	</script>
</body>

```

## 七、组件注册语法糖

在上面注册组件的方式,可能会有些繁琐。

- Vue为了简化这个过程,提供了注册的语法糖。
- 主要是省去了调用Vue.extend()的步骤,而是可以直接使用一个对象来代替。

语法糖注册全局组件和局部组件:

```html
<div id="app">
  <cpn1></cpn1>
  <cpn2></cpn2>
</div>

<body>
  <script src="../js/vue.js"></script>
  <script>
    // 1.全局组件注册的语法糖
    // 1.创建组件构造器
    // const cpn1 = Vue.extend({
    //   template:`
    //   <div>
    //   <h2>我是标题</h2>
    //   <p>我是内容，红红火火恍恍惚惚</p>
    //   </div>
    //   `
    // })

    // 2.注册组件
    Vue.component('cpn1', {
      template: `
      <div>
      <h2>我是标题</h2>
      <p>我是内容，红红火火恍恍惚惚</p>
      </div>
      `
    })

    // 注册局部组件的语法糖
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好"
      },
      components: {
        'cpn2': {
          template: `
      <div>
      <h2>我是标题</h2>
      <p>我是内容，呵呵呵呵呵呵呵</p>
      </div>
      `
        }
      }
    })
  </script>
</body>
```

## 八、模板的分离写法

刚才,我们通过语法糖简化了Vue组件的注册过程,另外还有一个地方的写法比较麻烦,就是template模块写法。
如果我们能将其中的HTML分离出来写,然后挂载到对应的组件上,必然结构会变得非常清晰。
Vue提供了两种方案来定义HTML模块内容:

- 使用<script>标签
- 使用<template>标签

```html
div id="app">
	<cpn></cpn>
</div>

<!-- 1.script标题，注意：类型必须是text/x-template -->

<script type="text/x-template" id="cpn">
<div>
  <h2>我是标题</h2>
  <p>我是内容，哈哈哈哈哈哈哈哈哈哈</p>
</div>
</script>

<!-- 2.template标签 -->

<template id="cpn">
  <div>
    <h2>我是标题</h2>
    <p>我是内容，哈哈哈哈哈哈哈哈哈哈</p>
  </div>
</template>

<body>
	<script src="../js/vue.js"></script>
	<script>
    // 2.注册一个全局组件
    Vue.component('cpn',{
      template:'#cpn'
    })

		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好"
			}
		})
	</script>
</body>
```

## 九、组件数据存放问题

 组件是一个单独功能模块的封装: .

- 这个模块有属于自己的HTML模板,也应该有属性自己的数据data。

- 组件不能访问vue实例数据
- 组件应该有自己保存数据的地方

组件自己的数据存放在哪里呢?

- 组件对象也有-个data属性(也可以有methods等属性，下面我们有用到)
- 只是这个data属性必须是-个函数
- 而且这个函数返回-一个对象,对象内部保存着数据

```html
<template id="cpn">
  <div>
    <h2>{{title}}</h2>
    <p>我是内容，哈哈哈哈哈哈哈哈哈哈</p>
  </div>
</template>

<body>
	<script src="../js/vue.js"></script>
	<script>
    // 2.注册一个全局组件
    Vue.component('cpn',{
      template:'#cpn',
			data(){
				return{
					title:'我是'
				}
			}
    })
```

#### 组件中的data为什么是一个函数：

1. vue中组件是用来复用的，为了防止data复用，将其定义为函数。

2. vue组件中的data数据都应该是相互隔离，互不影响的，组件每复用一次，data数据就应该被复制一次，之后，当某一处复用的地方组件内data数据被改变时，其他复用地方组件的data数据不受影响，就需要通过data函数返回一个对象作为组件的状态。

3. 当我们将组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一份新的data，拥有自己的作用域，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。

4. 当我们组件的date单纯的写成对象形式，这些实例用的是同一个构造函数，由于JavaScript的特性所导致，所有的组件实例共用了一个data，就会造成一个变了全都会变的结果。

```html
<!-- 组件实例  -->
<div id="app">
  <cpn></cpn>
  <cpn></cpn>
  <cpn></cpn>
</div>

<template id='cpn'>
  <div>
    <h2>
      当前计数:{{counter}}
    </h2>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
  </div>
</template>

<body>
  <script src="../js/vue.js"></script>
  <script>
    //1.注册组件
    Vue.component('cpn', {
      template: '#cpn',
      // 每次调用都在栈空间内创建一次新对象
      data() {
        return {
          counter: 0
        }
      },
      methods:{
        increment(){
          this.counter++
        },
        decrement(){
          this.counter--
        }
      }
    })

    const app = new Vue({
      el: "#app",
    })
  </script>
</body>
```

## 十、组件之间的通讯

![image-20210531153136273](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210531153136273.png)

但是,在开发中,往往一些数据确实需要从上层传递到下层:

- 比如在一个页面中,我们从服务器请求到了很多的数据。
- 其中一部分数据,并非是我们整个页面的大组件来展示的,而是需要下面的子组件进行展示。
- 这个时候,并不会让子组件再次发送一个网络请求 ,而是直接让大组件(父组件)将数据传递给小组件(子组件)。

### props基本用法

在组件中,使用选项props来声明需要从父级接收到的数据。
props的值有两种方式:

- 方式一 : 字符串数组,数组中的字符串就是传递时的名称。
- 方式二 : 对象,对象可以设置传递时的类型,也可以设置默认值等。

```html
<div id="app">
  <!-- 在引用组件时使用v-bind将子组件的props绑定父组件的数据 -->
	<cpn v-bind:cmovies="movies" :cmessage="massage"></cpn>
</div>

<!-- 组件 -->
<template id="cpn">
  <div>
    <ul>
      <li v-for="item in cmovies">{{item}}</li>
    </ul>
    <h2>{{cmessage}}</h2>
  </div>
</template>

<body>
	<script src="../js/vue.js"></script>
	<script>

    // 创建构造器(子组件)
    // 父传子：props
    const cpn={
      template:'#cpn',
      // 方式一:可以使用数组定义
      // props:['cmovies','cmessage']
        
      props:{
        // 方式二:对象定义
        // 1.类型限制
        // cmovies:Array,
        // cmessage:String,

        // 2.提供一些类型值,默认值,以及必传值
        cmessage:{
          type:String,
          default:'aaaaaa',
          required: true
        },
        // 类型是对象或者数组，默认值必须是一个函数
        cmovies:{
          type:Array,
          // default:[]  //Vue2.5以下
          default(){
            return [];
          }
        }
      }
    }

    //  可以把Vue当成一个root组件
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好",
        movies:['海王','海贼王','海尔兄弟']
			},
      components:{
        cpn
      }
		})
	</script>
</body>
```

![image-20210531180238532](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210531180238532.png)

### 驼峰标识

> HTML 特性是不区分大小写的。所以，当使用的不是字符串模版，camelCased (驼峰式) 命名的 prop 需要转换为相对应的 kebab-case (短横线隔开式)

```html
<div id="app">
	<cpn :c-info="info"></cpn>
</div>

<template id="cpn">
  <h2>{{cInfo}}</h2>
  <!-- 如果要在html中写驼峰命名就要使用短横线隔开 -->
</template>

<body>
	<script src="../js/vue.js"></script>
	<script>

    const cpn ={
      template:'#cpn',
      props:{
        cInfo:{
          type:Object,
          default(){
            return{}
          }
        }
      }
    }

		const app = new Vue({
			el: "#app",
			data: {
				info:{
          name:'lyc',
          age:18,
          height:1.88
        }
			},
      components:{
        cpn
      }
		})
	</script>
</body>
```

## 十一、子组件向父组件传值

- props用于父组件向子组件传递数据,还有一种比较常 见的是子组件传递数据或事件到父组件中。
- 我们应该如何处理呢?这个时候,我们需要使用**自定义事件**来完成。
- 什么时候需要自定义事件呢?
  - 当子组件需要向父组件传递数据时,就要用到自定义事件了。
  - 我们之前学习的v-on不仅仅可以用于监听DOM事件,也可以用于组件间的自定义事件。
- 自定义事件的流程:
  - 在子组件中,通过$emit()来触发事件。
  - 在父组件中,通过v-on来监听子组件事件。

>  子组件发射事件和参数，父组件监听发射的事件，并定义接收该事件

```html
<!-- 父组件模板 -->
<div id="app">
  <!-- 监听子组件发射的事件命名为cpnClick -->
  <cpn @item-click="cpnClick"></cpn>
</div>

<!-- 子组件模板 -->
<template id="cpn">
  <div>
    <button v-for="item in categories" @click="bntClick(item)">
      {{item.name}}
    </button>
  </div>
</template>

<body>
  <script src="../js/vue.js"></script>
  <script>
    // 1.子组件
    const cpn = {
      template: '#cpn',
      data() {
        return {
          categories: [{
              id: 'aaa',
              name: '热门推荐'
            },
            {
              id: 'bbb',
              name: '手机数码'
            },
            {
              id: 'ccc',
              name: '家用家电'
            },
            {
              id: 'ddd',
              name: '电脑办公'
            },
          ]
        }
      },
      methods: {
        bntClick(item){
          // 子组件发射'item-click'事件  自定义事件
          this.$emit('item-click',item)
        }
      }
    }

    // 2.父组件
    const app = new Vue({
      el: "#app",
      data: {
        info: {
          name: 'lyc',
          age: 18,
          height: 1.88
        }
      },
      components: {
        cpn
      },
      methods:{
        cpnClick(item){ 
          // 处理监听到的cpnClick事件
          console.log('cpnClick',item);
        }
      }
    })
  </script>
</body>
```

### 父子组件间的通信

- 通过props向子组件传递数据
- 通过事件向父组件发送消息

![image-20210601005223818](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210601005223818.png)

### 父子通信案例

> 父给子传值，子修改值并且将值传回父，修改父的值

````html
<div id="app">
  <cpn :number1="num1" :number2="num2" @num1change="num1change" @num2change="num2change"></cpn>
</div>

<template id="cpn">
  <div>
    <h2>props:{{number1}}</h2>
    <h2>data:{{dnumber1}}</h2>
    <!-- Vue不推荐将v-model绑定在props上，因为一个数据可以被两个对象修改会引起混乱 -->
    <!-- <input type="text" v-model="number1"> -->
    <!-- <input type="text" v-model="dnumber1"> -->
    <input type="text" :value="dnumber1" @input="num1Input">

    <h2>props:{{number2}}</h2>
    <h2>data:{{dnumber2}}</h2>
    <!-- <input type="text" v-model="number2"> -->
    <!-- <input type="text" v-model="dnumber2"> -->
    <input type="text" :value="dnumber2" @input="num2Input">
  </div>
</template>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        num1: 1,
        num2: 0
      },
      methods: {
        num1change(value) {
          this.num1 = parseFloat(value)
        },
        num2change(value) {
          this.num2 = parseFloat(value)
        }
      },
      components: {
        cpn: {
          template: '#cpn',
          props: {
            number1: Number,
            number2: Number
          },
          data() {
            return {
              dnumber1: this.number1,
              dnumber2: this.number2
            }
          },
          methods: {
            num1Input(event) {
              // 1.将input中的value赋值到dnumber中
              this.dnumber1 = event.target.value;
              // 2.为了让父组件可以修改值，发送一个事件
              this.$emit('num1change', this.dnumber1)
              // 3.同时修改dnumber2的值
              this.dnumber2 = this.dnumber1 * 100;
              this.$emit('num2change', this.dnumber2)
            },
            num2Input(event) {
              this.dnumber2 = event.target.value;
              this.$emit('num2change', this.dnumber2)

              // 3.同时修改dnumber1的值
              this.dnumber1 = this.dnumber2 / 100;
              this.$emit('num1change', this.dnumber1)
            }
          }
        }
      }
    })
  </script>
</body>
````

![image-20210602175906516](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210602175906516.png)

## 十二、父子组件的访问方式

有时候我们需要父组件直接访问子组件,子组件直接访问父组件,或者是子组件访问跟组件。

- 父组件访问子组件:使用\$children或$refs reference(引用)
- 子组件访问父组件:使用$parent

### 父访问子

- $children	获取全部子组件的信息
- $refs           获取特定组件的信息

```html
<div id="app">
	<cpn></cpn>
	<cpn></cpn>
	<cpn ref="aaa"></cpn>
	<button @click="bntClick">按钮</button>
</div>

<template id="cpn">
	<div>
		我是子组件
	</div>
</template>

<body>
	<script src="../js/vue.js"></script>
	<script>
		const app = new Vue({
			el: "#app",
			data: {
				massage: "你好"
			},
			methods:{
				bntClick(){
					// 1.$children
					// console.log(this.$children);
					// for (let c of this.$children) {
					// 	console.log(c.name);
					// 	c.showMessage();
					// }
					// console.log(this.$children[3].name)

					// 2.$refs => 对象类型，默认是一个空的对象 ref="aaa"
					console.log(this.$refs.aaa.name);
				}
			},
			components:{
				cpn:{
					template:'#cpn',
					data(){
						return{
							name:'我是子组件的name'
						}
					},
					methods:{
						showMessage(){
							console.log('showMessage')
						}
					}
				}
			}
		})
	</script>
</body>
```

### 子访问父

```html
<div id="app">
  <cpn></cpn>
</div>

<template id="cpn">
  <div>
    <h2>我是cpn组件</h2>
    <ccpn></ccpn>
  </div>
</template>

<template id="ccpn">
  <div>
    <h2>我是ccpn组件</h2>
    <button @click="bntClick">
      按钮
    </button>
  </div>
</template>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好"
      },
      components: {
        cpn: {
          template: '#cpn',
          data(){
            return{
              name:"我是cpn组件的name"
            }
          },
          components: {
            ccpn: {
              template: '#ccpn',
              methods: {
                bntClick() {
                  // 1.访问父组件$parent
                  console.log(this.$parent);
                  console.log(this.$parent.name);
                  
                  // 2.访问根组件$root
                  console.log(this.$root);
                  console.log(this.$root.massage)
                }
              }
            }
          }
        }
      }
    })
  </script>
```

## 十三、插槽slot

在生活中很多地方都有插槽,电脑的USB插槽,插板当中的电源插槽。

- 插槽的目的是让我们原来的设备具备更多的扩展性。
- 比如电脑的USB我们可以插入U盘、硬盘、手机、音响、键盘、鼠标等等

组件的插槽:

- 组件的插槽也是为了让我们封装的组件更加具有扩展性。
- 让使用者可以决定组件内部的一些内容到底展示什么。

栗子:移动网站中的导航栏。

- 移动开发中,几乎每个页面都有导航栏。
- 导航栏我们必然会封装成一个插件,比如nav-bar组件。
- 一旦有了这个组件,我们就可以在多个页面中复用了。

![image-20210603002639778](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210603002639778.png)

 如何去封装这类的组件呢?

- 它们也很多区别,但是也有很多共性。
- 如果,我们每一个单独去封装一个组件 ,显然不合适:比如每个页面都返回,这部分内容我们就要重复去封装。
- 但是,如果我们封装成一个,好像也不合理:有些左侧是菜单,有些是返回,有些中间是搜索,有些是文字,等等。

如何封装合适呢?**抽取共性,保留不同。**

- 最好的封装方式就是将共性抽取到组件中,将不同暴露为插槽。
- 一旦我们预留了插槽,就可以让使用者根据自己的需求,决定插槽中插入什么内容。
- 是搜索框,还是文字，还是菜单。由调用者自己来决定。

### 基本使用

1. 插槽的基本使用\<slot>\</slot>

2. 插槽的默认值 \<slot>\<button>默认按钮\</button>\</slot>
3. 如果有多个值，同时放入到组件进行替换是，一起作为替换元素

```html
<div id="app">
  <cpn> <button>按钮1</button> </cpn>
  <cpn>
    <i>哈哈哈</i>
    <span>对对对</span>
    <button>确定</button>
  </cpn>
  <cpn><span>呵呵呵</span></cpn>
  <cpn></cpn>
</div>

<template id="cpn">
  <div>
    <h2>我是组件</h2>
    <p>我是啊啊啊啊啊啊啊啊啊</p>
    <slot><button>默认按钮</button></slot>
  </div>
</template>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好"
      },
      components: {
        cpn: {
          template: '#cpn'
        }
      }
    })
  </script>
</body>
```

### 具名插槽

> 通过slot="center"来指定替换name="center"的插槽

```html
<div id="app">
  <cpn><span slot="center">标题</span><button slot="left">zb</button></cpn>
</div>

<template id="cpn">
  <div>
    <slot name="left"><span>左边</span></slot>
    <slot name="center"><span>中间</span></slot>
    <slot name="right"><span>右边</span></slot>
  </div>
</template>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好"
      },
      components: {
        cpn: {
          template: '#cpn'
        }
      }
    })
  </script>
</body>
```

### 编译作用域

>父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。

```html
<div id="app">
  <cpn v-show="isShow"></cpn>
</div>

<template id="cpn">
  <div>
    <h2 v-show="isShow">我是子组件</h2>
    <p>我是内容，哈哈哈</p>
  </div>
</template>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好",
        isShow: true
      },
      components: {
        cpn: {
          template: '#cpn',
          data() {
            return {
              isShow: false
            }
          }
        }
      }
    })
  </script>
</body>

```

### 作用域插槽

>父组件替换插槽的标签,但是内容由子组件来提供。
>
>就是说父组件拿到子组件的内容从新排版

```html
<div id="app">
  <cpn></cpn>

  <cpn>
    <!-- 新版本 -->
    <!-- 目的是获取子组件中的pLanguages -->
    <!-- 2.绑定插槽，并且命名为slot -->
    <template v-slot:footer="slot">
      <!-- <span v-for="item in slot.data">{{item}}——</span> -->
      <!-- 3.调用插槽里面的数据 -->
      <span>{{slot.data.join('——')}}</span>
    </template>
  </cpn>
  
  <cpn>
    <!-- 旧版本 -->
    <template slot="footer" slot-scope="slot">
      <!-- <span v-for="item in slot.data">{{item}}*</span> -->
      <span>{{slot.data.join('*')}}</span>
    </template>
  </cpn>

</div>

<template id="cpn">
  <div>
    <!-- 1.先定义插槽的名字和里面数据的名字 -->
    <slot name="footer" :data="pLanguages">
      <ul>
        <li v-for="item in pLanguages">{{item}}</li>
      </ul>
    </slot>
  </div>
</template>

<body>
  <script src="../js/vue.js"></script>
  <script>
    const app = new Vue({
      el: "#app",
      data: {
        massage: "你好",
      },
      components: {
        cpn: {
          template: '#cpn',
          data() {
            return {
              pLanguages: ['JavaScript', 'Python', 'Swift', 'Go', 'C++']
            }
          }
        }
      }
    })
  </script>
</body>
```

# 4、模块化开发

## ES6模块化的导入和导出

- 我们使用export指令导出了模块对外提供的接口,下面我们就可以通过import命令来加载对应的这个模块了
- 首先,我们需要在HTML代码中引入两个js文件,并且类型需要设置为module
- import指令用于导入模块中的内容.比如main.is的代码

**导出方法：**

```js
var name = '小明';
var age = 18;
var flag = true;

function sum(num1, num2) {
  return num1 + num2
}

if (flag) {
  console.log(sum(20, 30));
}

// 1.导出方式一：
export{
  flag,sum
}

// 2.导出方式二：
export var num1 = 100;
export var height = 1.88;

// 3.导出函数/类
export function mul(num1,num2){
  return num1+num2
}
export class Person{
  run(){
    console.log('再跑');
  }
}

// 5.export default
// 某些情况下, 一个模块中包含某个的功能,我们并不希望给这个功能命名,而且让导入者可以自己来命名，只能有一个

// const address = "北京市";
// export default address;

export default function(argument){
  console.log(argument);
}
```

**导入方法：**

```js
// 1.导入的{}中定义的变量
import {flag,sum} from "./aaa.js";
if(flag){
  console.log("小明666");
  console.log(sum(20,30));
}

// 2.直接导入export定义的变量
import{num1,height} from "./aaa.js";
console.log(num1);
console.log(height);

// 3.导入 export的function/class
import{mul,Person} from "./aaa.js";
console.log(mul(1000,100))
const p = new Person();
p.run();

// 4.导入export default中的内容
import addr from "./aaa.js";
addr('你好');

// 5.同一全部导入
import * as aaa from "./aaa.js";
console.log(aaa.flag)
```



# 5、Webpack

## 一、什么是webpack

前端模块化:

- 在前面学习中,我已经用了大量的篇幅解释了为什么前端需要模块化。
- 而且我也提到了目前使用前端模块化的一些方案: AMD、CMD、CommonJS、 ES6。
- 在ES6之前,我们要想进行模块化开发,就必须借助于其他的工具,让我们可以进行模块化开发。
- 并且在通过模块化开发完成了项目后,还需要处理模块间的各种依赖,并且将其进行整合打包。
- 而webpack其中一个核心就是让我们可能进行模块化开发 ,并且会帮助我们处理模块间的依赖关系。而且不仅仅是JavaScript文件,我们的CSS、图片、json文件等等在webpack中都可以被当做模块来使用(在后续我们会看到)。
- 这就是webpack中模块化的概念。

打包如何理解呢?

- 理解了webpack可以帮助我们进行模块化,并且处理模块间的各种复杂关系后,打包的概念就非常好理解了。
- 就是将webpack中的各种资源模块进行打包合并成一个或多个包(Bundle)。
- 并且在打包的过程中,还可以对资源进行处理比如压缩图片,将scss转成css ,将ES6语法转成ES5语法,将TypeScript转成JavaScript等等操作.

![image-20210712124430916](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210712124430916.png)

## 二、webpack安装

![image-20210712131815476](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210712131815476.png)

### 准备工作

- 我们创建如下文件和文件夹:
- 文件和文件夹解析:
  - dist文件夹:用于存放之后打包的文件
  - src文件夹:用于存放我们写的源文件
    - main.js :项目的入口文件。具体内容查看下面详情。
    - mathUtils.js :定义了一 -些数学工具函数 ,可以在其他地方引用,并且使用。具体内容查看下面的详情。
  -  index.html :浏览器打开展示的首页html
  - package.json :通过npm init生成的, npm包管理的文件
- mathUtils.js文件中的代码:
- main.js文件中的代码:

### JS文件的打包

- 现在的js文件中使用了模块化的方式进行开发,他们可以直接使用吗?不可以。
  - 因为如果直接在index.htmI引入这两个js文件,浏览器并不识别其中模块化代码。
  - 外,在真实项目中当有许多这样的js文件时,我们一个个引用非常麻烦,并且后期非常不方便对它们进行管理。
- 我们应该怎么做呢?使用webpack工具,对多个js文件进行打包。
  - 我们知道, webpack就是一个模块化的打包工垦 ,所以它支持我们代码中写模块化,可以对模块化的代码进行处理。( 如何处理的,待会儿在原理中, 我会讲解)
  - 另外,如果在处理完所有模块之间的关系后,将多个js打包到一个js文件中 ,引入时就变得非常方便了。
- OK ,如何打包呢?使用webpack的指令即可

```js
webpack ./src/main.js ./dist/bundle.js
```

![image-20210712135530268](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210712135530268.png)

- 打包后会在dist文件下,生成一个bundle.js文件
  - 文件内容有些复杂,这里暂时先不看,后续再进行分析。
  - bundle.js文件,是webpack处理了项目直接文件依赖后生成的一个js文件,我们只需要将这个js文件在index.htmlI中引入即可

### webpack.config.js和package.json的配置

#### webpack.config.js可以配置webpack的出入口

```js
//引用node的基本包
const path = require('path');

// 指定webpack的出入口
module.exports = {
  entry: './src/main.js',
  output: {
    // 动态获取路径 绝对路径
    path: path.resolve(__dirname,'dist'),
    filename: 'bundle.js'
  },
} 
```

#### package.json配置node脚本和依赖

```json
{
  "name": "meetwebpack",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
    "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"  //npm run build 运行本地webpack而不是全局webpack
  },
  "author": "",
  "license": "ISC",
  "dependencies": {},
  "devDependencies": {
    "webpack": "^3.6.0"	//所依赖的webpack版本
  }
}
```

局部安装webpack

```
npm install webpack@3.6.0 --save-dev
```

## 三、Loader

- loader是webpack中一个非常核心的概念。

- webpack用来做什么呢?

  - 在我们之前的实例中,我们主要是用webpack来处理我们写的js代码,并且webpack会自动处理js之间相关的依赖。
  - 但是,在开发中我们不仅仅有基本的js代码处理,我们也需要加载css、图片,也包括一些高级的将ES6转成ES5代码,将TypeScript转成ES5代码,将scss、less转成css ,将jsx、.vue文件转成js文件等等。
  - 对于webpack本身的能力来说,对于这些转化是不支持的。
  - 那怎么办呢?给webpack扩展对应的loader就可以啦。 

- loader使用过程:

  - 步骤一 : 通过npm安装需要使用的loader

  - 步骤二 : 在webpack.config.js中的modules关键字下进行配置 

- 大部分loader我们都可以在webpack的官网中找到,并且学习对应的用法。

### CSS和LESS文件处理

- 项目开发过程中,我们必然需要添加很多的样式,而样式我们往往写到一个单独的文件中。

  - 在src目录中,创建一个css文件 ,其中创建一个normal.css文件。

  - 我们也可以重新组织文件的目录结构,将零散的js文件放在一个js文件夹中。

- normal.css中的代码非常简单,就是将body设置为red

- 但是,这个时候normal.css中的样式会生效吗?

  - 当然不会,因为我们压根就没有引用它。
  - webpack也不可能找到它,因为我们只有一个入口, webpack会从入口开始查找其他依赖的文件。

![image-20210712153335881](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210712153335881.png)

mian.js

```js
// 1. 使用commonjs的模块化规范
const {add, mul} = require('./js/mathUtils.js')
  
console.log(add(20,30));
console.log(mul(20,30));

// 2.使用ES6的模块化规范
import { name,age,height} from './js/info.js';
console.log(name);
console.log(age);
console.log(height);

// 3.依赖css文件
require('./css/normal.css')

// 4.依赖less文件
require('./css/special.less')
document.writeln('<h2>你好<h2>')
```

在webpack里面找到CSS的loader

安装css-loader `css-loader只负责将css文件进行加载`

```
npm install --save-dev css-loader
```

安装style-loader `style-loader 把CSS样式插入到DOM中`

```
npm install --save-dev style-loader
```

使用多个loader时，是从右向左

webpack.config.js的配置

```js
const path = require('path');

// 指定webpack的出入口
module.exports = {
  entry: './src/main.js',
  output: {
    // 动态获取路径 绝对路径
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [{
        test: /\.css$/i,
        // css-loader只负责将css文件进行加载
        // style-loader 把CSS样式插入到DOM中
        // 使用多个loader时，是从右向左
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.less$/,
        use: [{
          loader: "style-loader" // creates style nodes from JS strings
        }, {
          loader: "css-loader" // translates CSS into CommonJS
        }, {
          loader: "less-loader" // compiles Less to CSS
        }]
      }
    ],
  },
}
```

### 图片文件处理

安装url-loader

```
npm install --save-dev url-loader
```

如果大于limit就要安装file-loader

```
npm install --save-dev file-loader
```

配置**webpack.config.js**

```js
{
        test: /\.(png|jpg|gif|jpeg)$/,
        use: [{
          loader: 'url-loader',
          options: {
            // 当加载图片时，小于limit时，会将图片编译成base64字符串形式。
            // 当加载图片时，大于limit时，需要使用file-loader模块进行加载。
            limit: 13000,
            name:'img/[name].[hash:8].[ext]'  //使图片全部储存在dist的img文件夹里且命名为 原来名字+8位hash值（防止重复）+.原来后缀
          },
        }]
      }
```

再次打包后dist文件夹会出现一个图片文件

- 我们发现webpack自动帮助我们生成- 个非常长的名字
  - 这是一个32位hash值，目的是防止名字重复
  - 但是,真实开发中,我们可能对打包的图片名字有一定的要求
  - 比如,将所有的图片放在一个文件夹中,跟上图片原来的名称,同时也要防止重复
- 所以,我们可以在options中添加上如下选项:
  - img:文件要打包到的文件夹
  - name :获取图片原来的名字,放在该位置
  - hash:8 :为了防止图片名称冲突,依然使用hash ,但是我们只保留8位
  - ext :使用图片原来的扩展名、
- 但是,我们发现图片并没有显示出来,这是因为图片使用的路径不正确
  - 默认情况下, webpack会将生成的路径直接返回给使用者
  - 但是,我们整个程序是打包在dist文件夹下的,所以这里我们需要在路径下再添加一个dist/

![image-20210712183557041](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210712183557041.png)

### ES6语法处理

如果你仔细阅读webpack打包的jis文件,发现写的ES6语法并没有转成ES5 ,那么就意味着可能一 些对ES6还不支持的浏览器没有办法很好的运行我们的代码。
在前面我们说过,如果希望将ES6的语法转成ES5 ,那么就需要使用babel。

- 而在webpack中,我们直接使用babel对应的loader就可以了。

- ```
  npm install --save-dev babel-loader@7 babel-core babel-preset-es2015
  ```

- 配置webpack.config.js文件

- ```
  	{
          test: /\.m?js$/,
          exclude: /(node_modules|bower_components)/,
          use: {
            loader: 'babel-loader',
            options: {
              presets: ['es2015']
            }
          }
        },
  ```

###  Webpack配置Vue

1. npm安装vue

   ```
   npm install vue --save
   ```

   

2. 依赖引入vue并使用

3. 指定vue的版本

- runtime-only 版本->代码中,不可以有任何的template
- runtime-compiler 版本 >代码中,可以有template,因为有compiler可以用于编译template

在webpack.config.js中配置

```js
resolve: {
    alias: {
      'Vue$': 'vue/dist/vue.esm.js'
    }
  }
```

### el和template区别

定义template属性:

- 在前面的Vue实例中,我们定义了el属性,用于和index.htmI中的#app进行绑定,让Vue实例之后可以管理它其中的内容

- 这里,我们可以将div元素中的{message}}内容删掉,只保留一个基本的id为div的元素

- 但是如果我依然希望在其中显示{{message}}的内容,应该怎么处理呢?

- 我们可以再定义一个template属性 ,代码如下: 

- ```js
  new Vue({
    el: '#app',
    template: `
    <div>
      <h1>{{message}}</h1>
    </div>
    `,
    data: {
      message: 'Hello Webpack'
    }
  })
  ```

### .vue文件的处理

**从html中写vue代码->main.js中写vue代码->vue.js中写vue代码**

main.js中写vue代码

```js
// 5.使用vue进行开发
import Vue from 'Vue'

new Vue({
  el: '#app',
  template: `
  <div>
    <h1>{{message}}</h1>
  </div>
  `,
  data: {
    message: 'Hello Webpack'
  }
})
```

`进行抽离`独立出来App.js

```js
export default {
  template: `
  <div>
    <h1>{{message}}</h1>
  </div>
  `,
  data() {
    return {
      message: 'Hello Webpack11'
    }
  }
}
```

`进一步抽离 `Vue.js中写vue代码

> Vue.js

```vue
<template>
  <div>
    <h1>{{ message }}</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "Hello Webpack11",
    };
  },

  components: {},

  computed: {},

  methods: {},
};
</script>
<style scoped>
h1 {
  color: aqua;
}
</style>
```

> Main.js

```js
import Vue from 'Vue'
import App from './vue/App.vue'

new Vue({
  el: '#app',
  template: '<App/>',
  components: {
    App
  }
})
```

#### 打包vue文件

npm安装vue-loader

```
npm install vue-loader@14.2.2 vue-template-compiler --save-dev
```

webpack.config.js配置文件

```js
{
        test: /\.vue$/,
        use: ['vue-loader']
      }
```

### plugin插件

- plugin是什么?
  - plugin是插件的意思,通常是用于对某个现有的架构进行扩展。
  - webpack中的插件,就是对webpack现有功能的各种扩展,比如打包优化,文件压缩等等。
- loader和plugin区别
  - loader主要用于转换某些类型的模块,它是一个转换器。
  - plugin是插件,它是对webpack本身的扩展,是-个扩展器。
- plugin的使用过程: 
  - 步骤一: 通过npm安装需要使用的plugins(某些webpack已经内置的插件不需要安装)
  - 步骤二:在webpack.config.js中的plugins中配置插件。
- 下面,我们就来看看可以通过哪些插件对现有的webpack打包过程进行扩容,让我们的webpack变得更加好用。

```js
const webpack = require('webpack')

plugins: [
    new webpack.BannerPlugin('最终版权归洛依尘所有')
  ],
```

#### 打包html的plugin

- 目前,我们的index.html文件是存放在项目的根目录下的。

  - 我们知道,在真实发布项目时 ,发布的是dist文件夹中的内容,但是dist文件夹中如果没有index.html文件,那么打包的js等文件也就没有意义了。
  - 所以,我们需要将index.html|文件打包到dist文件夹中,这个时候就可以使用HtmlWebpackPlugin插件

- HtmlWebpackPlugin插件可以为我们做这些事情:

  - 自动生成一个index.html文件(可以指定模板来生成)
  - 将打包的js文件,自动通过script标签插入到body中

- 安装HtmlWebpackPlugin插件

  ```
  npm install html-webpack-plugin@3.2.0 --save--dev
  ```

- 使用插件,修改webpack.config.js文件中plugins部分的内容如下:

  - 这里的template表示根据什么模板来生成index.html
  - 另外,我们需要删除之前在output中添加的publicPath属性
  - 否则插入的script标签中的src可能会有问题

  ```js
  plugins: [
      new webpack.BannerPlugin('最终版权归洛依尘所有'),
      new HtmlWebpackPlugin({
        template:'index.html'
        // 根据index.html模板生成
      })
    ],
  ```

#### js压缩的Plugin

- 在项目发布之前,我们必然需要对js等文件进行压缩处理

  - 这里,我们就对打包的js文件进行压缩
  - 我们使用一个第三方的插件uglifyjs-webpack-plugin ,并且版本号指定1.1.1 ,和CL2保持-致

  ```
  npm install uglifyjs-webpack-plugin@1.1.1 --save-dev
  ```

  

- 修改webpack.config.js文件,使用插件:

  ```js
  plugins: [
      new webpack.BannerPlugin('最终版权归洛依尘所有'),
      new HtmlWebpackPlugin({
        template:'index.html'
        // 根据index.html模板生成
      }),
      new UglifyjsWebpackPlugin()
    ],
  ```

#### 搭建本地服务器

- webpack提供了一个可选的本地开发服务器,这个本地服务器基于node.js搭建,内部使用express框架,可以实现我们想要的让浏览器自动刷新显示我们修改后的结果。

- 不过它是一-个单独的模块,在webpack中使用之前需要先安装它

  ```
  npm install --save-dev webpack-dev-server@2.9.1
  ```

  

- devserver也是作为webpack中的一个选项,选项本身可以设置如下属性:

  - contentBase :为哪一个文件夹提供本地服务 ,默认是根文件夹,我们这里要填写./dist
  - port :端口号
  - inline :页面实时刷新
  - historyApiFallback :在SPA页面中,依赖HTML5的history模式

- webpack.config.js文件配置修改如下:

  ```js
  devServer:{
      contentBase:'./dist',
      inline:true,
    }
  ```

- 我们可以再配置另外一个scripts :

  ```json
  "dependencies": {
      "html-webpack-plugin": "^3.2.0",
      "uglifyjs-webpack-plugin": "^1.1.1",
      "vue": "^2.6.14"
    },
  ```

  --open参数表示直接打开浏览器

