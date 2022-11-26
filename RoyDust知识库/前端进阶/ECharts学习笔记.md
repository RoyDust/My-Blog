# ECharts 学习笔记

## 一、ECharts基本使用

### 01-ECharts-介绍

常见的数据可视化库：

- D3.js   目前 Web 端评价最高的 Javascript 可视化工具库(入手难)  
- ECharts.js   百度出品的一个开源 Javascript 数据可视化库   
- Highcharts.js  国外的前端数据可视化库，非商用免费，被许多国外大公司所使用  
- AntV  蚂蚁金服全新一代数据可视化解决方案  等等
- Highcharts 和 Echarts 就像是 Office 和 WPS 的关系

> ECharts，一个使用 JavaScript 实现的开源可视化库，可以流畅的运行在 PC 和移动设备上，兼容当前绝大部分浏览器（IE8/9/10/11，Chrome，Firefox，Safari等），底层依赖矢量图形库 [ZRender](https://github.com/ecomfe/zrender)，提供直观，交互丰富，可高度个性化定制的数据可视化图表。

大白话：

- 是一个JS插件
- 性能好可流畅运行PC与移动设备
- 兼容主流浏览器
- 提供很多常用图表，且可**定制**。
  - [折线图](https://www.echartsjs.com/zh/option.html#series-line)、[柱状图](https://www.echartsjs.com/zh/option.html#series-bar)、[散点图](https://www.echartsjs.com/zh/option.html#series-scatter)、[饼图](https://www.echartsjs.com/zh/option.html#series-pie)、[K线图](https://www.echartsjs.com/zh/option.html#series-candlestick)

官网地址：<https://www.echartsjs.com/zh/index.html>

### 02-Echarts-体验

![image-20210916221539514](https://i.loli.net/2021/09/16/WKuTcfbZa5ijlX1.png)

官方教程：[五分钟上手ECharts](https://www.echartsjs.com/zh/tutorial.html#5 分钟上手 ECharts)

- 下载echarts  https://github.com/apache/incubator-echarts/tree/4.5.0  

使用步骤：

1. 引入echarts 插件文件到html页面中
2. 准备一个具备大小的DOM容器

```html
<div id="main" style="width: 600px;height:400px;"></div>
```

3.  初始化echarts实例对象

```js
var myChart = echarts.init(document.getElementById('main'));
```

4. 指定配置项和数据(option)

```js
    var option = {
      xAxis: {
        type: 'category',
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
      },
      yAxis: {
        type: 'value'
      },
      series: [{
        data: [820, 932, 901, 934, 1290, 1330, 1320],
        type: 'line'
      }]
    };
```

5. 将配置项设置给echarts实例对象

```js
myChart.setOption(option);
```

### 03-Echarts-基础配置

通用配置

- title 标题组件

  - 文字样式

    textStyle

  - 标题边框.
    borderWidth、borderColor、borderRadius

  - 标题位置
    left、top、right、bottom

- tooltip:提示框组件,用于配置鼠标滑过或点击图表时的显示框

  - 触发类型: trigger

    item（柱的内部）、axis（在坐标轴上）

  - 触发时机: triggerOn

    mouseover（划过）、click（点击）

  - 格式化: formatter

    字符串模板、回调函数

- toolbox: ECharts提供的工具栏

  - feature 显示工具栏按钮

    saveAslmage 导出图片

    dataView 数据视图

    restore 重置

    dataZoom 数据区域缩放

    magicType 动态类型切换

- legend:图例,用于筛选系列，需要和series配合使用
  - legend中的data是-个数组
  - legend中的data的值需要和series数组中谋组数据的name值一致
  - series里面有了name 值则legend 里面的data可以删掉

- grid：直角坐标系内绘图网格 x轴和y轴就是在grid的基础上进行绘制的
  - 显示grid
    show
  - grid的边框
    borderWidth、borderColor
  - grid的位置和大小
    left、top、right、bottom、width、height

- axis：直角坐标系 grid 中的轴
  - 坐标轴类型type
    value:数值轴,自动会从目标数据中读取数据.
    category:类目轴,该类型必须通过data设置类目数据
  - 显示位置position
    xAxis:可取值为top或者bottom
    yAxis:可取值为left或者right

- dataZoom用于区域缩放,对数据范围过滤, x轴和y轴都可以拥有，它是一个数组,意味着可以配置多个区域缩放器
  - 类型type
    slider:滑块
    inside:内置,依靠鼠标滚轮或者双指缩放
  - 指明产生作用的轴
    xAxisIndex:设置缩放组件控制的是哪个x轴,一般写0即可
    yAxisIndex:设置缩放组件控制的是哪个y轴,一般写0即可
  - 指明初始状态的缩放情况
    start:数据窗口范围的起始百分比
    end:数据窗口范围的结束百分比



这是要求同学们知道以下配置每个模块的主要作用干什么的就可以了

> 需要了解的主要配置：`series` `xAxis` `yAxis` `grid` `tooltip` `title` `legend` `color` 

- series

  - 系列列表。每个系列通过 `type` 决定自己的图表类型
  - 大白话：图标数据，指定什么类型的图标，可以多个图表重叠。

- xAxis：直角坐标系 grid 中的 x 轴

  - boundaryGap: 坐标轴两边留白策略 true，这时候刻度只是作为分隔线，标签和数据点都会在两个刻度之间的带(band)中间。

- yAxis：直角坐标系 grid 中的 y 轴

- grid：直角坐标系内绘图网格

- title：标题组件

- tooltip：提示框组件

- legend：图例组件

- color：调色盘颜色列表

  数据堆叠，同个类目轴上系列配置相同的`stack`值后 后一个系列的值会在前一个系列的值上相加。

~~~javascript
    var option = {
      // 设置标题
      title: {
        text: '折线图堆叠'
      },
      // color设置颜色
      color: ['pink', 'yellow', 'skybule', 'red'],
      // 图表的提示框组件
      tooltip: {
        // 触发方式
        trigger: 'axis'
      },
      // 图例组件
      legend: {
        // series里面有了name 值则legend 里面的data可以删掉
        data: ['邮件营销', '联盟广告', '视频广告', '直接访问', '搜索引擎']
      },
      // 网格配置 grid可以控制线形图 柱状图  图表大小
      grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        // 刻度标签
        containLabel: true
      },
      // 工具箱组件 可以另存为图片等
      toolbox: {
        feature: {
          saveAsImage: {}
        }
      },
      // x轴信息
      xAxis: {
        type: 'category',
        // 是否让我们的坐标轴和线条有缝隙
        boundaryGap: false,
        data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
      },
      yAxis: {
        type: 'value'
      },
      // 系列图表配置
      series: [{
          name: '邮件营销',
          type: 'line',
          // 数据堆叠  同个类目轴上系列配置相同的stack值后后个系列的值会在前一 个系列的值上相加。
          stack: '总量',
          data: [120, 132, 101, 134, 90, 230, 210]
        },
        {
          name: '联盟广告',
          type: 'line',
          stack: '总量',
          data: [220, 182, 191, 234, 290, 330, 310]
        },
        {
          name: '视频广告',
          type: 'line',
          stack: '总量',
          data: [150, 232, 201, 154, 190, 330, 410]
        },
        {
          name: '直接访问',
          type: 'line',
          stack: '总量',
          data: [320, 332, 301, 334, 390, 330, 320]
        },
        {
          name: '搜索引擎',
          type: 'line',
          stack: '总量',
          data: [820, 932, 901, 934, 1290, 1330, 1320]
        }
      ]
    };
~~~

### 04- 柱状图图表（两大步骤）

- 官网找到类似实例， 适当分析，并且引入到HTML页面中
- 根据需求定制图表

1. 引入到html页面中

~~~javascript
// 柱状图1模块
(function () {
  // 实例化对象  
  let myChart = echarts.init(document.querySelector(".bar .chart"));
  // 指定配置和数据 
  let option = {
    color: ["#3398DB"],
    tooltip: {
      trigger: "axis",
      axisPointer: {
        // 坐标轴指示器，坐标轴触发有效     
        type: "shadow"
        // 默认为直线，可选为：'line' | 'shadow'   
      }
    },
    grid: {
      left: "3%",
      right: "4%",
      bottom: "3%",
      containLabel: true
    },
    xAxis: [{
      type: "category",
      data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
      axisTick: {
        alignWithLabel: true
      }
    }],
    yAxis: [{
      type: "value"
    }],
    series: [{
      name: "直接访问",
      type: "bar",
      barWidth: "60%",
      data: [10, 52, 200, 334, 390, 330, 220]
    }]
  };
  // 把配置给实例对象
  myChart.setOption(option);
})();
~~~

2. 根据需求定制

   - 修改图表柱形颜色  #2f89cf


   - 修改图表大小  top 为 10px   bottom 为  4%    grid决定我们的柱状图的大小

   ~~~JavaScript
color: ["#2f89cf"],grid: {  left: "0%",  top: "10px",  right: "0%",  bottom: "4%",  containLabel: true},
   ~~~

   - X轴相关设置  xAxis
     - 文本颜色设置为   rgba(255,255,255,.6)   字体大小为 12px
     - X轴线的样式 不显示

   ~~~JavaScript
       xAxis: [{
         type: 'category',
         data: ["旅游行业", "教育培训", "游戏行业", "医疗行业", "电商行业", "社交行业", "金融行业"],
         axisTick: {
           alignWithLabel: true
         },
         // 修改刻度标签 
         axisLabel: {
           color: 'rgba(255,255,255,.6)',
           fontSize: '12'
         },
         // 不显示x坐标轴的样式
         axisLine: {
           show: false
         }
       }],
   ~~~

   - Y 轴相关定制
     - 文本颜色设置为   rgba(255,255,255,.6)   字体大小为 12px
     - Y 轴线条样式 更改为  1像素的  rgba(255,255,255,.1) 边框
     - 分隔线的颜色修饰为  1像素的  rgba(255,255,255,.1)   

   ~~~JavaScript
    yAxis: [{
      type: 'value',
      axisLabel: {
        color: 'rgba(255,255,255,.6)',
        fontSize: 12
      },
      // y轴的线条改为了2像素
      axisLine: {
        lineStyle: {
          color: 'rgba(255,255,255,.1)',
          width: 2
        }
      },
      // y轴分割线的颜色
      splitLine: {
        lineStyle: {
          color: "rgba(255,255,255,.1)"
        }
      }
    }],
   ~~~

   - 修改柱形为圆角以及柱子宽度  series 里面设置

   ~~~JavaScript
    series: [{
      name: '直接访问',
      type: 'bar',
      // 修改柱子宽度
      barWidth: '35%',
      data: [200, 300, 300, 900, 1500, 1200, 600],
      itemStyle: {
        // 修改柱子圆角
        barBorderRadius: 5
      }
    }]
   ~~~

   - 更换对应数据

   ~~~JavaScript
// x轴中更换data数据 
data: [ "旅游行业","教育培训", "游戏行业", "医疗行业", "电商行业", "社交行业", "金融行业" ],
    // series 更换数据 
    data: [200, 300, 300, 900, 1500, 1200, 600]
   ~~~

- 让图表跟随屏幕自适应

~~~javascript
   // 图表跟随屏幕自适应
  window.addEventListener("resize", function () {
    myChart.resize();
  })
~~~

### 05-柱状图2定制

- 官网找到类似实例， 适当分析，并且引入到HTML页面中
- 根据需求定制图表

需求1： 修改图形大小 grid

~~~javascript
 // 图标位置    
grid: {
      top: "10%",
      left: "22%",
      bottom: "10%",
      //containLabel: true
    },
~~~

需求2： 不显示x轴 

~~~javascript
    xAxis: {
      show: false
    },
~~~

需求3： y轴相关定制

- 不显示y轴线和相关刻度

~~~javascript
//不显示y轴线条axisLine: {    show: false        },// 不显示刻度axisTick: {   show: false},
~~~

- y轴文字的颜色设置为白色

~~~javascript
   axisLabel: {         
       color: "#fff" 
   },
~~~

需求4： 修改第一组柱子相关样式（条状）

~~~javascript
name: "条",
    // 柱子之间的距离
    barCategoryGap: 50,
        //柱子的宽度
        barWidth: 10,
            // 柱子设为圆角
            itemStyle: {    normal: {      barBorderRadius: 20,           }},
~~~

- 设置第一组柱子内百分比显示数据

~~~javascript
label: {
          normal: {
            show: true,
            // 图形内显示         
            position: "inside",
            // 文字的显示格式        
            formatter: "{c}%"
          }
        },
~~~

- 设置第一组柱子不同颜色

~~~javascript
// 声明颜色数组
var myColor = ["#1089E7", "#F57474", "#56D0E3", "#F8B448", "#8B78F6"];
// 2. 给 itemStyle  里面的color 属性设置一个 返回值函数  
itemStyle: {          
    normal: {            
        barBorderRadius: 20,              
    // params 传进来的是柱子对象            
    console.log(params);            
    // dataIndex 是当前柱子的索引号   
    return myColor[params.dataIndex];          
    }         
},
~~~

需求5： 修改第二组柱子的相关配置（框状）

~~~javascript
{
        name: "框",
        type: "bar",
        yAxisIndex: 1,
        barCategoryGap: 50,
        barWidth: 15,
        itemStyle: {
          color: "none",
          borderColor: "#00c1de",
          borderWidth: 3,
          barBorderRadius: 15
        },
        data: [100, 100, 100, 100, 100]
      }
~~~

需求6： 给y轴添加第二组数据

~~~javascript
    yAxis: [{
      type: "category",
      // 反转
      inverse: true,
      data: ["HTML5", "CSS3", "javascript", "VUE", "NODE"], // 不显示y轴的线      
      axisLine: {
        show: false
      }, // 不显示刻度      
      axisTick: {
        show: false
      }, // 把刻度标签里面的文字颜色设置为白色      
      axisLabel: {
        color: "#fff"
      }
    }, {
      show: true,
      inverse: true,
      data: [702, 350, 610, 793, 664], // 不显示y轴的线      
      axisLine: {
        show: false
      }, // 不显示刻度      
      axisTick: {
        show: false
      },
      axisLabel: {
        textStyle: {
          fontSize: 12,
          color: "#fff"
        }
      }
    }],
~~~

需求7： 设置两组柱子层叠以及更换数据

~~~javascript
// 给series  第一个对象里面的 添加 
yAxisIndex: 0,
    // 给series  第二个对象里面的 添加 
    yAxisIndex: 1,// series 第一个对象里面的data
        data: [70, 34, 60, 78, 69],// series 第二个对象里面的data
            data: [100, 100, 100, 100, 100],// y轴更换第一个对象更换data数据
                data: ["HTML5", "CSS3", "javascript", "VUE", "NODE"],// y轴更换第二个对象更换data数据
                    data:[702, 350, 610, 793, 664],	
~~~

完整代码：

~~~javascript
// 柱状图2
(function () {
  var myColor = ["#1089E7", "#F57474", "#56D0E3", "#F8B448", "#8B78F6"];
  // 实例化对象
  var myChart = echarts.init(document.querySelector('.bar2 .chart'));
  // 指定配置项和数据
  option = {
    grid: {
      top: "10%",
      left: "22%",
      bottom: "10%",
      // containLabel: true
    },
    xAxis: {
      show: false
    },
    yAxis: [{
      type: "category",
      // 反转
      inverse: true,
      data: ["HTML5", "CSS3", "javascript", "VUE", "NODE"], // 不显示y轴的线      
      axisLine: {
        show: false
      }, // 不显示刻度      
      axisTick: {
        show: false
      }, // 把刻度标签里面的文字颜色设置为白色      
      axisLabel: {
        color: "#fff"
      }
    }, {
      show: true,
      inverse: true,
      data: [702, 350, 610, 793, 664], // 不显示y轴的线      
      axisLine: {
        show: false
      }, // 不显示刻度      
      axisTick: {
        show: false
      },
      axisLabel: {
        textStyle: {
          fontSize: 12,
          color: "#fff"
        }
      }
    }],
    series: [{
        name: '条',
        type: 'bar',
        data: [70, 34, 60, 78, 69],
        yAxisIndex: 0,
        // 修改第一组柱子的圆角
        itemStyle: {
          barBorderRadius: 20,
          // 此时的color可以修改柱子颜色
          color: function (params) {
            // params传进来的是柱子对象
            // dataIndex是当前柱子的索引号
            return myColor[params.dataIndex]
          }
        },
        // 柱子之间的距离
        barCategoryGap: 50,
        //柱子的宽度
        barWidth: 10,
        // 图形上的文本标签
        label: {
          normal: {
            show: true,
            // 图形内显示         
            position: "inside",
            // 文字的显示格式        
            formatter: "{c}%"
          }
        },
      },
      {
        name: "框",
        type: "bar",
        yAxisIndex: 1,
        barCategoryGap: 50,
        barWidth: 15,
        itemStyle: {
          color: "none",
          borderColor: "#00c1de",
          borderWidth: 3,
          barBorderRadius: 15
        },
        data: [100, 100, 100, 100, 100]
      }
    ]
  };
  // 把配置给实例对象
  myChart.setOption(option);
  // 图表跟随屏幕自适应
  window.addEventListener("resize", function () {
    myChart.resize();
  })
})();
~~~

### 06-折线图1 人员变化模块制作

- 官网找到类似实例， 适当分析，并且引入到HTML页面中
- 根据需求定制图表

需求1： 修改折线图大小，显示边框设置颜色：#012f4a，并且显示刻度标签。

```js
// 设置网格样式    
    grid: {
      top: '20%',
      left: '3%',
      right: '4%',
      bottom: '3%',
      show: true,
      // 显示边框     
      borderColor: '#012f4a',
      // 边框颜色     
      containLabel: true
      // 包含刻度文字在内  
    },
```

需求2： 修改图例组件中的文字颜色 #4c9bfd， 距离右侧 right 为 10%

```javascript
    legend: {
      // 修改图例组件 文字颜色
      textStyle: {
        color: "#4c9bfd"
      },
      // 这个10%必须加引号
      right: "10%"
    },
```

需求3： x轴相关配置

- 刻度去除
- x轴刻度标签字体颜色：#4c9bfd
- 剔除x坐标轴线颜色（将来使用Y轴分割线)
- 轴两端是不需要内间距 boundaryGap

```javascript
xAxis: {
      type: 'category',
      data: ["周一", "周二"],
      axisTick: {
        show: false // 去除刻度线 
      },
      axisLabel: {
        color: '#4c9bfd' // 文本颜色
      },
      axisLine: {
        show: false // 去除轴线       
      },
      boundaryGap: false // 去除轴内间距 
    },
```

需求4： y轴的定制

- 刻度去除
- 字体颜色：#4c9bfd
- 分割线颜色：#012f4a

```javascript
    yAxis: {
      type: 'value',
      axisTick: {
        show: false // 去除刻度 
      },
      axisLabel: {
        color: '#4c9bfd' // 文字颜色   
      },
      splitLine: {
        lineStyle: {
          color: '#012f4a' // 分割线颜色      
        }
      }
    },
```

需求5： 两条线形图定制

- 颜色分别：#00f2f1  #ed3f35
- 把折线修饰为圆滑 series 数据中添加 smooth 为 true

```js
color: ['#00f2f1', '#ed3f35'], series: [{
  name: '新增粉丝',
  data: [820, 932, 901, 934, 1290, 1330, 1320],
  type: 'line', // 折线修饰为圆滑      
  smooth: true,
}, {
  name: '新增游客',
  data: [100, 331, 200, 123, 233, 543, 400],
  type: 'line',
  smooth: true,
}]
```

需求6： 配置数据

```js
// x轴的文字
xAxis: {  type: 'category',  data: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
```

```js
// 图标数据   
series: [{
  name: '新增粉丝',
  data: [24, 40, 101, 134, 90, 230, 210, 230, 120, 230, 210, 120],
  type: 'line',
  smooth: true
}, {
  name: '新增游客',
  data: [40, 64, 191, 324, 290, 330, 310, 213, 180, 200, 180, 79],
  type: 'line',
  smooth: true
}
}]
```

需求7： 新增需求  点击 2020年   2021年 数据发生变化

以下是后台送过来数据（ajax请求过来的）

~~~javascript
var yearData = [{
    year: '2020',
    // 年份        
    data: [
      // 两个数组是因为有两条线
      [24, 40, 101, 134, 90, 230, 210, 230, 120, 230, 210, 120],
      [40, 64, 191, 324, 290, 330, 310, 213, 180, 200, 180, 79]
    ]
  }, {
    year: '2021',
    // 年份        
    data: [
      // 两个数组是因为有两条线     
      [123, 175, 112, 197, 121, 67, 98, 21, 43, 64, 76, 38],
      [143, 131, 165, 123, 178, 21, 82, 64, 43, 60, 19, 34]
    ]
  }];
~~~

- tab栏切换事件
- 点击2020按钮   需要把 series 第一个对象里面的data  换成  2020年对象里面data[0] 
- 点击2020按钮   需要把 series 第二个对象里面的data  换成  2020年对象里面data[1] 
- 2021 按钮同样道理

完整代码：

~~~javascript
// 折线图1
(function () {
  var yearData = [{
    year: '2020',
    // 年份        
    data: [
      // 两个数组是因为有两条线
      [24, 40, 101, 134, 90, 230, 210, 230, 120, 230, 210, 120],
      [40, 64, 191, 324, 290, 330, 310, 213, 180, 200, 180, 79]
    ]
  }, {
    year: '2021',
    // 年份        
    data: [
      // 两个数组是因为有两条线     
      [123, 175, 112, 197, 121, 67, 98, 21, 43, 64, 76, 38],
      [143, 131, 165, 123, 178, 21, 82, 64, 43, 60, 19, 34]
    ]
  }];
  // 实例化对象
  var myChart = echarts.init(document.querySelector('.line .chart'));
  // 指定配置项和数据
  var option = {
    // 通过color修改两条线的颜色
    color: ['#00f2f1', '#ed3f35'],
    tooltip: {
      trigger: 'axis'
    },
    legend: {
      // 修改图例组件 文字颜色
      textStyle: {
        color: "#4c9bfd"
      },
      // 这个10%必须加引号
      right: "10%"
    },
    // 设置网格样式    
    grid: {
      top: '20%',
      left: '3%',
      right: '4%',
      bottom: '3%',
      show: true, // 显示边框     
      borderColor: '#012f4a', // 边框颜色     
      containLabel: true // 包含刻度文字在内  
    },
    xAxis: {
      type: 'category',
      data: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
      axisTick: {
        show: false // 去除刻度线 
      },
      axisLabel: {
        color: '#4c9bfd' // 文本颜色
      },
      axisLine: {
        show: false // 去除轴线       
      },
      boundaryGap: false // 去除轴内间距 
    },
    yAxis: {
      type: 'value',
      axisTick: {
        show: false // 去除刻度 
      },
      axisLabel: {
        color: '#4c9bfd' // 文字颜色   
      },
      splitLine: {
        lineStyle: {
          color: '#012f4a' // 分割线颜色      
        }
      }
    },
    series: [{
      name: '新增粉丝',
      data: yearData[0].data[0],
      type: 'line',
      smooth: true
    }, {
      name: '新增游客',
      data: yearData[0].data[1],
      type: 'line',
      smooth: true
    }]
  };
  // 把配置项给实例对象
  myChart.setOption(option);
  // 图表跟随屏幕自适应
  window.addEventListener("resize", function () {
    myChart.resize();
  })

  // 点击切换效果
  $('.line h2').on('click', 'a', function () {
    // console.log($(this).index());
    // 点击a后根据当前a索引号 找到对应的 yearData的相关对象
    // console.log(yearData[$(this).index()]);
    var obj = yearData[$(this).index()];
    option.series[0].data = obj.data[0];
    option.series[1].data = obj.data[1];
    // 重新渲染
    myChart.setOption(option);
  });
})();
~~~

### 07-折线图2 播放量模块制作

- 官网找到类似实例， 适当分析，并且引入到HTML页面中
- 根据需求定制图表

需求1： 更换图例组件文字颜色 rgba(255,255,255,.5)  文字大小为12

~~~javascript
    legend: {
      data: ['邮件营销', '联盟广告', '视频广告', '直接访问', '搜索引擎'],
      textStyle: {
        color: "rgba(255,255,255,.5)",
        fontSize: "12"
      }
    },
~~~

需求2： 修改图表大小

~~~javascript
grid: {
      left: "10",
      top: "30",
      right: "10",
      bottom: "10",
      containLabel: true
    },
~~~

需求3： 修改x轴相关配置

- 修改文本颜色为rgba(255,255,255,.6)  文字大小为 12
- x轴线的颜色为   rgba(255,255,255,.2)

~~~javascript
      axisLabel: {
        textStyle: {
          color: "rgba(255,255,255,.6)",
          fontSize: 12
        }
      }, // x轴线的颜色为  rgba(255, 255, 255, .2) 
          axisLine: {
        lineStyle: {
          color: "rgba(255,255,255,.2)"
        }
      },
~~~

需求4： 修改y轴的相关配置

~~~javascript
      axisTick: {
        show: false
      },
      axisLine: {
        lineStyle: {
          color: "rgba(255,255,255,.1)"
        }
      },
      axisLabel: {
        textStyle: {
          color: "rgba(255,255,255,.6)",
          fontSize: 12
        }
      }, // 修改分割线的颜色        
      splitLine: {
        lineStyle: {
          color: "rgba(255,255,255,.1)"
        }
      }
~~~

需求5： 修改两个线模块配置(注意在series 里面定制)

~~~javascript
    series: [{
        name: '邮件营销',
        type: 'line',
        smooth: true,
        // 单独修改当前线条的样式
        lineStyle: {
          color: "#0184d5",
          width: 2
        },
        // 填充区域     
        areaStyle: {
          // 渐变色 
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
            offset: 0,
            color: "rgba(1, 132, 213, 0.4)" // 渐变色的起始颜色           
          }, {
            offset: 0.8,
            color: "rgba(1, 132, 213, 0.1)" // 渐变线的结束颜色              
          }], false),
          shadowColor: "rgba(0, 0, 0, 0.1)"
        },
        // 设置拐点 小圆点       
        symbol: "circle",
        // 拐点大小        
        symbolSize: 8,
        // 设置拐点颜色以及边框   
        itemStyle: {
          color: "#0184d5",
          borderColor: "rgba(221, 220, 107, .1)",
          borderWidth: 12
        },
        // 开始不显示拐点， 鼠标经过显示  
        showSymbol: false,
        emphasis: {
          focus: 'series'
        },
        data: [30, 40, 30, 40, 30, 40, 30, 60, 20, 40, 30, 40, 30, 40, 30, 40, 30, 60, 20, 40, 30, 40, 30, 40, 30, 40, 20, 60, 50, 40],
      },
      {
        name: "转发量",
        type: "line",
        smooth: true,
        lineStyle: {
          normal: {
            color: "#00d887",
            width: 2
          }
        },
        areaStyle: {
          normal: {
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
              offset: 0,
              color: "rgba(0, 216, 135, 0.4)"
            }, {
              offset: 0.8,
              color: "rgba(0, 216, 135, 0.1)"
            }], false),
            shadowColor: "rgba(0, 0, 0, 0.1)"
          }
        }, // 设置拐点 小圆点        
        symbol: "circle",
        // 拐点大小       
        symbolSize: 5,
        // 设置拐点颜色以及边框  
        itemStyle: {
          color: "#00d887",
          borderColor: "rgba(221, 220, 107, .1)",
          borderWidth: 12
        },
        // 开始不显示拐点， 鼠标经过显示  
        showSymbol: false,
        data: [130, 10, 20, 40, 30, 40, 80, 60, 20, 40, 90, 40, 20, 140, 30, 40, 130, 20, 20, 40, 80, 70, 30, 40, 30, 120, 20, 99, 50, 20],
      },
    ]
~~~

需求6： 更换数据

~~~javascript
// x轴更换数据
data: [ "01","02","03","04","05","06","07","08","09","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","26","28","29","30"],
    // series  第一个对象data数据 
    data: [ 30, 40, 30, 40,30, 40, 30,60,20, 40, 30, 40, 30, 40,30, 40, 30,60,20, 40, 30, 40, 30, 40,30, 40, 20,60,50, 40],
        // series  第二个对象data数据 
        data: [ 130, 10, 20, 40,30, 40, 80,60,20, 40, 90, 40,20, 140,30, 40, 130,20,20, 40, 80, 70, 30, 40,30, 120, 20,99,50, 20],
~~~



### 08-饼形图 1年龄分布模块制作

- 官网找到类似实例， 适当分析，并且引入到HTML页面中
- 根据需求定制图表

定制图表需求1： 

- 修改图例组件在底部并且居中显示。 
- 每个小图标的宽度和高度修改为 10px   
- 文字大小为12 颜色  rgba(255,255,255,.5)

~~~javascript
    legend: {
      bottom: "0%",
      // 小图标的宽度和高度  
      itemWidth: 10,
      itemHeight: 10,
      // 修改图例组件的文字为 12px   
      textStyle: {
        color: "rgba(255,255,255,.5)",
        fontSize: "12"
      }
    },
~~~

定制需求2：

- 修改水平居中 垂直居中
- 修改内圆半径和外圆半径为    ["40%", "60%"]   pink老师友情提示，带有直角坐标系的比如折线图柱状图是 grid修改图形大小，而我们饼形图是通过 radius 修改大小

~~~javascript
series: [{
  name: "年龄分布",
  type: "pie",
  // 设置饼形图在容器中的位置        
  center: ["50%", "50%"],
  //  修改内圆半径和外圆半径为  百分比是相对于容器宽度来说的   
  radius: ["40%", "60%"],
  // 不显示标签文字       
  label: {
    show: false
  },
  // 不显示连接线       
  labelLine: {
    show: false
  },
}]
~~~

定制需求3：更换数据

~~~javascript
// legend 中的data  可省略
data: ["0岁以下", "20-29岁", "30-39岁", "40-49岁", "50岁以上"],
  //  series 中的数据
  data: [{
    value: 1,
    name: "0岁以下"
  }, {
    value: 4,
    name: "20-29岁"
  }, {
    value: 2,
    name: "30-39岁"
  }, {
    value: 2,
    name: "40-49岁"
  }, {
    value: 1,
    name: "50岁以上"
  }],
~~~

定制需求4： 更换颜色

~~~javascript
color: [          
    "#065aab",          "#066eab",          "#0682ab",          "#0696ab",          "#06a0ab",       
],
~~~

~~~javascript
 // 4. 让图表跟随屏幕自动的去适应  
window.addEventListener("resize", function() {    myChart.resize();  });
~~~

### 09-饼形图2 地区分布模块制作（南丁格尔玫瑰图）

- 官网找到类似实例， 适当分析，并且引入到HTML页面中
- 根据需求定制图表

第二步：按照需求定制

- 需求1：颜色设置

```js
color: ['#006cff', '#60cda0', '#ed8884', '#ff9f7f', '#0096ff', '#9fe6b8', '#32c5e9', '#1d9dff'],
```

- 需求2：修改饼形图大小 ( series对象)

```javascript
radius: ['10%', '70%'],
```

- 需求3： 把饼形图的显示模式改为 半径模式

```javascript
 roseType: "radius",
```

- 需求4：数据使用更换（series对象 里面 data对象）

```js
{
  value: 20,
  name: '云南'
}, {
  value: 26,
  name: '北京'
}, {
  value: 24,
  name: '山东'
}, {
  value: 25,
  name: '河北'
}, {
  value: 20,
  name: '江苏'
}, {
  value: 25,
  name: '浙江'
}, {
  value: 30,
  name: '四川'
}, {
  value: 42,
  name: '湖北'
}
```

- 需求5：字体略小些  10 px ( series对象里面设置 )

  饼图图形上的文本标签可以控制饼形图的文字的一些样式。   label 对象设置

```javascript
series: [{
  name: "面积模式",
  type: "pie",
  radius: [30, 110],
  center: ["50%", "50%"],
  roseType: "radius", // 文本标签控制饼形图文字的相关样式， 注意它是一个对象        
  label: {
    fontSize: 10
  },
}]
```

- 需求6：防止缩放的时候，引导线过长。引导线略短些   (series对象里面的  labelLine  对象设置  ) 
  - 连接图表 6 px
  - 连接文字 8 px

```js
      // 图形文字标签
      label: {
        fontSize: 10
      },
      // 链接文字和图形的线
      labelLine: {
        show: true,
        // length 链接图形线条长度
        length: 6,
        length2: 8
      },
```

- 需求6：浏览器缩放的时候，图表跟着自动适配。

```javascript
// 监听浏览器缩放，图表对象调用缩放resize函数
window.addEventListener("resize", function() {    myChart.resize();  });
```

### 10-散点图

- ECharts最基本的代码结构:

  引入js文件, DOM容器,初始化对象,设置option

- x轴数据和y轴的数据:二维数组

  数组1:[ [身高1,体重1]，[身高2, 体重2]，[身 高3,体重3]... ]

- 图表类型:

  在series下设置type:scatter

  xAxis和yAxis的type都要设置为value

气泡图效果

- 散点的大小不同
  symbolSize
- 散点的颜色不同
  itemStyle.color
- 涟漪动画效果
  type:effectScatter
  showEffectOn:'emphasis'
  rippleEffect:{}

```js
(function () {
  // 实例化对象
  var myChart = echarts.init(document.querySelector('.bar .chart'));
  // 指定配置项和数据
  //1. ECharts最基本的代码结构
  //2. x轴和y轴数据 二维数组 [ [身高,体重],...   ]
  //3. 将type的值设置为scatter, x轴和y轴的type都是value
  var data = [{
    "gender": "female",
    "height": 161.2,
    "weight": 51.6
  }, {
    "gender": "female",
    "height": 167.5,
    "weight": 59
  }, {
    "gender": "female",
    "height": 159.5,
    "weight": 49.2
  }]
  var axisData = []
  for (var i = 0; i < data.length; i++) {
    // 对原始数据进行处理，全部遍历一遍 
    var height = data[i].height
    var weight = data[i].weight
    var newArr = [height, weight]
    axisData.push(newArr)
  }
  var option = {
    xAxis: {
      type: 'value',
      scale: true //不一定以0为起点
    },
    yAxis: {
      type: 'value',
      scale: true
    },
    series: [{
      type: 'effectScatter', // 指明图表的类型为散点图
      showEffectOn:'emphasis',  //控制鼠标移到才产生涟漪动画
      rippleEffect:{  //涟漪动画范围
        scale:5
      },
      data: axisData,
      symbolSize: function (arg) {
        // symbolSize可以控制散点大小
        var height = arg[0] / 100;
        var weight = arg[1];
        // var bml = 体重kg / (身高m*身高m) 大于28,就代表肥胖
        var bml = weight / (height * height);
        if (bml > 28) {
          return 10
        }
        return 5
      },
      itemStyle: {
        color: function (arg) {
          var height = arg.data[0] / 100;
          var weight = arg.data[1];
          // var bml = 体重kg / (身高m*身高m) 大于28,就代表肥胖
          var bml = weight / (height * height);
          if (bml > 28) {
            return 'red'
          }
          return 'green'
        }
      }
    }]
  };
  // 把配置项给实例对象
  myChart.setOption(option);
  // 图表跟随屏幕自适应
  window.addEventListener("resize", function () {
    myChart.resize();
  })
})();
```

### 11-地图

- 地图图表的两种使用方式

  百度地图API

  矢量地图数据

- 地图的绘制

  加载数据

  将数据注册给echarts全局对象

  配置geo

- 常见效果

  缩放拖动/初始缩 放比例/中心点

  visualMap和地 图的结合

  散点图和地图的结合

- 地图特点

  地图主要 可以帮助我们从宏观的角度快速看出不同地理位置上数据的差异

```js
// 地图
(function () {
  // 实例化对象
  var myChart = echarts.init(document.querySelector('.bar2 .chart'));
  // 指定配置项和数据
  //1. ECharts最 基本的代码结构
  //2.准备中国地图的矢量数据
  //3.使用Ajax获取矢量地图数据
  //4.在Ajax的回调函数中注册地图矢量数据echarts.registerMap('chinaMap',矢量地图数据)
  //5. 配置geo的type为 'map', map为'chinaMap
  var airData = [{
      name: '北京',
      value: 39.92
    },
    {
      name: '天津',
      value: 39.13
    },
    {
      name: '上海',
      value: 31.22
    },
    {
      name: '重庆',
      value: 66
    },
    {
      name: '河北',
      value: 147
    },
    {
      name: '河南',
      value: 113
    },
    {
      name: '云南',
      value: 25.04
    },
    {
      name: '辽宁',
      value: 50
    },
    {
      name: '黑龙江',
      value: 114
    },
    {
      name: '湖南',
      value: 175
    },
    {
      name: '安徽',
      value: 117
    },
    {
      name: '山东',
      value: 92
    },
    {
      name: '新疆',
      value: 84
    },
    {
      name: '江苏',
      value: 67
    },
    {
      name: '浙江',
      value: 84
    },
    {
      name: '江西',
      value: 96
    },
    {
      name: '湖北',
      value: 273
    },
    {
      name: '广西',
      value: 59
    },
    {
      name: '甘肃',
      value: 99
    },
    {
      name: '山西',
      value: 39
    },
    {
      name: '内蒙古',
      value: 58
    },
    {
      name: '陕西',
      value: 61
    },
    {
      name: '吉林',
      value: 51
    },
    {
      name: '福建',
      value: 29
    },
    {
      name: '贵州',
      value: 71
    },
    {
      name: '广东',
      value: 38
    },
    {
      name: '青海',
      value: 57
    },
    {
      name: '西藏',
      value: 24
    },
    {
      name: '四川',
      value: 58
    },
    {
      name: '宁夏',
      value: 52
    },
    {
      name: '海南',
      value: 54
    },
    {
      name: '台湾',
      value: 88
    },
    {
      name: '香港',
      value: 66
    },
    {
      name: '澳门',
      value: 77
    },
    {
      name: '南海诸岛',
      value: 55
    }
  ] //空气质量数据
  var scatterData = [{
    value: [117.283042, 31.86119]
  }] //散点数据
  $.get('json/map/china.json', function (ret) {
    // ret 就是中国的各个省份的矢量地图数据
    // console.log(ret)
    echarts.registerMap('chinaMap', ret)
    var option = {
      geo: {
        type: 'map',
        map: 'chinaMap', // chinaMap需要和registerMap中的第一个参数保持一致
        roam: true, // 设置允许缩放以及拖动的效果
        label: {
          show: true // 展示标签
        },
        zoom: 1, // 设置初始化的缩放比例
        center: [87.617733, 43.792818] // 设置地图中心点的坐标
      },
      //2. 将空气质量的数据设置给series下的对象
      //3. 将series下的数据和geo关联起来
      //4. 配置visualMap
      series: [{
        data: airData,
        geoIndex: 0, // 将空气质量的数据和第0个geo配置关联在一起
        type: 'map'
      }, {
        data: scatterData, //配置散点的坐标数据
        type: 'effectScatter',
        coordinateSystem: 'geo', //指明散点使用的坐标系统 geo的坐标系统
        rippleEffect: {
          scale: 10   //设置涟漪动画缩放
        }
      }],
      visualMap: {
        min: 0,
        max: 300,
        inRange: {
          color: ['white', 'red'] // 控制颜色渐变的范围
        },
        calculable: true // 出现滑块
      }
    }
    myChart.setOption(option);
  })
  // 图表跟随屏幕自适应
  window.addEventListener("resize", function () {
    myChart.resize();
  })
})();
```

### 12-雷达图

- 雷达图的实现步骤

  定义各个维度的最大值

  定义图表的类型

- 雷达图的特点

  雷达图可以用来分析多个维度的数据与标准数据的对比情况

```js
// 雷达图
(function () {
  // 各个维度的最大值
  var dataMax = [{
      name: '易用性',
      max: 100
    },
    {
      name: '功能',
      max: 100
    },
    {
      name: '拍照',
      max: 100
    },
    {
      name: '跑分',
      max: 100
    },
    {
      name: '续航',
      max: 100
    }
  ]
  // 实例化对象
  var myChart = echarts.init(document.querySelector('.line .chart'));
  // 指定配置项和数据
  var option = {
    radar: {
      indicator: dataMax, //配置维度最大值
      shape:'circle'  //配置雷达图最外层的图形 circle polygon
    },
    series: [{
      type: 'radar', //说明此图是雷达图
      label: { //设置标签的样式
        show: true
      },
      areaStyle: {},//将雷达图区域形成阴影的面积
      data: [{
          name: '华为手机1',
          value: [80, 90, 80, 82, 90]
        },
        {
          name: '小米手机1',
          value: [70, 82, 75, 70, 78]
        }
      ]
    }]
  };
  // 把配置项给实例对象
  myChart.setOption(option);
  // 图表跟随屏幕自适应
  window.addEventListener("resize", function () {
    myChart.resize();
  })
})();
```

13-仪表盘图

- 仪表盘的实现步骤
  准备数据
  定义图表的类型
- 仪表盘的特点
  仪表盘可以更直观的表现出某个指标的进度或实际情况

```js
// 折线图2
(function () {
  // 实例化对象
  var myChart = echarts.init(document.querySelector('.line2 .chart'));
  // 指定配置项和数据
  var option = {
    series: [{
      type: 'gauge',
      data: [{
          value: 97,
          itemStyle: { // 指针的样式
            color: 'pink' // 指针的颜色
          }
        }, // 每一个对象就代表一个指针
        {
          value: 85,
          itemStyle: {
            color: 'green'
          }
        }
      ],
      min: 50 // min max 控制仪表盘数值范围
    }]
  };

  // 把配置项给实例对象
  myChart.setOption(option);
  // 图表跟随屏幕自适应
  window.addEventListener("resize", function () {
    myChart.resize();
  })
})();
```

### 小结

![image-20211005221239953](https://i.loli.net/2021/10/05/UtaPcmD24QhFyL7.png)

![image-20211005221541821](https://i.loli.net/2021/10/05/LZHD2raS5vs8FXY.png)

## 二、ECharts高阶用法

### 01-主题

- 内置主题
  ECharts中 默认内置了两套主题:light dark
  在初始化对象方法init中可以指明
  var chart = echarts.init(dom, 'light');
  var chart = echarts.init(dom, 'dark');
- 自定义主题
  1. 在主题编辑器中编辑主题
  2. 下载主题,是一个js文件
  3. 引入主题js文件
  4. 在init方法中使用主题

```js
  <script src="theme/purple.js"></script>

    // 初始化实例对象 echarts.init(dom容器);
    var myChart = echarts.init(document.querySelector('.box'),'purple');
```

####  调色盘

它是一组颜色，图形、系列会自动从其中选择颜色。

- 主题调色盘

- 全局调色盘:

  ```js
  option : {
  color: ['red','green', 'blue', ],
  }
  ```

- 局部调色盘:

  ```js
  series: [{
  type:"bar',
  color: ['red','green', 'blue',],
  }],
  ```

#### 颜色渐变

- 线性渐变:

  ```js
              color: {
                type: 'linear', // 线性渐变
                x: 0,
                y: 0,
                x2: 0,
                y2: 1,
                colorStops:[
                  {
                    offset: 0, color: 'red' // 0%处的颜色为红色
                  },
                  {
                    offset: 1, color: 'blue' // 100%处的颜色为蓝
                  }
                ]
              }
  ```

  

- 径向渐变:

  ```js
              color: {
                type: 'radial', // 径向渐变
                x: 0.5,
                y: 0.5,
                r: 0.5,
                colorStops: [
                  {
                    offset: 0, color: 'red' // 0%处的颜色为红色
                  },
                  {
                    offset: 1, color: 'blue' // 100%处的颜色为蓝
                  }
                ]
              }
  ```

#### 样式

- 直接样式

  itemStyle、textStyle、 lineStyle、 areaStyle、 label

- 高亮样式

  在emphasis中包裹itemStyle、textStyle、 lineStyle、 areaStyle、 label

- 优先级高,会覆盖主题中、调色盘的效果

```js
          data: [{
            value: 11231,
            name: "淘宝",
            itemStyle: { // 控制淘宝这一区域的样式
              color: 'yellow'
            },
            label: {
              color: 'green'
            },
            emphasis: {
              itemStyle: { // 控制淘宝这一区域的样式
                color: 'pink'
              },
              label: {
                color: 'black'
              }
            }
          },
```

### 加载动画

ECharts已经内置好了加载数据的动画,我们只需要在合适的时机显示或者隐藏即可

- 显示加载动画

  ```js
  mCharts.showLoading()
  ```

  

- 隐藏加载动画

  ```js
  mCharts.hideLoading()
  ```

- mCharts.setOption
  所有数据的更新都通过setOption实现
  不用考虑数据到底产生了那些变化
  ECharts会找到两组数据之间的差异然后通过合适的动画去表现数据的变化。

  ```js
      var btnModify = document.querySelector('#modify')
      btnModify.onclick = function () {
        var newYDataArr = [68, 32, 99, 77, 94, 80, 72, 86]
        // setOption 可以设置多次
        // 新的option 和 旧的option
        // 新旧option的关系并不是相互覆盖的关系, 是相互整合的关系
        // 我们在设置新的option的时候, 只需要考虑到变化的部分就可以
        var option = {
          series: [
            {
              data: newYDataArr
            }
          ]
        }
        mCharts.setOption(option)
      }
  ```

  #### 动画配置项

  - 开启动画
    animation: true

  - 动画时长
    animationDuration: 5000

  - 缓动动画
    animationEasing: 'bounceOut'

  - 动画阈值
    animationThreshold: 8

    ```js
          animation: true,  // 控制动画是否开启
          // animationDuration: 7000, // 动画的时长, 它是以毫秒为单位
          animationDuration: function(arg){
            console.log(arg)
            return 2000 * arg
          },
          animationEasing: 'bounceOut', // 缓动动画
          animationThreshold: 7, // 动画元素的阈值
    ```


### 交互API

#### 全局echarts对象

- 全局echarts对象
  全局echarts对象是引入echarts.js文件之后就可以直接使用的
- echartsInstance对象
  eChartsInstance对象是通过echarts.init方法调用之后得到的

#### echarts对象方法

- init方法
  初始化ECharts实例对象
  使用主题
- registerTheme方法
  注册主题
  只有注册过的主题,才能在init方法中使用该主题

- registerMap方法

  - 注册地图数据

    ```js
      $.get('json/map/china.json', function (ret) {
        echarts.registerMap('chinaMap', ret)
      });
    ```

    

  - geo组件使用地图数据

    ```js
          geo: {
            type: 'map',
            map: 'chinaMap', // chinaMap需要和registerMap中的第一个参数保持一致
            roam: true, // 设置允许缩放以及拖动的效果
            label: {
              show: true // 展示标签
            },
            zoom: 1, // 设置初始化的缩放比例
            center: [87.617733, 43.792818] // 设置地图中心点的坐标
          },
    ```

- connect方法

  - 一个页面中可以有多个独立的图表

  - 每一个图表对应一个ECharts实例对象

  - connect可以实现多图关联，传入联动目标为ECharts实例对象，支持数组。
    保存图片的自动拼接
    刷新按钮
    重置按钮
    提示框联动、图例选择、数据范围修改等.....

#### echartsInstance对象方法

- setOption方法

  - 设置或修改图表实例的配置项以及数据
  - 多次调用setOption方法
    合并新的配置和旧的配置
    增量动画

- resize方法

  - 重新计算和绘制图表

  - 一般和window对象的resize事件结合使用

    ```js
    window.onresize = function(){
    myChart.resize(); 
    }
    ```

- on\off方法
  - 绑定或者 解绑事件处理函数
  - 鼠标事件
    常见事件: 'click'、'dblclick'、 'mousedown'. 'mousemove'、'mouseup' 等
    事件参数arg:和事件相关的数据信息
  - ECharts事件
    常见事件: legendselectchanged、'datazoom'、 'pieselectchanged'. 'mapselectchanged'等
    事件参数arg:和事件相关的数据信息

- dispatchAction方法

  - 触发某些行为

  - 使用代码模拟用户 的行为

    ```js
    mCharts.dispatchAction({
        type: 'highlight', //事件类型
        seriesIndex: 0,//图表索引
        datalndex: 1//图表中哪一项高亮
    });
    
    ```

- clear方法
  - 清空当前实例， 会移除实例中所有的组件和图表.
  - 清空之后可以再次setOption
- dispose方法
  - 销毁实例
  - 销毁后实例无法再被使用

```js
    mCharts.setOption(option)
    mCharts.on('click', function (arg) {
      console.log(arg)
      console.log('click...')
    }) // 对事件进行监听

    mCharts.off('click') // 解绑click的事件

    mCharts.on('legendselectchanged', function (arg) {
      console.log(arg)
      console.log('legendselectchanged')
    })

    $('#btn1').click(function () {
      // 模拟用户的行为
      mCharts.dispatchAction({
        type: 'highlight',
        seriesIndex: 0, // 系列的索引
        dataIndex: 1 // 数据的索引
      })
      mCharts.dispatchAction({
        type: 'showTip',
        seriesIndex: 0,
        dataIndex: 2
      })
    })

    $('#btn2').click(function () {
      // 清空图表的实例
      mCharts.clear()
    })

    $('#btn3').click(function () {
      // 重新设置option
      mCharts.setOption(option)
    })

    $('#btn4').click(function () {
      // 销毁mCharts
      mCharts.dispose()
    })
```

## 三、Koa2

特点：

- 支持async\await
- 洋葱模型的中间件

### 上手

- 检查Node的环境
  node -V
- 安装Koa
  npm init -y
  npm install koa
- 创建并编写app.js文件
  1.创建Koa对象
  2.编写响应函数(中间件)
  3.监听端口
- 启动服务器
  node app.js

### 中间件特点

- Koa对象通过use方法加入一个中间件
- 一个中间件就是一个函数
- 中间件的执行顺序符合洋葱模型，
- 内层中间件能否执行取决于外层中间件的next函数是否调用
- 调用next函数得到的是Promise对象

```js
app.use(async (ctx, next) => {
//刚进入中间件想做的事情
await next()
//内层所有中间件结束之后想做的事情
})
```

![image-20211009225510511](https://i.loli.net/2021/10/09/LpxFN4OYDgPiH5E.png)

### 后台项目的目标

1. 计算服务器处理请求的总耗时
2. 在响应头上加上响应内容的mime类型
3. 根据URL读取指定目录下的文件内容

#### 总耗时中间件

1. 第1层中间件
2. 计算执行时间
   进入时记录开始时间
   其他所有中间件执行完后记录结束时间
   两者相减
3. 设置响应头
   X-Response-Time:5ms

```js
// 计算服务器消耗时长的中间件
module.exports = async (ctx, next) => {
  // 记录开始时间
  const start = Date.now();
  // 让内层中间件得到执行
  await next()
  // 记录结束的时间
  const end = Date.now();
  // 设置响应头X-Response-Time
  const duration = end - start;
  // ctx.set 设置响应头
  ctx.set('X-Response-Time', duration + 'ms');
}
```

#### 业务逻辑中间件

1. 第3层 中间件
2. 读取文件内容
   http://127.0.0.1:3000/api/seller
   获取请求的路径,拼接文件路径
   读取该路径对应文件的内容
3. 设置响应体
   ctx.response.body

```js
// 处理业务逻辑的中间件,读取某个json文件的数据
const path = require('path')
const fileUtils = require('../utils/file_utils')
module.exports = async (ctx, next) => {
  // 根据url
  const url = ctx.request.url // /api/seller   ../data/seller.json
  let filePath = url.replace('/api', '') //  /seller
  filePath = '../data' + filePath + '.json' // ../data/seller.json
  filePath = path.join(__dirname, filePath)
  try {
    const ret = await fileUtils.getFileJsonData(filePath)
    ctx.response.body = ret
  } catch (error) {
    const errorMsg = {
      message: '读取文件内容失败, 文件资源不存在',
      status: 404
    }
    ctx.response.body = JSON.stringify(errorMsg)
  }
  console.log(filePath)
  await next()
}
```

#### 允许跨域

1. 实际是通 过Ajax访问服务器

2. 同源策略
   同协议\同域名\同端口
   当前页面的地址和Ajax获取数据的地址

3. 设置响应头

   ```js
   // 设置响应头的中间件
   module.exports = async (ctx, next) => {
     const contentType = 'application/json; charset=utf-8'
     ctx.set('Content-Type', contentType)
     // ctx.response.body = '{"success":true}'
     ctx.set("Access-Control-Allow-Origin", "*")
     ctx.set("Access-Control-Allow-Methods", "OPTIONS, GET, PUT, POST, DELETE")
     await next()
   }
   ```

## 四、Vue结合ECharts

### 1、项目准备

![image-20211010162652827](https://i.loli.net/2021/10/10/ek2GOaCov4NIpPd.png)

### 2、单独图表组件开发

#### 通用代码结构和流程

![image-20211012153105411](https://i.loli.net/2021/10/12/sKGrv3wAWui1cE4.png)

```js
<template>
  <div class="com-container">
      记得改trend_ref
    <div class="com-chart" ref="trend_ref"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartInstance: null,
      allData: null //服务器返回数据
    };
  },
  mounted() {
    this.initChart();
    this.getData();
    window.addEventListener("resize", this.screenAdapter);
    this.screenAdapter();
  },
  destroyed() {
    window.removeEventListener("resize", this.screenAdapter);
  },
  methods: {
    initChart() {
      this.chartInstance = this.$echarts.init(this.$refs.trend_ref);
      const initOption = {};
      this.chartInstance.setOption(initOption);
    },
    async getData() {
      //await this . $http. get()
      //对allData进行赋值
      this.updateChart();
    },
    updateChart() {
      // 处理数据
      const dataOption = {};
      this.chartInstance.setOption(dataOption);
    },
    screenAdapter() {
      // 和分辨率大小相关的配置项
      const adapterOption = {};
      this.chartInstance.setOption(adapterOption);
      // 手动的调用图表对象的resize才能产生效果
      this.chartInstance.resize();
    }
  }
};
</script>

<style></style>

```

#### 商家销售统计(横向柱状图)

![image-20211012152427834](C:/Users/Roy_Dust/AppData/Roaming/Typora/typora-user-images/image-20211012152427834.png)

> Seller.vue

```js
<!--  商家销量统计的横向柱状图 -->
<template>
  <div class="com-container">
    <div class="com-chart" ref="seller_ref"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartInstance: null,
      allData: null, //服务器返回数据
      currentPage: 1, //当前显示的页数
      totalPage: 0, //一共有多少页
      timerId: null //定时器的标识
    };
  },
  mounted() {
    this.initChart();
    this.getData();
    window.addEventListener("resize", this.screenAdapter);
    // 在页面加载完成的时候，主动进行屏幕的适配
    this.screenAdapter();
  },
  destroyed() {
    clearInterval(this.timerId);
    // 销毁的时候，需要将监听器取消掉
    window.removeEventListener("resize", this.screenAdapter);
  },
  methods: {
    // 初始化echartInstance对象
    initChart() {
      this.chartInstance = this.$echarts.init(this.$refs.seller_ref, "chalk");
      // 对图表初始化配置的控制
      const initOption = {
        title: {
          text: "▎商家销售统计",
          left: 20,
          top: 20
        },
        grid: {
          top: "20%",
          left: "3%",
          right: "6%",
          bottom: "3%",
          containLabel: true //距离是包含坐标轴上的文字
        },
        xAxis: {
          type: "value"
        },
        yAxis: {
          type: "category"
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "line",
            z: 0,
            lineStyle: {
              color: "#2D3443"
            }
          }
        },
        series: [
          {
            type: "bar",
            label: {
              show: true,
              position: "right",
              textStyle: {
                color: "white"
              }
            },
            itemStyle: {
              // 指明颜色渐变的方向
              // 指明不同百分比之下颜色的值
              color: new this.$echarts.graphic.LinearGradient(0, 0, 1, 0, [
                // 百分之0状态之下的颜色值
                {
                  offset: 0,
                  color: "#5052EE"
                },
                // 百分之100状态之下的颜色值
                {
                  offset: 1,
                  color: "#AB6EE5"
                }
              ])
            }
          }
        ]
      };
      this.chartInstance.setOption(initOption);

      // 对图表对象进行鼠标事件的监听
      this.chartInstance.on("mouseover", () => {
        clearInterval(this.timerId);
      });
      this.chartInstance.on("mouseout", () => {
        this.startInterval();
      });
    },
    // 获取服务器的数据
    async getData() {
      // 127.0.0.1:8888/api/seller
      const { data: ret } = await this.$http.get("seller");
      this.allData = ret;
      // 对数据进行排序
      this.allData.sort((a, b) => {
        return a.value - b.value;
      });
      // 每五个元素显示一页
      this.totalPage = Math.ceil(this.allData.length / 5);
      this.updataChart();
      // 启动定时器
      this.startInterval();
    },
    // 更新图表
    updataChart() {
      const start = (this.currentPage - 1) * 5;
      const end = this.currentPage * 5;
      const showData = this.allData.slice(start, end);
      const sellerNames = showData.map(item => {
        return item.name;
      });
      console.log(sellerNames);
      const sellerValues = showData.map(item => {
        return item.value;
      });
      console.log(sellerValues);
      // echarts配置
      const dataOption = {
        yAxis: {
          data: sellerNames
        },
        series: [
          {
            data: sellerValues
          }
        ]
      };
      this.chartInstance.setOption(dataOption);
    },
    // 设置定时器，页数加一
    startInterval() {
      if (this.timerId) {
        clearInterval(this.timerId);
      }
      this.timerId = setInterval(() => {
        this.currentPage++;
        if (this.currentPage > this.totalPage) {
          this.currentPage = 1;
        }
        this.updataChart();
      }, 3000);
    },
    // 和器的大小发生变化的时度，会调用的方法。完成屏基的适配
    screenAdapter() {
      const titleFontSize = (this.$refs.seller_ref.offsetWidth / 100) * 3.6;
      // 和分辨率大小相关的配置项
      const adapterOption = {
        title: {
          textStyle: {
            fontSize: titleFontSize
          }
        },
        tooltip: {
          axisPointer: {
            lineStyle: {
              width: titleFontSize
            }
          }
        },
        series: [
          {
            barWidth: titleFontSize,
            itemStyle: {
              barBorderRadius: [0, titleFontSize / 2, titleFontSize / 2, 0]
            }
          }
        ]
      };
      this.chartInstance.setOption(adapterOption);
      // 手动的调用图表对象的resize才能产生效果
      this.chartInstance.resize();
    }
  }
};
</script>

<style></style>
```

#### 销量趋势图表(折线图)

![image-20211012175147435](https://i.loli.net/2021/10/12/FqGBbf6PikaTjA8.png)

```js
<template>
  <div class="com-container">
    <div class="title" :style="comStyle">
      <span>{{ "▎ " + showTitle }}</span>
      <span
        class="iconfont title-icon"
        @click="showChoice = !showChoice"
        :style="comStyle"
        >&#xe6eb;</span
      >
      <div class="select-con" v-show="showChoice" :style="marginStyle">
        <div
          class="select-item"
          v-for="item in selectTypes"
          :key="item.key"
          @click="handleSelect(item.key)"
        >
          {{ item.text }}
        </div>
      </div>
    </div>
    <div class="com-chart" ref="trend_ref"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartInstance: null,
      allData: null, //服务器返回数据
      showChoice: false, //是否显示可选项
      choiceType: "map", //显示数据类型
      titleFontSize: 0 //指明标题的字体大小
    };
  },
  mounted() {
    this.initChart();
    this.getData();
    window.addEventListener("resize", this.screenAdapter);
    this.screenAdapter();
  },
  destroyed() {
    window.removeEventListener("resize", this.screenAdapter);
  },
  computed: {
    selectTypes() {
      if (!this.allData) {
        return [];
      } else {
        return this.allData.type.filter(item => {
          return item.key !== this.choiceType;
        });
      }
    },
    showTitle() {
      if (!this.allData) {
        return "";
      } else {
        return this.allData[this.choiceType].title;
      }
    },
    // 设置给标题的样式
    comStyle() {
      return {
        fontSize: this.titleFontSize + "px"
      };
    },
    marginStyle() {
      return {
        marginLeft: this.titleFontSize + "px"
      };
    }
  },
  methods: {
    initChart() {
      this.chartInstance = this.$echarts.init(this.$refs.trend_ref, "chalk");
      const initOption = {
        grid: {
          left: "3%",
          top: "35%",
          right: "4%",
          bottom: "1%",
          containLabel: true
        },
        tooltip: {
          trigger: "axis"
        },
        legend: {
          left: 20,
          top: "15%",
          icon: "circle"
        },
        xAxis: {
          type: "category",
          boundaryGap: false
        },
        yAxis: {
          type: "value"
        }
      };
      this.chartInstance.setOption(initOption);
    },
    async getData() {
      //await this . $http. get()
      //对allData进行赋值
      const { data: ret } = await this.$http.get("trend");
      this.allData = ret;
      this.updateChart();
    },
    updateChart() {
      // 半透明的颜色值
      const colorArr1 = [
        "rgba(11, 168, 44, 0.5)",
        "rgba(44, 110, 255, 0.5)",
        "rgba(22, 242, 217, 0.5)",
        "rgba(254, 33, 30, 0.5)",
        "rgba(250, 105, 0, 0.5)"
      ];
      // 全透明的颜色值
      const colorArr2 = [
        "rgba(11, 168, 44, 0)",
        "rgba(44, 110, 255, 0)",
        "rgba(22, 242, 217, 0)",
        "rgba(254, 33, 30, 0)",
        "rgba(250, 105, 0, 0)"
      ];
      // 处理数据
      // 类目轴的数据
      const timeArr = this.allData.common.month;
      // y轴的数据 series下的数据
      const valueArr = this.allData[this.choiceType].data;
      const seriesArr = valueArr.map((item, index) => {
        return {
          name: item.name,
          type: "line",
          data: item.data,
          stack: this.choiceType,
          areaStyle: {
            color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [
              // 百分之0状态之下的颜色值
              {
                offset: 0,
                color: colorArr1[index]
              },
              // 百分之100状态之下的颜色值
              {
                offset: 1,
                color: colorArr2[index]
              }
            ])
          }
        };
      });
      // 图例的数据
      const legendArr = valueArr.map(item => {
        return item.name;
      });
      const dataOption = {
        xAxis: {
          data: timeArr
        },
        legend: {
          data: legendArr
        },
        series: seriesArr
      };
      this.chartInstance.setOption(dataOption);
    },
    screenAdapter() {
      // 和分辨率大小相关的配置项
      this.titleFontSize = (this.$refs.trend_ref.offsetWidth / 100) * 3.6;
      const adapterOption = {
        legend: {
          itemWidth: this.titleFontSize,
          itemHeight: this.titleFontSize,
          itemGap: this.titleFontSize,
          textStyle: {
            fontSize: this.titleFontSize / 2
          }
        }
      };
      this.chartInstance.setOption(adapterOption);
      // 手动的调用图表对象的resize才能产生效果
      this.chartInstance.resize();
    },
    handleSelect(currentType) {
      this.choiceType = currentType;
      this.updateChart();
      this.showChoice = false;
    }
  }
};
</script>

<style lang="less" scoped>
.title {
  position: absolute;
  left: 20px;
  top: 20px;
  z-index: 10;
  color: white;
  .title-icon {
    margin-left: 10px;
    cursor: pointer;
  }
  .select-con{
    background-color: #222733;
  }
}
</style>

```



#### 商家分布模块(地图+散点图)



```JS
<template>
  <div class="com-container" @dblclick="revertMap">
    <div class="com-chart" ref="map_ref"></div>
  </div>
</template>

<script>
import axios from "axios";
import { getProvinceMapInfo } from "@/utils/map_utils";
export default {
  data() {
    return {
      chartInstance: null,
      allData: null, //服务器返回数据
      mapData: {} //获取省份的地图矢量数据
    };
  },
  mounted() {
    this.initChart();
    this.getData();
    window.addEventListener("resize", this.screenAdapter);
    this.screenAdapter();
  },
  destroyed() {
    window.removeEventListener("resize", this.screenAdapter);
  },
  methods: {
    async initChart() {
      this.chartInstance = this.$echarts.init(this.$refs.map_ref, "chalk");
      // 获取中国地图的矢量数据
      // 于我们现在获取的地图矢量数据并不是位于KOA2的后台，所以咱们不能使用this.$http
      const ret = await axios.get(
        "http://localhost:8999/static/map/china.json"
      );
      this.$echarts.registerMap("china", ret.data);
      const initOption = {
        title: {
          text: "▎ 商家分布",
          left: 20,
          top: 20
        },
        geo: {
          type: "map",
          map: "china",
          top: "5%",
          bottom: "5%",
          itemStyle: {
            areaColor: "#2E72BF",
            borderColor: "#333"
          }
        },
        legend: {
          left: "5%",
          bottom: "5%",
          orient: "vertical"
        }
      };
      this.chartInstance.setOption(initOption);
      this.chartInstance.on("click", async arg => {
        // arg.name 得到所点击的省份，这个省份是中文 通过getProvinceMapInfo这个utils来改成拼音和获取json
        const provinceInfo = getProvinceMapInfo(arg.name);
        console.log(provinceInfo);
        // 需要获取这个省份的地图矢量数据
        // 判断当前所点击的省份的地图矢量数据是否存在
        if (!this.mapData[provinceInfo.key]) {
          const ret = await axios.get(
            "http://localhost:8999" + provinceInfo.path
          );
          this.mapData[provinceInfo.key] = ret.data;
          this.$echarts.registerMap(provinceInfo.key, ret.data);
        }
        const changeOption = {
          geo: {
            map: provinceInfo.key
          }
        };
        this.chartInstance.setOption(changeOption);
      });
    },
    async getData() {
      //await this.$http.get()
      //对allData进行赋值
      const { data: ret } = await this.$http.get("map");
      this.allData = ret;
      console.log(this.allData);
      this.updateChart();
    },
    updateChart() {
      // 处理数据
      // 图例的数据
      const legendArr = this.allData.map(item => {
        return item.name;
      });
      const seriesArr = this.allData.map(item => {
        // return的这个对象就代表的是一个类别下的所有散点数据
        // 示散点的数据，所以我们需要给散点的图表增加一个配置，coordinateSystem: geo
        return {
          type: "effectScatter",
          rippleEffect: {
            scale: 5,
            brushType: "stroke"
          },
          name: item.name,
          data: item.children,
          coordinateSystem: "geo"
        };
      });
      const dataOption = {
        legend: {
          data: legendArr
        },
        series: seriesArr
      };
      this.chartInstance.setOption(dataOption);
    },
    screenAdapter() {
      const titleFontSize = (this.$refs.map_ref.offsetWidth / 100) * 3.6;
      // 和分辨率大小相关的配置项
      const adapterOption = {
        title: {
          textStyle: {
            fontSize: titleFontSize
          }
        },
        legend: {
          itemWidth: titleFontSize / 2,
          itemHeight: titleFontSize / 2,
          itemGap: titleFontSize / 2,
          textStyle: {
            fontSize: titleFontSize / 2
          }
        }
      };
      this.chartInstance.setOption(adapterOption);
      // 手动的调用图表对象的resize才能产生效果
      this.chartInstance.resize();
    },
    // 回到中国地图
    revertMap() {
      const revertOption = {
        geo: {
          map: "china"
        }
      };
      this.chartInstance.setOption(revertOption);
    }
  }
};
</script>

<style></style>

```



#### 销量排行模块(柱状图)



```JS
<!-- 地区销售排行 -->
<template>
  <div class='com-container'>
    <div class='com-chart' ref='rank_ref'></div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      chartInstance: null,
      allData: null,
      startValue: 0, // 区域缩放的起点值
      endValue: 9, // 区域缩放的终点值
      timerId: null // 定时器的标识
    }
  },
  mounted () {
    this.initChart()
    this.getData()
    window.addEventListener('resize', this.screenAdapter)
    this.screenAdapter()
  },
  destroyed () {
    window.removeEventListener('resize', this.screenAdapter)
    clearInterval(this.timerId)
  },
  methods: {
    initChart () {
      this.chartInstance = this.$echarts.init(this.$refs.rank_ref, 'chalk')
      const initOption = {
        title: {
          text: '▎ 地区销售排行',
          left: 20,
          top: 20
        },
        grid: {
          top: '40%',
          left: '5%',
          right: '5%',
          bottom: '5%',
          containLabel: true
        },
        tooltip: {
          show: true
        },
        xAxis: {
          type: 'category'
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            type: 'bar'
          }
        ]
      }
      this.chartInstance.setOption(initOption)
      this.chartInstance.on('mouseover', () => {
        clearInterval(this.timerId)
      })
      this.chartInstance.on('mouseout', () => {
        this.startInterval()
      })
    },
    async getData () {
      // 获取服务器的数据, 对this.allData进行赋值之后, 调用updateChart方法更新图表
      const { data: ret } = await this.$http.get('rank')
      this.allData = ret
      // 对allData里面的每一个元素进行排序, 从大到小进行
      this.allData.sort((a, b) => {
        return b.value - a.value
      })
      console.log(this.allData)
      this.updateChart()
      this.startInterval()
    },
    updateChart () {
      const colorArr = [
        ['#0BA82C', '#4FF778'],
        ['#2E72BF', '#23E5E5'],
        ['#5052EE', '#AB6EE5']
      ]
      // 处理图表需要的数据
      // 所有省份所形成的数组
      const provinceArr = this.allData.map(item => {
        return item.name
      })
      // 所有省份对应的销售金额
      const valueArr = this.allData.map(item => {
        return item.value
      })
      const dataOption = {
        xAxis: {
          data: provinceArr
        },
        dataZoom: {
          show: false,
          startValue: this.startValue,
          endValue: this.endValue
        },
        series: [
          {
            data: valueArr,
            itemStyle: {
              color: arg => {
                let targetColorArr = null
                if (arg.value > 300) {
                  targetColorArr = colorArr[0]
                } else if (arg.value > 200) {
                  targetColorArr = colorArr[1]
                } else {
                  targetColorArr = colorArr[2]
                }
                return new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  {
                    offset: 0,
                    color: targetColorArr[0]
                  },
                  {
                    offset: 1,
                    color: targetColorArr[1]
                  }
                ])
              }
            }
          }
        ]
      }
      this.chartInstance.setOption(dataOption)
    },
    screenAdapter () {
      const titleFontSize = this.$refs.rank_ref.offsetWidth / 100 * 3.6
      const adapterOption = {
        title: {
          textStyle: {
            fontSize: titleFontSize
          }
        },
        series: [
          {
            barWidth: titleFontSize,
            itemStyle: {
              barBorderRadius: [titleFontSize / 2, titleFontSize / 2, 0, 0]
            }
          }
        ]
      }
      this.chartInstance.setOption(adapterOption)
      this.chartInstance.resize()
    },
    startInterval () {
      if (this.timerId) {
        clearInterval(this.timerId)
      }
      this.timerId = setInterval(() => {
        this.startValue++
        this.endValue++
        if (this.endValue > this.allData.length - 1) {
          this.startValue = 0
          this.endValue = 9
        }
        this.updateChart()
      }, 2000)
    }
  }
}
</script>

<style lang='less' scoped>
</style>

```



#### 热销商品占比模块(饼图)



```js
<template>
  <div class="com-container">
    <div class="com-chart" ref="hot_ref"></div>
    <span class="iconfont arr-left" @click="toLeft" :style="comStyle"
      >&#xe6ef;</span
    >
    <span class="iconfont arr-right" @click="toRight" :style="comStyle"
      >&#xe6ed;</span
    >
    <span class="cat-name" :style="comStyle">{{ catname }}</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartInstance: null,
      allData: null, //服务器返回数据
      currentIndex: 0, //当前所展示出的一级分类数据
      titleFontSize: 0
    };
  },
  computed: {
    catname() {
      if (!this.allData) {
        return "";
      } else {
        return this.allData[this.currentIndex].name;
      }
    },
    comStyle() {
      return {
        fontSize: this.titleFontSize + "px"
      };
    }
  },
  mounted() {
    this.initChart();
    this.getData();
    window.addEventListener("resize", this.screenAdapter);
    this.screenAdapter();
  },
  destroyed() {
    window.removeEventListener("resize", this.screenAdapter);
  },
  methods: {
    initChart() {
      this.chartInstance = this.$echarts.init(this.$refs.hot_ref, "chalk");
      const initOption = {
        title: {
          text: "▎热销商品的占比",
          left: 20,
          top: 20
        },
        legend: {
          top: "15%",
          icon: "circle"
        },
        tooltip: {
          show: true,
          formatter: arg => {
            const thirdCategory = arg.data.children;
            // 计算出所有三季分类的数值总和
            let total = 0;
            thirdCategory.forEach(item => {
              total += item.value;
            });
            let retStr = "";
            thirdCategory.forEach(item => {
              retStr += `
              ${item.name}:${parseInt((item.value / total) * 100) + "%"}
              <br/>
              `;
            });
            return retStr;
          }
        },
        series: [
          {
            type: "pie",
            label: {
              show: false
            },
            emphasis: {
              label: {
                show: true
              },
              labelLine: {
                show: false
              }
            }
          }
        ]
      };
      this.chartInstance.setOption(initOption);
    },
    async getData() {
      //await this . $http. get()
      //对allData进行赋值
      const { data: ret } = await this.$http.get("hotproduct");
      this.allData = ret;
      console.log(this.allData[0]);
      this.updateChart();
    },
    updateChart() {
      // 处理数据
      const legendData = this.allData[this.currentIndex].children.map(item => {
        return item.name;
      });
      const seriesData = this.allData[this.currentIndex].children.map(item => {
        return {
          name: item.name,
          value: item.value,
          children: item.children
        };
      });
      const dataOption = {
        legend: {
          data: legendData
        },
        series: [
          {
            data: seriesData
          }
        ]
      };
      this.chartInstance.setOption(dataOption);
    },
    screenAdapter() {
      // 和分辨率大小相关的配置项
      this.titleFontSize = (this.$refs.hot_ref.offsetWidth / 100) * 3.6;
      const adapterOption = {
        title: {
          textStyle: {
            fontSize: this.titleFontSize
          }
        },
        legend: {
          itemWidth: this.titleFontSize / 2,
          itemHeight: this.titleFontSize / 2,
          itemGap: this.titleFontSize / 2,
          textStyle: {
            fontSize: this.titleFontSize / 2
          }
        },
        series: [
          {
            radius: this.titleFontSize * 4.5,
            center: ["50%", "60%"]
          }
        ]
      };
      this.chartInstance.setOption(adapterOption);
      // 手动的调用图表对象的resize才能产生效果
      this.chartInstance.resize();
    },
    toLeft() {
      this.currentIndex--;
      if (this.currentIndex < 0) {
        this.currentIndex = this.allData.length - 1;
      }
      this.updateChart();
    },
    toRight() {
      this.currentIndex++;
      if (this.currentIndex > this.allData.length - 1) {
        this.currentIndex = 0;
      }
      this.updateChart();
    }
  }
};
</script>

<style lang="less" scoped>
.arr-left {
  position: absolute;
  left: 10%;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  color: white;
}
.arr-right {
  position: absolute;
  right: 10%;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  color: white;
}
.cat-name {
  position: absolute;
  left: 80%;
  bottom: 20px;
  color: white;
}
</style>

```



#### 库存与销量模块(圆环饼图)



```js
<template>
  <div class="com-container">
    <div class="com-chart" ref="stock_ref"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartInstance: null,
      allData: null, //服务器返回数据
      currentIndex: 0, //当前显示数据
      timerId: null //定时器的标识
    };
  },
  mounted() {
    this.initChart();
    this.getData();
    window.addEventListener("resize", this.screenAdapter);
    this.screenAdapter();
  },
  destroyed() {
    window.removeEventListener("resize", this.screenAdapter);
  },
  methods: {
    initChart() {
      this.chartInstance = this.$echarts.init(this.$refs.stock_ref, "chalk");
      const initOption = {
        title: {
          text: "▎库存和销量分析",
          left: 20,
          top: 20
        }
      };
      this.chartInstance.setOption(initOption);
      this.chartInstance.on("mouseover", () => {
        clearInterval(this.timerId);
      });
      this.chartInstance.on("mouseout", () => {
        this.startInterval();
      });
    },
    async getData() {
      //await this . $http. get()
      //对allData进行赋值
      const { data: ret } = await this.$http.get("stock");
      this.allData = ret;
      console.log(this.allData);
      this.updateChart();
      this.startInterval();
    },
    updateChart() {
      const centerArr = [
        ["18%", "40%"],
        ["50%", "40%"],
        ["82%", "40%"],
        ["34%", "75%"],
        ["66%", "75%"]
      ];
      const colorArr = [
        ["#4FF778", "#0BA82C"],
        ["#E5DD45", "#E8B11C"],
        ["#E8821C", "#E55445"],
        ["#5052EE", "#AB6EE5"],
        ["#23E5E5", "#2E72BF"]
      ];
      // 处理数据
      const start = this.currentIndex * 5;
      const end = (this.currentIndex + 1) * 5;
      const showData = this.allData.slice(start, end);
      const seriesArr = showData.map((item, index) => {
        return {
          type: "pie",
          radius: [110, 100],
          center: centerArr[index],
          hoverAnimation: false, //关闭鼠标移入到饼图时的动画效果
          labelLine: {
            show: false //隐藏指示线
          },
          label: {
            position: "center",
            color: colorArr[index][0]
          },
          data: [
            {
              name: item.name + "\n" + item.sales,
              value: item.sales,
              itemStyle: {
                color: new this.$echarts.graphic.LinearGradient(0, 1, 0, 0, [
                  {
                    offset: 0,
                    color: colorArr[index][0]
                  },
                  {
                    offset: 1,
                    color: colorArr[index][1]
                  }
                ])
              }
            },
            {
              value: item.stock,
              itemStyle: {
                color: "#333843"
              }
            }
          ]
        };
      });
      const dataOption = {
        series: seriesArr
      };
      this.chartInstance.setOption(dataOption);
    },
    screenAdapter() {
      const titleFontSize = this.$refs.stock_ref.offsetWidth / 100 * 3.6
      const innerRadius = titleFontSize * 2
      const outterRadius = innerRadius * 1.125
      const adapterOption = {
        title: {
          textStyle: {
            fontSize: titleFontSize
          }
        },
        series: [
          {
            type: 'pie',
            radius: [outterRadius, innerRadius],
            label: {
              fontSize: titleFontSize / 2
            }
          },
          {
            type: 'pie',
            radius: [outterRadius, innerRadius],
            label: {
              fontSize: titleFontSize / 2
            }
          },
          {
            type: 'pie',
            radius: [outterRadius, innerRadius],
            label: {
              fontSize: titleFontSize / 2
            }
          },
          {
            type: 'pie',
            radius: [outterRadius, innerRadius],
            label: {
              fontSize: titleFontSize / 2
            }
          },
          {
            type: 'pie',
            radius: [outterRadius, innerRadius],
            label: {
              fontSize: titleFontSize / 2
            }
          }
        ]
      }
      this.chartInstance.setOption(adapterOption)
      this.chartInstance.resize()
    },
    startInterval() {
      if (this.timerId) {
        clearInterval(this.timerId);
      }
      this.timerId = setInterval(() => {
        this.currentIndex++;
        if (this.currentIndex > 1) {
          this.currentIndex = 0;
        }
        this.updateChart();
      }, 5000);
    }
  }
};
</script>

<style></style>

```





### 3、WebSocket的引入

#### 后端

![image-20211017144539790](https://i.loli.net/2021/10/17/ugpoH3Fn5xwjLtC.png)

```js

const WebSocket = require('ws')
// 创建WebSocket服务端的对象，绑定的端口号是9998
const wss = new WebSocket.Server({
  port: 9998
})
// 对客户端的连接事件进行监听
// client: 代表的是客户端的连接socket对象
wss.on('connection', client => {
  console.log("有客户端链接成功了...");
  // 对客户端的连接对象进行message事件的监听
  // msg:由客户端发给服务端的数据
  client.on('message', msg => {
    console.log('客户端发送数据给服务端了：' + msg);
    // 由服务端往客户端发送数据
    client.send('hello socket from backend')
  })
})
```



#### 前端

![image-20211017152132454](https://i.loli.net/2021/10/17/nugk3R4WoEUsjrN.png)

```js
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <button id="connect">连接</button>
  <button id="send" disabled="true">发送数据</button> <br>
  从服务端接收的数据如下： <br>
  <span id="recv"></span>
  <script>
    var connect = document.querySelector('#connect')
    var send = document.querySelector('#send')
    var recv = document.querySelector('#recv')
    let ws = null;
    connect.onclick = function () {
      ws = new WebSocket('ws://localhost:9998')
      ws.onopen = () => {
        console.log('连接服务端成功了...');
        send.disabled= false
      }
      ws.onclose = () => {
        console.log("连接服务器失败...");
        send.disabled= true
      }
      ws.onmessage = msg => {
        console.log('接收到从服务端发送过来的数据了');
        console.log(msg);
        recv.innerHTML = msg.data
      }
    }
    send.onclick = function () {
      ws.send('hello socket from frontend')
    }
  </script>
</body>

</html>
```

#### websocket对后端的改造

##### 创建web_socket service.js

![image-20211017154634042](https://i.loli.net/2021/10/17/HxBhKlPry6oFQV7.png)



##### 服务端接收数据字段约定

![image-20211017154259574](https://i.loli.net/2021/10/17/WZXN4yDG1vYhtfx.png)

##### 服务端发送数据字段约定

![image-20211017155002533](https://i.loli.net/2021/10/17/8IbiE3QrxShHZjd.png)



### 4、细节处理

