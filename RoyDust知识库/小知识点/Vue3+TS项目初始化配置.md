# 项目搭建规范

## 一. 代码规范



### 1.1. 集成editorconfig配置

EditorConfig 有助于为不同 IDE 编辑器上处理同一项目的多个开发人员维护一致的编码风格。

```yaml
# http://editorconfig.org

root = true

[*] # 表示所有文件适用
charset = utf-8 # 设置文件字符集为 utf-8
indent_style = space # 缩进风格（tab | space）
indent_size = 2 # 缩进大小
end_of_line = lf # 控制换行类型(lf | cr | crlf)
trim_trailing_whitespace = true # 去除行首的任意空白字符
insert_final_newline = true # 始终在文件末尾插入一个新行

[*.md] # 表示仅 md 文件适用以下规则
max_line_length = off
trim_trailing_whitespace = false
```



VSCode需要安装一个插件：EditorConfig for VS Code

![image-20210722215138665](https://tva1.sinaimg.cn/large/008i3skNgy1gsq2gh989yj30pj05ggmb.jpg)



### 1.2. 使用prettier工具

Prettier 是一款强大的代码格式化工具，支持 JavaScript、TypeScript、CSS、SCSS、Less、JSX、Angular、Vue、GraphQL、JSON、Markdown 等语言，基本上前端能用到的文件格式它都可以搞定，是当下最流行的代码格式化工具。

1.安装prettier

```shell
npm install prettier -D
```

2.配置.prettierrc文件：

* useTabs：使用tab缩进还是空格缩进，选择false；
* tabWidth：tab是空格的情况下，是几个空格，选择2个；
* printWidth：当行字符的长度，推荐80，也有人喜欢100或者120；
* singleQuote：使用单引号还是双引号，选择true，使用单引号；
* trailingComma：在多行输入的尾逗号是否添加，设置为 `none`；
* semi：语句末尾是否要加分号，默认值true，选择false表示不加；

```json
{
  "useTabs": false,
  "tabWidth": 2,
  "printWidth": 80,
  "singleQuote": true,
  "trailingComma": "none",
  "semi": false
}
```



3.创建.prettierignore忽略文件

```
/dist/*
.local
.output.js
/node_modules/**

**/*.svg
**/*.sh

/public/*
```



4.VSCode需要安装prettier的插件

![image-20210722214543454](https://tva1.sinaimg.cn/large/008i3skNgy1gsq2acx21rj30ow057mxp.jpg)

5.测试prettier是否生效

* 测试一：在代码中保存代码；
* 测试二：配置一次性修改的命令；

在package.json中配置一个scripts：

```json
    "prettier": "prettier --write ."
```



### 1.3. 使用ESLint检测

1.在前面创建项目的时候，我们就选择了ESLint，所以Vue会默认帮助我们配置需要的ESLint环境。

2.VSCode需要安装ESLint插件：

![image-20210722215933360](https://tva1.sinaimg.cn/large/008i3skNgy1gsq2oq26odj30pw05faaq.jpg)

3.解决eslint和prettier冲突的问题：

安装插件：（vue在创建项目时，如果选择prettier，那么这两个插件会自动安装）

```shell
npm i eslint-plugin-prettier eslint-config-prettier -D
```

添加prettier插件：

```json
  extends: [
    "plugin:vue/vue3-essential",
    "eslint:recommended",
    "@vue/typescript/recommended",
    "@vue/prettier",
    "@vue/prettier/@typescript-eslint",
    'plugin:prettier/recommended'
  ],
```



### 1.4. git Husky和eslint

虽然我们已经要求项目使用eslint了，但是不能保证组员提交代码之前都将eslint中的问题解决掉了：

* 也就是我们希望保证代码仓库中的代码都是符合eslint规范的；

* 那么我们需要在组员执行 `git commit ` 命令的时候对其进行校验，如果不符合eslint规范，那么自动通过规范进行修复；

那么如何做到这一点呢？可以通过Husky工具：

* husky是一个git hook工具，可以帮助我们触发git提交的各个阶段：pre-commit、commit-msg、pre-push

如何使用husky呢？

这里我们可以使用自动配置命令：

```shell
npx husky-init && npm install
```

这里会做三件事：

1.安装husky相关的依赖：

![image-20210723112648927](https://tva1.sinaimg.cn/large/008i3skNgy1gsqq0o5jxmj30bb04qwen.jpg)

2.在项目目录下创建 `.husky` 文件夹：

```
npx huksy install
```



![image-20210723112719634](https://tva1.sinaimg.cn/large/008i3skNgy1gsqq16zo75j307703mt8m.jpg)

3.在package.json中添加一个脚本：

![image-20210723112817691](https://tva1.sinaimg.cn/large/008i3skNgy1gsqq26phpxj30dj06fgm3.jpg)

接下来，我们需要去完成一个操作：在进行commit时，执行lint脚本：

![image-20210723112932943](https://tva1.sinaimg.cn/large/008i3skNgy1gsqq3hn229j30nf04z74q.jpg)





这个时候我们执行git commit的时候会自动对代码进行lint校验。



### 1.5. git commit规范

#### 1.5.1. 代码提交风格

通常我们的git commit会按照统一的风格来提交，这样可以快速定位每次提交的内容，方便之后对版本进行控制。

![](https://tva1.sinaimg.cn/large/008i3skNgy1gsqw17gaqjj30to0cj3zp.jpg)

但是如果每次手动来编写这些是比较麻烦的事情，我们可以使用一个工具：Commitizen

* Commitizen 是一个帮助我们编写规范 commit message 的工具；

1.安装Commitizen

```shell
npm install commitizen -D
```

2.安装cz-conventional-changelog，并且初始化cz-conventional-changelog：

```shell
npx commitizen init cz-conventional-changelog --save-dev --save-exact
```

这个命令会帮助我们安装cz-conventional-changelog：

![image-20210723145249096](https://tva1.sinaimg.cn/large/008i3skNgy1gsqvz2odi4j30ek00zmx2.jpg)

并且在package.json中进行配置：

![](https://tva1.sinaimg.cn/large/008i3skNgy1gsqvzftay5j30iu04k74d.jpg)

这个时候我们提交代码需要使用 `npx cz`：

* 第一步是选择type，本次更新的类型

| Type     | 作用                                                         |
| -------- | ------------------------------------------------------------ |
| feat     | 新增特性 (feature)                                           |
| fix      | 修复 Bug(bug fix)                                            |
| docs     | 修改文档 (documentation)                                     |
| style    | 代码格式修改(white-space, formatting, missing semi colons, etc) |
| refactor | 代码重构(refactor)                                           |
| perf     | 改善性能(A code change that improves performance)            |
| test     | 测试(when adding missing tests)                              |
| build    | 变更项目构建或外部依赖（例如 scopes: webpack、gulp、npm 等） |
| ci       | 更改持续集成软件的配置文件和 package 中的 scripts 命令，例如 scopes: Travis, Circle 等 |
| chore    | 变更构建流程或辅助工具(比如更改测试环境)                     |
| revert   | 代码回退                                                     |

* 第二步选择本次修改的范围（作用域）

![image-20210723150147510](https://tva1.sinaimg.cn/large/008i3skNgy1gsqw8ca15oj30r600wmx4.jpg)

* 第三步选择提交的信息

![image-20210723150204780](https://tva1.sinaimg.cn/large/008i3skNgy1gsqw8mq3zlj60ni01hmx402.jpg)

* 第四步提交详细的描述信息

![image-20210723150223287](https://tva1.sinaimg.cn/large/008i3skNgy1gsqw8y05bjj30kt01fjrb.jpg)

* 第五步是否是一次重大的更改

![image-20210723150322122](https://tva1.sinaimg.cn/large/008i3skNgy1gsqw9z5vbij30bm00q744.jpg)

* 第六步是否影响某个open issue

![image-20210723150407822](https://tva1.sinaimg.cn/large/008i3skNgy1gsqwar8xp1j30fq00ya9x.jpg)

我们也可以在scripts中构建一个命令来执行 cz：

![image-20210723150526211](https://tva1.sinaimg.cn/large/008i3skNgy1gsqwc4gtkxj30e207174t.jpg)



#### 1.5.2. 代码提交验证

如果我们按照cz来规范了提交风格，但是依然有同事通过 `git commit` 按照不规范的格式提交应该怎么办呢？

* 我们可以通过commitlint来限制提交；

1.安装 @commitlint/config-conventional 和 @commitlint/cli

```shell
npm i @commitlint/config-conventional @commitlint/cli -D
```

2.在根目录创建commitlint.config.js文件，配置commitlint

```js
module.exports = {
  extends: ['@commitlint/config-conventional']
}
```

3.使用husky生成commit-msg文件，验证提交信息：

```shell
npx husky add .husky/commit-msg "npx --no-install commitlint --edit $1"
```



## 二. 第三方库集成

### 2.1. vue.config.js配置

 有三种配置方式：

* 方式一：直接通过CLI提供给我们的选项来配置：
  * 比如publicPath：配置应用程序部署的子目录（默认是 `/`，相当于部署在 `https://www.my-app.com/`）；
  * 比如outputDir：修改输出的文件夹；
* 方式二：通过configureWebpack修改webpack的配置：
  * 可以是一个对象，直接会被合并；
  * 可以是一个函数，会接收一个config，可以通过config来修改配置；
* 方式三：通过chainWebpack修改webpack的配置：
  * 是一个函数，会接收一个基于  [webpack-chain](https://github.com/mozilla-neutrino/webpack-chain) 的config对象，可以对配置进行修改；

```js
const path = require('path')

module.exports = {
  outputDir: './build',
  // configureWebpack: {
  //   resolve: {
  //     alias: {
  //       views: '@/views'
  //     }
  //   }
  // }
  // configureWebpack: (config) => {
  //   config.resolve.alias = {
  //     '@': path.resolve(__dirname, 'src'),
  //     views: '@/views'
  //   }
  // },
  chainWebpack: (config) => {
    config.resolve.alias.set('@', path.resolve(__dirname, 'src')).set('views', '@/views')
  }
}
```





### 2.2. vue-router集成

安装vue-router的最新版本：

```shell
npm install vue-router@next
```

创建router对象：

```ts
import { createRouter, createWebHashHistory } from 'vue-router'
import { RouteRecordRaw } from 'vue-router'

const routes: RouteRecordRaw[] = [
  {
    path: '/',
    redirect: '/main'
  },
  {
    path: '/main',
    component: () => import('../views/main/main.vue')
  },
  {
    path: '/login',
    component: () => import('../views/login/login.vue')
  }
]

const router = createRouter({
  routes,
  history: createWebHashHistory()
})

export default router
```

安装router：

```ts
import router from './router'

createApp(App).use(router).mount('#app')
```

在App.vue中配置跳转：

```html
<template>
  <div id="app">
    <router-link to="/login">登录</router-link>
    <router-link to="/main">首页</router-link>
    <router-view></router-view>
  </div>
</template>
```



### 2.3. vuex集成

安装vuex：

```shell
npm install vuex@next
```

创建store对象：

```ts
import { createStore } from 'vuex'

const store = createStore({
  state() {
    return {
      name: 'coderwhy'
    }
  }
})

export default store
```

安装store：

```ts
createApp(App).use(router).use(store).mount('#app')
```

在App.vue中使用：

```html
<h2>{{ $store.state.name }}</h2>
```



### 2.4. element-plus集成

Element Plus，一套为开发者、设计师和产品经理准备的基于 Vue 3.0 的桌面端组件库：

* 相信很多同学在Vue2中都使用过element-ui，而element-plus正是element-ui针对于vue3开发的一个UI组件库；
* 它的使用方式和很多其他的组件库是一样的，所以学会element-plus，其他类似于ant-design-vue、NaiveUI、VantUI都是差不多的；

安装element-plus

```shell
npm install element-plus
```



#### 2.4.1. 全局引入

一种引入element-plus的方式是全局引入，代表的含义是所有的组件和插件都会被自动注册：

```js
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'

import router from './router'
import store from './store'

createApp(App).use(router).use(store).use(ElementPlus).mount('#app')
```



#### 2.4.2. 局部引入

也就是在开发中用到某个组件对某个组件进行引入：

```vue
<template>
  <div id="app">
    <router-link to="/login">登录</router-link>
    <router-link to="/main">首页</router-link>
    <router-view></router-view>

    <h2>{{ $store.state.name }}</h2>

    <el-button>默认按钮</el-button>
    <el-button type="primary">主要按钮</el-button>
    <el-button type="success">成功按钮</el-button>
    <el-button type="info">信息按钮</el-button>
    <el-button type="warning">警告按钮</el-button>
    <el-button type="danger">危险按钮</el-button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import { ElButton } from 'element-plus'

export default defineComponent({
  name: 'App',
  components: {
    ElButton
  }
})
</script>

<style lang="less">
</style>
```

但是我们会发现是没有对应的样式的，引入样式有两种方式：

* 全局引用样式（像之前做的那样）；
* 局部引用样式（通过babel的插件）；

1.安装babel的插件：

```shell
npm install babel-plugin-import -D
```

2.配置babel.config.js

```js
module.exports = {
  plugins: [
    [
      'import',
      {
        libraryName: 'element-plus',
        customStyleName: (name) => {
          return `element-plus/lib/theme-chalk/${name}.css`
        }
      }
    ]
  ],
  presets: ['@vue/cli-plugin-babel/preset']
}
```



但是这里依然有个弊端：

* 这些组件我们在多个页面或者组件中使用的时候，都需要导入并且在components中进行注册；
* 所以我们可以将它们在全局注册一次；

> src/global/register-element.ts

```tsx
import 'element-plus/dist/index.css'
import { App } from 'vue'
import {
  ElAlert,
  ElAside,
  ElButton,
  ElForm,
  ElFormItem,
  ElInput,
  ElRadio
} from 'element-plus'

const components = [
  ElAlert,
  ElAside,
  ElButton,
  ElForm,
  ElFormItem,
  ElInput,
  ElRadio
]
export default function (app: App): void {
  for (const component of components) {
    app.component(component.name, component)
  }
}
```

> src/global/index.ts

```tsx
import { App } from 'vue'
import registerElement from './register-element'
export function globalregister(app: App): void {
  app.use(registerElement)
}
```

### 2.5. axios集成

安装axios：

```shell
npm install axios
```

封装axios：

```ts
import axios, { AxiosInstance, AxiosRequestConfig, AxiosResponse } from 'axios'
import { Result } from './types'
import { useUserStore } from '/@/store/modules/user'

class HYRequest {
  private instance: AxiosInstance

  private readonly options: AxiosRequestConfig

  constructor(options: AxiosRequestConfig) {
    this.options = options
    this.instance = axios.create(options)

    this.instance.interceptors.request.use(
      (config) => {
        const token = useUserStore().getToken
        if (token) {
          config.headers.Authorization = `Bearer ${token}`
        }
        return config
      },
      (err) => {
        return err
      }
    )

    this.instance.interceptors.response.use(
      (res) => {
        // 拦截响应的数据
        if (res.data.code === 0) {
          return res.data.data
        }
        return res.data
      },
      (err) => {
        return err
      }
    )
  }

  request<T = any>(config: AxiosRequestConfig): Promise<T> {
    return new Promise((resolve, reject) => {
      this.instance
        .request<any, AxiosResponse<Result<T>>>(config)
        .then((res) => {
          resolve((res as unknown) as Promise<T>)
        })
        .catch((err) => {
          reject(err)
        })
    })
  }

  get<T = any>(config: AxiosRequestConfig): Promise<T> {
    return this.request({ ...config, method: 'GET' })
  }

  post<T = any>(config: AxiosRequestConfig): Promise<T> {
    return this.request({ ...config, method: 'POST' })
  }

  patch<T = any>(config: AxiosRequestConfig): Promise<T> {
    return this.request({ ...config, method: 'PATCH' })
  }

  delete<T = any>(config: AxiosRequestConfig): Promise<T> {
    return this.request({ ...config, method: 'DELETE' })
  }
}

export default HYRequest
```



### 2.6. VSCode配置	(不一定要一样)

```json
{
  "workbench.iconTheme": "vscode-great-icons",
  "editor.fontSize": 17,
  "eslint.migration.2_x": "off",
  "[javascript]": {
    "editor.defaultFormatter": "dbaeumer.vscode-eslint"
  },
  "files.autoSave": "afterDelay",
  "editor.tabSize": 2,
  "terminal.integrated.fontSize": 16,
  "editor.renderWhitespace": "all",
  "editor.quickSuggestions": {
    "strings": true
  },
  "debug.console.fontSize": 15,
  "window.zoomLevel": 1,
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },
  "explorer.confirmDragAndDrop": false,
  "workbench.tree.indent": 16,
  "javascript.updateImportsOnFileMove.enabled": "always",
  "editor.wordWrap": "on",
  "path-intellisense.mappings": {
    "@": "${workspaceRoot}/src"
  },
  "hediet.vscode-drawio.local-storage": "eyIuZHJhd2lvLWNvbmZpZyI6IntcImxhbmd1YWdlXCI6XCJcIixcImN1c3RvbUZvbnRzXCI6W10sXCJsaWJyYXJpZXNcIjpcImdlbmVyYWw7YmFzaWM7YXJyb3dzMjtmbG93Y2hhcnQ7ZXI7c2l0ZW1hcDt1bWw7YnBtbjt3ZWJpY29uc1wiLFwiY3VzdG9tTGlicmFyaWVzXCI6W1wiTC5zY3JhdGNocGFkXCJdLFwicGx1Z2luc1wiOltdLFwicmVjZW50Q29sb3JzXCI6W1wiRkYwMDAwXCIsXCIwMENDNjZcIixcIm5vbmVcIixcIkNDRTVGRlwiLFwiNTI1MjUyXCIsXCJGRjMzMzNcIixcIjMzMzMzM1wiLFwiMzMwMDAwXCIsXCIwMENDQ0NcIixcIkZGNjZCM1wiLFwiRkZGRkZGMDBcIl0sXCJmb3JtYXRXaWR0aFwiOjI0MCxcImNyZWF0ZVRhcmdldFwiOmZhbHNlLFwicGFnZUZvcm1hdFwiOntcInhcIjowLFwieVwiOjAsXCJ3aWR0aFwiOjExNjksXCJoZWlnaHRcIjoxNjU0fSxcInNlYXJjaFwiOnRydWUsXCJzaG93U3RhcnRTY3JlZW5cIjp0cnVlLFwiZ3JpZENvbG9yXCI6XCIjZDBkMGQwXCIsXCJkYXJrR3JpZENvbG9yXCI6XCIjNmU2ZTZlXCIsXCJhdXRvc2F2ZVwiOnRydWUsXCJyZXNpemVJbWFnZXNcIjpudWxsLFwib3BlbkNvdW50ZXJcIjowLFwidmVyc2lvblwiOjE4LFwidW5pdFwiOjEsXCJpc1J1bGVyT25cIjpmYWxzZSxcInVpXCI6XCJcIn0ifQ==",
  "hediet.vscode-drawio.theme": "Kennedy",
  "editor.fontFamily": "Source Code Pro, 'Courier New', monospace",
  "editor.smoothScrolling": true,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "workbench.colorTheme": "Atom One Dark",
  "vetur.completion.autoImport": false,
  "security.workspace.trust.untrustedFiles": "open",
  "eslint.lintTask.enable": true,
  "eslint.alwaysShowStatus": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```



## 三. 接口文档

https://documenter.getpostman.com/view/12387168/TzsfmQvw

baseURL的值：

```
http://152.136.185.210:5000
```

设置全局token的方法：

```js
const res = pm.response.json();
pm.globals.set("token", res.data.token);
```



接口文档v2版本：（有部分更新）

**https://documenter.getpostman.com/view/12387168/TzzDKb12**









## 后台CMS项目分析

### 组件的抽离

![image-20220731184825759](https://s2.loli.net/2022/07/31/RobIrQGfZDEPTlJ.png)

三层封装

view页面层->components组件层->base-ui基础组件层

#### 通用组件

自定义公共组件base-ui，是最抽象最基础的组件

> ./base-ui/form/src/from.vue

根据传入的formItems参数来生成相应的组件，双向绑定modelValue[`${item.field}`]，发生改变时就调用handleValueChange传回父元素


```vue
<template>
  <div class="hy-form">
    <div class="header">
      <slot name="header"></slot>
    </div>
    <el-form :label-width="labelWidth">
      <el-row>
        <template v-for="item in formItems" :key="item.label">
          <el-col v-bind="colLayout">
            <el-form-item
              v-if="!item.isHidden"
              :label="item.label"
              :rules="item.rules"
              :style="itemStyle"
            >
              <template
                v-if="item.type === 'input' || item.type === 'password'"
              >
                <el-input
                  v-bind="item.otherOptions"
                  :placeholder="item.placeholder"
                  :show-password="item.type === 'password'"
                  :model-value="modelValue[`${item.field}`]"
                  @update:modelValue="handleValueChange($event, item.field)"
                />
              </template>
              <template v-else-if="item.type === 'select'">
                <el-select
                  :placeholder="item.placeholder"
                  style="width: 100%"
                  :model-value="modelValue[`${item.field}`]"
                  @update:modelValue="handleValueChange($event, item.field)"
                >
                  <el-option
                    v-bind="item.otherOptions"
                    v-for="option in item.options"
                    :key="option.value"
                    :value="option.value"
                  >
                    {{ option.title }}
                  </el-option>
                </el-select>
              </template>
              <template v-else-if="item.type === 'datepicker'">
                <el-date-picker
                  style="width: 100%"
                  v-bind="item.otherOptions"
                  :model-value="modelValue[`${item.field}`]"
                  @update:modelValue="handleValueChange($event, item.field)"
                />
              </template>
            </el-form-item> </el-col
        ></template>
      </el-row>
    </el-form>
    <div class="footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref, watch, computed } from 'vue'
import { IFormItem } from '../types'
export default defineComponent({
  props: {
    modelValue: {
      type: Object,
      required: true
    },
    formItems: {
      type: Array as PropType<IFormItem[]>,
      default: () => []
    },
    labelWidth: {
      type: String,
      default: '100px'
    },
    itemStyle: {
      type: Object,
      default: () => ({ padding: '10px 40px' })
    },
    colLayout: {
      type: Object,
      default: () => ({
        xl: 6,
        lg: 8,
        md: 12,
        sm: 24,
        sx: 24
      })
    }
  },
  emits: ['update:modelValue'],
  setup(props, { emit }) {
    const handleValueChange = (value: any, field: string) => {
      emit('update:modelValue', { ...props.modelValue, [field]: value })
    }
    return { handleValueChange }
  }
})
</script>
<style lang="less" scoped>
.hy-form {
  padding-top: 22px;
}
</style>

```

> ./base-ui/form/types/index.ts

这里存放vue接收的值的TS类型

```tsx
type IFormType = 'input' | 'password' | 'select' | 'datepicker'

export interface IFormItem {
  field: string
  type: IFormType
  label: string
  rules?: any[]
  placeholder?: any
  // 针对select
  options?: any[]
  // 针对特殊的属性
  otherOptions?: any
  isHidden?: boolean
}

export interface IForm {
  formItems: IFormItem[]
  lableWidth?: string
  colLayout?: any
  itemStyle?: any
}
```



> ./base-ui/form/index.ts

最后index做改组件的出口

```tsx
import HyForm from './src/form.vue'

export * from './types'

export default HyForm
```



#### 公共组件

> ./components/page-content/src/page-content.vue

- 获取父组件view传来的contentTableConfig配置文件并且交给通用子组件form
- 设置自定义的插槽和动态插槽，满足不同页面对组件的特殊需求
- 这里会请求此次登录的用户有没有操作权限，根据权限判断按钮的有无


```vue
<template>
  <div class="page-content">
    <HyTable
      :listData="dataList"
      :listCount="dataCount"
      v-bind="contentTableConfig"
      v-model:page="pageInfo"
    >
      <!-- haeder中的插槽 -->
      <template #headerHandler>
        <el-button
          v-if="isCreate"
          type="primary"
          size="medium"
          @click="handleNewClick"
        >
          新建数据
        </el-button>
      </template>

      <!-- 列中的固定插槽 -->
      <template #status="scope">
        <el-button
          plain
          size="mini"
          :type="scope.row.enable ? 'success' : 'danger'"
          >{{ scope.row.enable ? '启用' : '禁用' }}</el-button
        >
      </template>
      <template #createAt="scope">
        <span>{{ $filters.formatTime(scope.row.createAt) }}</span>
      </template>
      <template #updateAt="scope">
        <span>{{ $filters.formatTime(scope.row.createAt) }}</span>
      </template>
      <template #handler="scope">
        <div class="handle-btns">
          <el-button
            v-if="isUpdate"
            size="mini"
            type="text"
            @click="handleEditClick(scope.row)"
          >
            编辑
          </el-button>
          <el-button
            v-if="isDelete"
            size="mini"
            type="text"
            @click="handleDeleteClick(scope.row)"
            >删除</el-button
          >
        </div>
      </template>

      <!-- 在pageContent中动态插入剩余的插槽 -->
      <template
        v-for="item in otherPropSlots"
        :key="item.prop"
        #[item.slotName]="scope"
      >
        <template v-if="item.slotName">
          <slot :name="item.slotName" :row="scope.row"></slot>
        </template>
      </template>
    </HyTable>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed, ref, watch } from 'vue'
import { useStore } from '@/store'

import HyTable from '@/base-ui/table'
import { usePermission } from '@/hooks/use-permission'

export default defineComponent({
  components: {
    HyTable
  },
  props: {
    contentTableConfig: {
      type: Object,
      require: true
    },
    pageName: {
      type: String,
      required: true
    }
  },
  emits: ['newBtnClick', 'editBtnClick'],
  setup(props, { emit }) {
    const store = useStore()
    // 0.获取操作的权限
    const isCreate = usePermission(props.pageName, 'create')
    const isUpdate = usePermission(props.pageName, 'update')
    const isDelete = usePermission(props.pageName, 'delete')
    const isQuery = usePermission(props.pageName, 'query')

    // 1.双向绑定pageInfo(实现翻页)
    const pageInfo = ref({ currentPage: 1, pageSize: 10 })
    watch(pageInfo, () => {
      getPageData()
    })

    // 2.发送网络请求
    const getPageData = (queryInfo: any = {}) => {
      // 没有权限直接返回
      if (!isQuery) return
      store.dispatch('system/getPageListAction', {
        pageName: props.pageName,
        queryInfo: {
          offset: (pageInfo.value.currentPage - 1) * pageInfo.value.pageSize,
          size: pageInfo.value.pageSize,
          ...queryInfo
        }
      })
    }
    getPageData()

    // 3.从vuex中获取数据
    const dataList = computed(() =>
      store.getters[`system/pageListData`](props.pageName)
    )
    const dataCount = computed(() =>
      store.getters[`system/pageListCount`](props.pageName)
    )

    // 4.获取其他的动态插槽名称
    const otherPropSlots = props.contentTableConfig?.propList.filter(
      (item: any) => {
        if (item.slotName === 'status') return false
        if (item.slotName === 'createAt') return false
        if (item.slotName === 'updateAt') return false
        if (item.slotName === 'handler') return false
        return true
      }
    )

    // 5.删除/新建/编辑逻辑
    const handleDeleteClick = (item: any) => {
      console.log(item)
      store.dispatch('system/deletePageDataAction', {
        pageName: props.pageName,
        id: item.id
      })
    }

    const handleNewClick = () => {
      emit('newBtnClick')
    }

    const handleEditClick = (item: any) => {
      emit('editBtnClick', item)
    }

    return {
      dataList,
      dataCount,
      pageInfo,
      getPageData,
      otherPropSlots,
      isCreate,
      isUpdate,
      isDelete,
      handleDeleteClick,
      handleNewClick,
      handleEditClick
    }
  }
})
</script>
<style lang="less" scoped>
.page-content {
  padding: 20px;
  border-top: 20px solid #f5f5f5;
}
</style>

```



> ./components/page-content/index.ts

同理公共组件也是做一个index做接口

```tsx
import PageContent from './src/page-content.vue'

export default PageContent

```



### 抽离封装配置文件

**管理员按钮权限判断**

![image-20220804005603127](https://s2.loli.net/2022/08/04/YyWbhcqTNkDKBVC.png)

先收集全部权限资格到一个数组，再用一个hook判断该用户在当前页面有没有这个按钮的权限

> ./views/user/user.vue

由于上面抽离组件后，不同的页面只需要简单的设置页面和填写配置文件就可以了,甚至控制修改和新增的弹出层都抽离为一个hook

```vue
<template>
  <div class="user">
    <PageSearch
      :searchFormConfig="searchFormConfig"
      @resetBtnClick="handleResetClick"
      @queryBtnClick="handleQueryClick"
    ></PageSearch>
    <PageContent
      ref="pageContentRef"
      :contentTableConfig="contentTableConfig"
      pageName="users"
      @newBtnClick="handleNewData"
      @editBtnClick="handleEditData"
    ></PageContent>
    <PageModal
      :defaultInfo="defaultInfo"
      ref="pageModalRef"
      :modalConfig="modalConfigRef"
      pageName="users"
    ></PageModal>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed } from 'vue'
import { useStore } from '@/store'

import PageSearch from '@/components/page-search'
import PageContent from '@/components/page-content'
import PageModal from '@/components/page-modal'

import { searchFormConfig } from './config/search.config'
import { contentTableConfig } from './config/content.config'
import { modalConfig } from './config/modal.config'

// 控制content页面内容的搜索功能
import { usePageSearch } from '@/hooks/use-page-search'
// 控制新建和修改功能的弹出页面
import { usePageModal } from '@/hooks/use-page-modal'

export default defineComponent({
  name: 'users',
  components: {
    PageSearch,
    PageContent,
    PageModal
  },
  setup() {
    const [pageContentRef, handleQueryClick, handleResetClick] = usePageSearch()

    // pageModal相关的hook逻辑
    // 1.处理密码显示逻辑
    const newCallback = () => {
      const passwordItem = modalConfig.formItems.find(
        (item) => item.field === 'password'
      )
      passwordItem!.isHidden = false
    }
    const editCallback = () => {
      const passwordItem = modalConfig.formItems.find(
        (item) => item.field === 'password'
      )
      passwordItem!.isHidden = true
    }

    // 2.动态添加部门和角色列表
    const store = useStore()
    // 用computed来实现监听vuex动态数据的数据变化 把所有对modalConfig有依赖的函数放到modalConfigRef来
    const modalConfigRef = computed(() => {
      const departmentId = modalConfig.formItems.find(
        (item) => item.field === 'departmentId'
      )
      departmentId!.options = store.state.entireDepartment.map((item) => {
        return { title: item.name, value: item.id }
      })

      const roleItem = modalConfig.formItems.find(
        (item) => item.field === 'roleId'
      )
      roleItem!.options = store.state.entireRole.map((item) => {
        return { title: item.name, value: item.id }
      })
      return modalConfig
    })

    // 3.调用hook获取公共变量和函数
    const [pageModalRef, defaultInfo, handleNewData, handleEditData] =
      usePageModal(newCallback, editCallback)

    return {
      searchFormConfig,
      contentTableConfig,
      modalConfigRef,
      pageContentRef,
      handleResetClick,
      handleQueryClick,
      pageModalRef,
      defaultInfo,
      handleNewData,
      handleEditData
    }
  }
})
</script>

<style lang="less" scoped></style>

```

> ./views/user/config/content.config.ts

剩下的就是填写配置文件

```tsx
export const contentTableConfig = {
  title: '用户列表',
  propList: [
    {
      prop: 'name',
      label: '用户名',
      minWidth: '100'
    },
    {
      prop: 'realname',
      label: '真实姓名',
      minWidth: '100'
    },
    {
      prop: 'cellphone',
      label: '手机号码',
      minWidth: '100'
    },
    {
      prop: 'enable',
      label: '状态',
      minWidth: '100',
      slotName: 'status'
    },
    {
      prop: 'createAt',
      label: '创建时间',
      minWidth: '250',
      slotName: 'createAt'
    },
    {
      prop: 'updateAt',
      label: '更新时间',
      minWidth: '250',
      slotName: 'updateAt'
    },
    {
      label: '操作',
      minWidth: '120',
      slotName: 'handler'
    }
  ],
  showIndexColumn: true,
  showSelectColumn: true
}
```



### 由后端动态生成的路由权限控制

**权限控制的前后端逻辑**

<img src="http://img.roydust.top/img/202210192035038.png" alt="image-20220724175615640"  />

**路由的设计方案**

1. 写死，将所有路由注册

   缺点：可以通过url直接转跳到页面

2. 不同的角色注册不同的路由:
   superadmin: [{}, {}, {}]
   admin: [{}, {}]
   user:[{}]
   登录-> userInfo -> role.name ->动态的加载数组[] -> main .routes
   缺点：新增运营角色: [{},{}]=>修改前端代码=>重新部署

3. 菜单动态生成路由映射

   ![image-20220724180739139](http://img.roydust.top/img/202210192035377.png)



> nav-menu 组件

menu组件从vuex中获取用户能看见的权限菜单，再显示出来

```vue
<template>
  <div class="nav-menu">
    <div class="logo">
      <img class="img" src="~@/assets/img/logo.svg" alt="logo" />
      <span v-if="!collapse" class="title">Vue3+TS</span>
    </div>
    <el-menu
      :default-active="defaultValue"
      :collapse="collapse"
      class="el-menu-vertical"
      background-color="#0c2135"
      text-color="#b7bdc3"
      active-text-color="#0a60bd"
    >
      <template v-for="item in userMenus" :key="item.id">
        <!-- 二级菜单 -->
        <template v-if="item.type === 1">
          <!-- 二级菜单可以展开的标题 -->
          <el-sub-menu :index="item.id + ''">
            <template #title>
              <!-- <i v-if="item.icon" :class="item.icon"></i> -->
              <Grid style="width: 1em; height: 1em; margin-right: 8px" />
              <span>{{ item.name }}</span>
            </template>
            <!-- 遍历里面的item  -->
            <template v-for="subitem in item.children" :key="subitem.id">
              <el-menu-item
                :index="subitem.id + ''"
                @click="handleMenuItemClick(subitem)"
              >
                <i v-if="subitem.icon" :class="subitem.icon"></i>
                <span>{{ subitem.name }}</span>
              </el-menu-item>
            </template>
          </el-sub-menu>
        </template>
        <!-- 一级菜单 -->
        <template v-else-if="item.type === 2">
          <el-menu-item :index="item.id + ''">
            <i v-if="item.icon" :class="item.icon"></i>
            <span>{{ item.name }}</span>
          </el-menu-item>
        </template>
      </template>
    </el-menu>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed, ref } from 'vue'
import { useStore } from '@/store'
import { useRouter, useRoute } from 'vue-router'

import { pathMapToMenu } from '@/utils/map-menus'

export default defineComponent({
  props: {
    collapse: {
      type: Boolean,
      default: false
    }
  },
  setup() {
    // store
    const store = useStore()
    const userMenus = computed(() => store.state.login.userMenus)

    // router
    const router = useRouter()
    const route = useRoute()
    const currentPath = route.path

    // data
    const menu = pathMapToMenu(userMenus.value, currentPath)
    const defaultValue = ref(menu.id + '')

    const handleMenuItemClick = (item: any) => {
      // console.log(item)
      router.push({
        path: item.url ?? '/not-found'
      })
    }
    return { userMenus, defaultValue, handleMenuItemClick }
  }
})
</script>
<style lang="less" scoped>
.nav-menu {
  height: 100%;
  background-color: #001529;

  .logo {
    display: flex;
    height: 28px;
    padding: 12px 10px 8px 10px;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;

    .img {
      height: 100%;
      margin: 0 10px;
    }

    .title {
      font-size: 16px;
      font-weight: 700;
      color: white;
    }
  }

  .el-menu {
    border-right: none;
  }

  // 目录
  .el-sub-menu {
    background-color: #001529 !important;
    // 二级菜单 ( 默认背景 )
    .el-menu-item {
      padding-left: 50px !important;
      background-color: #0c2135 !important;
    }
  }

  ::v-deep .el-submenu__title {
    background-color: #001529 !important;
  }

  // hover 高亮
  .el-menu-item:hover {
    color: #fff !important; // 菜单
  }

  .el-menu-item.is-active {
    color: #fff !important;
    background-color: #0a60bd !important;
  }
}

.el-menu-vertical:not(.el-menu--collapse) {
  width: 100%;
  height: calc(100% - 48px);
}
</style>
```



> map-menus 这个是动态路由的核心hook

```tsx
import { IBreadcrumb } from '@/base-ui/breadcrumb/types'
import { RouteRecordRaw } from 'vue-router'

let firstMenu: any = null

export function mapMenusToRoutes(userMenus: any[]): RouteRecordRaw[] {
  const routes: RouteRecordRaw[] = []

  // 1.先去加载默认所有的routes[]
  const allRoutrs: RouteRecordRaw[] = []
  const routeFiles = require.context('../router/main', true, /\.ts/)
  routeFiles.keys().forEach((key) => {
    const route = require('../router/main' + key.split('.')[1])
    allRoutrs.push(route.default)
  })

  // 2.根据菜单获取需要添加的routes
  // 递归查找type为2并且路由相匹配时 添加进去
  const _recurseGetRoute = (menus: any[]) => {
    for (const menu of menus) {
      if (menu.type === 2) {
        const route = allRoutrs.find((route) => {
          return route.path === menu.url
        })
        if (route) routes.push(route)
        if (!firstMenu) {
          firstMenu = menu
        }
      } else {
        _recurseGetRoute(menu.children)
      }
    }
  }

  _recurseGetRoute(userMenus)

  return routes
}

// 获取面包屑数据
export function pathMapToBreadcrumbs(userMenus: any[], currentPath: string) {
  const breadcrumbs: IBreadcrumb[] = []
  pathMapToMenu(userMenus, currentPath, breadcrumbs)
  return breadcrumbs
}

// 拿到权限菜单 递归调用
export function pathMapToMenu(
  userMenus: any[],
  currentPath: string,
  breadcrumbs?: IBreadcrumb[]
): any {
  for (const menu of userMenus) {
    if (menu.type === 1) {
      const findMenu = pathMapToMenu(menu.children ?? [], currentPath)
      if (findMenu) {
        breadcrumbs?.push({ name: menu.name })
        breadcrumbs?.push({ name: findMenu.name })
        return findMenu
      }
    } else if (menu.type === 2 && menu.url === currentPath) {
      return menu
    }
  }
}

// 获取所有的菜单
export function mapMenusToPermissions(userMenus: any[]) {
  const permissions: string[] = []
  const _recurseGetPermisson = (menus: any[]) => {
    for (const menu of menus) {
      if (menu.type === 1 || menu.type === 2) {
        _recurseGetPermisson(menu.children ?? [])
      } else if (menu.type === 3) {
        permissions.push(menu.permission)
      }
    }
  }
  _recurseGetPermisson(userMenus)
  return permissions
}

// 获取所有的menu的id
export function getMapLeafKeys(menuList: any[]) {
  const leftKeys: number[] = []

  const _recurseGetLeaf = (menuList: any[]) => {
    for (const menu of menuList) {
      if (menu.children) {
        _recurseGetLeaf(menu.children)
      } else {
        leftKeys.push(menu.id)
      }
    }
  }
  _recurseGetLeaf(menuList)
  return leftKeys
}

export { firstMenu }
```



> vuex里面的login登录逻辑

```tsx
import { Module } from 'vuex'
import router from '@/router'

import {
  accountLoginRequest,
  requestUserInfoById,
  requestUserMenusByRoleId
} from '@/service/login/login'
import { mapMenusToRoutes, mapMenusToPermissions } from '@/utils/map-menus'
import localCache from '@/utils/cache'

import { IAccount } from '@/service/login/type'
import { IRootState } from '../type'
import { ILoginState } from './type'

const loginModule: Module<ILoginState, IRootState> = {
  namespaced: true,
  state() {
    return {
      token: '',
      userInfo: '',
      userMenus: [],
      permissions: []
    }
  },
  mutations: {
    changeToken(state, token: string) {
      state.token = token
    },
    changeUserInfo(state, userInfo: any) {
      state.userInfo = userInfo
    },
    changeUserMenus(state, userMenus: any) {
      state.userMenus = userMenus

      console.log('注册动态路由')

      // userMenus => routes
      const routes = mapMenusToRoutes(userMenus)

      // 将routes => router.main.children
      routes.forEach((route) => {
        router.addRoute('main', route)
      })

      // 获取用户按钮的权限
      const permissions = mapMenusToPermissions(userMenus)
      state.permissions = permissions
    }
  },
  getters: {},
  actions: {
    async accountLoginAction({ commit, dispatch }, payload: IAccount) {
      // 1.实现登入逻辑
      const loginResult = await accountLoginRequest(payload)
      // console.log(loginResult)
      const { id, token } = loginResult.data
      commit('changeToken', token)
      localCache.setCache('token', token)

      // 发送初始化请求（完整的role/department)
      dispatch('getInitialDataAction', null, { root: true })

      // 2.请求用户信息
      const userInfoResult = await requestUserInfoById(id)
      const userInfo = userInfoResult.data
      commit('changeUserInfo', userInfo)
      localCache.setCache('userInfo', userInfo)
      // 3.请求用户菜单
      const userMenusBesult = await requestUserMenusByRoleId(userInfo.role.id)
      const userMenus = userMenusBesult.data
      commit('changeUserMenus', userMenus)
      localCache.setCache('userMenus', userMenus)
      // 4.跳转到首页
      router.push('/main')
    },
    phoneLoginAction({ commit }, payload: any) {
      console.log('执行phoneLoginAction', payload)
    },
    loadLocalLogin({ commit, dispatch }) {
      const token = localCache.getCache('token')
      if (token) {
        commit('changeToken', token)
        // 发送初始化请求（完整的role/department)
        dispatch('getInitialDataAction', null, { root: true })
      }
      const userInfo = localCache.getCache('userInfo')
      if (userInfo) {
        commit('changeUserInfo', userInfo)
      }
      const userMenus = localCache.getCache('userMenus')
      if (userMenus) {
        commit('changeUserMenus', userMenus)
      }
    }
  }
}
export default loginModule
```



### 多层封装的Aioxs，拦截不同的请求



> ./service/request/index.ts

三层封装,可以对每一个请求实例进行拦截,也可以对一个new出来的request实例进行拦截

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
        // console.log('所有实例都会有的拦截器')
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
        // console.log('所有实例都会有的拦截器')
        return err
      }
    )
    this.instance.interceptors.response.use(
      (res) => {
        // console.log('所有实例都会有的拦截器')
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
        // console.log('所有实例都会有的拦截器')
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
  request<T = any>(config: YCRequestConfig<T>): Promise<T> {
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
  get<T = any>(config: YCRequestConfig<T>): Promise<T> {
    return this.request<T>({ ...config, method: 'GET' })
  }

  post<T = any>(config: YCRequestConfig<T>): Promise<T> {
    return this.request<T>({ ...config, method: 'POST' })
  }

  delete<T = any>(config: YCRequestConfig<T>): Promise<T> {
    return this.request<T>({ ...config, method: 'DELETE' })
  }

  patch<T = any>(config: YCRequestConfig<T>): Promise<T> {
    return this.request<T>({ ...config, method: 'PATCH' })
  }
}

export default YCRequest
```



> ./service/index.ts

```tsx
// service统一出口
import YCRequest from './request'
import { BASE_URL, TIME_OUT } from './request/config'

import localCache from '@/utils/cache'

// 创建request实例
const ycRequest = new YCRequest({
  baseURL: BASE_URL,
  timeout: TIME_OUT,
  interceptors: {
    requestInterceptor: (config: any) => {
      // 携带token的拦截
      const token = localCache.getCache('token')
      if (token) {
        config.headers.Authorization = `Bearer ${token}`
      }
      return config
      // console.log('请求成功拦截')
      return config
    },
    requestInterceptorCatch: (err) => {
      // console.log('请求失败拦截')
      return err
    },
    responseInterceptor: (config) => {
      // console.log('响应成功拦截')
      return config
    },
    responseInterceptorCatch: (err) => {
      // console.log('响应失败拦截')
      return err
    }
  }
})

// 如果有额外的接口要连接
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



> 应用API层

```tsx
import ycRequest from '../index'
import { IAccount, IloginResult } from './type'
import { IDataType } from '../types'

enum LoginAPI {
  AccountLogin = '/login',
  LoginUserInfo = '/users/',
  UserMenus = '/role/' //用法
}

export function accountLoginRequest(account: IAccount) {
  return ycRequest.post<IDataType<IloginResult>>({
    url: LoginAPI.AccountLogin,
    data: account
  })
}

export function requestUserInfoById(id: number) {
  return ycRequest.get<IDataType>({
    url: LoginAPI.LoginUserInfo + id,
    showLoading: false
  })
}
export function requestUserMenusByRoleId(id: number) {
  return ycRequest.get<IDataType>({
    url: LoginAPI.UserMenus + id + '/menu',
    showLoading: false
  })
}

```



### vue组件的TS类型

![image-20220722145530439](https://s2.loli.net/2022/07/22/K4FA6Wr7UxBOJ1H.png)

```vue
    // 传入LoginAccount的TS类型
    const accountRef = ref<InstanceType<typeof LoginAccount>>()

    accountRef.value?.logionAction()
```

组件相当于一个类，InstanceType帮助我们拿到.vue组件的类型









### **父元素双向绑定子元素value**

第一种：reactive 修改props

> 父元素

```vue
<HyForm v-bind="searchFormConfig" :formData="formData"></HyForm>
//向子元素传一个reactive对象

	setup() {
    const formData = reactive({
      id: '',
      name: '',
      password: '',
      sport: '',
      createTime: ''
    })

    return { searchFormConfig, formData }
  }
```

> 子元素

```vue
              <template
                v-if="item.type === 'input' || item.type === 'password'"
              >
                <el-input
                  v-bind="item.otherOptions"
                  :placeholder="item.placeholder"
                  :show-password="item.type === 'password'"
                  v-model="formData[`${item.field}`]"	//v-model绑定formData的field
                />
              </template>

  props: {
    formData: {
      type: Object,
      required: true
    },
	}
```

第二种：*v-moeld*

> 父

```vue
<HyForm v-bind="searchFormConfig" v-moeld="formData"></HyForm>

  setup() {
    const formData = reactive({
      id: '',
      name: '',
      password: '',
      sport: '',
      createTime: ''
    })

    return { searchFormConfig, formData }
  }
```

> 子

```vue

              <template
                v-if="item.type === 'input' || item.type === 'password'"
              >
                <el-input
                  v-bind="item.otherOptions"
                  :placeholder="item.placeholder"
                  :show-password="item.type === 'password'"
                  v-model="formData[`${item.field}`]"	//v-model绑定formData的field
                />
              </template>


  props: {
    moduleValue: {
      type: Object,
      required: true
    },
}

  emits: ['update:modelValue'],
  setup(props, { emit }) {
    const formData = computed({
      get: () => props.moduleValue,
      set: (newValue) => {
        emit('update:modelValue', newValue)
      }
    })

    return { formData }
  }
```

和第一种方法本质一样，当input的值改变时set也不会响应

第三种：

```vue
 <HyForm v-bind="searchFormConfig" v-model="formData"></HyForm>

setup() {
    const formData = ref({
      id: '',
      name: '',
      password: '',
      sport: '',
      createTime: ''
    })

    return { searchFormConfig, formData }
  }
```

```vue
              <template
                v-if="item.type === 'input' || item.type === 'password'"
              >
                <el-input
                  v-bind="item.otherOptions"
                  :placeholder="item.placeholder"
                  :show-password="item.type === 'password'"
                  v-model="formData[`${item.field}`]"
                />
              </template>

emits: ['update:modelValue'],
  setup(props, { emit }) {
    // 把原来的数据拷贝一份赋值
    const formData = ref({ ...props.moduleValue })

		// 监听改变并且传回新值
    watch(
      formData,
      (newValue) => {
        emit('update:modelValue', newValue)
      },
      {
        deep: true
      }
    )

    return { formData }
  }
```









### **跨组件插槽的实现**

![image-20220804000520327](https://s2.loli.net/2022/08/04/PpsTqZ1mf5IUXyn.png)

中间层做一个动态插槽，将props.contentConfig.propList里的(排除常用，已经写死了的插槽后)所有插槽作为动态插槽



### **目前页面架构**

![image-20220723140747882](https://s2.loli.net/2022/07/23/QS9t5siBFg2mXUE.png)

![image-20220806165456896](https://s2.loli.net/2022/08/07/Gse2w7yS35NDVbx.png)

### **Echart的封装结构**

![image-20220807171458475](https://s2.loli.net/2022/08/07/DvBitzQM2rxmgCp.png)









## OneList



### 前端缓存和竞态取消

**什么是竞态问题**

> **竞态问题**，又叫**竞态条件**（race condition），它旨在描述一个系统或者进程的输出依赖于不受控制的事件出现顺序或者出现时机。
>
> 此词源自于两个信号试着彼此竞争，来影响谁先输出。

简单来说，竞态问题出现的原因是无法保证异步操作的完成会按照他们开始时同样的顺序。举个🌰：

- 有一个分页列表，快速地切换第二页，第三页；
- 先后请求 data2 与 data3，分页器显示当前在第三页，并且进入 loading；
- 但由于网络的不确定性，先发出的请求不一定先响应，所以有可能 data3 比 data2 先返回；
- 在 data2 最终返回后，分页器指示当前在第三页，但展示的是第二页的数据。

这就是竞态条件，在前端开发中，常见于搜索，分页，选项卡等切换的场景。

那么如何解决竞态问题呢？在以上这些场景中，我们很容易想到：

**当发出新的请求时，取消掉上次请求即可。**



**axios 取消请求**

axios 是一个 HTTP 请求库，本质是对原生 XMLHttpRequest 的封装后基于 promise 的实现版本，因此 axios 请求也可以被取消。

可以利用 axios 的 CancelToken API 取消请求。

```javascript
const source = axios.CancelToken.source();

axios.get('/xxx', {
  cancelToken: source.token
}).then(function (response) {
  // ...
});

source.cancel() // 取消请求
复制代码
```

在 cancel 时，axios 会在内部调用 promise.reject() 与 xhr.abort()。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8ac9450b1d15475abf70977f7bb17c3c~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

所以我们在处理请求错误时，需要判断 error 是否是 cancel 导致的，避免与常规错误一起处理。

```php
axios.get('/xxx', {
  cancelToken: source.token
}).catch(function(err) { 
  if (axios.isCancel(err)) {
    console.log('Request canceled', err.message);
  } else {
    // 处理错误
  }
});
复制代码
```

但 cancelToken 从 `v0.22.0` 开始已被 axios 弃用。原因是基于实现该 API 的提案 [cancelable promises proposal](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Ftc39%2Fproposal-cancelable-promises) 已被撤销。

从 `v0.22.0` 开始，axios 支持以 fetch API 方式的 AbortController 取消请求

```javascript
const controller = new AbortController();

axios.get('/xxx', {
  signal: controller.signal
}).then(function(response) {
   //...
});

controller.abort() // 取消请求
复制代码
```

同样，在处理请求错误时，也需要判断 error 是否来自 cancel。

```js
import axios from 'axios'
import store from '@/store'
// 引入过期时间
import { EXPIRE_TIME } from '@/constants'
// 引入过期后的hook方法
import { handleLogout } from '@/hooks/handleLogout'
const service = axios.create({
  baseURL: import.meta.env.VITE_BASE_API,
  timeout: 5000
})
//前端缓存
let cache = {}
//取消重复请求
let pending = []

// 利用axios的cancelToken来取消请求
const CancelToken = axios.CancelToken
let cancel = null

/**
 * ? 请求拦截器
 */
service.interceptors.request.use((config) => {
  const requestStr = config.url + '&' + config.method
  console.log('cache', cache)
  console.log('pending', pending)
  //* 携带token
  if (store.getters.token) {
    config.headers.token = store.getters.token
  }
  //? 取消请求
  //* 判断是否存在未完成的相同请求 如果存在就取消之前的
  pending = pending.filter((item) => {
    if (item.request === requestStr) {
      console.log('service:取消前一次未完成请求请求')
      item.cancel()
    }
    return item.request !== requestStr
  })

  //* 携带 CancelToken ,加入pending
  config.cancelToken = new CancelToken(function executor(c) {
    cancel = c
    pending.push({ request: requestStr, cancel: c })
  })

  //* 判断数据是否存在以及过期
  // 在缓存池获取缓存数据
  let data = cache[config.url]
  // 获取当前时间戳
  let expire_time = getExpireTime()
  // 判断缓存池中是否存在已有数据 存在的话 再判断是否过期
  // 未过期 cancel取消当前的请求 并将内容返回到拦截器的err中
  if (data && expire_time - data.expire < EXPIRE_TIME) {
    console.log('service:从缓存池中获取数据')
    //需要从pending移出此次请求
    removePending(config)
    cancel(data)
  }

  return config // 必须返回配置
})
/**
 *? 响应拦截器
 */
service.interceptors.response.use(
  (response) => {
    //* 已经完成的请求从pending中移除
    removePending(response.config)
    //*缓存data
    // 只缓存get请求
    if (response.config.method === 'get') {
      // 缓存数据
      let data = {
        expire: getExpireTime(), //当前时间戳
        data: response.data //数据
      }
      cache[`${response.config.url}`] = data
    }
    return response.data
  },
  (err) => {
    // 请求拦截器中的cancel会将内容发送到error中
    // CanceledError {message: {…}, name: 'CanceledError', code: 'ERR_CANCELED'}
    // 通过axios.isCancel()来判断是否返回有数据
    if (axios.isCancel(err)) {
      return Promise.resolve({ ...err.message.data })
    }
    // 处理token超时
    handleLogout(err)
    return Promise.reject(err)
  }
)

//已经完成的请求从pending中移除
const removePending = (config) => {
  pending = pending.filter((item) => {
    return item.request !== config.url + '&' + config.method
  })
}
// 获取当前时间
function getExpireTime() {
  return new Date().getTime()
}
export default service

```





### 自动加载自定义公共组件

以message组件为例

> ./message/index.vue

```vue
<template>
  <transition name="down">
    <div
      v-show="isVisible"
      class="min-w-[420px] fixed top-[20px] left-[50%] translate-x-[-50%] z-50 flex items-center px-3 py-1.5 rounded-sm border cursor-pointer"
      :class="styles[type].containerClass"
    >
      <m-svg-icon
        :name="styles[type].icon"
        :fill-class="styles[type].fillClass"
        class="w-3 h-3 mr-1.5"
      ></m-svg-icon>
      <span class="text-sm" :class="styles[type].textClass">{{ content }}</span>
    </div>
  </transition>
</template>
<script>
const SUCCESS = 'success'
const WARN = 'warn'
const ERROR = 'error'
const typeEnum = [SUCCESS, WARN, ERROR]
</script>
<script setup>
import mSvgIcon from '../svg-icon/index.vue'
import { onMounted, ref } from 'vue'
const props = defineProps({
  //msg消息类型
  type: {
    type: String,
    required: true,
    validator(val) {
      const res = typeEnum.includes(val)
      if (!res) {
        throw new Error(`type必须为${typeEnum}中的一项`)
      }
      return res
    }
  },
  //描述内容
  content: {
    type: String,
    required: true
  },
  //展示时长
  duration: {
    type: Number
  },
  //关闭回调
  destory: {
    type: Function
  }
})
// 样式表数据
const styles = {
  // 警告
  warn: {
    icon: 'warn',
    fillClass: 'fill-warn-300',
    textClass: 'text-warn-300',
    containerClass:
      'bg-warn-100 border-warn-200  hover:shadow-lg hover:shadow-warn-100'
  },
  // 错误
  error: {
    icon: 'error',
    fillClass: 'fill-error-300',
    textClass: 'text-error-300',
    containerClass:
      'bg-error-100 border-error-200  hover:shadow-lg hover:shadow-error-100'
  },
  // 成功
  success: {
    icon: 'success',
    fillClass: 'fill-success-300',
    textClass: 'text-success-300',
    containerClass:
      'bg-success-100 border-success-200  hover:shadow-lg hover:shadow-success-100'
  }
}
//isVisible控制展示
const isVisible = ref(true)
//关闭动画 执行时间
const animDuration = '0.5s'
/**
 * 保证动画展示,需要在mounted之后进行展示
 */
onMounted(() => {
  isVisible.value = true
  setTimeout(() => {
    isVisible.value = false
    setTimeout(() => {
      props.destory && props.destory()
    }, parseInt(animDuration.replace('0.', '').replace('s', '') * 100))
  }, props.duration)
})
</script>

<style lang="scss" scoped>
.down-enter-active,
.down-leave-active {
  transition: all v-bind(animDuration);
}

.down-enter-from,
.down-leave-to {
  opacity: 0;
  transform: translate3d(-50%, -100px, 0);
}
</style>
```



> ./message/index.js

```js
import { h, render } from 'vue'
import messageCpn from './index.vue'
/**
 *
 * @param {*} type success/error/warn
 * @param {*} content 显示内容
 * @param {*} duration 显示时间 (ms)
 */
export const message = (type, content, duration = 3000) => {
  /**
   * 动画结束时的回调
   */
  const onDestory = () => {
    //3.删除vnode
    render(null, document.body)
  }
  return new Promise((resolve, reject) => {
    //1.生成vnode
    const vnode = h(messageCpn, {
      type,
      content,
      duration,
      destory: onDestory
    })
    //2.render渲染
    render(vnode, document.body)
    //3.删除render
  })
}
```



> ./index.js

**lib通用组件项目出口**

```js
import { defineAsyncComponent } from 'vue'

export default {
  //?vite通用组件自动化注册
  //*vite的glob导入功能->在系统中导入多个模块
  //*defineAsyncComponent按需加载的异步组件
  install(app) {
    //1.遍历当前目录下所有文件夹中的index.vue
    const components = import.meta.glob('./*/index.vue')

    //2.遍历获取到的组件模块
    for (const [fullPath, fn] of Object.entries(components)) {
      // 拼接
      const componentName = 'm-' + fullPath.replace('./', '').split('/')[0]
      //3.使用app.component进行注册
      app.component(componentName, defineAsyncComponent(fn))
    }
  }
}

```

