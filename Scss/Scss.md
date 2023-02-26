## 1.Scss的安装

​	在vscode中，我们可以直接通过插件来将scss编译为css文件

​	插件推荐：**Live Sass Compiler**

​	插件配置

```json
{
  "liveSassCompiler.settings.formats":[
    {
    	/*
        :nested -嵌套格式
        :expanded -展开格式
        :compact -紧液格式
        :compressed-压缩格式
       */
				"format": "compact"，//可定制的出口cSs样式（expanded，compact，compressed，nested)
				"extensionName": ".css",
				"savePath": "~/../css             //为null 表示当前目录
				//设置编译后的保存路径
    }
  ],
  "liveSassCompile.settingss.excludeList":[
    "**/node_modules/**",
    "./	vscode/**"
  ],
  /*
  	是否生成对应的map文件
  */
  "liveSassCompile.settingss.generateMap":true,
  /* 是否添加前缀 -webkit- -moz-   等*/
  "liveSassCompile.settingss.autoprefix":[
    ">1%",
    "last 2 version"
  ],
  "explorer.confirmDelete":true
}
```

## 2.Scss语法扩展

### （1）选择器嵌套

​	在css中我们一般会使用大量的子类选择器，来编写css样式，这样当层级深了之后就难以辨别。

```css
例如：下面的css样式表
.container{
  width:1200px;
  margin:0 auto;
}
.container .header{
  height:98px;
  line-height:98px;
}

在scss中我们可以通过选择器嵌套来编写
.container {
  width:1200px;
  margin:0 auto;
  .header {
    height:98px;
  	line-height:98px;
  }
}
```

### （2）父选择器&

​	在scss中当我们有一些伪元素需要绑定父元素时，我们可以直接通过&来绑定

```css
例如：给一个buttonbanging输入移入的样式
.btn:hover{
  backgroundColor:red;
  font-size:20px;
}

在scss中使用&来替代
.btn {
  &:hover {
     backgroundColor:red;
  	 font-size:20px;
  }
}
```

### （3）属性嵌套

在css中我们给一个字体添加样式例如font-size,font-weight,font-family

```css
.container a{
  color:#333;
  font-size:20px;
  font-family:sans-serif;
  font-weight:blod;
}

在scss中可以嵌套属性
.container{
  .a {
    color:#333;
    font: {
      size:20px;
      family:sans-serif;
      weight:blod;
    }
  }
}
```

### （4）占位符选择器%

有时候我们需要定义一套样式，但比并不是给某一个元素用，这时我们可以将这一套样式通过占位符定义，当**==没有使用@extend指令时，就不会编译到css中==**

```css
//定义按钮的基本样式，当没有用到时是不会编译到css中
.button%base{
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -ns-touch-action: manipulotion;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  padding: 6px 12px;
  font-size: 14px;
  line-height: 1.42857143;
  border-radius:4px;
  -webkit-user-sclect: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn-default{
  @extend:%base;
  color:#333;
  background-color:#fff;
  border-color:#ccc
}
.btn-success{
  @extend:%base;
  color:#fff;
  background-color:#5cb85c;
  border-color:#4cae4c
}
```

## 3.Scss的两种注释

多行注释：  /* */

单行注释：  //

## 4.Scss的变量

### （1）css中定义变量

在css中定义变量我们一般会在==**根选择器或body选择器下定义**==，如果在其他选择器下定义变量，但是**需要用到变量的元素不在该选择器下，那么变量是不可用的**

css中通过 ==--  来定义变量==

```css
:root{
  --color:red;
  --font-size:16px;
}
或
body{
  --color:red;
  --font-size:16px;
}
```

css通过 var(变量名)来使用变量

```css
p{
  color:var(--color)
}
```

### （2）scss中变量的定义

***定义规则***
	1.变量以美元符号(==$==开头，后面跟变量名）;

​	2.变量名是不以数字开头的可包含字母、数字、下划线、横线(连接符);

​	3.写法同css，即变量名和值之间用冒号(:)分隔;

​	4.**变量一定要先定义，后使用**;



***连接符和下划线***

​	通过连接符与下划线定义的同名变是为同一变量，建议使用连接符，后面的会覆盖前面的

### （3）scss中变量的作用域

​	scss中有**全局和局部**两种作用域，

​		在全局定义的变量就是==全局变量==，在==任何选择器中都可以使用==

​		在选择器中定义的变量就是==局部变量==，只能在==当前选择器或子选择器==中使用

​	【注】<u>**特殊情况，在局部变量后面使用  !global 那么该变量就会变成全局变量**</u>

### （4）scss中变量值的类型

SassScript 支持 6 种主要的数据类型：

* 数字，`1, 2, 13, 10px`
* 字符串，有引号字符串与无引号字符串，`"foo", 'bar', baz`
* 颜色，`blue, #04a3f9, rgba(255,0,0,0.5)`
* 布尔型，`true, false`
* 空值，`null`
* 数组 (list)，用空格或逗号作分隔符，`1.5em 1em 0 2em,       Helvetica, Arial, sans-serif`
* maps, 相当于 JavaScript 的 object，`(key1: value1, key2: value2)`

```css
$layer-index:10;Sborder-width: 3px;
$fork-base-family : "open Sans " , Helvetica,Sans-Serif;
$top-bg-color:Orgba(255,147,29,8.6);
$block-base-padding:6px 1epx 6px 10px;
$blank-mode:true;
$var:null;// 值null是其类型的唯一值。它表示缺少值，通常由函数返回头指示缺少结果。
$color-map: (color1: O#fae088，color2:#fbe20e，color3:#95d7eb);
$fonts: (serif:"Helvetica Neue",monospace: "Consolas");

.container {
	$font-size: 16px !global;
	font-size: $font-size;
	@if $blank-node {
		background-color: meee;
	}
	@else {
		background-color: wfff
	}
	content: type-of($var);
	content: length(Svar);
	color: map-get(Scolor-map,color2);
}
.footer {
	font-size: $font-size;
}

```

## 5.Scss中的@import

Sass 拓展了 `@import` 的功能，允许其导入 SCSS 或 Sass 文件。被导入的文件将合并编译到同一个 CSS 文件中.

通常，`@import` 寻找 Sass 文件并将其导入，但在以下情况下，`@import` 仅作为普通的 CSS 语句，不会导入任何 Sass 文件。

* 文件拓展名是 `.css`；
* 文件名以 `http://` 开头；
* 文件名是 `url()`；
* `@import` 包含 media queries。

如果不在上述情况中，==文件后缀名为 .scss或 .sass则会导入成功。==

如果==没有指定后缀名==，sass会默认在文件夹中寻找与其文件名相同后缀名为.scss或.sass的文件

```css
@import "foo.css";
@import "foo" screen;
@import "http://foo.com/bar";
@import url(foo);

//这几种导入方式都是直接导入
```

***scss还支持同时导入多个文件***

```css
@import "rounded-corners", "text-shadow";
```



一般我们在**被导入的scss文件**中定义变量，定义函数等，但是**会被编译成css文件**，我们是不需要就这些scss文件编译成css文件

因此我们可以在==命名文件名时前面加入  _  来区分，scss不会将带有_的文件编译==

并且我们==在导入这种文件时不需要加 _== 

***嵌套 @import***

我们可以在选择器中嵌套使用@import 导入

## 6.Scss混合指令@mixin

混合指令（Mixin）用于**==定义可重复使用的样式==**，避免了使用无语意的 class

混合指令中可以**==包含所有的css规则==**，**==绝大部分的scss规则==**

而且可以**==通过参数功能引入变量==**

### (1)基本语法

***用法：***    **@mixin 混合名**

```css
@mixin block{
  width:96%;
  margin-left:15px;
}
```

***引入***     **@inculde 混入名**

```css
.container{
  @include block;
}
```

***混入里面可以包含css选择器,并且可以直接在最外层引入***

```scss
@mixin warning-text{
  .warn-text{
    font-size:20px;
    color:#333;
  }
}
@include warning-text;
```

### (2)参数

***基本参数***

参数用于给混合指令中的样式设定变量，并且赋值使用。

在定义混合指令的时候，**==按照变量的格式，通过逗号分隔，将参数写进圆括号里==**。

**==引用指令时，按照参数的顺序，再将所赋的值对应写进括号==**：

```scss
@mixin sexy-border($color, $width) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border(blue, 1in); 
```

***参数默认值***

​	参数可以有默认值，当没有传入时就是用默认值

```scss
@mixin sexy-border($color, $width:100px) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border(blue); 
```

***关键词参数***

​	当我们进行传参时，我们可以直接通过 **==变量名:值==** 的形式传入 ，这样我们就可以不用按照定义混入时的形参顺序传入，这样就更加灵活

```scss
@mixin sexy-border($color, $width:100px) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border($width:200px,$color:red); 
```

***参数变量  （剩余参数）***

​	有时，不能确定混合指令需要使用多少个参数，比如一个关于 `box-shadow` 的混合指令不能确定有多少个 'shadow' 会被用到。

​	这时，可以使用参数变量 `…` 声明（写在参数的最后方）告诉 Sass 将这些参数视为值列表处理

```scss
@mixin box-shadow($shadows...) {
  -moz-box-shadow: $shadows;
  -webkit-box-shadow: $shadows;
  box-shadow: $shadows;
}
.shadows {
  @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
}
```

## 7.Scss继承指令@extend

