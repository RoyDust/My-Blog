# 使用PM2将egg.js部署到服务上



#### 服务器安装环境

- Node.js
- PM2


### 部署步骤

1. 修改默认端口

 找到config目录下的config.default.js，添加如下代码：

```js
config.cluster = {
   listen: {
    path: '',
    port: 8000,	// xxx.xxx.xxx.xxx:8000 就是你接口的前置URL
    hostname: '0.0.0.0',
   }
 };
```



2. 在eggjs[根目录](https://so.csdn.net/so/search?q=根目录&spm=1001.2101.3001.7020)下新建server.js，并添加如下代码：

```js
const egg = require('egg');

const workers = Number(process.argv[2] || require('os').cpus().length);
egg.startCluster({
  workers,
  baseDir: __dirname,
});
```

**如果域名需要https**

```js
const path = require('path')

const egg = require('egg')

 

const workers = Number(process.argv[2] || require('os').cpus().length)

egg.startCluster({

  workers,

  baseDir: __dirname,

  port: 5701,

  https: {
    
   key: path.join(__dirname, './ssl/xxx.key'), // https 证书绝对目录
   cert: path.join(__dirname, './ssl/xxx.crt'), // https 证书绝对目录
	 ca: path.join(__dirname, './ssl/xxx.crt'), // https 证书绝对目录
    
  },
})
```



3. 把eggjs所在的项目文件夹复制到服务器中,再npm安装依赖

![image-20221123155231587](http://img.roydust.top/img/202211231552619.png)

```
  cnpm install --production // 安装依赖
```





4. 用PM2启动程序     

```
pm2 start index.js --name server_name // server_name为自定义文件名
```

​	PM简单使用介绍

```
     pm2 start ...   启动项目
     pm2 restart ...   重启项目
     pm2 delete ...   删除项目
     pm2 logs ...     查看日志（也可以直接打开文件查看）
     pm2 gracefulReload ... 这个我用的比较少
```



6. 用Apifox/Postman试试连接

![image-20221123155957172](http://img.roydust.top/img/202211231559219.png)

