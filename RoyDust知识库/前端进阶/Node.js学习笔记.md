# Node.js学习笔记

Node.js 可以解析JS代码（没有浏览器安全级别的限制）提供很多系统级别的API，如：

- 文件的读写 (File System)
- 进程的管理 (Process)
- 网络通信 (HTTP/HTTPS)
- ……

1、基本用法

## 1、第一个node.js程序

```js
// 引入http模块
//  代码块： node-http-server
var http = require('http');
/* 创建一个web服务器
request  获取url传过来的信息
response 给浏览器响应信息
*/
http.createServer(function (request, response) {
  // 设置响应头
  response.writeHead(200, {'Content-Type': 'text/plain'});
  // 表示输出一句话并且结束响应
  response.end('Hello World1111');
}).listen(8081); //端口号

console.log('Server running at http://127.0.0.1:8081/');
```

### 创建web服务


```js
const http =require('http');

http.createServer((req,res)=>{

    console.log(req.url); //获取url
    
    //设置响应头
    //状态码是200， 文件类型是html, 字符集是utf-8 
    res.writeHead(200,{ 'Content-type':"text/html;charset=utf-8" });
	res .write("<head> <meta charset='UTF-8' ></head>"); //解决乱码
    res.write('小老弟');

    res.end(); //结束响应

}).listen(3000);
```

### url模块

```js
const http =require('http');
const url =require('url');

var api='http://www.baidu.com?name=zhangsan&age=19';

var getvalue=url.parse(api,true).query;

console.log(getvalue);
```

安装superviaor

```
cnpm install -g superviaor
```

运行

```
supervisor app.js
```

## 2、CommonJs

![image-20210325145725155](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210325145725155.png)

模块

核心模块：HTTP模块、URL模块、Fs模块都是nodejs内置的核心模块，可以直接引入使用。

自定义模块：自己写的模块

1. 我们可以把公共的功能抽离成为一个单独的js文件作为一个模块，
 默认情况下面这个模块里面的方法或者属性，外面是没法访问的。
    如果要让外部可以访问模块里面的方法或者属性，
    就必须在模块里面通过exports 或者module. exports暴露属性或者方法。
2. 在需要使用这些模块的文件中，通过require 的方式引入这个模块。
 这个时候就可以使用模块里面暴露的属性和方法。

### 三种暴露模块方法

```js
// var obj={

//     get:function(){
//         console.log('获取数据')
//     },
//     post:function(){
//         console.log('提交数据')
//     }
// }
// exports.xxx=obj;

// module.exports=obj;

exports.get=function () {
    console.log('获取数据')
}
exports.post=function () {
    console.log('提交数据')
}
```

```js
 var request=require('./module/request');

console.log(request);    { xxx: { get: [Function: get], post: [Function: post] } }

console.log(request);    { get: [Function: get], post: [Function: post] }

console.log(request);   { get: [Function (anonymous)], post: [Function (anonymous)] }
```

### 自定义模块位置

​	![image-20210325195423976](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210325195423976.png)

路径可以省写

```js
var axios=require('axios/index');

var axios=require('axios'); //也可以，默认启用index

console.log(axios);
```

### 包

![image-20210325231630551](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210325231630551.png)

完全符合CommonJs规范的包目录一般包含如下这些文件。

- package.json :包描述文件。
- lbin :用于存放可执行二进制文件的目录。
- lib :用于存放JavaScript代码的目录。
- doc:用于存放文档的目录。

==在NodeJs中通过NPM命令来下载第三方的模块(包)==

NPM

![image-20210325232325476](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210325232325476.png)

1、可以在[npm网站](https://www.npmjs.com/)下载包

2、安装

```
npm install md5 --save
```

![image-20210325232610189](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210325232610189.png)
3、引用

```js
var md5=require('md5');
```

```
npm i
```

可以找回所依赖的包

4、看文档使用

5、指定包的版本(非常重要)

```
npm install node - media-server@2.1.0 --save
npm install jquery@1.8.0
```

### 常用命令

- npm init(生成package.json说明书文件)
  - npm init -y(可以跳过向导，快速生成)
- npm install
  - 一次性把dependencies选项中的依赖项全部安装
  - 简写（npm i）
- npm install 包名
  - 只下载
  - 简写（npm i 包名）
- npm install --save 包名
  - 下载并且保存依赖项（package.json文件中的dependencies选项）
  - 简写（npm i  包名）
- npm uninstall 包名
  - 只删除，如果有依赖项会依然保存
  - 简写（npm un 包名）
- npm uninstall --save 包名
  - 删除的同时也会把依赖信息全部删除
  - 简写（npm un 包名）
- npm help
  - 查看使用帮助
- npm 命令 --help
  - 查看具体命令的使用帮助（npm uninstall --help）

### package.json

每一个项目都要有一个`package.json`文件（包描述文件，就像产品的说明书一样）

这个文件可以通过`npm init`自动初始化出来

### npm init生成package.json

```cmd
npm init --yes
```

![image-20210325200745570](C:\Users\32140\AppData\Roaming\Typora\typora-user-images\image-20210325200745570.png)

生成 package.json

```json
{
  "name": "db",
  "version": "1.0.0",
  "description": "",
  "main": "db.js", //默认启动bd.js
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

对于目前来讲，最有用的是`dependencies`选项，可以用来帮助我们保存第三方包的依赖信息。

如果`node_modules`删除了也不用担心，只需要在控制面板中`npm install`就会自动把`package.json`中的`dependencies`中所有的依赖项全部都下载回来。

- 建议每个项目的根目录下都有一个`package.json`文件

- 建议执行`npm install 包名`的时候都加上`--save`选项，目的是用来保存依赖信息

  

## 3、fs的使用

引入

```js
const fs=require('fs');
```

### *1. fs.stat     检测是文件还是目录*

```js
fs.stat('./html',(err,date)=>{
    if(err){
        console.log(err);
        return;
    }

    console.log(`是文件；${date.isFile()}`);
    console.log(`是目录；${date.isDirectory()}`);
})
```



### *2. fs.mkdir     创建目录*



```js
fs.mkdir('./css',(err)=>{
    if(err){
        console.log(err);
        return;
    }

    console.log('创建成功');
})
path        将创建的目录路径
mode        目录权限(读写权限)，默认777
callback    回调，传递异常参数err
```



### *3. fs.writeFile   创建写入文件*

```js
fs.writeFile('./html/index.html','你好node.js',(err)=>{
    if(err){
        console.log(err);
        return;
    }
    console.log('写入成功');
})

filename    (String)             文件名称
data        (String| Buffer)    将要写入的内容，可以使字符串或buffer数据。
options     (object)            option数组对象，包含:
    .encoding    (string)    可选值，默认'utf8'
    .mode        (Number)    文件读写权限，默认值438
    .flag        (String )       默认值“w'
callback    {Function}   回调， 传递一个异常参数err。
```



### *4. fs.appendFile  追加文件*

```js
fs.appendFile('./html/index.html','\n你好node.js',(err)=>{
    if(err){
        console.log(err);
        return;
    }
    console.log('追加成功');
})
```



### *5. fs.readFile   读取文件*

```js
fs.readFile('./html/index.html',(err,date)=>{
    if(err){
        console.log(err);
        return;
    }
    console.log(date.toString());
})
```



### *6. fs.readdir   读取目录*

```js
fs.readdir('./html',(err,date)=>{
    if(err){
        console.log(err);
        return;
    }
    console.log(date);
})
```



### *7. fs.rename    重命名 功能：重命名&移动文件*

```js
fs.rename('./html/new.html','./html/dd.html',(err)=>{
    if(err){
        console.log(err);
        return;
    }
    console.log('重命名成功');
})
```



### *8. fs.rmdir     删除目录*

```js
fs.rmdir('./css',(err)=>{
    if(err){
        console.log(err);
        return;
    }
    console.log('删除目录成功');
})
```



### *9. fs.unlink    删除文件*

```js
fs.unlink('./html/dd.html',(err)=>{
    if(err){
        console.log(err);
        return;
    }
    console.log('删除文件成功');
})
```

10、流

> 读取文件

```js
const fs=require('fs');
var readStream=fs.createReadStream('./data/1.txt');

var count=0;
var str='';
readStream.on('data',(data)=>{
    str+=data;
    count++;
})

readStream.on('end',()=>{
    console.log(str);
    console.log(count);
})

readStream.on('err',()=>{
    console.log(err);
})
```

> 写入文件

```js
const fs=require('fs');
var str='';

for(var i=0;i<500;i++){
    str+='你是dd吗？\n';
}

var  WriteStream=fs.createWriteStream('./data/1.txt');

WriteStream.write(str);

// 标记文件末尾
WriteStream.end();

WriteStream.on('finish',()=>{
    console.log('写入完成');
})
```

> 管道流

```js
const fs=require('fs');
var readStream=fs.createReadStream('./1.jpg');
var  WriteStream=fs.createWriteStream('./data/1.jpg');

readStream.pipe(WriteStream);
```

题目：

1.判断服务器上面有没有upload目录。如果没有创建这个目录，如果有的话不做操作。

```js
const fs=require('fs');
var path='./upload';

fs.stat(path,(err,date)=>{
    if(err){
        mkdir(path);
    }
    if(date.isDirectory()){
        console.log('upload目录存在');
    }else{
        // 首先删除文件，创建目录
        fs.unlink(path,(err)=>{
            if(!err){
                mkdir(path);
            }else{
                console.log('请检查传入数据是否正确');
            }
        })
        
    }
})

function mkdir(dir){
    fs.mkdir(dir,(err)=>{
        if(err){
            console.log(err);
        }
    });
}
```

*2.找出xxx文件夹下面的所有目录，把文件夹加放在一个数组里*

![image-20210326163815674](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210326163815674.png)

> 因为异步，导致先console.log输出了，而数组还没有执行，最好用递归解决

![image-20210326163958888](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210326163958888.png)

### ES6新特性

*1. let const*

*let块作用域*

*2.箭头函数*

```js
run(function(){
    console.log('执行');
})
//等于
run(()=>{
    console.log('执行');
})
```

*3.对象、属性的简写*

```js
var name='张三';
var app={
    name,    //属性名和变量一样可以简写
    run(){
        console.log(`${name}在跑步`);
    }
}
app.run();
console.log(app.name)
```

*4.模板字符串*

```js
var name='张三';
var age=20;
console.log(`${name}的年龄是${age}`);
```

*5.Promise*

> *Promise来处理异步  resolve 成功的回调函数  reject失败的回调函数*

```js
var p=new Promise(function(resolve,reject){
    setTimeout(function(){
        var name='张三';
        resolve(name);
        },1000);
})

p.then((date)=>{
    console.log(date);
})
```

> 回调本质

```js
function getData(ca11bck){
    //ajax
    setTimeout(function(){
    var name='张三';
    ca11bck(name);
    },1000);
}

getData((aaa)=>{
    console.log(aaa);
})
```

6.*await*

> await在等待async方法执行完毕，其实await等待的只是-一个表达式，这个表达式在官方文档里说的是Promise对象，但是它也可以接受普通值。

`注意`:await必须在async方法中才可以使用因为await问本身就会造成程序停正堵塞，所以必须在异步方法中才可以使用。

```js
async function test(){
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            var name='张三 222';
            resolve(name);
        },1000);
    })
}

async function main(){
    var date=await test();  //获取异步方法里面的数据
    console.log(date);      //await必须用在async异步方法里
}

main();
```

## 4、用node.js创建一个静态web服务器

### 1、创建服务器

Web 服务器一般指网站服务器，是指驻留于因特网上某种类型计算机的程序，可以向浏览器等 Web 客户端提供文档，也可以放置网站文件让全世界浏览，还可以放置数据文件，让全世界下载。目前最主流的 Web 服务器有 Apache 、Nginx 、 IIS 等

> 接下来我们使用 http.createServer() 方法创建服务器，并使用 listen 方法绑定 3000 端口。函数通过 request, response 参数来接收和响应数

> app.js

```js
const http = require('http');
const fs = require('fs');
const common=require('./module/common.js');
const path=require('path');
const url=require('url');

http.createServer(function (req, res) {
    // 1、获取地址
    let pathname=url.parse(req.url).pathname;
    pathname=pathname=='/'?'/index.html':pathname;
    // 后去后缀名path.extname()
    let extname=path.extname(pathname);

    // 2、通过fs模块读取文件
    if(pathname!='/favicon.ico'){
        fs.readFile('./static'+pathname,async(err,data)=>{ //异步方法
            if(err){
                res.writeHead(404, {
                    'Content-Type': 'text/html;charset="utf-8"'
                });
                res.end('404');
            }
            let mime = await common.getFilename(extname);
            res.writeHead(200, {
            'Content-Type': ''+mime+';charset="utf-8"'
            });
            res.end(data);
        })
    }
    
}).listen(3000);

console.
log('Server running at http://127.0.0.1:3000/');
```

> common.js

```js
var fs = require('fs')

exports.getMime=(extname)=>{
    switch(extname){
        case '.html':
            return 'text/html';
        case '.css':
            return 'text/css';
        case '.js':
            return 'text/javascript';
        default:
            return 'text/html';            
    }
}


exports.getFilename = function(extname){	//读取mime.json里的后缀
    return new Promise((resolve,reject)=>{
        fs.readFile('./data/mime.json',(err,data)=>{	//目录是相对于app.js
            if(err){
                console.log(err);
                reject(err);
                return;
            }
            let mimeObj=JSON.parse(data.toString());
            resolve(mimeObj[extname]);
        })
    })
}
```

> 由于读取mime.json文件是异步的，所以需要用readFileSync()把它变成同步。
> 由于data是文件，所以要先把内容转换成字符串再变成JSON格式

也可以使用同步方法（必须要等待读取完才能进行下一步）

```js
exports.getFilename = function(extname){ 
    var data = fs.readFile('./data/mime.json'); //同步方法
    let mimeObj=JSON.parse(data.toString());
    resolve(mimeObj[extname]);
}
```

### 2、 Nodejs 封装静态 web

```js
const http = require('http');
const routes = require('./module/routes');

http.createServer(function (req, res) {
    // 创建web服务
    routes.static(req,res,'static');
}).listen(3000);
```

```js
const fs = require('fs');
const path=require('path');
const url=require('url');

//封装成私有方法
let getFilename = function(extname){ 
    var data = fs.readFileSync('./data/mime.json'); //同步方法
    let mimeObj=JSON.parse(data.toString());
    return mimeObj[extname];
}

exports.static = function(req,res,staticPath){ 
    let pathname=url.parse(req.url).pathname;
    pathname=pathname=='/'?'/index.html':pathname;
    // 后去后缀名path.extname()
    let extname=path.extname(pathname);

    // 通过fs模块读取文件
    if(pathname!='/favicon.ico'){
        fs.readFile('./'+staticPath+pathname,(err,data)=>{
            if(err){
                res.writeHead(404, {
                    'Content-Type': 'text/html;charset="utf-8"'
                });
                res.end('404');
            }
            let mime = getFilename(extname);
            res.writeHead(200, {
            'Content-Type': ''+mime+';charset="utf-8"'
            });
            res.end(data);
        })
    }
}
```

### 2、 路由

官方解释：
	路由（Routing）是由一个 URI（或者叫路径）和一个特定的 HTTP 方法（GET、POST 等）组成的，涉及到应用如何响应客户端对某个网站节点的访问。
通俗的说：
	路由指的就是针对不同请求的 URL，处理不同的业务逻辑。

​																									**Get 请求路由示**

![image-20210328230533040](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210328230533040.png)

```js
//路由
    let pathname=url.parse(req.url).pathname;
    let extname = path.extname(pathname);
    if(!extname){ //如果有请求地址有后缀名的话让静态web服务去处理 
        if(pathname=='/login'){
            res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
            res.end("执行登录");
        }else if(pathname=='/register'){
            res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
            res.end("执行注册");
        }else if(pathname=='/admin'){
            res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
            res.end("处理后的业务逻辑");
        }else{
            res.writeHead(404, { 'Content-Type': 'text/html;charset="utf-8"' });
            res.end("404");
        }
    }
```

```js
exports.static = function (req, res, staticPath) {
    //1、获取地址
    let pathname = url.parse(req.url).pathname;
    let extname = path.extname(pathname);
    if (extname) {  //如果有后缀名让静态web处理 否则路由处理
        //2、通过fs模块读取文件
        if (pathname != '/favicon.ico') {
            try {
                let data = fs.readFileSync('./' + staticPath + pathname);
                if (data) {
                    let mime = getFileMime(extname);
                    res.writeHead(200, { 'Content-Type': '' + mime + ';charset="utf-8"' });
                    res.end(data);
                }
            } catch (error) {
                console.log(error)
            }
        }
    }
}
```

### 3、 初识 EJS 模块引擎

我们学的 EJS 是后台模板，可以把我们数据库和文件读取的数据显示到 Html 页面上面。它是一个第三方模块，需要通过 npm 安装
https://www.npmjs.com/package/ejs

EJS 常用标签

- <% %>流程控制标签（写js的代码）
- <%= %>输出标签（原文输出 HTML 标签）
-  <%- %>输出标签（HTML 会被浏览器解

```js
const ejs = require('ejs');		//要先下载好ejs和引入

if(pathname=='/login'){
            let msg = "数据库里面获得的数据";
            let list = [
                {
                    title: '新闻111'
                },
                {
                    title: '新闻222'
                },
                {
                    title: '新闻3333'
                },
                {
                    title: '新闻4444'
                }, {
                    title: '新闻5555'
                }
            ]
			
            //(渲染到什么地方，渲染的数据，返回的数据)
            ejs.renderFile('./views/login.ejs',{
                msg:msg,
                list:list
            },(err,data)=>{
                res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
                res.end(data);
            })
        }
```

> ejs

```ejs
<h2>登入页面</h2>

    <h3><%=msg%></h3>
    <br>

    <ul>
        <%for(var i=0;i<list.length;i++){%>
        <li><%=list[i].title%></li>
        <%}%>
    </ul>
```

### 4、 Get、Post

超文本传输协议（HTTP）的设计目的是保证客户端机器与服务器之间的通信。在客户端和服务器之间进行请求-响应时，两种最常被用到的方法是：GET 和 POST。GET - 从指定的资源请求数据。（一般用于获取数据）POST - 向指定的资源提交要被处理的数据。（一般用于提交数据）

路由：

- 请求方法

- 请求路径
- 请求处理函数

get:

```javascript
//当你以get方法请求/的时候，执行对应的处理函数
app.get('/',function(req,res){
    res.send('hello world');
})
```

post:

```javascript
//当你以post方法请求/的时候，执行对应的处理函数
app.post('/',function(req,res){
    res.send('hello world');
})
```

```js
	// 获取请求类型
    console.log(req.method);
    if(!extname){ //如果有请求地址有后缀名的话让静态web服务去处理 
        if(pathname=='/news'){
            // 获得get传值
            var query = url.parse(req.url,true).query;
            console.log(query);
            res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
            res.end('get传值成功');
        }else if (pathname == '/login') {
            //post演示
            ejs.renderFile("./views/form.ejs", {}, (err, data) => {
                res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
                res.end(data)
            })

        }else if(pathname=='/doLogin'){
            // 获得post传值
            let postData = '';
            req.on('data',(chunk)=>{
                postData+=chunk;
            })
            req.on('end',()=>{
                console.log(postData);
                res.end(postData);
            })
        }else{
            res.writeHead(404, { 'Content-Type': 'text/html;charset="utf-8"' });
            res.end("404");
        }
    }
```

### 5、模块化的方式封装

```js
let app = {
    static: (req, res, staticPath) => {
        //1、获取地址
        let pathname = url.parse(req.url).pathname;
        let extname = path.extname(pathname);
        if (extname) { //如果有后缀名让静态web处理 否则路由处理
            //2、通过fs模块读取文件
            if (pathname != '/favicon.ico') {
                try {
                    let data = fs.readFileSync('./' + staticPath + pathname);
                    if (data) {
                        let mime = getFileMime(extname);
                        res.writeHead(200, {
                            'Content-Type': '' + mime + ';charset="utf-8"'
                        });
                        res.end(data);
                    }
                } catch (error) {
                    console.log(error)
                }
            }
        }
    },
    login: (req, res) => {
        ejs.renderFile('./views/form.ejs', {}, (err, data) => {
            res.writeHead(200, {
                'Content-Type': 'text/html;charset="utf-8"'
            });
            res.end(data)
        })
    },
    news: (req, res) => {
        res.end('news');
    },
    doLogin: (req, res) => {
        //获取post传值        
        let postData = '';
        req.on('data', (chunk) => {
            postData += chunk;
        })
        req.on('end', () => {
            console.log(postData);
            res.end(postData);
        })
    },
    error: (req, res) => {
        res.end('404');
    }
}

module.exports = app;
```

```js
	//路由
    let pathname=url.parse(req.url).pathname.replace("/","");//去掉'/new'的'/'
    // 获取请求类型
    try {
        routes[pathname](req, res);
    } catch (error) {
        routes['error'](req, res);
    }
```

### 6、封装一个类似 express 框架的路由

 **路由设计**

| 路由            | 方法 | get参数 | post参数                | 是否需要登录 | 备注         |
| --------------- | ---- | ------- | ----------------------- | ------------ | ------------ |
| /               | get  |         |                         |              | 渲染首页     |
| /register(登录) | get  |         |                         |              | 渲染注册页面 |
| /register       | post |         | email,nickname,password |              | 处理注册请求 |
| /login          | get  |         |                         |              | 渲染登陆界面 |
| /login          | post |         | email,password          |              | 处理登录请求 |
| /loginout       | get  |         |                         |              | 处理退出请求 |
|                 |      |         |                         |              |              |

> route.js

```js
//封装get方法
const url= require("url");

let G={};

let app=function(req,res){
    let pathname=url.parse(req.url).pathname;
    if(G[pathname]){
        G[pathname](req,res);  //执行方法
    }else{
        res.writeHead(404, { 'Content-Type': 'text/html;charset="utf-8"' });
        res.end('页面不存在');
    }
}
app.get=function(str,cb){   //封装get方法
    //注册方法
    G[str]=cb;  
}
module.exports=app;
```

> expreess_router

```js
const http = require("http");
const app=require('./module/route')

//注册web服务
http.createServer(app).listen(3000);

//配置路由
app.get('/',function(req,res){
    res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
    res.end('首页');
})
//配置路由
app.get('/login',function(req,res){
    res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
    res.end('执行登录操作');
})
//配置路由
app.get('/news',function(req,res){
    res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
    res.end('新闻页面');
})
```

#### get和post的封装

> app.js

```js
const http = require("http");
const app=require('./module/route');
const ejs = require("ejs");

//注册web服务
http.createServer(app).listen(3000);

//配置路由
app.get('/',function(req,res){
    res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
    res.end('首页');
})
//配置路由
app.get('/login',function(req,res){
    // res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
    // res.end('执行登录操作');
    ejs.renderFile("./views/form.ejs",{},(err,data)=>{
        res.send(data)
    })
})

app.post('/doLogin',function(req,res){
    console.log(req.body);
    res.send(req.body)
})
```

> route.js

```js
const url = require("url");

function changeRes(res) {   //封装res方法
    res.send = (data) => {
        res.writeHead(200, {
            'Content-Type': 'text/html;charset="utf-8"'
        });
        res.end(data);
    }
}

let server = () => {
    let G = {};
    //把get 和 post分开
    G._get = {};
    G._post = {};
    let app = function (req, res) {
        //扩展res的方法
        changeRes(res);
        let pathname = url.parse(req.url).pathname;
        //获取请求类型
        let method = req.method.toLowerCase();
        console.log(method)
        if (G['_' + method][pathname]) {
            if (method == "get") {
                G['_' + method][pathname](req, res); //执行方法
            } else {
                //post  获取post的数据 把它绑定到req.body
                let postData = '';
                req.on('data', (chunk) => {
                    postData += chunk;
                })
                req.on('end', () => {
                    req.body = postData;
                    G['_' + method][pathname](req, res); //执行方法
                })
            }
        } else {
            res.writeHead(404, {
                'Content-Type': 'text/html;charset="utf-8"'
            });
            res.end('页面不存在');
        }
    }
    app.get = function (str, cb) {
        //注册方法
        G._get[str] = cb;
    }
    app.post = function (str, cb) {
        //注册方法
        G._post[str] = cb;
    }

    return app;
}
module.exports = server(); 
```

#### 静态web服务

> app.js

```js
const http = require("http");
const app=require('./module/route');
const ejs = require("ejs");

//注册web服务
http.createServer(app).listen(3000);

app.static("static");    //修改默认静态web目录

//配置路由
app.get('/',function(req,res){
    res.send("首页")
})

//配置路由
app.get('/login',function(req,res){
    // res.writeHead(200, { 'Content-Type': 'text/html;charset="utf-8"' });
    // res.end('执行登录操作');
    ejs.renderFile("./views/form.ejs",{},(err,data)=>{
        res.send(data)
    })
})

app.post('/doLogin',function(req,res){
    console.log(req.body);
    res.send(req.body)
})
```

> route.js

```js
const fs = require('fs');
const path = require('path');
const url = require('url');

//扩展res
function changeRes(res) {
    res.send = (data) => {
        res.writeHead(200, {
            'Content-Type': 'text/html;charset="utf-8"'
        });
        res.end(data);
    }
}

//根据后缀名获取文件类型
function getFileMime(extname) {
    var data = fs.readFileSync('./data/mime.json'); //同步方法
    let mimeObj = JSON.parse(data.toString());
    return mimeObj[extname];
}
//静态web服务的方法
function initStatic(req, res, staticPath) {

    //1、获取地址
    let pathname = url.parse(req.url).pathname;
    // pathname = pathname == '/' ? '/index.html' : pathname;
    let extname = path.extname(pathname);
    //2、通过fs模块读取文件

    if (extname) { //如果有后缀名用静态web服务处理
        try {
            let data = fs.readFileSync('./' + staticPath + pathname);
            if (data) {
                let mime = getFileMime(extname);
                res.writeHead(200, {
                    'Content-Type': '' + mime + ';charset="utf-8"'
                });
                res.end(data);
            }
        } catch (error) {

            console.log(error);
        }
    }

}

let server = () => {
    let G = {
        _get: {},
        _post: {},
        staticPath: 'static' //，默认静态web目录
    };


    let app = function (req, res) {
        //扩展res的方法
        changeRes(res);
        //配置静态web服务
        initStatic(req, res, G.staticPath);

        let pathname = url.parse(req.url).pathname;
        //获取请求类型
        let method = req.method.toLowerCase();
        console.log(method);
        let extname = path.extname(pathname);
        if (!extname) { //如果有后缀名用静态web处理
            if (G['_' + method][pathname]) {
                if (method == "get") {
                    G['_' + method][pathname](req, res); //执行方法
                } else {
                    //post  获取post的数据 把它绑定到req.body
                    let postData = '';
                    req.on('data', (chunk) => {
                        postData += chunk;
                    })
                    req.on('end', () => {
                        req.body = postData;
                        G['_' + method][pathname](req, res); //执行方法
                    })

                }

            } else {
                res.writeHead(404, {
                    'Content-Type': 'text/html;charset="utf-8"'
                });
                res.end('页面不存在');
            }
        }
    }
    //get请求
    app.get = function (str, cb) {
        //注册方法
        G._get[str] = cb;
    }
    //post请求
    app.post = function (str, cb) {
        //注册方法
        G._post[str] = cb;
    }
    //配置静态web服务目录
    app.static = function (staticPath) {
        G.staticPath = staticPath;
    }

    return app;
}
module.exports = server();
```

## 5、MongoDB数据库

### 关系型和非关系型数据库

#### 关系型数据库（表就是关系，或者说表与表之间存在关系）。

- 所有的关系型数据库都需要通过`sql`语言来操作
- 所有的关系型数据库在操作之前都需要设计表结构
- 而且数据表还支持约束
  - 唯一的
  - 主键
  - 默认值
  - 非空

#### 非关系型数据库

- 非关系型数据库非常的灵活
- 有的关系型数据库就是key-value对儿
- 但MongDB是长得最像关系型数据库的非关系型数据库
  - 数据库 -》 数据库
  - 数据表 -》 集合（数组）
  - 表记录 -》文档对象

一个数据库中可以有多个数据库，一个数据库中可以有多个集合（数组），一个集合中可以有多个文档（表记录）

```javascript
{
    qq:{
       user:[
           {},{},{}...
       ]
    }
}
```



- 也就是说你可以任意的往里面存数据，没有结构性这么一说

**NoSQL 数据库在以下的这几种情况下比较适用：**

1. 数据模型比较简单；
2. 需要灵活性更强的 IT 系统；
3. 对数据库性能要求较；

4. 不需要高度的数据一致性；
5. 对于给定 key，比较容易映射复杂值的环境

**NoSql 和传统数据库简单对比**

![image-20210330135731020](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210330135731020.png)

### 1、MongoDb 介绍

MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像
关系数据库的 NoSql 数据库。他支持的数据结构非常松散，是类似 json 的 bson 格式，因此可以存储比较复
杂的数据类型。Mongodb 最大的特点是他支持的查询语言非常强大，其语法有点类似于面向对象的查询语
言，几乎可以实现类似关系数据库单表查询的绝大部分功能，而且还支持对数据建立索引。它的特点是高
性能、易部署、易使用，存储数据非常方便

### 2、数据库基本操作

启动mongodb服务

```
mongod --dbpath C:\MongoDB\data\db
```



1. 清屏

   ```
   cls
   ```

2. 查看所有数据库列表

   ```js
   show dbs
   ```
   
3. 使用（创建）数据库

   ```js
   use itying
   ```

   如果真的想把这个数据库创建成功，那么必须插入一个数据。
   数据库中不能直接插入数据，只能往集合(collections)中插入数据。下面命令表示给 itying 数
   据库的 user 表中插入数据。

4. 查看当前连接的数据库

   ```js
   db
   ```


5. 显示当前的数据集合（mysql 中叫表）

   ```js
   show collections
   ```


6. 删除集合，删除指定的集合 删除表

   ```js
   db.user.drop()	//删除user这个集合
   ```


7. 删除数据库，删除当前所在的数据库

   ```js
   db.dropDatabase();
   ```


8. 插入（增加）数据

   ```js
   db.表名.insert({"name":"zhangsan","age":20,status:1})
   ```


9. 查询当前数据库的所有数据集合

   ```js
   db.user.find();
   ```


10. 查询去掉后的当前聚集集合中的某列的重复数据

    ```js
    db.user.distinct("name");
    ```


11. 查询指定条件的数据

    ```js
    db.user.find({"age":22});	//查询年龄为22岁的数据
    ```

12. 查询大于小于等于的数据

    ```js
    db.user.find({age:{$gt:22}});	//大于
    db.user.find({age:{$lt:22}});	//小于
    db.user.find({age:{$gte:22}});	//大于等于
    db.user.find({age:{$lte:22}});	//小于等于
    ```


13. 查询多个条件的数据

    ```js
    db.user.find({age: {$gte: 23, $lte: 26}};
    ```


14. 简单模糊搜索

    ```js
    db.user.find({name:/mongo/};
    ```


15. 查询表中以 xx 开头或者结尾的

    ```js
    db.user.find({name: /^mongo/}	//开头
    db.user.find({name: /mongo$/}	//结尾         
    ```


16. 查询指定列数据

    ```js
    db.user.find({},{name: 1, age: 1});	//查询所有行的名字和年龄
    ```


17. 排序

    ```js
    db.user.find().sort({age: 1});	//升序
    db.user.find().sort({age: -1});	//降序
    ```


18. 显示列数据限制

    ```js
    db.user.find().limit(5);	//前5个数
    db.user.find().skip(10);	//跳过10个数
    ```
    
    可用于分页，limit 是 pageSize，skip 是(page-1)*pageSize
    
19. 查询某个结果集的记录条数 统计数量

    ```js
    db.user.find({age: {$gte: 25}}).count();
    ```

20. or 与 查询

    ```js
    db.user.find({$or: [{age: 22}, {age: 25}]});
    ```
    
21. 修改数据

    ```js
     db.student.update({"name":"小明"},{$set:{"age":16}});	//前面查找数据，后面修改数据
    
     db.student.update({"name":"小明"},{"age":16});			//完整替换，不出现$set 关键字了：
    
     db.student.update({"sex":"男"},{$set:{"age":33}},{multi: true});	//修改符合条件的多条数据
    ```

22. 删除数据

    如删除集合下全部文档：

    ```
    db.inventory.deleteMany({})
    ```

    删除 status 等于 A 的全部文档：

    ```
    db.inventory.deleteMany({ status : "A" })
    ```

    删除 status 等于 D 的一个文档：

    ```sql
    db.inventory.deleteOne( { status: "D" } )
    ```

### 3、索引

#### 	一、索引基础

​	索引是对数据库表中一列或多列的值进行排序的一种结构，可以让我们查询数据库变得更快。MongoDB 的索引几乎与传统的关系型数据库一模一样，这其中也包括一些基本的查询优化技巧。

- 创建索引命令：

  >  数字 1 表示 username 键的索引按升序存储，-1 表示 age 键的索引按照降序方式存

  ```sql
  db.user.ensureIndex({"userame":1});
  ```

- 获得当前索引命令：

  ```sql
  db.user.getIndexes()
  ```

- 删除索引命令：

  ```sql
  db.user.dropIndex({"username":1})
  ```

**复合索引**

> 该索引被创建后，基于 username 和 age 的查询将会用到该索引，或者是基于 username的查询也会用到该索引，但是只是基于 age 的查询将不会用到该复合索引。因此可以说，如果想用到复合索引，必须在查询条件中包含复合索引中的前 N 个索引列。然而如果查询条件中的键值顺序和复合索引中的创建顺序不一致的话，MongoDB 可以智能的帮助我们调整该顺序，以便使复合索引可以为查询所用。

```sql
db.user.ensureIndex({"username":1, "age":-1})
```

**可以在创建索引时为其指定索引名**

```sql
db.user.ensureIndex({"username":1},{"name":"userindex"})
```

#### 二、唯一索引

​	**创建唯一索引**

> 如果再次插入 userid 重复的文档时，MongoDB 将报错，以提示插入重复键；
>
> 如果插入的文档中不包含 userid 键，那么该文档中该键的值为 null，如果多次插入类似的文档，MongoDB 将会报出同样的错误。

```sql
db.user.ensureIndex({"userid":1},{"unique":true})
```

### 4、管理员权限

1、创建超级管理用户

```sql
use admin
db.createUser({
user:'admin', pwd:'123456', roles:[{role:'root',db:'admin'}]
})
```

2、修改 Mongodb 数据库配置文件

```sql
security:
    authorization: enabled
```

3、重启 mongodb 服务

![image-20210331000826008](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210331000826008.png)	

4、用超级管理员账户连接数据库

```sql
mongo admin -u 用户名 -p 密码

mongo 192.168.1.200:27017/test -u user -p password
```

5、给 eggcms 数据库创建一个用户 只能访问 eggcms 不能访问其他数据库

```sql
use eggcms
db.createUser({
user: "eggadmin", pwd: "123456", roles: [ { role: "dbOwner", db: "eggcms" } ]
})
```

`Mongodb 账户权限配置中常用的命令`

```sql
show users;			#查看当前库下的用户
db.dropUser("eggadmin") 	#删除用户
db.updateUser( "admin",{pwd:"password"}); #修改用户
db.auth("admin","password"); #密码认证
```

`Mongodb 数据库角色`
1.数据库用户角色：read、readWrite;
2.数据库管理角色：dbAdmin、dbOwner、userAdmin；
3.集群管理角色：clusterAdmin、clusterManager、clusterMonitor、hostManager；
4.备份恢复角色：backup、restore；
5.所有数据库角色：readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、
dbAdminAnyDatabase
6.超级用户角色：root

`连接数据库的时候需要配置账户密码`

```js
const url = 'mongodb://admin:123456@localhost:27017/';
```

### 简述关系数据库中表与表的 3 种关系

1）一对一的关系例如：一个人对应一个唯一的身份证号，即为一对一的关系。

2）一对多关系例如：一个班级对应多名学生，一个学生只能属于一个班级，即为一对多关

3）多对多关系例如：一个学生可以选多门课程，而同一门课程可以被多个学生选修，彼此的对应关即是多对多

![image-20210331211549142](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210331211549142.png)

### MongoDB 的高级查询 aggregate 聚合管道

#### 一、MongoDB 聚合管道（Aggregation Pipeline）

使用聚合管道可以对集合中的文档进行变换和组合。实际项目：表关联查询、数据的统计。MongoDB 中使用 db.COLLECTION_NAME.aggregate([{< stage >},...]) 方法来构建和使用聚合管道。先看下官网给的实例，感受一下聚合管道的用法

![image-20210331214424853](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210331214424853.png)

#### 二、MongoDB Aggregation 管道操作符与表达式

| 管道操作符 |                      Descripti                       |
| :--------: | :--------------------------------------------------: |
|  $project  |                增加、删除、重命名字段                |
|  $project  |      条件匹配。只满足条件的文档才能进入下一阶段      |
|   $limit   |                    限制结果的数量                    |
|   $skip    |                    跳过文档的数量                    |
|   $sort    |                       条件排序                       |
|   $group   |                  条件组合结果 统计                   |
|  $lookup   | $lookup 操作符 用以引入其它集合的数据 （表关联查询） |

**管道表达式:**

管道操作符作为“键”,所对应的“值”叫做管道表达式。
例如`如{$match:{status:"A"}}，$match`称为管道操作符，而 status:"A"称为管道表达式，是管道操作符的操作数(Operand)。
每个管道表达式是一个文档结构，它是由字段名、字段值、和一些表达式操作符组成的。

![image-20210331215037303](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210331215037303.png)

##### $project

> 修改文档的结构，可以用来重命名、增加或删除文档中的字段。

```sql
db.order.aggregate([
{
$project:{ trade_no:1, all_price:1 }
}
])
```

##### $match

> 用于过滤文档。用法类似于 find() 方法中的参数

```sql
db.order.aggregate([
{
$project:{ trade_no:1, all_price:1 }
}, {
$match:{"all_price":{$gte:90}}
}
])
```

##### $group

> 将集合中的文档进行分组，可用于统计结果。
> 统计每个订单的订单数量，按照订单号分组

```sql
db.order_item.aggregate([
{
$group: {_id: "$order_id", total: {$sum: "$num"}}
}
])
```

##### $sort

> 将集合中的文档进行排序

```sql
db.order.aggregate([
{
$project:{ trade_no:1, all_price:1 }
}, {
$match:{"all_price":{$gte:90}}
}, {
$sort:{"all_price":-1}
}
])
```

##### $limit

> 限制数据数目

```sql
db.order.aggregate([
{
$project:{ trade_no:1, all_price:1 }
}, {
$match:{"all_price":{$gte:90}}
}, {
$sort:{"all_price":-1}
}, {
$limit:1
}
])
```

##### $skip

> 跳过数据

```sql
db.order.aggregate([
{
$project:{ trade_no:1, all_price:1 }
}, {
$match:{"all_price":{$gte:90}}
}, {
$sort:{"all_price":-1}
},
{
$skip:1
}
])
```

##### $lookup

> 表关联

```sql
db.order.aggregate([
{
$lookup:
{
from: "order_item",		//连接哪一个表
localField: "order_id", foreignField: "order_id", as: "items"	
//			当前的连接列					要连接表的连接列	放到什么地方（名字）
}
}
])
```

结果：

```sql
{
	"_id": ObjectId("5b743d8c2c327f8d1b360540"),
	"order_id": "1",
	"uid": 10,
	"trade_no": "111",
	"all_price": 100,
	"all_num": 2,
	"items": [{
		"_id": ObjectId("5b743d9c2c327f8d1b360543"),
		"order_id": "1",
		"title": "商品鼠标1",
		"price": 50,
		"num": 1
	}, {
		"_id": ObjectId("5b743da12c327f8d1b360544"),
		"order_id": "1",
		"title": "商品键盘2",
		"price": 50,
		"num": 1
	}, {
		"_id": ObjectId("5b74f457089f78dc8f0a4f3b"),
		"order_id": "1",
		"title": "商品键盘3",
		"price": 0,
		"num": 1
	}]
} {
	"_id": ObjectId("5b743d902c327f8d1b360541"),
	"order_id": "2",
	"uid": 7,
	"trade_no": "222",
	"all_price": 90,
	"all_num": 2,
	"items": [{
		"_id": ObjectId("5b743da52c327f8d1b360545"),
		"order_id": "2",
		"title": "牛奶",
		"price": 50,
		"num": 1
	}, {
		"_id": ObjectId("5b743da92c327f8d1b360546"),
		"order_id": "2",
		"title": "酸奶",
		"price": 40,
		"num": 1
	}]
} {
	"_id": ObjectId("5b743d962c327f8d1b360542"),
	"order_id": "3",
	"uid": 9,
	"trade_no": "333",
	"all_price": 20,
	"all_num": 6,
	"items": [{
		"_id": ObjectId("5b743dad2c327f8d1b360547"),
		"order_id": "3",
		"title": "矿泉水",
		"price": 2,
		"num": 5
	}, {
		"_id": ObjectId("5b743dff2c327f8d1b360548"),
		"order_id": "3",
		"title": "毛巾",
		"price": 10,
		"num": 1
	}]
}
```

#### MongoDB 备份(mongodump)与恢复(mongorestore)

```sql
>mongodump -h dbhost -d dbname -o dbdirectory
```

- -h：

  MongoDB 所在服务器地址，例如：127.0.0.1，当然也可以指定端口号：127.0.0.1:27017

- -d：

  需要备份的数据库实例，例如：test

- -o：

  备份的数据存放位置，例如：c:\data\dump，当然该目录需要提前建立，在备份完成后，系统自动在dump目录下建立一个test目录，这个目录里面存放该数据库实例的备份数据。

```sql
>mongorestore -h <hostname><:port> -d dbname <path>
```

- --host <:port>, -h <:port>：

  MongoDB所在服务器地址，默认为： localhost:27017

- --db , -d ：

  需要恢复的数据库实例，例如：test，当然这个名称也可以和备份时候的不一样，比如test2

- --drop：

  恢复的时候，先删除当前数据，然后恢复备份的数据。就是说，恢复后，备份后添加修改的数据都会被删除，慎用哦！

- <path>：

  mongorestore 最后的一个参数，设置备份数据所在位置，例如：c:\data\dump\test。

  你不能同时指定 <path> 和 --dir 选项，--dir也可以设置备份目录。

- --dir：

  指定备份的目录

  你不能同时指定 <path> 和 --dir 选项。

### node.js操作mongodb数据库

1、查找数据

```js
db.collection("user").find({}).toArray((err,data)=>{
        console.log(data);
        // 关闭数据库
        client.close();
    })
```

2、增加数据

```js
db.collection("user").insertOne({"username":"nodejs操作mongodb","age":10},(err,result)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log("增加成功");
        console.log(result);
        client.close();
    })
```

3、修改数据

```js
db.collection("user").updateOne({"username":"zhangsan"},{$set:{"age":10}},(err,result)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log("修改成功");
        console.log(result);
        client.close();
    })
```

4、删除一条数据

```js
 db.collection("user").deleteOne({"username":"zhangsan"},(err)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log("删除一条成功");
        client.close();
    })
```

 5、删除多条数据

```js
b.collection("user").deleteMany({"username":"zhangsan"},(err)=>{
        if(err){
            console.log(err);
            return;
        }
        console.log("删除多条成功");
        client.close();
    })
```



6、通过ejs显示列表，和表单增加数据库数据

```js
const http = require("http");
const app = require('./module/route');
const ejs = require("ejs");
const querystring = require('querystring');//引用querystring处理string成对象，方便加入数据库
const { MongoClient } = require('mongodb');
const url = 'mongodb://localhost:27017';
const dbName = 'itying';
// const client = new MongoClient(url,{ useUnifiedTopology: true });
//注册web服务
http.createServer(app).listen(3000);
// app.static("public");    //修改默认静态web目录
//配置路由
app.get('/', function (req, res) {

    MongoClient.connect(url,{ useUnifiedTopology: true }, (err, client) => {	//分离数据库，方便执行一个命令关闭数据库后再执行另一个命令
        
        if (err) {
            console.log(err);
            return;
        }
        let db = client.db(dbName);

        //查询数据
        db.collection("user").find({}).toArray((err, result) => {
            if (err) {
                console.log(err);
                return;
            }            
            client.close();
            ejs.renderFile("./views/index.ejs", {
                list: result
            }, (err, data) => {
                res.send(data);
            })
        })

    })


})


app.get('/register', function (req, res) {
    ejs.renderFile("./views/register.ejs",{},(err,data)=>{	//渲染ejs
        res.send(data);
    })
})

app.post('/doRegister', function (req, res) {
    // name=zhangsan&age=13
    // {
    //     "name":"zhangsan",
    //     "age":13
    // }    
    let body=querystring.parse(req.body);
    MongoClient.connect(url,{ useUnifiedTopology: true },(err,client)=>{

        if(err){
            console.log(err);
            return;
        }
        let db=client.db(dbName);

        db.collection("user").insertOne(body,(err,result)=>{
            if(err){
                console.log(err);
                return;
            }
            console.log("增加数据成功");
            res.send("增加数据成功");
        })
    })
})
```



## 6、Express

### 基本使用

1. npm安装express

   ```
   cnpm install express
   ```

   

2. 引入express

   ```js
   const express = require('express');
   const app = express();
   ```

   

3. 多种路由

   ```js
   app.get('/', function (req, res) {      //显示数据
       res.send('Hello World')
   })
   app.post('/post', function (req, res) {     //增加数据
       console.log("增加数据");
       res.send("增加数据");
   })
   
   app.put('/put', function (req, res) {  //修改数据
       console.log("修改数据");
       res.send("修改数据");
   })
   
   app.delete('/delete', function (req, res) {  //删除数据
       console.log("删除数据");   
       res.send('删除数据');
   })  
   
   // 配置路由多级目录
   app.get('/news/user', function (req, res) {      
       res.send('Hello World')
   })
   ```

   

4. 动态路由

   ```js
   // 动态路由，注意顺序
   app.get('/news/:id', function (req, res) {    
       var id =req.params["id"];       //获取动态路由
       res.send('动态路由'+id);
   })
   ```

   

5. get传值

   ```js
   // get 传值
   app.get('/product', function (req, res) {    
       var query = req.query;      //获取get传值
       console.log(query)
       res.send(query.id);
   })
   ```

   

### Express中ejs的使用

> app.js

```js
const express = require('express');
const app = express();
//配置模板引擎
app.set("view engine","ejs")
//配置静态web目录		利用 Express. static 托管静态文件	引用css
app.use(express.static("static"))

app.get("/",(req,res)=>{
    let title = "你好ejs";
    res.render("index",{	//渲染ejs
        title:title
    })
})
app.get("/news",(req,res)=>{
    let userinfo={
        username:"张三",
        age:20
    }
    let article="<h3>我是一个h3</h3>"

    let list=["1111","22222","3333333"]

    let newsList=[
        {
            title:"新闻1111",          
        },
        {
            title:"新闻122222",          
        },
        {
            title:"新闻33331",          
        },
        {
            title:"新闻44444",          
        }
    ]
    res.render("news",{
        userinfo:userinfo,
        article:article,
        flag:true,
        score:60,
        list:list,
        newsList:newsList
    })
})
//监听端口  端口号建议写成3000以上
app.listen(3000)
```

> index.ejs

```ejs
<body>
    <h2>我是一个ejs模板引擎</h2>
    <p><%=title%></p>				//调取app.js里的title
    <%- include('footer.ejs') %>	//引用另一个ejs
</body>
```

> news.ejs

```ejs
<body>
    <h2>绑定数据</h2>
    <p><%=userinfo.username%>---<%=userinfo.age%></p>
    <p><%=article%></p>
    <p><%-article%></p>
    
    <h2>条件判断</h2>
    <%if(flag==true){%>
    <strong>flag=true</strong>
    <%}%>
    <%if(score>=60){%>
    <p>及格</p>
    <%}else{%>
    不及格
    <%}%>
    
    <h2>循环遍历</h2>
    <ul>
        <%for(let i=0;i<list.length;i++){%>
    <li><%=list[i]%></li>
    <%}%>        
    </ul>
    <br>
    <ul>
        <%for(let i=0;i<newsList.length;i++){%>
    <li><%=newsList[i].title%></li>
    <%}%>   
        
    <h2>引入模块</h2>
    </ul>
    <%- include('footer.ejs') %>
</body>
```

### Express 中间件

> 中间件：把很复杂的事情分割成单个，然后依次有条理的执行。就是一个中间处理环节，有输入，有输出。
>
> 说的通俗易懂点儿，中间件就是一个（从请求到响应调用的方法）方法。
>
> 把数据从请求到响应分步骤来处理，每一个步骤都是一个中间处理环节。
>
> 中间件中如果想往下匹配的话，那么需要写 next()

**中间件的功能包括：**

- 执行任何代码。
- 修改请求和响应对象。
- 终结请求-响应循环。
- 调用堆栈中的下一个中间件。

**Express 应用可使用如下几种中间件：**

- 应用级中间件 

  ```js
  // 应用级中间件 (用于权限判断)
  app.use((req,res,next)=>{
      console.log(new Date())
      next();
  })
  ```

- 路由级中间件

  ```js
  // 路由级中间件 (用的比较较少)
  app.get('/news/add', function (req, res,next) {      //显示数据
      console.log("ddd");
      next()
  })
  app.get('/news/:id', function (req, res) {      //显示数据
      res.send('新闻动态路由')
  })
  ```

- 错误处理中间件

  ```js
  // 错误处理中间件(放在最后面)
  app.use((req,res,next)=>{
      res.status(404).send(404);
  })
  ```

- 内置中间件

  ```js
  // 内置中间件	
  app.use(express.static("static"));
  ```

- 第三方中间件

  ```js
  /*
  获取post传过来的数据
  1、cnpm install body-parser --save
  
  2、var bodyParser = require('body-parser')
  
  3、配置中间件
  
      app.use(bodyParser.urlencoded({ extended: false }))
  
      app.use(bodyParser.json())
      
  4、接收post数据
      req.body
  
  */
  
  const express = require("express");
  const bodyParser = require('body-parser')
  const ejs = require("ejs");
  const app = express()
  
  //配置模板引擎
  app.engine("html",ejs.__express)
  app.set("view engine","html")
  //配置静态web目录
  app.use(express.static("static"))
  
  //配置第三方中间件
  app.use(bodyParser.urlencoded({ extended: false }))
  app.use(bodyParser.json())
  
  app.get("/",(req,res)=>{
      res.send("首页")
  })
  
  app.get("/login",(req,res)=>{
     // req.query 获取get传值
     res.render("login",{})
  })
  
  app.post("/doLogin",(req,res)=>{
     // req.body 获取post传值
     var body = req.body;
     console.log(body)
     res.send("执行提交"+body.username)
  })
  
  //监听端口  端口号建议写成3000以上
  app.listen(3000)
  ```

### Express Cookie 的基本使用

#### 一、Cookie 简介

- cookie 是存储于访问者的计算机中的变量。可以让我们用同一个浏览器访问同一个域名的时候共享数据。
-  HTTP 是无状态协议。简单地说，当你浏览了一个页面，然后转到同一个网站的另一个页面，服务器无法认识到这是同一个浏览器在访问同一个网站。每一次的访问，都是没有任何关系的。
-  Cookie 是一个简单到爆的想法：当访问一个页面的时候，服务器在下行 HTTP 报文中，命令浏览器存储一个字符串; 浏览器再访问同一个域的时候，将把这个字符串携带到上行HTTP 请求中。第一次访问一个服务器，不可能携带 cookie。 必须是服务器得到这次请求，在下行响应报头中，携带 cookie 信息，此后每一次浏览器往这个服务器发出的请求，都会携带这个 cookie。 

#### 二、Cookie 特点

- cookie 保存在浏览器本地
-  正常设置的 cookie 是不加密的，用户可以自由看到;
-  用户可以删除 cookie，或者禁用它
-  cookie 可以被篡改
-  cookie 可以用于攻击
-  cookie 存储量很小。未来实际上要被 localStorage 替代，但是后者 IE9 兼容。

```js
1.安装 cnpm instlal cookie-parser --save
2.引入 var cookieParser = require('cookie-parser');
3.设置中间件
app.use(cookieParser());
4.设置 cookie
res.cookie("name",'zhangsan',{maxAge: 900000});
5. 获取 cookie
req.cookies.name
```

Cookie 属性说明:

|  domain  | 正常情况不要设置默认就是当前域下面的所有页面都可以方法       |
| :------: | ------------------------------------------------------------ |
| http0nly | true表示这个cookie只有服务器端可以访问，false表示客户端(js) ，服务器端都可以访问 |
|  singed  | 表示是否签名 cookie, 设为 true 会对这个 cookie 签名，这样就需要用res.signedCookies 而不是 res.cookies 访问它。被篡改的签名 cookie 会被服务器拒绝，并且 cookie 值会重置为它的原始值 |
|  maxAge  | 最大失效时间（毫秒），设置在多少后失效                       |
|   Path   | 表示 cookie 影响到的路路径，如 path=/。如果路径不能匹配时，浏览器则不发送这个 Cookie |

```js
const express = require('express');
var cookieParser = require('cookie-parser')
const app = express();
// 配置cookieParser中间件
app.use(cookieParser("itying"))

app.get('/', function (req, res) {      //显示数据
    // 设置cookie   如果cookie没有过期的话，关闭浏览器后重新打开cookie, cookie不会销毁
    // cookie的名字     cookie的value值     过期时间    设置那一些路由可以访问
   	res.cookie("username","zhansan",{maxAge:1000*60*60,path:"/news"})
    
    // 多域名共享cookie  仅限相同的一级域名   aaa.itying.com  bbb.itying.com
    res.cookie("username","zhansan",{maxAge:1000*60*60,domain:"itying.com"})
    
    // 中文cookie
    res.cookie("username","张三",{maxAge:1000*60*60})
    
    /*
    	cookie加密
        1、配置中间件的时候需要传入加密的参数
        app.use(cookieParser("itying"))
        2、res.cookie("username","张三",{maxAge:1000*60*60,signed:true})
        3、req.signedCookies
    */ 
    res.cookie("username","张三",{maxAge:1000*60*60,signed:true})
    res.send('Hello World')
})
app.get('/news', function (req, res) {
    // 获取cookie
    let username = req.cookies.username;
    res.send('news--'+username)
})
app.get('/user', function (req, res) {      //显示数据
    let username = req.cookies.username;
    res.send('user--'+username)
}) 
app.get('/product', function (req, res) {      //显示数据
    let username = req.signedCookies.username;
    res.send('user--'+username)
}) 
    app.listen(80)
```

### Express Session 的基本使用

#### 一、 Session 简单介绍

session 是另一种记录客户状态的机制，不同的是 Cookie 保存在客户端浏览器中，而session 保存在服务器上。Cookie 数据存放在客户的浏览器上，Session 数据放在服务器上。Session 相比 Cookie 要更安全一些。由于 Session 保存到服务器上，所以当访问量增多的时候，会比较占用服务器的性能。单个 cookie 保存的数据大小不能超过 4K，很多浏览器都限制一个站点最多保存 20个 cookie。Session 没有这方面的限制。Session 是基于 Cookie 进行工作的。 

#### 二、 Session 的工作流程

当浏览器访问服务器并发送第一次请求时，服务器端会创建一个 session 对象，生成一个类似于 key,value 的键值对， 然后将 key(cookie)返回到浏览器(客户)端，浏览器下次再访问时，携带 key(cookie)，找到对应的 session(value)。 

#### 三、 express-session 的使用

```js
const express = require('express');
const app = express();
const session = require('express-session')		//引用session

// 配置session的中间件
app.use(session({
    secret: 'keyboard cat',     //服务器端生成session 的签名
    name:"lyc",         //修改session对应cookie的名称
    resave: false,      //'强制保存session 即使它并没有变化
    saveUninitialized: true,    //强制将未初始化的session 存储
    cookie: {
        maxAge:1000*60,     
        secure: false       //true表示只有https协议才能访问cookie
    },
    rolling:true    //在每次请求时强行设置cookie, 这将重置cookie 过期时间(默认:false)        
}))


app.get('/', function (req, res) { //显示数据
    // 获取session
    if(req.session.username){
        res.send(req.session.username+"-已登入")
    }else{
        res.send('Hello World')
    }
})
app.get('/login', function (req, res) { //显示数据
    // 设置session
    req.session.username="张三"
    res.send("登入")
})
app.get('/loginOut', function (req, res) { //显示数据
    // 1、设置session过期时间为0    (他会把所有的cookie都销毁)
    req.session.cookie.maxAge=0;

    // 2、指定销毁session
    req.session.username="";

    // 3、销毁session destroy
    req.session.destroy();
    res.send("退出登入");       
})
app.listen(3000)
```

#### 四、负载均衡配置 Session，把 Session 保存到数据库里面

![image-20210404131444195](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210404131444195.png)

1. 配置express-session

2. 安装connect-mongo

3. 引入

   ```js
   const MongoStore = require('connect-mongo');
   ```

4. 配置中间件

   ```js
   // 配置session的中间件
   app.use(session({
       secret: 'keyboard cat', //服务器端生成session 的签名
       name: "lyc", //修改session对应cookie的名称
       resave: false, //'强制保存session 即使它并没有变化
       saveUninitialized: true, //强制将未初始化的session 存储
       cookie: {
           maxAge: 1000 * 60,
           secure: false //true表示只有https协议才能访问cookie
       },
       rolling: true, //在每次请求时强行设置cookie, 这将重置cookie 过期时间(默认:false)        
       store: MongoStore.create({
           mongoUrl: 'mongodb://127.0.0.1:27017/shop',
           touchAfter: 24*3600 	//不管发出了多少请求在24小时内只更新一次session,除非改变了这个session
       })
   }))
   ```


### Express 路由模块化以及 Express 应用程序生成器

#### 一、 Express 路由模块化

https://expressjs.com/en/guide/routing.html
Express 中允许我们通过 express.Router 创建模块化的、可挂载的路由处理程序

> app.js

```js
const express = require('express');

// 引入外部模块
const app = express();
const index = require("./routes/index");
const api = require("./routes/api");
const admin = require("./routes/admin");

// 挂载login模块
app.use("/admin",admin);
app.use("/api",api);
app.use("/",index);

    app.listen(3000)
```

> admin.js

```js
const express = require('express');
var router = express.Router();

// 引入下一级模块
const user = require("./admin/user")

router.get("/",(req,res)=>{
    res.send("后台页面");
})
// 挂载下一级路由
router.use("/user",user);

module.exports = router;
```

> admin/user.js

```js
const express = require('express');
var router = express.Router();


router.get("/admin/user",(req,res)=>{
    res.send("后台用户页面");
})

module.exports = router;
```

#### 二、Express 应用生成器

通过应用生成器工具 express-generator 可以快速创建一个应用的骨架。

你可以通过 npx （包含在 Node.js 8.2.0 及更高版本中）命令来运行 Express 应用程序生成器。

```
npx express-generator
或者
cnpm install -g express-generator
```

```
express --view=ejs express09
```

### Express 结合 multer 上传图片

#### 一、 Multer 模块介绍

Multer 是一个 node.js 中间件，用于处理 multipart/form-data 类型的表单数据，它主要用于上传文件。它是写在 busboy 之上非常高效。
**注意: Multer 不会处理任何非 multipart/form-data 类型的表单数据。**

#### 二、 Express 上传文件模块 multer 的使用

1. 安装multer

2. 引用

   ```js
   const multer = require('multer');
   const path = require("path");
   ```

3. 配置和封装

   ```js
   let tools = {
       multer() {
           // var upload = multer({ dest: 'static/upload' })      //上传之前目录必须存在
           var storage = multer.diskStorage({
               // 配置上传的目录
               destination: function (req, file, cb) {
                   cb(null, 'static/upload')
               },
               // 修改上传后的文件名
               filename: function (req, file, cb) {
                   // 1、获取后缀名
                   let extname = path.extname(file.originalname);
                   // 2、根据时间戳来生成文件名
                   cb(null, Date.now() + extname);
               }
           })
           var upload = multer({
               storage: storage
           })
           return upload;
       },
       md5(){
       }
   }
   module.exports = tools;
   ```

4. 使用

   ```js
   router.get("/add", (req, res) => {
       res.render("admin/nav/add")
   })
   
   router.post("/doAdd",tools.multer().single("pic"), (req, res) => {
       // 获取表单传来的数据
       res.send({
           body: req.body,
           file: req.file
       });
   })
   ```

5. 按照日期生成上传文件目录

   ```js
   const multer = require('multer');
   const path = require("path");
   var sd = require('silly-datetime');
   const mkdirp = require('mkdirp');
   
   let tools = {
       multer() {
           // var upload = multer({ dest: 'static/upload' })      //上传之前目录必须存在
           var storage = multer.diskStorage({
               // 配置上传的墓目录
               destination: async (req, file, cb) => {
                   // 1、获取当前日期
                   let day = sd.format(new Date(), 'YYYYMMDD');
                   // static/upload/20210404
                   let dir = path.join("static/upload", day); //拼接目录
                   // 2、按照日期生成图片储存目录  mkdirp是一个异步方法
                   await mkdirp(dir)
                   cb(null, dir) //目录必须存在
               },
               // 修改上传后的文件名
               filename: function (req, file, cb) {
                   // 1、获取后缀名
                   let extname = path.extname(file.originalname);
                   // 2、根据时间戳来生成文件名
                   cb(null, Date.now() + extname);
               }
           })
           var upload = multer({
               storage: storage
           })
           return upload;
       },
       md5() {}
   }
   module.exports = tools;
   ```

6. 多文件上传

   ```js
   let cpUpload = tools.multer().fields([{name:'pic1',maxCount:1},{name:'pic2',maxCount:1}]);
   
   router.post("/doAdd",cpUpload, (req, res) => {
       res.send({
           body: req.body,
           file: req.files
       })
   })
   ```

   

### Mongoose的使用

#### 一、mongoose 介绍

Mongoose 是在 node.js 异步环境下对 mongodb 进行便捷操作的对象模型工具。Mongoose是 NodeJS 的驱动，不能作为其他语言的驱动

1、通过关系型数据库的思想来设计非关系型数据库
2、基于 mongodb 驱动，简化操作



- 基本使用

```js
//1.引入mongoose
const mongoose = require('mongoose');

//2、建立连接  
mongoose.connect('mongodb://127.0.0.1:27017/eggcms');

//3、操作users表（集合）   定义一个Schema   Schema里面的对象和数据库表里面的字段需要一一对应
var UserSchema = mongoose.Schema({
    name: String,
    age: Number,
    status: Number
})


//4、定义数据库模型  操作数据库
// model里面的第一个参数 要注意：1首字母大写  2、要和数据库表（集合 ）名称对应  这个模型会和模型名称相同的复数的数据库表建立连接
// var User=mongoose.model('User',UserSchema);    // 默认会操作 users表（集合）
var User = mongoose.model('User', UserSchema, 'user'); //默认会操作第三个参数配置的表  user表（集合）

//5、查询users表的数据
User.find({},function(err,doc){ 
    if(err){
        console.log(err);
        return;
    }
    console.log(doc);
})  
```

- 增删改查

```js
//1.引入mongoose
const mongoose = require('mongoose');

//2、建立连接  
mongoose.connect('mongodb://127.0.0.1:27017/eggcms');

//3、定义一个Schema 
var NewsSchema = mongoose.Schema({
    title: "string",
    author: String,
    pic: String,
    content: String,
    status: Number
})

//4、定义操作数据库的Model
var News = mongoose.model('News', NewsSchema, 'news');

//5、增加数据
//通过实例化 Model 创建增加的数据
var news = new News({
    title: "我是一个新闻11111",
    author: '张三1',
    content: '我是新闻的内容',
    status: 1
});
news.save(function (err) {
    if (err) {
        return console.log(err);
    }
    console.log('成功')
});

//6、修改数据
News.updateOne({
        "_id": "5b7563e2ba3c6747d0612204"
    }, {
        "title": "我是一个新闻2222"
    },
    function (err, doc) {
        if (err) {
            return console.log(err);
        }
        console.log(doc)
    })


//删除数据
News.deleteOne({
    "_id": "5b7563e2ba3c6747d0612204"
}, (err, result) => {
    if (err) {
        return console.log(err);
    }
    console.log(result)
})
```

- 默认操作

```js
// 定义数据表(集合的)映射注意:字段名称必须和数据库保持一 致
var UserSchema = mongoes.Schema({
    name: String,
    age: Number,
    status: {
        type:Number,
        default:1       //如果没有数据 默认参数
    }
})


//增加数据
var u = new UserModel({
    name:"张三",
    age:19,
    status:1,
    sex:"男"        //和model不同 --无效
})
u.save((err)=>{
    if(err){
        console.log(err);
        return;
    }
    console.log('成功增加数据');
})
```

- 模块化

> app.js

```js
var UserModel = require('./model/user.js');

var user = new UserModel({
    name: "李四666",
    age: 40
})

user.save(function (err) {
    if (err) {
        console.log(err);
        return;
    }
    //获取user表的数据
    UserModel.find({}, function (err, docs) {
        if (err) {
            console.log(err);
            return;
        }
        console.log(docs);
    })
})
```

> user.js

```js
var mongoose=require('./db.js');

var UserSchema=mongoose.Schema({
    name:String,
    age:Number,
    status:{
        type:Number,
        default:1   
    }
})

module.exports=mongoose.model('User',UserSchema,'user');
```

> db.js

```js
//连接数据库
var mongoose=require('mongoose');

//useNewUrlParser这个属性会在url里识别验证用户所需的db,未升级前是不需要指定的,升级到一定要指定。

mongoose.connect('mongodb://127.0.0.1:27017/eggcms',{ useNewUrlParser: true },function(err){
        if(err){
            console.log(err);
            return;
        }
        console.log('数据库连接成功')
});

module.exports=mongoose;
```

#### 预定义模式修饰符

```js
var NewsSchema=mongoose.Schema({
    title:{
        type:String,
        trim:true    //定义 mongoose模式修饰符 去掉空格
    },
    author:String,
    pic:String,    
    content:String,
    status:{
        type:Number,
        default:1
    }
})
```

Getters 与 Setters 自定义修饰符

除了 mongoose 内置的修饰符以外，我们还可以通过 set（建议使用） 修饰符在增加数据的时候对数据进行格式化。也可以通过 get（不建议使用）在实例获取数据的时候对数据进行格式化。

> set方法

```js
var FocusSchema = mongoose.Schema({
    title: {
        type: String,
        trim: true //定义 mongoose模式修饰符 去掉空格
    },
    pic: String,
    redirect: {
        type: String,
        set(parmas) { //增加数据的时候对redirect字段进行处理
            // parmas可以获取redirect的值 、    返回的数据就是redirect在数据库实际保存的值
            /*
            www.baidu.com              http://www.baidu.com
            http://www.baidu.com       http://www.baidu.com
            */
            if (!parmas) {
                return ''
            } else {
                if (parmas.indexOf('http://') != 0 && parmas.indexOf('https://') != 0) {
                    return 'http://' + parmas;
                }
                return parmas
            }
        }
    },
    status: {
        type: Number,
        default: 1
    }
})
```

> get方法

```js
var UserSchema=mongoose.Schema({
    
    name:{
        type:String,
        get(params){   //不建议使用
            return "a001"+params
        }   
    },
    age:Number,       
    status:{
        type:Number,
        default:1 
    }
})
```

#### Mongoose 索引扩展和Mongoose Model 的静态方法和实例方法

**Mongoose 索引**

索引是对数据库表中一列或多列的值进行排序的一种结构，可以让我们查询数据库变得更快。MongoDB 的索引几乎与传统的关系型数据库一模一样，这其中也包括一些基本的查询优化技巧。

mongoose 中除了以前创建索引的方式，我们也可以在定义 Schema 的时候指定创建索引。

```js
var UserSchema=mongoose.Schema({
    
    name:{
        type:String,
        unique: true    //唯一索引   
    },
    sn:{
        type:String,
        index:true      // 普通索引
    },
    age:Number,       
    status:{
        type:Number,
        default:1
    }
})
```

**Mongoose Model 的静态方法和实例方法**

```js
//静态方法 
UserSchema.statics.findBySn=function(sn,cb){
    //通过 find方法获取 sn的数据    this 关键字获取当前的model
    this.find({"sn":sn},function(err,docs){
        cb(err,docs)
    })   
}

// 实例方法   (基本不用)
UserSchema.methods.print=function(){
    console.log('我是一个实例方法')
    console.log(this.name)
}
```

#### Mongoose 数据校验

- required : 表示这个数据必须传入
- max: 用于 Number 类型数据，最大值
- min: 用于 Number 类型数据，最小值
- enum:枚举类型，要求数据必须满足枚举值 enum: ['0', '1', '2']
- match:增加的数据必须符合 match（正则）的规则
- maxlength：最大值
- minlength：最小值

```js
var mongoose=require('./db.js');

//mongoose数据校验:用户通过mongoose给mongodb数据库增加数据的时候，对数据的合法性进行的验证
//mongoose里面定义Schema:字段类型，修饰符、默认参数 、数据校验都是为了数据库数据的一致性
//Schema，为数据库对象的集合,每个schema会映射到mongodb中的一个collection,定义Schema可以理解为表结构的定义

var UserSchema=mongoose.Schema({
    name:{
        type:String,//指定类型
        trim:true,   //修饰符         
        required:true      
    },
    sn:{
        type:String,
        index:true,  //索引.
        set(val){  //自定义修饰符
            return val;
        },
        // maxlength:20,
        // minlength:10
        // match:/^sn(.*)/ ,
        validate: function(sn) {
            return sn.length >= 10;
        }        
    },   
    age:{
        type:Number,
        min:0,    //用在number类型上面
        max:150
    },       
    status:{
        type:String, 
        default:'success', //默认值
        enum:['success','error']   //status的值必须在 对应的数组里面  注意枚举是用在String
    }
})

module.exports=mongoose.model('User',UserSchema,'user');
```

#### Mongoose 中使用 aggregate 聚合管道

**使用聚合管道可以对集合中的文档进行变换和组合。**
实际项目：表关联查询、数据的统计

```js
/*

mongodb数据库使用 聚合管道

db.order.aggregate([
    {
      $lookup:
        {
          from: "order_item",
          localField: "order_id",
          foreignField: "order_id",
          as: "items"
        }
  },
{
    $match:{"all_price":{$gte:90}}
}
])
*/

var OrderModel = require('./model/order.js');


//查询order 表的数据
/*
    OrderModel.find({},function(err,docs){
        console.log(docs);
    })
*/


//order表关联order_item
OrderModel.aggregate([
  {
    $lookup: {
      from: "order_item",
      localField: "order_id",
      foreignField: "order_id",
      as: "items"
    }
  },
  {
    $match: {
      "all_price": {
        $gte: 90
      }
    }
  }
], function (err, docs) {
  if (err) {
    console.log(err);
    return;
  }
  console.log(JSON.stringify(docs))
})
```

> 查询order_item，找出商品名称是酸奶的商品，酸奶这个商品对应的订单的订单号以及订单的总价格

```js
var OrderItemModel = require('./model/order_item.js');
var OrderModel = require('./model/order.js');
var mongoose = require('mongoose');

//第一种实现方式

    OrderItemModel.find({"_id":"5b743da92c327f8d1b360546"},function(err,docs){
        // console.log(docs);
        var order_item=JSON.parse(JSON.stringify(docs));
        var order_id=order_item[0].order_id;
        OrderModel.find({"order_id":order_id},function(err,order){
            //    console.log(order);
            order_item[0].order_info=order[0];
            console.log(order_item)
        })
    })


//第二种方式 
//mongoose中获取ObjectId           mongoose.Types.ObjectId

OrderItemModel.aggregate([{
    $lookup: {
      from: "order",
      localField: "order_id",
      foreignField: "order_id",
      as: "order_info"
    }
  }, {
    $match: {
      _id: mongoose.Types.ObjectId('5b743da92c327f8d1b360546')
    }
  }
], function (err, docs) {
  if (err) {
    console.log(err)
    return;
  }
  console.log(JSON.stringify(docs))
})
```

## 7、Koa

Koa 是基于 Node.js 平台的下一代 web 开发框架。

Koa是由 Express 原班人马打造的，致力于成为一个更小、更富有表现力、更健壮的 Web 框架。 使用 Koa 编写 web 应用，可以免除重复繁琐的回调函数嵌套， 并极大地提升错误处理的效率。Koa不在内核方法中绑定任何中间件， 它仅仅提供了一个轻量优雅的函数库，使得编写 Web 应用变得得心应手，开发思路和 Express 差不多，最大的特点就是可以避免异步嵌套

### 1、koa的基本使用

```js
// 引入Koa
var koa = require('koa');
// 实例化Koa
var app = new koa();
 
app.use( async(ctx)=>{
    ctx.body = "hello,koa"
});
 
// 监听端口
app.listen(3000);
```

#### koa路由的使用

```js
// 1.引入路由并实例化
var router = require('koa-router')();
// 两种写法
var Koa = require('koa');
var app = new Koa();


// 路由路径前缀设置
router.prefix('/api')

// 3.配置路由
//ctx 上下文context，包含了request和response等信息
router.get('/', async (ctx) => { // 路径: /api/get
    // 返回数据给前端
    ctx.body = "你好";
}).get('/news',async (ctx)=>{
    console.log(ctx.query);     //获取的是对象
    console.log(ctx.querystring);  //获取的是字符串

    ctx.body = "你好";
})
// 动态路由 可以传入多个值
.get('/news/:aid/:cid',async (ctx)=>{
    // 获取动态路由的传值
    console.log(ctx.params);
    ctx.body="新闻"
})

// 4.启动路由(来自于官方文档);
// router.allowedMethods()可以配置也可以不配置。
// 如果之前的没有设置响应头，配置此选项以后可以自动设置响应头。
app
    .use(router.routes())
    .use(router.allowedMethods());

// 监听端口
app.listen(3000);
```

#### Koa中间件

中间件是配合路由匹配完成做的一系列的操作，我们就可以把它叫做中间件。Koa中运用中间件可以实现以下一些功能：

(1).添加应用。主要通过app.use()这个函数添加或是启动一些应用，如常见的一些第三方中间件的使用。
(2)匹配路由。主要通过next()这个函数完成多级路由匹配。
(3)错误处理。如果当前访问的路由一直向下匹配没有匹配到，可以通过中间件给出错误响应。

```js
var Koa = require('koa');
var Router = require('koa-router');
var app = new Koa();
var router = new Router();
// Koa 错误处理中间件
// 无论app.use放到路由前面还是后面
// 都是先执行app.use再去执行路由
app.use(async (ctx, next) => {
    console.log('这是一个中间件'); // 执行顺序1
    
    await next();

    if (ctx.status == 404) { // 执行顺序3
        ctx.body = '这是一个404页面';
    } else {
        console.log(ctx.url);
    }
});

// 配置新闻页                            // 执行顺序2
router.get('/news', async (ctx, next) => {  //匹配到news后继续向下执行
    console.log('这是新闻路由');
    await next();
});
router.get('/news',async (ctx)=>{
    ctx.body = '这是新闻路由';
})


app.use(router.routes());
app.use(router.allowedMethods());

app.listen(3000);
```

### Koa异步处理Async、Await 和Promise的使用(重点)

- async是让方法变成异步
- await是等待异步方法执行完成。

> await在等待async方法执行完毕，其实await等待的只是-一个表达式，这个表达式在官方文档里说的是Promise对象，但是它也可以接受普通值。

`注意`:await必须在async方法中才可以使用因为await问本身就会造成程序停正堵塞，所以必须在异步方法中才可以使用。

```js
async function test(){
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            var name='张三 222';
            resolve(name);
        },1000);
    })
}

async function main(){
    var date=await test();  //获取异步方法里面的数据
    console.log(date);      //await必须用在async异步方法里
}

main();
```

### ejs模板使用

>  同express一样使用ejs

```js
var router = require('koa-router')(),
    views = require('koa-views'),
    Koa = require('koa');

app = new Koa();

//配置模板引擎中间件 --第三方中间件
//app. use(views('views'， { map: (html: 'ejs' })); //这样配置也可以 注意如果这样配置的话模板的后缀名是. html
app.use(views('views',{
    extension:'ejs'
}))

// 写一个中间件配置公共的信息	在任何一个ejs中都可以调用
app.use(async(ctx,next)=>{
    ctx.state.userinfo='张三';
    await next();
})

router.get('/', async (ctx) => { 
    let title = "你好";
    await ctx.render('index',{
        title:title
    });
});

app
    .use(router.routes())
    .use(router.allowedMethods());

// 监听端口
app.listen(3000);
```

```ejs
<h2><%=title%>-----<%=userinfo%></h2>
```

### post提交数据

> 原生node.js,在koa中获取表单提交的数据

![image-20210407232217148](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210407232217148.png)

![image-20210407232340305](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210407232340305.png)

**最新node中获取post数据**

> Koa中koa-bodyparser中间件获取表单提交的数据

```js
/*
    Koa中koa-bodyparser中间件获取表单提交的数据
    
    1.cnpm install --save koa -bodyparser
    2.引入var bodyParser = require( koa-bodyparser' ) ;
    3. app.use(bodyParser();
    4. ctx.request.body;  获取表单提交的数据
*/ 

var router = require('koa-router')(),
    views = require('koa-views'),
    Koa = require('koa'),
    bodyParser = require('koa-bodyparser');

var app = new Koa();

app.use(views('views',{
    extension:'ejs'
}))
//配置bodyParser中间件
app.use(bodyParser());

router.get('/', async (ctx) => { 
    await ctx.render('index');
});

router.post('/doAdd',async (ctx)=>{
    console.log(ctx.request.body);
    ctx.body = ctx.request.body;
})

app.use(router.routes());
app.use(router.allowedMethods());

// 监听端口
app.listen(3000);
```

> ejs

```ejs
<form action="/doAdd" method="post">
    用户名：<input type="text" name="username"/>
    <br>
    <br>
    密  码：<input type="password" name="username"/>
    <br>
    <br>
    <button type="submit">提交</button>
    </form>
```

### koa-static静态web中间件

```js
/*
1. cnpm install koa-static --save
2. const static = require('koa-static' )
3.配置中间件  app. use(static(' static' )
*/
var router = require('koa-router')(),
    views = require('koa-views'),
    Koa = require('koa'),
    bodyParser = require('koa-bodyparser'),
    static = require('koa-static');

var app = new Koa();

app.use(views('views',{
    extension:'ejs'
}))


// 配置静态web中间件    首先去static中找，如果能找到返回对应的文件，找不到next()
app.use(static('static'));  //koa中间件可以配置多个

app.use(bodyParser());

router.get('/', async (ctx) => { 
    await ctx.render('index');
});

router.post('/doAdd',async (ctx)=>{
    console.log(ctx.request.body);
    ctx.body = ctx.request.body;
})

app.use(router.routes());
app.use(router.allowedMethods());

// 监听端口
app.listen(3000);
```

### art-template的使用

#### 介绍

art-template 是一个简约、超快的模板引擎。

它采用作用域预声明的技术来优化模板渲染速度，从而获得接近 JavaScript 极限的运行性能，并且同时支持 NodeJS 和浏览器。

#### 特性

1. 拥有接近 JavaScript 渲染极限的的性能
2. 调试友好：语法、运行时错误日志精确到模板所在行；支持在模板文件上打断点（Webpack Loader）
3. 支持 Express、Koa、Webpack
4. 支持模板继承与子模板
5. 浏览器版本仅 6KB 大小

#### 语法

art-template 支持标准语法与原始语法。标准语法可以让模板易读写，而原始语法拥有强大的逻辑表达能力。

标准语法支持基本模板语法以及基本 JavaScript 表达式；原始语法支持任意 JavaScript 语句，这和 EJS 一样。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    {{list.name}}
    <br>
    {{@list.h}}
    <br>
    {{if num>20}} 大于 {{else}} 小于 {{/if}}
    <br>
    <ul>
    {{each list.data}}
        <li> {{$index}} --- {{$value}} </li>
    {{/each}}
    </ul>
    <br>
    {{include 'public/footer.html'}}
</body>
</html>
```

### Koa中的cookie

使用同express中的cookie

```JS
var router = require('koa-router')(),
    Koa = require('koa'),
    render = require('koa-art-template'),
    path = require('path');

var app = new Koa();

// 配置 koa-art-template 模板引擎
render(app, {
    root: path.join(__dirname, 'views'), //视图的位置
    extname: '.html',    //后缀名
    debug: process.env.NODE_ENV !== 'production'    //是否开启调试模式
});

router.get('/', async (ctx) => {
    // 在koa中无法直接设置中文cookie
    var userinfo = new Buffer('张三').toString('base64');
    ctx.cookies.set('userinfo',userinfo,{
        maxAge:60*1000*60
    });
    await ctx.render('index');
});
router.get('/news', async (ctx) => {
    var data = ctx.cookies.get('userinfo');
    var userinfo = new Buffer(data,'base64').toString();
    console.log(userinfo);
    let app={
        name:'张三'
    };
    await ctx.render('news',{
        list:app
    });
});

app
    .use(router.routes())
    .use(router.allowedMethods());

// 监听端口
app.listen(3000);
```

### Koa中的cookie

![image-20210409182139241](http://blogimg-dust.oss-cn-beijing.aliyuncs.com/img/image-20210409182139241.png)

```js
var router = require('koa-router')(),
    Koa = require('koa'),
    render = require('koa-art-template'),
    path = require('path'),
    session = require('koa-session');	//安装并且引用koa-session

var app = new Koa();

render(app, {
    root: path.join(__dirname, 'views'), 
    extname: '.html', 
    debug: process.env.NODE_ENV !== 'production' //是否开启调试模式
});

// 配置session中间件
app.keys = ['some secret hurr'];    //cookie的签名
const CONFIG = {
    key: 'koa:sess', //cookie is key
	maxAge: 86400000, // cookie 的过期时间 默认一天 ms
	overwrite: true, //是否可以 overwrite 
	httpOnly: true, //cookie 是否只有服务器端可以访问 
	signed: true, //签名默认 true 
	rolling: false, //在每次请求时强行设置 cookie，这将重置 cookie 过期时间（默认：false） 
	renew: true, //快过期的时候配置过期时间 需要修改 默认false
};
app.use(session(CONFIG, app));

router.get('/', async (ctx) => {
    // 设置session
    ctx.session.userinfo='张三';
    await ctx.render('index');
});
router.get('/news', async (ctx) => {
    // 获取session
    console.log(ctx.session.userinfo);
    let app = {
        name: '张三'
    };
    await ctx.render('news', {
        list: app
    });
});

app
    .use(router.routes())
    .use(router.allowedMethods());

// 监听端口
app.listen(3000);
```

### js中面向对象继承

#### 1.1 原型链继承

原型链继承 ：子类的原型对象 = 父类的实例对象

```JS
//1.父类构造函数
function Student(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.arr = [1,2,3];
}
Student.prototype.classId = "1116"
Student.prototype.study = function(){
    console.log("good good study , day day sleep!");
}


//2.子类构造函数
function MiniStudent(){
    this.play = function(){
        console.log("玩王者荣耀");
    }
}

//3.继承的操作  原型链继承 子类的原型对象 = 父类的实例对象
MiniStudent.prototype = new Student("小夏",6,"男");

//4.实例化对象
var mS = new MiniStudent();
```

原型链：属性或方法的查找方式

```js
//原型链：实例本身----》__proto__（prototype）---->父类的实例对象---->父类的__proto__(prototype)....... undefined
        console.log(mS.name);
        console.log(mS.classId);
```

原型链继承问题：

```JS
//缺点1：不能传参，每次创建出来都是一样的
var ms1 = new MiniStudent();
console.log(ms1.arr);
ms1.arr.push(4)
console.log(ms1.arr);


//缺点2：继承了引用数据类型一改全改
var ms2 = new MiniStudent();
console.log(ms2.arr);
```

#### 1.2 对象冒充继承

```JS
//2.子类构造函数
function MiniStudent(name,age,sex){
    //3.对象冒充继承
    Student.call(this,name,age,sex);
    this.play = function(){
        console.log("玩王者荣耀");
    }
}

//4.实例化对象
var s1 = new MiniStudent("如花","6","女");
console.log(s1);
s1.arr.push(4);//[1,2,3,4]
```

优点：可以传参，引用数据类型不会再一改全改

缺点：不能继承原型中的属性和方法

#### 1.3 混合继承

混合继承：对象冒充继承+原型链继承

```JS
//1.父类构造函数
function Student(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.arr = [1,2,3];
}
Student.prototype.classId = "1116"
Student.prototype.study = function(){
    console.log("good good study , day day sleep!");
}


//2.子类构造函数
function MiniStudent(name,age,sex){
    //3.对象冒充继承
    Student.call(this,name,age,sex)
    this.play = function(){
        console.log("玩王者荣耀");
    }
}
//混合继承  对象冒充（构造函数中属性和方法）+原型链继承(继承原型对象中属性和方法)
//4.原型链继承 
MiniStudent.prototype = new Student("小明",3,"男");

//5.实例化对象
var ms1 = new MiniStudent("小郝",10,"女");
console.log(ms1);
```

优点：可以传参，引用数据类型不会再一改全改，可以继承父类原型中的属性和方法

缺点：创建了一个多余的父类实例

#### 1.4 寄生式组合继承

```JS
//2.子类构造函数
function MiniStudent(name,age,sex){
    //3.对象冒充继承
    Student.call(this,name,age,sex)
    this.play = function(){
        console.log("玩王者荣耀");
    }
}
//混合继承  对象冒充（构造函数中属性和方法）+原型链继承(继承原型对象中属性和方法)
//4.原型链继承    Object.create():以原型为基础创建对象
MiniStudent.prototype = Object.create(Student.prototype);
MiniStudent.prototype.constructor = MiniStudent;

//5.实例化对象
var ms1 = new MiniStudent("小郝",10,"女");
console.log(ms1);
```

优点：可以传参，引用数据类型不会再一改全改，可以继承父类原型中的属性和方法，不会创建多余的父类实例。

#### 1.5 ES6中的继承方法

```js
    // 继承是 两个父子级关系的构造函数之间的应用

    // 如何定义一个构造函数
    // ES5语法
    function Fun1(name, age) {
    // 定义属性
    this.name = name;
    this.age = age;
		}
		//定义方法
		Fun1.prototype.f1 = function () {
	    console.log(this.name, this.age);
	}

    // ES6语法
    class Fun2{
        // 构造器中定义属性
        constructor(name,age){
            this.name = name;
            this.age = age;
        }
        // 定义方法
        f2(){
            console.log(this.name,this.age);
        }
    }

    // ES6的继承语法
    // 先定义父级构造函数 Father
    // 通过 extends 来指定 继承的父级的构造函数名称
    // 在构造器 constructor 中 通过 super 来 指定,哪个属性来自于父级构造函数
    // extends 关键词 指定父级构造函数
    // super 指定 属性来源父级

    // 继承属性,如果父级中有多个属性
    // 在 super 中, 只继承一部分,并且只设定一部分,没有设定的,执行结果是 undefined

    // 父级的属性 可以 只继承部分
    // 其他的属性 如果没有操作, 是 undefined
    // 也可以在子级中,定义父级属性的数据数值

    // 子级中也可以定义新的属性和属性值




    // 定义父级构造函数

    function Father(name,age){
        this.name = name;
        this.age = age;
    }
    Father.prototype.f1 = function(){
        console.log(this.name,this.age);
    }

    // extends 指定从 Father 构造函数中,执行继承操作
    class Son extends Father{
        constructor(name,age,sex){
            // 在构造其中,通过 super 来指定,从父级继承来的属性

            // 继承父级的name
            super(name);
            // 自行定义父级的age
            this.age = age;
            // 自定义属性sex和sex的数值
            this.sex = sex;
        }

        // 自定义方法
        f2(){
            console.log('我是自定义的子级方法');
        }

    }

    const obj1 = new Father('张三' , 18);
    console.log(obj1);

    // 属性是直接继承父级中,定义的属性的形式
    // 方法是调用父级中定义的方法
    const obj2 = new Son('李四' , 20 , '男');
    console.log(obj2);
    /*
    总结  ES6的继承语法
    1,继承语法是为了,简化代码,防止重复代码的出现
    2,继承是两个构造函数之间的应用
    3,ES6语法,默认是继承父级构造函数的所有的属性和所有方法
        属性如果没有指定数据,执行结果是undefined
        方法是通过原型链,找到父级构造函数中,定义的方法
    4,语法形式:
      class 子级 extends 父级{
          constructor(属性参数...){

              先写继承的属性,再写自定义的属性
              super(继承父级的属性);

              自定义属性
          }

          自定义的方法
          自定义方法(){

          }
      }

    */
```

#### 1.6单例

> 单例模式（Singleton Pattern）是 Java 中最简单的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。
>
> 这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。
>
> **注意：**
>
> - 1、单例类只能有一个实例。
> - 2、单例类必须自己创建自己的唯一实例。
> - 3、单例类必须给所有其他对象提供这一实例。

```js
class Db{
    static getInstance(){   //单例
        if(!Db.Instance){
            Db.Instance = new Db();
        }
        return Db.Instance;
    }
    constructor(){
        console.log('实例化');
        this.connect();
    }
    connect(){
        console.log('连接数据库')
    }
}

var myDB = Db.getInstance();
var myDB2 = Db.getInstance();
```

### kao中的mongodb数据库

```js
var MongoClient = require('mongodb').MongoClient;

var dbUrl = 'mongodb://127.0.0.1:27017/';

var dbName = 'koa';

// 连接数据库 
MongoClient.connect(dbUrl, (err, client) => {
    if (err) {
        console.log(err);
        return;
    }
    var db = client.db(dbName);

    // 增加数据
    db.collection('user').insertOne({'username':"dd",'age':29,'sex':"男","status":"1"},(err,res)=>{
        if(!err){
            console.log("连接成功");
            client.close();
        }
    })

    // 查询数据
    var result = db.collection('user').find({});
    result.toArray((err,docs)=>{
        console.log(docs);
    })
})
```

### **封装 MongoDB 类**

在项目的根目录创建一个 mongodb 目录，然后在该目录下新建 **config.js**，用来保存一些数据库常量配置

```js
// /mongodb/config.js

const dbUrl = 'mongodb://127.0.0.1:27017'; // 数据库地址
const dbName = 'Movie'; //数据库名称

module.exports = {
  dbUrl,
  dbName
}
```

在 mongodb 目录下创建一个 **index.js**，使用中间件连接 MongoDB 数据库

```js
// /mongodb/index.js

const { MongoClient, ObjectID } = require("mongodb");
const Config = require("./config");

class Db {
  static getInstance() {
    // 单例模式 解决多次实例化 实例不共享的问题
    if (!Db.instance) {
      Db.instance = new Db();
    }

    return Db.instance;
  }

  constructor() {
    this.dbClient = ""; //db对象
    this.connect(); // 实例化的时候就连接数据库
  }

  connect() {
    // 连接数据库
    return new Promise((resolve, reject) => {
      if (!this.dbClient) {
        //解决数据库多次连接的问题
        MongoClient.connect(Config.dbUrl, { useUnifiedTopology: true }, (err, client) => {
          if (err) {
            reject(err);
            return;
          }
          this.dbClient = client.db(Config.dbName);
          resolve(this.dbClient);
        });
      } else {
        resolve(this.dbClient);
      }
    });
  }

  //查找操作 collection：表名 json：查找条件
  find(collection, json) {
    return new Promise((resolve, reject) => {
      this.connect().then((db) => {
        let result = db.collection(collection).find(json);
        result.toArray((err, docs) => {
          if (!err) {
            resolve(docs);
          } else {
            reject(err);
          }
        });
      });
    });
  }

  //新增操作
  insert(collection, json) {
    return new Promise((resolve, reject) => {
      this.connect().then((db) => {
        db.collection(collection).insertOne(json, (err, result) => {
          if (!err) {
            resolve(result);
          } else {
            reject(err);
          }
        });
      });
    });
  }

  //修改操作
  update(collection, json1, json2) {
    return new Promise((resolve, reject) => {
      this.connect().then((db) => {
        db.collection(collection).updateOne(
          json1,
          {
            $set: json2,
          },
          (err, result) => {
            if (!err) {
              resolve(result);
            } else {
              reject(err);
            }
          }
        );
      });
    });
  }

  //删除操作
  delete(collection, json) {
    return new Promise((resolve, reject) => {
      this.connect().then((db) => {
        db.collection(collection).removeOne(json, (err, result) => {
          if (!err) {
            resolve(result);
          } else {
            reject(err);
          }
        });
      });
    });
  }

  //在进行查询或者删除操作的时候，我们一般都会通过id去进行操作，但是我们直接使用传递过来的id是不起作用的，需要使用mongodb提供的ObjectID方法，生成一个新的id去查询。
  getObjectID(id) {
    return new ObjectID(id);
  }
}

module.exports = Db.getInstance();
```

app.js 

```js
var Koa=require('koa'),
    router = require('koa-router')(),
    render = require('koa-art-template'),
    path=require('path'),
    bodyParser=require('koa-bodyparser'),
    DB=require('./module/db.js');

var app=new Koa();

//配置post提交数据的中间件
app.use(bodyParser());

//配置 koa-art-template模板引擎
render(app, {
    root: path.join(__dirname, 'views'),   // 视图的位置
    extname: '.html',  // 后缀名
    debug: process.env.NODE_ENV !== 'production'  //是否开启调试模式
});
//显示学员信息
router.get('/',async (ctx)=>{
    var result=await DB.find('user',{});
    console.log(result);
    await ctx.render('index',{
        list:result
    });
})
//增加学员
router.get('/add',async (ctx)=>{
    await ctx.render('add');
})


//执行增加学员的操作
router.post('/doAdd',async (ctx)=>{
    //获取表单提交的数据
   // console.log(ctx.request.body);  //{ username: '王麻子', age: '12', sex: '1' }
    let data=await DB.insert('user',ctx.request.body);
    //console.log(data);
    try{
        if(data.result.ok){
            ctx.redirect('/')
        }
    }catch(err){
        console.log(err);
        return;
        ctx.redirect('/add');
    }
})



//编辑学员
router.get('/edit',async (ctx)=>{
    //通过get传过来的id来获取用户信息
    let id=ctx.query.id;
    let data=await DB.find('user',{"_id":DB.getObjectId(id)});
    //获取用户信息
    await ctx.render('edit',{
        list:data[0]
    });
})


router.post('/doEdit',async (ctx)=>{
    //通过get传过来的id来获取用户信息
    //console.log(ctx.request.body);
    var id=ctx.request.body.id;
    var username=ctx.request.body.username;
    var age=ctx.request.body.age;
    var sex=ctx.request.body.sex;
    let data=await DB.update('user',{"_id":DB.getObjectId(id)},{
        username,age,sex
    })
    try{
        if(data.result.ok){
            ctx.redirect('/')
        }
    }catch(err){
        console.log(err);
        return;
        ctx.redirect('/');
    }
})


//删除学员
router.get('/delete',async (ctx)=>{
    let id=ctx.query.id;
    var data=await DB.remove('user',{"_id":DB.getObjectId(id)});
    console.log(data);
    if(data){
        ctx.redirect('/')
    }
})


app.use(router.routes());   /*启动路由*/
app.use(router.allowedMethods());
app.listen(3000);
```

