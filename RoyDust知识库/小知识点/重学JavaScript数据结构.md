# 重学JavaScript数据结构

## 一、常用api

1. 从头部删除元素——shift()方法 返回值为删除的元素

```javascript
var arr=[1,2,3,4]
re=arr.shift()//[2,3,4]
console.log(re)//1
123
```

2. 从尾部删除——pop()方法 返回值为删除的元素

```javascript
var arr=[1,2,3,4]
re=arr.pop()//[1,2,3]
console.log(re)//4
123
```

3. 向尾部添加元素——push()方法 返回值为新数组的长度

```javascript
var arr=[1,2,3]
re=arr.push(4,5,6)//[1,2,3,4,5,6]
console.log(re)//6
123
```

4. 向头部添加元素——unshift()方法 返回值为新数组的长度

```javascript
var arr=[1,2,3]
re=arr.unshift(4,5,6)//[4,5,6,1,2,3]
console.log(re)//6
123
```

5. 运用splice()方法可以进行任意删除、增加、修改的操作

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi"); //(规定从何处添加/删除元素,规定应该删除多少元素,要添加到数组的新元素)
console.log(fruits); //[ 'Banana', 'Orange', 'Lemon', 'Kiwi', 'Apple', 'Mango' ]
```

6. 字符串转化为数组

```js
var arr=s.split('')
```

7. 查找数组中最大值

```js
arr = [5, 2, 3, 4, 5, 6, 8];
//直接返回数组中最大值
console.log(Math.max(...arr));
//使用apply
const max = Math.max.apply(Math, arr); // 8
const min = Math.min.apply(Math, arr); // 2
console.log(max);
console.log(min);
```

8. 字符与ASCII码互转

```js
//将字母转为ascii码
var str = "A";
console.log(str.charCodeAt()); // 65
//将ascii码转为对应字母
var num = 97;
console.log(String.fromCharCode(num)); // 'a'
```

9. 创建新的拷贝数组

```js
let a=Array.from(b);//a=b
```

10. 替换字符串中的字符

```js
let str="abcdfaakg";
let str1=a.replace('a','o');//"obcdfaakg";
let str2=a.replace(/a/g,'o');//"obcdfookg";
//"/g"是全局替换
```

11. 字符串分割为数组，数组转为字符串

```js
let str='asdfg';
const arr = str.split('');
arr[0]='q';
let re=arr.join('');//'qsdfg'
```

12. 数组和字符串转换

```js
let str = "asdfg";
const arr = str.split("");
console.log(arr); //[ 'a', 's', 'd', 'f', 'g' ]
arr[0] = "q";
let res = arr.join("");
console.log(res); //'qsdfg'
```

13. 常见数学函数

```js
Math.ceil(count / pagesize); //向上整除 4/3=2;
Math.floor(count / pagesize); //向下整除 4/3=1;
Math.round(5/2);//四舍五入     
Math.parseInt(5/2);//丢弃小数部分,保留整数部分
Math.abs(-5);//绝对值
```

## 二、**数组**

#### 数组的访问和遍历

```js
// 数组的访问和遍历
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
//通过取 forEach 方法中传入函数的第一个入参和第二个入参，我们也可以取到数组每个元素的值及其对应索引
arr.forEach((item, index) => {
  console.log(item, index);
});
// map 方法在调用形式上与 forEach 无异，区别在于 map 方法会根据你传入的函数逻辑对数组中每个元素进行处理、进而返回一个全新的数组。
const newArr = arr.map((item, index) => {
  console.log(item, index);
  return item + 1;
});
```

#### fill 的局限性

当你给 fill 传递一个入参时，**如果这个入参的类型是引用类型，那么 fill 在填充坑位时填充的其实就是入参的引用**也就是说虽然看似我们给7个坑位各初始化了一个数组,其实这7个数组对应了同一个引用、指向的是同一块内存空间，**它们本质上是同一个数组**。因此当你修改第0行第0个元素的值时，第1-6行的第0个元素的值也都会跟着发生改变。

```js
const arr = new Array(7).fill([]);
```

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/3/8/170b9d27489b1815~tplv-t2oaga2asx-zoom-in-crop-mark:3024:0:0:0.awebp)

