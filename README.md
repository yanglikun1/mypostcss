# postvue

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

# portCSS 部分常用插件的使用

---
## 简介
[PostCSS](https://github.com/postcss/postcss)是一个允许使用JS插件转换样式的工具。这些插件可以检查（lint）你的CSS，支持CSS变量和Mixins，编译未被浏览器广泛支持的先进的CSS语法，内联图片，以及其它很多优秀的功能。

> // 安装环境 vue-cli 创建的webpack 项目

```
// .postcssrc.js文件内容

module.exports = {
  "plugins": {
    "postcss-mixins":{},
    "postcss-define-property":{},
    "postcss-import": {},
    "postcss-url": {},
    "autoprefixer": {},
    "precss":{},
    "postcss-custom-selectors": {},
    "postcss-custom-media": {},
  }
}
```

## [preCSS](https://github.com/jonathantneal/precss)插件

简单说，PreCSS语法和Sass是最相似的。然而，PreCSS也有一些自己独特的方法，接下来我们会介绍。

> npm insatll precss --save-dev

## 官网实例代码
```
$blue: #056ef0;
$column: 200px;

.menu {
  width: calc(4 * $column);
}

.menu_link {
  background: color-mod($blue alpha(90%));
  width: $column;
}
```

### 嵌套
使用```&```符,把父选择器复制到子选择其中。
```
.menu {
    width: 100%;
    a{
        text-decoration:none;
    }
    &::before {
        content: '';
    }
}
```
### 变量
 PreCSS ,在```$```符号后面紧跟变量名，然后```:``` 再是变量值
```
 $color: #ccc;
```
### 条件

在PreCSS中也有条件命令这样的特性，其语法和Sass的相同，也是使用@if和@else.

```
 $linkcolor: 2;   // 当然这里可以是字符串
.preType {
   background: blue;
   @if $linkcolor == 2 {
     height: 100px;
   } @else {
     height: 50px;
   }
}
```

### 循环： @for 和 @each.
@for 循环通过一个数字计数器完成一个循环周期
@each 循环可以用来遍历一个项目列表

@for循环 有一个计数器变量，用来设置循环的周期，通常设置位```$i```,
可以在选择器或样式规则中插入这个变量```$i```,这样可以方便的生成像nth-of-type() 的选择器和计算宽度。
```
@for $i from 1 to 3 {
    p:nth-of-type($i) {
        margin-left:calc(100%/$i);
    }
}
```

@each循环
此循环中，他的循环周期是一个项目列表而不是数字。
注意：插入到一个字符串中你需要使用一组括号包裹一个变量名（如($var)）
```
$imgas: apply, loginbg, password, user;
$urls: ../assets/;

@each $icon in ($imgas) {
  .div-$(icon) {  // 这里不能写成 .div-($icon）
    width:100px;
    height: 100px;
    background: url($urls$icon.jpg) no-repeat;
    background-size: 100%;
  }
}
```

## [postcss-mixins](https://github.com/postcss/postcss-mixins)插件
实现样式复用可传参数；
> npm install --save-dev postcss-mixins

使用实例：
```
@define-mixin icon  $color: blue {
    .icon {
        color: $color;
    }
    .icon:hover {
        color: white;
        background: $color;
    }
}

@mixin icon ...可传参;
// output
.icon {
     color: blue;
 }
.icon:hover {
  color: white;
  background: blue;
}
```
嵌套使用

```
@define-mixin icon $name {
    padding-left: 16px;
    &::after {
        content: "";
        background-url: url(/icons/$(name).png);
    }
}

.search {
    @mixin icon search;
}
```
> 更多使用可到 github学习
> tips： [postcss-define-property](https://github.com/daleeidd/postcss-define-property) 可以实现类似的操作。

## [postcss-custom-selectors](https://github.com/postcss/postcss-custom-selectors)插件

实现 W3C CSS Extensions(Custom Selectors) 的插件

> npm install postcss-custom-selectors

使用实例：

```
@custom-selector :--heading h1, h2, h3, h4, h5, h6;

article :--heading + p {
  margin-top: 0;
}

//output
article h1 + p,
article h2 + p,
article h3 + p,
article h4 + p,
article h5 + p,
article h6 + p {
  margin-top: 0;
}

```

自定义选择其是一个伪类，所以必须使用:-- 来定义。
> tips: 目前不支持在用一个选择器中调用多个自定义选择器

例如：
```
@custom-selector :--heading h1, h2, h3, h4, h5, h6;
@custom-selector :--any-link :link, :visited;

.demo :--heading, a:--any-link {
  font-size: 32px;
}
// 将输出错误的css代码

.demo h1,
.demo h2,
.demo h3,
.demo h4,
.demo h5,
.demo h6,:link,
:visited {
  font-size: 32px;
}
```

## [postcss-custom-media](https://github.com/postcss/postcss-custom-media) 插件

将W3C CSS自定义媒体查询语法转换为更兼容的CSS

> npm install postcss-custom-media

使用示例：
```
@custom-media --small-viewport (max-width: 30em);

@media (--small-viewport) {
  /* styles for small viewport */
}

@media (max-width: 30em) {
  /* styles for small viewport */
}
```

## [postcss-import](https://github.com/postcss/postcss-import)插件

这个插件可以使用本地文件，节点模块或web_modules
```
//style.css
body{background: green}


//
@import './lib/style';
@import './lib/style' (min-width: 600px) and (orientation: landscape); //媒体类型加载不同的样式
```

## 总结

针对与PostCSS 插件的使用还有很多，上面介绍的几个插件也是项目中基本会用到的。更多细节希望在今后的使用中慢慢发现，如果对你有帮助请点赞。。。
