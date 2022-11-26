# 常用css

## 背景平铺

```js
body {
            background:url("image/游戏.png")  no-repeat center center;   /*加载背景图*/   /* 背景图不平铺 */
            background-size:cover;  /* 让背景图基于容器大小伸缩 */
            background-attachment:fixed;        /* 当内容高度大于图片高度时，背景图像的位置相对于viewport固定 */    //此条属性必须设置否则可能无效/
        background-color:#CCCCCC;   /* 设置背景颜色，背景图加载过程中会显示背景色 */
        }
```

