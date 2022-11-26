# JS做题笔记



[TOC]

## JS题目

### 1.执行以下程序，输出结果为（）

```js
var one;
var two = null;
console.log(one == two,one === two);
```

**true false**

在JavaScript中下面的值被当作假 false. undefined. null. 空字符串 数字0 数字NAN == 和 = = =的区别是，==会将两边的值进行隐式类型转换，而 = = =也不会。 题目中，var one; 只定义未赋值，故one是的值为undefined, undefined和null转换为Boolean类型后都为false，= = =不会进行转换，那么undefined和null当然不相等啦，所以是true！

------

### 2.执行以下程序，输出结果为（）

```js
var uname = "window";

var object = {

            uname :"object",

            fun:function(){

                console.log(this.uname);

                return function(){

                   console.log(this.uname);

                }

            }

}

object.fun()();
```

**object window**

object.fun()()等效于var fn = object.fun(); fn();实际上是调用函数两次，第一次是调用object对象的fun函数，第二次是调用fun函数的返回函数。第一次调用fun函数时，this指向上一级对象，即object对象，因此输出对象object的uname属性值object,第二次调用的返回函数，其this指向window对象，这是因为匿名函数具有全局性，匿名函数的this指向window对象，因此输出结果为window对象的uname属性值window。

![image-20220708135745076](https://s2.loli.net/2022/07/08/Xk7cvB3mlSDsAzH.png)

------

### 3.下列表达式中，返回值为true的是（）

①Object.is(NaN,NaN)

②Object.is(+0,-0)

③NaN === NaN

④+0 === -0

**①④**

Object.is()与= = =都是判断两个数是否严格相等。它们的区别主要在NaN自身和+0与-0的判断。对于NaN自身的判断，Object.is(NaN,NaN)的返回结果为true，而NaN = = =NaN的返回结果为false；对于+0、-0的判断，Object.is(+0,-0)的返回结果为false，而+0 === -0的返回结果为true，故A选项正确。



### 4.Alert(1&&2)的值是？

**2**

&& 运算，如果前面值为true,则结果为后面的值。如果前面值为false,则值为false.

|| 运算，如果前面值为true,则结果为前面的值,如果前面的值为false,则结果为后面的值。



### 5.已知数组arr = [1,3,10,2,20]，现要对数组筛选出小于10的元素，作为新数组的元素并输出新数组，下列选项中，不符合要求的是（）

```js
var arr = [1,3,10,2,20];

var result = arr.map(value=>value < 10);

console.log(result);
```

选项的最终输出结果为[true, true, false, true, false]，不符合要求，应该换成arr.filter()才是筛选数组



####  > 知识点：map，filter，reduce

map 作用是生成一个新数组，遍历原数组，将每个元素拿出来做一些变换然后放入到新的数组中。

```js
let arr = [1,2,3]
let newArr = arr.map(item => item + 1)
console.log(newArr)//[2,3,4]
```

filter 的作用也是生成一个新数组，在遍历数组的时候将返回值为 true 的元素放入新数组，我们可以利用这个函数删除一些不需要的元素。

```js
	let arr = [1,2,3,4,5,6,7,8,9]
    let newArr = arr.filter(item => item % 2 == 0)
    console.log(newArr) // [2, 4, 6, 8]
```

reduce 可以将数组中的元素通过回调函数最终转换为一个值。

**计算每个元素出现的次数**

```js
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

var countedNames = names.reduce(function (allNames, name) {
    // allNames 初始值为{}
    if (name in allNames) {	// 当前元素是allNames对象的属性表示遍历过 次数+1
        allNames[name]++;
    }
    else {                  // 当前元素不存在 设置为allNames对象的属性 第一次遍历：1
        allNames[name] = 1;
    }
    return allNames;        // 返回统计的对象 当做累计器
}, {});
console.log(countedNames);  // {Alice: 2, Bob: 1, Tiff: 1, Bruce: 1}

```

**数组去重**

```js
let arr = [1, 2, 3, 4, 4, 1, 2, 5]
let newArr = arr.reduce((pre, cur) => {
    // pre初始值为[] 
    if (!pre.includes(cur)) { // 当前元素不在数组中就加进去
        pre.push(cur);
    }
    return pre;
}, [])
console.log(newArr);// [1, 2, 3, 4, 5]
```

**将二维数组转化为一维**

```js
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(
// 合并数组
 ( acc, cur ) => acc.concat(cur),
 []
);
console.log(flattened);	// (6) [0, 1, 2, 3, 4, 5]
```

**求对象里的属性和**

```js
var result = [
    {
        subject: 'math',
        score: 10
    },
    {
        subject: 'chinese',
        score: 20
    },
    {
        subject: 'english',
        score: 30
    }
];

var sum = result.reduce(function(prev, cur) {
    return cur.score + prev;
}, 0);
console.log(sum) //60
```



### 6.假设document是HTML文档中的一个节点，点击该节点后会发生什么？

```js
function test() {
  this.flag = false;
  this.change = () => {
    this.flag = true;
    console.log(button.flag);
  };
}
const button = new test();
document.addEventListener("click", button.change);
```

**输出true**

除了箭头函数，this的指向就看它的直接调用者是谁！而箭头函数就找它外面第一个不是箭头函数的函数。题目中调用button.change，所以去分析change(),而难点就在于 this.flag = true;的this是谁？当看到change是一个箭头函数的this时，就什么也不要考虑，就去找外面第一个不是箭头函数的函数，也就是说，他会把this绑定到text上，那this.flag = true;就意味着text()的实例中的flag会变成true，所以button.flag为true。

### 7.执行以下程序，输出结果为（）

```js
var arr = [2,1,3,5,9];

var count = 0;

arr.forEach((val1,val2)=>{

        count++;

        if(count % 3 == 0){

            return;

        }

        console.log(val1);

})
```

**2 1 5 9**

arr.forEach()是循环遍历数组，它的参数是一个函数，每迭代一次数组，就执行函数一次，也就是，虽然在函数内部存在return语句，但是当执行return时相当于退出一次迭代，当前数组会继续下一次迭代，函数有两个参数，参数val1为数组的元素值，参数val2为数组元素对应的索引，因此正确答案为D选项。

### 8.下面求a中最大值的代码正确的是

var a =[1,4,5,2,9];

```js
Math.max.apply(null,a)
```

Math对象包含max()方法，用于确认一组数值中的最大值。该方法接收任意多个数值参数，不接受数组参数。要找到数组中的最值，可以使用apply()方法，D表示将Math.max()方法的执行环境切换到null上，apply()方法接收两个参数，第二个参数是一个数组。call()需要传递明确几个参数，写全，apply（）可以接收一个数组作为参数，不管数组中有多少个元素

### 9.现有如下html结构

```html
<ul>
 <li>click me</li>
 <li>click me</li>
 <li>click me</li>
 <li>click me</li>
</ul>
```

运行如下代码：

```js
var elements=document.getElementsByTagName('li');
var length=elements.length;
for(var i=0;i<length;i++){
    elements[i].onclick=function() {
        alert(i);
    }
}
```

依次点击4个li标签，哪一个选项是正确的运行结果?

**依次弹出4，4，4，4**

这里考的是JS的运行机制！ 事件(click,focus等等)，定时器(setTimeout和setInterval)，ajax,都是会触发异步，属于异步任务；js是单线程的，一个时间点只能做一件事，优先处理同步任务； 按照代码从上往下执行，遇到异步，就挂起，放到异步任务里，继续执行同步任务，只有同步任务执行完了，才去看看有没有异步任务，然后再按照顺序执行！ 这里for循环是同步任务，onclick是异步任务，所以等for循环执行完了，i变成4了，注意：这里因为i是全局变量，最后一个i++，使得i为4(后面的onclick函数，最后在循环外面执行，不受i<length限制)； 所以for循环每执行一次，onclick事件函数都会被挂起一次，共4次； for循环结束后，点击事件 触发了4个onclick函数，接着输出4个4！

### 10.下面判断对象myObj是否存在的写法错误的是( )

**myObj === null**

前提是myobj是一个对象，只是存在与不存在的问题，几种表示方法：

1、！obj

2、！window.obj

3、typeof myObj == "undefined（判断对象是否有定义，已定义未赋值，返回true）

4、myObj == undefined（已定义未赋值。返回true）

5、myObj === undefined （已定义未赋值，返回true）

6、!this.hasOwnProperty('myObj'))（判断是否为顶层对象的一个属性）

7、myobj == null（注意null与undefined的区别，ull指的是已经赋值为null的空对象，即这个对象实际上是有值的，而undefined指的是不存在或没有赋值的对象。）

以上几种都正确，但是我用的最多争议最少的是第三种

### 11.在ES6规范中，以下类型哪些属于基本数据类型（）

最新的 ECMAScript 标准定义了8种数据类型：

- 七种基本数据类型:
  - 布尔值（Boolean），有2个值分别是：true 和 false.
  - null ， 一个表明 null 值的特殊关键字。 JavaScript 是大小写敏感的，因此null与Null、NULL或变体完全不同。
  - undefined ，和 null 一样是一个特殊的关键字，undefined 表示变量未赋值时的属性。
  - 数字（Number），整数或浮点数，例如： 42 或者 3.14159。
  - 任意精度的整数 (BigInt) ，可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。
  - 字符串（String），字符串是一串表示文本值的字符序列，例如："Howdy" 。
  - 代表（Symbol） ( 在 ECMAScript 6 中新添加的类型).。一种实例是唯一且不可改变的数据类型。
- 以及对象（Object）。
