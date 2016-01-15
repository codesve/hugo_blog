---
author: 本根
comments: true
date: 2015-06-24 20:14:03+00:00
layout: post
slug: use r.js to build requirejs project
title: 用r.js优化require/backbone前端项目
wordpress_id: 1
categories:
- nothing
---


## 目的

> * 将用RequireJs和BackboneJs开发的WEB项目打包发布；
> * 将所有模块的js压缩到一个js文件中；
> * 将所有的css压缩到一个css文件中；
> * 从而减少网络访问次数，提升用户体验；

## 步骤

### 1. 安装node.js

* 直接下载安装即可[https://nodejs.org/download/](https://nodejs.org/download/ "下载NodeJs")


### 2. 安装requireJs模块

```bash

	npm install -g requirejs

```

可能需要sudo权限


### 3. 安装almond.js

在项目根目录下运行以下命令

```bash

	bower install almond

```

关于almond可以到[https://github.com/jrburke/almond](https://github.com/jrburke/almond "almond")了解


### 4. 在项目根目录新建一个build.js文件，内容如下：

```js

	/**
	 * r.js config
	 * See all the options and more at:
	 * https://github.com/jrburke/r.js/blob/master/build/example.build.js
	 */

	({
    mainConfigFile: 'js/main.js',
    baseUrl: 'js',

    fileExclusionRegExp: /^(r|build)\.js$/,
    name: '../bower_components/almond/almond',

    out: './dist/js/shop.min.js',

    optimize: 'uglify2',/*none or uglify2*/

    include: [
      'main',
      'views/FirstView',
      'views/TimePeriodView',
      'views/WelcomeView',
      'views/bath/BathView',
      'views/beauty/BeautyView',
      'views/store/CommodityView',
      'views/store/CommodityDetailView',
      'views/cart/CartView',
      'views/address/AddressView',
      'views/order/OrderView',
      'views/evaluate/EvaluateView',
      'views/coupon/CouponView',
      'views/pay/PayView'
    ]
	})

```

* `mainConfigFile`指定requirejs的入口文件
* `baseUrl`指定requirejs的js目录
* `fileExclusionRegExp`排除规则，满足条件的文件不会被优化
* `name`指定almond所在目录
* `out`指定优化后的输出文件
* `optimize`压缩方式
* `include`要优化的模块，必须包含main，其它的复制router.js里指定的View文件路径即可

### 5. 执行build.js

```bash

	r.js -o build.js

```

可能需要sudo权限，运行后项目根目录多了个dist文件夹，过程可能报错，根据报错信息处理即可

### 6. 合并压缩CSS文件

```bash

	r.js -o cssIn=css/styles.css out=dist/css/shop.min.css 

```

`styles.css`中@import了所有css文件

### 7. 修改index.html

将

```html 

	<link rel="stylesheet" href="css/styles.css"> 

```

修改为

```html 

	<link rel="stylesheet" href="dist/css/shop.min.css"> 

```

将

```html

	<script data-main="js/main" src="libs/require/require.js"></script>

```

修改为

```html

	<script type="text/javascript" src="dist/js/shop.min.js"></script>

```

### 8. 正常部署

-end-
