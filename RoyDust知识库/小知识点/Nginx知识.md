# Nginx小知识



### Vue打包后，上传到服务器上，但是后端接口是没有代理的，还是用的当前地址

**应为Vue项目打包成静态资源后无法在用proxy进行服务器代理，但可以使用Nginx来实现服务器代理**

原vue中的config.js

```js
  //代理配置
  server: {
    proxy: {
      // 代理所有 /api 的请求，该求情将被代理到 target 中
      '/api': {
        // 代理请求之后的请求地址
        target: 'http://8.130.38.74:6661/',
        rewrite: (path) => path.replace(/^\/api/, ''), //重写地址!!!!
        // 跨域
        changeOrigin: true
      }
    }
  }
```

Nginx设置中的

```js
        
       location /ding/ {
        proxy_pass http://8.130.38.74:6661/;#注意这里/和不加/区别很大哟
        proxy_set_header  X-Real-IP  $remote_addr;
        proxy_set_header  X-Forwarded-For  $proxy_add_x_forwarded_for;
        }
```





### 解决nginx: [error] invalid PID number "" in "/var/run/nginx/nginx.pid"

重启[nginx](https://so.csdn.net/so/search?q=nginx&spm=1001.2101.3001.7020)报错，提示：
[emerg] open() “/var/run/nginx/nginx.pid” failed (2: No such file or directory)
解决：在var/run/下建立一个文件夹命名为nginx，然后：

```vi
[root@localhost ~]# /usr/local/nginx/sbin/nginx 
[root@localhost ~]# /usr/local/nginx/sbin/nginx -s reload 
```

