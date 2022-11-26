# **Vue3学习笔记**

# 一、基础语法

## 1.template写法

​	方式一:使用script标签66577

![image-20211110171350174](https://i.loli.net/2021/11/10/tU4sCrh6vdWQNRJ.png)

方式二:使用template

![image-20211110171444113](https://i.loli.net/2021/11/10/I9yP4XWpvZnK5fF.png)

这个时候,在createApp的对象中,我们需要传入的template以#开头:
如果字符串是以#开始,那么它将被用作querySelector ,并且使用匹配元素的innerHTML作为模板字符串;

## 2.Data属性

- data属性是传入一 个函数,并且该函数需要返回一个对象:
  - 在Vue2.x的时候,也可以传入一个对象(虽然官方推荐是一个函数) ;
  - 在Vue3..x的时候,比如传入一个函数,否则就会直接在浏览器中报错;
- data中返回的对象会被Vue的响应式系统劫持,之后对该对象的修改或者访问都会在劫持中被处理: 
  - 所以我们在template中通过{{counter}} 访问counter ,可以从对象中获取到数据;
  - 所以我们修改counter的值时, template中的{{counter}}也会发生改变;

## 3.methods属性

methods属性是一个对象,通常我们会在这个对象中定义很多的方法:

- 这些方法可以被绑定到template模板中;

- 在该方法中,我们可以使用this关键字来直接访问到data中返回的对象的属性;

- 如果想要学习Vue的源码，比如看createApp的实现过程，应该怎么办呢？

- 第一步：在GitHub上搜索 vue-next，下载源代码；

  - 这里推荐通过 git clone 的方式下载；

- 第二步：安装Vue源码项目相关的依赖；

  - 执行 yarn install

- 第三步：对项目执行打包操作

  - 执行yarn dev（执行前修改脚本）

    ![image-20211110175734724](https://i.loli.net/2021/11/10/dQO6NGwWVhtKyj1.png)

- 第四步：通过 packages/vue/dist/vue.global.js 调试代码

## 一. 知识补充

###  1.1. methods中的this

#### 1.1.1. 不能使用箭头函数

我们在methods中要使用data返回对象中的数据，那么这个this是必须有值的，并且应该可以通过this获取到data返回对象中的数据。

那么我们这个this能不能是window呢？

- 不可以是window，因为window中我们无法获取到data返回对象中的数据；
- 但是如果我们使用箭头函数，那么这个this就会是window了；

我们来看下面的代码：

- 我将increment换成了箭头函数，那么它其中的this进行打印时就是window；

```vue
tmlconst App = {
  template: "#my-app",
  data() {
    return {
      counter: 0
    }
  },
  methods: {
    increment: () => {
      // this.counter++;
      console.log(this);
    },
    decrement() {
      this.counter--;
    }
  }
}
```

为什么是window呢？

- 这里涉及到箭头函数使用this的查找规则，它会在自己的上层作用域中来查找this；
- 最终刚好找到的是script作用域中的this，所以就是window；

this到底是如何查找和绑定的呢？

- 在我的公众号有另外一篇文章，专门详细的讲解了this的绑定规则；
- https://mp.weixin.qq.com/s/hYm0JgBI25grNG_2sCRlTA；
- 认真学习之后你绝对对this的绑定一清二楚；

#### 1.1.2. this到底指向什么

事实上Vue的源码当中就是对methods中的所有函数进行了遍历，并且通过bind绑定了this：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BibEXe7FB2uibM1ictoXEPWEsbQZfDCT6GnyVeQzGCu8bFEvLqYXDCUufg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)vue3源码的this绑定过程

### 1.2. VSCode增加代码片段

我们在前面练习Vue的过程中，有些代码片段是需要经常写的，我们在VSCode中我们可以生成一个代码片段，方便我们快速生成。

VSCode中的代码片段有固定的格式，所以我们一般会借助于一个在线工具来完成。

具体的步骤如下：

- 第一步，复制自己需要生成代码片段的代码；
- 第二步，https://snippet-generator.app/在该网站中生成代码片段；

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BRgXbO9nLiaPpLsiaQia4fdL4TNpDxKjq8XJtVxWSiamAaPHKHeiaq2HjyYw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)生成代码片段

- 第三步，在VSCode中生成代码片段；

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BlETfc0huGhCaBkggoaR4AIA9vjNnOqibZYjqu1VEOFmVlSYCyw0uW9Q/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)打开生成代码片段的配置

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BzwbDFHpr65aRJTRbibpU9UCusribqAcNwWvDKQckComNsqXSv8xVWLZg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)选择HTML

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BwBWV5zGfhqick90GOP7oHNuniaMHaXv8BforlgzDZHZjJcXL1PS9hQZg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)生成代码片段

## 二. 模板语法

React的开发模式：

- React使用的jsx，所以对应的代码都是编写的类似于js的一种语法；
- 之后通过Babel将jsx编译成 `React.createElement` 函数调用；

Vue也支持jsx的开发模式（后续有时间也会讲到）：

- 但是大多数情况下，使用基于HTML的模板语法；
- 在模板中，允许开发者以声明式的方式将DOM绑定到底层组件实例的数据；
- 在底层的实现中，Vue将模板编译成虚拟DOM渲染函数，这个我会在后续给大家讲到；

所以，对于学习Vue来说，学习模板语法是非常重要的。

### 2.1. 插值语法

#### 2.1.1. mustache语法

如果我们希望把数据显示到模板（template）中，使用最多的语法是 “Mustache”语法 (双大括号) 的文本插值：

```html
<div>{{message}}</div>
```

并且我们前端提到过，data返回的对象是有添加到Vue的响应式系统中，当data中的数据发生改变时，对应的内容也会发生更新。

当然，Mustache中不仅仅可以是data中的属性，也可以是一个JavaScript的表达式：

```html
<body>
  <div id="app"></div>

  <template id="my-app">
    <div>
      <!-- mustache基本使用 -->
      <h2>{{message}}</h2>
      <!-- JavaScript表达式 -->
      <h2>{{ counter * 2}}</h2>
      <h2>{{message.split(" ").reverse().join(" ")}}</h2>
      <!-- 调用一个methods中的函数 -->
      <h2>{{reverse(message)}}</h2>
    </div>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    // 创建App组件
    const App = {
      template: '#my-app',
      data() {
        return {
          message: "Hello World",
          counter: 10,
        }
      },
      methods: {
        reverse(msg) {
          return msg.split(" ").reverse().join(" ")
        }
      }
    }

    // 创建应用程序, 并且挂载
    Vue.createApp(App).mount('#app');
  </script>
</body>
```

但是下面的代码是错误的：

```html
<!-- 错误的写法 -->
<!-- 这是一个赋值语句, 不是表达式 -->
<h2>{{var name = "Hello"}}</h2>
<!-- 控制流的if语句也是不支持的, 可以使用三元运算符 -->
<h2>{{ if (true) { return message } }}</h2>
```

三元运算符是可以的：

```html
<!-- 三元运算符 -->
<h2>{{ true ? message: counter }}</h2>
```

#### 2.1.2. v-once

用于指定元素或者组件只渲染一次：

- 当数据发生变化时，元素或者组件以及其所有的自己诶单将视为静态内容并且跳过；
- 该指令可以用于性能优化；

```html
<h2 v-once>当前计数: {{counter}}</h2>
<button @click="increment">+1</button>
```

如果是子节点，也是只会渲染一次：

```html
<div v-once>
  <h2>当前计数: {{counter}}</h2>
  <button @click="increment">+1</button>
</div>
```

#### 2.1.3. v-text

用于更新元素的 textContent：

```html
<span v-text="msg"></span>
<!-- 等价于 -->
<span>{{msg}}</span>
```

#### 2.1.4. v-html

默认情况下，如果我们展示的内容本身是 html 的，那么vue并不会对其进行特殊的解析。

如果我们希望这个内容被Vue可以解析出来，那么可以使用 v-html 来展示：

```html
<body>
  <div id="app"></div>

  <template id="my-app">
    <div v-html='info'></div>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          info: `<span style='color: red; font-size: 30px'>哈哈哈</span>`
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
</body>
```

#### 2.1.5. v-pre

v-pre用于跳过元素和它的子元素的编译过程，显示原始的Mustache标签：

- 跳过不需要编译的节点，加快编译的速度；

```html
<div v-pre>{{message}}</div>
```

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BYvr1ANPmRklP3HyMKfGm08RdTkLU0uFDyhibGlqCEd3dQOHLCqM6dAw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)显示效果

#### 2.1.6. v-cloak

这个指令保持在元素上直到关联组件实例结束编译。

和 CSS 规则如 `[v-cloak] { display: none }` 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到组件实例准备完毕。

```html
[v-cloak] {
  display: none;
}
<div v-cloak>
  {{ message }}
</div>
```

<div> 不会显示，直到编译结束。

### 2.2. v-bind

前端讲的一系列指令，主要是和内容相关的，元素除了内容之外还会有各种各样的属性。

绑定属性我们使用v-bind：

- **缩写**：`:`

- **预期**：`any (with argument) | Object (without argument)`

- **参数**：`attrOrProp (optional)`

- **修饰符**：

- - `.camel` - 将 kebab-case attribute 名转换为 camelCase。

- **用法**：动态地绑定一个或多个 attribute，或一个组件 prop 到表达式。

#### 2.2.1. 绑定基本属性

前面我们讲的Mustache等语法主要是将内容插入到 `innerHTML` 中。

很多时候，元素的属性也是动态的：

- 比如a元素的href属性、img元素的src属性；

```html
  <div id="app"></div>

  <template id="my-app">
    <div>{{message}}</div>
    <img v-bind:src="src" alt="">
    <!-- 语法糖写法 -->
    <img :src="src" alt="">
    <!-- 注意这两种写法的不同 -->
    <img src="src" alt="">

    <!-- 绑定a元素 -->
    <a :href="href"></a>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          message: "Hello World",
          src: "https://avatars.githubusercontent.com/u/10335230?v=4",
          href: "http://www.baidu.com"
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
```

#### 2.2.2. 绑定class属性

**对象语法**

- 我们可以传给 `:class` (`v-bind:class` 的简写) 一个对象，以动态地切换 class。

```html
  <div id="app"></div>

  <template id="my-app">
    <!-- 1.普通的绑定方式 -->
    <div :class="className">{{message}}</div>
    <!-- 2.对象绑定 -->
    <!-- 动态切换class是否加入: {类(变量): boolean(true/false)} -->
    <div class="why" :class="{nba: true, 'james': true}"></div>
    <!-- 案例练习 -->
    <div :class="{'active': isActive}">哈哈哈</div>
    <button @click="toggle">切换</button>
    <!-- 绑定对象 -->
    <div :class="classObj">哈哈哈</div>
    <!-- 从methods中获取 -->
    <div :class="getClassObj()">呵呵呵</div>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          message: "Hello World",
          className: "why",
          nba: 'kobe',
          isActive: false,
          classObj: {
            why: true,
            kobe: true,
            james: false
          }
        }
      },
      methods: {
        toggle() {
          this.isActive = !this.isActive;
        },
        getClassObj() {
          return {
            why: true,
            kobe: true,
            james: false
          }
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
```

数组语法：

- 我们可以把一个数组传给 `:class`，以应用一个 class 列表；

```html
  <div id="app"></div>

  <template id="my-app">
    <div :class="['why', nba]">哈哈哈</div>
    <div :class="['why', nba, isActive? 'active': '']">呵呵呵</div>
    <div :class="['why', nba, {'actvie': isActive}]">嘻嘻嘻</div>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          message: "Hello World",
          nba: 'kobe',
          isActive: true
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
```

#### 2.2.3. 绑定style属性

对象语法：

- `:style` 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。
- CSS property 名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名

```html
  <div id="app"></div>

  <template id="my-app">
    <div :style="{color: 'red', fontSize: '30px', 'background-color': 'blue'}">{{message}}</div>
    <div :style="{color: 'red', fontSize:  size+'px', 'background-color': 'blue'}">{{message}}</div>
    <div :style="styleObj">{{message}}</div>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          message: "Hello World",
          size: 50,
          styleObj: {
            color: 'red', 
            fontSize: '50px', 
            'background-color': 'blue'
          } 
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
```

数组语法：

- `:style` 的数组语法可以将多个样式对象应用到同一个元素上；

```html
  <div id="app"></div>

  <template id="my-app">
    <div :style="[styleObj1, styleObj2]">{{message}}</div>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          message: "Hello World",
          size: 50,
          styleObj1: {
            color: 'red', 
            fontSize: '50px', 
            'background-color': 'blue'
          },
          styleObj2: {
            textDecoration: 'underline',
            fontWeight: 700
          } 
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
```

#### 2.2.4. 动态绑定属性

属性的名称和值都是动态的

```html
  <template id="my-app">
    <!-- 属性的名称是动态的 -->
    <div :[name]="value">{{message}}</div>
  </template>
```

#### 2.2.5. 绑定一个对象

- info对象会被拆解成div的各个属性；

```html
  <template id="my-app">
    <div v-bind="info">{{message}}</div>
  </template>
```

### 2.3. v-on

前面我们绑定了元素的内容和属性，在前端开发中另外一个非常重要的特性就是交互。

在前端开发中，我们需要经常和用户进行各种各样的交互：

- 这个时候，我们就必须监听用户发生的时间，比如点击、拖拽、键盘事件等等
- 在Vue中如何监听事件呢？使用v-on指令

v-on的使用：

- **缩写**：`@`

- **预期**：`Function | Inline Statement | Object`

- **参数**：`event`

- **修饰符**：

- - `.stop` - 调用 `event.stopPropagation()`。
  - `.prevent` - 调用 `event.preventDefault()`。
  - `.capture` - 添加事件侦听器时使用 capture 模式。
  - `.self` - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
  - `.{keyAlias}` - 仅当事件是从特定键触发时才触发回调。
  - `.once` - 只触发一次回调。
  - `.left` - 只当点击鼠标左键时触发。
  - `.right` - 只当点击鼠标右键时触发。
  - `.middle` - 只当点击鼠标中键时触发。
  - `.passive` - `{ passive: true }` 模式添加侦听器

- **用法**：绑定事件监听

案例演练：

```html
  <div id="app"></div>

  <template id="my-app">
    <div>{{message}}</div>
    <!-- 基本使用 -->
    <!-- 1.绑定函数 -->
    <button v-on:click="btnClick">按钮1</button>
    <button @click="btnClick">按钮2</button>
    <div v-on:mousemove="mouseMove">div的区域</div>

    <!-- 2.绑定对象 -->
    <button v-on="{click: btnClick, mousemove: mouseMove}">特殊按钮3</button>

    <!-- 3.内联语句 -->
    <!-- 默认会把event对象传入 -->
    <button @click="btn4Click">按钮4</button>
    <!-- 内联语句传入其他属性 -->
    <button @click="btn4Click($event, 'why')">按钮5</button>

    <!-- 4.修饰符 -->
    <div @click="divClick">
      <button @click.stop="btnClick">按钮6</button>
    </div>
    <input type="text" @keyup.enter="onEnter">

  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          message: "Hello World"
        }
      },
      methods: {
        btnClick() {
          console.log("按钮被点击了");
        },
        btn4Click(event) {
          console.log(event);
        },
        btn4Click(event, message) {
          console.log(event, message);
        },
        mouseMove() {
          console.log("鼠标移动");
        },
        divClick() {
          console.log("divClick");
        },
        onEnter(event) {
          console.log(event.target.value);
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
```

### 2.4. 条件渲染

在某些情况下，我们需要根据当前的条件决定某些元素或组件是否渲染，这个时候我们就需要进行条件判断了。

Vue提供了下面的指令来进行条件判断：

- v-if
- v-else
- v-else-if
- v-show

下面我们来对它们进行学习。

#### 2.4.1. v-if、v-else、v-else-if

v-if、v-else、v-else-if用于根据条件来渲染某一块的内容：

- 这些内容只有在条件为true时，才会被渲染出来；
- 这三个指令与JavaScript的条件语句if、else、else if类似；

```html
    <!-- vue3中, template不再要求必须只有一个根元素 -->
    <template id="my-app">
      <input type="text" v-model.number="score">
      <h2 v-if="score > 90">优秀</h2>
      <h2 v-else-if="score > 80">良好</h2>
      <h2 v-else-if="score > 60">普通</h2>
      <h2 v-else>不及格</h2>
    </template>
```

v-if的渲染原理：

- v-if是惰性的；
- 当条件为false时，其判断的内容完全不会被渲染或者会被销毁掉；
- 当条件为true时，才会真正渲染条件块中的内容；

#### 2.4.2. template元素

因为v-if是一个指令，所以必须将其添加到一个元素上：

- 但是如果我们希望切换的是多个元素呢？
- 此时我们渲染div，但是我们并不希望div这种元素被渲染；
- 这个时候，我们可以选择使用template；

template元素可以当做不可见的包裹元素，并且在v-if上使用，但是最终template不会被渲染出来：

- 有点类似于小程序中的block

```html
  <template id="my-app">
    <template v-if="showHa">
      <h2>哈哈哈哈</h2>
      <h2>哈哈哈哈</h2>
      <h2>哈哈哈哈</h2>
    </template>
    <template v-else>
      <h2>呵呵呵呵</h2>
      <h2>呵呵呵呵</h2>
      <h2>呵呵呵呵</h2>
    </template>
    <button @click="toggle">切换</button>
  </template>
```

#### 2.4.3. v-show

v-show和v-if的用法看起来是一致的：

```html
  <template id="my-app">
    <h2 v-show="isShow">哈哈哈哈</h2>
  </template>
```

#### 2.4.4. v-show和v-if区别

首先，在用法上的区别：

- v-show是不支持template；
- v-show不可以和v-else一起使用；

其次，本质的区别：

- v-show元素无论是否需要显示到浏览器上，它的DOM实际都是有渲染的，只是通过CSS的display属性来进行切换；
- v-if当条件为false时，其对应的原生压根不会被渲染到DOM中；

开发中如何进行选择呢？

- 如果我们的原生需要在显示和隐藏之间频繁的切换，那么使用v-show；
- 如果不会频繁的发生切换，那么使用v-if；

### 2.5. 列表渲染

在真实开发中，我们往往会从服务器拿到一组数据，并且需要对其进行渲染。

- 这个时候我们可以使用v-for来完成；
- v-for类似于JavaScript的for循环，可以用于遍历一组数据；

#### 1.5.1. v-for基本使用

v-for的基本格式是 `"item in 数组"`：

- 数组通常是来自data或者prop，也可以是其他方式；
- item是我们给每项元素起的一个别名，这个别名可以自定来定义；

```html
  <template id="my-app">
    <h2>电影列表</h2>
    <ul>
      <li v-for="item in movies">{{item}}</li>
    </ul>
  </template>
```

我们知道，在遍历一个数组的时候会经常需要拿到数组的索引：

- 如果我们需要索引，可以使用格式：`"(item, index) in 数组"`；
- 注意上面的顺序：数组元素项item是在前面的，索引项index是在后面的；

```html
  <template id="my-app">
    <h2>电影列表</h2>
    <ul>
      <li v-for="(item, index) in movies">{{index}}-{{item}}</li>
    </ul>
  </template>
```

#### 1.5.2. v-for支持类型

v-for也支持遍历对象，并且支持有一二三个参数：

- 一个参数：`"value in object"`;
- 二个参数：`"(value, key) in object"`;
- 三个参数：`"(value, key, index) in object"`;

```html
  <template id="my-app">
    <h2>遍历对象</h2>
    <ul>
      <li v-for="(value, key, index) in info">
        {{index}} - {{key}} - {{value}}
      </li>
    </ul>
  </template>
```

v-for同时也支持数字的遍历：

#### 1.5.3. template元素

类似于v-if，你可以使用 `template` 元素来循环渲染一段包含多个元素的内容：

- 我们使用template来对多个元素进行包裹，而不是使用div来完成；

```html
  <div id="app"></div>

  <template id="my-app">
    <ul>
      <template v-for="(value, key) in info">
        <li>{{key}}</li>
        <li>{{value}}</li>
        <hr>
      </template>
    </ul>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          info: {
            name: 'why',
            age: 18,
            height: 1.88
          }
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
```

#### 1.5.4. 数组更新检测

Vue 将被侦听的数组的变更方法进行了包裹，所以它们也将会触发视图更新。这些被包裹过的方法包括：

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

**替换数组的方法**

上面的方法会直接修改原来的数组，但是某些方法不会替换原来的数组，而是会生成新的数组，比如 `filter()`、`concat()` 和 `slice()`。

```js
const nums = [10, 21, 34, 6];
const newNums = nums.filter(num => num % 2 === 0);
console.log(newNums);
```

### 2.6. key和diff算法

#### 2.6.1. 认识VNode和VDOM

在使用v-for进行列表渲染时，我们通常会给元素或者组件绑定一个key属性。

这个key属性有什么作用呢？我们先来看一下官方的解释：

- key属性主要用在Vue的虚拟DOM算法，在新旧nodes对比时辨识VNodes；
- 如果不使用key，Vue会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法；
- 而使用key时，它会基于key的变化重新排列元素顺序，并且会移除/销毁key不存在的元素；

官方的解释对于初学者来说并不好理解，比如下面的问题：

- 什么是新旧nodes，什么是VNode？
- 没有key的时候，如何尝试修改和复用的？
- 有key的时候，如何基于key重新排列的？

我们先来解释一下VNode的概念：

- 因为目前我们还没有比较完整的学习组件的概念，所以目前我们先理解HTML元素创建出来的VNode；
- VNode的全称是Virtual Node，也就是虚拟节点；
- 事实上，无论是组件还是元素，它们最终在Vue中表示出来的都是一个个VNode；
- VNode的本质是一个JavaScript的对象；

```html
<div class="title" style="font-size: 30px; color: red;">哈哈哈</div>
```

在我们的Vue中会被转化创建出一个VNode对象：

```html
const vnode = {
  type: 'div',
  props: { 
    'class': 'title',
    style: {
      'font-size': '30px',
      color: 'red'
    }
  },
  children: '哈哈哈'
}
```

Vue内部在拿到vnode对象后，会对vnode进行处理，渲染成真实的DOM。

- 这一部分我会在后面专门和大家阅读createApp函数中讲到；

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)DOM渲染过程

如果我们不只是一个简单的div，而是有一大堆的元素，那么它们应该会形成一个VNode Tree：

```html
<div>
  <p>
    <i>哈哈哈哈</i>
    <i>哈哈哈哈</i>
  </p>
  <span>嘻嘻嘻嘻</span>
  <strong>呵呵呵呵</strong>
</div>
```

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BJoZw0zRtKIMQ6wx6meUUV0REzV0IKKXUSHvqD8BF259TCscUsib02Qg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

这个和我们的key有什么关系呢？

- 接下来我们就进行具体的分析；

#### 2.6.2. key作用和diff算法

我们先来看一个例子：

- 这个例子是当我点击按钮时会在中间插入一个f；

```html
  <div id="app"></div>

  <template id="my-app">
    <ul>
      <li v-for="item in letters">{{item}}</li>
    </ul>
    <button @click="insertF">insert f</button>
  </template>

  <script src="../js/vue.js"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          letters: ['a', 'b', 'c', 'd']
        }
      },
      methods: {
        insertF() {
          this.letters.splice(2, 0, 'f');
        }
      }
    }

    Vue.createApp(App).mount('#app');
  </script>
```

我们可以确定的是，这次更新对于ul和button是不需要进行更新，需要更新的是我们li的列表：

- 在Vue中，对于相同父元素的子元素节点并不会重新渲染整个列表；
- 因为对于列表中 a、b、c、d它们都是没有变化的；
- 在操作真实DOM的时候，我们只需要在中间插入一个f的li即可；

那么Vue中对于列表的更新究竟是如何操作的呢？

- Vue事实上会对于有key和没有key会调用两个不同的方法；
- 有key，那么就使用 `patchKeyedChildren`方法；
- 没有key，那么就使用 `patchUnkeyedChildren`方法；

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BcjbOJsI8s65F6rKFoc9NWYzCjEAY9MKicOF7Kd1oaaygUodm3l0UQsQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)有key和没有key的操作

#### 2.6.3. 没有key执行操作

没有key对应的源代码如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BHyeicqeNibAEnqR3gibA5XxRqibEFM084aytyZ8vxI1TNLZcbTkKOYh5yw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)patchUnkeyedChildren

它的过程画图就是如下的操作：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BZV7MDwf0e5E1SSmu2PZpSXoBGwvPo5m1hlhdwWAQc19wHEJ33ALxDw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)patchUnkeyedChildren画图

我们会发现上面的diff算法效率并不高：

- c和d来说它们事实上并不需要有任何的改动；
- 但是因为我们的c被f所使用了，所有后续所有的内容都要一次进行改动，并且最后进行新增；

#### 2.6.4. 有key执行操作

如果有key，那么会执行什么样的操作呢？

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BQl83peGiax7SYwl7hMU5vZib2J6qGM3kw2JhiabqOsCwbY72RUIGKQFwA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)patchKeyedChildren

第一步的操作是从头开始进行遍历、比较：

- a和b是一致的会继续进行比较；
- c和f因为key不一致，所以就会break跳出循环；

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0B97JgSjS8Ulbt9OfFTXiabuS1TQtJUCLdQT25NWia92VykibIjAaNNJYKg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)第一步对比的过程

第二步的操作是从尾部开始进行遍历、比较：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0Bqz4dlrcI8O05WL8eyJCT7uNeL6LMM95U8FjJQcZfJCOHGw5OFata3w/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)第二步对比过程

第三步是如果旧节点遍历完毕，但是依然有新的节点，那么就新增节点：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0Bk1jtwiaycrWnnAwnjGgoZEbjiboKxxTd9g3bA5PSZU67CziaqjkzZS8dQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)新增节点

第四步是如果新的节点遍历完毕，但是依然有旧的节点，那么就移除旧节点：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BISGgcIRvWPUu41ia5VF5kYUfIlOCy7NKkicGmohAV6Brn2FgAicP71CkA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)移除旧节点

第五步是最特色的情况，中间还有很多未知的或者乱序的节点：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/O8xWXzAqXuuF8t6OdhSGibqh6ibTTSfl0BGWAic3PoxrfibU335aEmbQiaDuUgwB5thyEYuVNPwwM7ZnQJAg1l9ufmQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)未知序列操作

所以我们可以发现，Vue在进行diff算法的时候，会尽量利用我们的key来进行优化操作：

- 在没有key的时候我们的效率是非常低效的；
- 在进行插入或者重置顺序的时候，保持相同的key可以让diff算法更加的高效；

### 2.7.计算属性computed

什么是计算属性呢？

- 官方并没有给出直接的概念解释；
- 而是说：对于任何包含响应式数据的复杂逻辑，你都应该使用计算属性；
- 计算属性将被混入到组件实例中。所有 getter 和 setter 的 this 上下文自动地绑定为组件实例；

计算属性 vs methods

- 计算属性和methods的实现看起来是差别是不大的，而且我们多次提到计算属性有缓存的。

- 接下来我们来看一下同一个计算多次使用，计算属性和methods的差异

  ![image-20220109153127460](https://s2.loli.net/2022/01/09/fJF19rtgeAYjqLl.png)

计算属性的缓存

- 这是因为计算属性会基于它们的依赖关系进行缓存；
- 在数据不发生变化时，计算属性是不需要重新计算的；
- 但是如果依赖的数据发生变化，在使用时，计算属性依然会重新进行计算；

计算属性的setter和getter

- 计算属性在大多数情况下，只需要一个getter方法即可，所以我们会将计算属性直接写成一个函数。

- 但是，如果我们确实想设置计算属性的值呢？

  - 这个时候我们也可以给计算属性设置一个setter的方法；

    ![image-20220109153258836](https://s2.loli.net/2022/01/09/NSQwHLqKeCWtahy.png)

### 2.8 侦听器watch

什么是侦听器呢？

- 开发中我们在data返回的对象中定义了数据，这个数据通过插值语法等方式绑定到template中；
- 当数据变化时，template会自动进行更新来显示最新的数据；
- 但是在某些情况下，我们希望在代码逻辑中监听某个数据的变化，这个时候就需要用侦听器watch来完成了；

侦听器watch的配置选项

- deep 进行更深层的侦听；
- immediate 希望一开始的就会立即执行一次

```js
      data() {
        return {
          info: {
            name: "lyc",
            age: 18
          }
        }
      },
      watch: {
        // 默认情况下我们侦听器只会正针对监听数据本身的改变（内部发生的改变是不能监听的）
        // info(newInfo, oldInfo) {
        //   console.log(newInfo, oldInfo);
        // }

        // 深度监听/立即执行（一定会执行一次）
        info: {
          handler: function (newInfo, oldInfo) {
            console.log(newInfo, oldInfo);
          },
          deep: true, //深度侦听
          immediate: true //立即执行
        },

        "info.name"(newInfo, oldInfo) {
          console.log(newInfo, oldInfo, "第二次");
        }
      },
```

另外一种方式就是使用 $watch 的API：

```js
created() {
        this.$watch("info", function (newInfo, oldInfo) {
          console.log(newInfo, oldInfo,"created"), {
            deep: true,
            immediate: true
          }
        })
      },
```

还可以传入回调数组：

![image-20220110161025428](https://s2.loli.net/2022/01/10/j6DsBlNkVGn3OXe.png)

### 2.9 v-model的基本使用

在代码逻辑中获取到用户提交的数据，我们通常会使用v-model指令来完成：

- v-model指令可以在表单 input、textarea以及select元素上创建双向数据绑定；
- 它会根据控件类型自动选取正确的方法来更新元素；
- 尽管有些神奇，但 v-model 本质上不过是语法糖，它负责监听用户的输入事件来更新数据，并在某种极端场景下进行一些特殊处理；

v-model的原理

- v-bind绑定value属性的值；
- v-on绑定input事件监听到函数中，函数会获取最新的值赋值到绑定的属性中

![image-20220111174902893](https://s2.loli.net/2022/01/11/NvPVDYoq8xTJcSG.png)

v-model实例

```html
<body>
  <div id="app"></div>
  <template id="my-app">
    <div>
      <!-- 1.单选框 -->
      <label for="agree">
        <input type="checkbox" id="agree" value="agree" v-model="isAgree">同意协议
      </label>
      <h2>{{isAgree}}</h2>

      <!-- 2.多选框 -->
      <span>你的爱好：</span>
      <label for="basketball">
        <input type="checkbox" id="basketball" value="basketball" v-model="hobbies">篮球
      </label>
      <label for="football">
        <input type="checkbox" id="football" value="football" v-model="hobbies">篮球
      </label>
      <label for="tennis">
        <input type="checkbox" id="tennis" value="tennis" v-model="hobbies">篮球
      </label>
      <h2>{{hobbies}}</h2>

      <!-- 3.radio -->
      <span>你的性别：</span>
      <label for="male">
        <input type="radio" id="male" v-model="gender" value="male">男
      </label>
      <label for="female">
        <input type="radio" id="female" v-model="gender" value="female">女
      </label>
      <h2>{{gender}}</h2>
    </div>

    <!-- 4.select -->
    <span>喜欢的水果：</span>
    <select v-model="fruit" multiple>
      <option value="apple">苹果</option>
      <option value="orange">橘子</option>
      <option value="banana">香蕉</option>
    </select>
    <h2>{{fruit}}</h2>
  </template>

  <script src="https://unpkg.com/vue@next"></script>
  <script>
    const App = {
      template: '#my-app',
      data() {
        return {
          isAgree: false,
          hobbies: [],
          gender: "",
          fruit: ""
        }
      },
    }
    Vue.createApp(App).mount("#app")
  </script>
</body>
```

v-model修饰符

- lazy 如果我们在v-model后跟上lazy修饰符，那么会将绑定的事件切换为 change 事件，只有在提交时（比如回车）才会触发；
- number 如果我们希望转换为数字类型，那么可以使用 .number 修饰符;
- trim 如果要自动过滤用户输入的守卫空白字符，可以给v-model添加 trim 修饰符;

# 二、Webpack

**webpack是一个静态的模块化打包工具，为现代的JavaScript应用程序；**

- 打包bundler：webpack可以将帮助我们进行打包，所以它是一个打包工具
- 静态的static：这样表述的原因是我们最终可以将代码打包成最终的静态资源（部署到静态服务器）；
- 模块化module：webpack默认支持各种模块化开发，ES Module、CommonJS、AMD等；
- 现代的modern：我们前端说过，正是因为现代前端开发面临各种各样的问题，才催生了webpack的出现和发展；

随着前端的快速发展，目前前端的开发已经变的越来越复杂了：

- 比如开发过程中我们需要通过模块化的方式来开发；
- 比如也会使用一些高级的特性来加快我们的开发效率或者安全性，比如通过ES6+、TypeScript开发脚本逻辑，通过sass、less等方式来编写css样式代码；
- 比如开发过程中，我们还希望实时的监听文件的变化来并且反映到浏览器上，提高开发的效率；
- 比如开发完成后我们还需要将代码进行压缩、合并以及其他相关的优化；
- 等等….

Vue项目加载的文件有哪些呢？

-  JavaScript的打包：
  -  将ES6转换成ES5的语法；
  -  TypeScript的处理，将其转换成JavaScript；
-  Css的处理：
  - CSS文件模块的加载、提取；
  -  Less、Sass等预处理器的处理；
-  资源文件img、font：
  - 图片img文件的加载；
  -  字体font文件的加载； 
-  HTML资源的处理：
  - 打包HTML资源文件；
- 处理vue项目的SFC文件.vue文件；

## Webpack的安装

webpack的安装目前分为两个：webpack、webpack-cli

-  执行webpack命令，会执行node_modules下的.bin目录下的webpack；
-  webpack在执行时是依赖webpack-cli的，如果没有安装就会报错；
-  而webpack-cli中代码执行时，才是真正利用webpack进行编译和打包的过程；
-  所以在安装webpack时，我们需要同时安装webpack-cli（第三方的脚手架事实上是没有使用webpack-cli的，而是类似于自己的vue-service-cli的东西）

### 创建局部的webpack

-  第一步：创建package.json文件，用于管理项目的信息、库依赖等

  ```
  npm init
  ```

-  第二步：安装局部的webpack

  ```
  npm install webpack webpack-cli -D
  ```

-  第三步：使用局部的webpack

  ```
  npx webpack
  ```

-  第四步：在package.json中创建scripts脚本，执行脚本打包即可

  ```json
    "scripts": {
      "build": "webpack"
    },
  ```

  ```
  npm run build
  ```

  

### Webpack配置文件

我们可以在根目录下创建一个webpack.config.js文件，来作为webpack的配置文件：

![image-20220113154840185](https://s2.loli.net/2022/01/13/kSt45UL6JNqg9ZT.png)

### Webpack的依赖图

-  事实上webpack在处理应用程序时，它会根据命令或者配置文件找到入口文件；
-  从入口开始，会生成一个 依赖关系图，这个依赖关系图会包含应用程序中所需的所有模块（比如.js文件、css文件、图片、字体等）；
-  然后遍历图结构，打包一个个模块（根据文件的不同使用不同的loader来解析）；

![image-20220113154105309](https://s2.loli.net/2022/01/13/Myqi5Lnj61CDQIS.png)

## Loader的使用

-  上面的错误信息告诉我们需要一个loader来加载这个css文件，但是loader是什么呢？

  - loader 可以用于对模块的源代码进行转换；
  - 我们可以将css文件也看成是一个模块，我们是通过import来加载这个模块的；
  - 在加载这个模块时，webpack其实并不知道如何对其进行加载，我们必须制定对应的loader来完成这个功能；

-  那么我们需要一个什么样的loader呢？

  - 对于加载css文件来说，我们需要一个可以读取css文件的loader；
  - 这个loader最常用的是css-loader；

-  css-loader的安装：

  ```
  npm install css-loader -D
  ```

### loader配置方式

- 配置方式表示的意思是在我们的webpack.config.js文件中写明配置信息：
  - module.rules中允许我们配置多个loader（因为我们也会继续使用其他的loader，来完成其他文件的加载）；
  - 这种方式可以更好的表示loader的配置，也方便后期的维护，同时也让你对各个Loader有一个全局的概览；
-  module.rules的配置如下：
-  rules属性对应的值是一个数组：[Rule]
-  数组中存放的是一个个的Rule，Rule是一个对象，对象中可以设置多个属性：
  - test属性：用于对 resource（资源）进行匹配的，通常会设置成正则表达式；
  -  use属性：对应的值时一个数组：[UseEntry]
    - UseEntry是一个对象，可以通过对象的属性来设置一些其他属性
      - loader：必须有一个 loader属性，对应的值是一个字符串；
      -  options：可选的属性，值是一个字符串或者对象，值会被传入到loader中；
      -  query：目前已经使用options来替代；
    -  传递字符串（如：use: [ 'style-loader' ]）是 loader 属性的简写方式（如：use: [ { loader: 'style-loader'} ]）；
  -  loader属性： Rule.use: [ { loader } ] 的简写。

webpack.config.js

```js
const path = require('path');

module.exports = {
  entry: "./src/main.js",
  output: {
    path: path.resolve(__dirname, "./build"),
    filename: "bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.css$/, //正则表达式
        // 1.loader的写法(语法糖)
        // loader: "css-loader"

        // 2.完整的写法
        use: [
          // {loader: "css-loader"}
          "style-loader",
          "css-loader",
          "postcss-loader"
          // {
          //   loader: "postcss-loader",
          //   options: {
          //     postcssOptions: {
          //       plugins: [
          //         require("autoprefixer")
          //       ]
          //     }
          //   }
          // }
        ]
      },
      {
        test: /\.less$/,
        use: [
          "style-loader",
          "css-loader",
          "less-loader"
        ]
      },
      // {
      //   test: /\.(less|css)$/,
      //   use: [
      //     "style-loader",
      //     "css-loader",
      //     "less-loader"
      //   ]
      // }
    ]
  }
}
```

### 配置style-loader

css-loader只是负责将.css文件进行解析，并不会将解析之后的css插入到页面中,如果我们希望再完成插入style的操作，那么我们还需要另外一个loader，就是style-loader；

```
npm install style-loader -D
```

因为loader的执行顺序是从右向左（或者说从下到上，或者说从后到前的），所以我们需要将styleloader写到css-loader的前面；

![image-20220113155025542](https://s2.loli.net/2022/01/13/8uqm3iDtkJGAOL2.png)

### 认识PostCSS工具

- 什么是PostCSS呢？
  - PostCSS是一个通过JavaScript来转换样式的工具；
  - 这个工具可以帮助我们进行一些CSS的转换和适配，比如自动添加浏览器前缀、css样式的重置；
  - 但是实现这些功能，我们需要借助于PostCSS对应的插件；
-  如何使用PostCSS呢？主要就是两个步骤：
  - 第一步：查找PostCSS在构建工具中的扩展，比如webpack中的postcss-loader；
  - 第二步：选择可以添加你需要的PostCSS相关的插件；

安装：postcss、postcss-cli

```
npm install postcss postcss-cli -D
```

插件autoprefixer

-  因为我们需要添加前缀，所以要安装autoprefixer：

  ```
  npm install autoprefixer -D
  ```

-  直接使用使用postcss工具，并且制定使用autoprefixer

  ```
  npx postcss --use autoprefixer -o end.css ./src/css/style.css
  ```

-  转化之后的css样式如下：

  ![image-20220113155536132](https://s2.loli.net/2022/01/13/8JnmETeYydfvBbx.png)

#### postcss配置文件

我们可以将这些配置信息放到一个单独的文件中进行管理：

postcss.config.js

```js
module.exports = {
  plugins: [
    require("postcss-preset-env")
  ]
}
```

### 文件的命名规则

- 有时候我们处理后的文件名称按照一定的规则进行显示：
  - 比如保留原来的文件名、扩展名，同时为了防止重复，包含一个hash值等； 
-  这个时候我们可以使用PlaceHolders来完成，webpack给我们提供了大量的PlaceHolders来显示不同的内容：
  - https://webpack.js.org/loaders/file-loader/#placeholders
  -  我们可以在文档中查阅自己需要的placeholder；
-  我们这里介绍几个最常用的placeholder：
  - [ext]： 处理文件的扩展名；
  -  [name]：处理文件的名称；
  -  [hash]：文件的内容，使用MD4的散列函数处理，生成的一个128位的hash值（32个十六进制）；
  -  [contentHash]：在file-loader中和[hash]结果是一致的（在webpack的一些其他地方不一样，后面会讲到）；
  -  [hash:<length>]：截图hash的长度，默认32个字符太长了；
  -  [path]：文件相对于webpack配置文件的路径；

## 加载静态文件

### file-loader

- 要处理jpg、png等格式的图片，我们也需要有对应的loader：file-loader
  - file-loader的作用就是帮助我们处理import/require()方式引入的一个文件资源，并且会将它放到我们输出的文件夹中；
  - 当然我们待会儿可以学习如何修改它的名字和所在文件夹；

- 安装file-loader：

-  配置处理图片的Rule：

  ```js
        {
          test: /\.(jpe?g|png|gif|svg)$/,
          use: {
            loader: "file-loader",
            options: {
              // outputPath: "img",
              name: "img/[name]_[hash:6].[ext]",
              limit: 100 * 1024
            }
          }
        },
  ```

  ### url-loader

  - url-loader和file-loader的工作方式是相似的，但是可以将较小的文件，转成base64的URI。

  -  安装url-loader：

    ```
    npm install url-loader -D
    ```

    ```js
          {
            test: /\.(jpe?g|png|gif|svg)$/,
            use: {
              loader: "file-loader",
              options: {
                // outputPath: "img",
                name: "img/[name]_[hash:6].[ext]",
                limit: 100 * 1024	//限制大小 100kb
              }
            }
          },
    ```

  ### 资源模块类型(asset module type)

  资源模块类型(asset module type)，通过添加 4 种新的模块类型，来替换所有这些 loader：

  - asset/resource 发送一个单独的文件并导出 URL。之前通过使用 file-loader 实现；
  - asset/inline 导出一个资源的 data URI。之前通过使用 url-loader 实现；
  - asset/source 导出资源的源代码。之前通过使用 raw-loader 实现；
  - asset 在导出一个 data URI 和发送一个单独的文件之间自动选择。之前通过使用 url-loader，并且配置资源体积限制实现；

```js
      {
        test: /\.(jpe?g|png|gif|svg)$/,
        type: "asset",
        generator: {
          filename: "img/[name]_[hash:6][ext]",	//输出路径和文件名
        },
        parser: {
          dataUrlCondition: {
            maxSize: 10 * 1024,	//大小限制
          },
        },
      },
```

### 加载字体文件

使用file-loader来处理，也可以选择直接使用webpack5的资源模块类型来处理；

```js
      {
        test: /\.(eot|ttf|woff2?)$/,
        type: "asset/resource",
        generator: {
          filename: "font/[name]_[hash:6][ext]",
        },
      },
```

## Plugin插件

- Loader是用于特定的模块类型进行转换；
- Plugin可以用于执行更加广泛的任务，比如打包优化、资源管理、环境变量注入等；

### 1. CleanWebpackPlugin

自动删除dist文件夹

```
npm install clean-webpack-plugin -D
```

### 2.HtmlWebpackPlugin

- 我们的HTML文件是编写在根目录下的，而最终打包的dist文件夹中是没有index.html文件的。
- 在进行项目部署的时，必然也是需要有对应的入口文件index.html；
- 所以我们也需要对index.html进行打包处理；

```
npm install html-webpack-plugin -D
```

#### 自定义HTML模板

**如果我们想在自己的模块中加入一些比较特别的内容：**

- 比如添加一个noscript标签，在用户的JavaScript被关闭时，给予响应的提示；
- 比如在开发vue或者react项目时，我们需要一个可以挂载后续组件的根标签 <div id="app"></div>；

![image-20220115151421138](https://s2.loli.net/2022/01/15/pitgZN7W1cFHLks.png)

**在配置HtmlWebpackPlugin时，我们可以添加如下配置：**

- ptemplate：指定我们要使用的模块所在的路径；
- ptitle：在进行htmlWebpackPlugin.options.title读取时，就会读到该信息；

### 3.DefinePlugin

-  这是因为在编译template模块时，有一个BASE_URL：

  ```
  <link rel="icon" href="<%= BASE_URL %>favicon.ico">；
  ```

  但是我们并没有设置过这个常量值，所以会出现没有定义的错误；

-  这个时候我们可以使用DefinePlugin插件；

-  DefinePlugin允许在编译时创建配置的全局常量，是一个webpack内置的插件（不需要单独安装）：

### 4.CopyWebpackPlugin

- 在vue的打包过程中，如果我们将一些文件放到public的目录下，那么这个目录会被复制到dist文件夹中。
  - 这个复制的功能，我们可以使用CopyWebpackPlugin来完成；
-  安装CopyWebpackPlugin插件：
-  接下来配置CopyWebpackPlugin即可：
  - 复制的规则在patterns中设置；
  - from：设置从哪一个源中开始复制；
  - to：复制到的位置，可以省略，会默认复制到打包的目录下；
  - globOptions：设置一些额外的选项，其中可以编写需要忽略的文件：
    - DS_Store：mac目录下回自动生成的一个文件；
    -  index.html：也不需要复制，因为我们已经通过HtmlWebpackPlugin完成了index.html的生成；

```js
const path = require("path");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { DefinePlugin } = require("webpack");
const CopyWebpackPlugin = require('copy-webpack-plugin'); 
plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
      template: "./public/index.html",
      title: "哈哈哈哈"
    }),
    new DefinePlugin({
      BASE_URL: "'./'"
    }),
    new CopyWebpackPlugin({ 
      patterns: [
        {
          from: "public",
          to: "./",
          globOptions: {
            ignore: [
              "**/index.html"
            ]
          }
        }
      ]
    })
  ],
```

## Mode配置

Mode配置选项，可以告知webpack使用响应模式的内置优化：

- 默认值是production（什么都不设置的情况下）；
- 可选值有：'none' | 'development' | 'production'；

```
  // 设置模式
  // development 开发阶段, 会设置development
  // production 准备打包上线的时候, 设置production
  mode: "development",
  // 设置source-map, 建立js映射文件, 方便调试代码和错误
  devtool: "source-map",
  
  entry: "./src/main.js",
```

## Babel工具链

- Babel是一个工具链，主要用于旧浏览器或者环境中将ECMAScript 2015+代码转换为向后兼容版本的JavaScript；
- 包括：语法转换、源代码转换等；

### Babel命令行使用

-  babel本身可以作为一个独立的工具（和postcss一样），不和webpack等构建工具配置来单独使用。

-  如果我们希望在命令行尝试使用babel，需要安装如下库：

  - @babel/core：babel的核心代码，必须安装；

  - @babel/cli：可以让我们在命令行使用babel；

    ```
    npm install @babel/cli @babel/core -D
    ```

-  使用babel来处理我们的源代码：
  psrc：是源文件的目录；
  p--out-dir：指定要输出的文件夹dist；

  ```
  npx babel src --out-dir dist

### 插件的使用

-  比如我们需要转换箭头函数，那么我们就可以使用箭头函数转换相关的插件：

  ```
  npm install @babel/plugin-transform-arrow-functions -D
  npx babel src --out-dir dist --plugins=@babel/plugin-transform-arrow-functions
  ```

-  查看转换后的结果：我们会发现 const 并没有转成 var

  - 这是因为 plugin-transform-arrow-functions，并没有提供这样的功能；

  - 我们需要使用 plugin-transform-block-scoping 来完成这样的功能；

    ```
    npm install @babel/plugin-transform-block-scoping -D 
    npx babel src --out-dir dist --plugins=@babel/plugin-transform-block-scoping,@babel/plugin-transform-arrow-functions
    ```

### Babel的预设preset

-  但是如果要转换的内容过多，一个个设置是比较麻烦的，我们可以使用预设（preset）：

  - 后面我们再具体来讲预设代表的含义；

-  安装@babel/preset-env预设：

  ```
  npm install @babel/preset-env -D
  ```

- 执行如下命令：

  ```
  npx babel src --out-dir dist --presets=@babel/preset-env
  ```

### Babel的底层原理

-  babel是如何做到将我们的一段代码（ES6、TypeScript、React）转成另外一段代码（ES5）的呢？
  - 从一种源代码（原生语言）转换成另一种源代码（目标语言），这是什么的工作呢？
  - 就是编译器，事实上我们可以将babel看成就是一个编译器。
  - Babel编译器的作用就是将我们的源代码，转换成浏览器可以直接识别的另外一段源代码；
-  Babel也拥有编译器的工作流程：
  - 解析阶段（Parsing）
  - 转换阶段（Transformation）
  -  生成阶段（Code Generation）

![image-20220117211716530](https://s2.loli.net/2022/01/17/Hl6yxLjEWKJI5sD.png)

### babel-loader

- 在实际开发中，我们通常会在构建工具中通过配置babel来对其进行使用的，比如在webpack中。

-  那么我们就需要去安装相关的依赖：

  - 如果之前已经安装了@babel/core，那么这里不需要再次安装；

    ```
    npm install babel-loader @babel/core
    ```

- 我们可以设置一个规则，在加载js文件时，使用我们的babel：

  ```js
        {
          test: /\.js$/,
          use: {
            loader: "babel-loader",
            options: {	//插件
              // plugins: [
              //   "@babel/plugin-transform-arrow-functions",
              //   "@babel/plugin-transform-block-scoping",
              // ]
              presets: [	//预设
                "@babel/preset-env"
              ]
            }
          }
        }
  ```

### Babel的配置文件

我们可以将babel的配置信息放到一个独立的文件中，babel给我们提供了两种配置文件的编写：

- babel.config.json（或者.js，.cjs，.mjs）文件；
- babelrc.json（或者.babelrc，.js，.cjs，.mjs）文件；

```js
module.exports = {
  presets: [
    "@babel/preset-env"
  ]
}
```

## Vue的打包

### Vue打包后不同版本解析

-  vue(.runtime).global(.prod).js：
  - 通过浏览器中的 <script src="..."> 直接使用；
  -  我们之前通过CDN引入和下载的Vue版本就是这个版本；
  -  会暴露一个全局的Vue来使用；
-  vue(.runtime).esm-browser(.prod).js：
  - 用于通过原生 ES 模块导入使用 (在浏览器中通过 <script type="module"> 来使用)。
-  vue(.runtime).esm-bundler.js：
  - 用于 webpack，rollup 和 parcel 等构建工具；
  -  构建工具中默认是vue.runtime.esm-bundler.js；
  -  如果我们需要解析模板template，那么需要手动指定vue.esm-bundler.js；
-  vue.cjs(.prod).js：
  - 服务器端渲染使用；
  - 通过require()在Node.js中使用；

### 运行时+编译器 vs 仅运行时

- 在Vue的开发过程中我们有三种方式来编写DOM元素：
  - 方式一：template模板的方式（之前经常使用的方式）；
  -  方式二：render函数的方式，使用h函数来编写渲染的内容；
  -  方式三：通过.vue文件中的template来编写模板；
-  它们的模板分别是如何处理的呢？
  - 方式二中的h函数可以直接返回一个虚拟节点，也就是Vnode节点；
  -  方式一和方式三的template都需要有特定的代码来对其进行解析：
    - 方式三.vue文件中的template可以通过在vue-loader对其进行编译和处理；
    -  方式一种的template我们必须要通过源码中一部分代码来进行编译；
-  所以，Vue在让我们选择版本的时候分为 运行时+编译器 vs 仅运行时
  - 运行时+编译器包含了对template模板的编译代码，更加完整，但是也更大一些；
  -  仅运行时没有包含对template版本的编译代码，相对更小一些；

### App.vue的打包过程

使用vue-loader：

```
npm install vue-loader -D
```

在webpack的模板规则中进行配置：

```js
      {
        test: /\.vue$/,
        loader: "vue-loader"
      }
```

#### @vue/compiler-sfc

- 打包依然会报错，这是因为我们必须添加@vue/compiler-sfc来对template进行解析：

  ```
  npm install @vue/compiler-sfc -D
  ```

-  另外我们需要配置对应的Vue插件：

  ```
  new VueLoaderPlugin()
  ```

-  重新打包即可支持App.vue的写法

-  另外，我们也可以编写其他的.vue文件来编写自己的组件；

## 本地服务器

当文件发生变化时，可以自动的完成 编译 和 展示；

为了完成自动编译，webpack提供了几种可选的方式：

- webpack watch mode；
- webpack-dev-server（常用）；
- webpack-dev-middleware；

### Webpack watch

可以监听到文件的变化，但是事实上它本身是没有自动刷新浏览器的功能的

- webpack给我们提供了watch模式：
  - 在该模式下，webpack依赖图中的所有文件，只要有一个发生了更新，那么代码将被重新编译；
  - 我们不需要手动去运行 npm run build指令了；

-  如何开启watch呢？两种方式：
  - 方式一：在导出的配置中，添加 watch: true；
  - 方式二：在启动webpack的命令中，添加 --watch的标识；

### webpack-dev-server

可以具备live reloading（实时重新加载）的功能

- 安装webpack-dev-server

  ```
  npm install webpack-dev-server -D
  ```

- 修改配置文件，告知 dev server，从什么位置查找文件：

  ![image-20220120162928583](https://s2.loli.net/2022/01/20/CQZDOLRMJo9HrwK.png)

- webpack-dev-server 在编译之后不会写入到任何输出文件。而是将 bundle 文件保留在内存中：

  - 事实上webpack-dev-server使用了一个库叫memfs（memory-fs webpack自己写的）

## 模块热替换（HMR）

-  什么是HMR呢？
  - HMR的全称是Hot Module Replacement，翻译为模块热替换；
  - 模块热替换是指在 应用程序运行过程中，替换、添加、删除模块，而无需重新刷新整个页面；
-  HMR通过如下几种方式，来提高开发的速度：
  - 不重新加载整个页面，这样可以保留某些应用程序的状态不丢失；
  - 只更新需要变化的内容，节省开发的时间；
  - 修改了css、js源代码，会立即在浏览器更新，相当于直接在浏览器的devtools中直接修改样式；
-  如何使用HMR呢？
  - 默认情况下，webpack-dev-server已经支持HMR，我们只需要开启即可；
  - 在不开启HMR的情况下，当我们修改了源代码之后，整个页面会自动刷新，使用的是live reloading；

### 开启HMR

- 修改webpack的配置：![image-20220120163357206](C:/Users/Roy_Dust/AppData/Roaming/Typora/typora-user-images/image-20220120163357206.png)

- 浏览器可以看到如下效果：![image-20220120163418993](https://s2.loli.net/2022/01/20/xwIWmHyqCBlsOgD.png)

- 但是你会发现，当我们修改 了某一个模块的代码时，依然是刷新的整个页面：

  ```js
  if(module.hot){
    module.hot.accept("./js/element.js",()=>{
      console.log("element模块发生更新了");
    })
  }
  ```

- 这是因为我们需要去指定哪些模块发生更新时，进行HMR；

### HMR的原理

- 那么HMR的原理是什么呢？如何可以做到只更新一个模块中的内容呢？
  - webpack-dev-server会创建两个服务：提供静态资源的服务（express）和Socket服务（net.Socket）；
  - express server负责直接提供静态资源的服务（打包后的资源直接被浏览器请求和解析）；
-  HMR Socket Server，是一个socket的长连接：
  - 长连接有一个最好的好处是建立连接后双方可以通信（服务器可以直接发送文件到客户端）；
  - 当服务器监听到对应的模块发生变化时，会生成两个文件.json（manifest文件）和.js文件（update chunk）；
  - 通过长连接，可以直接将这两个文件主动发送给客户端（浏览器）；
  - 浏览器拿到两个新的文件后，通过HMR runtime机制，加载这两个文件，并且针对修改的模块进行更新；

![image-20220120163546911](https://s2.loli.net/2022/01/20/1LEBZ5z8JWVdFDR.png)

## hotOnly、host配置

- host设置主机地址
  - 如果希望其他地方也可以访问，可以设置为 0.0.0.0；
- localhost 和 0.0.0.0 的区别：
  - localhost：本质上是一个域名，通常情况下会被解析成127.0.0.1;
  - 127.0.0.1：回环地址(Loop Back Address)，表达的意思其实是我们主机自己发出去的包，直接被自己接收;
    - 正常的数据库包经常 应用层 - 传输层 - 网络层 - 数据链路层 - 物理层 ;
    -  而回环地址，是在网络层直接就被获取到了，是不会经常数据链路层和物理层的;
    -  比如我们监听 127.0.0.1时，在同一个网段下的主机中，通过ip地址是不能访问的;
  - 0.0.0.0：监听IPV4上所有的地址，再根据端口找到不同的应用程序;
    - 比如我们监听 0.0.0.0时，在同一个网段下的主机中，通过ip地址是可以访问的; 

## port、open、compress配置

- port设置监听的端口，默认情况下是8080
  - open是否打开浏览器：
- 默认值是false，设置为true会打开浏览器；
  - 也可以设置为类似于 Google Chrome等值；
- compress是否为静态文件开启gzip compression：
  - 默认值是false，可以设置为true；

## Proxy配置（设置代理来解决跨域访问）

- proxy是我们开发中非常常用的一个配置选项，它的目的设置代理来解决跨域访问的问题：

  - 比如我们的一个api请求是 http://localhost:8888，但是本地启动服务器的域名是 http://localhost:8000，这个时候发送网络请求就会出现跨域的问题；

  - 那么我们可以将请求先发送到一个代理服务器，代理服务器和API服务器没有跨域的问题，就可以解决我们的跨域问题了；

- 我们可以进行如下的设置：

  - target：表示的是代理到的目标地址，比如 /api-hy/moment会被代理到 http://localhost:8888/apihy/moment；
  - pathRewrite：默认情况下，我们的 /api-hy 也会被写入到URL中，如果希望删除，可以使用pathRewrite；
  - secure：默认情况下不接收转发到https的服务器上，如果希望支持，可以设置为false；
  - changeOrigin：它表示是否更新代理后请求的headers中host地址；

## changeOrigin的解析

- 这个 changeOrigin官方说的非常模糊，通过查看源码我发现其实是要修改代理请求中的headers中的host属性(就是更改使用原来的请求头)：
  - 因为我们真实的请求，其实是需要通过 http://localhost:8888来请求的；
  - 但是因为使用了代码，默认情况下它的值时 http://localhost:8000；
  - 如果我们需要修改，那么可以将changeOrigin设置为true即可；

## historyApiFallback配置

- historyApiFallback是开发中一个非常常见的属性，它主要的作用是解决SPA页面在路由跳转之后，进行页面刷新时，返回404的错误。
-  boolean值：默认是false
  - 如果设置为true，那么在刷新时，返回404错误时，会自动返回 index.html 的内容；
-  object类型的值，可以配置rewrites属性：
  - 可以配置from来匹配路径，决定要跳转到哪一个页面；
-  事实上devServer中实现historyApiFallback功能是通过connect-history-api-fallback库的：
  - 可以查看connect-history-api-fallback 文档

## resolve模块解析

- resolve用于设置模块如何被解析：
  - 在开发中我们会有各种各样的模块依赖，这些模块可能来自于自己编写的代码，也可能来 自第三方库；
  -  resolve可以帮助webpack从每个 require/import 语句中，找到需要引入到合适的模块代码；
  -  webpack 使用 enhanced-resolve 来解析文件路径；
-  webpack能解析三种文件路径：
-  绝对路径
  - 由于已经获得文件的绝对路径，因此不需要再做进一步解析。
-  相对路径
  - 在这种情况下，使用 import 或 require 的资源文件所处的目录，被认为是上下文目录；
  -  在 import/require 中给定的相对路径，会拼接此上下文路径，来生成模块的绝对路径；
-  模块路径
  - 在 resolve.modules中指定的所有目录检索模块；
    - 默认值是 ['node_modules']，所以默认会从node_modules中查找文件； 
  -  我们可以通过设置别名的方式来替换初识模块路径，具体后面讲解alias的配置；

### resolve怎么确实文件还是文件夹

- 如果是一个文件：
  - 如果文件具有扩展名，则直接打包文件；
  - 否则，将使用 resolve.extensions选项作为文件扩展名解析；
-  如果是一个文件夹：
  - 会在文件夹中根据 resolve.mainFiles配置选项中指定的文件顺序查找；
    - resolve.mainFiles的默认值是 ['index']；
    -  再根据 resolve.extensions来解析扩展名；

### extensions和alias配置

- extensions是解析到文件时自动添加扩展名：
  - 默认值是 ['.wasm', '.mjs', '.js', '.json']；
  - 所以如果我们代码中想要添加加载 .vue 或者 jsx 或者 ts 等文件时，我们必须自己写上扩展名；
-  另一个非常好用的功能是配置别名alias：
  - 特别是当我们项目的目录结构比较深的时候，或者一个文件的路径可能需要 ../../../这种路径片段；
  - 我们可以给某些常见的路径起一个别名；

```js
  resolve:{
    extensions:[".js",".mjs",".json",".jsx",".ts",".vue"],
    alias:{
      "@": resolveApp('./src'),
      page: resolveApp('./src/pages'),
    }
  },
```

# 三、Vue脚手架

## Vue CLI 

### Vue CLI 安装和使用

- 安装Vue CLI（目前最新的版本是v4.5.13）

  - 我们是进行全局安装，这样在任何时候都可以通过vue的命令来创建项目；

    ```
    npm install @vue/cli -g
    ```

-  升级Vue CLI：

  - 如果是比较旧的版本，可以通过下面的命令来升级

    ```
    npm update @vue/cli -g
    ```

-  通过Vue的命令来创建项目

  ```
  Vue create 项目的名称
  ```

### vue create 项目的过程

![image-20220122010233626](https://s2.loli.net/2022/01/22/EVhJSBHfnG3Zk1z.png)

### 项目的目录结构

![image-20220122010321223](https://s2.loli.net/2022/01/22/6omW1fUeujyICYw.png)



### Vue CLI的运行原理(源码)

![image-20220122010342499](https://s2.loli.net/2022/01/22/oA5R7MTPqN12pnV.png)

## Vite

下一代前端开发与构建工具

### Vite的构造

它主要由两部分组成：

- 一个开发服务器，它基于原生ES模块提供了丰富的内建功能，HMR的速度非常快速；
- 一套构建指令，它使用rollup打开我们的代码，并且它是预配置的，可以输出生成环境的优化过的静态资源；

**浏览器原生支持模块化**

![image-20220122010544729](https://s2.loli.net/2022/01/22/rk8cnpvSbqTUB2Z.png)

-  但是如果我们不借助于其他工具，直接使用ES Module来开发有什么问题呢？
  - 首先，我们会发现在使用loadash时，加载了上百个模块的js代码，对于浏览器发送请求是巨大的消耗；
  - 其次，我们的代码中如果有TypeScript、less、vue等代码时，浏览器并不能直接识别；
-  事实上，vite就帮助我们解决了上面的所有问题。

### Vite的安装和使用

- 首先，我们安装一下vite工具：

  ```
  npm install vite –g # 全局安装
  npm install vite –D # 局部安装
  ```

- 通过vite来启动项目：

  ```
  npx vite
  ```

### Vite对css的支持

- vite可以直接支持css的处理

  - 直接导入css即可；

-  vite可以直接支持css预处理器，比如less

  - 直接导入less；

  - 之后安装less编译器；

    ```
    npm install less -D
    ```

-  vite直接支持postcss的转换：

  - 只需要安装postcss，并且配置 postcss.config.js 的配置文件即可；

    ```
    npm install postcss postcss-preset-env -D
    ```

    ![image-20220122010739149](https://s2.loli.net/2022/01/22/AFK4aWfI58zChOn.png)

### Vite对TypeScript的支持

-  vite对TypeScript是原生支持的，它会直接使用ESBuild来完成编译：
  - 只需要直接导入即可；
-  如果我们查看浏览器中的请求，会发现请求的依然是ts的代码：
  - 这是因为vite中的服务器Connect会对我们的请求进行转发；
  - 获取ts编译后的代码，给浏览器返回，浏览器可以直接进行解析；
-  注意：在vite2中，已经不再使用Koa了，而是使用Connect来搭建的服务器

### vite的服务器原理

![image-20220121212912680](https://s2.loli.net/2022/01/21/6y4NmV5BCphej7i.png)

### Vite对vue的支持

- vite对vue提供第一优先级支持：

  - Vue 3 单文件组件支持：@vitejs/plugin-vue
  - Vue 3 JSX 支持：@vitejs/plugin-vue-jsx
  - Vue 2 支持：underfin/vite-plugin-vue2

-  安装支持vue的插件：

  ```
  npm install @vitejs/plugin-vue -D
  ```

- 在vite.config.js中配置插件：

  ![image-20220122010936364](https://s2.loli.net/2022/01/22/mqPBzv6byNh8ieA.png)

### Vite打包和预览项目

- 打包项目

  ```
  npx vite build
  ```

- 预览项目

  ```
  npx vite preview
  ```

### ESBuild解析

- ESBuild的特点：
  - 超快的构建速度，并且不需要缓存；
  - 支持ES6和CommonJS的模块化；
  - 支持ES6的Tree Shaking；(代码压缩)
  - 支持Go、JavaScript的API；(它是由go语言开发的)
  - 支持TypeScript、JSX等语法编译；
  - 支持SourceMap；
  - 支持代码压缩；
  - 支持扩展其他插件；

-  ESBuild为什么这么快呢？
  - 使用Go语言编写的，可以直接转换成机器代码，而无需经过字节码；
  - ESBuild可以充分利用CPU的多内核，尽可能让它们饱和运行；
  - ESBuild的所有内容都是从零开始编写的，而不是使用第三方，所以从一开始就可以考虑各种性能问题；

### Vite脚手架工具

Vite实际上是有两个工具的：

- vite：相当于是一个构件工具，类似于webpack、rollup；
- @vitejs/create-app：类似vue-cli、create-react-app；

使用脚手架

```
npm init @vitejs/app
```

上面的做法相当于省略了安装脚手架的过程：

```
npm install @vitejs/create-app -g # 全局
create-app
```

# 四、Vue3组件化开发

## 组件的拆分

- 如果我们一个应用程序将所有的逻辑都放在一个组件中，那么这个组件就会变成非常的臃肿和难以维护；
- 所以组件化的核心思想应该是对组件进行拆分，拆分成一个个小的组件；
- 再将这些组件组合嵌套在一起，最终形成我们的应用程序；

![image-20220123150158536](https://s2.loli.net/2022/01/23/afpFjvsWmU4NMrS.png)

## 组件的通信

**父子组件之间如何进行通信呢？**

- 父组件传递给子组件：通过props属性；
- 子组件传递给父组件：通过$emit触发事件；

![image-20220123150302766](https://s2.loli.net/2022/01/23/YQAIZkLeBsa3pNb.png)

### 父组件传递给子组件

-  在开发中很常见的就是父子组件之间通信，比如父组件有一些数据，需要子组件来进行展示：
  - 这个时候我们可以通过props来完成组件之间的通信；
-  什么是Props呢？
  - Props是你可以在组件上注册一些自定义的attribute；
  - 父组件给这些attribute赋值，子组件通过attribute的名称获取到对应的值；
-  Props有两种常见的用法：
  - 方式一：字符串数组，数组中的字符串就是attribute的名称；
  - 方式二：对象类型，对象类型我们可以在指定attribute名称的同时，指定它需要传递的类型、是否是必须的、默认值等等；

![image-20220123150619526](https://s2.loli.net/2022/01/23/jwIuG1nvpoStx2C.png)

#### Props的对象用法

-  数组用法中我们只能说明传入的attribute的名称，并不能对其进行任何形式的限制，接下来我们来看一下对象的写法是如何让我们的props变得更加完善的。

-  当使用对象语法的时候，我们可以对传入的内容限制更多：

  - 比如指定传入的attribute的类型；
  - 比如指定传入的attribute是否是必传的；
  - 比如指定没有传入时，attribute的默认值；

  ```js
    props: {
      title: String,
      inheritAttrs:false,
      content: {
        type: String,
        required: true,
        default:"123"
      },
    },
  ```

#### 细节方面

##### 那么type的类型都可以是哪些呢？

- String
- Number
- Boolean
- Array
- Objec
- Date
- Function
- Symbol

##### 对象类型的其他写法？

![image-20220123151110357](https://s2.loli.net/2022/01/23/gGeOcY1xTpBqtyf.png)

##### Prop 的大小写命名？

- Prop 的大小写命名
  - HTML 中的 attribute 名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符；
  - 这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名；

### 子组件传递给父组件

-  什么情况下子组件需要传递内容到父组件呢？
  - 当子组件有一些事件发生的时候，比如在组件中发生了点击，父组件需要切换内容；
  - 子组件有一些内容想要传递给父组件的时候；
-  我们如何完成上面的操作呢？
  - 首先，我们需要在子组件中定义好在某些情况下触发的事件名称；
  - 其次，在父组件中以v-on的方式传入要监听的事件名称，并且绑定到对应的方法中；
  - 最后，在子组件中发生某个事件的时候，根据事件名称触发对应的事件；

![image-20220123152059790](https://s2.loli.net/2022/01/23/Re2wXTtMWnGOg17.png)

#### 自定义事件的参数和验证

-  自定义事件的时候，我们也可以传递一些参数给父组件：

  ```js
      incrementN() {
        this.$emit("addN", this.num);
      },
  ```

-  在vue3当中，我们可以对传递的参数进行验证：

  ```js
    // 对象的写法的目的是为了进行参数的验证
    emits: {
      add: null,
      sub: null,
      addN: (num) => {
        console.log(num);
        if (num > 10) {
          return true;
        } 
        return false;
      },
    },
  ```

## 非Prop的Attribute

-  什么是非Prop的Attribute呢？
  - 当我们传递给一个组件某个属性，但是该属性并没有定义对应的props或者emits时，就称之为 非Prop的Attribute；
  - 常见的包括class、style、id属性等；

-  Attribute继承
  - 当组件有单个根节点时，非Prop的Attribute将自动添加到根节点的Attribute中：

-  如果我们不希望组件的根元素继承attribute，可以在组件中设置 inheritAttrs: false：

  - 禁用attribute继承的常见情况是需要将attribute应用于根元素之外的其他元素；

  - 我们可以通过 $attrs来访问所有的 非props的attribute；

    ```vue
      <div>
        <h2 :dd="$attrs.dd">{{ title }}</h2>
        <p v-bind="$attrs">{{ content }}</p>
      </div>
    ```

- 多个根节点的attribute

  - 多个根节点的attribute如果没有显示的绑定，那么会报警告，我们必须手动的指定要绑定到哪一个属性上：

    ```vue
      <div :dd="$attrs.dd">我是子组件1</div>
      <div>我是子组件2</div>
      <div>我是子组件3</div>
    ```

## 组件间通信案例

> App.vue 父组件

```vue
<template>
  <div>
    <TabControl :titles="titles" @titleClick="titleClick"></TabControl>
    <h2>{{contents[currentIndex]}}</h2>
  </div>
</template>

<script> 
import TabControl from './TabControl'
export default {
  data() {
    return {
      titles:['衣服','鞋子','裤子'],
      contents:['衣服页面','鞋子页面','裤子页面'],
      currentIndex:0
    }
  },
  components:{
    TabControl
  },
  methods: {
    // 接收子组件发来的值
    titleClick(index){
      this.currentIndex = index;
    }
  },
}
</script>
```

> TabControl.vue 子组件

```vue
<template>
  <div class="tab-control">
    <div
      class="tab-control-item"
      :class="{ active: currentIndex === index }" 
      v-for="(title, index) in titles"
      :key="title"
      @click="itemClick(index)"
    >
      <span>{{ title }}</span>
    </div>
  </div>
</template>

<script>
export default {
  // 定义发送给父组件的emits
  emits: ["titleClick"],
  // 接收父组件发送的titles
  props: {
    titles: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      currentIndex: 0,
    };
  },
  methods: {
    // 将当前点击的index发送给父组件
    itemClick(index) {
      this.currentIndex = index;
      this.$emit("titleClick",index)
    },
  },
};
</script>
```

## 非父子组件的通信

### Provide/Inject 父孙传递

- 无论层级结构有多深，父组件都可以作为其所有子组件的依赖提供者；
- 父组件有一个 provide 选项来提供数据；
- 子组件有一个 inject 选项来开始使用这些数据；

实际上，你可以将依赖注入看作是“long range props”，除了：

- 父组件不需要知道哪些子组件使用它 provide 的 property
-  子组件不需要知道 inject 的 property 来自哪里

![image-20220124230936842](https://s2.loli.net/2022/01/24/fwBx9Xi3g2dUhDO.png)

#### Provide和Inject函数的写法

```js
  provide() {
      //利用函数方法来使this指向这个vue
    return {
      name: "code",
      age: 18,
      length: computed(() => {
        this.names.length;
      }),
    };
  },
```

#### 处理响应式数据

- 我们会发现对应的子组件中是没有反应的：
  - 这是因为当我们修改了names之后，之前在provide中引入的 this.names.length 本身并不是响应式的；
-  那么怎么样可以让我们的数据变成响应式的呢？
  - 非常的简单，我们可以使用响应式的一些API来完成这些功能，比如说computed函数；
  - 当然，这个computed是vue3的新特性，在后面我会专门讲解，这里大家可以先直接使用一下；
-  注意：我们在使用length的时候需要获取其中的value
  - 这是因为computed返回的是一个ref对象，需要取出其中的value来使用；

![image-20220124233135788](https://s2.loli.net/2022/01/24/pEjRyuJgwnBfm3r.png)

### 全局事件总线mitt库

#### 安装mitt库

```
npm install mi
```

以封装一个工具eventbus.js：

```js
import mitt from 'mitt';

const emitter = mitt();

export default emitter;
```

#### 使用事件总线工具

- 我们在Home.vue中监听事件；
- 我们在App.vue中触发事件；

![image-20220124233426739](https://s2.loli.net/2022/01/24/ezm6wMYFW5EsAku.png)

#### Mitt的事件取消

望取消掉之前注册的函数监听:

![image-20220124233543457](https://s2.loli.net/2022/01/24/1yJOaKRNhH52TkB.png)

## 插槽Slot

在开发中，我们会经常封装一个个可复用的组件：

- 前面我们会通过props传递给组件一些数据，让组件来进行展示；
-  但是为了让这个组件具备更强的通用性，我们不能将组件中的内容限制为固定的div、span等等这些元素；
-  比如某种情况下我们使用组件，希望组件显示的是一个按钮，某种情况下我们使用组件希望显示的是一张图片；
-  我们应该让使用者可以决定某一块区域到底存放什么内容和元素；

### 如何使用插槽slot？

-  来定义插槽slot：
  - 插槽的使用过程其实是抽取共性、预留不同；
  - 我们会将共同的元素、内容依然在组件内进行封装；
  - 同时会将不同的元素使用slot作为占位，让外部决定到底显示什么样的元素；

- 如何使用slot呢？
  - Vue中将 <slot> 元素作为承载分发内容的出口；
  - 在封装组件中，使用特殊的元素<slot>就可以为封装组件开启一个插槽；
  - 该插槽插入什么内容取决于父组件如何使用；

> App.vue 父组件

```vue
  <div>
    <my-slot-cpn> <button>我是按钮</button></my-slot-cpn>
    <my-slot-cpn> <MyButton></MyButton> </my-slot-cpn>
    <my-slot-cpn></my-slot-cpn>
  </div>
```

> MySlotCpn.vue

```vue
  <div>
    <h2>组件开始</h2>
    <slot>
      <!--没有插入对应的内容，那么我们需要显示一个默认的内容-->
      <i>我是默认的i元素</i>
    </slot>
    <h2>组件结束</h2>
  </div>
```

### 多个插槽的效果

如果一个组件中含有多个插槽,我们会发现默认情况下每个插槽都会获取到我们插入的内容来显示；

![image-20220124234014255](https://s2.loli.net/2022/01/24/aye618sGFuQBDNM.png)

### 具名插槽的使用

事实上，我们希望达到的效果是插槽对应的显示，这个时候我们就可以使用 具名插槽：

- 具名插槽顾名思义就是给插槽起一个名字，<slot> 元素有一个特殊的 attribute：name；
- 一个不带 name 的slot，会带有隐含的名字 default；

![image-20220124234124875](https://s2.loli.net/2022/01/24/9D3CjaHqTgtGe5l.png)

### 动态插槽名

什么是动态插槽名呢？

- 比如 v-slot:left、v-slot:center等等；
- 我们可以通过 v-slot:[dynamicSlotName]方式动态绑定一个名称；

![image-20220124234206101](https://s2.loli.net/2022/01/24/we6SkdabliNIYFn.png)

### 具名插槽使用的时候语法糖

具名插槽使用的时候缩写：

- 跟 v-on 和 v-bind 一样，v-slot 也有缩写；
- 即把参数之前的所有内容 (v-slot:) 替换为字符 #；

```vue
    <NavBar :name="name">
      <template #left>
        <div>
          <button>左边的按钮</button>
        </div>
      </template>
      <template #center>
        <div>
          <h2>我是标题</h2>
        </div>
      </template>
      <template #right>
        <div>
          <i>右边的i元素 </i>
        </div>
      </template>
      <template #[name]>
        <div>
          <i>lyc内容</i>
        </div>
      </template>
    </NavBar>
```

### 渲染作用域

在Vue中有渲染作用域的概念：

- 父级模板里的所有内容都是在父级作用域中编译的；
- 子模板里的所有内容都是在子作用域中编译的；

![image-20220124234431934](https://s2.loli.net/2022/01/24/JKHb2R6O1n4dAoF.png)

#### 认识作用域插槽

但是有时候我们希望插槽可以访问到子组件中的内容是非常重要的：

- 当一个组件被用来渲染一个数组元素时，我们使用插槽，并且希望插槽中没有显示每项的内容；
- 这个Vue给我们提供了作用域插槽；

![image-20220124234609452](https://s2.loli.net/2022/01/24/5pm9cyu42IzSaQg.png)

### 独占默认插槽的缩写

- 如果我们的插槽是默认插槽default，那么在使用的时候 v-slot:default="slotProps"可以简写为vslot="slotProps"：

  ```vue
      <show-names :names="names">
        <template v-slot="coderwhy">
          <button>{{coderwhy.item}}-{{coderwhy.index}}</button>
        </template>
      </show-names>
  ```

- 并且如果我们的插槽只有默认插槽时，组件的标签可以被当做插槽的模板来使用，这样，我们就可以将 v-slot 直接用在组件上：

  ```vue
      <!-- 独占默认插槽缩写 -->
      <show-names :names="names" v-slot="coderwhy">
        <button>{{coderwhy.item}}-{{coderwhy.index}}</button>
      </show-names>
  ```

- 但是，如果我们有默认插槽和具名插槽，那么按照完整的template来编写

  ```vue
      <!-- 注意: 如果还有其他的具名插槽, 那么默认插槽也必须使用template来编写 -->
      <show-names :names="names">
        <template v-slot="coderwhy">
          <button>{{coderwhy.item}}-{{coderwhy.index}}</button>
        </template>
  
        <template v-slot:why>
          <h2>我是why的插入内容</h2>
        </template>
      </show-names>
  ```


## 动态组件

通过的attribute is 来判断，显示不同的组件；

动态组件是使用 component 组件，通过一个特殊的attribute is 来实现：

```vue
<template>
  <div>
    <button
      v-for="item in tabs"
      :key="item"
      @click="itemClick(item)"
      :class="{ active: currentTab === item }"
    >
      {{ item }}
    </button>
  
  <!-- 动态组件 -->
  <component :is="currentTab"></component>
  </div>
</template> 
```

- **这个currentTab的值需要是什么内容呢？**
  - 可以是通过component函数注册的组件；
  - 在一个组件对象的components对象中注册的组件；

- 如果是动态组件我们可以给它们传值和监听事件吗？
  - 也是一样的；
  - 只是我们需要将属性和监听事件放到component上来使用；

### keep-alive

- 为默认情况下，我们在切换组件后，about组件会被销毁掉，再次回来时会重新创建组件；
- 但是，在开发中某些情况我们希望继续保持组件的状态，而不是销毁掉，这个时候我们就可以使用一个内置组件：
  keep-alive

```vue
  <keep-alive max="1" include="a,b">
  <component :is="currentTab"></component>
  </keep-alive>
```

- keep-alive有一些属性：
  - **include** - string | RegExp | Array。只有名称匹配的组件会被缓存；
  - **exclude** - string | RegExp | Array。任何名称匹配的组件都不会被缓存；
  - **max** - number | string。最多可以缓存多少组件实例，一旦达到这个数字，那么缓存组件中最近没有被访问的实例会被销毁；
-  include 和 exclude prop 允许组件有条件地缓存：
  - 二者都可以用逗号分隔字符串、正则表达式或一个数组来表示；
  - 匹配首先检查组件自身的 name 选项；

![image-20220126223922159](https://s2.loli.net/2022/01/26/6kRzUrdOVSMP3Zl.png)

### 缓存组件的生命周期

- 对于缓存的组件来说，再次进入时，我们是不会执行created或者mounted等生命周期函数的：
  - 但是有时候我们确实希望监听到何时重新进入到了组件，何时离开了组件；
  - 这个时候我们可以使用activated 和 deactivated 这两个生命周期钩子函数来监听；

![image-20220126224220477](https://s2.loli.net/2022/01/26/oIUqOWDjkVNgeYi.png)

## Vue中实现异步组件

### Webpack的代码分包

-  默认的打包过程：
  - 默认情况下，在构建整个组件树的过程中，因为组件和组件之间是通过模块化直接依赖的，那么webpack在打包时就会将组件模块打包到一起（比如一个app.js文件中）；
  - 这个时候随着项目的不断庞大，app.js文件的内容过大，会造成首屏的渲染速度变慢；
-  打包时，代码的分包：
  - 所以，对于一些不需要立即使用的组件，我们可以单独对它们进行拆分，拆分成一些小的代码块chunk.js；
  -  这些chunk.js会在需要时从服务器加载下来，并且运行代码，显示对应的内容；

- 那么webpack中如何可以对代码进行分包呢？

![image-20220126224706612](https://s2.loli.net/2022/01/26/rKwU43sRQbvTPVZ.png)

### Vue中实现异步组件

- 如果我们的项目过大了，对于某些组件我们希望通过异步的方式来进行加载（目的是可以对其进行分包处理），那么Vue中给我们提供了一个函数：defineAsyncComponent
- defineAsyncComponent接受两种类型的参数：
  - 类型一：工厂函数，该工厂函数需要返回一个Promise对象；
  - 类型二：接受一个对象类型，对异步函数进行配置；

```js
  const AsyncCategory = defineAsyncComponent(() => import("./AsyncCategory.vue"))
```

另一种写法：

```js
  const AsyncCategory = defineAsyncComponent({
    loader: () => import("./AsyncCategory.vue"),
    loadingComponent: Loading,
    // errorComponent,
    // 在显示loadingComponent组件之前, 等待多长时间
    delay: 2000,
    /**
     * err: 错误信息,
     * retry: 函数, 调用retry尝试重新加载
     * attempts: 记录尝试的次数
     */
    onError: function(err, retry, attempts) {
    }
  })

```

### 异步组件和Suspense

- 注意：目前（2021-06-08）Suspense显示的是一个实验性的特性，API随时可能会修改。
-  Suspense是一个内置的全局组件，该组件有两个插槽：
  - default：如果default可以显示，那么显示default的内容；
  - fallback：如果default无法显示，那么会显示fallback插槽的内容；

```vue
    <suspense>
      <template #default>
        <async-category></async-category>
      </template>
      <template #fallback>
        <loading></loading>
      </template>
    </suspense>
```

## $refs的使用

- 某些情况下，我们在组件中想要直接获取到元素对象或者子组件实例：
  - 在Vue开发中我们是不推荐进行DOM操作的；
  - 这个时候，我们可以给元素或者组件绑定一个ref的attribute属性；
-  组件实例有一个$refs属性：
  - 它一个对象Object，持有注册过 ref attribute 的所有 DOM 元素和组件实例

```js
   bntClick(){
     this.$refs.NavBar.sayhello();
     console.log(this.$refs.NavBar.sayhello);
     console.log(this.$refs.NavBar.$el);
   }
```

### $parent和$root

- 我们可以通过$parent来访问父元素。
- 这里我们也可以通过$root来实现，因为App是我们的根组件；

```js
getParentAndRoot(){
    console.log(this.$parent.names);
  }
```

## Vue的生命周期

- 什么是生命周期呢？
  - 每个组件都可能会经历从创建、挂载、更新、卸载等一系列的过程；
  - 在这个过程中的某一个阶段，用于可能会想要添加一些属于自己的代码逻辑（比如组件创建完后就请求一些服务器数据）；
  - 但是我们如何可以知道目前组件正在哪一个过程呢？Vue给我们提供了组件的生命周期函数；
-  生命周期函数：
  - 生命周期函数是一些钩子函数，在某个时间会被Vue源码内部进行回调；
  - 通过对生命周期函数的回调，我们可以知道目前组件正在经历什么阶段；
  - 那么我们就可以在该生命周期中编写属于自己的逻辑代码了；

![image-20220126230921323](https://s2.loli.net/2022/01/26/HaKYLZkBCcgXfbM.png)



## 组件的v-model

- 前面我们在input中可以使用v-model来完成双向绑定：
  - 这个时候往往会非常方便，因为v-model默认帮助我们完成了两件事；
  - **v-bind:value的数据绑定**和**@input的事件监听**；
-  如果我们现在封装了一个组件，其他地方在使用这个组件时，是否也可以使用v-model来同时完成这两个功能呢？
  - 也是可以的，vue也支持在组件上使用v-model；
-  当我们在组件上使用的时候，等价于如下的操作：
  - 我们会发现和input元素不同的只是属性的名称和事件触发的名称而已；

```vue
    <Home v-model="message"></Home>
	<!--等同于-->
    <Home :modelValue="message" @update:model-value="message = $event"></Home>
```

- 那么，为了我们的MyInput组件可以正常的工作，这个组件内的 <input> 必须：
  - 将其 value attribute 绑定到一个名叫 modelValue 的 prop上；
  - 在其 input 事件被触发时，将新的值通过自定义的 update:modelValue 事件抛出；

![image-20220126231247024](https://s2.loli.net/2022/01/26/cENi6HVu3FhlX1s.png)

### computed实现

- 我们依然希望在组件内部按照双向绑定的做法去完成，应该如何操作呢？我们可以使用计算属性的setter和getter来完成。

![image-20220126231415627](https://s2.loli.net/2022/01/26/dmto7HRB4MaLCkh.png)

### 绑定多个属性

- 我们现在通过v-model是直接绑定了一个属性，如果我们希望绑定多个属性呢？

  - 也就是我们希望在一个组件上使用多个v-model是否可以实现呢？
  - 我们知道，默认情况下的v-model其实是绑定了 modelValue 属性和 @update:modelValue的事件；
  - 如果我们希望绑定更多，可以给v-model传入一个参数，那么这个参数的名称就是我们绑定属性的名称；

- 注意：这里我是绑定了两个属性的

  ```vue
  <Home v-model="message" v-model:title="title"></Home>
  ```

- v-model:title相当于做了两件事：

  - 绑定了title属性；
  - 监听了 @update:title的事件；

![image-20220126231651604](https://s2.loli.net/2022/01/26/BVTtEb2xnG6hdKe.png)



# 五、Vue3过度动画

## Vue的transition动画

Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加进入/离开过渡：

- 条件渲染 (使用 v-if)条件展示 (使用 v-show)
- 动态组件
-  组件根节点

```vue
    <transition name="lyc">
      <h2 class="title" v-if="isShow">hello world!</h2>
      <h2 class="title" v-else>i你好啊</h2>
    </transition>

    <style scoped>
        .title {
          display: inline-block;
        }
        .lyc-enter-from,
        .lyc-leave-to{
          opacity: 0;
        }
        .lyc-enter-active,
        .lyc-leave-active{ 
          transition: opacity 1s ease;
        }
    </style>
```

### Transition组件的原理

**当插入或删除包含在 transition 组件中的元素时，Vue 将会做以下处理：**

1. 自动嗅探目标元素是否应用了CSS过渡或者动画，如果有，那么在恰当的时机添加/删除 CSS类名；
2. 如果 transition 组件提供了JavaScript钩子函数，这些钩子函数将在恰当的时机被调用；
3. 如果没有找到JavaScript钩子并且也没有检测到CSS过渡/动画，DOM插入、删除操作将会立即执行；

### 过渡动画class

**我们会发现上面提到了很多个class，事实上Vue就是帮助我们在这些class之间来回切换完成的动画：**

- v-enter-from：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。
-  v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。
-  v-enter-to：定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter-from 被移除)，在过渡/动画完成之后移除。
-  v-leave-from：定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
-  v-leave-active：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。
-  v-leave-to：离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave-from 被删除)，在过渡/动画完成之后移除

![image-20220128142916609](https://s2.loli.net/2022/01/28/tKkxXmMTc2JS8Es.png)

**class的name命名规则如下：**

- 如果我们使用的是一个没有name的transition，那么所有的class是以 v- 作为默认前缀；
- 如果我们添加了一个name属性，比如 **transtion name="why"**，那么所有的class会以 why- 开头；

### animation过渡css动画

**前面我们是通过transition来实现的动画效果，另外我们也可以通过animation来实现。**

```css
.lyc-enter-active {
  animation: bounce 1s ease;
}
.lyc-leave-active {
  animation: bounce 1s ease reverse;
}

@keyframes bounce {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}
```

### 同时设置过渡和动画

- Vue为了知道过渡的完成，内部是在监听 transitionend 或 animationend，到底使用哪一个取决于元素应用的CSS规则：
  - 如果我们只是使用了其中的一个，那么Vue能自动识别类型并设置监听；

- 但是如果我们同时使用了过渡和动画呢？
  - 并且在这个情况下可能某一个动画执行结束时，另外一个动画还没有结束；
  - 在这种情况下，我们可以设置 type 属性为 animation 或者 transition 来明确的告知Vue监听的类型；

### 显示的指定动画时间

- 我们也可以显示的来指定过渡的时间，通过 duration 属性。
- duration可以设置两种类型的值：
  - number类型：同时设置进入和离开的过渡时间；
  - object类型：分别设置进入和离开的过渡时间；

### 过渡的模式mode

- 我们来看当前的动画在两个元素之间切换的时候存在的问题：进入和离开动画是同时发生的,所以会很突兀
- 但是如果我们不希望同时执行进入和离开动画，那么我们需要设置transition的过渡模式：
  - in-out: 新元素先进行过渡，完成之后当前元素过渡离开；
  - out-in: 当前元素先进行过渡，完成之后新元素过渡进入；

### 动态组件的切换

- transition同样适用于我们的动态组件

### appear初次渲染

默认情况下，首次渲染的时候是没有动画的，如果我们希望给他添加上去动画，那么就可以增加另外一个属性appear

```vue
<transition name="lyc" type="animation" :datatype="1000" mode="out-in" appear>
      <component :is="isShow?'home':'about' "></component>
    </transition>
```

## 第三方动画库使用

### 认识animate.css

Animate.css是一个已经准备好的、跨平台的动画库为我们的web项目，对于强调、主页、滑动、注意力引导非常有用；

如何使用Animate库呢？

- 第一步：需要安装animate.css库；

  ```
  npm install animate.css
  ```

- 第二步：导入animate.css库的样式；

  ```js
  import "animate.css"
  ```

- 第三步：

  - 用法一：直接使用animate库中定义的 keyframes 动画；
  - 用法二：直接使用animate库提供给我们的类；

  ```vue
      <transition
        name="lyc"
        type="animation"
        enter-active-class="animate__animated  animate__backInLeft"
        leave-active-class="animate__animated animate__backOutDown"
      >
        <h2 class="title" v-if="isShow">hello world!</h2>
        <h2 class="title" v-else>i你好啊</h2>
      </transition>
  
      <style>
      .lyc-enter-active{
        animation: bounceInUp 1s ease;
      }
      .lyc-leave-active {
        animation: bounceInUp 1s ease reverse;
      }
      </style>
  ```

#### 自定义过渡class

我们可以通过以下 attribute 来自定义过渡类名：

他们的优先级高于普通的类名，这对于 Vue 的过渡系统和其他第三方 CSS 动画库，如 Animate.css. 结合使用十分有用

- enter-from-class
- enter-active-class
- enter-to-class
- leave-from-class
- leave-active-class
- leave-to-class

### gsap库(通过JavaScript来实现一些动画的效果)

什么是gsap呢？

- GSAP是The GreenSock Animation Platform（GreenSock动画平台）的缩写；
- 它可以通过JavaScript为CSS属性、SVG、Canvas等设置动画，并且是浏览器兼容的；

这个库应该如何使用呢？

- 第一步：需要安装gsap库；

  ```
  npm install gsap
  ```

- 第二步：导入gsap库；

  ```js
  import gsap from "gsap";
  ```

- 第三步：使用对应的api即可；

#### JavaScript钩子

- 在使用动画之前，我们先来看一下transition组件给我们提供的JavaScript钩子，这些钩子可以帮助我们监听动画执行到什么阶段了
- 当我们使用JavaScript来执行过渡动画时，需要进行 done 回调，否则它们将会被同步调用，过渡会立即完成。
- 添加 :css="false"，也会让 Vue 会跳过 CSS 的检测，除了性能略高之外，这可以避免过渡过程中 CSS 规则的影响

![image-20220128145013746](https://s2.loli.net/2022/01/28/VkmHO3CfEh7lqLA.png)

接下来我们就可以结合gsap库来完成动画效果：

```js
    enter(el, done) {
      gsap.from(el, {
        scale: 0,
        x: this.distance,
        onComplete: done,
      });
    },
    leave(el, done) {
      gsap.to(el, {
        scale: 0,
        x: this.distance,
        onComplete: done,
      });
```

#### 认识列表的过渡

- 目前为止，过渡动画我们只要是针对单个元素或者组件的：
  - 要么是单个节点；
  - 要么是同一时间渲染多个节点中的一个；
- 那么如果希望渲染的是一个列表，并且该列表中添加删除数据也希望有动画执行呢？
  - 这个时候我们要使用 transition-group 组件来完成；
- 使用 transition-group 有如下的特点：
  - 默认情况下，它不会渲染一个元素的包裹器，但是你可以指定一个元素并以 tag attribute 进行渲染；
  - 过渡模式不可用，因为我们不再相互切换特有的元素；
  - 内部元素总是需要提供唯一的 key attribute 值；
  - CSS 过渡的类将会应用在内部的元素中，而不是这个组/容器本身；

## 案例

### gsap实现数字变化

在一些项目中，我们会见到数字快速变化的动画效果，这个动画可以很容易通过gsap来实现：

```vue
<template>
  <div class="app">
    <input type="number" step="100" v-model="counter" />
    <h2>当前计数:{{ showCounter }}</h2>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  data() {
    return {
      counter: 0,
      showNumber: 0,
    };
  },
  methods: {},
  computed: {
    showCounter() {
      return this.showNumber.toFixed(0);
    },
  },
  watch: {
    counter(newValue) {
      gsap.to(this, { duration: 1, showNumber: newValue });
    },
  },
};
</script>
```

### 列表过渡的基本使用

我们来做一个案例：

- 案例是一列数字，可以继续添加,删除数字,；
- 在添加和删除数字的过程中，对添加的或者移除的数字添加动画；

![image-20220128145953170](https://s2.loli.net/2022/01/28/ZLW3EYyt91h7kKl.png)

```vue
<template>
  <div>
    <button @click="add">添加数字</button>
    <button @click="remove">删除数字</button>
    <button @click="shuffleNum">数字洗牌</button>
    <transition-group tag="p" name="why">
      <span v-for="item in numbers" :key="item" class="item">
        {{ item }}
      </span>
    </transition-group>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
  data() {
    return {
      numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      numCounter: 10,
    };
  },
  methods: {
    add() {
      this.numbers.splice(this.randomIndex(), 0, this.numCounter++);
    },
    remove() {
      this.numbers.splice(this.randomIndex(), 1);
    },
    shuffleNum(){
      this.numbers = _.shuffle(this.numbers)
    },
    randomIndex() {
      return Math.floor(Math.random() * this.numbers.length);
    },
  },
};
</script>

<style>
.item {
  margin-right: 10px;
  display: inline-block;
}
.why-enter-from,
.why-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.why-enter-active,
.why-leave-active {
  transition: all 1s ease;
}

.why-leave-active{
  position: absolute;
}

.why-move {
  transition: transform 1s ease ;
}
</style>

```



### 列表的交错过渡案例

我们来通过gsap的延迟delay属性，做一个交替消失的动画：

```vue
<template>
  <div>
    <input type="text" v-model="keyword" />
    <transition-group
      tag="ul"
      :css="false"
      @before-enter="beforeEnter"
      @enter="enter"
      @leave="leave"
    >
      <li
        v-for="(item, index) in showMames"
        :data-index="index"
        :key="item"
        name="why"
      >
        {{ item }}
      </li>
    </transition-group>
  </div>
</template>

<script>
import gsap from "gsap";
export default {
  data() {
    return {
      names: ["abc", "cba", "nab", "lie", "wyc", "wrn", "aaa"],
      keyword: "",
    };
  },
  methods: {
    beforeEnter(el) {
      el.style.opacity = 0;
      el.style.height = 0;
    },
    enter(el, done) {
      gsap.to(el, {
        opacity: 1,
        height: "1.5em",
        delay: el.dataset.index * 0.5,
          //根据index来延迟消失
        onComplete: done,
      });
    },
    leave(el, done) {
      gsap.to(el, {
        opacity: 0,
        height: 0,
        delay: el.dataset.index * 0.5,
        onComplete: done,
      });
    },
  },
  computed: {
    showMames() {
      return this.names.filter((item) => item.indexOf(this.keyword) !== -1);
    },
  },
};
</script>

<style></style>

```

# 六、代码复用

## Mixin方法

目前我们是使用组件化的方式在开发整个Vue的应用程序，但是组件和组件之间有时候会存在相同的代码逻辑，我们希望对相同的代码逻辑进行抽取

- Mixin提供了一种非常灵活的方式，来分发Vue组件中的可复用功能；
- 一个Mixin对象可以包含任何组件选项；
- 当组件使用Mixin对象时，所有Mixin对象的选项将被 混合 进入该组件本身的选项中；

![image-20220204153104915](https://s2.loli.net/2022/02/04/nIC6MQG2UrdHkK1.png)

### Mixin的合并规则

- 情况一：如果是data函数的返回值对象
  - 返回值对象默认情况下会进行合并；
  - 如果data返回值对象的属性发生了冲突，那么会保留组件自身的数据；
- 情况二：如何生命周期钩子函数
  - 生命周期的钩子函数会被合并到数组中，都会被调用；
- 情况三：值为对象的选项，例如 methods、components 和 directives，将被合并为同一个对象。
  - 比如都有methods选项，并且都定义了方法，那么它们都会生效；
  - 但是如果对象的key相同，那么会取组件对象的键值对；

### 全局混入Mixin

如果组件中的某些选项，是所有的组件都需要拥有的，那么这个时候我们可以使用全局的mixin：

- 全局的Mixin可以使用 应用app的方法 mixin 来完成注册；
- 一旦注册，那么全局混入的选项将会影响每一个组件；

```js
app.mixin({
  created() {
    console.log("全局mixin混入");
  },
})
```

## Extends方法

另外一个类似于Mixin的方式是通过extends属性：

- 允许声明扩展另外一个组件，类似于Mixins；

![image-20220204153711763](https://s2.loli.net/2022/02/04/PmUdLIZgScx81Hh.png)

## Options API的弊端

- 在Vue2中，我们编写组件的方式是Options API：
  - Options API的一大特点就是在对应的属性中编写对应的功能模块；
  - 比如data定义数据、methods中定义方法、computed中定义计算属性、watch中监听属性改变，也包括生命周期钩子；
-  但是这种代码有一个很大的弊端：
  - 当我们实现某一个功能时，这个功能对应的代码逻辑会被拆分到各个属性中；
  - 当我们组件变得更大、更复杂时，逻辑关注点的列表就会增长，那么同一个功能的逻辑就会被拆分的很分散；
  - 尤其对于那些一开始没有编写这些组件的人来说，这个组件的代码是难以阅读和理解的（阅读组件的其他人）；
-  下面我们来看一个非常大的组件，其中的逻辑功能按照颜色进行了划分：
  - 这种碎片化的代码使用理解和维护这个复杂的组件变得异常困难，并且隐藏了潜在的逻辑问题；
  - 并且当我们处理单个逻辑关注点时，需要不断的跳到相应的代码块中；

- 如果我们能将同一个逻辑关注点相关的代码收集在一起会更好。
-  这就是Composition API想要做的事情，以及可以帮助我们完成的事情

# 七、Composition API

## setup函数

setup就是组件的另外一个选项：

- 只不过这个选项强大到我们可以用它来替代之前所编写的大部分其他选项；
- 比如methods、computed、watch、data、生命周期等等；

#### setup函数的参数

-  我们先来研究一个setup函数的参数，它主要有两个参数：
  - 第一个参数：props
  - 第二个参数：context
-  props非常好理解，**它其实就是父组件传递过来的属性会被放到props对象中**，我们在setup中如果需要使用，那么就可以直接通过props参数获取：
  - 对于定义props的类型，我们还是和之前的规则是一样的，在props选项中定义；
  - 并且在template中依然是可以正常去使用props中的属性，比如message；
  - 如果我们在setup函数中想要使用props，那么不可以通过 this 去获取；
  - 因为props有直接作为参数传递到setup函数中，所以我们可以直接通过参数来使用即可；
-  另外一个参数是context，我们也称之为是一个SetupContext，它里面包含三个属性：
  - **attrs**：所有的非prop的attribute；
  - **slots**：父组件传递过来的插槽（这个在以渲染函数返回时会有作用，后面会讲到）；
  - **emit**：当我们组件内部需要发出事件时会用到emit（因为我们不能访问this，所以不可以通过 this.$emit发出事件）；

#### etup函数的返回值

- setup既然是一个函数，那么它也可以有返回值，它的返回值用来做什么呢？

  - setup的返回值可以在模板template中被使用；
  - 也就是说我们可以通过setup的返回值来替代data选项；

- 甚至是我们可以返回一个执行函数来代替在methods中定义的方法：

  ```js
      return {
        increment,
        state,
      };
  ```

- 但是，如果我们将 counter 在 increment 或者 decrement （改变setup里的值时）进行操作时，不可以实现界面的响应式！

#### setup不可以使用this

- 官方关于this有这样一段描述：
  - 表达的含义是this并没有指向当前组件实例；
  - 并且在setup被调用之前，data、computed、methods等都没有被解析；
  - 所以无法在setup中获取this；

### 响应式数据使用

#### Reactive API

如果想为在setup中定义的数据提供响应式的特性，那么我们可以使用reactive的函数：

```js
    const state = reactive({
      counter:100
    })
```

那么这是什么原因呢？为什么就可以变成响应式的呢？

- 这是因为当我们使用reactive函数处理我们的数据之后，数据再次被使用时就会进行依赖收集；
- 当数据发生改变时，所有收集到的依赖都是进行对应的响应式操作（比如更新界面）；
- 事实上，我们编写的data选项，也是在内部交给了reactive函数将其编程响应式对象的；

reactive API对传入的类型是有限制的，它要求我们必须传入的是一个对象或者数组类型：

- 如果我们传入一个基本数据类型（String、Number、Boolean）会报一个警告

  ![image-20220204160915080](C:/Users/Roy_Dust/AppData/Roaming/Typora/typora-user-images/image-20220204160915080.png)

#### Ref API

这个时候Vue3给我们提供了另外一个API：ref API

- ref 会返回一个可变的响应式对象，该对象作为一个 响应式的引用 维护着它内部的值，这就是ref名称的来源；

- 它内部的值是在ref的 value 属性中被维护的；

  ```js
      let count = ref(100)
  ```

- 这里有两个注意事项：
  - 在模板中引入ref的值时，Vue会自动帮助我们进行解包操作，所以我们并不需要在模板中通过 ref.value 的方式来使用；
  - 但是在 setup 函数内部，它依然是一个 ref引用， 所以对其进行操作时，我们依然需要使用 ref.value的方式；

#### Ref自动解包

- 模板中的解包是浅层的解包，如果我们的代码是下面的方式：
-  如果我们将ref放到一个reactive的属性当中，那么在模板中使用时，它会自动解包：

![image-20220204161156102](https://s2.loli.net/2022/02/04/DzM2UueqHQxl6P5.png)

#### readonly

- 我们通过reactive或者ref可以获取到一个响应式的对象，但是某些情况下，我们传入给其他地方（组件）的这个响应式对象希望在另外一个地方（组件）被使用，但是不能被修改，这个时候如何防止这种情况的出现呢？
  - Vue3为我们提供了readonly的方法；
  - readonly会返回原生对象的只读代理（也就是它依然是一个Proxy，这是一个proxy的set方法被劫持，并且不能对其进行修改）；

- 在readonly的使用过程中，有如下规则：
  - **readonly返回的对象都是不允许修改的**；
  - 但是经过readonly处理的原来的对象是允许被修改的；
    - 比如 const info = readonly(obj)，info对象是不允许被修改的；
    - 当obj被修改时，readonly返回的info对象也会被修改；
    - 但是我们不能去修改readonly返回的对象info；
  - 其实**本质上就是readonly返回的对象的setter方法被劫持了而已**；

![image-20220204161431450](https://s2.loli.net/2022/02/04/rclmK3J1w9d2OEq.png)

#### Reactive判断的API

-  isProxy
  - 检查对象是否是由 reactive 或 readonly创建的 proxy。
-  isReactive
  - 检查对象是否是由 reactive创建的响应式代理：
  - 如果该代理是 readonly 建的，但包裹了由 reactive 创建的另一个代理，它也会返回 true；
-  isReadonly
  - 检查对象是否是由 readonly 创建的只读代理。
-  toRaw
  - 返回 reactive 或 readonly 代理的原始对象（不建议保留对原始对象的持久引用。请谨慎使用）。
-  shallowReactive
  - 创建一个响应式代理，它跟踪其自身 property 的响应性，但不执行嵌套对象的深层响应式转换 (深层还是原生对象)。
-  shallowReadonly
  - 创建一个 proxy，使其自身的 property 为只读，但不执行嵌套对象的深度只读转换（深层还是可读、可写的）。

#### toRefs和toRef

- 如果我们使用ES6的解构语法，对reactive返回的对象进行解构获取值，那么之后无论是修改结构后的变量，还是修改reactive返回的state对象，数据都不再是响应式的

- 那么有没有办法让我们解构出来的属性是响应式的呢？

  - Vue为我们提供了一个toRefs的函数，可以将reactive返回的对象中的属性都转成ref；
  - 那么我们再次进行结构出来的 name 和 age 本身都是 ref的；

- 这种做法相当于已经在state.name和ref.value之间建立了 链接，任何一个修改都会引起另外一个变化；

- 如果我们只希望转换一个reactive对象中的属性为ref, 那么可以使用toRef的方法：

  ```js
        const info = reactive({name: "why", age: 18});
        // 1.toRefs: 将reactive对象中的所有属性都转成ref, 建立链接
        // let { name, age } = toRefs(info);
        // 2.toRef: 对其中一个属性进行转换ref, 建立链接
        let { name } = info;
        let age = toRef(info, "age");
  ```

#### ref其他的API

- unref

  - 如果我们想要获取一个ref引用中的value，那么也可以通过unref方法：
  - 如果参数是一个 ref，则返回内部值，否则返回参数本身；
  - 这是 val = isRef(val) ? val.value : val 的语法糖函数；

-  isRef

  - 判断值是否是一个ref对象。

-  shallowRef

  - 创建一个浅层的ref对象；

-  triggerRef

  - 手动触发和 shallowRef 相关联的副作用：

  ```js
        const changeInfo = () => {
          info.value.name = "james";
          triggerRef(info);
        }
  ```

#### customRef自定义ref

创建一个自定义的ref，并对其依赖项跟踪和更新触发进行显示控制：

- 它需要一个工厂函数，该函数接受 track 和 trigger 函数作为参数；
- 并且应该返回一个带有 get 和 set 的对象；

![image-20220206145321352](https://s2.loli.net/2022/02/06/4vuHTaBbhmOCE1F.png)



## computed

如何使用computed呢？

- 方式一：接收一个getter函数，并为 getter 函数返回的值，返回一个不变的 ref 对象；
- 方式二：接收一个具有 get 和 set 的对象，返回一个可变的（可读写）ref 对象；

```js
      const firstName = ref("Kobe");
      const lastName = ref("Bryant");

      // 1.用法一: 传入一个getter函数
      // computed的返回值是一个ref对象
      const fullName = computed(() => firstName.value + " " + lastName.value);

      // 2.用法二: 传入一个对象, 对象包含getter/setter
      const fullName = computed({
        get: () => firstName.value + " " + lastName.value,
        set(newValue) {
          const names = newValue.split(" ");
          firstName.value = names[0];
          lastName.value = names[1];
        }
      });
```

## 侦听数据的变化

- watchEffect用于自动收集响应式数据的依赖；
- watch需要手动指定侦听的数据源；

### setup中使用ref

我们只需要定义一个ref对象，绑定到元素或者组件的ref属性上即可在setup中如何使用ref或者元素或者组件；

![image-20220206150910607](https://s2.loli.net/2022/02/06/wix8mlgtaGubXMR.png)

### watchEffect

- 首先，watchEffect传入的函数会被立即执行一次，并且在执行的过程中会收集依赖；
- 其次，只有收集的依赖发生变化时，watchEffect传入的函数才会再次执行；

```js
      // watchEffect: 自动收集响应式的依赖
      const name = ref("why");
      const age = ref(18);

      const changeName = () => name.value = "kobe"
      const changeAge = () => age.value++

      watchEffect(() => {
        console.log("name:", name.value, "age:", age.value);
      });
```

#### watchEffect的停止侦听

- 如果在发生某些情况下，我们希望停止侦听，这个时候我们可以获取watchEffect的返回值函数，调用该函数即可。

```js
      const stop = watchEffect(() => {
        console.log("name:", name.value, "age:", age.value);
      });

      const changeName = () => name.value = "kobe"
      const changeAge = () => {
        age.value++;
        if (age.value > 25) {
          stop();
        }
      }
```

#### watchEffect清除副作用

- 什么是清除副作用呢？
  - 比如在开发中我们需要在侦听函数中执行网络请求，但是在网络请求还没有达到的时候，我们停止了侦听器，或者侦听器侦听函数被再次执行了。
  - 那么上一次的网络请求应该被取消掉，这个时候我们就可以清除上一次的副作用；
-  在我们给watchEffect传入的函数被回调时，其实可以获取到一个参数：onInvalidate
  - 当副作用**即将重新执行** 或者 **侦听器被停止** 时会执行该函数传入的回调函数；
  - 我们可以在传入的回调函数中，执行一些清楚工作；

```js
      const stop = watchEffect((onInvalidate) => {
        const timer = setTimeout(() => {
          console.log("网络请求成功~");
        }, 2000)

        // 根据name和age两个变量发送网络请求
        onInvalidate(() => {
          // 在这个函数中清除额外的副作用
          // request.cancel()
          clearTimeout(timer);
          console.log("onInvalidate");
        })
        console.log("name:", name.value, "age:", age.value);
      });
```

#### watchEffect的执行时机

- 我们可以设置副作用函数的执行时机：

```js
      const title = ref(null);

      watchEffect(() => {
        console.log(title.value);
      }, {
        //默认值是pre
        flush: "post"
      })
```

- flush 选项还接受 sync，这将强制效果始终同步触发。然而，这是低效的，应该很少需要。

### watch

- watch的API完全等同于组件watch选项的Property：
  - watch需要侦听特定的数据源，并在回调函数中执行副作用；
  - 默认情况下它是惰性的，只有当被侦听的源发生变化时才会执行回调；
-  与watchEffect的比较，watch允许我们：
  - 懒执行副作用（第一次不会直接执行）；
  - 更具体的说明当哪些状态发生变化时，触发侦听器的执行；
  - 访问侦听状态变化前后的值；

watch侦听函数的数据源有两种类型：

- 一个getter函数：但是该getter函数必须引用可响应式的对象（比如reactive或者ref）；
- 直接写入一个可响应式的对象，reactive或者ref（比较常用的是ref）；

如果我们希望侦听一个数组或者对象，那么可以使用一个getter函数，并且对可响应对象进行解构

```js
      const info = reactive({name: "why", age: 18});

      // 1.侦听watch时,传入一个getter函数
      watch(() => info.name, (newValue, oldValue) => {
        console.log("newValue:", newValue, "oldValue:", oldValue);
      })

      // 2.传入一个可响应式对象: reactive对象/ref对象
      // 情况一: reactive对象获取到的newValue和oldValue本身都是reactive对象
      watch(info, (newValue, oldValue) => {
        console.log("newValue:", newValue, "oldValue:", oldValue);
      })
      // 如果希望newValue和oldValue是一个普通的对象
      watch(() => {
        return {...info}
      }, (newValue, oldValue) => {
        console.log("newValue:", newValue, "oldValue:", oldValue);
      })
      // 情况二: ref对象获取newValue和oldValue是value值的本身
      const name = ref("why");
      watch(name, (newValue, oldValue) => {
        console.log("newValue:", newValue, "oldValue:", oldValue);
      })
```

还可以侦听多个源

```js
      // 1.定义可响应式的对象
      const info = reactive({name: "why", age: 18});
      const name = ref("why");

      // 2.侦听器watch
      watch([() => ({...info}), name], ([newInfo, newName], [oldInfo, oldName]) => {
        console.log(newInfo, newName, oldInfo, oldName);
      })
```

- 如果我们希望侦听一个深层的侦听，那么依然需要设置 deep 为true：
- 也可以传入 immediate 立即执行；

```js
      // 1.定义可响应式的对象
      const info = reactive({
        name: "why", 
        age: 18,
        friend: {
          name: "kobe"
        }
      });

      // 2.侦听器watch
      watch(() => ({...info}), (newInfo, oldInfo) => {
        console.log(newInfo, oldInfo);
      }, {
        deep: true,
        immediate: true
      })
```

## 生命周期钩子

**setup中如何使用生命周期函数呢？**

可以使用直接导入的 onX 函数注册生命周期钩子；

- onBeforeMount
- onMounted
- onBeforeUpdate
- onUpdated
- onBeforeUnmount
- onUnmounted
- onActivated
- onDeactivated
- onErrorCaptured

```js
import { onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted, onActivated, onDeactivated, onErrorCaptured } from 'vue'

export default {
  setup() {
    onBeforeMount(() => {
      // ... 
    })
    onMounted(() => {
      // ... 
    })
    onBeforeUpdate(() => {
      // ... 
    })
    onUpdated(() => {
      // ... 
    })
    onBeforeUnmount(() => {
      // ... 
    })
    onUnmounted(() => {
      // ... 
    })
    onActivated(() => {
      // ... 
    })
    onDeactivated(() => {
      // ... 
    })
    onErrorCaptured(() => {
      // ... 
    })
  }
}
```

![image-20220210145621065](https://s2.loli.net/2022/02/10/c4VO1FMTSLtEw2y.png)

## 数据传输Provide和Inject函数

我们可以通过 provide来提供数据：

- 可以通过 provide 方法来定义每个 Property；
- provide可以传入两个参数：
  - name：提供的属性名称；
  - value：提供的属性值； 

```js
  setup(props) {
    const name = "lyc";
    const counter = 100;

    provide("name", name);
    provide("counter", counter);
  },
```

在后代组件 中可以通过 inject 来注入需要的属性和对应的值：

- 可以通过 inject 来注入需要的内容；
- inject可以传入两个参数：
  - 要 inject 的 property 的 name；
  - 默认值；

```js
    const name = inject("name","")
    const name = inject("counter","")
    return{
      name,counter
    }
```

如果我们需要修改可响应的数据，那么最好是在数据提供的位置来修改：

- 我们可以将修改方法进行共享，在后代组件中进行调用；
- 而不是让后代直接修改父代的值

![image-20220210150709670](https://s2.loli.net/2022/02/10/hlANOqCMixHUtdm.png)

## 抽取封装hooks

在Vue3使用中可以将一个单独的函数和值抽离出来封装成一个个hook，原来Vue在引用相对应的hook

**案例：**

> Vue.js

```vue
<template>
  <div>
    <h2>当前计数: {{counter}}</h2>
    <h2>计数*2: {{doubleCounter}}</h2>
    <button @click="increment">+1</button>
    <button @click="decrement">-1</button>

    <h2>{{data}}</h2>
    <button @click="changeData">修改data</button>

    <p class="content"></p>

    <div class="scroll">
      <div class="scroll-x">scrollX: {{scrollX}}</div>
      <div class="scroll-y">scrollY: {{scrollY}}</div>
    </div>
    
    <div class="mouse">
      <div class="mouse-x">mouseX: {{mouseX}}</div>
      <div class="mouse-y">mouseY: {{mouseY}}</div>
    </div>
  </div>
</template>

<script>
  // 从hooks的入口拿取函数
  import {
    useCounter,
    useLocalStorage,
    useMousePosition,
    useScrollPosition,
    useTitle
  } from './hooks';

  export default {
    setup() {
      // counter
      const { counter, doubleCounter, increment, decrement } = useCounter();

      // title
      const titleRef = useTitle("coderwhy");
      setTimeout(() => {
        titleRef.value = "kobe"
      }, 3000);

      // 滚动位置
      const { scrollX, scrollY } = useScrollPosition();

      // 鼠标位置
      const { mouseX, mouseY } = useMousePosition();

      // localStorage
      const data = useLocalStorage("info");
      const changeData = () => data.value = "哈哈哈哈"

      return {
        counter,
        doubleCounter,
        increment,
        decrement,

        scrollX,
        scrollY,

        mouseX,
        mouseY,

        data,
        changeData
      }
    }
  }
</script>
```

> hooks index.js

```js
import useCounter from './useCounter';
import useTitle from './useTitle';
import useScrollPosition from './useScrollPosition';
import useMousePosition from './useMousePosition';
import useLocalStorage from './useLocalStorage';

export {
  useCounter,
  useTitle,
  useScrollPosition,
  useMousePosition,
  useLocalStorage
}
```

> useLocalStorage 封装的localstorage

```js
import { ref, watch } from 'vue';

export default function(key, value) {
  const data = ref(value);

  if (value) {
    window.localStorage.setItem(key, JSON.stringify(value));
  } else {
    data.value = JSON.parse(window.localStorage.getItem(key));
  }

  watch(data, (newValue) => {
    window.localStorage.setItem(key, JSON.stringify(newValue));
  })
  
  return data;
}
```

# 八、渲染函数

## h函数

- Vue推荐在绝大数情况下使用模板来创建你的HTML，然后一些特殊的场景，你真的需要JavaScript的完全编程的能力，这个时候你可以使用 渲染函数 ，它比模板更接近编译器；
  - 前面我们讲解过VNode和VDOM的改变：
  - Vue在生成真实的DOM之前，会将我们的节点转换成VNode，而VNode组合在一起形成一颗树结构，就是虚拟DOM（VDOM）；
  - 事实上，我们之前编写的 template 中的HTML 最终也是使用渲染函数生成对应的VNode；
  - 那么，如果你想充分的利用JavaScript的编程能力，我们可以自己来编写 createVNode 函数，生成对应的VNode；
-  那么我们应该怎么来做呢？使用 h()函数：
  - h() 函数是一个用于创建 vnode 的一个函数；
  - 其实更准备的命名是 createVNode() 函数，但是为了简便在Vue将之简化为 h() 函数；

![image-20220210193220206](https://s2.loli.net/2022/02/10/498h3PEb5OcpWdB.png)

注意：

- 如果没有props，那么通常可以将children作为第二个参数传入；
- 如果会产生歧义，可以将null作为第二个参数传入，将children作为第三个参数传入；

**h函数可以在两个地方使用：**

- render函数选项中；
- setup函数选项中（setup本身需要是一个函数类型，函数再返回h函数创建的VNode）；

![image-20220210193411609](https://s2.loli.net/2022/02/10/oMb3KLu5qz4SiNZ.png)

**函数组件和插槽的使用**

![image-20220210193511782](https://s2.loli.net/2022/02/10/bm1g5HTLqfxnKQr.png)

## JSX

### jsx的babel配置

- 如果我们希望在项目中使用jsx，那么我们需要添加对jsx的支持：

  - jsx我们通常会通过Babel来进行转换（React编写的jsx就是通过babel转换的）；
  - 对于Vue来说，我们只需要在Babel中配置对应的插件即可；

-  安装Babel支持Vue的jsx插件：

  ```
  npm install @vue/babel-plugin-jsx -D
  ```

- 在babel.config.js配置文件中配置插件：

  ![image-20220210193643991](https://s2.loli.net/2022/02/10/E6AUtTQBIYLHd3j.png)

### jsx计数器案例和组件的使用

```vue
<script>
  import HelloWorld from './HelloWorld.vue';

  export default {
    data() {
      return {
        counter: 0
      }
    },

    render() {
      const increment = () => this.counter++;
      const decrement = () => this.counter--;

      return (
        <div>
          <h2>当前计数: {this.counter}</h2>
          <button onClick={increment}>+1</button>
          <button onClick={decrement}>-1</button>
          <HelloWorld>
          </HelloWorld>
        </div>
      )
    }
  }
</script>

<style lang="scss" scoped>

</style>
```

```vue
<script>
  export default {
    render() {
      return (
        <div>
          <h2>HelloWorld</h2>
          {this.$slots.default ? this.$slots.default(): <span>哈哈哈</span>}
        </div>
      )
    }
  }
</script>

<style scoped>

</style>
```

# 九、自定义指令

## 自定义指令

**Vue允许我们来自定义自己的指令**

- 注意：在Vue中，代码的复用和抽象主要还是通过组件；
- 通常在某些情况下，你需要对DOM元素进行底层操作，这个时候就会用到自定义指令；

- 自定义局部指令：组件中通过 directives 选项，只能在当前组件中使用；
- 自定义全局指令：app的 directive 方法，可以在任意组件中被使用；

**案例：当某个元素挂载完成后可以自定获取焦点**

- 实现方式一：如果我们使用默认的实现方式；

  ```vue
  <template>
    <div>
      <input type="text" ref="input" />
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from "vue";
  
  export default {
    setup() {
      const input = ref(null);
  
      onMounted(() => {
        input.value.focus();
      });
  
      return {
        input,
      };
    },
  };
  </script>
  
  <style scoped></style>
  
  ```

- 实现方式二：自定义一个 v-focus 的局部指令；

  - 这个自定义指令实现非常简单，我们只需要在组件选项中使用 **directives** 即可；
  - 它是一个对象，在对象中编写我们**自定义指令的名称**（注意：这里不需要加v-）；
  - 自定义指令有一个生命周期，是在组件挂载后调用的 **mounted**，我们可以在其中完成操作；

  ```vue
  <template>
    <div>
      <input type="text" v-focus>
    </div>
  </template>
  
  <script>
    export default {
      // 局部指令
      directives: {
        focus: {
          mounted(el, bindings, vnode, preVnode) {
            console.log("focus mounted");
            el.focus();
          }
        }
      }
    }
  </script>
  
  <style scoped>
  
  </style>
  ```

  

- 实现方式三：自定义一个 v-focus 的全局指令；

  > mian.js

  ```js
  app.directive("focus", {
    mounted(el, bindings, vnode, preVnode) {
      console.log(focus);
      el.focus();
    },
  })
  ```

## 指令的生命周期

**一个指令定义的对象，Vue提供了如下的几个钩子函数：**

- created：在绑定元素的 attribute 或事件监听器被应用之前调用；
-  beforeMount：当指令第一次绑定到元素并且在挂载父组件之前调用；
-  mounted：在绑定元素的父组件被挂载后调用；
-  beforeUpdate：在更新包含组件的 VNode 之前调用；
-  updated：在包含组件的 VNode 及其子组件的 VNode 更新后调用；
-  beforeUnmount：在卸载绑定元素的父组件之前调用；
-  unmounted：当指令与元素解除绑定且父组件已卸载时，只调用一次；

## 指令的参数和修饰符

如果我们指令需要接受一些参数或者修饰符应该如何操作呢？

- info是参数的名称；
- aaa-bbb是修饰符的名称；
- 后面是传入的具体的值；

在我们的生命周期中，我们可以通过 bindings 获取到对应的内容：

![image-20220227181137473](https://s2.loli.net/2022/02/27/6o1GDBj8WnCEbgL.png)

## 自定义指令练习

时间戳的处理需求：

> format-time.js

```js
import dayjs from 'dayjs';

export default function(app) {
  app.directive("format-time", {
    // 刚刚创建指令时，检测有没有传入格式，如果没有则使用默认格式
    created(el, bindings) {
      bindings.formatString = "YYYY-MM-DD HH:mm:ss";
      if (bindings.value) {
        bindings.formatString = bindings.value;
      }
    },
    // 通过dayjs处理时间戳并且挂载
    mounted(el, bindings) {
      const textContent = el.textContent;
      let timestamp = parseInt(textContent);
      if (textContent.length === 10) {
        timestamp = timestamp * 1000
      }
      el.textContent = dayjs(timestamp).format(bindings.formatString);
    }
  })
}
```

## Teleport

- 在组件化开发中，我们封装一个组件A，在另外一个组件B中使用：
  - 那么组件A中template的元素，会被挂载到组件B中template的某个位置；
  - 最终我们的应用程序会形成一颗DOM树结构；
-  但是某些情况下，我们希望组件不是挂载在这个组件树上的，可能是移动到Vue app之外的其他位置：
  - 比如移动到body元素上，或者我们有其他的div#app之外的元素上；
  - 这个时候我们就可以通过teleport来完成；
-  Teleport是什么呢？
  - 它是一个Vue提供的内置组件，类似于react的Portals；
  -  teleport翻译过来是心灵传输、远距离运输的意思；

teleport有两个属性：

- to：指定将其中的内容移动到的目标元素，可以使用选择器；
-  disabled：是否禁用 teleport 的功能；

![image-20220227182358829](https://s2.loli.net/2022/03/05/hmc1t8VM7uwrAIB.png)

也和组件结合使用：

![image-20220227182422090](https://s2.loli.net/2022/03/05/YBrQoibLWtmHedj.png)

当传入多个teleport应用到同一个目标上（to的值相同），那么这些目标会进行合并：

![image-20220227182446457](http://img.roydust.top/img/202210191612802.png)

## Vue插件

- 通常我们向Vue全局添加一些功能时，会采用插件的模式，它有两种编写方式：
  - 对象类型：一个对象，但是必须包含一个 **install** 的函数，该函数会在安装插件时执行；
  - 函数类型：**一个function**，这个函数会在安装插件时自动执行；
-  插件可以完成的功能没有限制，比如下面的几种都是可以的：
  - 添加全局方法或者 property，通过把它们添加到 **config.globalProperties** 上实现；
  - 添加**全局资源**：指令/过滤器/过渡等；
  - 通过全局 **mixin** 来添加一些组件选项；
  - 一个库，提供自己的 API，同时提供上面提到的一个或多个功能；

![image-20220227184404927](https://s2.loli.net/2022/03/05/EocjIDyAzL3KfgM.png)

# 十、Vue3源码

## DOM渲染

### 真实的DOM渲染

![image-20220305000934084](https://s2.loli.net/2022/03/05/IkJXSajDWTiCp5e.png)

### 虚拟DOM的优势

- 目前框架都会引入虚拟DOM来对真实的DOM进行抽象，这样做有很多的好处：
- 首先是可以对真实的元素节点进行抽象，抽象成VNode（虚拟节点），这样方便后续对其进行各种操作：
  - 因为对于直接操作DOM来说是有很多的限制的，比如diff、clone等等，但是使用JavaScript编程语言来操作这些，就变得非常的简单；
  - 我们可以使用JavaScript来表达非常多的逻辑，而对于DOM本身来说是非常不方便的；
- 其次是方便实现跨平台，包括你可以将VNode节点渲染成任意你想要的节点
  - 如渲染在canvas、WebGL、SSR、Native（iOS、Android）上；
  - 并且Vue允许你开发属于自己的渲染器（renderer），在其他的平台上渲染；

### 虚拟DOM的渲染过程

![image-20220305001042700](https://s2.loli.net/2022/03/05/unavWc4iUHV19AP.png)

## Vue三大核心系统

Vue的源码包含三大核心：

- Compiler模块：编译模板系统；
- Runtime模块：也可以称之为Renderer模块，真正渲染的模块；
- Reactivity模块：响应式系统；

![image-20220305001131068](https://s2.loli.net/2022/03/05/kDvbRtNuC5as1hg.png)

三个系统之间如何协同工作呢：

![image-20220305001152317](https://s2.loli.net/2022/03/05/Ko268IrOSV49dEz.png)

## 实现Mini-Vue

这里我们实现一个简洁版的Mini-Vue框架，该Vue包括三个模块：

- 渲染系统模块；
- 可响应式系统模块；
- 应用程序入口模块；

### 渲染系统实现

渲染系统，该模块主要包含三个功能：

- 功能一：h函数，用于返回一个VNode对象；
- 功能二：mount函数，用于将VNode挂载到DOM上；
- 功能三：patch函数，用于对两个VNode进行对比，决定如何处理新的VNode；

#### h函数 – 生成VNode

h函数的实现：

- 直接返回一个VNode对象即可

```js
const h = (tag, props, children) => {
  // vnode -> javascript对象 -> {}
  return {
    tag,
    props,
    children
  }
}
```

#### Mount函数 – 挂载VNode

mount函数的实现：

- 第一步：根据tag，创建HTML元素，并且存储到vnode的el中；
- 第二步：处理props属性
  - 如果以on开头，那么监听事件；
  - 普通属性直接通过 setAttribute 添加即可；
- 第三步：处理子节点
  - 如果是字符串节点，那么直接设置textContent；
  - 如果是数组节点，那么遍历调用 mount 函数；

```js
const mount = (vnode, container) => {
  // vnode -> element
  // 1.创建出真实的原生, 并且在vnode上保留el
  const el = vnode.el = document.createElement(vnode.tag);

  // 2.处理props
  if (vnode.props) {
    for (const key in vnode.props) {
      const value = vnode.props[key];

      if (key.startsWith("on")) { // 对事件监听的判断
        el.addEventListener(key.slice(2).toLowerCase(), value)
      } else {
        el.setAttribute(key, value);
      }
    }
  }

  // 3.处理children
  if (vnode.children) {
    if (typeof vnode.children === "string") {
      el.textContent = vnode.children;
    } else {
      vnode.children.forEach(item => {
        mount(item, el);
      })
    }
  }

  // 4.将el挂载到container上
  container.appendChild(el);
}
```

#### Patch函数 – 对比两个VNode

- patch函数的实现，分为两种情况
-  n1和n2是不同类型的节点：
  - 找到n1的el父节点，删除原来的n1节点的el；
  - 挂载n2节点到n1的el父节点上；
-  n1和n2节点是相同的节点：
  - 处理props的情况
    - 先将新节点的props全部挂载到el上；
    - 判断旧节点的props是否不需要在新节点上，如果不需要，那么删除对应的属性；
  -  处理children的情况
    - 如果新节点是一个字符串类型，那么直接调用 el.textContent = newChildren；
    -  如果新节点不同一个字符串类型：
      - 旧节点是一个字符串类型
        - 将el的textContent设置为空字符串；
        - 就节点是一个字符串类型，那么直接遍历新节点，挂载到el上；
      -  旧节点也是一个数组类型
        -  取出数组的最小长度；
        -  遍历所有的节点，新节点和旧节点进行path操作；
        -  如果新节点的length更长，那么剩余的新节点进行挂载操作；
        -  如果旧节点的length更长，那么剩余的旧节点进行卸载操作；

```js
const patch = (n1, n2) => {
  if (n1.tag !== n2.tag) {
    const n1ElParent = n1.el.parentElement;
    n1ElParent.removeChild(n1.el);
    mount(n2, n1ElParent);
  } else {
    // 1.取出element对象, 并且在n2中进行保存
    const el = n2.el = n1.el;

    // 2.处理props
    const oldProps = n1.props || {};
    const newProps = n2.props || {};
    // 2.1.获取所有的newProps添加到el
    for (const key in newProps) {
      const oldValue = oldProps[key];
      const newValue = newProps[key];
      if (newValue !== oldValue) {
        if (key.startsWith("on")) { // 对事件监听的判断
          el.addEventListener(key.slice(2).toLowerCase(), newValue)
        } else {
          el.setAttribute(key, newValue);
        }
      }
    }

    // 2.2.删除旧的props
    for (const key in oldProps) {
      if (key.startsWith("on")) { // 对事件监听的判断
        const value = oldProps[key];
        el.removeEventListener(key.slice(2).toLowerCase(), value)
      } 
      if (!(key in newProps)) {
        el.removeAttribute(key);
      }
    }

    // 3.处理children
    const oldChildren = n1.children || [];
    const newChidlren = n2.children || [];

    if (typeof newChidlren === "string") { // 情况一: newChildren本身是一个string
      // 边界情况 (edge case)
      if (typeof oldChildren === "string") {
        if (newChidlren !== oldChildren) {
          el.textContent = newChidlren
        }
      } else {
        el.innerHTML = newChidlren;
      }
    } else { // 情况二: newChildren本身是一个数组
      if (typeof oldChildren === "string") {
        el.innerHTML = "";
        newChidlren.forEach(item => {
          mount(item, el);
        })
      } else {
        // oldChildren: [v1, v2, v3, v8, v9]
        // newChildren: [v1, v5, v6]
        // 1.前面有相同节点的原生进行patch操作
        const commonLength = Math.min(oldChildren.length, newChidlren.length);
        for (let i = 0; i < commonLength; i++) {
          patch(oldChildren[i], newChidlren[i]);
        }

        // 2.newChildren.length > oldChildren.length
        if (newChidlren.length > oldChildren.length) {
          newChidlren.slice(oldChildren.length).forEach(item => {
            mount(item, el);
          })
        }

        // 3.newChildren.length < oldChildren.length
        if (newChidlren.length < oldChildren.length) {
          oldChildren.slice(newChidlren.length).forEach(item => {
            el.removeChild(item.el);
          })
        }
      }
    }
  }
}
```

### 可响应式系统模块

#### 依赖收集系统

![image-20220305002913496](https://s2.loli.net/2022/03/05/BgHfjlxR6ydeOpS.png)



响应式系统Vue2实现

```js
const targetMap = new WeakMap();

function getDep(target, key) {
  let depsMap = targetMap.get(target);
  if (!depsMap) {
    depsMap = new Map();
    targetMap.set(target, depsMap);
  }

  let dep = depsMap.get(key);
  if (!dep) {
    dep = new Dep();
    depsMap.set(key, dep)
  }
  return dep;
}

// vue2
function reactive(raw) {
  Object.keys(raw).forEach(key => {

    const dep = getDep(raw, key);
    let value = raw[key];
    Object.defineProperty(raw, key, {
      get() {
        dep.depend();
        return value;
      },
      set(newValue) {
        if (value !== newValue) {
          value = newValue;
          dep.notify();
        }

      }
    })
  })
  return raw;
}
```

响应式系统Vue3实现

```js
// vue3
function reactive(raw) {
  return new Proxy(raw, {
    get(target, key) {
      const dep = getDep(target, key);
      dep.depend();
      return target[key];
    },
    set(target, key, newValue) {
      const dep = getDep(target, key);
      target[key] = newValue;
      dep.notify();
    }
  });
}
```

#### 完整响应式代码

```js
class Dep {
  constructor() {
    this.subscribers = new Set();
  }

  depend() {
    if (activeEffect) {
      this.subscribers.add(activeEffect);
    }
  }

  notify() {
    this.subscribers.forEach(effect => {
      effect();
    })
  }
}

let activeEffect = null;
function watchEffect(effect) {
  activeEffect = effect;
  effect();
  activeEffect = null;
}


// Map({key: value}): key是一个字符串
// WeakMap({key(对象): value}): key是一个对象, 弱引用
const targetMap = new WeakMap();
function getDep(target, key) {
  // 1.根据对象(target)取出对应的Map对象
  let depsMap = targetMap.get(target);
  if (!depsMap) {
    depsMap = new Map();
    targetMap.set(target, depsMap);
  }

  // 2.取出具体的dep对象
  let dep = depsMap.get(key);
  if (!dep) {
    dep = new Dep();
    depsMap.set(key, dep);
  }
  return dep;
}


// vue3对raw进行数据劫持
function reactive(raw) {
  return new Proxy(raw, {
    get(target, key) {
      const dep = getDep(target, key);
      dep.depend();
      return target[key];
    },
    set(target, key, newValue) {
      const dep = getDep(target, key);
      target[key] = newValue;
      dep.notify();
    }
  })
}
```

### 应用程序入口模块

这样我们就知道了，从框架的层面来说，我们需要有两部分内容：

- createApp用于创建一个app对象；
- 该app对象有一个mount方法，可以将根组件挂载到某一个dom元素上；

```js
function createApp(rootComponent) {
  return {
    mount(selector) {
      const container = document.querySelector(selector);
      let isMounted = false;
      let oldVNode = null;

      watchEffect(function () {
        if (!isMounted) {
          oldVNode = rootComponent.render(),
            mount(oldVNode, container);
          isMounted = true;
        } else {
          const newVNode = rootComponent.render();
          patch(oldVNode, newVNode);
          oldVNode = newVNode
        }
      })
    },
  }
}
```



## App组件的挂载和渲染过程

### createApp

![image-20220319152829913](https://s2.loli.net/2022/03/19/MlreJKOv3EjWLHB.png)

![App组件的挂载和渲染过程](https://s2.loli.net/2022/03/15/lUjvhOi3QMXHarg.png)

### 挂载根组件

![image-20220319152955171](https://s2.loli.net/2022/03/19/fY4QdmqKksGAcev.png)

![image-20220316001927979](https://s2.loli.net/2022/03/16/zGkoxvU7Rqawlb9.png)

### 组件化的初始化

![image-20220319153035862](https://s2.loli.net/2022/03/19/ZRPu5N6gow3mkxL.png)

![image-20220315230836658](https://s2.loli.net/2022/03/15/j3xOWHEYvGJ5ITP.png)

### Compile过程

![image-20220319153113640](https://s2.loli.net/2022/03/19/Uvbir1qfshczaQM.png)

### Block Tree分析

常量值会定义在render外面，因为他无需更新，其他变量都在render里面，当发生改变时，再进行petch，再挂载新的属性

![image-20220319153137943](https://s2.loli.net/2022/03/19/KCOB87j6oUakNvL.png)

### 生命周期回调

![image-20220319153549847](https://s2.loli.net/2022/03/19/9NUHXDpLnjuqh81.png)

### template中数据的使用顺序

![image-20220319153526376](https://s2.loli.net/2022/03/19/htdYam289VcWTvp.png)

# 十一、Vue-Router

## 认识路由

- 路由其实是网络工程中的一个术语：
- 在架构一个网络时，非常重要的两个设备就是路由器和交换机。
- 当然，目前在我们生活中路由器也是越来越被大家所熟知，因为我们生活中都会用到路由器：
- 事实上，路由器主要维护的是一个映射表；
- 映射表会决定数据的流向；

路由的概念在软件工程中出现，最早是在后端路由中实现的，原因是web的发展主要经历了这样一些阶段：

- 后端路由阶段；
- 前后端分离阶段；
- 单页面富应用（SPA）；

**后端路由阶段**

- 早期的网站开发整个HTML页面是由服务器来渲染的.
  - 服务器直接生产渲染好对应的HTML页面, 返回给客户端进行展示.
-  但是, 一个网站, 这么多页面服务器如何处理呢?
  - 一个页面有自己对应的网址, 也就是URL；
  - URL会发送到服务器, 服务器会通过正则对该URL进行匹配, 并且最后交给一个Controller进行处理；
  - Controller进行各种处理, 最终生成HTML或者数据, 返回给前端.
-  上面的这种操作, 就是后端路由：
  - 当我们页面中需要请求不同的路径内容时, 交给服务器来进行处理, 服务器渲染好整个页面, 并且将页面返回给客户端.
  - 这种情况下渲染好的页面, 不需要单独加载任何的js和css, 可以直接交给浏览器展示, 这样也有利于SEO的优化.
-  后端路由的缺点:
  - 一种情况是整个页面的模块由后端人员来编写和维护的；
  - 另一种情况是前端开发人员如果要开发页面, 需要通过PHP和Java等语言来编写页面代码；
  - 而且通常情况下HTML代码和数据以及对应的逻辑会混在一起, 编写和维护都是非常糟糕的事情；

**前后端分离阶段**

- 前端渲染的理解：
  - 每次请求涉及到的静态资源都会从静态资源服务器获取，这些资源包括HTML+CSS+JS，然后在前端对这些请求回来的资源进行渲染；
  - 需要注意的是，客户端的每一次请求，都会从静态资源服务器请求文件；
  - 同时可以看到，和之前的后端路由不同，这时后端只是负责提供API了；
-  前后端分离阶段：
  - 随着Ajax的出现, 有了前后端分离的开发模式；
  - 后端只提供API来返回数据，前端通过Ajax获取数据，并且可以通过JavaScript将数据渲染到页面中；
  - 这样做最大的优点就是前后端责任的清晰，后端专注于数据上，前端专注于交互和可视化上；
  - 并且当移动端(iOS/Android)出现后，后端不需要进行任何处理，依然使用之前的一套API即可；
  - 目前比较少的网站采用这种模式开发（jQuery开发模式）；

### URL的hash

- 前端路由是如何做到URL和内容进行映射呢？监听URL的改变。
- URL的hash
  - URL的hash也就是锚点(#), 本质上是改变window.location的href属性；
  - 我们可以通过直接赋值location.hash来改变href, 但是页面不发生刷新

![image-20220321002721607](https://s2.loli.net/2022/03/21/2jW8GYReaQIvoUh.png)

### HTML5的History

- history接口是HTML5新增的, 它有l六种模式改变URL而不刷新页面：
  - replaceState：替换原来的路径；
  - pushState：使用新的路径；
  - popState：路径的回退；
  - go：向前或向后改变路径；
  - forward：向前改变路径；
  - back：向后改变路径；

![image-20220321002801673](https://s2.loli.net/2022/03/21/17OQP8uxfMcgoUk.png)

## vue-router使用

使用vue-router的步骤:

- 第一步：创建路由组件的组件；
- 第二步：配置路由映射: 组件和路径映射关系的routes数组；
- 第三步：通过createRouter创建路由对象，并且传入routes和history模式；
- 第四步：使用路由: 通过< router-link >和< router-view >；

![image-20220321003549448](https://s2.loli.net/2022/03/21/nfoNiukYd6L2K7w.png)

### redirect重定向

如何可以让路径默认跳到到首页, 并且<router-view>渲染首页组件呢?

```js
{
    path: "/",
    redirect: "/Home"
  },
```

### 路由懒加载

- 当打包构建应用时，JavaScript 包会变得非常大，影响页面加载：
  - 如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就会更加高效；
  - 也可以提高首屏的渲染效率；
-  其实这里还是我们前面讲到过的webpack的分包知识，而Vue Router默认就支持动态来导入组件：
  - 这是因为component可以传入一个组件，也可以接收一个函数，该函数 需要放回一个Promise；
  - 而import函数就是返回一个Promise；

```js
  {
    path: "/About",
    component: () => {
      return import("../view/About.vue");
    }
  }
```

### 路由携带参数

```js
  { 
    path: "/home", 
    name: "home",
    component: () => import(/* webpackChunkName: "home-chunk" */"../pages/Home.vue"),
    meta: {		//meta 可以携带参数
      name: "why",
      age: 18,
      height: 1.88
    }
  }      
```



## router-link

**router-link事实上有很多属性可以配置：**

- to属性：
  - 是一个字符串，或者是一个对象
- replace属性：
  - 设置 replace 属性的话，当点击时，会调用 router.replace()，而不是 router.push()；
- active-class属性：
  - 设置激活a元素后应用的class，默认是router-link-active
- exact-active-class属性：
  - 链接精准激活时，应用于渲染的 <a> 的 class，默认是router-link-exact-active；

## 动态路由基本匹配

- 很多时候我们需要将给定匹配模式的路由映射到同一个组件：
  - 例如，我们可能有一个 User 组件，它应该对所有用户进行渲染，但是用户的ID是不同的；
  - 在Vue Router中，我们可以在路径中使用一个动态字段来实现，我们称之为 路径参数

```js
  {
    path: "/User/:username",
    component: () => import("../view/User.vue")
  },
```

- 在router-link中进行如下跳转：

```vue
  <router-link to="/User/why">user</router-link>
```

### 获取动态路由的值

那么在User中如何获取到对应的值呢？

- 在template中，直接通过 $route.params获取值；
- 在created中，通过 this.$route.params获取值；
- 在setup中，我们要使用 vue-router库给我们提供的一个hook useRoute；
  - 该Hook会返回一个Route对象，对象中保存着当前路由相关的值；

```vue
<template>
  <h2>User:{{ $route.params.username }}</h2>
</template>

<script>
import { useRoute } from "vue-router";
export default {
  setup() {
    const route = useRoute();
    console.log(route.params.username);
  },
};
</script>

<style></style>
```

### 匹配多个参数

![image-20220321160026077](https://s2.loli.net/2022/03/21/FzRjimU3n4VatrD.png)

## NotFound没有匹配到路由

- 对于哪些没有匹配到的路由，我们通常会匹配到固定的某个页面
  - 比如NotFound的错误页面中，这个时候我们可编写一个动态路由用于匹配所有的页面；

```js
  {
    path: "/:pathMatch(.*)",
    component: () => import("../view/404.vue")
  }
```

- 我们可以通过 $route.params.pathMatch获取到传入的参数：

```vue
<h1>404:{{ $route.params.pathMatch }}</h1>
```

- 这里还有另外一种写法：
  - 注意：我在/:pathMatch(.*)后面又加了一个 *；

```js
  {
    path: "/:pathMatch(.*)*",
    component: () => import("../view/404.vue")
  }
```

- 它们的区别在于解析的时候，是否解析 /：

![image-20220321160418381](https://s2.loli.net/2022/03/21/2RMhzynWHJqcu35.png)

## 路由的嵌套Children

什么是路由的嵌套呢？

- 目前我们匹配的Home、About、User等都属于底层路由，我们在它们之间可以来回进行切换；
- 但是呢，我们Home页面本身，也可能会在多个组件之间来回切换：
  - 比如Home中包括Product、Message，它们可以在Home内部来回切换；
- 这个时候我们就需要使用嵌套路由，在Home中也使用 router-view 来占位之后需要渲染的组件；

```js
  {
    path: "/Home",
    component: () => {
      return import("../view/Home.vue");
    },
    children: [{
        path: "message",
        component: () => import("../view/HomeMessage.vue")
      },
      {
        path: "shops",
        component: () => import("../view/HomeShops.vue")
      }
    ]
  },
```

## 代码的页面跳转

- 有时候我们希望通过代码来完成页面的跳转，比如点击的是一个按钮：

  ![image-20220321160842770](https://s2.loli.net/2022/03/21/Hqw6XG9mxfJz4ty.png)

- 当然，我们也可以传入一个对象：

  ![image-20220321160901793](https://s2.loli.net/2022/03/21/XLg6GiohyAF1PUN.png)

- 如果是在setup中编写的代码，那么我们可以通过 useRouter 来获取：

  ![image-20220321160909933](https://s2.loli.net/2022/03/21/F5SAUmPrpaigo7N.png)

### query方式的参数

- 我们也可以通过query的方式来传递参数：

  ![image-20220321161009386](https://s2.loli.net/2022/03/21/o5Xxhp6RIQBdCnT.png)

- 在界面中通过 $route.query 来获取参数：

  ![image-20220321161045509](https://s2.loli.net/2022/03/21/JM9DgrK2eAsySX8.png)

## 页面的前进后退

**router的go方法：**

![image-20220321161150675](https://s2.loli.net/2022/03/21/yLn8i4EszpDmCQX.png)

- router也有back：
  - 通过调用 history.back() 回溯历史。相当于 router.go(-1)；
-  router也有forward：
  - 通过调用 history.forward() 在历史中前进。相当于 router.go(1)；

## 路由中的v-slot

### router-link的v-slot

- 在vue-router3.x的时候，router-link有一个tag属性，可以决定router-link到底渲染成什么元素：
  - 但是在vue-router4.x开始，该属性被移除了；
  - 而给我们提供了更加具有灵活性的v-slot的方式来定制渲染的内容；
-  v-slot如何使用呢？
  - 首先，我们需要使用custom表示我们整个元素要自定义
    - 如果不写，那么自定义的内容会被包裹在一个 a 元素中；
  -  其次，我们使用v-slot来作用域插槽来获取内部传给我们的值：
    - href：解析后的 URL；
    -  route：解析后的规范化的route对象；
    -  navigate：触发导航的函数；
    -  isActive：是否匹配的状态；
    -  isExactActive：是否是精准匹配的状态；

```vue
  <router-link
    to="/About"
    v-slot="{ href, route, navigate, isActive, isExactActive }"
  >
    <p @click="navigate">转跳</p>
    <div>
      <p>href:{{ href }}</p>
      <p>route:{{ route }}</p>
      <p>isActive:{{ isActive }}</p>
      <p>isExactActive :{{ isExactActive }}</p>
    </div>
  </router-link>
```

### router-view的v-slot

可以用于 <transition> 和 <keep-alive> 组件来包裹你的路由组件：

- Component：要渲染的组件；
- route：解析出的标准化路由对象；

```vue
  <router-view v-slot="{ Component }">
    <transition name="why">
      <keep-alive>
        <component :is="Component"></component>
      </keep-alive>
    </transition>
  </router-view>
```

css:

```css
.why-enter-from,
.why-leave-to {
  opacity: 0;
}
.why-enter-active,
.why- leave-active {
  transition: opacity 1s ease-in;
}
```

##  动态添加路由

- 某些情况下我们可能需要动态的来添加路由：
  - 比如根据用户不同的权限，注册不同的路由；
  - 这个时候我们可以使用一个方法 addRoute；
-  如果我们是为route添加一个children路由，那么可以传入对应的name：

```js
// 创建一个路由对象router
const router = createRouter({
  routes,
  history: createWebHistory()
})

// 动态添加路由
const categoryRoute = {
  path: "/category",
  component: () => import("../pages/Category.vue")
}

// 添加顶级路由对象(重点)
router.addRoute(categoryRoute);

// 添加二级路由对象
router.addRoute("home", {
  path: "moment",
  component: () => import("../pages/HomeMoment.vue")
})
```

![image-20220320165626374](https://s2.loli.net/2022/03/20/nmEe3PMo4YjR8aS.png)

### 动态删除路由

删除路由有以下三种方式：

- 方式一：添加一个name相同的路由；
- 方式二：通过removeRoute方法，传入路由的名称；
- 方式三：通过addRoute方法的返回值回调；

![image-20220321215332978](https://s2.loli.net/2022/03/21/PwbGIAmDzN4YUR3.png)

路由的其他方法补充：

- router.hasRoute()：检查路由是否存在。
- router.getRoutes()：获取一个包含所有路由记录的数组

## 路由导航守卫

- vue-router 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。
-  全局的前置守卫beforeEach是在导航触发时会被回调的：
-  它有两个参数：
  - to：即将进入的路由Route对象；
  - from：即将离开的路由Route对象；
-  它有返回值：
  - false：取消当前导航；
  - 不返回或者undefined：进行默认导航；
  - 返回一个路由地址：
    - 可以是一个string类型的路径；
    - 可以是一个对象，对象中包含path、query、params等信息；
-  可选的第三个参数：next (不推荐使用)
  - 在Vue2中我们是通过next函数来决定如何进行跳转的；
  - 但是在Vue3中我们是通过返回值来控制的，不再推荐使用next函数，这是因为开发中很容易调用多次next；

```js
// 导航守卫beforeEach
let counter = 0;
// to: Route对象, 即将跳转到的Route对象
// from: Route对象, 
/**
 * 返回值问题:
 *    1.false: 不进行导航
 *    2.undefined或者不写返回值: 进行默认导航
 *    3.字符串: 路径, 跳转到对应的路径中
 *    4.对象: 类似于 router.push({path: "/login", query: ....})
 */
router.beforeEach((to, from) => {
  console.log(`进行了${++counter}路由跳转`)
  // if (to.path.indexOf("/home") !== -1) {
  //   return "/login"
  // }
  if (to.path !== "/login") {
    const token = window.localStorage.getItem("token");
    if (!token) {
      return "/login"
    }
  }
})
```

**Vue3代码中使用：**

![image-20220321215755792](https://s2.loli.net/2022/03/21/AUdVjRxQNSBqoYG.png)

**完整的导航解析流程**：

-  导航被触发。
-  在失活的组件里调用 beforeRouteLeave 守卫。
-  调用全局的 beforeEach 守卫。
-  在重用的组件里调用 beforeRouteUpdate 守卫(2.2+)。
-  在路由配置里调用 beforeEnter。
-  解析异步路由组件。
-  在被激活的组件里调用 beforeRouteEnter。
-  调用全局的 beforeResolve 守卫(2.5+)。
-  导航被确认。
-  调用全局的 afterEach 钩子。
-  触发 DOM 更新。
-  调用 beforeRouteEnter 守卫中传给 next 的回调函数，创建好的组件实例会作为回调函数的参数传入。

## Vue3setup中Router和Route获取及使用

### useRouter

```JS
   const router2 = useRouter();
      
    // 下面提供了router对应的方法使用大全
    // ------------------------------------------------------
    // router1.addRoute(parentOrRoute, route)
    // router1.afterEach(回调函数)
    // router1.back() 等价于 go(-1)
    // router1.beforeEach(回调函数)
    // router1.beforeResolve(回调函数)
    // router1.currentRoute 获取当前路由：如： {_rawValue: {…}, _shallow: true, __v_isRef: true, _value: {…}}
    // router1.forward() 等价于 go(1)
    // router1.getRoutes: ƒ getRoutes()
    // router1.go(delta) 等价于 routerHistory.go(delta) 跳到指定历史记录
    // router1.hasRoute(name) 判断是否有对应的路由
    // router1.isReady() 判断路由是否准备跳转
    // router1.onError(回调函数) 当发生错误的时候执行的
    // router1.options 获取所有路由信息 {history: {…}, routes: Array(5)}
    // router1.push(to) 跳转到指定路由对应的页面，有历史记录
    // router1.removeRoute(name) 动态的删除某个路由
    // router1.replace(to) 直接跳转到指定路由页面，没有历史记录
    // router1.resolve(rawLocation, currentLocation)  可以自定义跳转参数的方法
```

### useRoute

```js
const route2 = useRoute();

    // 下面提供了route对应的属性使用大全
    // ------------------------------------------------------
    // fullPath: "/user"  完整路由路径
    // hash: "" 锚点部分
    // href: "/user"  跳转来的时候的路径
    // matched: [{…}]   路由匹配日规则数组
    // meta: {0: "istabbar"}  路由附加的元数据
    // name: "个人中心" 路由的名称
    // params: {}   路由跳转时带过来的附加参数，如果是对象需要转换成JSON格式
    // path: "/user"  编码 URL 的 pathname 部分，与路由地址有关
    // query: {}   地址附带的参数
    // redirectedFrom: undefined  重定向跳转过来之前的地址，如果没有重定向，则为 undefined。
```

# 十二、Vuex

## 状态管理

- 在开发中，我们会的应用程序需要处理各种各样的数据，这些数据需要保存在我们应用程序中的某一个位置，对于这些数据的管理我们就称之为是 **状态管理**。
- 在前面我们是如何管理自己的状态呢？
  - 在Vue开发中，我们使用组件化的开发方式；
  - 而在组件中我们定义data或者在setup中返回使用的数据，这些数据我们称之为state；
  - 在模块template中我们可以使用这些数据，模块最终会被渲染成DOM，我们称之为View；
  - 在模块中我们会产生一些行为事件，处理这些行为事件时，有可能会修改state，这些行为事件我们称之为actions；

- 管理不断变化的state本身是非常困难的：
  - 状态之间相互会存在依赖，一个状态的变化会引起另一个状态的变化，View页面也有可能会引起状态的变化；
  - 当应用程序复杂时，state在什么时候，因为什么原因而发生了变化，发生了怎么样的变化，会变得非常难以控制和追踪；
-  因此，我们是否可以考虑将组件的内部状态抽离出来，以一个全局单例的方式来管理呢？
  - 在这种模式下，我们的组件树构成了一个巨大的 “试图View”；
  - 不管在树的哪个位置，任何组件都能获取状态或者触发行为；
  - 通过定义和隔离状态管理中的各个概念，并通过强制性的规则来维护视图和状态间的独立性，我们的代码边会变得更加结构化和易于维护、跟踪；

![image-20220330144241300](https://s2.loli.net/2022/03/30/ja7y2KqRfQ9Xnr8.png)

### 单一状态树

- Vuex 使用单一状态树：
  - 用一个对象就包含了全部的应用层级状；
  - 采用的是SSOT，Single Source of Truth，也可以翻译成单一数据源；
  - 这也意味着，每个应用将仅仅包含一个 store 实例；
  - 单状态树和模块化并不冲突，后面我们会讲到module的概念；
-  单一状态树的优势：
  - 如果你的状态信息是保存到多个Store对象中的，那么之后的管理和维护等等都会变得特别困难；
  - 所以Vuex也使用了单一状态树来管理应用层级的全部状态；
  - 单一状态树能够让我们最直接的方式找到某个状态的片段，而且在之后的维护和调试过程中，也可以非常方便的管理和维护；



## store的基本使用

### 创建store

- 每一个Vuex应用的核心就是store（仓库）：
  - store本质上是一个容器，它包含着你的应用中大部分的状态（state）；
-  **Vuex和单纯的全局对象有什么区别呢？**
  - 第一：Vuex的状态存储是响应式的
    - 当Vue组件从store中读取状态的时候，若store中的状态发生变化，那么相应的组件也会被更新；
  -  第二：你不能直接改变store中的状态
    - 改变store中的状态的唯一途径就显示提交 (commit) mutation；
    - 这样使得我们可以方便的跟踪每一个状态的变化，从而让我们能够通过一些工具帮助我们更好的管理应用的状态；
-  使用步骤：
  - 创建Store对象；
  - 在app中通过插件安装；

### 在组件中使用store

> template

```vue
   <h2>Home:{{ $store.state.counter }}</h2>
```

> Vue2 computed 计算属性

```js
import { mapState } from 'vuex'

  export default {
    computed: {
      fullName() {
        return "Kobe Bryant"
      },
      // 其他的计算属性, 从state获取
      // ...mapState(["counter", "name", "age", "height"])
      ...mapState({
        sCounter: state => state.counter,
        sName: state => state.name
      })
    }
  }
```

> Vue3 setup

Vuex并没有提供非常方便的使用mapState的方式，这里我们进行了一个函数的封装：

```js
  import { mapState, useStore } from 'vuex'
  import { computed } from 'vue'

  export default {
    setup() {
      const store = useStore()
      const sCounter = computed(() => store.state.counter)
      // const sName = computed(() => store.state.name)
      // const sAge = computed(() => store.state.age)

      const storeStateFns = mapState(["counter", "name", "age", "height"])

      // {name: function, age: function, height: function}
      // {name: ref, age: ref, height: ref}
      const storeState = {}
      
      //这里将storeStateFns的每一个函数取出来根据key来解析成一个ref对象
      Object.keys(storeStateFns).forEach(fnKey => {
        const fn = storeStateFns[fnKey].bind({$store: store})
        storeState[fnKey] = computed(fn)
      })

      return {
        sCounter,
        //这里再将一个storeState这个ref对象里的键值对解析出来
        ...storeState
      }
    }
  }
```

## getters的基本使用

Vuex中某些属性我们可能需要经过变化后来使用，这个时候可以使用getters(相当于**computed**)

### getters第多个参数

```js
  getters: {
    doubleHomeCounter(state , getters, rootState, rootGetters) {
        //state 当前的模块的状态库
        //getters 当前的模块的其他getters
        //rootState rootGetters 根组件的state和getters
      return state.homeCounter * 2
    },
    otherGetter(state) {
      return 100
    }
  },
```

### getters的返回函数

> getters中的函数本身，可以返回一个函数，那么在使用的地方相当于可以调用这个函数：

![image-20220330152538651](https://s2.loli.net/2022/03/30/abZLCjhny5D23XM.png)

### mapGetters的辅助函数

> Vue2

```vue
<template>
  <div>
    <h2>总价值: {{ $store.getters.totalPrice }}</h2>
    <h2>总价值: {{ $store.getters.totalPriceCountGreaterN(1) }}</h2>
    <hr>
    <h2>{{ sNameInfo }}</h2>
    <h2>{{ sAgeInfo }}</h2>
    <hr>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'

  export default {
    computed: {
      ...mapGetters(["nameInfo", "ageInfo", "heightInfo"]),
      ...mapGetters({
        sNameInfo: "nameInfo",
        sAgeInfo: "ageInfo"
      })
    },
  }
</script>

<style scoped>

</style>
```

> Vue3 setup

```vue
<template>
  <div>
    <h2>总价值: {{ $store.getters.totalPrice }}</h2>
    <h2>总价值: {{ $store.getters.totalPriceCountGreaterN(1) }}</h2>
    <hr>
    <h2>{{ nameInfo }}</h2>
    <h2>{{ ageInfo }}</h2>
    <h2>{{ heightInfo }}</h2>
    <hr>
  </div>
</template>
<script>
  import { useGetters } from '../hooks/useGetters'
  export default {
    setup() {
      const storeGetters = useGetters(["nameInfo", "ageInfo", "heightInfo"])
      return {
        ...storeGetters
      }
    }
  }
</script>
```

## Mutation基本使用

- 更改 Vuex 的 store 中的状态的唯一方法是提交 mutation：

```js
  mutations: {
    increment(state) {
      state.homeCounter++
    }
  },
```

- 很多时候我们在提交mutation的时候，会携带一些数据，这个时候我们可以使用参数：

![image-20220330222438791](https://s2.loli.net/2022/03/30/DGmZ3XlNsuTnBrF.png)

### **Mutation常量类型**

先在外定义一个常量：mutation-type.js

```js
export const INCREMENT_N = "increment_n"
```

定义mutation

```js
    [INCREMENT_N](state, payload) {
      console.log(payload);
      state.counter += payload.n
    },
```

提交mutation

```js
      addTen() {
        // this.$store.commit('incrementN', 10)
        // this.$store.commit('incrementN', {n: 10, name: "why", age: 18})
        // 另外一种提交风格
        this.$store.commit({
          type: INCREMENT_N,
          n: 10, 
          name: "why", 
          age: 18
        })
      }
```

### **mapMutations辅助函数**

> Vue2

```JS
    methods: {
      ...mapMutations(["increment", "decrement", INCREMENT_N]),
      ...mapMutations({
        add: "increment"
      })
    },
```

> Vue3

```js
    setup() {
      const storeMutations = mapMutations(["increment", "decrement", INCREMENT_N])

      return {
        ...storeMutations
      }
    }
```

### **mutation重要原则**

一条重要的原则就是要记住 **mutation 必须是同步函数**

- 这是因为devtool工具会记录mutation的日记； 
- 每一条mutation被记录，devtools都需要捕捉到前一状态和后一状态的快照； 
- 但是在mutation中执行异步操作，就无法追踪到数据的变化；
- 所以Vuex的重要原则中要求 mutation必须是同步函数；

## **actions的基本使用**

- Action类似于mutation，不同在于：
  - Action提交的是mutation，而不是直接变更状态；
  - Action可以包含任意异步操作； 

- 这里有一个非常重要的参数context： 
  - context是一个和store实例均有相同方法和属性的context对象； 
  - 所以我们可以从其中获取到commit方法来提交一个mutation，或者通过 context.state 和 context.getters 来获取 state 和 getters； 

```js
  actions: {
    // 放函数
    // 1.参数问题
    incrementAction(context, payload) {
      console.log(payload)
      setTimeout(() => {
        context.commit('increment')
      }, 1000);
    },
    // 2.context的其他属性
    decrementAction({ commit, dispatch, state, rootState, getters, rootGetters }) {
      commit("decrement")
    },
  }
```

### **actions的分发操作**

如何使用action呢？进行action的分发：	

```js
      increment() {
        this.$store.dispatch("incrementAction", {count: 100})
      },
      decrement() {
        // 3.派发风格(对象类型)
        this.$store.dispatch({
          type: "decrementAction"
        })
      }
```

### **actions的辅助函数**

action也有对应的辅助函数：

- 对象类型的写法

```js
    methods: {
      ...mapActions(["incrementAction", "decrementAction"]),
      ...mapActions({
        add: "incrementAction",
        sub: "decrementAction"
      })
    },
```

- 数组类型的写法

```js
    setup() {
      const actions = mapActions(["incrementAction", "decrementAction"])
      const actions2 = mapActions({
        add: "incrementAction",
        sub: "decrementAction"
      })

      return {
        ...actions,
        ...actions2
      }
    }
```

### **actions的异步操作（重点）**

Action 通常是异步的，那么如何知道 action 什么时候结束呢？

- 我们可以通过让action返回Promise，在Promise的then中来处理完成后的操作；

```js
  actions: {
  getHomeMultidata(context) {
      return new Promise((resolve, reject) => {
        axios.get("http://123.207.32.32:8000/home/multidata").then(res => {
          context.commit("addBannerData", res.data.data.banner.list)
          resolve({name: "coderwhy", age: 18})
        }).catch(err => {
          reject(err)
        })
      })
    }
  }
```

> Vue中

```js
      onMounted(() => {
        const promise = store.dispatch("getHomeMultidata")
        promise.then(res => {
          console.log(res)
        }).catch(err => {
          console.log(err)
        })
      })
```

## **module的基本使用**

什么是Module？ 

- 由于使用单一状态树，应用的所有状态会集中到一个比较大的对象，当应用变得非常复杂时，store 对象就有可能变得相当臃肿； 
- 为了解决以上问题，Vuex 允许我们将 store 分割成**模块（module）**； 
- 每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块；

> index.js

```js
import { createStore } from "vuex"
import home from './modules/home'
import user from './modules/user'

const store = createStore({
  state() {
    return {
      rootCounter: 100
    }
  },
  getters: {
    doubleRootCounter(state) {
      return state.rootCounter * 2
    }
  },
  mutations: {
    increment(state) {
      state.rootCounter++
    }
  },
  modules: {
    home,
    user
  }
});

export default store;

```

> user.js

```js
const userModule = {
  namespaced: true,
  state() {
    return {
      userCounter: 10
    }
  },
  getters: {

  },
  mutations: {

  },
  actions: {

  }
}
export default userModule
```

### **module的局部状态**

对于模块内部的 mutation 和 getter，接收的第一个参数是 **模块的局部状态对象** ,后面是根组件的状态对象

```js
  getters: {
    doubleHomeCounter(state, getters, rootState, rootGetters) {
      return state.homeCounter * 2
    },
  },
  actions: {
    incrementAction({commit, dispatch, state, rootState, getters, rootGetters}) {
      commit("increment")
      commit("increment", null, {root: true})
      
      // dispatch
      // dispatch("incrementAction", null, {root: true})
    }
  }
```

### **module的命名空间**

默认情况下，模块内部的action和mutation仍然是注册在**全局的命名空间**中的：

- 这样使得多个模块能够对同一个 action 或 mutation 作出响应；
- Getter 同样也默认注册在全局命名空间；

如果我们希望模块具有更高的封装度和复用性，可以添加 namespaced: true 的方式使其成为带命名空间的模块：

- 当模块被注册后，它的所有 getter、action 及 mutation 都会自动根据模块注册的路径调整命名；

```js
const homeModule = {
  namespaced: true,
  state() {
    return {
      homeCounter: 100
    }
  },
}
```

### **module的辅助函数**

如果辅助函数有三种使用方法： 

- 方式一：通过完整的模块空间名称来查找； 
- 方式二：第一个参数传入模块空间名称，后面写上要使用的属性；
- 方式三：通过 createNamespacedHelpers 生成一个模块的辅助函数；

```vue
<template>
  <div>
    <hr>
    <h2>{{ homeCounter }}</h2>
    <h2>{{ doubleHomeCounter }}</h2>
    <button @click="increment">home+1</button>
    <button @click="incrementAction">home+1</button>
    <hr>
  </div>
</template>

<script>
  import { createNamespacedHelpers, mapState, mapGetters, mapMutations, mapActions } from "vuex";

  import { useState, useGetters } from '../hooks/index'

  //写法三依赖于 createNamespacedHelpers 函数
  const { mapState, mapGetters, mapMutations, mapActions } = createNamespacedHelpers("home")

  export default {
    computed: {
      // 1.写法一:
      ...mapState({
        homeCounter: state => state.home.homeCounter
      }),
      ...mapGetters({
        doubleHomeCounter: "home/doubleHomeCounter"
      }),

      // 2.写法二:
      ...mapState("home", ["homeCounter"]),
      ...mapGetters("home", ["doubleHomeCounter"]),

      // 3.写法三:
      ...mapState(["homeCounter"]),
      ...mapGetters(["doubleHomeCounter"])
    },
    methods: {
      // 1.写法一:
      ...mapMutations({
        increment: "home/increment"
      }),
      ...mapActions({
        incrementAction: "home/incrementAction"
      }),

      // 2.写法二
      ...mapMutations("home", ["increment"]),
      ...mapActions("home", ["incrementAction"]),
      
      // 3.写法三:
      ...mapMutations(["increment"]),
      ...mapActions(["incrementAction"]),
    },

    setup() {
      {homeCounter: function}
      const state = useState(["rootCounter"])
      const rootGetters = useGetters(["doubleRootCounter"])
      const getters = useGetters("home", ["doubleHomeCounter"])

      const mutations = mapMutations(["increment"])
      const actions = mapActions(["incrementAction"])

      return {
        ...state,
        ...getters,
        ...rootGetters,
        ...mutations,
        ...actions
      }
    }
  }
</script>

<style scoped>

</style>
```







# 知识补充

## 为什么Vue3选择Proxy呢？

- Object.definedProperty 是劫持对象的属性时，如果新增元素：
  - 那么Vue2需要再次 调用definedProperty，而 Proxy 劫持的是整个对象，不需要做特殊处理；
-  修改对象的不同：
  - 使用 defineProperty 时，我们修改原来的 obj 对象就可以触发拦截；
  - 而使用 proxy，就必须修改代理对象，即 Proxy 的实例才可以触发拦截；
-  Proxy 能观察的类型比 defineProperty 更丰富
  - has：in操作符的捕获器；
  - deleteProperty：delete 操作符的捕捉器；
  - 等等其他操作；
- Proxy 作为新标准将受到浏览器厂商重点持续的性能优化；
- 缺点：Proxy 不兼容IE，也没有 polyfill, defineProperty 能支持到IE9



## Nexttick的使用和原理

官方解释：将回调推迟到下一个 DOM 更新周期之后执行。在更改了一些数据以等待 DOM 更新后立即使用它。 

比如我们有下面的需求： 

- 点击一个按钮，我们会修改在h2中显示的message； 
- message被修改后，获取h2的高度； 

实现上面的案例我们有三种方式：

- 方式一：在点击按钮后立即获取到h2的高度（错误的做法）

- 方式二：在updated生命周期函数中获取h2的高度（但是其他数据更新，也会执行该操作） 

- 方式三：使用nexttick函数；

### **nexttick是如何做到的呢？**

Vue中的任务队列有很多中（宏任务队列【优先级高】，微任务队列），如生命周期函数和watch之类都属于微任务队列，在宏任务队列之后执行。如果当时查询它的改变后的值会发现他没有改变还是原来值，因为此时微任务队列还没有执行。nexttick就可以让当前函数也插入微任务队列中，查询的值就是改变后的值了。

![image-20220327235648624](https://s2.loli.net/2022/03/28/8NnqJxKyWUTOmi1.png)

## **historyApiFallback**

- historyApiFallback是开发中一个非常常见的属性，它主要的作用是解决SPA页面在路由跳转之后，进行页面刷新时，返回404的错误。 
-  boolean值：默认是false
  - 如果设置为true，那么在刷新时，返回404错误时，会自动返回 index.html 的内容；
- object类型的值，可以配置rewrites属性：
  - 可以配置from来匹配路径，决定要跳转到哪一个页面；
- 事实上devServer中实现historyApiFallback功能是通过connect-history-api-fallback库的：
  - 可以查看connect-history-api-fallback 文档

![image-20220330231046746](https://s2.loli.net/2022/03/30/b4k72zTaWKxHDXy.png)

## 对象的引用-浅拷贝-深拷贝

- 浅拷贝是创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以**如果其中一个对象改变了这个地址，就会影响到另一个对象**。

- 深拷贝是将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且**修改新对象不会影响原对象**。

![浅拷贝的过程](https://s2.loli.net/2022/01/10/CcpDWRGv3Ya7A58.png)

```js
<!-- 1.对象的应用赋值 -->
  <script>
    // 对象是引用类型
    const info = {
      name: "lyc",
      age = 18
    };
    const obj = info;
    info.name = "kobe";
    console.log(obj.name);
  </script>

  <!-- 2.对象的浅拷贝 -->
  <script>
    const info = {
      name: "lyc",
      age: 18,
      friend: {
        name: "kebo"
      }
    };
    const obj = Object.assign({}, info);

    info.name = "kobe";
    console.log(obj.name);

    info.friend.name = 'lyc';
    console.log(obj.friend.name
    );
  </script>

  <!-- 3.对象的深拷贝 -->
  <script>
    const info = {
      name: "lyc",
      age: 18,
      friend: {
        name: "kebo"
      }
    };
    const obj = JSON.parse(JSON.stringify(info));
    info.friend.name = "lyc";
    console.log(obj.friend.name);
  </script>
```



## 前端面试之彻底搞懂this指向

this是JavaScript中的一个关键字，但是又一个相对比较特别的关键字，不像function、var、for、if这些关键字一样，可以很清楚的搞清楚它到底是如何使用的。

this会在执行上下文中绑定一个对象，但是是根据什么条件绑定的呢？在不同的执行条件下会绑定不同的对象，这也是让人捉摸不定的地方。

这一次，我们一起来彻底搞定this到底是如何绑定的吧！

一. 理解this 1.1. 为什么使用this 在常见的编程语言中，几乎都有this这个关键字（Objective-C中使用的是self），但是JavaScript中的this和常见的面向对象语言中的this不太一样：

常见面向对象的编程语言中，比如Java、C++、Swift、Dart等等一系列语言中，this通常只会出现在 类的方法 中。 也就是你需要有一个类，类中的方法（特别是实例方法）中，this代表的是当前调用对象。

但是JavaScript中的this更加灵活，无论是它出现的位置还是它代表的含义。

使用this有什么意义呢？下面的代码中，我们通过对象字面量创建出来一个对象，当我们调用对象的方法时，希望将对象的名称一起进行打印。

如果没有this，那么我们的代码会是下面的写法：

在方法中，为了能够获取到name名称，必须通过obj的引用（变量名称）来获取。

但是这样做有一个很大的弊端：如果我将obj的名称换成了info，那么所有的方法中的obj都需要换成info。

```js
var obj = {
  name: "why",
  running: function() {
    console.log(obj.name + " running");
  },
  eating: function() {
    console.log(obj.name + " eating");
  },
  studying: function() {
    console.log(obj.name + " studying");
  }
}
```

事实上，上面的代码，在实际开发中，我们都会使用this来进行优化：

当我们通过obj去调用running、eating、studying这些方法时，this就是指向的obj对象

```js
var obj = {
  name: "why",
  running: function() {
    console.log(this.name + " running");
  },
  eating: function() {
    console.log(this.name + " eating");
  },
  studying: function() {
    console.log(this.name + " studying");
  }
}
```

所以我们会发现，在某些函数或者方法的编写中，this可以让我们更加便捷的方式来引用对象，在进行一些API设计时，代码更加的简洁和易于复用。

当然，上面只是应用this的一个场景而已，开发中使用到this的场景到处都是，这也是为什么它不容易理解的原因。

1.2. this指向什么 我们先说一个最简单的，this在全局作用域下指向什么？

这个问题非常容易回答，在浏览器中测试就是指向window

所以，在全局作用域下，我们可以认为this就是指向的window

```js
console.log(this); // window

var name = "why";
console.log(this.name); // why
console.log(window.name); // why
```

但是，开发中很少直接在全局作用域下去使用this，通常都是在 函数中使用 。

所有的函数在被调用时，都会创建一个执行上下文：

这个上下文中记录着函数的调用栈、函数的调用方式、传入的参数信息等；

this也是其中的一个属性；

我们先来看一个让人困惑的问题：

定义一个函数，我们采用三种不同的方式对它进行调用，它产生了三种不同的结果

```js
// 定义一个函数
function foo() {
  console.log(this);
}

// 1.调用方式一: 直接调用
foo(); // window

// 2.调用方式二: 将foo放到一个对象中,再调用
var obj = {
  name: "why",
  foo: foo
}
obj.foo() // obj对象

// 3.调用方式三: 通过call/apply调用
foo.call("abc"); // String {"abc"}对象
```

上面的案例可以给我们什么样的启示呢？ 

1.函数在调用时，JavaScript会默认给this绑定一个值；

2.this的绑定和定义的位置（编写的位置）没有关系；

3.this的绑定和调用方式以及调用的位置有关系；

4.this是在运行时被绑定的；

那么this到底是怎么样的绑定规则呢？一起来学习一下吧

二. this绑定规则 我们现在已经知道this无非就是在函数调用时被绑定的一个对象，我们就需要知道它在不同的场景下的绑定规则即可。

2.1. 默认绑定 什么情况下使用默认绑定呢？独立函数调用。

独立的函数调用我们可以理解成函数没有被绑定到某个对象上进行调用；

案例一：普通函数调用 该函数直接被调用，并没有进行任何的对象关联；

这种独立的函数调用会使用默认绑定，通常默认绑定时，函数中的this指向全局对象（window）；

```js
function foo() {
  console.log(this); // window
}

foo();
复制代码
```

案例二：函数调用链（一个函数又调用另外一个函数） 所有的函数调用都没有被绑定到某个对象上；

```js
// 2.案例二:
function test1() {
  console.log(this); // window
  test2();
}

function test2() {
  console.log(this); // window
  test3()
}

function test3() {
  console.log(this); // window
}
test1();
复制代码
```

案例三：将函数作为参数，传入到另一个函数中

```js
function foo(func) {
  func()
}

function bar() {
  console.log(this); // window
}

foo(bar);
复制代码
```

我们对案例进行一些修改，考虑一下打印结果是否会发生变化：

这里的结果依然是window，为什么呢？

原因非常简单，在真正函数调用的位置，并没有进行任何的对象绑定，只是一个独立函数的调用；

```js
function foo(func) {
  func()
}

var obj = {
  name: "why",
  bar: function() {
    console.log(this); // window
  }
}

foo(obj.bar);
```

2.2. 隐式绑定 另外一种比较常见的调用方式是通过某个对象进行调用的：

也就是它的调用位置中，是通过某个对象发起的函数调用。

案例一：通过对象调用函数 foo的调用位置是obj.foo()方式进行调用的

那么foo调用时this会隐式的被绑定到obj对象上

```js
function foo() {
  console.log(this); // obj对象
}

var obj = {
  name: "why",
  foo: foo
}

obj.foo();
```

案例二：案例一的变化 我们通过obj2又引用了obj1对象，再通过obj1对象调用foo函数；

那么foo调用的位置上其实还是obj1被绑定了this；

```js
function foo() {
  console.log(this); // obj对象
}

var obj1 = {
  name: "obj1",
  foo: foo
}

var obj2 = {
  name: "obj2",
  obj1: obj1
}

obj2.obj1.foo();
```

案例三：隐式丢失 结果最终是window，为什么是window呢？

因为foo最终被调用的位置是bar，而bar在进行调用时没有绑定任何的对象，也就没有形成隐式绑定；

相当于是一种默认绑定；

```js
function foo() {
  console.log(this);
}

var obj1 = {
  name: "obj1",
  foo: foo
}

// 讲obj1的foo赋值给bar
var bar = obj1.foo;
bar();
```

2.3. 显示绑定 隐式绑定有一个前提条件：

必须在调用的 对象内部 有一个对函数的引用（比如一个属性）； 如果没有这样的引用，在进行调用时，会报找不到该函数的错误；

正是通过这个引用，间接的将this绑定到了这个对象上；

如果我们不希望在 对象内部 包含这个函数的引用，同时又希望在这个对象上进行强制调用，该怎么做呢？

JavaScript所有的函数都可以使用call和apply方法（这个和Prototype有关）。

它们两个的区别这里不再展开；

其实非常简单，第一个参数是相同的，后面的参数，apply为数组，call为参数列表；

这两个函数的第一个参数都要求是一个对象，这个对象的作用是什么呢？就是给this准备的。

在调用这个函数时，会将this绑定到这个传入的对象上。

因为上面的过程，我们明确的绑定了this指向的对象，所以称之为 显示绑定 。

2.3.1. call、apply 通过call或者apply绑定this对象 显示绑定后，this就会明确的指向绑定的对象

```js
function foo() {
  console.log(this);
}

foo.call(window); // window
foo.call({name: "why"}); // {name: "why"}
foo.call(123); // Number对象,存放时123
```

2.3.2. bind函数 如果我们希望一个函数总是显示的绑定到一个对象上，可以怎么做呢？ 方案一：自己手写一个辅助函数（了解）

我们手动写了一个bind的辅助函数

这个辅助函数的目的是在执行foo时，总是让它的this绑定到obj对象上

```js
function foo() {
  console.log(this);
}

var obj = {
  name: "why"
}

function bind(func, obj) {
  return function() {
    return func.apply(obj, arguments);
  }
}

var bar = bind(foo, obj);

bar(); // obj对象
bar(); // obj对象
bar(); // obj对象
复制代码
```

方案二：使用Function.prototype.bind

```js
function foo() {
  console.log(this);
}

var obj = {
  name: "why"
}

var bar = foo.bind(obj);

bar(); // obj对象
bar(); // obj对象
bar(); // obj对象
复制代码
```

2.3.3. 内置函数 有些时候，我们会调用一些JavaScript的内置函数，或者一些第三方库中的内置函数。

这些内置函数会要求我们传入另外一个函数；

我们自己并不会显示的调用这些函数，而且JavaScript内部或者第三方库内部会帮助我们执行；

这些函数中的this又是如何绑定的呢？

案例一：setTimeout setTimeout中会传入一个函数，这个函数中的this通常是window

```js
setTimeout(function() {
  console.log(this); // window
}, 1000);
复制代码
```

为什么这里是window呢？

这个和setTimeout源码的内部调用有关；

setTimeout内部是通过apply进行绑定的this对象，并且绑定的是全局对象；

案例二：数组的forEach 数组有一个高阶函数forEach，用于函数的遍历：

在forEach中传入的函数打印的也是Window对象；

这是因为默认情况下传入的函数是自动调用函数（默认绑定）；

```js
var names = ["abc", "cba", "nba"];
names.forEach(function(item) {
  console.log(this); // 三次window
});
```

我们是否可以改变该函数的this指向呢？



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/20/172d20ad4f7c5a05~tplv-t2oaga2asx-watermark.awebp)



```js
var names = ["abc", "cba", "nba"];
var obj = {name: "why"};
names.forEach(function(item) {
  console.log(this); // 三次obj对象
}, obj);
```

案例三：div的点击 如果我们有一个div元素：

注意：省略了部分代码

```js
 <style>
    .box {
      width: 200px;
      height: 200px;
      background-color: red;
    }
  </style>

  <div class="box"></div>
```

获取元素节点，并且监听点击：

在点击事件的回调中，this指向谁呢？box对象；

这是因为在发生点击时，执行传入的回调函数被调用时，会将box对象绑定到该函数中；

```js
var box = document.querySelector(".box");
box.onclick = function() {
  console.log(this); // box对象
}
复制代码
```

所以传入到内置函数的回调函数this如何确定呢？

某些内置的函数，我们很难确定它内部是如何调用传入的回调函数；

一方面可以通过分析源码来确定，另一方面我们可以通过经验（见多识广）来确定；

但是无论如何，通常都是我们之前讲过的规则来确定的；

2.4. new绑定 JavaScript中的函数可以当做一个类的构造函数来使用，也就是使用new关键字。

使用new关键字来调用函数时，会执行如下的操作：

1.创建一个全新的对象；

2.这个新对象会被执行Prototype连接；

3.这个新对象会绑定到函数调用的this上（this的绑定在这个步骤完成）；

4.如果函数没有返回其他对象，表达式会返回这个新对象；

```js
// 创建Person
function Person(name) {
  console.log(this); // Person {}
  this.name = name; // Person {name: "why"}
}

var p = new Person("why");
console.log(p);
复制代码
```

2.5. 规则优先级 学习了四条规则，接下来开发中我们只需要去查找函数的调用应用了哪条规则即可，但是如果一个函数调用位置应用了多条规则，优先级谁更高呢？

1.默认规则的优先级最低 毫无疑问，默认规则的优先级是最低的，因为存在其他规则时，就会通过其他规则的方式来绑定this

2.显示绑定优先级高于隐式绑定 显示绑定和隐式绑定哪一个优先级更高呢？这个我们可以测试一下：

结果是obj2，说明是显示绑定生效了

```js
function foo() {
  console.log(this);
}

var obj1 = {
  name: "obj1",
  foo: foo
}

var obj2 = {
  name: "obj2",
  foo: foo
}

// 隐式绑定
obj1.foo(); // obj1
obj2.foo(); // obj2

// 隐式绑定和显示绑定同时存在
obj1.foo.call(obj2); // obj2, 说明隐式绑定优先级更高
复制代码
```

3.new绑定优先级高于隐式绑定 结果是foo，说明是new绑定生效了

```js
function foo() {
  console.log(this);
}

var obj = {
  name: "why",
  foo: foo
}

new obj.foo(); // foo对象, 说明new绑定优先级更高
复制代码
```

4.new绑定优先级高于bind new绑定和call、apply是不允许同时使用的，所以不存在谁的优先级更高

```js
function foo() {
  console.log(this);
}

var obj = {
  name: "obj"
}

var foo = new foo.call(obj);
复制代码
```



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/20/172d20cb1ae8aae6~tplv-t2oaga2asx-watermark.awebp)

new和call同时使用 但是new绑定是否可以和bind后的函数同时使用呢？可以



结果显示为foo，那么说明是new绑定生效了

```js
function foo() {
  console.log(this);
}

var obj = {
  name: "obj"
}

// var foo = new foo.call(obj);
var bar = foo.bind(obj);
var foo = new bar(); // 打印foo, 说明使用的是new绑定
复制代码
```

优先级总结：

new绑定 > 显示绑定（bind）> 隐式绑定 > 默认绑定

三. this规则之外 我们讲到的规则已经足以应付平时的开发，但是总有一些语法，超出了我们的规则之外。（神话故事和动漫中总是有类似这样的人物）

3.1. 忽略显示绑定 如果在显示绑定中，我们传入一个null或者undefined，那么这个显示绑定会被忽略，使用默认规则：

```js
function foo() {
  console.log(this);
}

var obj = {
  name: "why"
}

foo.call(obj); // obj对象
foo.call(null); // window
foo.call(undefined); // window

var bar = foo.bind(null);
bar(); // window
复制代码
```

3.2. 间接函数引用 另外一种情况，创建一个函数的 间接引用 ，这种情况使用默认绑定规则。

我们先来看下面的案例结果是什么？

(num2 = num1)的结果是num1的值；

```js
var num1 = 100;
var num2 = 0;
var result = (num2 = num1);
console.log(result); // 100
复制代码
```

我们来下面的函数赋值结果：

赋值(obj2.foo = obj1.foo)的结果是foo函数；

foo函数被直接调用，那么是默认绑定；

```js
function foo() {
  console.log(this);
}

var obj1 = {
  name: "obj1",
  foo: foo
}; 

var obj2 = {
  name: "obj2"
}

obj1.foo(); // obj1对象
(obj2.foo = obj1.foo)();  // window
复制代码
```

3.3. ES6箭头函数 在ES6中新增一个非常好用的函数类型：箭头函数

这里不再具体介绍箭头函数的用法，可以自行学习。

箭头函数不使用this的四种标准规则（也就是不绑定this），而是根据外层作用域来决定this。

我们来看一个模拟网络请求的案例：

这里我使用setTimeout来模拟网络请求，请求到数据后如何可以存放到data中呢？

我们需要拿到obj对象，设置data；

但是直接拿到的this是window，我们需要在外层定义： var _this = this 在setTimeout的回调函数中使用_this就代表了obj对象

```js
var obj = {
  data: [],
  getData: function() {
    var _this = this;
    setTimeout(function() {
      // 模拟获取到的数据
      var res = ["abc", "cba", "nba"];
      _this.data.push(...res);
    }, 1000);
  }
}

obj.getData();
复制代码
```

上面的代码在ES6之前是我们最常用的方式，从ES6开始，我们会使用箭头函数：

为什么在setTimeout的回调函数中可以直接使用this呢？

因为箭头函数并不绑定this对象，那么this引用就会从上层作用域中找到对应的this

```js
var obj = {
  data: [],
  getData: function() {
    setTimeout(() => {
      // 模拟获取到的数据
      var res = ["abc", "cba", "nba"];
      this.data.push(...res);
    }, 1000);
  }
}

obj.getData();
复制代码
```

思考：如果getData也是一个箭头函数，那么setTimeout中的回调函数中的this指向谁呢？

答案是window；

依然是不断的从上层作用域找，那么找到了全局作用域；

在全局作用域内，this代表的就是window

```js
var obj = {
  data: [],
  getData: () => {
    setTimeout(() => {
      console.log(this); // window
    }, 1000);
  }
}

obj.getData();
复制代码
```

四. this面试题 4.1. 面试题一：

```js
var name = "window";
var person = {
  name: "person",
  sayName: function () {
    console.log(this.name);
  }
};
function sayName() {
  var sss = person.sayName;
  sss(); 
  person.sayName(); 
  (person.sayName)(); 
  (b = person.sayName)(); 
}
sayName();
复制代码
```

这道面试题非常简单，无非就是绕一下，希望把面试者绕晕：

```js
function sayName() {
  var sss = person.sayName;
  // 独立函数调用，没有和任何对象关联
  sss(); // window
  // 关联
  person.sayName(); // person
  (person.sayName)(); // person
  (b = person.sayName)(); // window
}
复制代码
```

4.2. 面试题二：

```js
var name = 'window'
var person1 = {
  name: 'person1',
  foo1: function () {
    console.log(this.name)
  },
  foo2: () => console.log(this.name),
  foo3: function () {
    return function () {
      console.log(this.name)
    }
  },
  foo4: function () {
    return () => {
      console.log(this.name)
    }
  }
}

var person2 = { name: 'person2' }

person1.foo1(); 
person1.foo1.call(person2); 

person1.foo2();
person1.foo2.call(person2);

person1.foo3()();
person1.foo3.call(person2)();
person1.foo3().call(person2);

person1.foo4()();
person1.foo4.call(person2)();
person1.foo4().call(person2);
复制代码
```

下面是代码解析：

```js
// 隐式绑定，肯定是person1
person1.foo1(); // person1
// 隐式绑定和显示绑定的结合，显示绑定生效，所以是person2
person1.foo1.call(person2); // person2

// foo2()是一个箭头函数，不适用所有的规则
person1.foo2() // window
// foo2依然是箭头函数，不适用于显示绑定的规则
person1.foo2.call(person2) // window

// 获取到foo3，但是调用位置是全局作用于下，所以是默认绑定window
person1.foo3()() // window
// foo3显示绑定到person2中
// 但是拿到的返回函数依然是在全局下调用，所以依然是window
person1.foo3.call(person2)() // window
// 拿到foo3返回的函数，通过显示绑定到person2中，所以是person2
person1.foo3().call(person2) // person2

// foo4()的函数返回的是一个箭头函数
// 箭头函数的执行找上层作用域，是person1
person1.foo4()() // person1
// foo4()显示绑定到person2中，并且返回一个箭头函数
// 箭头函数找上层作用域，是person2
person1.foo4.call(person2)() // person2
// foo4返回的是箭头函数，箭头函数只看上层作用域
person1.foo4().call(person2) // person1
复制代码
```

4.3. 面试题三:

```js
var name = 'window'
function Person (name) {
  this.name = name
  this.foo1 = function () {
    console.log(this.name)
  },
  this.foo2 = () => console.log(this.name),
  this.foo3 = function () {
    return function () {
      console.log(this.name)
    }
  },
  this.foo4 = function () {
    return () => {
      console.log(this.name)
    }
  }
}
var person1 = new Person('person1')
var person2 = new Person('person2')

person1.foo1()
person1.foo1.call(person2)

person1.foo2()
person1.foo2.call(person2)

person1.foo3()()
person1.foo3.call(person2)()
person1.foo3().call(person2)

person1.foo4()()
person1.foo4.call(person2)()
person1.foo4().call(person2)
复制代码
```

下面是代码解析：

```js
// 隐式绑定
person1.foo1() // peron1
// 显示绑定优先级大于隐式绑定
person1.foo1.call(person2) // person2

// foo是一个箭头函数，会找上层作用域中的this，那么就是person1
person1.foo2() // person1
// foo是一个箭头函数，使用call调用不会影响this的绑定，和上面一样向上层查找
person1.foo2.call(person2) // person1

// 调用位置是全局直接调用，所以依然是window（默认绑定）
person1.foo3()() // window
// 最终还是拿到了foo3返回的函数，在全局直接调用（默认绑定）
person1.foo3.call(person2)() // window
// 拿到foo3返回的函数后，通过call绑定到person2中进行了调用
person1.foo3().call(person2) // person2

// foo4返回了箭头函数，和自身绑定没有关系，上层找到person1
person1.foo4()() // person1
// foo4调用时绑定了person2，返回的函数是箭头函数，调用时，找到了上层绑定的person2
person1.foo4.call(person2)() // person2
// foo4调用返回的箭头函数，和call调用没有关系，找到上层的person1
person1.foo4().call(person2) // person1
复制代码
```



```js
var name = 'window' function Person (name) { this.name = name this.obj = { name: 'obj', foo1: function () { return function () { console.log(this.name) } }, foo2: function () { return () => { console.log(this.name) } } } } var person1 = new Person('person1') var person2 = new Person('person2')

person1.obj.foo1()() person1.obj.foo1.call(person2)() person1.obj.foo1().call(person2)

person1.obj.foo2()() person1.obj.foo2.call(person2)() person1.obj.foo2().call(person2)
```

下面是代码解析：

```js
// obj.foo1()返回一个函数
// 这个函数在全局作用于下直接执行（默认绑定）
person1.obj.foo1()() // window
// 最终还是拿到一个返回的函数（虽然多了一步call的绑定）
// 这个函数在全局作用于下直接执行（默认绑定）
person1.obj.foo1.call(person2)() // window
person1.obj.foo1().call(person2) // person2

// 拿到foo2()的返回值，是一个箭头函数
// 箭头函数在执行时找上层作用域下的this，就是obj
person1.obj.foo2()() // obj
// foo2()的返回值，依然是箭头函数，但是在执行foo2时绑定了person2
// 箭头函数在执行时找上层作用域下的this，找到的是person2
person1.obj.foo2.call(person2)() // person2
// foo2()的返回值，依然是箭头函数
// 箭头函数通过call调用是不会绑定this，所以找上层作用域下的this是obj
person1.obj.foo2().call(person2) // obj
复制代码
```

有想了解更多的小伙伴可以加Q群[链接](https://link.juejin.cn/?target=undefined)里面看一下，应该对你们能够有所帮助。

![粉紫色三色鹿设计公司logo创意艺术中文logo](D:/Desktop/%E7%B2%89%E7%B4%AB%E8%89%B2%E4%B8%89%E8%89%B2%E9%B9%BF%E8%AE%BE%E8%AE%A1%E5%85%AC%E5%8F%B8logo%E5%88%9B%E6%84%8F%E8%89%BA%E6%9C%AF%E4%B8%AD%E6%96%87logo.svg)
