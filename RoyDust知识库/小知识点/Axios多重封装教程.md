# Axios多重封装教程

### **axios请求方式**

- 支持多种请求方式: 
  - axios(config)
  - axios.request(config)
  - axios.get(url[, config])
  - axios.delete(url[, config])
  - axios.head(url[, config])
  - axios.post(url[, data[, config]])
  - axios.put(url[, data[, config]])
  - axios.patch(url[, data[, config]])

- 有时候, 我们可能需求同时发送两个请求
  - 使用axios.all, 可以放入多个请求的数组. 
  - axios.all([]) 返回的结果是一个数组，使用 axios.spread 可将数组 [res1,res2] 展开为 res1, res2

### **常见的配置选项**

![image-20220721000059408](https://s2.loli.net/2022/07/21/1ZS4NOBoYIf8EPM.png)

### **axios的实例和拦截器**

- 为什么要创建axios的实例呢? 
  - 当我们从axios模块中导入对象时, 使用的实例是默认的实例. 
  - 当给该实例设置一些默认配置时, 这些配置就被固定下来了. 
  - 但是后续开发中, 某些配置可能会不太一样. 
  - 比如某些请求需要使用特定的baseURL或者timeout或者content-Type等. 
  - 这个时候, 我们就可以创建新的实例, 并且传入属于该实例的配置信息. 

- axios的也可以设置拦截器：拦截每次请求和响应
  - axios.interceptors.request.use(请求成功拦截, 请求失败拦截) 
  - axios.interceptors.response.use(响应成功拦截, 响应失败拦截)



### **区分不同环境**

- 在开发中，有时候我们需要根据不同的环境设置不同的环境变量，常见的有三种环境：
  - 开发环境：development； 
  - 生产环境：production； 
  - 测试环境：test； 

- 如何区分环境变量呢？常见有三种方式：

  - 方式一：手动修改不同的变量；

  ```tsx
  // 1、手动切换不同环境
  const BASE_URL = 'http://lyc.org/dev'
  const BASE_NAME = 'lyc'
  
  const BASE_URL = 'http://lyc.org/prod'
  const BASE_NAME = 'hhh'
  
  const BASE_URL = 'http://lyc.org/test'
  const BASE_NAME = 'test'
  ```

  

  - 方式二：根据process.env.NODE_ENV的值进行区分；

  ```tsx
  // 2.根据process.env.NODE_ENV
  // 开发环境：development
  // 生成环境：production
  // 测试环境：test
  
  let BASE_URL = ''
  const TIME_OUT = 1000
  
  if (process.env.NODE_ENV === 'development') {
    BASE_URL = 'http://123.207.32.32:8000/'
  } else if (process.env.NODE_ENV === 'production') {
    BASE_URL = 'http://lyc.org/prod'
  } else if (process.env.NODE_ENV === 'test') {
    BASE_URL = 'http://lyc.org/test'
  }
  
  export { BASE_URL, TIME_OUT }
  ```

  

  - 方式三：编写不同的环境变量配置文件；

  > 项目根目录下赠加.env.production等等

  ![image-20220721000413561](https://s2.loli.net/2022/07/21/DmLe1V6lMkEG5zd.png)

  ```
  VUE_APP_BASE_URL=http://lyc.org/dev
  VUE_APP_BASE_NAME=lyc
  ```

  

### **axios+ts请求库封装**

#### 目录分析

service

- **index.ts**	service统一出口	创建request实例

- request   request接口层
  - **index.ts**	定义axios的类
  - config.ts   根据process.env.NODE_ENV切换环境
  - type.ts    扩展原来AxiosRequestConfig的参数类型加上了接收响应和返回的拦截器

> /service/index.ts

```tsx
// service统一出口
import YCRequest from './request'
import { BASE_URL, TIME_OUT } from './request/config'

// 创建request实例
const ycRequest = new YCRequest({
  baseURL: BASE_URL,
  timeout: TIME_OUT,
  //实例需要的拦截器
  interceptors: {
    requestInterceptor: (config) => {
      console.log('请求成功拦截')
      return config
    },
    requestInterceptorCatch: (err) => {
      console.log('请求失败拦截')
      return err
    },
    responseInterceptor: (config) => {
      console.log('响应成功拦截')
      return config
    },
    responseInterceptorCatch: (err) => {
      console.log('响应失败拦截')
      return err
    }
  }
})

// 如果有额外的实例要连接
// const ycRequest2 = new YCRequest({
//   baseURL: BASE_URL,
//   timeout: TIME_OUT,
//   interceptors: {
//     requestInterceptor: (config) => {
//       return config
//     },
//     requestInterceptorCatch: (err) => {
//       return err
//     },
//     responseInterceptor: (config) => {
//       return config
//     },
//     responseInterceptorCatch: (err) => {
//       return err
//     }
//   }

export default ycRequest

```

> /service/request/index.ts

```tsx
import axios from 'axios'
import type { AxiosInstance } from 'axios'
import type { YCRequestInterceptors, YCRequestConfig } from './type'

import { ElLoading } from 'element-plus'
import { LoadingInstance } from 'element-plus/lib/components/loading/src/loading'

const DEAFULT_LOADING = true

// 用这种方法封装的类，每次new出来都是一个单独的实例，并且非常具有扩展性
class YCRequest {
  // axios的实例
  instance: AxiosInstance
  // 拦截器 类型来着自己定义的type.ts
  interceptors?: YCRequestInterceptors
  // 判断每个请求是否显示loading
  showLoading?: boolean
  // 自己定义的loading实例，方便取消
  loading?: LoadingInstance

  // 类的构造器 初始化aioxs实例
  constructor(config: YCRequestConfig) {
    // 创建axios实例
    this.instance = axios.create(config)

    // 保存基本信息
    this.showLoading = config.showLoading ?? DEAFULT_LOADING
    this.interceptors = config.interceptors

    // 初始化并且应用拦截器(可选) 从config中取出的拦截器是对应的实例的拦截器
    this.instance.interceptors.request.use(
      this.interceptors?.requestInterceptor,
      this.interceptors?.requestInterceptorCatch
    )
    this.instance.interceptors.response.use(
      this.interceptors?.responseInterceptor,
      this.interceptors?.responseInterceptorCatch
    )

    // 添加所有的实例都有的拦截器
    this.instance.interceptors.request.use(
      (config) => {
        console.log('所有实例都会有的拦截器')
        if (this.showLoading) {
          // 加载时出现loading
          this.loading = ElLoading.service({
            lock: true,
            text: '正在请求数据。。。',
            background: 'rgba(0,0,0,0.5)'
          })
        }
        return config
      },
      (err) => {
        console.log('所有实例都会有的拦截器')
        return err
      }
    )
    this.instance.interceptors.response.use(
      (res) => {
        console.log('所有实例都会有的拦截器')
        // 将loading移除
        this.loading?.close()
        const data = res.data
        if (data.returnCode === '-1001') {
          console.log('请求失败~，错误信息')
        } else {
          return data
        }
      },
      (err) => {
        console.log('所有实例都会有的拦截器')
        // 将loading移除
        this.loading?.close()
        // 例子：判断不同的httpErrorCode显示不同的错误信息
        if (err.response.status === 404) {
          console.log('404的错误')
        }
        return err
      }
    )
  }

  //request方法 传入对应参数
  request<T>(config: YCRequestConfig<T>): Promise<T> {
    return new Promise((resolve, reject) => {
      // 1.单个请求对请求config的处理
      if (config.interceptors?.requestInterceptor) {
        config = config.interceptors.requestInterceptor(config)
      }

      // 2.判断是否显示loading
      if (config.showLoading === false) {
        this.showLoading = config.showLoading
      }

      this.instance
        .request<any, T>(config)
        .then((res) => {
          // 1.单个请求对数据的处理
          if (config.interceptors?.responseInterceptor) {
            res = config.interceptors.responseInterceptor(res)
          }
          console.log(res)

          // 2.将showLoading设置冲true，这样不会影响到下一个请求
          this.showLoading = DEAFULT_LOADING

          // 3.讲结果resolve返回出去
          resolve(res)
        })
        .catch((err) => {
          //将showLoading设置冲true，这样不会影响到下一个请求
          this.showLoading = DEAFULT_LOADING
          reject(err)
          return err
        })
    })
  }
  //定义get请求，就是把config配置解构传入request，并且加上了method
  get<T>(config: YCRequestConfig<T>): Promise<T> {
    return this.request<T>({ ...config, method: 'GET' })
  }

  post<T>(config: YCRequestConfig<T>): Promise<T> {
    return this.request<T>({ ...config, method: 'POST' })
  }

  delete<T>(config: YCRequestConfig<T>): Promise<T> {
    return this.request<T>({ ...config, method: 'DELETE' })
  }

  patch<T>(config: YCRequestConfig<T>): Promise<T> {
    return this.request<T>({ ...config, method: 'PATCH' })
  }
}

export default YCRequest

```

> /service/request/type.ts

```tsx
import type { AxiosRequestConfig, AxiosResponse } from 'axios'

// 新增一个接口类型，接收响应和返回的拦截器
export interface YCRequestInterceptors<T = AxiosResponse> {
  requestInterceptor?: (config: AxiosRequestConfig) => AxiosRequestConfig
  requestInterceptorCatch?: (error: any) => any
  responseInterceptor?: (res: T) => T
  responseInterceptorCatch?: (error: any) => any
}

// 扩展原来AxiosRequestConfig的参数类型加上了接收响应和返回的拦截器
export interface YCRequestConfig<T = AxiosResponse> extends AxiosRequestConfig {
  interceptors?: YCRequestInterceptors<T>
  showLoading?: boolean
}
```

> /service/request/config.ts

```tsx
let BASE_URL = ''
const TIME_OUT = 1000

if (process.env.NODE_ENV === 'development') {
  BASE_URL = 'http://123.207.32.32:8000/'
} else if (process.env.NODE_ENV === 'production') {
  BASE_URL = 'http://lyc.org/prod'
} else if (process.env.NODE_ENV === 'test') {
  BASE_URL = 'http://lyc.org/test'
}

export { BASE_URL, TIME_OUT }
```

#### **应用**

> main.ts

```tsx
import ycRequest from './service'

//可以打印环境变量
console.log(process.env.VUE_APP_BASE_URL)
console.log(process.env.VUE_APP_BASE_NAME)

//根据后端接口数据格式定义返回值接口
interface DataType {
  data: any
  returnCode: string
  success: boolean
}

//调用ycRequest
ycRequest
  .get<DataType>({
    url: '/home/multidata',
    showLoading: true,
  	//每个请求单独需要的拦截器（一般不用单独请求）
    interceptors: {
      requestInterceptor: (config) => {
        console.log('单独请求的config')
        return config
      },
      responseInterceptor: (res) => {
        console.log('单独响应的res')
        return res
      }
    }
  })
  .then((res) => {
    console.log(res.data)
    console.log(res.returnCode)
    console.log(res.success)
  })
```

