# React18学习笔记

## 一、React初体验

### **React是什么呢？**

- 相信每个做开发的人对它都或多或少有一些印象；

- 这里我们来看一下官方对它的解释：用于构建用户界面的 JavaScript 库； 

◼ **目前对于前端开发来说，几乎很少直接使用原生的JavaScript来开发应用程序，而是选择一个**JavaScript库 **（框架）。**

- 在过去的很长时间内，jQuery是被使用最多的JavaScript库；

- 在过去的一份调查中显示，全球前10,000个访问最高的网站中，有65%使用了jQuery，是当时最受欢迎的JavaScript库；

- 但是，目前甚至已经处于淘汰的边缘了；

◼ **而无论是国内外，最流行的其实是三大框架：**Vue、React、Angular。

### 如何学习React

![image-20221017140802294](http://img.roydust.top/img/202210171408348.png)

### **React的介绍（技术角度）**

**React是什么？**

- React：用于构建用户界面的 JavaScript 库；

- React的官网文档：https://zh-hans.reactjs.org/

![image-20221017141152196](http://img.roydust.top/img/202210171411248.png)

### React特点

◼ **声明式编程：**

- 声明式编程是目前整个大前端开发的模式：Vue、React、Flutter、SwiftUI； 

- 它允许我们只需要维护自己的状态，当状态改变时，React可以根据最新的状态去渲染我们的UI界面；

◼ **组件化开发：**

- 组件化开发页面目前前端的流行趋势，我们会将复杂的界面拆分成一个个小的组件； 

- 如何合理的进行组件的划分和设计也是后面我会讲到的一个重点；

◼ **多平台适配：**

- 2013年，React发布之初主要是开发Web页面； 

- 2015年，Facebook推出了ReactNative，用于开发移动端跨平台；（虽然目前Flutter非常火爆，但是还是有很多公司在使用ReactNative）；

- 2017年，Facebook推出ReactVR，用于开发虚拟现实Web应用程序；（VR也会是一个火爆的应用场景）；



### **React的开发依赖**

◼ **开发React必须依赖三个库：**

- react：包含react所必须的核心代码

- react-dom：react渲染在不同平台所需要的核心代码

- babel：将jsx转换成React代码的工具

◼ **第一次接触React会被它繁琐的依赖搞蒙，居然依赖这么多东西： （直接放弃？）**

- 对于Vue来说，我们只是依赖一个vue.js文件即可，但是react居然要依赖三个包。 

- 其实呢，这三个库是各司其职的，目的就是让每一个库只单纯做自己的事情; 

- 在React的0.14版本之前是没有react-dom这个概念的，所有功能都包含在react里；

◼ **为什么要进行拆分呢？原因就是react-native。** 

- react包中包含了react web和react-native所共同拥有的核心代码。 

- react-dom针对web和native所完成的事情不同：
  - web端：react-dom会将jsx最终渲染成真实的DOM，显示在浏览器中
  - native端：react-dom会将jsx最终渲染成原生的控件（比如Android中的Button，iOS中的UIButton）。



#### **Babel和React的关系**

◼ **babel是什么呢？**

- **Babel** ，又名 **Babel.js**。 

- 是目前前端使用非常广泛的编译器、转移器。 

- 比如当下很多浏览器并不支持ES6的语法，但是确实ES6的语法非常的简洁和方便，我们**开发时**希望使用它。 

- 那么编写源码时我们就可以使用ES6来编写，之后通过Babel工具，将ES6转成大多数浏览器都支持的ES5的语法。 

◼ **React和Babel的关系：**

- 默认情况下开发React其实可以不使用babel。 

- 但是前提是我们自己使用 React.createElement 来编写源代码，它编写的代码非常的繁琐和可读性差。 

- 那么我们就可以直接编写jsx（JavaScript XML）的语法，并且让babel帮助我们转换成React.createElement。 

#### **React的依赖引入**

◼ **所以，我们在编写React代码时，这三个依赖都是必不可少的。**

◼ **那么，如何添加这三个依赖：**

- 方式一：直接CDN引入

- 方式二：下载后，添加本地依赖

- 方式三：通过npm管理（后续脚手架再使用）

◼ **暂时我们直接通过CDN引入，来演练下面的示例程序：**

```html
    <!-- 添加依赖 -->
    <script
      crossorigin
      src="https://unpkg.com/react@18/umd/react.development.js"
    ></script>
    <script
      crossorigin
      src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"
    ></script>
    <!-- bable -->
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```



### **Hello World**

◼ **第一步：在界面上通过React显示一个Hello World**

- 注意：这里我们编写React的script代码中，必须添加 type="text/babel"，作用是可以让babel解析jsx的语法

◼ **ReactDOM. createRoot函数：用于创建一个React根，之后渲染的内容会包含在这个根中**

- 参数：将渲染的内容，挂载到哪一个HTML元素上
  - 这里我们已经提定义一个id为app的div

◼ **root.render函数:** 

- 参数：要渲染的根组件

◼ **我们可以通过{}语法来引入外部的变量或者表达式**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Hello React</title>
  </head>
  <body>
    <div id="root"></div>

    <!-- 添加依赖 -->
    <script
      crossorigin
      src="https://unpkg.com/react@18/umd/react.development.js"
    ></script>
    <script
      crossorigin
      src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"
    ></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

    <script type="text/babel">
    	// 编写React代码(jsx语法)
      // jsx语法 -> 普通的JavaScript代码 -> bable
    
      const root = ReactDOM.createRoot(document.querySelector("#root"));

      // 1.将文本定义成变量
      let message = "hello world";

      // 2.监听按钮的点击
      function bntClick() {
        // 1.修改数据
        message = "Hello React";

        // 2.重新渲染界面
        rootRender();
      }

      rootRender();
      // 3.封装一个渲染函数
      function rootRender() {
        root.render(
          <div>
            <h2>{message}</h2>
            <button onClick={bntClick}>修改文本</button>
          </div>
        );
      }
    </script>
  </body>
</html>
```



#### **Hello React – 组件化开发**

◼ **整个逻辑其实可以看做一个整体，那么我们就可以将其封装成一个组件：**

- 我们说过root.render 参数是一个HTML元素或者一个组件； 

- 所以我们可以先将之前的业务逻辑封装到一个组件中，然后传入到 ReactDOM.render 函数中的第一个参数；

◼ **在React中，如何封装一个组件呢？**这里我们暂时使用类的方式封装组件：

1. 定义一个类（类名大写，组件的名称是必须大写的，小写会被认为是HTML元素），继承自React.Component

2. 实现当前组件的render函数
   - render当中返回的jsx内容，就是之后React会帮助我们渲染的内容



##### **组件化 - 数据依赖**

◼ **组件化问题一：****数据在哪里定义****？** 

◼ **在组件中的数据，我们可以分成两类：**

- 参与界面更新的数据：当数据变量时，需要更新组件渲染的内容；

- 不参与界面更新的数据：当数据变量时，不需要更新将组建渲染的内容；

◼ **参与界面更新的数据我们也可以称之为是**参与数据流，这个数据是定义在**当前对象的state中**

- 我们可以通过在构造函数中 this.state = {定义的数据} 

- 当我们的数据发生变化时，我们可以调用 this.setState 来更新数据，并且通知React进行update操作；
  - 在进行update操作时，就会重新调用render函数，并且使用最新的数据，来渲染界面

```html
      class App extends React.Component {
        // 组件数据
        constructor() {
          super();

          this.state = {
            message: "Hello World",
          };
          // 对需要绑定的方法，提前绑定好this
          this.bntClick = this.bntClick.bind(this);
        }
		}
```



##### **组件化 – 事件绑定**

◼ **组件化问题二：事件绑定中的this**

- 在类中直接定义一个函数，并且将这个函数绑定到元素的onClick事件上，当前这个函数的this指向的是谁呢？

◼ **默认情况下是undefined**

- 很奇怪，居然是undefined； 

- 因为在正常的DOM操作中，监听点击，监听函数中的this其实是节点对象（比如说是button对象）；

- 这次因为React并不是直接渲染成真实的DOM，我们所编写的button只是一个语法糖，它的本质React的Element对象；

- 那么在这里发生监听的时候，react在执行函数时并没有绑定this，默认情况下就是一个undefined； 

◼ **我们在绑定的函数中，可能想要使用当前对象，比如执行 this.setState 函数，就必须拿到当前对象的this**

- 我们就需要在传入函数时，给这个函数直接绑定this

- 类似于下面的写法： 

  ```html
  <button onClick={this.changeText.bind(this)}>改变文本</button>
  ```

![image-20221011165220049](http://lyc-markdownimg.test.upcdn.net/img/202210111652214.png)



##### 重构Hello World

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="root"></div>

    <script src="../lib/react.js"></script>
    <script src="../lib//react-dom.js"></script>
    <script src="../lib//bable.js"></script>

    <script type="text/babel">
      // 使用组件进行重构代码
      // 类组件和函数式组件
      class App extends React.Component {
        // 组件数据
        constructor() {
          super();

          this.state = {
            message: "Hello World",
          };
          // 对需要绑定的方法，提前绑定好this
          this.bntClick = this.bntClick.bind(this);
        }
        // 组件方法(实例方法)
        bntClick() {
          // console.log(this);   undefined
          // 内部完成了两件事：1.将state中的message值修改掉 2.自动执行重新执行render函数
          this.setState({
            message: "Hello React",
          });
        }

        // 渲染内容render方法
        render() {
          return (
            <div>
              <h2>{this.state.message}</h2>
              <button onClick={this.bntClick}>修改文本</button>
            </div>
          );
        }
      }

      // 将组件渲染到界面上
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      // App根组件
      root.render(<App />);
    </script>
  </body>
</html>

```

### 综合案例

#### **电影列表展示**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="root"></div>

    <script src="../lib/react.js"></script>
    <script src="../lib//react-dom.js"></script>
    <script src="../lib//bable.js"></script>

    <script type="text/babel">
      // 1.创建root
      const root = ReactDOM.createRoot(document.querySelector("#root"));

      // 封装App组件
      class App extends React.Component {
        constructor() {
          super();

          this.state = {
            movies: ["星际穿越", "流浪地球", "大话西游"],
          };
        }

        render() {
          // 1.对movies进行for循环
          // const liEls = [];
          // for (let i = 0; i < this.state.movies.length; i++) {
          //   const movie = this.state.movies[i];
          //   const liEl = <li>{movie}</li>;
          //   liEls.push(liEl);
          // }

          // 2. movies数组 =》 liEls数组
          // const liEls = this.state.movies.map((movie) => <li>{movie}</li>);
          return (
            <div>
              <h2>电影列表</h2>
              <ul>
                {this.state.movies.map((movie) => (
                  <li>{movie}</li>
                ))}
              </ul>
            </div>
          );
        }
      }

      // 2.渲染组件
      root.render(<App />);
    </script>
  </body>
</html>

```

#### **计数器案例**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="root"></div>

    <script src="../lib/react.js"></script>
    <script src="../lib/react-dom.js"></script>
    <script src="../lib/bable.js"></script>

    <script type="text/babel">
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            number: 100,
          };
        }

        render() {
          const { number } = this.state;
          return (
            <div>
              <h2>当前计数：{number}</h2>
              <button onClick={this.increment.bind(this)}>+1</button>
              <button onClick={this.decrement.bind(this)}>-1</button>
            </div>
          );
        }

        // 组件的方法
        increment() {
          this.setState({
            number: this.state.number + 1,
          });
        }
        decrement() {
          this.setState({
            number: this.state.number - 1,
          });
        }
      }

      root.render(<App />);
    </script>
  </body>
</html>

```



## 二、JSX语法

### **认识JSX**

**JSX是什么？**

- JSX是一种JavaScript的语法扩展（eXtension），也在很多地方称之为JavaScript XML，因为看起就是一段XML语法； 

- 它用于描述我们的UI界面，并且其完成可以和JavaScript融合在一起使用； 

- 它不同于Vue中的模块语法，你不需要专门学习模块语法中的一些指令（比如v-for、v-if、v-else、v-bind）；



### **为什么React选择了JSX**

◼ **React认为**渲染逻辑本质上与其他UI逻辑存在内在耦合

- 比如UI需要绑定事件（button、a原生等等）；

- 比如UI中需要展示数据状态；

- 比如在某些状态发生改变时，又需要改变UI； 

◼ 他们之间是密不可分，所以React没有将标记分离到不同的文件中，而是将它们组合到了一起，这个地方就是组件（Component）； 

- 当然，后面我们还是会继续学习更多组件相关的东西；

◼ 在这里，我们只需要知道，JSX其实是嵌入到JavaScript中的一种结构语法；

◼ **JSX的书写规范：**

- JSX的顶层只能有一个根元素，所以我们很多时候会在外层包裹一个div元素（或者使用后面我们学习的Fragment）；

- 为了方便阅读，我们通常在jsx的外层包裹一个小括号()，这样可以方便阅读，并且jsx可以进行换行书写；

- JSX中的标签可以是单标签，也可以是双标签； 
  - 注意：如果是单标签，必须以/>结尾；



### **JSX的使用**

◼ **jsx中的注释**

```html
{/* jsx的注释写法 */}
```

◼ **JSX嵌入变量作为子元素**

- 情况一：当变量是Number、String、Array类型时，可以直接显示

- 情况二：当变量是null、undefined、Boolean类型时，内容为空；
  - 如果希望可以显示null、undefined、Boolean，那么需要转成字符串；
  - 转换的方式有很多，比如toString方法、和空字符串拼接，String(变量)等方式；

- 情况三：Object对象类型不能作为子元素（not valid as a React child） 

◼ **JSX嵌入表达式**

- 运算表达式

- 三元运算符

- 执行一个函数

◼ **jsx绑定属性**

- 比如元素都会有title属性

- 比如img元素会有src属性

- 比如a元素会有href属性

- 比如元素可能需要绑定class

- 比如原生使用内联样式style

```jsx
    <script type="text/babel">
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            message: "Hello World",
            title: "hhh",
            imgUrl:
              "https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fc90dcae96df46df906098437db738f0~tplv-k3u1fbpfcp-watermark.image?",
            isActive: true,
            ObjectStyle: { color: "red", fontSize: "30px" },
          };
        }

        render() {
          const { title, imgUrl, isActive, ObjectStyle } = this.state;
          // 1.class绑定写法一：字符串的拼接
          const className = `aaa bbb ${isActive ? "active" : ""}`;
          // 2.class绑定写法二：将所有的class放到一个数组中
          const classList = ["aaa", "bbb"];
          if (isActive) classList.push("active");
          // 3.class绑定的写法三：第三方库classnames

          return (
            <div>
              {/* 1.基本绑定 */}
              <h2 title={title}>我是H2元素</h2>
              <img src={imgUrl} alt="" />

              {/* 2.绑定class属性：最好使用className */}
              <h2 className={className}>哈哈哈</h2>
              <h2 className={classList.join(" ")}>哈哈哈哈</h2>

              {/* 3.绑定style属性:绑定的是对象类型 */}
              <h2 style={{ color: "red", fontSize: "30px" }}>哈哈哈哈哈哈</h2>
              <h2 style={ObjectStyle}>哈哈哈哈哈哈</h2>
            </div>
          );
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
```



### **React事件绑定**

◼ **如果原生DOM原生有一个监听事件，我们可以如何操作呢？**

- 方式一：获取DOM原生，添加监听事件；

- 方式二：在HTML原生中，直接绑定onclick； 

◼ **在React中是如何操作呢？**我们来实现一下React中的事件监听，这里主要有两点不同

- React 事件的命名采用小驼峰式（camelCase），而不是纯小写； 

- 我们需要通过{}传入一个事件处理函数，这个函数会在事件发生时被执行；

```jsx
    <script type="text/babel">
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            count: 100,
          };
        }

        bnt1Click() {
          this.setState({
            count: "1000",
          });
        }
        bnt2Click = () => {
          this.setState({
            count: "2000",
          });
        };
        bnt3Click() {
          this.setState({
            count: "9999",
          });
        }

        render() {
          const { count } = this.state;
          return (
            <div>
              {/* 1.this绑定方式一：bind绑定 */}
              <button onClick={this.bnt1Click.bind(this)}>按钮</button>

              {/* 2.this绑定方式二：ES6 class field */}
              <button onClick={this.bnt2Click}>按钮</button>

              {/* 3.this绑定方式三：直接传入一个箭头函数（zyao） */}
              <button onClick={() => console.log("bnt3Click")}>按钮</button>
              <button onClick={() => this.bnt3Click()}>按钮</button>
              <h2>{count}</h2>
            </div>
          );
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
```





### **this的绑定问题**

◼ **在事件执行后，我们可能需要获取当前类的对象中相关的属性，这个时候需要用到this**

- 如果我们这里直接打印this，也会发现它是一个undefined

◼ **为什么是undefined呢？**

- 原因是btnClick函数并不是我们主动调用的，而且当button发生改变时，React内部调用了btnClick函数；

- 而它内部调用时，并不知道要如何绑定正确的this； 

◼ **如何解决this的问题呢？**

- 方案一：bind给btnClick显示绑定this

- 方案二：使用 ES6 class fields 语法

- 方案三：事件监听时传入箭头函数（个人推荐）

```jsx
<script type="text/babel">
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            count: 100,
          };
        }

        bnt1Click() {
          this.setState({
            count: "1000",
          });
        }
        bnt2Click = () => {
          this.setState({
            count: "2000",
          });
        };
        bnt3Click() {
          this.setState({
            count: "9999",
          });
        }

        render() {
          const { count } = this.state;
          return (
            <div>
              {/* 1.this绑定方式一：bind绑定 */}
              <button onClick={this.bnt1Click.bind(this)}>按钮</button>

              {/* 2.this绑定方式二：ES6 class field */}
              <button onClick={this.bnt2Click}>按钮</button>

              {/* 3.this绑定方式三：直接传入一个箭头函数（zyao） */}
              <button onClick={() => console.log("bnt3Click")}>按钮</button>
              <button onClick={() => this.bnt3Click()}>按钮</button>
              <h2>{count}</h2>
            </div>
          );
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
```



### **事件参数传递**

◼ **在执行事件函数时，有可能我们需要获取一些参数信息：比如event对象、其他参数**

◼ **情况一：获取event对象**

- 很多时候我们需要拿到event对象来做一些事情（比如阻止默认行为）

- 那么默认情况下，event对象有被直接传入，函数就可以获取到event对象；

◼ **情况二：获取更多参数**

- 有更多参数时，我们最好的方式就是传入一个箭头函数，主动执行的事件函数，并且传入相关的其他参数；

```jsx
    <script type="text/babel">
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            message: "Hello World",
          };
        }

        bntClick(event, name, age) {
          console.log(event, this);
          console.log(name, age);
        }

        render() {
          const { message } = this.state;
          return (
            <div>
              {/* 1.event参数的传递 */}
              <button onClick={this.bntClick.bind(this)}>按钮1</button>
              <button onClick={(event) => this.bntClick(event)}>按钮2</button>

              {/* 2.额外的参数传递 */}
              <button onClick={this.bntClick.bind(this, "kobe", 30)}>
                按钮3(不推荐)
              </button>
              <button onClick={(event) => this.bntClick(event, "kobe", 30)}>
                按钮4
              </button>
            </div>
          );
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
```



### **React条件渲染**

◼ **某些情况下，界面的内容会根据不同的情况显示不同的内容，或者决定是否渲染某部分内容：**

- 在vue中，我们会通过指令来控制：比如v-if、v-show； 

- 在React中，所有的条件判断都和普通的JavaScript代码一致； 

◼ **常见的条件渲染的方式有哪些呢？**

◼ **方式一：条件判断语句**

- 适合逻辑较多的情况

◼ **方式二：三元运算符**

- 适合逻辑比较简单

◼ **方式三：与运算符&&**

- 适合如果条件成立，渲染某一个组件；如果条件不成立，什么内容也不渲染；

```jsx
<script type="text/babel">
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            message: "Hello World",
            isReady: true,
            friend: {
              name: "kobe",
              age: 30,
            },
          };
        }

        render() {
          const { message, isReady, friend } = this.state;

          // 1.条件判断一：使用if进行条件判断
          let showElement = null;
          if (isReady) {
            showElement = <h2>准备开始比赛吧</h2>;
          } else {
            showElement = <h1>请提前做好准备</h1>;
          }

          return (
            <div>
              {/* 1.根据条件判断 */}
              <div>{showElement}</div>

              {/* 2.三元运算符 */}
              <div>
                {isReady ? <button>开始战斗</button> : <h3>赶快准备</h3>}
              </div>

              {/* 3.&&逻辑与的运算符 */}
              {/* 场景：当取出来的friend可能为undefined时，使用&&进行条件判断 */}
              <div>{friend && <div>{friend.name + " " + friend.age}</div>}</div>
            </div>
          );
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
```



◼ **v-show的效果**

- 主要是控制display属性是否为none

```jsx
<script type="text/babel">
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            message: "Hello World",
            isShow: true,
          };
        }
        changeShow() {
          this.setState({
            isShow: !this.state.isShow,
          });
        }

        render() {
          const { message, isShow } = this.state;

          let showEl = null;
          if (isShow) {
            showEl = <h2>{message}</h2>;
          }
          return (
            <div>
              <button onClick={() => this.changeShow()}>切换</button>
              {isShow && <h2>{message}</h2>}

              {/* v-show的效果实现 */}
              <h2 style={{ display: isShow ? "block" : "none" }}>哈哈哈哈哈</h2>
            </div>
          );
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
```



### **React列表渲染**

◼ **真实开发中我们会从服务器请求到大量的数据，数据会以列表的形式存储：**

- 比如歌曲、歌手、排行榜列表的数据；

- 比如商品、购物车、评论列表的数据；

- 比如好友消息、动态、联系人列表的数据；

◼ **在React中并没有像Vue模块语法中的v-for指令，而且需要我们通过JavaScript代码的方式组织数据，转成JSX：** 

- 很多从Vue转型到React的同学非常不习惯，认为Vue的方式更加的简洁明了； 

- 但是React中的JSX正是因为和JavaScript无缝的衔接，让它可以更加的灵活； 

- 另外我经常会提到React是真正可以提高我们编写代码能力的一种方式； 

◼ **如何展示列表呢？**

- 在React中，展示列表最多的方式就是使用数组的map高阶函数； 

◼ **很多时候我们在展示一个数组中的数据之前，需要先对它进行一些处理：**

- 比如过滤掉一些内容：filter函数

- 比如截取数组中的一部分内容：slice函数

```jsx
 <script type="text/babel">
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            students: [
              { id: 123, name: "why12", score: 199 },
              { id: 154, name: "why23", score: 91 },
              { id: 143, name: "why45", score: 195 },
              { id: 146, name: "why42", score: 198 },
            ],
          };
        }

        render() {
          const { message, students } = this.state;

          // 分数大于100的学生显示
          const filterStudents = students.filter((item) => {
            return item.score > 100;
          });

          // 分数大于100，而且只显示2个人
          const sliceStudents = filterStudents.slice(0, 2);

          return (
            <div>
              <h2>学生列表数据</h2>
              <div className="list">
                {students
                  .filter((item) => {
                    return item.score > 100;
                  })
                  .slice(0, 2)
                  .map((item) => {
                    return (
                      <div className="item" key={item.id}>
                        <h2>学号：{item.id}</h2>
                        <h3>姓名：{item.name}</h3>
                        <h1>分数：{item.score}</h1>
                      </div>
                    );
                  })}
              </div>
            </div>
          );
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
```



**列表中的key**

◼ **我们会发现在前面的代码中只要展示列表都会报一个警告：**

![image-20221017145731930](http://img.roydust.top/img/202210171457985.png)

◼ **这个警告是告诉我们需要在列表展示的jsx中添加一个key。** 

- key主要的作用是为了提高diff算法时的效率；

```jsx
<div className="item" key={item.id}>
  <h2>学号：{item.id}</h2>
</div>
```



### **JSX的本质**

◼ **实际上，jsx 仅仅只是 React.createElement(component, props, ...children) 函数的语法糖。**

- 所有的jsx最终都会被转换成React.createElement的函数调用。

◼ **createElement需要传递三个参数：**

◼ 参数一：type

- 当前ReactElement的类型；

- 如果是标签元素，那么就使用字符串表示 “div”； 

- 如果是组件元素，那么就直接使用组件的名称；

◼ 参数二：config

- 所有jsx中的属性都在config中以对象的属性和值的形式存储；

- 比如传入className作为元素的class； 

◼ 参数三：children

- 存放在标签中的内容，以children数组的方式进行存储；

- 当然，如果是多个元素呢？React内部有对它们进行处理，处理的源码在下方

![image-20221017145937414](http://img.roydust.top/img/202210171459498.png)



### **直接编写jsx代码**

◼ **我们自己来编写React.createElement代码：**

- 我们就没有通过jsx来书写了，界面依然是可以正常的渲染。

- 另外，在这样的情况下，你还需要babel相关的内容吗？不需要了
  - 所以，type="text/babel"可以被我们删除掉了；
  - 所以，< script src="../react/babel.min.js">< /script>可以被我们删除掉了；

```html
<script>
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            message: "Hello World",
          };
        }

        render() {
          const { message } = this.state;

          const element = /*#__PURE__*/ React.createElement(
            "div",
            null,
            /*#__PURE__*/ React.createElement(
              "div",
              {
                className: "header",
              },
              "Header"
            ),
            /*#__PURE__*/ React.createElement(
              "div",
              {
                className: "content",
              },
              /*#__PURE__*/ React.createElement("div", null, "Banner"),
              /*#__PURE__*/ React.createElement(
                "ul",
                null,
                /*#__PURE__*/ React.createElement(
                  "li",
                  null,
                  "\u5217\u8868\u6570\u636E1"
                ),
                /*#__PURE__*/ React.createElement(
                  "li",
                  null,
                  "\u5217\u8868\u6570\u636E2"
                ),
                /*#__PURE__*/ React.createElement(
                  "li",
                  null,
                  "\u5217\u8868\u6570\u636E3"
                ),
                /*#__PURE__*/ React.createElement(
                  "li",
                  null,
                  "\u5217\u8868\u6570\u636E4"
                ),
                /*#__PURE__*/ React.createElement(
                  "li",
                  null,
                  "\u5217\u8868\u6570\u636E5"
                ),
                /*#__PURE__*/ React.createElement(
                  "li",
                  null,
                  "\u5217\u8868\u6570\u636E6"
                )
              )
            ),
            /*#__PURE__*/ React.createElement(
              "div",
              {
                className: "footer",
              },
              "Footer"
            )
          );
          return element;
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(React.createElement(App, null));
    </script>
```

### 什么是虚拟DOM?虚拟DOM在React中起到什么作用?

- 虚拟DOM diff
- 跨平台渲染
- 声明式编程  

### **虚拟DOM的创建过程**

◼ **我们通过 React.createElement 最终创建出来一个 ReactElement对象：**

◼ **这个ReactElement对象是什么作用呢？React为什么要创建它呢？**

- 原因是React利用ReactElement对象组成了一个JavaScript的对象树； 

- JavaScript的对象树就是虚拟DOM（Virtual DOM）； 

◼ **如何查看ReactElement的树结构呢？**

- 我们可以将之前的jsx返回结果进行打印； 

- 注意下面代码中我打jsx的打印；

◼ **而ReactElement最终形成的树结构就是Virtual DOM；**

![image-20221017150311251](http://img.roydust.top/img/202210171503316.png)



#### **声明式编程**

◼ **虚拟DOM帮助我们从命令式编程转到了声明式编程的模式**

◼ **React官方的说法：**Virtual DOM 是一种编程理念。

- 在这个理念中，UI以一种理想化或者说虚拟化的方式保存在内存中，并且它是一个相对简单的JavaScript对象

- 我们可以通过ReactDOM.render让 虚拟DOM 和 真实DOM同步起来，这个过程中叫做协调（Reconciliation）；

◼ 这种编程的方式赋予了React声明式的API： 

- 你只需要告诉React希望让UI是什么状态；

- React来确保DOM和这些状态是匹配的；

- 你不需要直接进行DOM操作，就可以从手动更改DOM、属性操作、事件处理中解放出来；



### **阶段案例练习**

◼ 1.在界面上以表格的形式，显示一些书籍的数据；

◼ 2.在底部显示书籍的总价格；

◼ 3.点击+或者-可以增加或减少书籍数量（如果为1，那么不能继续-）；

◼ 4.点击移除按钮，可以将书籍移除（当所有的书籍移除完毕时，显示：购物车为空~）；

```jsx
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>购物车案例</title>
    <style>
      table {
        border-collapse: collapse;
        text-align: center;
      }
      thead {
        background-color: #f2f2f2;
      }
      th,
      td {
        padding: 10px 16px;
        border: 1px solid #aaa;
      }
    </style>
  </head>
  <body>
    <div id="root"></div>

    <script src="../lib/react.js"></script>
    <script src="../lib/react-dom.js"></script>
    <script src="../lib/bable.js"></script>

    <script src="./data.js"></script>
    <script src="./format.js"></script>

    <script type="text/babel">
      // 1.定义根组件
      class App extends React.Component {
        constructor() {
          super();
          this.state = {
            books: books,
          };
        }

        getTotalPrice() {
          const totalPrice = this.state.books.reduce((preValue, item) => {
            return preValue + item.count * item.price;
          }, 0);
          return totalPrice;
        }

        increment(index) {
          const newBooks = [...this.state.books];
          newBooks[index].count += 1;
          this.setState({
            books: newBooks,
          });
        }

        decrement(index) {
          const newBooks = [...this.state.books];
          newBooks[index].count -= 1;
          this.setState({
            books: newBooks,
          });
        }

        changeCount(index, count) {
          const newBooks = [...this.state.books];
          newBooks[index].count += count;
          this.setState({
            books: newBooks,
          });
        }

        removeItem(index) {
          const newBooks = [...this.state.books];
          newBooks.splice(index, 1);
          this.setState({
            books: newBooks,
          });
        }

        renderBookList() {
          const { books } = this.state;
          return (
            <div>
              <table>
                <thead>
                  <tr>
                    <th>序号</th>
                    <th>书籍名称</th>
                    <th>出版日期</th>
                    <th>价格</th>
                    <th>购买数量</th>
                    <th>操作</th>
                  </tr>
                </thead>
                <tbody>
                  {books.map((item, index) => {
                    return (
                      <tr key={item.id}>
                        <td>{index + 1}</td>
                        <td>{item.name}</td>
                        <td>{item.date}</td>
                        <td>{formatPrice(item.price)}</td>
                        <td>
                          <button
                            disabled={item.count <= 1}
                            onClick={() => this.changeCount(index, -1)}
                          >
                            -
                          </button>
                          {item.count}
                          <button onClick={() => this.changeCount(index, 1)}>
                            +
                          </button>
                        </td>
                        <td>
                          <button onClick={() => this.removeItem(index)}>
                            删除
                          </button>
                        </td>
                      </tr>
                    );
                  })}
                </tbody>
              </table>
              <h2>总价格:{formatPrice(this.getTotalPrice())}</h2>
            </div>
          );
        }

        renderBookEmpty() {
          return (
            <div>
              <h2>购物车为空，请添加书籍</h2>
            </div>
          );
        }

        render() {
          const { books } = this.state;

          // 1.计算总价格方式一：
          // let totalPrice = 0;
          // for (let i = 0; i < books.length; i++) {
          //   const book = books[i];
          //   totalPrice += book.price * book.count;
          // }

          // 2.计算总价格的方式二：
          // const totalPrice = books.reduce((preValue, item) => {
          //   return preValue + item.count * item.price;
          // }, 0);

          return books.length ? this.renderBookList() : this.renderBookEmpty();
        }
      }
      // 2.创建root并且渲染App组件
      const root = ReactDOM.createRoot(document.querySelector("#root"));
      root.render(<App />);
    </script>
  </body>
</html>
```





## **三React脚手架解析**

### **前端工程的复杂化**

◼ **如果我们只是开发几个小的demo程序，那么永远不需要考虑一些复杂的问题：**

- 比如目录结构如何组织划分；

- 比如如何管理文件之间的相互依赖；

- 比如如何管理第三方模块的依赖；

- 比如项目发布前如何压缩、打包项目；

◼ **现代的前端项目已经越来越复杂了：**

- 不会再是在HTML中引入几个css文件，引入几个编写的js文件或者第三方的js文件这么简单；

- 比如css可能是使用less、sass等预处理器进行编写，我们需要将它们转成普通的css才能被浏览器解析；

- 比如JavaScript代码不再只是编写在几个文件中，而是通过模块化的方式，被组成在**成百上千**个文件中，我们需要通过模块化的技术来管理它们之间的相互依赖；

- 比如项目需要依赖很多的第三方库，如何更好的管理它们（比如管理它们的依赖、版本升级等）；

◼ **为了解决上面这些问题，我们需要再去学习一些工具：**

- 比如babel、webpack、gulp，配置它们转换规则、打包依赖、热更新等等一些的内容；

- 脚手架的出现，就是帮助我们解决这一系列问题的；



### **脚手架是什么呢？**

◼ **编程中提到的脚手架（Scaffold），其实是一种工具，帮我们可以快速生成项目的工程化结构；**

- 每个项目作出完成的效果不同，但是它们的基本工程化结构是相似的；

- 既然相似，就没有必要每次都从零开始搭建，完全可以使用一些工具，帮助我们生产基本的工程化模板； 

- 不同的项目，在这个模板的基础之上进行项目开发或者进行一些配置的简单修改即可；

- 这样也可以间接保证项目的基本机构一致性，方便后期的维护； 

◼ 总结：**脚手架让项目从搭建到开发，再到部署，整个流程变得快速和便捷；**



### **创建React项目**

- NPM下載create-react-app包

- **现在，我们就可以通过脚手架来创建React项目了。**

- *创建React项目的命令如下：**

  - 注意：项目名称不能包含大写字母

  - 另外还有更多创建项目的方式，可以参考GitHub的readm

- 创建完成后，进入对应的目录，就可以将项目跑起来：

- **创建React项目**

  create-react-app 项目名称

  cd 01-test-react

  yarn start



### 目录分析

![image-20221017151647923](http://img.roydust.top/img/202210171516013.png)



### **了解PWA**

◼ **整个目录结构都非常好理解，只是有一个PWA相关的概念：**

- PWA全称Progressive Web App，即渐进式WEB应用； 

- 一个 PWA 应用首先是一个网页, 可以通过 Web 技术编写出一个网页应用； 

- 随后添加上 App Manifest 和 Service Worker 来实现 PWA 的安装和离线等功能；

- 这种Web存在的形式，我们也称之为是 Web App； 

◼ **PWA解决了哪些问题呢？**

- 可以添加至主屏幕，点击主屏幕图标可以实现启动动画以及隐藏地址栏；

- 实现离线缓存功能，即使用户手机没有网络，依然可以使用一些离线功能；

- 实现了消息推送； 

- 等等一系列类似于Native App相关的功能；



### **脚手架中的webpack**

◼ **React脚手架默认是基于Webpack来开发的；**

◼ **但是，很奇怪：我们并没有在目录结构中看到任何webpack相关的内容？**

- 原因是React脚手架将webpack相关的配置隐藏起来了（其实从Vue CLI3开始，也是进行了隐藏）；

◼ **如果我们希望看到webpack的配置信息，应该怎么来做呢？**

- 我们可以执行一个package.json文件中的一个脚本："eject": "react-scripts eject"

- 这个操作是不可逆的，所以在执行过程中会给与我们提示；

**脚手架中的webpack**

```
yarn eject
```

![image-20221017152009384](http://img.roydust.top/img/202210171520492.png)



### **开始编写代码**

◼ **在src目录下，创建一个index.js文件，因为这是webpack打包的入口。**

◼ **在index.js中开始编写React代码：**

- 我们会发现和写的代码是逻辑是一致的；

- 只是在模块化开发中，我们需要手动的来导入React、ReactDOM，因为它们都是在我们安装的模块中；

```js
import React from "react"
import ReactDOM from "react-dom/client";
// 编写React代码，并且通过React渲染出来对应的内容

import App from "./App";

const root = ReactDOM.createRoot(document.querySelector("#root"))
root.render(<App />)
```



◼ **如果我们不希望直接在 root.render 中编写过多的代码，就可以单独抽取一个组件App.js：**

```jsx
import React from "react";
import HelloWorld from "./Component/HelloWorld";
// 编写一个组件
class App extends React.Component {
  constructor() {
    super();
    this.state = {
      message: "Hello React",
    };
  }

  render() {
    const { message } = this.state;

    return (
      <div>
        <h2>{message}</h2>
        <HelloWorld></HelloWorld>
      </div>
    );
  }
}
export default App;
```



## 四、React组件学习

###   组件化开发概念

- 组件化是一种分而治之的思想：
  - 如果我们将一个页面中所有的处理逻辑全部放在一起，处理起来就会变得非常复杂，而且不利于后续的管理及扩展。
  - 但如果，我们讲一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能，那么之后整个页面的管理和维护就变得非常容易了。
- 我们需要通过组件化的思想来思考整个应用程序：
  - 我们将一个完整的页面分成很多个组件；
  - 每个组件都用于实现页面的一个功能块；
  - 而每一个组件又可以进行细分；
  - 而组件本身又可以在多个地方进行复用；

![image-20221023161833715](http://img.roydust.top/img/202210231618831.png)

- 组件化是React的核心思想，也是我们后续课程的重点，前面我们封装的App本身就是一个组件：
  - 组件化提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用。
  - 任何的应用都会被抽象成一颗组件树。

#### React的组件化

- React的组件相对于Vue更加的灵活和多样，按照不同的方式可以分成很多类组件：
  - 根据组件的定义方式，可以分为：函数组件(Functional Component )和类组件(Class Component)；
  - 根据组件内部是否有状态需要维护，可以分成：无状态组件(Stateless Component )和有状态组件(Stateful Component)；
  - 根据组件的不同职责，可以分成：展示型组件(Presentational Component)和容器型组件(Container Component)；
- 这些概念有很多重叠，但是他们最主要是关注数据逻辑和UI展示的分离：
  - 函数组件、无状态组件、展示型组件主要关注UI的展示；
  - 类组件、有状态组件、容器型组件主要关注数据逻辑；

### 类组件

类组件的定义有如下要求：

- 组件的名称是大写字符开头
  - 类组件需要继承React.Component
  - 类组件必须实现render函数
- 在ES6之前，可以通过create-react-class 模块来定义类组件，但是目前官网建议我们使用ES6的class类定义。
- 使用class定义一个组件：
  - constructor是可选的，我们通常在constructor中初始化一些数据；
  - this.state中维护的就是我们组件内部的数据；
  - **render() 方法是 class 组件中唯一必须实现的方法；**



#### Render 函数的返回值

- 当 render 被调用时，它会检查 **this.props 和 this.state 的变化**并返回以下类型之一：
- React 元素：
  - 通常通过 JSX 创建。
  - 例如，<div / > 会被 React 渲染为 DOM 节点，<MyComponent / > 会被 React 渲染为自定义组件；
  - 无论是 <div / > 还是 <MyComponent / > 均为 React 元素。
- 数组或 fragments：使得 render 方法可以返回多个元素。
- Portals：可以渲染子节点到不同的 DOM 子树中。
- 字符串或数值类型：它们在 DOM 中会被渲染为文本节点
- 布尔类型或 null：什么都不渲染。

```jsx
import React, { Component } from "react";

// 1.类组件
export class App extends Component {
  constructor() {
    super();
    this.state = {
      message: "Hello Component",
    };
  }
  render() {
    const { message } = this.state;
    /* 1.React元素：通过jsx编译的代码就会被编译成React.createElement,所以返回的就是一个React元素 */
    /* return <h2>{message}</h2> */

    /* 2.组件或者fragments */
    // return ["abc", "bbb", "vax"];

    // 3.返回字符串/数字类型
    // return "Hello World";

    // 4.返回null或者布尔值
    return true;
  }
}

export default App;
```



### 函数组件

- **函数组件是使用function来进行定义的函数，只是这个函数会返回和类组件中render函数返回一样的内容。**
- 函数组件有自己的特点（当然，后面我们会讲hooks，就不一样了）：
  - 没有生命周期，也会被更新并挂载，但是没有生命周期函数；
  - this关键字不能指向组件实例（因为没有组件实例）；
  - 没有内部状态（state）；
- 我们来定义一个函数组件：

```jsx
// 函数式组件
function App() {
  return <h1>App Function Component</h1>;
}

export default App;
```



### 组件的生命周期

- **很多的事物都有从创建到销毁的整个过程，这个过程称之为是生命周期；**
- React组件也有自己的生命周期，了解组件的生命周期可以让我们在最合适的地方完成自己想要的功能；
- 生命周期和生命周期函数的关系：
- **生命周期是一个抽象的概念**，在生命周期的整个过程，分成了很多个阶段；
  - 比如装载阶段（Mount），组件第一次在DOM树中被渲染的过程；
  - 比如更新过程（Update），组件状态发生变化，重新更新渲染的过程；
  - 比如卸载过程（Unmount），组件从DOM树中被移除的过程；
- React内部为了告诉我们当前处于哪些阶段，会对我们组件内部实现的**某些函数进行回调**，**这些函数就是生命周期函数**：
  - 比如实现componentDidMount函数：组件已经挂载到DOM上时，就会回调；
  - 比如实现componentDidUpdate函数：组件已经发生了更新时，就会回调；
  - 比如实现componentWillUnmount函数：组件即将被移除时，就会回调；
  - 我们可以在这些回调函数中编写自己的逻辑代码，来完成自己的需求功能；
- 我们谈React生命周期时，主要谈的类的生命周期，因为函数式组件是没有生命周期函数的



#### 常用生命周期

![image-20221023163048175](http://img.roydust.top/img/202210231630242.png)

##### Constructor

- 如果不初始化state或者不进行方法绑定，则不需要为React组件实现构造函数
- constructor中通常只做两件事
  - 通过this.state复制对象来初始化内部的state
  - 为事件绑定实例（this）



##### componentDidMount

- componentDidMount()会在组件挂载后（插入dom树种）立即调用
- componentDidMount中通常进行哪些操作呢？
  - 依赖于DOM的操作可以在这里进行
  - 在此处就是发送网络请求的最好地方(官方推荐)
  - 可以在此处添加一些订阅（会在componentWillUnmount取消订阅）



##### componentDidUpdate

- componentDidUpdate() 会在更新后被立即调用，首次渲染不会执行此方法
  - 当组件更新后，可以在此处对DOM进行操作
  - 如果你对更新前后的props进行了比较，也可以选择在此处进行网络请求；（例如：放props未发生变化时，则不会执行网络请求）



##### componentWillUnmount

- componentWillUnmount() 会在组件卸载及销毁之前直接调用
  - 在此方法中执行必要的清理操作
  - 例如：清除timer，取消网络请求或清除在componentDidMount()中创建的订阅等



```jsx
import React, { Component } from "react";

export class HelloWorld extends Component {
  // 1.构造方法：constructor
  constructor() {
    console.log("constructor");
    super();
    this.state = {
      message: "Hello 生命周期",
    };
  }
  changeText() {
    this.setState({
      message: "你好啊，洛依尘",
    });
  }
  // 2.执行render函数
  render() {
    console.log("render");
    const { message } = this.state;
    return (
      <div>
        <h2>{message}</h2>
        <button onClick={(e) => this.changeText()}>修改文本</button>
      </div>
    );
  }
  // 3.组件被渲染到DOM：被挂载到DOM
  componentDidMount() {
    console.log("组件被渲染到DOM componentDidMount");
  }
  // 4.组件的DOM被更新完成：DOM发生更新
  componentDidUpdate(prevProps, prevState, snapshot) {
    console.log(
      "组件的DOM被更新完成 componentDidUpdate",
      prevProps,
      prevState,
      snapshot
    );
  }
  // 5.组件从DOM中卸载掉：从DOM移除掉
  componentWillUnmount() {
    console.log("组件从DOM中卸载掉 componentWillUnmount ");
  }

  // 不常用生命周期
  shouldComponentUpdate() {
    return true;
  }

  getSnapshotBeforeUpdate() {
    console.log("DOM更新前 getSnapshotBeforeUpdate");
    return {
      scrollPosition: 1000,
    };
  }
}

export default HelloWorld;
```





#### 不常用生命周期函数

**完整生命周期**![image-20221023164758372](http://img.roydust.top/img/202210231647500.png)

- 除了上面介绍的生命周期函数之外，还有一些不常用的生命周期函数：
  - getDerivedStateFromProps：state 的值在任何时候都依赖于 props时使用；该方法返回一个对象来更新state；
  - getSnapshotBeforeUpdate：在React更新DOM之前回调的一个函数，可以获取DOM更新前的一些信息（比如说滚动位置）；
  - shouldComponentUpdate：该生命周期函数很常用，但是等待讲性能优化时再来详细讲解；





### 组件间的通信

- 在开发过程中，我们会经常遇到需要组件之间相互进行通信：
  - 比如App可能使用了多个Header，每个地方的Header展示的内容不同，那么我们就需要使用者传递给Header一些数据，让其进行展示；
  - 又比如我们在Main中一次性请求了Banner数据和ProductList数据，那么就需要传递给他们来进行展示；
  - 也可能是子组件中发生了事件，需要由父组件来完成某些操作，那就需要子组件向父组件传递事件；
- 总之，在一个React项目中，组件之间的通信是非常重要的环节；
- 父组件在展示子组件，可能会传递一些数据给子组件：
  - 父组件通过 属性=值 的形式来传递给子组件数据；
  - 子组件通过 props 参数获取父组件传递过来的数据；



#### 参数propTypes

- 对于传递给子组件的数据，有时候我们可能希望进行验证，特别是对于大型项目来说：
  - 当然，如果你项目中默认继承了Flow或者TypeScript，那么直接就可以进行类型验证；
  - 但是，即使我们没有使用Flow或者TypeScript，也可以通过 prop-types 库来进行参数验证；
- 从 React v15.5 开始，React.PropTypes 已移入另一个包中：prop-types 库
- 更多的验证方式，可以参考官网：https://zh-hans.reactjs.org/docs/typechecking-with-proptypes.html
  - 比如验证数组，并且数组中包含哪些元素；
  - 比如验证对象，并且对象中包含哪些key以及value是什么类型；
  - 比如某个原生是必须的，使用 requiredFunc: PropTypes.func.isRequired
- 如果没有传递，我们希望有默认值呢？
  - 我们使用defaultProps就可以了



#### 父传子方式

> 父组件

```jsx
import React, { Component } from "react";
import axios from "axios";

import MainBanner from "./MainBanner";
import MainProductList from "./MainProductList";

export class Main extends Component {
  constructor() {
    super();
    this.state = {
      banners: ["新歌曲", "新MV", "新歌单"],
      productList: ["推荐商品", "热门商品", "流行商品"],
    };
  }
  componentDidMount() {
    axios.get("http://123.207.32.32:8000/home/multidata").then((res) => {
      const banners = res.data.data.banner.list;
      const recommend = res.data.data.recommend.list;
      this.setState({
        banners,
        productList: recommend,
      });
    });
  }
  render() {
    const { banners, productList } = this.state;
    return (
      <div className="main">
        <MainBanner banners={banners} title="轮播图" />
        <MainBanner  />
        <MainProductList productList={productList} />
      </div>
    );
  }
}

export default Main;
```

> 子组件

```jsx
import React, { Component } from "react";
import PropTypes from "prop-types";

export class MainBanner extends Component {
  // 新增defaultProps的方式
  static defaultProps = {
    banners: [],
    title: "默认标题",
  };
  render() {
    const { title, banners } = this.props;
    return (
      <div className="banner">
        <h2>{title}</h2>
        <ul>
          {banners.map((item) => {
            return <li key={item.acm}>{item.title}</li>;
          })}
        </ul>
      </div>
    );
  }
}
// MainBanner传入的props类型进行验证
MainBanner.protTypes = {
  banners: PropTypes.array.isRequired,
  title: PropTypes.string,
};
// MainBanner传入的props的默认值
MainBanner.defaultProps = {
  banners: [],
  title: "默认标题",
};

export default MainBanner;
```



#### 子传父方式

> 父组件

```jsx
import React, { Component } from "react";
import AddCounter from "./AddCounter";
import SubCounter from "./SubCounter";

export class App extends Component {
  constructor() {
    super();
    this.state = {
      counter: 100,
    };
  }

  // 定义一个回调函数改变父组件的count
  changeCount(count) {
    this.setState({
      counter: this.state.counter + count,
    });
  }

  render() {
    const { counter } = this.state;
    return (
      <div>
        <h2>当前计数：{counter}</h2>
        <AddCounter
          addClick={(count) => {
            this.changeCount(count);
          }}
        />
      </div>
    );
  }
}

export default App;
```

> 子组件

```jsx
import React, { Component } from "react";
import PropTypes from "prop-types";

export class AddCounter extends Component {
  addCount(count) {
    console.log("count", count);
    // 子组件调用通过父组件props传来的addClick方法
    this.props.addClick(count);
  }

  render() {
    return (
      <div>
        <button onClick={(e) => this.addCount(1)}>+1</button>
        <button onClick={(e) => this.addCount(5)}>+5</button>
        <button onClick={(e) => this.addCount(10)}>+10</button>
      </div>
    );
  }
}

AddCounter.protoType = {
  addClick: PropTypes.function,
};

export default AddCounter;
```



#### 组件通信案例练习

![image-20221023170011376](http://img.roydust.top/img/202210231700433.png)

> 父组件

```jsx
import React, { Component } from "react";
import TabControl from "./TabControl";

export class App extends Component {
  constructor() {
    super();
    this.state = {
      titles: ["流行", "新款", "精选"],
      tabIndex: 0,
    };
  }

  // 改变父组件的回调函数
  tabClick(tabIndex) {
    this.setState({
      tabIndex,
    });
  }

  render() {
    const { titles, tabIndex } = this.state;
    return (
      <div className="app">
        <TabControl titles={titles} tabClick={(i) => this.tabClick(i)} />
        <h1>{titles[tabIndex]}</h1>
      </div>
    );
  }
}

export default App;
```

> 子组件

```jsx
import React, { Component } from "react";
import "./style.css";

export class TabControl extends Component {
  constructor() {
    super();

    this.state = {
      currentIndex: 0,
    };
  }

  itemClick(index) {
    this.setState({
      currentIndex: index,
    });
    this.props.tabClick(index);
  }

  render() {
    const { titles } = this.props;
    const { currentIndex } = this.state;
    return (
      <div className="tab-control">
        {titles.map((item, index) => {
          return (
            <div
              className={`item ${index === currentIndex ? "active" : ""}`}
              key={item}
              onClick={(e) => this.itemClick(index)}
            >
              <span className="text"> {item}</span>
            </div>
          );
        })}
      </div>
    );
  }
}

export default TabControl;
```



### React中的插槽(Slot)

- 在开发中，我们抽取了一个组件，但是为了让这个组件具备更强的通用性，我们不能将组件中的内容限制为固定的div、span等等这些元素。
- 我们应该让使用者可以决定某一块区域到底存放什么内容。
  ![image-20221023170251374](http://img.roydust.top/img/202210231702429.png)

- 这种需求在Vue当中有一个固定的做法是通过slot来完成的，React呢？
- React对于这种需要插槽的情况非常灵活，有两种方案可以实现：
  - 组件的children子元素；
  - props属性传递React元素；



> 父组件

```jsx
import React, { Component } from "react";
import NavBar from "./nav-bar";
import NavBar2 from "./nav-bar2";

export class App extends Component {
  render() {
    const btn = <button>按钮</button>;

    return (
      <div>
        {/* 1.使用children实现插槽 */}
        <NavBar>
          <button>按钮</button>
          <h2>我是标题</h2>
          <i>斜体文字</i>
        </NavBar>

        {/* 2.使用props实现插槽 */}
        <NavBar2 leftSlot={btn} centerSlot={321} rightSlot={111} />
      </div>
    );
  }
}

export default App;
```



#### 组件的children子元素

- 每个组件都可以获取到 props.children：它包含组件的开始标签和结束标签之间的内容。

![image-20221022175841519](http://img.roydust.top/img/202210221758659.png)

```jsx
import React, { Component } from "react";
import protoTypes from "prop-types";
import "./style.css";

export class NavBar extends Component {
  render() {
    const { children } = this.props;
    return (
      <div className="nav-bar">
        <div className="left">{children[0]}</div>
        <div className="center">{children[1]}</div>
        <div className="right">{children[2]}</div>
      </div>
    );
  }
}

NavBar.protoTypes = {
  children: protoTypes.element,
};

export default NavBar;

```

- 通过children实现的方案虽然可行，但是有一个弊端：通过索引值获取传入的元素很容易出错，不能精准的获取传入的原生；

#### props属性传递React元素

- 另外一个种方案就是使用 props 实现：
  - 通过具体的属性名，可以让我们在传入和获取时更加的精准；

```jsx
import React, { Component } from "react";

export class NavBar2 extends Component {
  render() {
    const { leftSlot, centerSlot, rightSlot } = this.props;
    return (
      <div className="nav-bar">
        <div className="left">{leftSlot}</div>
        <div className="center">{centerSlot}</div>
        <div className="right">{rightSlot}</div>
      </div>
    );
  }
}

export default NavBar2;
```



#### 组件的作用域插槽

- 如果我们需要自定义插槽类型，但是插槽的数据需要子组件提供就需要传入一个回调函数



> 父组件

```jsx
import React, { Component } from "react";
import TabControl from "./TabControl";

export class App extends Component {
  constructor() {
    super();
    this.state = {
      titles: ["流行", "新款", "精选"],
      tabIndex: 0,
    };
  }

  // 切换active
  tabClick(tabIndex) {
    this.setState({
      tabIndex,
    });
  }

  //  作用域插槽
  tabItemType(item) {
    if (item === "流行") {
      return <span>{item}</span>;
    } else if (item === "新款") {
      return <button>{item}</button>;
    } else {
      return <i>{item} </i>;
    }
  }

  render() {
    const { titles, tabIndex } = this.state;
    return (
      <div className="app">
        <TabControl
          titles={titles}
          tabClick={(i) => this.tabClick(i)}
          // 父组件传回一个回调函数，回调函数获取到item传回后再进行处理
          itemType={(item) => this.tabItemType(item)}
        />
        <h1>{titles[tabIndex]}</h1>
      </div>
    );
  }
}

export default App;
```

> 子组件

```jsx
import React, { Component } from "react";
import "./style.css";

export class TabControl extends Component {
  constructor() {
    super();

    this.state = {
      currentIndex: 0,
    };
  }

  itemClick(index) {
    this.setState({
      currentIndex: index,
    });
    this.props.tabClick(index);
  }

  render() {
    // 子组件获取props里的itemType，并且传回item参数
    const { titles, itemType } = this.props;
    const { currentIndex } = this.state;
    return (
      <div className="tab-control">
        {titles.map((item, index) => {
          return (
            <div
              className={`item ${index === currentIndex ? "active" : ""}`}
              key={item}
              onClick={(e) => this.itemClick(index)}
            >
              {itemType(item)}
            </div>
          );
        })}
      </div>
    );
  }
}

export default TabControl;
```



### Context共享数据

- 非父子组件数据的共享：
  - 在开发中，比较常见的数据传递方式是通过props属性自上而下（由父到子）进行传递。
  - 但是对于有一些场景：比如一些数据需要在多个组件中进行共享（地区偏好、UI主题、用户登录状态、用户信息等）。
  - 如果我们在顶层的App中定义这些信息，之后一层层传递下去，那么对于一些中间层不需要数据的组件来说，是一种冗余的操作。
- 我们实现一个一层层传递的案例：
  - 我这边顺便补充一个小的知识点：Spread Attributes
- 但是，如果层级更多的话，一层层传递是非常麻烦，并且代码是非常冗余的：
  - React提供了一个API：**Context**；
  - Context 提供了一种在**组件之间共享此类值的方式，而不必显式地通过组件树的逐层传递 props；**
  - Context 设计目的是为了**共享那些对于一个组件树而言是“全局”的数据**，例如当前认证的用户、主题或首选语言；



#### Spread Attributes

有时候你需要给组件设置多个属性，你不想一个个写下这些属性，或者有时候你甚至不知道这些属性的名称，这时候 *spread attributes* 的功能就很有用了。

比如：

```javascript
var props = {};
props.foo = x;
props.bar = y;
var component = <Component {...props} />;
```

`props` 对象的属性会被设置成 `Component` 的属性。

属性也可以被覆盖：

```javascript
var props = { foo: 'default' };
var component = <Component {...props} foo={'override'} />;
console.log(component.props.foo); // 'override'
```

写在后面的属性值会覆盖前面的属性。



#### Context相关API

- React.createContext
  - 创建一个需要共享的Context对象：
  - 如果一个组件订阅了Context，那么这个组件会从离自身最近的那个匹配的 Provider 中读取到当前的context值；
  - defaultValue是组件在顶层查找过程中没有找到对应的Provider，那么就使用默认值



- Context.Provider
  - 每个 Context 对象都会返回一个 Provider React 组件，它允许消费组件订阅 context 的变化：
  - Provider 接收一个 value 属性，传递给消费组件；
  - 一个 Provider 可以和多个消费组件有对应关系；
  - 多个 Provider 也可以嵌套使用，里层的会覆盖外层的数据；
  - 当 Provider 的 value 值发生变化时，它内部的所有消费组件都会重新渲染；



- Class.contextType
  - 挂载在 class 上的 contextType 属性会被重赋值为一个由 React.createContext() 创建的 Context 对象：
  - 这能让你使用 this.context 来消费最近 Context 上的那个值；
  - 你可以在任何生命周期中访问到它，包括 render 函数中；



- Context.Consumer
  - 这里，React 组件也可以订阅到 context 变更。这能让你在 函数式组件 中完成订阅 context。
  - 这里需要 函数作为子元素（function as child）这种做法；
  - 这个函数接收当前的 context 值，返回一个 React 节点；



**什么时候使用默认值defaultValue呢？**

```jsx
import React from "react";
// 一、创建一个Context ()里面是默认数据，当ThemeContext.Provider外的组件获取共享数据时可以使用共享数据
const ThemeContext = React.createContext({ color: "blue", size: "10 " });

export default ThemeContext;

```

- 当ThemeContext.Provider外的组件获取共享数据时可以使用共享数据

**什么时候使用Context.Consumer呢？**

1. 当使用value的组件是一个函数式组件时；
2. 当组件中需要使用多个Context时；



#### 实际案例

> context 实例

```jsx
import React from "react";
// 一、创建一个Context ()里面是默认数据，当ThemeContext.Provider外的组件获取共享数据时可以使用共享数据
const ThemeContext = React.createContext({ color: "blue", size: "10 " });

export default ThemeContext;
```

> 主组件

```jsx
import React, { Component } from "react";
import Home from "./Home";
import ThemeContext from "./context/theme-context";
import UserContext from "./context/user-context";
import Profile from "./Profile";

export class App extends Component {
  constructor() {
    super();

    this.state = {
      info: { name: "kobe", age: 30 },
    };
  }
  render() {
    const { info } = this.state;
    return (
      <div>
        <h2>App</h2>
        {/* 二、通过ThemeContext里的Provider为后代提供数据,可以多层嵌套 */}
        <UserContext.Provider value={{ nickname: "kobe", age: "30" }}>
          <ThemeContext.Provider value={{ color: "red", size: "30" }}>
            <Home {...info} />
          </ThemeContext.Provider>
        </UserContext.Provider>
        <Profile />
      </div>
    );
  }
}

export default App;
```

> 子组件(正常调用)

```jsx
import React, { Component } from "react";
import HomeBanner from "./HomeBanner";
import HomeInfo from "./HomeInfo";

export class Home extends Component {
  render() {
    const { name, age } = this.props;
    return (
      <div>
        <h2>
          Home:{name}-{age}
        </h2>
        <HomeInfo />
        <HomeBanner/>
      </div>
    );
  }
}

export default Home;
```

> 孙组件

```jsx
import React, { Component } from "react";
import ThemeContext from "./context/theme-context";
import UserContext from "./context/user-context";

export class HomeInfo extends Component {
  render() {
    // 四、获取数据，并且使用数据
    console.log(this.context);
    return (
      <div>
        {/* 方法一：通过context获取 共享数据 */}
        HomeInfo：{this.context.color}
        {/* 方法二：通过Consumer获取共享数据 */}
        <UserContext.Consumer>
          {(value) => {
            return <h2>Info User：{value.nickname}</h2>;
          }}
        </UserContext.Consumer>
      </div>
    );
  }
}

// 三、设置组件的contextType为某一个Context
HomeInfo.contextType = ThemeContext;

export default HomeInfo;
```



#### 函数组件调用

- 函数组件就只能通过Consumer获取共享数据

```jsx
import ThemeContext from "./context/theme-context";

function HomeBanner() {
  return (
    <div>
      <span>HomeBanner</span>
      {/* 函数式组件中使用Context共享的数据 */}
      <ThemeContext.Consumer>
        {/* 传入一个children */}
        {(value) => {
          return <h2>HomeBanner theme: {value.color}</h2>;
        }}
      </ThemeContext.Consumer>
    </div>
  );
}

export default HomeBanner;
```



### 事件总线eventBus

- 如果一个组件想要发送数据或者事件到其他组件，那就要用到事件总线eventBus
- pnpm install hy-event-store
- 调用后，用eventBus.emit()发送数据
- 用eventBus.on()监听数据

> event-bus.js

```js
import { HYEventBus } from "hy-event-store"

const eventBus = new HYEventBus()

export default eventBus
```



> HomeBanner.jsx

```jsx
import React, { Component } from "react";
import eventBus from "./utils/event-bus";

export class HomeBanner extends Component {
  preClick() {
    console.log("preClick");
    // 事件名称，数据
    eventBus.emit("bannerPrev", "why", 18, 1.88);
  }
  nextClick() {
    console.log("nextClick");
    eventBus.emit("bannerNext", { name: "kobe", age: 30 });
  }
  render() {
    const { nextClick, preClick } = this;
    return (
      <div>
        <h2>HomeBanner</h2>
        <button onClick={(e) => preClick()}>上一个</button>
        <button onClick={(e) => nextClick()}>下一个</button>
      </div>
    );
  }
}

export default HomeBanner;
```



> App.jsx

```jsx
import React, { Component } from "react";
import Home from "./Home";
import eventBus from "./utils/event-bus";

export class App extends Component {
  constructor() {
    super();
    this.state = {
      name: "",
      age: 0,
      height: 0,
    };
  }
  componentDidMount() {
    // 事件名称，绑定方法，绑定this
    eventBus.on("bannerPrev", this.bannerPrevClick, this);
    eventBus.on("bannerNext", this.bannerNextClick, this);
  }

  bannerPrevClick = (name, age, height) => {
    console.log("App中监听到bannerPrev");
    this.setState({
      name,
      age,
      height,
    });
  };
  bannerNextClick(info) {
    console.log("bannerNextClick：", info);
  }

  componentWillUnmount() {
    eventBus.off("bannerPrev", this.bannerPrevClick);
  }

  render() {
    const { name, age, height } = this.state;
    return (
      <div>
        <h2>
          App Component:{name}-{age}-{height}
        </h2>
        <Home />
      </div>
    );
  }
}

export default App;
```



## 五、React优化

### Vue和React的数据管理和界面渲染的对比

- Vue已经将render函数封装好了，只需要对数据进行劫持，监听他的变化再执行render函数
- React没有做数据劫持而是将这一切交给程序员来进行判断，用setState进行数据更新，重新渲染

![image-20221024143911964](http://img.roydust.top/img/202210241439051.png)

#### 为什么React要使用setState

- 开发中我们并不能直接通过修改state的值来让界面发生更新：
  - 因为我们修改了state之后，希望React根据最新的State来重新渲染界面，但是这种方式的修改React并不知道数据发生了变化；
  - React并没有实现类似于Vue2中的Object.defineProperty或者Vue3中的Proxy的方式来监听数据的变化；
  - 我们必须通过setState来告知React数据已经发生了变化；
- 疑惑：在组件中并没有实现setState的方法，为什么可以调用呢？
  - 原因很简单，setState方法是从Component中继承过来的。

![image-20221024144808589](http://img.roydust.top/img/202210241448660.png)



### setState的详细使用

#### setState原理

- 将新obj和旧obj合并

![image-20221024185056258](http://img.roydust.top/img/202210241850359.png)



#### setState用法

1. 基本使用

```jsx
    // 1.基本使用
    this.setState({
      message: "aaa  ",
    });
```



2. setState可以传入一个回调函数

```jsx
    // 2.setState可以传入一个回调函数
    // 好处一：可以在回调函数中编写新的state的逻辑
    // 好处二：当前的回调函数会将之前的state和props传递进来
    this.setState((state, props) => {
      // 1.编写一些对新的state处理逻辑
      // 2.可以获取我们之前的state和props值
      console.log(state);
      console.log(props);
      return {
        message: "bbb",
      };
    });
```



3. setState在React的事件处理中是一个异步调用

```jsx
    // 3.setState在React的事件处理中是一个异步调用
    // 如果希望在数据更新之后(数据合并),获取到对应的结果执行一些逻辑代码
    // 那么可以在setState中传入第二个参数：callback
    this.setState(
      {
        message: "你好，世界",
      },
      () => {
        console.log("+++++++++++", this.state.message); // +++++++++++ 你好，世界
      }
    );
    console.log("---------", this.state.message);	// --------- Hello World
```



### setState异步更新



- 为什么setState设计为异步呢？
  - setState设计为异步其实之前在GitHub上也有很多的讨论；
  - React核心成员（Redux的作者）Dan Abramov也有对应的回复，有兴趣的同学可以参考一下；
  - https://github.com/facebook/react/issues/11527#issuecomment-360199710；
- 我对其回答做一个简单的总结：
- setState设计为异步，可以**显著的提升性能**；
  - 如果每次调用 setState都进行一次更新，那么意味着render函数会被频繁调用，界面重新渲染，这样效率是很低的；
  - **最好的办法应该是获取到多个更新，之后进行批量更新**；
- **如果同步更新了state，但是还没有执行render函数，那么state和props不能保持同步**；
  - state和props不能保持一致性，会在开发中产生很多的问题；

![image-20221024192031804](http://img.roydust.top/img/202210241920896.png)

```jsx
import React, { Component } from "react";

function Hello(props) {
  // 如果message在父组件更新了，但是没有执行render函数，所以父组件的state和传递给子组件的props数据不一致会出问题
  return <h2>{props.message}</h2>;
}

export class App extends Component {
  constructor() {
    super();
    this.state = {
      message: "Hello World",
      counter: 0,
    };
  }

  changeText() {
    this.setState({
      message: "aaa  ",
    });
  }
  increment() {
    this.setState({
      counter: this.state.counter + 1,
    });
    this.setState({
      counter: this.state.counter + 1,
    });
    this.setState({
      counter: this.state.counter + 1,
    });
    // counter结果为1

    this.setState((state) => {
      return {
        counter: state.counter + 1,
      };
    });
    this.setState((state) => {
      return {
        counter: state.counter + 1,
      };
    });
    this.setState((state) => {
      return {
        counter: state.counter + 1,
      };
    });
    // counter结果为3
  }

  render() {
    console.log("render函数被执行");
    const { message, counter } = this.state;
    return (
      <div>
        <h2>message:{message}</h2>
        <button onClick={(e) => this.changeText()}>修改文本</button>
        <h2>当前计数：{counter}</h2>
        <button onClick={(e) => this.increment()}>counter+1</button>

        <Hello message={message} />
      </div>
    );
  }
}

export default App;
```



#### **setState一定是异步吗？**

**在React18以前**

其实分成两种情况：

- 在组件生命周期或React合成事件中，setState是异步；
- 在setTimeout或者原生dom事件中，setState是同步；

验证一：在setTimeout中的更新：

![image-20221024200324155](http://img.roydust.top/img/202210242003204.png)

证二：原生DOM事件：

![image-20221024200404122](http://img.roydust.top/img/202210242004166.png)



**在React18以后**

- 在React18之后，默认所有的操作都被放到了批处理中（异步处理）

![image-20221024200445124](http://img.roydust.top/img/202210242004172.png)

- 如果希望代码可以同步会拿到，则需要执行特殊的flushSync操作：

```jsx
	hangeText() {
    setTimeout(() => {
      // 在React18之前，setTimeout中setState操作，是同步操作
      // 在React18之后，setTimeout中setState都是异步操作(批处理)

      // React18之后的同步更新方法flushSync
      flushSync(() => {
        this.setState({ message: "你好啊，洛依尘" });
      });
      console.log(this.state.message);
    }, 0);
  }
```

 

### React性能优化

#### React的更新机制

![image-20221025133039576](http://img.roydust.top/img/202210251330672.png)

**React在props或state发生改变时，会调用React的render方法，会创建一颗不同的树。**

- React需要基于这两颗不同的树之间的差别来判断如何有效的更新UI:
  - 如果-棵树参考另外-棵树进行完全比较更新,那么即使是最先进的算法，该算法的复杂程度为0(n3),其中n是树中元素的数量;
  - https://qrfia.dlsi.ua.es/m/algorithms/references/editsurvey bille.pdf;
  - 如果在React中使用了该算法，那么展示1000个元素所需要执行的计算量将在十亿的量级范围;
  - 这个开销太过昂贵了，React的更新性能会变得非常低效;
- 于是，React对这个算法进行了优化，将其优化成了O(n),如何优化的呢?
  - 同层节点之间相互比较,不会垮节点比较;
  - 不同类型的节点，产生不同的树结构;
  - 开发中，可以通过key来指定哪些节点在不同的渲染下保持稳定;

![image-20221025135628736](http://img.roydust.top/img/202210251356790.png)

#### Keys的优化

- 方法一：在最后的位置插入数据
  - 这种情况，有无key意义不大
- 方法二：在前面插入数据
  - 这种做法，在没有key的情况下，所有的子元素都要进行修改
- 当子元素拥有key时，React使用key来匹配原有树上的子元素以及最新树上的子元素
- key的注意事项
  - key应该是唯一 的;
  - key不要使用随机数(随机数在下一 次render时， 会重新生成一 个数字) ;
  - 使用index作为key,对性能是没有优化的;



#### render函数SCU优化

- 我们可以思考一下，在以后的开发中，我们只要是修改了App中的数据，所有的组件都需要重新render,进行diff算法，性能必然是很低的:
  - 事实上，很多的组件没有必须要重新render;
  - 它们调用render应该有一个前提，就是依赖的数据(state、props)发生改变时，再调用自己的render方法;
- 如何来控制render方法是否被调用呢?
  - 通过shouldComponentUpdate方法即可,但是这样所有的改变都不会去调用render函数了



 **shouldComponentUpdate**

- React给我们提供了-个生命周期方法shouldComponentUpdate (很多时候，我们简称为SCU) , 这个方法接受参数，并且需要有返回值:
- 该方法有两个参数:
  - 参数一: nextProps修改之后，最新的props属性
  - 参数二: nextState修改之后，最新的state属性
- 该方法返回值是一个boolean类型:
  - 返回值为true,那么就需要调用render方法;
  - 返回值为false,那么久不需要调用render方法;
  - 默认返回的是true,也就是只要state发生改变,就会调用render方法;
- 比如我们在App中增加一个message属性:
  - jsx中并没有依赖这个message,那么它的改变不应该引|起重新渲染;
  - 但是因为render监听到state的改变，就会重新render, 所以最后render方法还是被重新调用了;

> App.jsx

```jsx
 shouldComponentUpdate(nextProps, newState) {
    // App进行性能优化的点
    if (
      this.state.message !== newState.message ||
      this.state.counter !== newState.counter
    ) {
      return true;
    }
    return false;
  }

	
  render() {
    const { message, counter } = this.state;
    console.log("App render");
    return (
      <div>
        <h2>
          App-{message}-{counter}
        </h2>
        <button onClick={(e) => this.changeText()}>修改文本</button>
        <button onClick={(e) => this.increment()}>counter+1</button>
        <Home message={message} />
        <Recommend counter={counter} />
      </div>
    );
  }
```

> Home.jsx

```jsx
shouldComponentUpdate(newProps, nextState) {
    // 自己对比state是否发生改变：this.state和nextState
    if (this.props.message !== newProps.message) {
      return true;
    }
    return false;
  }

  render() {
    console.log("Home render");
    return (
      <div>
        <h2>Home Page:{this.props.message}</h2>
      </div>
    );
  }
```



#### PureComponent和memo

- 如果所有的类，我们都需要手动来实现shouldComponentUpdate,那么会给我们开发者增加非常多的工作量。

  - 我们来设想一下shouldComponentUpdate中的各种判断的目的是什么?
  - props或者state中的数据是否发生了改变,来决定shouldComponentUpdate返回true或者false;

- 事实上React已经考虑到了这一点，所以React已经默认帮我们实现好了，如何实现呢?

  - 将class继承自PureComponent.

  ![image-20221025171936958](http://img.roydust.top/img/202210251719058.png)

- class继承自PureComponent后该class就会自动判断render函数是否需要渲染

```jsx
import React, { PureComponent } from "react";
export class App extends PureComponent {
}
```

**但是函数组件怎么处理render函数渲染问题**

- 引入react中的memo方法

```jsx
// 函数组件怎么处理render函数渲染问题
import { memo } from "react";

const Profile = memo(function Profile(props) {
  console.log("Profile render");
  return <h2>Profile:{props.message}</h2>;
});

export default Profile;
```



#### 数据不可变的力量

不可变数据的力量（The Power Of Not Mutating Data）代表的就是不可变数据设计原则。

React的生命周期中每次调用ComponentShouldUpdate()会获取props/state，利用现有的数据跟将要改变的数据进行比较,更新变化的数据并进行渲染。此举最大限度减少不必要的更新，达到性能优化的目的。因此，使用时不建议直接更改state里面的数据，而是通过setState去改变参数。

##### 案例：

```jsx
import React, { PureComponent } from "react";

export class App extends PureComponent {
  constructor() {
    super();
    this.state = {
      books: [
        { name: "你不知道的JS", price: 99, count: 1 },
        { name: "你不知道的Java", price: 69, count: 1 },
        { name: "你不知道的Python", price: 49, count: 3 },
        { name: "你不知道的Go", price: 79, count: 2 },
      ],
      friend: {
        name: "kobe",
      },
    };
  }
  // shouldComponentUpdate(nextProps, nextState) {
  //   shallowEqual(nextProps, this.props);
  //   shallowEqual(nextState, this.state);
  // }

  addNewBook() {
    const newBook = { name: "高级JS程序设计", price: 78, count: 3 };
    // 1.直接修改原有的state,重新设置一遍
    // 在PureComponent是不能引入重现渲染（re-render）
    this.state.books.push(newBook);

    // 2.赋值一份books，在新books中修改，设置新的books
    const books = [...this.state.books];
    books.push(newBook);

    this.setState({ books: books });
  }

  addBookCount(index) {
    const books = [...this.state.books];
    books[index].count++;
    this.setState({
      books,
    });
  }

  render() {
    const { books } = this.state;
    return (
      <div>
        <h2>数据展示</h2>
        <ul>
          {books.map((item, index) => {
            return (
              <li key={index}>
                <span>
                  name:{item.name}-price:{item.price}-count:{item.count}
                </span>
                <button onClick={(e) => this.addBookCount(index)}>+1</button>
              </li>
            );
          })}
        </ul>
        <button onClick={(e) => this.addNewBook()}>添加新书籍</button>
      </div>
    );
  }
}

export default App;
```

**如果直接修改原有的state,重新设置一遍在PureComponent是不能引入重现渲染**

因为在PureComponent源码中会先判断新的state和旧的state是否为同一地址，再去判断state里面的东西是否一致，而我们再直接进行push的时候，不会改变原函数的首地址，因此首地址相同。那么books就等于this.state.books，被判定为数据没有发生改变，也就不会执行更新操作了。

##### **PureComponent的检查是否要更新render函数的源码**

![image-20221026002546263](http://img.roydust.top/img/202210260025364.png)

- shallowequal只是做了一层浅层比较

![image-20221026002914278](http://img.roydust.top/img/202210260029377.png)



### 获取DOM方式refs

如果需要对DOM进行操作可以使用ref

当前有三种ref获取DOM的方式

- 第一种，字符串获取
  使用时通过 this.refs.传入的字符串获取对应元素
- 第二种，传入对象获取
  通过 React.createRef() 创建对象
  使用时获取创建的对象，其中有一个current属性就是对应的元素
- 第三种，传入函数获取
  该函数会在DOM被挂载时进行回调，函数会传入一个元素对象，可以自己保存
  使用时，直接使用保存的元素对象即可

```jsx
import React, { PureComponent, createRef } from "react";

export class App extends PureComponent {
  constructor() {
    super();

    this.titleRef = createRef();
    this.titleEl = null;
  }
  getNativeDOM() {
    // 1.在React元素上绑定一个ref字符串
    console.log(this.refs.lyc);

    // 2.提前创建好ref对象，createRef()，将创建出来的对象绑定到元素上
    console.log(this.titleRef.current);

    // 3.传入一个回调函数，在对应的元素被渲染之后，回调函数被执行，并且将元素传入
    console.log(this.titleEl);
  }
  render() {
    return (
      <div>
        <h2 ref="lyc">Hello World</h2>
        <h2 ref={this.titleRef}>你好啊，洛依尘</h2>
        <h2
          ref={(el) => {
            this.titleEl = el;
          }}
        >
          你好啊，小师妹
        </h2>
        <button onClick={(e) => this.getNativeDOM()}>获取DOM</button>
      </div>
    );
  }
}

export default App;
```

根据官方更新的进程，第一种字符串方式可能在未来被移除，所以这边优先推荐使用第二、第三种方式来获取要操作的DOM

**ref类型**的值根据节点的类型而有所不同

- 当 ref 属性用于 HTML 元素时，构造函数中使用 React.createRef() 创建的 ref 接收底层 DOM 元素作为其 current 属性
- 当 ref 属性用于自定义 class 组件时，ref 对象接收组件的挂载实例作为其 current 属性
- 不能在函数组件上使用 ref 属性，因为他们没有实例

因此，可以在一个组件内通过ref调用另外一个组件的方法（*挺像vue中this.$ref来调用其他组件中方法的*）

```jsx
import React, { PureComponent, createRef } from "react";

class HelloWorld extends PureComponent {
  test() {
    console.log("子组件的方法");
  }
  render() {
    return <h2>Hello World</h2>;
  }
}

export class App extends PureComponent {
  constructor() {
    super();

    this.hwRef = createRef();
  }
  getComponent() {
    console.log(this.hwRef.current);
    this.hwRef.current.test();
  }
  render() {
    return (
      <div>
        <HelloWorld ref={this.hwRef} />
        <button onClick={(e) => this.getComponent()}>获取组件实例</button>
      </div>
    );
  }
}

export default App;
```

如果是ref想要绑定函数组件内部元素呢？

- 那就必须要用forwardRef方法来包裹函数组件，并且转发绑定ref

```jsx
import React, { PureComponent, createRef, forwardRef } from "react";

const HelloWorld = forwardRef(function (props, ref) {
  // 获取传递过来的props和ref，并且将ref绑定在想要的的DOM上
  return (
    <div>
      <h2 ref={ref}>Hello World</h2>
      <p>哈哈哈</p>
    </div>
  );
});

export class App extends PureComponent {
  constructor() {
    super();

    this.hwRef = createRef();
  }
  getComponent() {
    console.log(this.hwRef.current);
  }
  render() {
    return (
      <div>
        <HelloWorld ref={this.hwRef} />
        <button onClick={(e) => this.getComponent()}>获取组件实例</button>
      </div>
    );
  }
}

export default App;
```



### 受控和非受控组件

#### 受控组件

**React中表单元素交由框架内部的state中处理**

而在React中，可变状态(mutable state)通常保存在组件的state属性中，并且只能通过使用setState()来更新。

- 我们将两者结合起来，**使React的state成为 “唯一数据源”**;
- 渲染表单的React组件还控制着用户输入过程中表单发生的操作;
- 被React以这种方式控制取值的表单输入元素就叫做“ 受控组件”;

```jsx
import React, { PureComponent } from "react";

export class App extends PureComponent {
  constructor() {
    super();
    this.state = {
      username: "123",
    };
  }
  inputChange(e) {
    console.log("inputChange:", e.target.value);
    this.setState({
      username: e.target.value,
    });
  }
  render() {
    const { username } = this.state;
    return (
      <div>
        {/* 受控组件 value绑定state中，无法改变内容，只能通过onClick来改变state */}
        <input
          type="text"
          value={username}
          onChange={(e) => this.inputChange(e)}
        />
        <h2>username:{username}</h2>
      </div>
    );
  }
}

export default App;
```

在这个用例中，先通过onChange监听获取input中的value，再将value赋给state，state发生改变后，主动再将state的数据重新赋给一次input。

这种通过state作为组件唯一数据源并且时刻保持state和value双向绑定的组件，就是受控组件，该案例是受控组件的一种基本使用形式。

`注意：这种双向绑定并非双向数据流，而是一种单向数据流`

#### 非受控组件

**表单数据交由DOM节点来处理**

官方不建议使用非受控组件来处理表单数据

一般由ref方式来获取表单数据，例如：

```jsx
import React, { PureComponent } from "react";

export class App extends PureComponent {
  constructor() {
    super();
    this.state = {
      username: "123",
    };
  }
  inputChange(e) {
    console.log("inputChange:", e.target.value);
    this.setState({
      username: e.target.value,
    });
  }
  render() {
    const { username } = this.state;
    return (
      <div>
        {/* 非受控组件 */}
        <input type="text" onChange={(e) => this.inputChange(e)} />
        <h2>username:{username}</h2>
      </div>
    );
  }
}

export default App;
```

此处通过this.[refObject].current.value来获取表单中的数据。



#### 表单组件的使用

![image-20221026205228522](http://img.roydust.top/img/202210262052594.png)

- 在 HTML 中，表单元素（如<input/>、 <textarea/> 和 <select/>）之类的表单元素通常自己维护 state，并根据用户输入进行更新
- 由于在表单元素上设置了 value 属性，因此显示的值将始终为 this.state.value，这使得 React 的 state 成为唯一数据源。
- 由于 handleUsernameChange 在每次按键时都会执行并更新 React 的 state，因此显示的值将随着用户输入而更新

```jsx
import React, { PureComponent } from "react";

export class App extends PureComponent {
  constructor() {
    super();
    this.state = {
      username: "123",
      password: "",
    };
  }
  handleSubmitClick(event) {
    // 1.阻止默认的行为
    event.preventDefault();
    // 2.获取到所有的表单数据，对数据进行组件
    console.log(this.state.username, this.state.password);
    // 3.以网络请求的方式，将数据传递给服务器
  }

  handleInputChange(event) {
    this.setState({
      [event.target.name]: event.target.value,
    });
  }

  render() {
    const { username, password } = this.state;
    return (
      <div>
        <form onSubmit={(e) => this.handleSubmitClick(e)}>
          <label htmlFor="username">
            用户：
            <input
              type="text"
              id="username"
              name="username"
              value={username}
              onChange={(e) => this.handleInputChange(e)}
            />
          </label>
          <label htmlFor="password">
            密码：
            <input
              type="text"
              id="password"
              name="password"
              value={password}
              onChange={(e) => this.handleInputChange(e)}
            />
          </label>
          <button type="submit">提交</button>
        </form>
      </div>
    );
  }
}

export default App;
```

#### **checkbox的单选和多选**

```jsx
  // 监听单选改变
  handleAgreeChange(event) {
    console.log(event.target.checked);
    this.setState({
      isAgree: event.target.checked,
    });
  }

  // 监听多选改变
  handleHobbiesChange(event, index) {
    const hobbies = [...this.state.hobbies];
    hobbies[index].isChecked = event.target.checked;
    this.setState({ hobbies });
  }



          {/* 2.checkbox单选 */}
          <label htmlFor="agree">
            <input
              id="agree"
              type="checkbox"
              checked={isAgree}
              onChange={(e) => this.handleAgreeChange(e)}
            />
            同意协议
          </label>

          {/* 3.checkbox多选 */}
          <div>
            您的爱好：
            {hobbies.map((item, index) => {
              return (
                <label htmlFor={item.value} key={item.value}>
                  <input
                    type="checkbox"
                    id={item.value}
                    checked={item.isChecked}
                    onChange={(e) => this.handleHobbiesChange(e, index)}
                  />
                  <span>{item.text}</span>
                </label>
              );
            })}
          </div>
```

#### Select的单选和多选

```jsx
  // 监听多选选择框的改变
  handleFruitChange(event) {
    const options = Array.from(event.target.selectedOptions);
    const values = options.map((item) => item.value);
    console.log(values);
    this.setState({
      fruit: values,
    });

    // 额外补充：Array.from(可迭代对象)
    // Array.from(arguments);
    const values2 = Array.from(
      event.target.selectedOptions,
      (item) => item.value
    );  
    console.log(values2);
  }


          {/* 4.select元素 */}
          <select
            name=""
            id=""
            value={fruit}
            onChange={(e) => this.handleFruitChange(e)}
            multiple
          >
            <option value="apple">苹果</option>
            <option value="orange">橘子</option>
            <option value="banana">香蕉</option>
          </select>
```

#### 非受控组件

◼ **React推荐大多数情况下使用 受控组件 来处理表单数据：**

-  一个受控组件中，表单数据是由 React 组件来管理的；

- 另一种替代方案是使用非受控组件，这时表单数据将交由 DOM 节点来处理；

◼ **如果要使用非受控组件中的数据，那么我们需要使用 ref 来从DOM节点中获取表单数据。**

- 我们来进行一个简单的演练：

- 使用ref来获取input元素；

◼ **在非受控组件中通常使用defaultValue来设置默认值；**

◼ **同样，<input type="checkbox"> 和 <input type="radio"> 支持 defaultChecked，<select> 和 <textarea> 支持 defaultValue。**

```jsx
  constructor() {
    super();
    this.state = {
      intro: "哈哈哈",
    };
    this.introRef = createRef();
  }



          {/* 5.非受控组件 */}
          <input type="text" defaultValue={intro} ref={this.introRef} />
```





### React的高阶组件

#### 什么是高阶组件，**高阶组件的定义**？

1.高阶组件本身不是一个组件,而是一个函数
2.特点:

- 接受一个组件作为它的参数
- 返回一个新的组件

**高阶组件的调用过程类似于这样：**

```js
const Home = enhancedUserInfo(function (props) {
  return (
    <h2>
      Home:{props.name}-{props.level}-{props.banners}
    </h2>
  );
});
```

**高阶函数的编写过程类似于这样：**

```js
import ThemeContext from "../context/theme_context"

function withTheme(OriginComponment) {
  return props => {
    return (
      <ThemeContext.Consumer>
        {
          value => {
            return <OriginComponment {...value} {...props} />
          }
        }
      </ThemeContext.Consumer>
    )
  }
}

export default withTheme
```

**组件的名称问题：**

- 在ES6中，类表达式中类名是可以省略的；

- 组件的名称都可以通过displayName来修改；

**注意：**

**高阶组件并不是React API的一部分，它是基于React的组合特性而形成的设计模式**

- **高阶组件在一些React第三方库中非常常见：**
  - 比如redux中的connect；
  - 比如react-router中的withRouter；



#### 高阶组件的应用

##### **props的增强**

- **不修改原有代码的情况下，添加新的props**

- **利用高阶组件来共享Context**

> enhanced_props.js  HOC高阶组件

```js
import React, { PureComponent } from 'react'
// 定义组件：给需要特殊数据的组件，注入props
function enhancedUserInfo(OriginComponent) {
  class NewComponent extends PureComponent {
    constructor(props) {
      super(props);

      this.state = {
        userInfo: {
          name: "lyc",
          level: 99,
        },
      };
    }

    render() {
      return <OriginComponent {...this.props} {...this.state.userInfo} />;
    }
  }
  return NewComponent;
}

export default enhancedUserInfo
```

> App.jsx

```jsx
import React, { Profiler, PureComponent } from "react";

import enhancedUserInfo from "./hoc/enhanced_props";
import About from "./pages/About";

const Home = enhancedUserInfo(function (props) {
  return (
    <h2>
      Home:{props.name}-{props.level}-{props.banners}
    </h2>
  );
});
const Profile = enhancedUserInfo(function (props) {
  return (
    <h2>
      Profile:{props.name}-{props.level}
    </h2>
  );
});

const HelloFriend = enhancedUserInfo(function (props) {
  return (
    <h2>
      HelloFriend:{props.name}-{props.level}
    </h2>
  );
});

export class App extends PureComponent {
  render() {
    return (
      <div>
        <Home banners={["轮播图1", "轮播图2"]} />
        <Profile />
        <HelloFriend />
        <About />
      </div>
    );
  }
}

export default App;
```



##### **渲染判断鉴权**

- **在开发中，我们可能遇到这样的场景：**
  - 某些页面是必须用户登录成功才能进行进入；
  - 如果用户没有登录成功，那么直接跳转到登录页面；

- **这个时候，我们就可以使用高阶组件来完成鉴权操作：**

> login_auth.js

```js
function loginAuth(OriginComponent) {
  return props => {
    // 从localStorage中获取token
    const token = localStorage.getItem("token")
    if (token) {
      return <OriginComponent {...props} />
    } else {
      return <h2>请先登录，再进行操作</h2>
    }
  }
}

export default loginAuth
```

> Cart.jsx

如果需要鉴权的组件就用loginAuth包裹一下

```jsx
import React, { PureComponent } from "react";
import loginAuth from "../hoc/login-auth";

export class Cart extends PureComponent {
  render() {
    return <h1>Cart</h1>;
  }
}

export default loginAuth(Cart);
```

> App.jsx

```jsx
import React, { PureComponent } from "react";
import Cart from "./pages/Cart";

export class App extends PureComponent {
  loginClick() {
    localStorage.setItem("token", "lyc");

    // 强制刷新
    this.forceUpdate();
  }

  render() {
    return (
      <div>
        App
        <button onClick={(e) => this.loginClick()}>登录</button>
        <Cart />
      </div>
    );
  }
}

export default App;
```



##### **生命周期劫持**

- **我们也可以利用高阶函数来劫持生命周期，在生命周期中完成自己的逻辑：**

> log_render_time.js

```js
import { PureComponent } from "react";

function logRenderTime(OriginComponent) {
  // 匿名类
  return class NewComponent extends PureComponent {
    // 已废弃的生命周期，仅作测试使用
    UNSAFE_componentWillMount() {
      this.beginTime = new Date().getTime();
    }
    componentDidMount() {
      this.endTime = new Date().getTime();
      const interval = this.endTime - this.beginTime;
      console.log(`当前${OriginComponent.name}页面渲染花费了${interval}ms渲染完成`);
    }
    render() {
      return <OriginComponent {...this.props} />
    }
  }
}
export default logRenderTime
```

> Detail.jsx

如果需要测试渲染时间的组件就用logRenderTime包裹一下

```jsx
import React, { PureComponent } from "react";
import logRenderTime from "../hoc/log_render_time";

export class Detail extends PureComponent {
  render() {
    return (
      <div>
        <h2>Detail Page</h2>
        <ul>
          <li>数据列表1</li>
          <li>数据列表2</li>
          <li>数据列表3</li>
        </ul>
      </div>
    );
  }
}

export default logRenderTime(Detail);
```



#### **高阶函数的意义**

- **我们会发现利用高阶组件可以针对某些React代码进行更加优雅的处理。**

- **其实早期的React有提供组件之间的一种复用方式是mixin，目前已经不再建议使用：**
  - Mixin 可能会相互依赖，相互耦合，不利于代码维护； 
  - 不同的Mixin中的方法可能会相互冲突； 
  - Mixin非常多时，组件处理起来会比较麻烦，甚至还要为其做相关处理，这样会给代码造成滚雪球式的复杂性；

- **当然，HOC也有自己的一些缺陷：**
  - HOC需要在原组件上进行包裹或者嵌套，如果大量使用HOC，将会产生非常多的嵌套，这让调试变得非常困难； 
  - HOC可以劫持props，在不遵守约定的情况下也可能造成冲突； 

- **Hooks的出现，是开创性的，它解决了很多React之前的存在的问题**
  -  比如this指向问题、比如hoc的嵌套复杂度问题等等；

- 其实我们可以发现很多React封装的高阶函数本质上也是高阶组件
  - 例如支持函数组件灵活渲染的memo高阶函数和ref的转发的orwardRef高阶函数





### Portals和Fragment

#### Portals

◼ **某些情况下，我们希望渲染的内容独立于父组件，甚至是独立于当前挂载到的DOM元素中（默认都是挂载到id为root的DOM元素上的）。**

◼ **Portal 提供了一种将子节点渲染到存在于父组件以外的 DOM 节点的优秀的方案：**

- 第一个参数（child）是任何可渲染的 React 子元素，例如一个元素，字符串或 fragment； 

- 第二个参数（container）是一个 DOM 元素； 

![image-20221027201939286](http://img.roydust.top/img/202210272019396.png)

◼ **通常来讲，当你从组件的 render 方法返回一个元素时，该元素将被挂载到 DOM 节点中离其最近的父节点：**

◼ **然而，有时候将子元素插入到 DOM 节点中的不同位置也是有好处的**

```jsx
    return (
      <div className="app">
        <h1>App H1</h1>
        {createPortal(<h2>App H2</h2>, document.querySelector("#lyc"))}
      </div>
    );
```



##### **Modal组件案例**

- **比如说，我们准备开发一个Modal组件，它可以将它的子组件渲染到屏幕的中间位置：**
  - 步骤一：修改index.html添加新的节点
  - 步骤二：编写这个节点的样式
  - 步骤三：编写组件代码

```jsx
    <div id="modal"></div>

    <style>
      #modal {
        position: fixed;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
      }
    </style>

import React, { PureComponent } from "react";
import { createPortal } from "react-dom";

export class Modal extends PureComponent {
  render() {
    return createPortal(this.props.children, document.querySelector("#modal"));
  }
}

export default Modal;
```

#### Fragment

◼ **在之前的开发中，我们总是在一个组件中返回内容时包裹一个div元素**

◼ **我们又希望可以不渲染这样一个div应该如何操作呢？**

- 使用Fragment

- Fragment 允许你将子列表分组，而无需向 DOM 添加额外节点；

◼ **React还提供了Fragment的短语法：**

- 它看起来像空标签 <> </>； 

- 但是，如果我们需要在Fragment中添加key，那么就不能使用短语法

```jsx
import React, { PureComponent, Fragment } from "react";

export class App extends PureComponent {
  constructor() {
    super();

    this.state = {
      sections: [
        { title: "哈哈哈", content: "我是内容，哈哈哈" },
        { title: "嘿嘿嘿", content: "我是内容，嘿嘿嘿" },
        { title: "呵呵呵", content: "我是内容，呵呵呵" },
        { title: "嘻嘻嘻", content: "我是内容，嘻嘻嘻" },
      ],
    };
  }
  render() {
    const { sections } = this.state;
    return (
      <div>
        <>
          <h2>我的App的标题</h2>
          <p>我是App的内容,哈哈哈</p>
          <hr />
          {sections.map((item) => {
            return (
              <Fragment key={item.title}>
                <h2>{item.title}</h2>
                <p>{item.content}</p>
              </Fragment>
            );
          })}
        </>
      </div>
    );
  }
}

export default App;
```

![image-20221027204617127](http://img.roydust.top/img/202210272046180.png)





### StrictMode严格模式

◼ **StrictMode 是一个用来突出显示应用程序中潜在问题的工具：**

- 与 Fragment 一样，StrictMode 不会渲染任何可见的 UI； 
- 它为其后代元素触发额外的检查和警告；
- 严格模式检查仅在开发模式下运行；*它们不会影响生产构建*； 

◼ **可以为应用程序的任何部分启用严格模式：**

- 不会对 Header 和 Footer 组件运行严格模式检查；
- 但是，ComponentOne 和 ComponentTwo 以及它们的所有后代元素都将进行检查；

```jsx
      <div>
        <StrictMode>
          <Home />
        </StrictMode>
        <Profile />
      </div>
```



#### **严格模式检查的是什么？**

1. 识别不安全的生命周期：

2. 使用过时的ref API

3. 检查意外的副作用
   - 这个组件的constructor会被调用两次；
   - 这是严格模式下故意进行的操作，让你来查看在这里写的一些逻辑代码被调用多次时，是否会产生一些副作用；
   - 在生产环境中，是不会被调用两次的；

4. 使用废弃的findDOMNode方法
   - 在之前的React API中，可以通过findDOMNode来获取DOM，不过已经不推荐使用了，可以自行学习演练一下

5. 检测过时的context API
   - 早期的Context是通过static属性声明Context对象属性，通过getChildContext返回Context对象等方式来使用Context的；
   - 目前这种方式已经不推荐使用，大家可以自行学习了解一下它的用法；

![image-20221028164840792](http://img.roydust.top/img/202210281648850.png)



## 六、React中的CSS使用

### React的过渡动画

**◼ 在开发中，我们想要给一个组件的显示和消失添加某种过渡动画，可以很好的增加用户体验。**

◼ **当然，我们可以通过原生的CSS来实现这些过渡动画，但是React社区为我们提供了react-transition-group用来完成过渡动画。**

◼ **React曾为开发者提供过动画插件 react-addons-css-transition-group，后由社区维护，形成了现在的 react-transitiongroup。** 

- 这个库可以帮助我们方便的实现组件的 入场 和 离场 动画，使用时需要进行额外的安装：

```
# npm
npm install react-transition-group --save
# yarn
yarn add react-transition-group
```

◼ **react-transition-group本身非常小，不会为我们应用程序增加过多的负担。**



**react-transition-group主要包含四个组件：**

- Transition
  - 该组件是一个和平台无关的组件（不一定要结合CSS）；
  - 在前端开发中，我们一般是结合CSS来完成样式，所以比较常用的是CSSTransition； 

- CSSTransition
  - 在前端开发中，通常使用CSSTransition来完成过渡动画效果

- SwitchTransition
  - 两个组件显示和隐藏切换时，使用该组件

- TransitionGroup
  - 将多个动画组件包裹在其中，一般用于列表中元素的动画；



#### CSSTransiton使用

◼ **CSSTransition是基于Transition组件构建的：**

◼ **CSSTransition执行过程中，有三个状态：appear、enter、exit；** 

◼ **它们有三种状态，需要定义对应的CSS样式：**

- 第一类，开始状态：对于的类是-appear、-enter、exit； 

- 第二类：执行动画：对应的类是-appear-active、-enter-active、-exit-active； 

- 第三类：执行结束：对应的类是-appear-done、-enter-done、-exit-done； 

◼ **CSSTransition常见对应的属性：**

◼ **in：触发进入或者退出状态**

- 如果添加了unmountOnExit={true}，那么该组件会在执行退出动画结束后被移除掉； 

- 当in为true时，触发进入状态，会添加-enter、-enter-acitve的class开始执行动画，当动画执行结束后，会移除两个class，并且添加-enter-done的class； 

- 当in为false时，触发退出状态，会添加-exit、-exit-active的class开始执行动画，当动画执行结束后，会移除两个class，并且添加-enter-done的class；



#### 常见的属性设置

◼ **classNames：动画class的名称**

- 决定了在编写css时，对应的class名称：比如card-enter、card-enter-active、card-enter-done； 

◼ **timeout：** 

- 过渡动画的时间

◼ **appear：** 

- 是否在初次进入添加动画（需要和in同时为true） 

◼ **unmountOnExit：退出后卸载组件**

◼ **其他属性可以参考官网来学习：**

- https://reactcommunity.org/react-transition-group/transition

◼ **CSSTransition对应的钩子函数：主要为了检测动画的执行过程，来完成一些JavaScript的操作**

- onEnter：在进入动画之前被触发；

- onEntering：在应用进入动画时被触发；

- onEntered：在应用进入动画结束后被触发；

> App.jsx

```jsx
import React, { createRef, PureComponent } from "react";
import { CSSTransition } from "react-transition-group";
import "./style.css";

export class App extends PureComponent {
  constructor() {
    super();

    this.state = {
      isShow: true,
    };
    this.sectionRef = createRef();
  }
  render() {
    const { isShow } = this.state;
    return (
      <div>
        <button onClick={(e) => this.setState({ isShow: !isShow })}>
          切换
        </button>
        {/* {isShow && <h2>哈哈哈</h2>} */}
        <CSSTransition
          nodeRef={this.sectionRef}
          in={isShow}
          unmountOnExit={true}
          classNames="lyc"
          timeout={2000}
          appear
          onEnter={(e) => console.log("开始进入动画")}
          onEntering={(e) => console.log("正在执行动画")}
          onEntered={(e) => console.log("执行进入结束")}
          onExit={(e) => console.log("开始离开动画")}
          onExiting={(e) => console.log("执行离开动画")}
          onExited={(e) => console.log("离开动画结束")}
        >
          <div className="section" ref={this.sectionRef}>
            <h2>哈哈哈</h2>
            <p>哈哈哈哈哈</p>
          </div>
        </CSSTransition>
      </div>
    );
  }
}

export default App;
```

> style.css

```css
/* 进入动画 */
/* .lyc-appear {
  transform: translateX(-150px);
}

.lyc-appear-active {
  transform: translateX(0);
  transition: transform 2s ease;
} */

.lyc-appear .lyc-enter {
  opacity: 0;
}

.lyc-appear-active .lyc-enter-active {
  opacity: 1;
  transition: opacity 2s ease;
}

/* 离开动画 */
.lyc-exit {
  opacity: 1;
}
.lyc-exit-active {
  opacity: 0;
  transition: opacity 2s ease;
}
```



#### SwitchTransition

◼ **SwitchTransition可以完成两个组件之间切换的炫酷动画：**

- 比如我们有一个按钮需要在on和off之间切换，我们希望看到on先从左侧退出，off再从右侧进入；

- 这个动画在vue中被称之为 vue transition modes； 

- react-transition-group中使用SwitchTransition来实现该动画；

◼ **SwitchTransition中主要有一个属性：mode，有两个值**

- in-out：表示新组件先进入，旧组件再移除；

- out-in：表示就组件先移除，新组建再进入；

◼ **如何使用SwitchTransition呢？**

- SwitchTransition组件里面要有CSSTransition或者Transition组件，不能直接包裹你想要切换的组件；

- SwitchTransition里面的CSSTransition或Transition组件不再像以前那样接受in属性来判断元素是何种状态，取而代之的是key属性；

> App.jsx

```jsx
import React, { PureComponent } from "react";
import { SwitchTransition, CSSTransition } from "react-transition-group";
import "./style.css";

export class App extends PureComponent {
  constructor() {
    super();

    this.state = {
      isLogin: true,
    };
  }
  render() {
    const { isLogin } = this.state;
    return (
      <div>
        <SwitchTransition mode="out-in">
          <CSSTransition
            key={isLogin ? "exit" : "login"}
            classNames="login"
            timeout={1000}
          >
            <button onClick={(e) => this.setState({ isLogin: !isLogin })}>
              {isLogin ? "退出" : "登录"}
            </button>
          </CSSTransition>
        </SwitchTransition>
      </div>
    );
  }
}

export default App;
```

> style.css

```css
.login-enter {
  transform: translateX(100px);
  opacity: 0;
}

.login-enter-active {
  transform: translateX(0);
  opacity: 1;
  transition: all 1s ease;
}

.login-exit {
  transform: translateX(0);
  opacity: 1;
}

.login-exit-active {
  transform: translateX(-100px);
  opacity: 0;
  transition: all 1s ease;
}
```



#### TransitionGroup

**当我们有一组动画时，需要将这些CSSTransition放入到一个TransitionGroup中来完成动画：**

> App.jsx

```jsx
import React, { PureComponent } from "react";
import { CSSTransition, TransitionGroup } from "react-transition-group";
import "./style.css";

export class App extends PureComponent {
  constructor() {
    super();

    this.state = {
      books: [
        { id: 111, name: "你不知道的JS", price: 99 },
        { id: 222, name: "JS高级程序设计", price: 89 },
        { id: 333, name: "Vue高级设计", price: 77 },
      ],
    };
  }

  addNewBook() {
    const books = [...this.state.books];
    books.push({
      id: new Date().getTime(),
      name: "React高级程序设计",
      price: 98,
    });
    this.setState({ books });
  }
  removeBoos(index) {
    const books = [...this.state.books];
    books.splice(index, 1);
    this.setState({ books });
  }

  render() {
    const { books } = this.state;
    return (
      <div>
        <h2>书籍列表：</h2>
        <TransitionGroup component="ul">
          {books.map((item, index) => {
            return (
              <CSSTransition key={item.id} classNames="book" timeout={1000}>
                <li>
                  {item.name}-{item.price}
                  <button onClick={(e) => this.removeBoos(index)}>删除</button>
                </li>
              </CSSTransition>
            );
          })}
        </TransitionGroup>
        <button onClick={(e) => this.addNewBook()}>添加新书籍</button>
      </div>
    );
  }
}

export default App;

```

> style.css

```css
.book-enter {
  transform: translateX(100px);
  opacity: 0;
}

.book-enter-active {
  transform: translateX(0);
  opacity: 1;
  transition: all 1s ease;
}

.book-exit {
  transform: translateX(0);
  opacity: 1;
}

.book-exit-active {
  transform: translateX(100px);
  opacity: 0;
  transition: all 1s ease;
}
```

 

### **React中CSS**

◼ **事实上，css一直是React的痛点，也是被很多开发者吐槽、诟病的一个点。**

◼ **在这一点上，Vue做的要好于React：** 

- Vue通过在.vue文件中编写 <style><style> 标签来编写自己的样式；

- 通过是否添加 scoped 属性来决定编写的样式是全局有效还是局部有效；

- 通过 lang 属性来设置你喜欢的 less、sass等预处理器；

- 通过内联样式风格的方式来根据最新状态设置和改变css； 

- 等等...

◼ **Vue在CSS上虽然不能称之为完美，但是已经足够简洁、自然、方便了，至少统一的样式风格不会出现多个开发人员、多个项目采用不一样的样式风格。**

◼ **相比而言，React官方并没有给出在React中统一的样式风格：**

- 由此，从普通的css，到css modules，再到css in js，有几十种不同的解决方案，上百个不同的库；

- 大家一致在寻找最好的或者说最适合自己的CSS方案，但是到目前为止也没有统一的方案；



#### **内联样式CSS写法**

◼ **内联样式是官方推荐的一种css样式的写法：**

- style 接受一个采用小驼峰命名属性的 JavaScript 对象，而不是 CSS 字符串；

- 并且可以引用state中的状态来设置相关的样式；

◼ **内联样式的优点:** 

- 1.内联样式, 样式之间不会有冲突

- 2.可以动态获取当前state中的状态

◼ **内联样式的缺点：**

- 1.写法上都需要使用驼峰标识

- 2.某些样式没有提示

- 3.大量的样式, 代码混乱

- 4.某些样式无法编写(比如伪类/伪元素) 

```jsx
import React, { PureComponent } from 'react'

export class App extends PureComponent {
  constructor() {
    super()

    this.state = {
      titleSize: 30
    }
  }

  addTitleSize() {
    this.setState({ titleSize: this.state.titleSize + 2 })
  }

  render() {
    const { titleSize } = this.state
    return (
      <div>
        <button onClick={e => this.addTitleSize()}>增加titleSize</button>
        <h2 style={{ color: "red", fontSize: `${titleSize}px` }}>我是标题</h2>
        <p style={{ color: "blue", fontSize: "20px" }}>我是内容，哈哈哈</p>
      </div>
    )
  }
}

export default App
```





#### **普通CSS文件写法**

◼ **普通的css我们通常会编写到一个单独的文件，之后再进行引入。**

◼ **这样的编写方式和普通的网页开发中编写方式是一致的：**

- 如果我们按照普通的网页标准去编写，那么也不会有太大的问题；

- 但是组件化开发中我们总是希望组件是一个独立的模块，即便是样式也只是在自己内部生效，不会相互影响；

- 但是普通的css都属于全局的css，样式之间会相互影响；

◼ **这种编写方式最大的问题是样式之间会相互层叠掉**

```jsx
import React, { PureComponent } from "react";
import "./App.css";
import Home from "./Home/Home";
import Profile from "./Profile/Profile";

export class App extends PureComponent {
  render() {
    return (
      <div>
        <h2 className="title">我是标题</h2>
        <p className="content">我是内容，哈哈哈</p>
        <Home />
        <Profile />
      </div>
    );
  }
}

export default App;
```





#### **CSS Module写法**

◼ **css modules并不是React特有的解决方案，而是所有使用了类似于**webpack配置的环境下都可以使用的。

- 如果在其他项目中使用它，那么我们需要自己来进行配置，比如配置webpack.config.js中的modules: true等。

◼ **React的脚手架已经内置了css modules的配置：**

- .css/.less/.scss 等样式文件都需要修改成 .module.css/.module.less/.module.scss 等；

- 之后就可以引用并且进行使用了；

◼ **css modules确实解决了局部作用域的问题，也是很多人喜欢在React中使用的一种方案。**

◼ **但是这种方案也有自己的缺陷：**

- 引用的类名，不能使用连接符(.home-title)，在JavaScript中是不识别的；

- 所有的className都必须使用{style.className} 的形式来编写；

- 不方便动态来修改某些样式，依然需要使用内联样式的方式； 

◼ **如果你觉得上面的缺陷还算OK，那么你在开发中完全可以选择使用css modules来编写，并且也是在React中很受欢迎的一种方式。**

```jsx
import React, { PureComponent } from "react";
import Home from "./Home/Home";
import Profile from "./Profile/Profile";

import appStyle from "./App.module.css";

export class App extends PureComponent {
  render() {
    return (
      <div>
        <h2 className={appStyle.title}>我是标题</h2>
        <p className={appStyle.content}>我是内容，哈哈哈</p>
        <Home />
        <Profile />
      </div>
    );
  }
}

export default App;
```



#### **CSS in JS解决方案**

◼ **官方文档也有提到过CSS in JS这种方案：**

- “CSS-in-JS” 是指一种模式，其中 CSS 由 JavaScript 生成而不是在外部文件中定义； 

- 注意此功能并不是 React 的一部分，而是由第三方库提供；

- React 对样式如何定义并没有明确态度；

◼ **在传统的前端开发中，我们通常会将结构（HTML）、样式（CSS）、逻辑（JavaScript）进行分离。**

- 但是在前面的学习中，我们就提到过，React的思想中认为逻辑本身和UI是无法分离的，所以才会有了JSX的语法。 

- **样式呢？**样式也是属于UI的一部分； 

- 事实上CSS-in-JS的模式就是一种将样式（CSS）也写入到JavaScript中的方式，并且可以方便的使用JavaScript的状态； 

- 所以React有被人称之为 All in JS； 



##### **认识styled-components**

◼ **批评声音虽然有，但是在我们看来很多优秀的CSS-in-JS的库依然非常强大、方便：**

- CSS-in-JS通过JavaScript来为CSS赋予一些能力，包括类似于CSS预处理器一样的样式嵌套、函数定义、逻辑复用、动态修

改状态等等； 

- 虽然CSS预处理器也具备某些能力，但是获取动态状态依然是一个不好处理的点； 

- 所以，目前可以说CSS-in-JS是React编写CSS最为受欢迎的一种解决方案； 

◼ **目前比较流行的CSS-in-JS的库有哪些呢？**

- styled-components

- emotion

- glamorous

◼ **目前可以说styled-components依然是社区最流行的CSS-in-JS库，所以我们以styled-components的讲解为主；**

◼ **安装styled-components：**

```
pnpm install styled-components
```



##### **styled的基本使用**

◼ **styled-components的本质是通过函数的调用，最终创建出一个组件：**

- 这个组件会被自动添加上一个不重复的class； 

- styled-components会给该class添加相关的样式；

◼ **另外，它支持类似于CSS预处理器一样的样式嵌套：**

- 支持直接子代选择器或后代选择器，并且直接编写样式； 

- 可以通过&符号获取当前元素； 

- 直接伪类选择器、伪元素等；

```jsx
import React, { PureComponent } from "react";
import { AppWrapper, SectionWrapper } from "./style";
import Home from "./home";

export class App extends PureComponent {
  constructor() {
    super();

    this.state = {
      size: 30,
      color: "yellow",
    };
  }
  render() {
    const { size, color } = this.state;
    return (
      <AppWrapper>
        <SectionWrapper size={size} color={color}>
          <h2 className="title">我是标题</h2>
          <p className="content">我是内容，红红火火恍恍惚惚</p>
          <button onClick={(e) => this.setState({ color: "skyblue" })}>
            修改颜色
          </button>
        </SectionWrapper>

        <Home />

        <div className="footer">
          <p>免责声明</p>
          <p>版权声明</p>
        </div>
      </AppWrapper>
    );
  }
}

export default App;
```



##### **props、attrs属性**

◼ **props可以传递**

```jsx
  <SectionWrapper size={size} color={color}>
```



◼ **props可以被传递给styled组件**

- 获取props需要通过${}传入一个插值函数，props会作为该函数的参数；

- 这种方式可以有效的解决动态样式的问题；

◼ **添加attrs属性**

> style.js

```js
import styled from "styled-components";
import * as vars from "./style/variables.js"

// 1.基本使用
export const AppWrapper = styled.div`
  .footer{
    border:1px solid orange;
  }
`

// 2.子元素单独抽离到一个组件
// 3.可以接受外部传入的props
// 4.可以通过attrs给标签模板字符串中提供的属性
// 5.从一个单独的文件中引入变量
export const SectionWrapper = styled.div.attrs(props => {
  return {
    tColor: props.color || "blue"
  }
})`
    border:1px solid red;

    .title{
      font-size: ${props => props.size}px;
      color: ${props => props.tColor};

      &:hover{
        background-color: purple;
      }
    }

    .content{
      font-size: ${vars.largeSize}px;
      color: ${vars.primaryColor};
    }
`
```

##### css的公共内容

在index.js中引入ThemeProvider，在style.js中调用${props => props.theme.color}

> index.js

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import { ThemeProvider } from 'styled-components';

import App from './06_classnames库/App';


const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <ThemeProvider theme={{ color: "red", size: "50px" }}>
      <App />
    </ThemeProvider>
  </React.StrictMode>
);
```

> style.js

```js
import styled from "styled-components";

// 6.css的继承
const HYButton = styled.button`
  border: 1px solid red;
  border-radius: 5px;
`
export const HYButtonWrapper = styled(HYButton)`
  background-color: #0f0;
  color: #fff;
` 

export const HomeWrapper = styled.div`
  .top {
    .banner {
      color: red;
    }
  }

  .bottom {
    .header {
      color: ${props => props.theme.color};
      font-size: ${props => props.theme.size};
    }

    .product-list {
      .item {
        color: blue;
      }
    }
  }
`

```



##### **styled高级特性**

- 子元素单独抽离到一个组件
- 可以接受外部传入的props
- 可以通过attrs给标签模板字符串中提供的属性
- 从一个单独的文件中引入变量
- css的继承



##### **React中添加class**

**◼ React在JSX给了我们开发者足够多的灵活性，你可以像编写JavaScript代码一样，通过一些逻辑来决定是否添加某些class：** 

```jsx
render() {
    const { isbbb, isccc } = this.state;
    const classList = ["aaa"];
    if (isbbb) classList.push("bbb");
    if (isccc) classList.push("ccc");
    const classname = classList.join(" ");

    return (
      <div>
        <h2 className={`aaa ${isbbb ? "bbb" : ""} ${isccc ? "ccc" : ""}`}>
          哈哈哈
        </h2>
        <h2 className={classname}>嘿嘿嘿</h2>
      </div>
    );
  }
```



◼ **这个时候我们可以借助于一个第三方的库：****classnames**

- 很明显，这是一个用于动态添加classnames的一个库。

```jsx
classNames('foo', 'bar'); // => 'foo bar'
classNames('foo', { bar: true }); // => 'foo bar'
classNames({ 'foo-bar': true }); // => 'foo-bar'
classNames({ 'foo-bar': false }); // => ''
classNames({ foo: true }, { bar: true }); // => 'foo bar'
classNames({ foo: true, bar: true }); // => 'foo bar'
```





## 七、Redux

### 为什么需要Redux

◼ **JavaScript开发的应用程序，已经变得越来越复杂了：**

- JavaScript需要管理的状态越来越多，越来越复杂； 

- 这些状态包括服务器返回的数据、缓存数据、用户操作产生的数据等等，也包括一些UI的状态，比如某些元素是否被选中，是否显示加载动效，当前分页； 

◼ **管理不断变化的state是非常困难的：**

- 状态之间相互会存在依赖，一个状态的变化会引起另一个状态的变化，View页面也有可能会引起状态的变化； 

- 当应用程序复杂时，state在什么时候，因为什么原因而发生了变化，发生了怎么样的变化，会变得非常难以控制和追踪； 

◼ **React是在视图层帮助我们解决了DOM的渲染过程，但是State依然是留给我们自己来管理：**

- 无论是组件定义自己的state，还是组件之间的通信通过props进行传递；也包括通过Context进行数据之间的共享； 

- React主要负责帮助我们管理视图，state如何维护最终还是我们自己来决定； 

![image-20221102201035594](http://img.roydust.top/img/202211022010707.png)

◼ **Redux就是一个帮助我们管理State的容器：Redux是****JavaScript的状态容器****，提供了****可预测的状态管理****；** 

◼ **Redux除了和React一起使用之外，它也可以和其他界面库一起来使用（比如Vue），并且它非常小（包括依赖在内，只有2kb）**



### **Redux的核心思想**



#### **Store**

◼ **Redux的核心理念非常简单。**

◼ **比如我们有一个朋友列表需要管理：**

- 如果我们没有定义统一的规范来操作这段数据，那么整个数据的变化就是无法跟踪的； 

- 比如页面的某处通过products.push的方式增加了一条数据；

- 比如另一个页面通过products[0].age = 25修改了一条数据；

◼ **整个应用程序错综复杂，当出现bug时，很难跟踪到底哪里发生的变化；**

◼ 所以我们需要一个总的数据中心（store）来管理全部的数据

```js
// 初始化数据
const initialState = {
  name: "lyc",
  count: 100
}
```



#### **action**

◼ **Redux要求我们通过action来更新数据：**

- 所有数据的变化，必须通过派发（dispatch）action来更新； 

- action是一个普通的JavaScript对象，用来描述这次更新的type和content； 

◼ **比如下面就是几个更新friends的action：** 

- 强制使用action的好处是可以清晰的知道数据到底发生了什么样的变化，所有的数据变化都是可跟追、可预测的； 

- 当然，目前我们的action是固定的对象；

- 真实应用中，我们会通过函数来定义，返回一个action；

```js
const changeNameAction = (name) => {
  return {
    type: "CHANGE_NAME",
    name
  }
}

const addNumberAction = (num) => {
  return {
    type: "ADD_NUMBER",
    num
  }
}

module.exports = {
  changeNameAction,
  addNumberAction
}

```



#### **reducer**

◼ **但是如何将state和action联系在一起呢？答案就是reducer**

- reducer是一个纯函数； 

- reducer做的事情就是将传入的state和action结合起来生成一个新的state；

```js
// 定义reducer函数
// 两个参数：
// 参数一：store中目前保存的store
// 参数二：本次需要更新的action(dispatch传入的action)
// 返回值：它的返回值会作为store之后存储的state 
function reducer(state = initialState, action) {
  console.log("reducer:", state, action);
  // 有新数据进行更新的时候，那么返回一个新的state
  switch (action.type) {
    case "change_name":
      return { ...state, name: action.name }
    case "add_number":
      return { ...state, count: action.count }
    default:
      return state
  }

  // 没有新数据更新，那么就返回之前的state
  return state
}
```





#### **Redux的三大原则**

◼ **单一数据源**

- 整个应用程序的state被存储在一颗object tree中，并且这个object tree只存储在一个 store 中：

- Redux并没有强制让我们不能创建多个Store，但是那样做并不利于数据的维护； 

- 单一的数据源可以让整个应用程序的state变得方便维护、追踪、修改； 

◼ **State是只读的**

- 唯一修改State的方法一定是触发action，不要试图在其他地方通过任何的方式来修改State： 

- 这样就确保了View或网络请求都不能直接修改state，它们只能通过action来描述自己想要如何修改state； 

- 这样可以保证所有的修改都被集中化处理，并且按照严格的顺序来执行，所以不需要担心race condition（竟态）的问题； 

◼ **使用纯函数来执行修改**

- 通过reducer将 旧state和 actions联系在一起，并且返回一个新的State： 

- 随着应用程序的复杂度增加，我们可以将reducer拆分成多个小的reducers，分别操作不同state tree的一部分； 

- 但是所有的reducer都应该是纯函数，不能产生任何的副作用；



### **Redux的基本使用**

◼ **安装redux：** 

```
pnpm install redux --save
```

◼ **1.创建一个新的项目文件夹：learn-redux**

```
pnpm init
```

◼ **2.创建src目录，并且创建index.js文件**

◼ **3.修改package.json可以执行index.js**

```
"scripts": {
"start": "node src/index.js" 
}
```



#### Redux的使用

◼ **1.创建一个对象，作为我们要保存的状态：**

```jsx
// 初始化数据
const initialState = {
  name: "lyc",
  count: 100
}
```



◼ **2.创建Store来存储这个state**

- 创建store时必须创建reducer； 

- 我们可以通过 store.getState 来获取当前的state； 

```jsx
const { createStore } = require("redux")
const reducer = require("./reducer.js")

// 创建的store
const store = createStore(reducer)

module.exports = store
```



◼ **3.通过action来修改state**

- 通过dispatch来派发action； 

- 通常action中都会有type属性，也可以携带其他的数据；

```jsx
const { CHANGE_NAME, ADD_NUMBER } = require("./constants")

const changeNameAction = (name) => {
  return {
    type: "CHANGE_NAME",
    name
  }
}

const addNumberAction = (num) => {
  return {
    type: "ADD_NUMBER",
    num
  }
}

module.exports = {
  changeNameAction,
  addNumberAction
}
```



◼ **4.修改reducer中的处理代码**

- 这里一定要记住，reducer是一个纯函数，不需要直接修改state； 

```jsx
const { ADD_NUMBER, CHANGE_NAME } = require("./constants")

// 初始化数据
const initialState = {
  name: "lyc",
  count: 100
}

function reducer(state = initialState, action) {
  console.log("reducer:", state, action);
  // 有新数据进行更新的时候，那么返回一个新的state
  switch (action.type) {
    case ADD_NUMBER:
      return { ...state, name: action.name }
    case CHANGE_NAME:
      return { ...state, count: action.count }
    default:
      return state
  }

  // 没有新数据更新，那么就返回之前的state
  return state
}

module.exports = reducer
```



◼ **5.还可以抽离出公共的变量，防止打错字

```js
const ADD_NUMBER = "add_number"
const CHANGE_NAME = "change_name"

module.exports = {
  ADD_NUMBER,
  CHANGE_NAME
}
```



◼ **6.可以在派发action之前，监听store的变化：**

```jsx
const store = require("./store")

const unsubscribe = store.subscribe(() => {
  console.log("订阅数据的变量", store.getState());
})

// 修改store中的数据：必须action

store.dispatch({ type: "change_name", name: "kobe" })

// 取消订阅
unsubscribe()

store.dispatch({ type: "add_number", count: 999 })
```



#### **Redux结构划分**

◼ **如果我们将所有的逻辑代码写到一起，那么当redux变得复杂时代码就难以维护。**

- 接下来，我会对代码进行拆分，将store、reducer、action、constants拆分成一个个文件。

- 创建store/index.js文件：

- 创建store/reducer.js文件：

- 创建store/actionCreators.js文件：

- 创建store/constants.js文件：

◼ **我们已经知道了redux的基本使用过程，那么我们就更加清晰来认识一下redux在实际开发中的流程：**

![pic](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0a69e42c39154d89be3ab2186a5f4e71~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

![image-20221102203026101](http://img.roydust.top/img/202211022030197.png)

**Redux官方图**

![image-20221102203049298](http://img.roydust.top/img/202211022030390.png)



### **React结合Redux**

◼ **目前redux在react中使用是最多的，所以我们需要将之前编写的redux代码，融入到react当中去。**

◼ **这里我创建了两个组件：**

- Home组件：其中会展示当前的counter值，并且有一个+1和+5的按钮；

- Profile组件：其中会展示当前的counter值，并且有一个-1和-5的按钮；

◼ **核心代码主要是两个：**

- 在 componentDidMount 中定义数据的变化，当数据发生变化时重新设置 counter;

- 在发生点击事件时，调用store的dispatch来派发对应的action；



#### 案例结构

![image-20221102203303893](http://img.roydust.top/img/202211022033980.png)

#### 详细代码

##### Redux代码

> store/index.js    

```js
import { createStore } from "redux";
import reducer from "./reducer";

const store = createStore(reducer)

export default store
```



> store/reducer.js    修改state

```js
import * as actionTypes from "./constants"

const initialState = {
  counter: 100
}

// 进行逻辑操作
function reducer(state = initialState, action) {
  switch (action.type) {
    case actionTypes.ADD_NUMBER:
      return { ...state, counter: state.counter + action.num }
    case actionTypes.SUB_NUMBER:
      return { ...state, counter: state.counter - action.num }
    default:
      return state
  }
}

export default reducer
```



> store/constants.js   公共变量

```js
export const ADD_NUMBER = "add_number"
export const SUB_NUMBER = "sub_number"
```



> store/actionCreators.js     更改数据

```js
import * as actionTypes from "./constants"
export const addNumberAction = (num) => ({
  type: actionTypes.ADD_NUMBER,
  num
})

export const subNumberAction = (num) => ({
  type: actionTypes.SUB_NUMBER,
  num
})
```



##### 应用层

> home.js

```jsx
import React, { PureComponent } from "react";
import store from "../store";
import { addNumberAction } from "../store/actionCreators";

export class home extends PureComponent {
  constructor() {
    super();

    this.state = {
      counter: store.getState().counter,
    };
  }
  componentDidMount() {
    store.subscribe(() => {
      const state = store.getState();
      this.setState({
        counter: state.counter,
      });
    });
  }

  addNumber(num) {
    store.dispatch(addNumberAction(num));
  }

  render() {
    const { counter } = this.state;
    return (
      <div>
        <h2>home counter:{counter}</h2>
        <div>
          <button onClick={(e) => this.addNumber(1)}>+1</button>
          <button onClick={(e) => this.addNumber(5)}>+5</button>
          <button onClick={(e) => this.addNumber(10)}>+10</button>
        </div>
      </div>
    );
  }
}

export default home;
```



### **React-redux使用**

◼ 开始之前需要强调一下，redux和react没有直接的关系，你完全可以在React, Angular, Ember, jQuery, or vanillaJavaScript中使用Redux。

◼ 尽管这样说，redux依然是和React库结合的更好，因为他们是通过state函数来描述界面的状态，Redux可以发射状态的更新，让他们作出相应。

◼ 虽然我们之前已经实现了connect、Provider这些帮助我们完成连接redux、react的辅助工具，但是实际上redux官方帮助我们提供了 react-redux 的库，可以直接在项目中使用，并且实现的逻辑会更加的严谨和高效。

6.1 安装

```css
npm install --save react-redux
```

6.2 核心

- ```jsx
  < Provider store>
  ```

- ```jsx
  connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])
  ```

Provider 内的任何一个组件，如果需要使用 state 中的数据，就必须是「被 connect 过的」组件——使用 connect 方法对「你编写的组件（MyComp）」进行包装后的产物。

这个函数允许我们将 store 中的数据作为 props 绑定到组件上。

简单的流程如下图所示：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/95e279721bec4ec4a9f3314a470d2f9c~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

react-redux中的connect方法将store上的getState 和 dispatch 包装成组件的props。

将之前直接在组件上dispatch的代码修改为如下：

```jsx
import React, { PureComponent } from 'react'
import { connect } from "react-redux"
// import store from "../store"
import { addNumberAction, subNumberAction } from '../store/counter'

export class About extends PureComponent {

  calcNumber(num, isAdd) {
    if (isAdd) {
      this.props.addNumber(num)
    } else {
      this.props.subNumber(num)
    }
  }

  render() {
    const { counter, banners, recommends, userInfo } = this.props

    return (
      <div>
        <div className='user'>
          <h2>nickname: {userInfo.nickname}</h2>
        </div>
        <h2>About Page: {counter}</h2>
        <div>
          <button onClick={e => this.calcNumber(6, true)}>+6</button>
          <button onClick={e => this.calcNumber(88, true)}>+88</button>
          <button onClick={e => this.calcNumber(6, false)}>-6</button>
          <button onClick={e => this.calcNumber(88, false)}>-88</button>
        </div>
        <div className='banner'>
          <h2>轮播图数据:</h2>
          <ul>
            {
              banners.map((item, index) => {
                return <li key={index}>{item.title}</li>
              })
            }
          </ul>
        </div>
        <div className='recommend'>
          <h2>推荐数据:</h2>
          <ul>
            {
              recommends.map((item, index) => {
                return <li key={index}>{item.title}</li>
              })
            }
          </ul>
        </div>
      </div>
    )
  }
}

const mapStateToProps = (state) => ({
  counter: state.counter.counter,
  banners: state.home.banners,
  recommends: state.home.recommends,
  userInfo: state.user.userInfo
})

const mapDispatchToProps = (dispatch) => ({
  addNumber(num) {
    dispatch(addNumberAction(num))
  },
  subNumber(num) {
    dispatch(subNumberAction(num))
  }
})

export default connect(mapStateToProps, mapDispatchToProps)(About)
```



### connect高阶组件

> /hoc/connenct.js

```js
// 手写connect的函数：
// 参数一：函数
// 函数二：函数
// 返回值：函数

// import store from "../store"   将store解耦

import { PureComponent } from "react";
import { StoreContext } from "./StoreContext";

export function connect(mapStateToProps, mapDispatchToProps) {

  // 高阶组件：函数
  return function (WrapperComponent) {
    class NewComponent extends PureComponent {
      constructor(props, context) {
        super(props)

        this.state = mapStateToProps(context.getState())
      }
      componentDidMount() {
        this.unsubscribe = this.context.subscribe(() => {
          // this.forceUpdate()
          this.setState(mapStateToProps(this.context.getState()))
        })
      }
      render() {
        // 传入store里的state
        const stateObj = mapStateToProps(this.context.getState())
        // 传入store里的dispatch
        const dispatchObj = mapDispatchToProps(this.context.dispatch)
        // 绑定组件，将上面的值作为注入为props
        return <WrapperComponent {...this.props} {...stateObj} {...dispatchObj} />
      }
    }

    NewComponent.contextType = StoreContext

    return NewComponent
  }
}
```

> /hoc/StoreContext.js

**创建一个Context，用于获取用户Store**

```js
import { createContext } from "react";

export const StoreContext = createContext()
```

> /hoc/index.js

```js
// 统一导出
export { StoreContext } from "./StoreContext"
export { connect } from "./connect"
```

> index.js 主函数

**我们提供一个Provider，Provider来自于我们创建的Context，让用户将store传入到value中即可；**

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import { Provider } from "react-redux"
import { StoreContext } from "./hoc"
import App from './App';
import "./style.css"
import store from './store';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  // 由此可见react-redux官方也是使用的Provider来获取用户的Store
  <Provider store={store}>
    <StoreContext.Provider value={store}>
      <App />
    </StoreContext.Provider>
  </Provider>
);
```



### **Redux的异步操作**

**在redux中如何可以进行异步的操作呢？**

- 答案就是使用**中间件（Middleware）**； 

- 学习过Express或Koa框架的童鞋对中间件的概念一定不陌生；

- 在这类框架中，Middleware可以帮助我们在请求和响应之间嵌入一些操作的代码，比如cookie解析、日志记录、文件压缩等操作；

![image-20221109134026835](http://img.roydust.top/img/202211091340989.png)

◼ **redux也引入了中间件（Middleware）的概念：**

- 这个中间件的目的是在dispatch的action和最终达到的reducer之间，扩展一些自己的代码； 

- 比如日志记录、调用异步接口、添加代码调试功能等等；

◼ **我们现在要做的事情就是发送异步的网络请求，所以我们可以添加对应的中间件：**

- 这里官网推荐的、包括演示的网络请求的中间件是使用 redux-thunk； 

◼ **redux-thunk是如何做到让我们可以发送异步的请求呢？**

- 我们知道，默认情况下的dispatch(action)，action需要是一个JavaScript的对象； 

- redux-thunk可以让dispatch(action函数)，action可以是一个函数； 

- 该函数会被调用，并且会传给这个函数一个dispatch函数和getState函数； 
  - dispatch函数用于我们之后再次派发action； 
  - getState函数考虑到我们之后的一些操作需要依赖原来的状态，用于让我们可以获取之前的一些状态；

> actionCreators.js

```js
// 编写异步请求数据函数
export const fetchHomeMultidataAction = () => {
  return function(dispatch) {
    axios.get("http://123.207.32.32:8000/home/multidata").then(res => {
      const banners = res.data.data.banner.list
      const recommends = res.data.data.recommend.list

      dispatch(changeBannersAction(banners))
      dispatch(changeRecommendsAction(recommends))
    })
  }
}
```

> category.jsx

```jsx
import React, { PureComponent } from 'react'
import { connect } from "react-redux"
import { fetchHomeMultidataAction } from "../store/home"

export class Category extends PureComponent {

  componentDidMount() {
    this.props.fetchHomeMultidata()
  }

  render() {
    return (
      <div>
        <h2>Category Page: {this.props.counter}</h2>
      </div>
    )
  }
}

const mapStateToProps = (state) => ({
  counter: state.counter.counter
})

// 调用异步请求数据函数
const mapDispatchToProps = (dispatch) => ({
  fetchHomeMultidata() {
    dispatch(fetchHomeMultidataAction())
  }
})

export default connect(mapStateToProps, mapDispatchToProps)(Category)
```



### **如何使用redux-thunk**

◼ **1.安装redux-thunk**

◼ **2.在创建store时传入应用了middleware的enhance函数**

- 通过applyMiddleware来结合多个Middleware, 返回一个enhancer； 

- 将enhancer作为第二个参数传入到createStore中；

```js
import { createStore, applyMiddleware } from "redux"
import thunk from "redux-thunk"
import reducer from "./reducer"

// 正常情况下 store.dispatch(object)
// 想要派发函数 store.dispatch(function)


const store = createStore(reducer, composeEnhancers(applyMiddleware(thunk)))

export default store
```



◼ **3.定义返回一个函数的action：** 

- 注意：这里不是返回一个对象了，而是一个函数；

- 该函数在dispatch之后会被执行；

```js
export const fetchHomeMultidataAction = () => {
  // 如果是一个普通的action, 那么我们这里需要返回action对象
  // 问题: 对象中是不能直接拿到从服务器请求的异步数据的
  // return {}

  return function(dispatch, getState) {
    // 异步操作: 网络请求
    // console.log("foo function execution-----", getState().counter)
    axios.get("http://123.207.32.32:8000/home/multidata").then(res => {
      const banners = res.data.data.banner.list
      const recommends = res.data.data.recommend.list

      // dispatch({ type: actionTypes.CHANGE_BANNERS, banners })
      // dispatch({ type: actionTypes.CHANGE_RECOMMENDS, recommends })
      dispatch(changeBannersAction(banners))
      dispatch(changeRecommendsAction(recommends))
    })
  }

  // 如果返回的是一个函数, 那么redux是不支持的
  // return foo
}
```



### Redux-Devtools

redux官网为我们提供了redux-devtools的工具； 

利用这个工具，我们可以知道每次状态是如何被修改的，修改前后的状态变化等等；

◼ **安装该工具需要两步：**

- 第一步：在对应的浏览器中安装相关的插件（比如Chrome浏览器扩展商店中搜索Redux DevTools即可）；

- 第二步：在redux中继承devtools的中间件；

```js
import { createStore, applyMiddleware, compose } from "redux"
import thunk from "redux-thunk"
import reducer from "./reducer"

// 正常情况下 store.dispatch(object)
// 想要派发函数 store.dispatch(function)

// redux-devtools
const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({trace: true}) || compose;
const store = createStore(reducer, composeEnhancers(applyMiddleware(thunk)))

export default store
```



### **reducer的模块拆分**

◼ **我们先来理解一下，为什么这个函数叫reducer？** 

◼ **我们来看一下目前我们的reducer：** 

```JS
import * as actionTypes from "./constants"

const initialState = {
  counter: 100,
  
  banners: [],
  recommends: []
}

function reducer(state = initialState, action) {
  switch (action.type) {
    case actionTypes.ADD_NUMBER:
      return { ...state, counter: state.counter + action.num }
    case actionTypes.SUB_NUMBER:
      return { ...state, counter: state.counter - action.num }
    case actionTypes.CHANGE_BANNERS:
      return { ...state, banners: action.banners }
    case actionTypes.CHANGE_RECOMMENDS:
      return { ...state, recommends: action.recommends }
    default:
      return state
  }
}

export default reducer
```

- 当前这个reducer既有处理counter的代码，又有处理home页面的数据；

- 后续counter相关的状态或home相关的状态会进一步变得更加复杂；

- 我们也会继续添加其他的相关状态，比如购物车、分类、歌单等等；

- 如果将所有的状态都放到一个reducer中进行管理，随着项目的日趋庞大，必然会造成代码臃肿、难以维护。

◼ **因此，我们可以对reducer进行拆分：**

- 我们先抽取一个对counter处理的reducer； 

- 再抽取一个对home处理的reducer； 

- 将它们合并起来；

![image-20221109135033585](http://img.roydust.top/img/202211091350647.png)





#### **combineReducers函数**

◼ **目前我们合并的方式是通过每次调用reducer函数自己来返回一个新的对象。**

◼ 事实上，redux给我们提供了一个 **combineReducers函数** **可以方便的让我们对多个reducer进行合并：**

```js
import { createStore, compose, combineReducers } from "redux"
import { log, thunk, applyMiddleware } from "./middleware"
// import thunk from "redux-thunk"

import counterReducer from "./counter"
import homeReducer from "./home"
import userReducer from "./user"

// 正常情况下 store.dispatch(object)
// 想要派发函数 store.dispatch(function)

// 将两个reducer合并在一起
const reducer = combineReducers({
  counter: counterReducer,
  home: homeReducer,
  user: userReducer
})
```



◼ **那么combineReducers是如何实现的呢？**

- 事实上，它也是将我们传入的reducers合并到一个对象中，最终返回一个combination的函数（相当于我们之前的reducer函数了）；

- 在执行combination函数的过程中，它会通过判断前后返回的数据是否相同来决定返回之前的state还是新的state； 

- 新的state会触发订阅者发生对应的刷新，而旧的state可以有效的组织订阅者发生刷新； 

```js
// combineReducers实现原理(了解)
function reducer(state = {}, action) {
  // 返回一个对象, store的state
  return {  
    counter: counterReducer(state.counter, action),
    home: homeReducer(state.home, action),
    user: userReducer(state.user, action)
  }
}
```



### **ReduxToolkit**

◼ **Redux Toolkit 是官方最新推荐的编写 Redux 逻辑的方法。**

- 在前面我们学习Redux的时候应该已经发现，redux的编写逻辑过于的繁琐和麻烦。

- 并且代码通常分拆在多个文件中（虽然也可以放到一个文件管理，但是代码量过多，不利于管理）；

- Redux Toolkit包旨在成为编写Redux逻辑的标准方式，从而解决上面提到的问题；

- 在很多地方为了称呼方便，也将之称为“RTK”；

◼ **安装Redux Toolkit：** 

```
pnpm install @reduxjs/toolkit react-redux
```

◼ **Redux Toolkit的核心API主要是如下几个：**

- **configureStore**：包装createStore以提供简化的配置选项和良好的默认值。它可以自动组合你的 slice reducer，添加你提供的任何 Redux 中间件，redux-thunk默认包含，并启用 Redux DevTools Extension。 

- **createSlice**：接受reducer函数的对象、切片名称和初始状态值，并自动生成切片reducer，并带有相应的actions。 

- **createAsyncThunk**: 接受一个动作类型字符串和一个返回承诺的函数，并生成一个pending/fulfilled/rejected基于该承诺分派动作类型的 thunk



#### **ReduxToolkit重构**

我们先对counter的reducer进行重构：**通过createSlice创建一个slice。**

◼ **createSlice****主要包含如下几个参数：**

◼ name：用户标记slice的名词

- 在之后的redux-devtool中会显示对应的名词；

◼ initialState：初始化值

- 第一次初始化时的值；

◼ reducers：相当于之前的reducer函数

- 对象类型，并且可以添加很多的函数；

- 函数类似于redux原来reducer中的一个case语句；

- 函数的参数：
  - 参数一：state
  -  参数二：调用这个action时，传递的action参数；

◼ **createSlice**返回值是一个对象，包含所有的actions；

> /store/features/counter.js

```js
import { createSlice } from "@reduxjs/toolkit";


const counterSlice = createSlice({
  // 用户标记slice的名词
  name: "counter",
  // 初始值
  initialState: {
    counter: 888
  },
  // reduce函数
  reducers: {
    addNumber(state, { payload }) {
      state.counter = state.counter + payload
    },
    subNumber(state, { payload }) {
      // console.log("counter reducer subNumber", action);
      state.counter = state.counter - payload
    }
  }
})

// 导出actions方法
export const { subNumber, addNumber } = counterSlice.actions

// 导出counterSlice的reducer作为子reducer进行合并
export default counterSlice.reducer
```



#### **store的创建**

◼ **configureStore用于创建store对象，常见参数如下：**

- reducer，将slice中的reducer可以组成一个对象传入此处；

- middleware：可以使用参数，传入其他的中间件；

- devTools：是否配置devTools工具，默认为true；

```js
import { configureStore } from "@reduxjs/toolkit";

import counterReducer from "./features/counter"
import homeReducer from "./features/home"

const store = configureStore({
  reducer: {
    counter: counterReducer,
    home: homeReducer
  }
})

export default store
```



#### **ReduxToolkit异步**

◼ **在之前的开发中，我们通过redux-thunk中间件让dispatch中可以进行异步操作。**

◼ **Redux Toolkit默认已经给我们继承了Thunk相关的功能：createAsyncThunk**

```js
export const fetchHomeMultidataAction = createAsyncThunk(
  "fetch/homemultidata",
  async (extraInfo, { dispatch, getState }) => {
    // extraInfo 是调用时传入的参数

    const res = await axios.get("http://123.207.32.32:8000/home/multidata")
    return res.data.data
  })
```



◼ **当createAsyncThunk创建出来的action被dispatch时，会存在三种状态：**

- pending：action被发出，但是还没有最终的结果；

- fulfilled：获取到最终的结果（有返回值的结果）；

- rejected：执行过程中有错误或者抛出了异常；

◼ **我们可以在createSlice的entraReducer中监听这些结果：**

```js
  // fetchHomeMultidataAction 有三种状态，可以在fulfilled时期更改数据
  extraReducers: {
    [fetchHomeMultidataAction.pending](state, action) {
      console.log("fetchHomeMultidataAction pending");
    },
    [fetchHomeMultidataAction.fulfilled](state, { payload }) {
      console.log("fetchHomeMultidataAction fulfilled", payload);
      state.banners = payload.banner.list
      state.recommends = payload.recommend.list
    },
    [fetchHomeMultidataAction.rejected](state, actions) {
      console.log("fetchHomeMultidataAction rejected");
    }
  }
```

◼ **extraReducers另一种写法 链式调用**

```js
  // extraReducers另一种写法 链式调用
  extraReducers: (builder) => {
    builder
      .addCase(fetchHomeMultidataAction.pending, (state, actions) => {
        console.log("fetchHomeMultidataAction pending");
      })
      .addCase(fetchHomeMultidataAction.fulfilled, (state, { payload }) => {
        console.log("fetchHomeMultidataAction fulfilled", payload);
        state.banners = payload.banner.list
        state.recommends = payload.recommend.list
      })
      .addCase(fetchHomeMultidataAction.rejected, (state, actions) => {
        console.log("fetchHomeMultidataAction rejected");
      })
  }
```



##### 最新方案

```js
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";
import axios from "axios"

// 获取异步数据
export const fetchHomeMultidataAction = createAsyncThunk(
  "fetch/homemultidata",
  async (extraInfo, { dispatch, getState }) => {
    // extraInfo 是调用时传入的参数

    // 1.发送网络请求
    const res = await axios.get("http://123.207.32.32:8000/home/multidata")

    // 2.取出数据，并且在此处直接dispatch数据(可以不做，在extraReducers里面做)
    const banners = res.data.data.banner.list
    const recommends = res.data.data.recommend.list
    dispatch(changeBanners(banners))
    dispatch(changeRecommends(recommends))

    // 3，返回结果，那么action状态会变成fulfilled状态
    return res.data.data
  })

const homeSlice = createSlice({
  name: "home",
  initialState: {
    banners: [],
    recommends: []
  },
  reducers: {
    changeBanners(state, { payload }) {
      state.banners = payload
    },
    changeRecommends(state, { payload }) {
      state.recommends = payload
    }
  }
})

export const { changeBanners, changeRecommends } = homeSlice.actions

export default homeSlice.reducer 
```



#### **Redux Toolkit的数据不可变性**

◼ **在React开发中，我们总是会强调数据的不可变性：**

- 无论是类组件中的state，还是redux中管理的state； 

- 事实上在整个JavaScript编码过程中，数据的不可变性都是非常重要的；

◼ **所以在前面我们经常会进行浅拷贝来完成某些操作，但是浅拷贝事实上也是存在问题的：**

- 比如过大的对象，进行浅拷贝也会造成性能的浪费；

- 比如浅拷贝后的对象，在深层改变时，依然会对之前的对象产生影响；

◼ **事实上Redux Toolkit底层使用了immerjs的一个库来保证数据的不可变性。**

◼ **在coderwhy公众号的一片文章中也有专门讲解immutable-js库的底层原理和使用方法：**

- https://mp.weixin.qq.com/s/hfeCDCcodBCGS5GpedxCGg

◼ 为了节约内存，又出现了一个新的算法：**Persistent Data Structure**（持久化数据结构或一致性数据结构）

- 用一种数据结构来保存数据；

- 当数据被修改时，会返回一个对象，但是新的对象会尽可能的利用之前的数据结构而不会对内存造成浪费；



### **中间件的实现原理**

◼ **当需要在store进行劫持处理时，就需要实现中间件**

◼ **我们可以利用一个hack一点的技术：Monkey Patching，利用它可以修改原有的程序逻辑；**

> /store/index.js

```js
import { log, thunk, applyMiddleware } from "./middleware"

applyMiddleware(store, log, thunk)
```

> /store/middleware/index.js

**统一出口**

```js
import log from "./log"
import thunk from "./thunk"
import applyMiddleware from "./applyMiddleware"

export {
  log,
  thunk,
  applyMiddleware
}
```

> /store/middleware/log.js

**监控派发dispatch**

```>js
function log(store) {
  // 记录篡改之前的dispatch
  const next = store.dispatch

  function logAndDispatch(action) {
    console.log("当前派发的action:", action)
    // 真正派发的代码: 使用之前的dispatch进行派发
    next(action)
    console.log("派发之后的结果:", store.getState())
  }

  // monkey patch: 猴补丁 => 篡改现有的代码, 对整体的执行逻辑进行修改
  store.dispatch = logAndDispatch
}

export default log
```

> /store/middleware/thunk.js

**自己实现thunk功能**

```js
function thunk(store) {
  const next = store.dispatch
  function dispatchThunk(action) {
    if (typeof action === "function") {
      // 如果传入的是函数就直接执行（比如调起异步数据请求）
      action(store.dispatch, store.getState)
    } else {
      // 如果不是函数那就正常执行
      next(action)
    }
  }
  store.dispatch = dispatchThunk
}

export default thunk
```

> /store/middleware/applyMiddleware.js

**单个调用某个函数来合并中间件并不是特别的方便，我们可以封装一个函数来实现所有的中间件合并：**

```js
 function applyMiddleware(store, ...fns) {
  fns.forEach(fn => {
    fn(store)
  })
}

export default applyMiddleware
```

**我们来理解一下上面操作之后，代码的流程：**

![image-20221112141538583](http://img.roydust.top/img/202211121415714.png)



### **React中的state如何管理**

◼ **我们学习了Redux用来管理我们的应用状态，并且非常好用（当然，你学会前提下，没有学会，好好回顾一下）。**

◼ **目前我们已经主要学习了三种状态管理方式：**

- 方式一：组件中自己的state管理； 

- 方式二：Context数据的共享状态； 

- 方式三：Redux管理应用状态

◼ **Redux的作者有给出自己的建议：**

![image-20221112141631605](http://img.roydust.top/img/202211121416684.png)

◼ **目前项目中我采用的state管理方案：**

- UI相关的组件内部可以维护的状态，在组件内部自己来维护；

- 大部分需要共享的状态，都交给redux来管理和维护；

- 从服务器请求的数据（包括请求的操作），交给redux来维护；



## 八、Redux-Router

### **认识路由**

◼ **路由其实是网络工程中的一个术语：**

- 在架构一个网络时，非常重要的两个设备就是路由器和交换机。 

- 当然，目前在我们生活中路由器也是越来越被大家所熟知，因为我们生活中都会用到路由器： 

- 事实上，路由器主要维护的是一个映射表； 

- 映射表会决定数据的流向；

◼ **路由的概念在软件工程中出现，最早是在后端路由中实现的，原因是web的发展主要经历了这样一些阶段：**

- 后端路由阶段；

- 前后端分离阶段；

- 单页面富应用（SPA）；



#### **后端路由阶段**

◼ 早期的网站开发整个HTML页面是由**服务器来渲染**的. 

- 服务器直接生产渲染好对应的HTML页面, 返回给客户端进行展示. 

◼ 但是, 一个网站, **这么多页面服务器如何处理呢?** 

- 一个页面有自己对应的网址, 也就是URL； 

- URL会发送到服务器, 服务器会通过正则对该URL进行匹配, 并且最后交给一个Controller进行处理； 

- Controller进行各种处理, 最终生成HTML或者数据, 返回给前端. 

◼ 上面的这种操作, 就是**后端路由**： 

- 当我们页面中需要请求不同的**路径**内容时, 交给服务器来进行处理, 服务器渲染好整个页面, 并且将页面返回给客户端. 

- 这种情况下渲染好的页面, 不需要单独加载任何的js和css, 可以直接交给浏览器展示, 这样也有利于SEO的优化. 

◼ **后端路由的缺点:** 

- 一种情况是整个页面的模块由后端人员来编写和维护的；

- 另一种情况是前端开发人员如果要开发页面, 需要通过PHP和Java等语言来编写页面代码； 

- 而且通常情况下HTML代码和数据以及对应的逻辑会混在一起, 编写和维护都是非常糟糕的事情；



#### **前后端分离阶段**

◼ **前端渲染的理解：**

- 每次请求涉及到的静态资源都会从**静态资源服务器获取**，这些资源**包括HTML+CSS+JS**，然后在前端对这些请求回来的资源进行渲染； 

- 需要注意的是，客户端的每一次请求，都会从静态资源服务器请求文件； 

- 同时可以看到，和之前的后端路由不同，这时后端只是负责提供API了；

◼ **前后端分离阶段：**

- 随着Ajax的出现, 有了前后端分离的开发模式； 

- 后端只提供API来返回数据，前端通过Ajax获取数据，并且可以通过JavaScript将数据渲染到页面中；

- 这样做最大的优点就是前后端责任的清晰，后端专注于数据上，前端专注于交互和可视化上；

- 并且当移动端(iOS/Android)出现后，后端不需要进行任何处理，依然使用之前的一套API即可；

- 目前比较少的网站采用这种模式开发；



#### **单页面富应用阶段**

◼ **单页面富应用阶段:** 

- 其实SPA最主要的特点就是在前后端分离的基础上加了一层前端路由. 

- 也就是前端来维护一套路由规则. 

◼ **前端路由的核心是什么呢？改变URL，但是页面不进行整体的刷新。**



#### **URL的hash**

◼ **前端路由是如何做到URL和内容进行映射呢？监听URL的改变。**

◼ **URL的hash**

- URL的hash也就是锚点(#), 本质上是改变window.location的href属性；

- 我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新；

![image-20221112142150384](http://img.roydust.top/img/202211121421452.png)



◼ **hash的优势就是兼容性更好，在老版IE中都可以运行，但是缺陷是有一个#，显得不像一个真实的路径。**

◼ **history接口是HTML5新增的, 它有六种模式改变URL而不刷新页面：**

- replaceState：替换原来的路径；

- pushState：使用新的路径；

- popState：路径的回退；

- go：向前或向后改变路径；

- forward：向前改变路径；

- back：向后改变路径；



### **Router的基本使用**

#### **使用React Router**

- 安装时，我们选择react-router-dom； 

- react-router会包含一些react-native的内容，web开发并不需要；

```sh
npm install react-router-dom
```



◼ **react-router最主要的API是给我们提供的一些组件：**

◼ **BrowserRouter或HashRouter**

- Router中包含了对路径改变的监听，并且会将相应的路径传递给子组件；

- BrowserRouter使用history模式；

- HashRouter使用hash模式；

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { HashRouter } from "react-router-dom"

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <HashRouter>
        <App />
    </HashRouter>
  </React.StrictMode>
);
```



#### **路由映射配置**

◼ **Routes：包裹所有的Route，在其中匹配一个路由**

- Router5.x使用的是Switch组件

◼ **Route：Route用于路径的匹配；**

- path属性：用于设置匹配到的路径；

- element属性：设置匹配到路径后，渲染的组件；
  - Router5.x使用的是component属性

- exact：精准匹配，只有精准匹配到完全一致的路径，才会渲染对应的组件；
  - Router6.x不再支持该属性

> index.jsx

```jsx
<div className="content">
        {/* 映射关系 ：path => Component */}

        <Routes>
          <Route path="/" element={<Navigate to="/home" />} />
          <Route path="/about" element={<About />} />
          <Route path="/login" element={<Login />} />
        </Routes>
      </div>
```



#### **路由配置和跳转**

◼ **Link和NavLink：** 

- 通常路径的跳转是使用Link组件，最终会被渲染成a元素；

- NavLink是在Link基础之上增加了一些样式属性；

- to属性：Link中最重要的属性，用于设置跳转到的路径；

```jsx
          <Link to="/home">首页</Link>
          <NavLink to="/about">关于</NavLink>
          <NavLink to="/login">登录</NavLink>
```

◼ **需要路径选中时，对应的a元素变为红色的这个时候，我们要使用NavLink组件来替代Link组件：**

- style：传入函数，函数接受一个对象，包含isActive属性

- className：传入函数，函数接受一个对象，包含isActive属性

◼ **默认的activeClassName：** 

- 事实上在默认匹配成功时，NavLink就会添加上一个动态的active class； 

- 所以我们也可以直接编写样式

◼ 当然，如果你担心这个class在其他地方被使用了，出现样式的层叠，也可以自定义class

```jsx
          <div className="nav">
            <NavLink
              to="/home"
              style={(isActive) => ({ color: isActive ? "yellow" : "blue" })}
            >
              首页
            </NavLink>
            <NavLink to="/about">关于</NavLink>

            <NavLink
              to="/home"
              className={({ isActive }) => (isActive ? "link-active" : "")}
            >
              首页
            </NavLink>
            <NavLink
              to="/about"
              className={({ isActive }) => (isActive ? "link-active" : "")}
            >
              关于
            </NavLink>
  				</div>
```

```css
.nav .active {
  color: red;
}
```



#### **Navigate导航**

◼ **Navigate****用于路由的重定向，当这个组件出现时，就会执行跳转到对应的to路径中：**

◼ **我们这里使用这个的一个案例：**

- 用户跳转到Profile界面；

- 但是在Profile界面有一个isLogin用于记录用户是否登录：
  - true：那么显示用户的名称；
  - false：直接重定向到登录界面；

```jsx
      <div>
        <h1>Login Page</h1>
        {!isLogin ? (
          <button onClick={(e) => this.login()}>登录</button>
        ) : (
          <Navigate to="/home/" />
        )}
      </div>
```

◼ **我们也可以在匹配到/的时候，直接跳转到/home页面**

```jsx
<Route path="/" element={<Navigate to="/home" />} />
          <Route path="/home" element={<Home />} />
```



#### **Not Found页面配置**

◼ **如果用户随意输入一个地址，该地址无法匹配，那么在路由匹配的位置将什么内容都不显示。**

◼ **很多时候，我们希望在这种情况下，让用户看到一个Not Found的页面。**

◼ **这个过程非常简单：**

- 开发一个Not Found页面；

- 配置对应的Route，并且设置path为*即可；

```jsx
<Route path="*" element={<NotFound />} />
```



### **Router的路由嵌套**

◼ **在开发中，路由之间是存在嵌套关系的。**

◼ **这里我们假设Home页面中有两个页面内容：**

- 推荐列表和排行榜列表；

- 点击不同的链接可以跳转到不同的地方，显示不同的内容；

◼ < Outlet >组件用于在父路由元素中作为子路由的占位元素。

```jsx
          <Route path="/home" element={<Home />}>
            <Route path="/home" element={<Navigate to="/home/recommend" />} />
            <Route path="/home/recommend" element={<HomeRecommend />} />
            <Route path="/home/ranking" element={<HomeRanking />} />
            <Route path="/home/songmenu" element={<HomeSongMenu />} />
          </Route>
```

```jsx
			<div className="home-nav">
          <Link to="/home/recommend">推荐</Link>
          <Link to="/home/ranking">排行榜</Link>
  
        {/* 占位组件 */}
        <Outlet />
      </div>
```



### **Router的代码跳转**

◼ **目前我们实现的跳转主要是通过Link或者NavLink进行跳转的，实际上我们也可以通过****JavaScript代码**进行跳转。**

- 我们知道Navigate组件是可以进行路由的跳转的，但是依然是组件的方式。

- 如果我们希望通过JavaScript代码逻辑进行跳转（比如点击了一个button），那么就需要获取到navigate对象。 

◼ **在Router6.x版本之后，代码类的API都迁移到了hooks的写法：**

- 如果我们希望进行代码跳转，需要通过useNavigate的Hook获取到navigate对象进行操作；

- 那么如果是一个函数式组件，我们可以直接调用，但是如果是一个类组件呢？



#### 函数式组件跳转

```jsx
export function App(props) {
  // 通过useNavigate的Hook获取到navigate对象
  const navigate = useNavigate();
  function navigateTo(path) {
    console.log(path);
    navigate(path);
  }
  return (
    <div className="app">
      <div className="header">
        <span>Header</span>
        <div className="nav">
          <button onClick={(e) => navigateTo("/category")}>分类</button>
          <span onClick={(e) => navigateTo("/order")}>分类</span>
        </div>
        <hr />
      </div>
      <div className="content">
        {/* 映射关系 ：path => Component */}

        <Routes>
          <Route path="/category" element={<Category />} />
          <Route path="/order" element={<Order />} />
        </Routes>
      </div>
    </div>
  );
}  
```



#### 类组件跳转

封装一个Hoc高阶函数with_router

```js
import { useLocation, useNavigate, useParams, useSearchParams } from "react-router-dom"

// 高阶组件：函数  因为Hook只能在函数组件中使用，所以要用一个高阶组件包装一下
function withRouter(WrapperComponent) {
  return function (props) {
    // 1.导航hook
    const navigate = useNavigate();

    const router = { navigate };
		
    // 将routerHook嵌入组件的router中
    return <WrapperComponent {...props} router={router} />;
  };
}

export default withRouter
```

```js
import withRouter from "./with_router";

export {
  withRouter
}
```



> Home.jsx

```JSX
import React, { PureComponent } from "react";
import { Link, Outlet } from "react-router-dom";
import { withRouter } from "../hoc";

export class Home extends PureComponent {
  navigateTo(path) {
    console.log(path);
    const { navigate } = this.props.router;
    navigate(path);
  }

  render() {
    return (
      <div>
        <h1>Home Page</h1>
        <div className="home-nav">
          <Link to="/home/recommend">推荐</Link>
          <Link to="/home/ranking">排行榜</Link>
          <button onClick={(e) => this.navigateTo("/home/songmenu")}>
            歌单
          </button>
        </div>

        {/* 占位组件 */}
        <Outlet />
      </div>
    );
  }
}

// 引用withRoute包裹组件即可使用Hook
export default withRouter(Home);
```



### **Router的参数传递**

◼ **传递参数有二种方式：**

- 动态路由的方式；

- search传递参数；



#### 动态路由

◼ **动态路由的概念指的是路由中的路径并不会固定：**

- 比如/detail的path对应一个组件Detail； 

- 如果我们将path在Route匹配时写成/detail/:id，那么 /detail/abc、/detail/123都可以匹配到该Route，并且进行显示；

- 这个匹配规则，我们就称之为动态路由； 

- 通常情况下，使用动态路由可以为路由传递参数。

```jsx
import React, { PureComponent } from "react";
import { withRouter } from "../hoc";

export class HomeSongMenu extends PureComponent {
  constructor(porps) {
    super(porps);

    this.state = {
      songMenus: [
        { id: 111, name: "华语流行" },
        { id: 112, name: "古典音乐" },
        { id: 113, name: "民谣歌曲" },
      ],
    };
  }

  NavigateToDetail(id) {
    const { navigate } = this.props.router;
    navigate("/detail/" + id);
  }

  render() {
    const { songMenus } = this.state;
    return (
      <div>
        <h1>Home Song Menu</h1>
        <ul>
          {songMenus.map((item) => {
            return (
              <li key={item.id} onClick={(e) => this.NavigateToDetail(item.id)}>
                {item.name}
              </li>
            );
          })}
        </ul>
      </div>
    );
  }
}

export default withRouter(HomeSongMenu);
```

```jsx
<Route path="/detail/:id" element={<Detail />} />
```



#### search传递参数

◼ **search传递参数**

- 指通过Params传递一些小数据

```jsx
  <NavLink to="/user?name=lyc&age=18">用户</NavLink>
```



#### 解决方案

在封装的with-router中再加上一些hooks

> hoc/with-router.js

```js
import { useLocation, useNavigate, useParams, useSearchParams } from "react-router-dom"

// 高阶组件：函数  因为Hook只能在函数组件中使用，所以要用一个高阶组件包装一下
function withRouter(WrapperComponent) {
  return function (props) {
    // 1.导航
    const navigate = useNavigate();

    // 2.动态路由参数：/detail/:id
    const params = useParams()

    // 3.查询字符串的参数：/user?name=lyc&age=18
    const location = useLocation()

    const [searchParams] = useSearchParams()
    const query = Object.fromEntries(searchParams)


    const router = { navigate, params, location, query };

    return <WrapperComponent {...props} router={router} />;
  };
}

export default withRouter
```

> Detail.jsx

```jsx
import React, { PureComponent } from "react";
import { withRouter } from "../hoc";

export class Detail extends PureComponent {
  render() {
    const { router } = this.props;
    const { params } = router;

    return (
      <div>
        <h1>Detail Page</h1>
        <h2>id:{params.id}</h2>
      </div>
    );
  }
}

export default withRouter(Detail);
```

> User.jsx

```jsx
import React, { PureComponent } from "react";
import { withRouter } from "../hoc";

export class User extends PureComponent {
  render() {
    const { router } = this.props;
    const { query } = router;

    return (
      <div>
        <h1>
          User:{query.name}-{query.age}
        </h1>
      </div>
    );
  }
}

export default withRouter(User);
```



### **Router的配置方式**

◼ **目前我们所有的路由定义都是直接使用Route组件，并且添加属性来完成的。**

◼ **但是这样的方式会让路由变得非常混乱，我们希望将所有的路由配置放到一个地方进行集中管理：**

- 在早期的时候，Router并且没有提供相关的API，我们需要借助于react-router-config完成；

- 在Router6.x中，为我们提供了useRoutes API可以完成相关的配置；

> App.jsx

```jsx
import React, { PureComponent } from "react";
import {
  Routes,
  Route,
  NavLink,
  Navigate,
  useNavigate,
  useRoutes,
} from "react-router-dom";
// import About from "./pages/About";
// import Category from "./pages/Category";
// import Detail from "./pages/Detail";
// import Home from "./pages/Home";
// import HomeRanking from "./pages/HomeRanking";
// import HomeRecommend from "./pages/HomeRecommend";
// import HomeSongMenu from "./pages/HomeSongMenu";
// import Login from "./pages/Login";
// import NotFound from "./pages/NotFound";
// import Order from "./pages/Order";
// import User from "./pages/User";
import routes from "./router";
import "./style.css";

export function App(props) {
  const navigate = useNavigate();
  function navigateTo(path) {
    console.log(path);
    navigate(path);
  }

  return (
    <div className="app">
      <div className="header">
        <span>Header</span>
        <div className="nav">
          <NavLink to="/home">首页</NavLink>
          <NavLink to="/about">关于</NavLink>
          <NavLink to="/login">登录</NavLink>

          <button onClick={(e) => navigateTo("/category")}>分类</button>
          <span onClick={(e) => navigateTo("/order")}>分类</span>

          <NavLink to="/user?name=lyc&age=18">用户</NavLink>
        </div>
        <hr />
      </div>
      <div className="content">
        {/* 映射关系 ：path => Component */}

        {useRoutes(routes)}
      </div>
      <div className="footer">
        <hr />
        Footer
      </div>
    </div>
  );
}

export default App;
```

> /router/index.js

```js
import { Navigate } from "react-router-dom";
// import About from "../pages/About";
import Category from "../pages/Category";
import Detail from "../pages/Detail";
import Home from "../pages/Home";
import HomeRanking from "../pages/HomeRanking";
import HomeRecommend from "../pages/HomeRecommend";
import HomeSongMenu from "../pages/HomeSongMenu";
// import Login from "../pages/Login";
import NotFound from "../pages/NotFound";
import Order from "../pages/Order";
import User from "../pages/User";

import React from 'react'

// 组件懒加载 在webpack中import会自动分包
const About = React.lazy(() => import("../pages/About"))
const Login = React.lazy(() => import("../pages/Login"))

const routes = [
  {
    path: "/",
    element: <Navigate to="/home" />
  },
  { 
    path: "/home",
    element: <Home />,
    children: [
      {
        path: "/home",
        element: <Navigate to="/home/recommend" />
      },
      {
        path: "/home/recommend",
        element: <HomeRecommend />
      },
      {
        path: "/home/ranking",
        element: <HomeRanking />
      },
      {
        path: "/home/songmenu",
        element: <HomeSongMenu />
      }
    ]
  },
  {
    path: "/about",
    element: <About />
  },
  {
    path: "/login",
    element: <Login />
  },
  {
    path: "/category",
    element: <Category />
  },
  {
    path: "/order",
    element: <Order />
  },
  {
    path: "/detail/:id",
    element: <Detail />
  },
  {
    path: "/user",
    element: <User />
  },
  {
    path: "*",
    element: <NotFound />
  },
]

export default routes
```



◼ **如果我们对某些组件进行了异步加载（懒加载），那么需要使用Suspense进行包裹：**

让浏览器在下载js文件时有一个加载时间

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { HashRouter } from "react-router-dom"
import { Suspense } from "react"

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <HashRouter>
      <Suspense fallback={<h3>Loading...</h3>}>
        <App />
      </Suspense>
    </HashRouter>
  </React.StrictMode>
);
```



## 九、ReactHook

### **认识和体验Hooks**

◼ **Hook**是 React 16.8 的新增特性，它可以让我们在不编写class的情况下使用state以及其他的React特性（比如生命周期）。

◼ **我们先来思考一下class组件相对于函数式组件有什么优势？比较常见的是下面的优势：**

◼ class组件可以定义自己的state，用来保存组件自己内部的状态； 

- 函数式组件不可以，因为函数每次调用都会产生新的临时变量；

◼ class组件有自己的生命周期，我们可以在对应的生命周期中完成自己的逻辑； 

- 比如在componentDidMount中发送网络请求，并且该生命周期函数只会执行一次；

- 函数式组件在学习hooks之前，如果在函数中发送网络请求，意味着每次重新渲染都会重新发送一次网络请求；

◼ class组件可以在状态改变时只会重新执行render函数以及我们希望重新调用的生命周期函数componentDidUpdate等；

- 函数式组件在重新渲染时，整个函数都会被执行，似乎没有什么地方可以只让它们调用一次；

◼ **所以，在Hook出现之前，对于上面这些情况我们通常都会编写class组件。**



#### **Class组件存在的问题**

◼ **复杂组件变得难以理解：**

- 我们在最初编写一个class组件时，往往逻辑比较简单，并不会非常复杂。但是随着业务的增多，我们的class组件会变得越来越复杂； 

- 比如componentDidMount中，可能就会包含大量的逻辑代码：包括网络请求、一些事件的监听（还需要在

componentWillUnmount中移除）；

- 而对于这样的class实际上非常难以拆分：因为它们的逻辑往往混在一起，强行拆分反而会造成过度设计，增加代码的复杂度； 

◼ **难以理解的class：** 

- 很多人发现学习ES6的class是学习React的一个障碍。 

- 比如在class中，我们必须搞清楚this的指向到底是谁，所以需要花很多的精力去学习this； 

- 虽然我认为前端开发人员必须掌握this，但是依然处理起来非常麻烦；

◼ **组件复用状态很难**： 

- 在前面为了一些状态的复用我们需要通过高阶组件； 

- 像我们之前学习的redux中connect或者react-router中的withRouter，这些高阶组件设计的目的就是为了状态的复用； 

- 或者类似于Provider、Consumer来共享一些状态，但是多次使用Consumer时，我们的代码就会存在很多嵌套； 

- 这些代码让我们不管是编写和设计上来说，都变得非常困难；



#### **Hook的出现**

◼ **Hook的出现，可以解决上面提到的这些问题；**

◼ **简单总结一下hooks：** 

- 它可以让我们在不编写class的情况下使用state以及其他的React特性； 

- 但是我们可以由此延伸出非常多的用法，来让我们前面所提到的问题得到解决； 

◼ **Hook的使用场景：**

- Hook的出现基本可以代替我们之前所有使用class组件的地方； 

- 但是如果是一个旧的项目，你并不需要直接将所有的代码重构为Hooks，因为它完全向下兼容，你可以渐进式的来使用它； 

- Hook只能在函数组件中使用，不能在类组件，或者函数组件之外的地方使用； 

◼ **在我们继续之前，请记住 Hook 是：**

- 完全可选的**：**你无需重写任何已有代码就可以在一些组件中尝试 Hook。但是如果你不想，你不必现在就去学习或使用 Hook。 

- 100% 向后兼容的**：**Hook 不包含任何破坏性改动。

- 现在可用**：**Hook 已发布于 v16.8.0。

![image-20221116121828999](http://img.roydust.top/img/202211161218098.png)



### **useState**



◼ **State Hook的API就是 useState，我们在前面已经进行了学习：**

- **useState**会帮助我们定义一个 state变量，useState 是一种新方法，它与 class 里面的 this.state 提供的功能完全相同。 
  - 一般来说，在函数退出后变量就会”消失”，而 state 中的变量会被 React 保留。 

- **useState**接受唯一一个参数，在第一次组件被调用时使用来作为初始化值。（如果没有传递参数，那么初始化值为undefined）。

- **useState**的返回值是一个数组，我们可以通过数组的解构，来完成赋值会非常方便。
  - https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

◼ **FAQ：为什么叫 useState 而不叫 createState?** 

- “create” 可能不是很准确，因为 state 只在组件首次渲染的时候被创建。 

- 在下一次重新渲染时，useState 返回给我们当前的 state。 

- 如果每次都创建新的变量，它就不是 “state”了。

- 这也是 Hook 的名字*总是*以 use 开头的一个原因。 

◼ **当然，我们也可以在一个组件中定义多个变量和复杂变量（数组、对象）**



#### **useState解析**

```jsx
const App = memo(() => {
  const [message, setMessage] = useState("Hello World");

  function changeMessage() {
    setMessage("你好 世界");
  }

  return (
    <div>
      <h2>App:{message}</h2>
      <button onClick={changeMessage}>修改文本</button>
    </div>
  );
});
```



◼ **那么我们来研究一下核心的一段代码代表什么意思：**

- useState来自react，需要从react中导入，它是一个hook； 
  - 参数：初始化值，如果不设置为undefined； 
  - 返回值：数组，包含两个元素； 
    - 元素一：当前状态的值（第一调用为初始化值）；
    -  元素二：设置状态值的函数； 

- 点击button按钮后，会完成两件事情：
  - 调用setCount，设置一个新的值； 
  - 组件重新渲染，并且根据新的值返回DOM结构；

◼ **useStateHook原理**

- 在useStateHook中，React会在一个地方将状态保存下来

- 当新的值改变状态时，会使组件重新渲染
- 并且将新的值返回到原来的组件中

![image-20221112172647943](http://img.roydust.top/img/202211121726258.png)

**◼ 但是使用它们会有两个额外的规则：**

- 只能在函数最外层调用 Hook。不要在循环、条件判断或者子函数中调用。 

- 只能在 React 的函数组件中调用 Hook。不要在其他 JavaScript 函数中调用。



### **useEffect**

◼ **目前我们已经通过hook在函数式组件中定义state，那么类似于生命周期这些呢？**

- Effect Hook 可以让你来完成一些**类似于class中生命周期的功能**； 

- 事实上，类似于**网络请求、手动更新DOM、一些事件的监听**，都是React更新DOM的一些副作用（Side Effects）；

- 所以**对于完成这些功能的Hook被称之为 Effect Hook**； 

◼ 假如我们现在有一个需求：**页面的title总是显示counter的数字，使用Hook实现：**

```jsx
import React, { memo, useState, useEffect } from "react";

const App = memo(() => {
  const [count, setCount] = useState(200);

  useEffect(() => {
    // 当前传入的回调函数会在组件被渲染完成后，自动执行
    // 网络请求/DOM操作（修改标签）/事件监听
    document.title = count;
  });

  return (
    <div>
      <h2>当前计数：{count}</h2>
      <button onClick={(e) => setCount(count + 1)}>+1</button>
    </div>
  );
});

export default App;
```

◼ **useEffect的解析：**

- 通过useEffect的Hook，可以告诉**React需要在渲染后执行某些操作**； 

- useEffect**要求我们传入一个回调函数**，在React**执行完更新DOM操作之后，就会回调这个函数**； 

- 默认情况下，**无论是第一次渲染之后**，还是每次更新之后，都会**执行这个 回调函数**；



#### **需要清除Effect**

◼ **在class组件的编写过程中，某些副作用的代码，我们需要在componentWillUnmount中进行清除：**

- 比如我们之前的事件总线或Redux中手动调用subscribe； 

- 都需要在componentWillUnmount有对应的取消订阅； 

- Effect Hook通过什么方式来模拟componentWillUnmount呢？

◼ useEffect传入的**回调函数A**本身可以有一个返回值，这个返回值是另外一个回调函数B：

```jsx
type EffectCallback = () => (void | (() => void | undefined));
```

◼ **为什么要在 effect 中返回一个函数？**

- 这是 effect 可选的清除机制。每个 effect 都可以返回一个清除函数； 

- 如此可以将添加和移除订阅的逻辑放在一起； 

- 它们都属于 effect 的一部分； 

```jsx
import React, { memo, useEffect, useState } from "react";

const App = memo(() => {
  const [count, setCount] = useState(100);
  // 负责告知react，在执行玩当前组件渲染之后要执行的副作用代码
  useEffect(() => {
    // 1.监听事件
    // const unubscribe = store.subscribe(() => {});
    // function foo() {}
    // eventBus.on("why", foo);
    console.log("监听redux数据变化");

    // 返回值：回调函数 => 组件被重新渲染或者组件卸载的时候执行
    return () => {
      console.log("取消监听redux中数据变化");
    };
  });
  return (
    <div>
      <button onClick={(e) => setCount(count + 1)}>+1({count})</button>
    </div>
  );
});

export default App;
```

◼ **React 何时清除 effect？** 

- React 会在组件更新和卸载的时候执行清除操作； 

- 正如之前学到的，effect 在每次渲染的时候都会执行；



#### **使用多个Effect**

◼ **使用Hook的其中一个目的就是解决class中生命周期经常将很多的逻辑放在一起的问题：**

- 比如网络请求、事件监听、手动修改DOM，这些往往都会放在componentDidMount中；

◼ **使用Effect Hook，我们可以将它们分离到不同的useEffect中：**

◼ **Hook 允许我们按照代码的用途分离它们，** 而不是像生命周期函数那样：

- React 将按照 effect 声明的顺序依次调用组件中的每一个effect；

```jsx
import React, { memo, useEffect, useState } from "react";

const App = memo(() => {
  const [count, setCount] = useState(100);
  // 负责告知react，在执行玩当前组件渲染之后要执行的副作用代码
  useEffect(() => {
    // 1.修改document的title
    console.log("修改title");
  });

  // 一个函数式组件中，可以存在多个useEffect
  useEffect(() => {
    // 2.对redux中数据变化监听
    console.log("对redux进行监听");
    return () => {
      // 取消redux中数据的监听
    };
  });

  useEffect(() => {
    // 3.监听eventBus中的why事件
    console.log("对eventBus中的why事件监听");
    return () => {
      // 取消监听eventBus中的why事件
    };
  });

  return (
    <div>
      <button onClick={(e) => setCount(count + 1)}>+1({count})</button>
    </div>
  );
});

export default App;
```



#### **Effect性能优化**

◼ **默认情况下，useEffect的回调函数会在每次渲染时都重新执行，但是这会导致两个问题：**

- 某些代码我们只是希望执行一次即可，类似于componentDidMount和componentWillUnmount中完成的事情；（比如网络请求、订阅和取消订阅）；

- 另外，多次执行也会导致一定的性能问题； 

◼ **我们如何决定useEffect在什么时候应该执行和什么时候不应该执行呢？**

- useEffect实际上有两个参数：

- 参数一：执行的回调函数； 

- 参数二：该useEffect在哪些state发生变化时，才重新执行；（受谁的影响）

◼ **但是，如果一个函数我们不希望依赖任何的内容时，也可以传入一个空的数组 []：** 

- 那么这里的两个回调函数分别对应的就是componentDidMount和componentWillUnmount生命周期函数了；

```jsx
import React, { memo, useEffect, useState } from "react";

const App = memo(() => {
  const [count, setCount] = useState(100);
  const [message, setMessage] = useState("Hello World");
  // 负责告知react，在执行玩当前组件渲染之后要执行的副作用代码
  useEffect(() => {
    // 1.修改document的title
    console.log("修改title");
    // 当count发生变化时才会重新执行
  }, [count]);

  // 一个函数式组件中，可以存在多个useEffect
  useEffect(() => {
    // 2.对redux中数据变化监听
    console.log("对redux进行监听");
    return () => {
      // 取消redux中数据的监听
    };
  }, []);

  useEffect(() => {
    // 3.监听eventBus中的why事件
    console.log("对eventBus中的why事件监听");
    return () => {
      // 取消监听eventBus中的why事件
    };
  }, []);

  useEffect(() => {
    console.log("从服务器获取数据");
  }, []);

  return (
    <div>
      <button onClick={(e) => setCount(count + 1)}>+1({count})</button>
      <button onClick={(e) => setMessage("你好啊")}>{message}</button>
    </div>
  );
});

export default App;
```



### **useContext**

◼ **在之前的开发中，我们要在组件中使用共享的Context有两种方式：**

- 类组件可以通过 类名.contextType = MyContext方式，在类中获取context； 

- 多个Context或者在函数式组件中通过 MyContext.Consumer 方式共享context； 

◼ **但是多个Context共享时的方式会存在大量的嵌套：**

- Context Hook允许我们通过Hook来直接获取某个Context的值； 

```jsx
import { UserContext, ThemeContext } from './05-useContext的使用/content';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <UserContext.Provider value={{ name: "why", level: 99 }}>
    <ThemeContext.Provider value={{ color: "red", size: 30 }}>
      <App />
    </ThemeContext.Provider>
  </UserContext.Provider>
);
```

```js
import { createContext } from "react";

const UserContext = createContext()
const ThemeContext = createContext()

export {
  UserContext, ThemeContext
}
```

```jsx
import React, { memo, useContext } from "react";
import { UserContext, ThemeContext } from "./content";

const App = memo(() => {
  // 使用context
  const user = useContext(UserContext);
  const theme = useContext(ThemeContext);

  return (
    <div>
      <h2>
        User:{user.name}-{user.level}
      </h2>
      <h2 style={{ color: theme.color, fontSize: theme.size }}>Theme</h2>
    </div>
  );
});

export default App;
```

◼ **注意事项：**

- 当组件上层最近的 <MyContext.Provider> 更新时，该 Hook 会触发重新渲染，并使用最新传递给 MyContext provider 的 context value 值。



### **useReducer**

◼ **很多人看到useReducer的第一反应应该是redux的某个替代品，其实并不是。**

◼ **useReducer仅仅是useState的一种替代方案：**

- 在某些场景下，如果state的处理逻辑比较复杂，我们可以通过useReducer来对其进行拆分； 

- 或者这次修改的state需要依赖之前的state时，也可以使用；

```jsx
import React, { memo, useReducer, useState } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { ...state, counter: state.counter + 1 };
    case "decrement":
      return { ...state, counter: state.counter - 1 };
    case "add_number":
      return { ...state, counter: state.counter + action.num };
    case "sub_number":
      return { ...state, counter: state.counter - action.num };
    default:
      return state;
  }
}

const App = memo(() => {
  // const [count, setCount] = useState(0);

  const [state, dispatch] = useReducer(reducer, { counter: 0 });
  return (
    <div>

      <h2>当前计数：{state.count}</h2>
      <button onClick={(e) => dispatch({ type: "increment" })}>+1</button>
      <button onClick={(e) => dispatch({ type: "decrement" })}>-1</button>
      <button onClick={(e) => dispatch({ type: "add_number", num: 5 })}>
        +5
      </button>
      <button onClick={(e) => dispatch({ type: "sub_number", num: 5 })}>
        -5
      </button>
      <button onClick={(e) => dispatch({ type: "add_number", num: 100 })}>
        +100
      </button>
    </div>
  );
});

export default App;
```

◼ **数据是不会共享的，它们只是使用了相同的counterReducer的函数而已。**

◼ **所以，useReducer只是useState的一种替代品，并不能替代Redux。**



### **useCallback**

◼ **useCallback实际的目的是为了进行性能的优化。**

◼ **如何进行性能的优化呢？**

- useCallback会返回一个函数的 memoized（记忆的） 值； 

- 在依赖不变的情况下，多次定义的时候，返回的值是相同的；

◼ **通常使用useCallback的目的是不希望子组件进行多次渲染，并不是为了函数进行缓存；**

```jsx
import React, { memo, useCallback, useRef, useState } from "react";

// useCallback性能优化的点：
// 1.当需要一个函数传递给子组件时，最好使用useCallback进行优化，将优化之后的函数，传递给子组件(只有传递的props发生改变时才会重新渲染组件)

// 当props发生改变时，组件就会被重新渲染
const LYCIncrement = memo((props) => {
  const { increment } = props;
  console.log("组件被重新渲染");
  return (
    <div>
      <button onClick={increment}>increment+1</button>
    </div>
  );
});

const App = memo(() => {
  const [count, setCount] = useState(0);
  const [message, setMassage] = useState("hello");

  // 普通的函数
  // const increment = () => {
  //   setCount(count + 1);
  // };

  // 闭包陷阱: useCallback
  // const increment = useCallback(
  //   function () {
  //     setCount(count + 1);
  //   },
  //   [count]
  // );

  // 进一步优化：当count发生改变时，也使用同一个函数
  // 做法一：将count依赖移除掉，缺点：闭包陷阱
  // 做法二：useRef，在组件渲染时，返回同一个值
  const countRef = useRef();
  countRef.current = count;
  const increment = useCallback(function () {
    setCount(countRef.current + 1);
  }, []);

  return (
    <div> 
      <h2>计数：{count}</h2>
      <button onClick={increment}>+1</button>
      <LYCIncrement increment={increment}></LYCIncrement>
      <h2>message:{message}</h2>
      <button onClick={(e) => setMassage(Math.random())}>修改message</button>
    </div>
  );
});

export default App;
```



### **useMemo**

◼ **useMemo实际的目的也是为了进行性能的优化。**

◼ 如何进行性能的优化呢？

- useMemo返回的也是一个 memoized（记忆的） 值；

- 在依赖不变的情况下，多次定义的时候，返回的值是相同的；

```jsx
import React, { memo, useMemo, useState } from "react";

const HelloWorld = memo(function (props) {
  console.log("Hello World组件被重新渲染了哦");
  return <h2>Hello World</h2>;
});

function calcNumTotal(num) {
  console.log("重新计数了哦");
  let total = 0;
  for (let i = 1; i <= num; i++) {
    total += i;
  }
  return total;
}

const App = memo(() => {
  const [count, setCount] = useState(0);

  // const result = calcNumTotal(50);

  // 1.不依赖任何的值,进行计算 只会计算一次
  // let result = useMemo(() => {
  //   return calcNumTotal(50);
  // }, []);

  // useMemo拿到的是他的返回值
  // 2.依赖count
  let result = useMemo(() => {
    return calcNumTotal(count * 2);
  }, [count]);

  // 3.useMemo实现useCallback功能
  // function fn() {}
  // const increment = useCallback(fn, []);
  // const increment2 = useMemo(() => fn, []);

  // 4.使用useMemo对子组件渲染进行优化
  // const info = { name: "lyc", age: 18 }; 会使子组件重新渲染
  const info = useMemo(() => ({ name: "lyc", age: 18 }), []);

  return (
    <div>
      <h2>计算结果: {result}</h2>
      <h2>计数器：{count}</h2>
      <button onClick={(e) => setCount(count + 1)}>+1</button>
      <HelloWorld result={result} info={info}></HelloWorld>
    </div>
  );
});

export default App;
```





### **useRef**

◼ **useRef返回一个ref对象，返回的ref对象再组件的整个生命周期保持不变。**

◼ **最常用的ref是两种用法：**

- 用法一：引入DOM（或者组件，但是需要是class组件）元素；

- 用法二：保存一个数据，这个对象在整个生命周期中可以保存不变；

> 绑定DOM

```jsx
import React, { memo, useRef } from "react";

const App = memo(() => {
  const titleRef = useRef();
  const inputRef = useRef();

  function showTitleDom() {
    console.log(titleRef.current);
    inputRef.current.focus();
  }
  return (
    <div>
      <h2 ref={titleRef}>Hello World</h2>
      <input type="text" ref={inputRef} />
      <button onClick={showTitleDom}>查看title的dom</button>
    </div>
  );
});

export default App;
```



> 保存数据

```jsx
import React, { memo, useCallback, useRef, useState } from "react";

let obj = null;

const App = memo(() => {
  const [count, setCount] = useState(0);
  const nameRef = useRef();
  console.log(obj === nameRef);
  obj = nameRef;

  // 通过useRef解决闭包陷阱
  const countRef = useRef();
  countRef.current = count;

  const increment = useCallback(() => {
    setCount(countRef.current + 1);
  }, []);

  return (
    <div>
      <h2>Hello World:{count}</h2>
      <button onClick={(e) => setCount(count + 1)}>+1</button>
      <button onClick={increment}>+1</button>
    </div>
  );
});

export default App;
```



### 其他Hooks的使用

#### **useImperativeHandle**

◼ **我们先来回顾一下ref和forwardRef结合使用：**

- 通过forwardRef可以将ref转发到子组件；

- 子组件拿到父组件中创建的ref，绑定到自己的某一个元素中；

◼ **forwardRef的做法本身没有什么问题，但是我们是将子组件的DOM直接暴露给了父组件：**

- 直接暴露给父组件带来的问题是某些情况的不可控；

- 父组件可以拿到DOM后进行任意的操作；

- 但是，事实上在上面的案例中，我们只是希望父组件可以操作的focus，其他并不希望它随意操作；

◼ **通过useImperativeHandle可以值暴露固定的操作：**

- 通过useImperativeHandle的Hook，将传入的ref和useImperativeHandle第二个参数返回的对象绑定到了一起；

- 所以在父组件中，使用 inputRef.current时，实际上使用的是返回的对象；

- 比如我调用了 focus函数，甚至可以调用 printHello函数；

```jsx
import React, { memo, useRef, forwardRef, useImperativeHandle } from "react";

const HelloWorld = memo(
  forwardRef((props, ref) => {
    // 可以在子组件内部定义ref
    const inputRef = useRef();

    // 子组件对父组件传入的ref进行处理
    useImperativeHandle(ref, () => {
      return {
        focus() {
          console.log("focus");
          inputRef.current.focus();
        },
        setValue(value) {
          inputRef.current.value = value;
        },
      };
    });

    // 如果ref直接绑定组件，就会可能有操作危险
    return <input type="text" ref={inputRef} />;
  })
);
const App = memo(() => {
  const titleRef = useRef();
  const inputRef = useRef();

  function handleDOM() {
    // console.log(inputRef.current);
    inputRef.current.focus();
    // inputRef.current.value = "";
    inputRef.current.setValue("哈哈哈");
  }
  return (
    <div>
      <h2 ref={titleRef}>哈哈哈</h2>
      <HelloWorld ref={inputRef} />
      <button onClick={handleDOM}>DOM操作</button>
    </div>
  );
});

export default App;
```



#### **useLayoutEffect**

◼ **useLayoutEffect看起来和useEffect非常的相似，事实上他们也只有一点区别而已：**

- useEffect会在渲染的内容更新到DOM上后执行，不会阻塞DOM的更新；

- useLayoutEffect会在渲染的内容更新到DOM上之前执行，会阻塞DOM的更新；

◼ **如果我们希望在某些操作发生之后再更新DOM，那么应该将这个操作放到useLayoutEffect。** 

![image-20221116170348305](http://img.roydust.top/img/202211161703465.png)

◼ **官方更推荐使用useEffect而不是useLayoutEffect。**

```jsx
import React, { memo, useEffect, useLayoutEffect, useState } from "react";

const App = memo(() => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("useEffect");
  });

  useLayoutEffect(() => {
    console.log("useLayoutEffect");
  });

  console.log("App render");

  return (
    <div>
      <h2>count:{count}</h2>
      <button onClick={(e) => setCount(count + 1)}> +1 </button>
    </div>
  );
});

export default App;
```



#### useId

◼ **官方的解释：useId 是一个用于生成横跨服务端和客户端的稳定的唯一 ID 的同时避免 hydration 不匹配的 hook。** 

◼ **这里有一个词叫hydration，要想理解这个词，我们需要理解一些服务器端渲染（SSR）的概念。**

#####  **什么是SSR？** 

- SSR（**Server Side Rendering，服务端渲染**），指的是页面在服务器端已经生成了完成的HTML页面结构，不需要浏览器解析；

- 对应的是CSR（**Client Side Rendering，客户端渲染**），我们开发的SPA页面通常依赖的就是客户端渲染；![image-20221117165149043](http://img.roydust.top/img/202211171651170.png)

◼ **早期的服务端渲染包括PHP、JSP、ASP等方式，但是在目前前后端分离的开发模式下，前端开发人员不太可能再去学习PHP、JSP等技术来开发网页；**

◼ **不过我们可以借助于Node来帮助我们执行JavaScript代码，提前完成页面的渲染；**

◼ **SPA的缺陷和服务器渲染SSR的优势**

![image-20221116200730442](http://img.roydust.top/img/202211162007598.png)



##### **SSR同构应用**

◼ **什么是同构？**

- 一套代码既可以在服务端运行又可以在客户端运行，这就是同构应用。

◼ **同构是一种SSR的形态，是现代SSR的一种表现形式。**

- 当用户发出请求时，先在服务器通过SSR渲染出首页的内容。

- 但是对应的代码同样可以在客户端被执行。

- 执行的目的包括事件绑定等以及其他页面切换时也可以在客户端被渲染；

![image-20221117165657631](http://img.roydust.top/img/202211171656754.png)



##### **Hydration**

◼ 什么是Hydration？这里我引入**vite-plugin-ssr**插件的官方解释。

![image-20221117165750681](http://img.roydust.top/img/202211171657760.png)

◼ **在进行** **SSR** **时，我们的页面会呈现为** **HTML**。

- 但仅 HTML 不足以使页面具有交互性。例如，浏览器端 JavaScript 为零的页面不能是交互式的（没有 JavaScript 事件处理程序来响应用户操作，例如单击按钮）。

- 为了使我们的页面具有交互性，除了在 Node.js 中将页面呈现为 HTML 之外，我们的 UI 框架（Vue/React/...）还在浏览器中加载和呈现页面。（它创建页面的内部表示，然后将内部表示映射到我们在 Node.js 中呈现的 HTML 的 DOM 元素。）

◼ **这个过程称为hydration**



##### **useId的作用**

◼ **我们再来看一遍：useId 是一个用于生成横跨服务端和客户端的稳定的唯一 ID 的同时避免 hydration 不匹配的 hook。** 

◼ **所以我们可以得出如下结论：**

- useId是用于react的同构应用开发的，前端的SPA页面并不需要使用它；

- useId可以保证应用程序在客户端和服务器端生成唯一的ID，这样可以有效的避免通过一些手段生成的id不一致，造成hydration mismatch；

```jsx
import React, { memo, useId, useState } from "react";

const App = memo(() => {
  const [count, setCount] = useState(0);
  const id = useId();
  console.log(id);
  return (
    <div>
      <button onClick={(e) => setCount(count + 1)}>count+1:{count}</button>

      <label htmlFor={id}>
        用户名：
        <input type="text" id={id} />
      </label>
    </div>
  );
});

export default App;
```



#### **useTransition**

◼ **官方解释：**返回一个状态值表示过渡任务的等待状态，以及一个启动该过渡任务的函数。

- 事实上官方的说法，还是让人云里雾里，不知所云。

◼ **useTransition到底是干嘛的呢？它其实在告诉react对于某部分任务的更新优先级较低，可以稍后进行更新。**

```jsx
import React, { memo, useState, useTransition } from "react";
import namesArray from "./namesArray";

const App = memo(() => {
  const [showNames, setShowNames] = useState(namesArray);

  //useTransition会延迟更新，让html页面先渲染再进行高耗时的js操作后再次渲染
  const [pending, startTransition] = useTransition();

  function valueChangeHandle(e) {
    startTransition(() => {
      const keyword = e.target.value;
      const filterShowNames = namesArray.filter((item) =>
        item.includes(keyword)
      );
      setShowNames(filterShowNames);
    });
  }

  return (
    <div>
      <input type="text" onInput={(e) => valueChangeHandle(e)} />
      <h2>用户名列表：{pending && <span>data loading</span>}</h2>
      <ul>
        {showNames.map((item, index) => {
          return <li key={index}>{item}</li>;
        })}
      </ul>
    </div>
  );
});

export default App;
```



#### **useDeferredValue**

◼ **官方解释：useDeferredValue 接受一个值，并返回该值的新副本，该副本将推迟到更紧急地更新之后。**

◼ **在明白了useTransition之后，我们就会发现useDeferredValue的作用是一样的效果，可以让我们的更新延迟。**

```jsx
import React, { memo, useDeferredValue, useState, useTransition } from "react";
import namesArray from "./namesArray";

const App = memo(() => {
  const [showNames, setShowNames] = useState(namesArray);
  // useDeferredValue 会生成一个延迟渲染的数据
  const deferedShowNames = useDeferredValue(showNames);

  function valueChangeHandle(e) {
    const keyword = e.target.value;
    const filterShowNames = namesArray.filter((item) => item.includes(keyword));
    setShowNames(filterShowNames);
  }

  return (
    <div>
      <input type="text" onInput={(e) => valueChangeHandle(e)} />
      <h2>用户名列表：</h2>
      <ul>
        {deferedShowNames.map((item, index) => {
          return <li key={index}>{item}</li>;
        })}
      </ul>
    </div>
  );
});

export default App;
```





### **自定义Hooks使用**

◼ **自定义Hook本质上只是一种函数代码逻辑的抽取，严格意义上来说，它本身并不算React的特性。**

#### 案例一：所有的组件在创建和销毁时都进行打印

```jsx
import React, { memo, useEffect, useState } from "react";

function useLogLife(cName) {
  useEffect(() => {
    console.log(cName + "组件被创建");
    return () => {
      console.log(cName + "组件被销毁");
    };
  }, [cName]);
}

const Home = memo(() => {
  useLogLife("home");
  return <h1>Home Page</h1>;
});

const About = memo(() => {
  useLogLife("about");
  return <h1>About Page</h1>;
});

const App = memo(() => {
  const [isShow, setIsShow] = useState(true);
  useLogLife("root");
  return (
    <div>
      <h1>App Root Component</h1>
      <button onClick={(e) => setIsShow(!isShow)}>切换</button>
      {isShow && <Home />}
      {isShow && <About />}
    </div>
  );
});

export default App;
```



#### 案例二：**Context的共享**

```jsx
import React, { memo } from "react";
import { useUserToken } from "./hooks";

const Home = memo(() => {
  const [user, token] = useUserToken();
  return (
    <h1>
      Home Page:{user.name}-{token}
    </h1>
  );
});

const About = memo(() => {
  const [user, token] = useUserToken();
  return (
    <h1>
      About Page:{user.name}-{token}
    </h1>
  );
});

const App = memo(() => {
  return (
    <div>
      <h1>App Root Component</h1>
      <Home />
      <About />
    </div>
  );
});

export default App;
```

> ./hooks/useUserToken.js

```js
import { useContext } from "react";
import { UserContext, TokenContext } from "../context";

function useUserToken() {
  const user = useContext(UserContext)
  const token = useContext(TokenContext)

  return [user, token]
}

export default useUserToken
```

>./context/index.js

```js
import { createContext } from "react";

const UserContext = createContext()
const TokenContext = createContext()

export {
  UserContext, TokenContext
}
```

> index.js

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import { UserContext, TokenContext } from './12-自定义Hooks/context';

import App from './12-自定义Hooks/App';


const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <UserContext.Provider value={{ name: "why", level: 99 }}>
    <TokenContext.Provider value={'lyc'}>
      <App />
    </TokenContext.Provider>
  </UserContext.Provider>
);
```



#### 案例三：**获取滚动位置**

```jsx
import React, { memo } from "react";
import "../12-自定义Hooks/style.css";
import { useScrollPosition } from "./hooks";

const Home = memo(() => {
  const [scrollX, scrollY] = useScrollPosition();

  return (
    <h1>
      Home Page:{scrollX}-{scrollY}
    </h1>
  );
});

const About = memo(() => {
  const [scrollX, scrollY] = useScrollPosition();
  return (
    <h1>
      About Page:{scrollX}-{scrollY}
    </h1>
  );
});

const App = memo(() => {
  return (
    <div className="app">
      <h1>App Root Component</h1>
      <Home />
      <About />
    </div>
  );
});

export default App;
```

> ./hooks/useScrollPosition

```js
import { useEffect, useState } from "react";

function useScrollPosition() {
  const [scrollX, setScrollX] = useState(0)
  const [scrollY, setScrollY] = useState(0)

  useEffect(() => {
    function handleScroll() {
      setScrollX(window.scrollX)
      setScrollY(window.scrollY)
    }

    window.addEventListener("scroll", handleScroll);

    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  }, []);

  return [scrollX, scrollY]
}

export default useScrollPosition
```



#### 案例四：**localStorage数据存储**

```jsx
import React, { memo, useEffect, useState } from "react";
import { useLocalStorage } from "./hooks";

const App = memo(() => {
  // 通过key,直接从loaclStorage中获取一个数据
  const [token, setToken] = useLocalStorage("token");
  function setTokenHandle() {
    setToken("james");
  }

  const [avatarUrl, setAvatarUrl] = useLocalStorage("avatarUrl");

  function setAvatarUrlHandle() {
    setAvatarUrl("http://www.roydust.com/abc.png");
  }

  return (
    <div className="app">
      <h1>App Root Component: {token}</h1>
      <button onClick={setTokenHandle}>设置token</button>
      <h1>avatarURL:{avatarUrl}</h1>
      <button onClick={setAvatarUrlHandle}>设置新头像地址</button>{" "}
    </div>
  );
});

export default App;

```

> ./hooks/useLocalStorage.js

```jsx
import { useEffect, useState } from "react"

function useLocalStorage(key) {
  const [data, setData] = useState(() => {
    // 1.从loacalStorage中获取数据，并且数据创建的组件的state
    const item = JSON.parse(localStorage.getItem(key))
    if (!item) return ""
    return JSON.parse(item)
  })

  // 2.监听data改变，一旦发生改变就会存储data的最新值
  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(data))
  }, [data])

  // 3.将data/setData的操作返回组件，让组件可以使用和修改
  return [data, setData]
}

export default useLocalStorage
```











useSelector监听的是全部的state，所以在父组件的count发生变化时，子组件也会重新渲染

![image-20221116193431350](http://img.roydust.top/img/202211161934526.png)



### **redux hooks**

◼ **在之前的redux开发中，为了让组件和redux结合起来，我们使用了react-redux中的connect：** 

- 但是这种方式必须使用高阶函数结合返回的高阶组件；

- 并且必须编写：mapStateToProps和 mapDispatchToProps映射的函数；

◼ **在Redux7.1开始，提供了Hook的方式，我们再也不需要编写connect以及对应的映射函数了**

◼ **useSelector**的作用是将state映射到组件中：

- 参数一：将state映射到需要的数据中；

- 参数二：可以进行比较来决定是否组件重新渲染； 

◼ **useSelector**默认会比较我们返回的两个对象是否相等；

- 如何比较呢？ const refEquality = (a, b) => a === b； 
- 第二参数可以传入shallowEqual会比较映射前后的数据变化 如果没有变化就不会重新渲染

- 也就是我们必须返回两个完全相等的对象才可以不引起重新渲染；

◼ **useDispatch非常简单，就是直接获取dispatch函数，之后在组件中直接使用即可；**

◼ **我们还可以通过useStore来获取当前的store对象；**

```jsx
import React, { memo } from "react";
import { useSelector, useDispatch, shallowEqual } from "react-redux";
import {
  addNumberAction,
  changeMessageAction,
  subNumberAction,
} from "./store/modules/counter";

// memo高阶组件包裹起来的组件有对应的特点: 只有props发生改变时, 才会重新渲染
const Home = memo((props) => {
  const { message } = useSelector(
    (state) => ({
      message: state.counter.message,
    }),
    // shallowEqual 会比较映射前后的数据变化 如果没有变化就不会重新渲染
    shallowEqual
  );

  const dispatch = useDispatch();
  function changeMessageHandle() {
    dispatch(changeMessageAction("你好啊, 师姐!"));
  }

  console.log("Home render");

  return (
    <div>
      <h2>Home: {message}</h2>
      <button onClick={(e) => changeMessageHandle()}>修改message</button>
    </div>
  );
});

const App = memo((props) => {
  // 1.使用useSelector将redux中store的数据映射到组件内
  const { count } = useSelector(
    (state) => ({
      count: state.counter.count,
    }),
    shallowEqual
  );

  // 2.使用dispatch直接派发action
  const dispatch = useDispatch();
  function addNumberHandle(num, isAdd = true) {
    if (isAdd) {
      dispatch(addNumberAction(num));
    } else {
      dispatch(subNumberAction(num));
    }
  }

  console.log("App render");

  return (
    <div>
      <h2>当前计数: {count}</h2>
      <button onClick={(e) => addNumberHandle(1)}>+1</button>
      <button onClick={(e) => addNumberHandle(6)}>+6</button>
      <button onClick={(e) => addNumberHandle(6, false)}>-6</button>

      <Home />
    </div>
  );
});

export default App;
```



### ReactHooks的闭包陷阱

```js
import { useEffect, useState } from 'react';

function Dong() {

    const [count,setCount] = useState(0);

    useEffect(() => {
        setInterval(() => {
            setCount(count + 1);
        }, 500);
    }, []);

    useEffect(() => {
        setInterval(() => {
            console.log(count);
        }, 500);
    }, []);

    return <div>guang</div>;
}

export default Dong;
```

用 useState 创建了个 count 状态，在一个 useEffect 里定时修改它，另一个 useEffect 里定时打印最新的 count 值。

我们跑一下：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cd481a83f09b4af78ce487c032a44dc4~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp?)

打印的并不是我们预期的 0、1、2、3，而是 0、0、0、0，这是为什么呢？

这就是所谓的闭包陷阱!

如何解决呢？

```jsx
import { useEffect, useState } from 'react';

function Dong() {

    const [count,setCount] = useState(0);

    useEffect(() => {
        setInterval(() => {
            setCount(count + 1);
        }, 500);
    }, [count]);

    useEffect(() => {
        setInterval(() => {
            console.log(count);
        }, 500);
    }, [count]);

    return <div>guang</div>;
}

export default Dong;
```

这样每次 count 变了就会执行引用了最新 count 的函数了：

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/704e2df024cf4d74adcfddd45bb606d3~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp?)

现在确实不是全 0 了，但是这乱七八遭的打印是怎么回事？

那是因为现在确实是执行传入的 fn 来设置新定时器了，但是之前的那个没有清楚呀，需要加入一段清除逻辑：

```jsx
import { useEffect, useState } from 'react';

function Dong() {

    const [count,setCount] = useState(0);

    useEffect(() => {
        const timer = setInterval(() => {
            setCount(count + 1);
        }, 500);
        return () => clearInterval(timer);
    }, [count]);

    useEffect(() => {
        const timer = setInterval(() => {
            console.log(count);
        }, 500);
        return () => clearInterval(timer);
    }, [count]);

    return <div>guang</div>;
}

export default Dong;
```

加上了 clearInterval，每次执行新的函数之前会把上次设置的定时器清掉。

再试一下：

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b4bbe8b392014e459306914f5a17b81f~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp?)

现在就是符合我们预期的了，打印 0、1、2、3、4。

很多同学学了 useEffect 却不知道要返回一个清理函数，现在知道为啥了吧。就是为了再次执行的时候清掉上次设置的定时器、事件监听器等的。

这样我们就完美解决了 hook 闭包陷阱的问题。



**我们了解 hooks 的实现原理：**

[从根上理解 React Hooks 的闭包陷阱](https://juejin.cn/post/7093699777556119565)

在 fiber 节点的 memorizedState 属性存放一个链表，链表节点和 hook 一一对应，每个 hook 都在各自对应的节点上存取数据。

useEffect、useMomo、useCallback 等都有 deps 的参数，实现的时候会对比新旧两次的 deps，如果变了才会重新执行传入的函数。所以 undefined、null 每次都会执行，[] 只会执行一次，[state] 在 state 变了才会再次执行。

**闭包陷阱产生的原因就是 useEffect 等 hook 里用到了某个 state，但是没有加到 deps 数组里，这样导致 state 变了却没有执行新传入的函数，依然引用的之前的 state。**

**闭包陷阱的解决也很简单，正确设置 deps 数组就可以了，这样每次用到的 state 变了就会执行新函数，引用新的 state。不过还要注意要清理下上次的定时器、事件监听器等。**

要理清 hooks 闭包陷阱的原因是要理解 hook 的原理的，什么时候会执行新传入的函数，什么时候不会。

hooks 的原理确实也不难，就是在 memorizedState 链表上的各节点存取数据，完成各自的逻辑的，唯一需要注意的是 deps 数组引发的这个闭包陷阱问题。
