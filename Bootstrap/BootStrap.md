# BootStrap

## 1.认识BootStrap

> **BootStrap:** 
>
> ​	最流行的 HTML、CSS和JSs框架，用于在web上开发**响应式、移动优先**的项目。(v3.x)
>
> ​	响应式页面:页面布局会随着屏幕尺寸的变化而自动调整布局，作用是适配各个屏幕。
>
> ​	Bootstrap是**功能强大、可扩展，且功能丰富的前端工具包**。(v5.x)
>
> ​	Bootstrap**底层是使用Sass构建**，支持定制(Sass、Color、csS variable ...）。(v5.x)
>
> ​	Bootstrap中的网格系统、组件以及强大的JavaScript 插件可以让我们**快速搭建响应式网站**。(v5.x)

简单理解：

- Bootstrap是由HTML、CSS和JavaScript编写可复用代码的集合(包括全局样式、组件、插件等)，它是一个前端框架使用该框架能够快速开发出响应的网站（**即适配Pc、平板和移动端的网站**)。
- Bootstrap可以让我们**免去编写大量的css代码(Write less)**，让我们**更专注于网站业务逻辑的开发**
- Bootstrap是开源免费的，可以从GitHub直接拿到源码。	

【注】**`为了保持不同设备网页的风格统一`**

## 2.BootStrap 的优缺点

**（1）优点：**

- Bootstrap在Web开发人员中如此受欢迎的原因之一是它具有简单的文件结构，只需要懂HTML、CSS和JS的基本知识，就可以上手使用Bootstrap，甚至阅读其源码，对于初学者来是说易于学习。
- Bootstrap拥有一个**强大的网格系统，它是由行和列组成，我们可以直接创建网格**，无需自行编写媒体查询来创建。
- Bootstrap**预定义很多响应式的类**。例如，给图片添加.img-responsive类，图片将会根据用户的屏幕尺寸自动调整图像大小更方便我们去做各个屏幕的适配。另外Bootstrap还提供了很多额外的工具类辅助我们进行网页开发。
- Bootstrap框架**提供的组件、插件、布局、栅格系统、响应式工具**等等，可以为我们节省了大量的开发时间。

**（2）缺点：**

- **不适合高度定制类型的项目**，因为Bootstrap**具有统一的视觉风格**，**高度定制类的项目需要大量的自定义和样式覆盖**

- Bootstrap的**框架文件比较大**(61KB JS + 159KB CSS)，资源文件过大会**增加网站首屏加载的时间，并加重服务器的负担**。
- Bootstrap样式相对笨重，也会额外添加一些不必要的HTML元素，他会浪费一小部分浏览器的资源。

## 3.BootStrap 安装方式

**方式一:在页面中，直接通过CDN的方式引入。**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">
    <title>Document</title>
</head>
<body>
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-Fy6S3B9q64WdZWQUiU+q4/2Lc9npb8tCaSX9FK7E8HnRr0Jz8D6OP9dO5Vg3Q9ct" crossorigin="anonymous"></script>
</body>
</html>
```

**方式二:下载Bootstrap框架，并在页面中手动引入。**

​	**（1）官网下载Bootstrap源码**

​	**（2）在页面中是以哦那个link标签引入bootstrap.css**

​	**（3）引入jQuery文件**

​	**（4）引入Bootstrap JS组件、插件文件文件**

源码包包含的文件：

![16754034753012c52151da814c8e7.png](https://img.picgo.net/2023/02/03/16754034753012c52151da814c8e7.png)

**方式三:使用npm包管理工具安装到项目中(npm在Node基础阶段会讲解)**

```cmd
# 使用 npm 命令
npm install bootstrap
```

## 4.屏幕分割点（Breakpoints）

**Bootstrap的一大核心就是响应式**，即开发一套系统便可以适配不同尺寸的屏幕。它**`底层原理是使用媒体查询来为我们的布局和页面创建合理的断点`**

(Breakpoints)，然后根据这些**合理的断点来给不同尺寸屏幕应用不同的CSS样式**。

媒体查询是CSS的一项功能，它允许你根据浏览器的分辨率来应用不同的CSS样式，如**@media (min-width: 576px)**

![1675406267949131a5e203b431ff9.png](https://img.picgo.net/2023/02/03/1675406267949131a5e203b431ff9.png)

## 5.响应式容器（Containers）

- **Containers容器是Bootstrap中最基本的布局元素，并且该布局支持响应式。**在使用**默认网格系统时是必需**的。
- Containers容器用于包含、填充，有时也会作为内容居中使用。容器也是可以嵌套，但大多数布局不需要嵌套容器。
- Bootstrap带有三个不同的containers容器:
  - **.container:它在每个断点处会设置不同的max-width。**
  - **.container-fluid:在所有断点处都是width: 100%**。
  - **.container-(breakpoint},默认是width:100%，直到指定断点才会修改为响应的值。**

![16754078385003d0d5020a4ce58fd.png](https://img.picgo.net/2023/02/03/16754078385003d0d5020a4ce58fd.png)

## 6.网格/栅格系统（Grid System）

在我们在开发一个页面时，经常会遇到一些列表（例如，商品列表)，这些列表通常都是通过行和列来排版。

- 对于这种列表我们可以使用float来实现，也可以使用flexbox布局实现。
- 为了方便我们对这种常见列表的布局，Bootstrap框架对它进行了封装，封装为一个网格系统(Grid system)

那什么是网格系统?

- Bootstrap网格系统是用于**构建移动设备优先的强大布局系统**，可支持**`12列网格、5个断点和数十个预定义类。`**

- 提供了一种简单而强大的方法来创建各种形状和大小的响应式布局。
- 底层使用了强大的flexbox来构建弹性布局，并支持12列的网格布局。

那么我们应该如何使用网格系统?

- 1.编写一个**container或container-fluid**容器;
- 2.在**container容器中编写row容器**;
- 3.在**row容器中编写列col容器**。

**下面我们通过一个需求来认识一下网格系统:如，使用Boostrap来实现一行3列的布局。**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">
    <title>Document</title>
    <style>
        .container{
            background-color: pink;
            margin-top: 10px;
        }
        .item{
            height: 40px;
            border:1px solid black;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="row">
            <div class="col item">1</div>
            <div class="col item">2</div>
            <div class="col item">3</div>
        </div>
    </div>
</body>
</html>
```

## 7.十二列网格系统

从Bootstrap2开始，网格系统从16列转向12列网格，原因之一是12列比以前的16列系统更灵活。

将一个容器(row)被划分为12列网格，**具有更广泛的应用,因为12可以被12、6、4、3、2、1整除，而16列网格只能被16、8、4、2、1整除**，所以12列网格能够在一行中表示更多种列数组合情况。



**`网格系统原理`**

**网格系统是由container、row、col三部分组成，底层使用flexbox来布局，并且支持12列网格布局。**

- container或container-fluid是布局容器,网格系统中必用的容器（该容器也会应用在:内容居中或作为包含其它内容等)。
  - **width: 100%/某个断点的宽;-布局的宽**
  - padding-right: 15px;-让包含的内容不会靠在布局右边缘
  - padding-left: 15px; -让包含的内容不会靠在布局左边缘
  - margin-right: auto; -布局居中
  - margin-left: auto; -布局居中

**row是网格系统中的每一行，row是存放在container容器中。**

- **如果指定列宽（使用col-【数字】），那么一行最多可以存放12列，超出列数会换行。**
- **display: flex;-指定row为弹性布局(并支持12列网格布局)**
- flex-wrap: wrap; -支持多行展示flex item。
- margin-right: -15px;-抵消container右边15px的padding
- margin-left: -15px;-抵消container左边15px的padding

**col是网格系统的每一列，col是存放在row容器中**

- **position: relative;-相对定位布局**
- **flex-grow: 1（网格系统 只使用col） / flex:0 0 x%(12列网格系统 使用 col-数字);-自动拉伸布局或占百分比**
- max-width: 100% / max-width: x%;-最大的宽
- padding-right: 15px;-让包含内容不会靠右边缘
- padding-left: 15px;-让包含内容不会靠左边缘。

## 8.网格系统-嵌套（nesting）

Bootstrap的网格系统是可以支持嵌套的，例如:

- 我们可以在某**个网格系统的某一列上继续嵌套一个网格系统**

- 当网格系统中的某一列嵌套一个网格系统的时候，嵌套的网络系统可以省略container容器。
- 因为**网格系统中的col是可以充当一个container-fluid容器**来使用(col的属性和container-fluid的属性基本一样)。

**案例：使用网格系统实现一行8列的布局**

**（1）网格系统 （只是用col）**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">
    <title>Document</title>
    <style>
        .container{
            background-color: pink;
            margin-top: 10px;
        }
        .item{
            height: 40px;
            border:1px solid black;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="row">
            <div class="col item">1</div>
            <div class="col item">2</div>
            <div class="col item">3</div>
            <div class="col item">4</div>
            <div class="col item">5</div>
            <div class="col item">6</div>
            <div class="col item">7</div>
            <div class="col item">8</div>
        </div>
    </div>
</body>
</html>
```

**（2）12列网格系统（col-数字）**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">
    <title>Document</title>
    <style>
        .container{
            background-color: pink;
            margin-top: 10px;
        }
        .item{
            height: 40px;
            border:1px solid black;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="row">
            <div class="col-6 item">
                <div class="row">
                    <div class="col-3 item">1</div>
                    <div class="col-3 item">2</div>
                    <div class="col-3 item">3</div>
                    <div class="col-3 item">4</div>
                </div>
            </div>
            <div class="col-6 item">
                <div class="row">
                    <div class="col-3 item">5</div>
                    <div class="col-3 item">6</div>
                    <div class="col-3 item">7</div>
                    <div class="col-3 item">8</div>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
```

**【注】先将一行分成两份，然后再将每一份分成4份**

## 9.网格系统的自动布局（Auto-layout）

**自动布局列col(auto layout)**

​	**col：等宽列** **底层是flex-grow : 1, max-width: 100%。该类网格系统仅用flexbox布局。**

​	**col-auto :列的宽为auto(Variable width content),底层是flex: 0 0 auto; width: auto**

​	**col-{num}:指定某个列的宽(支持12列网格) 底层是flex: 0 o x%，max-width: x%**

## 10.网格系统响应式类（Responsive Class）

- 5个断点(Breakpoints)

  **none(xs): <576px  、 sm : >=576px  、 md : >=768px  、 lg : >=992  、 xl : >=1200px**

- **响应式列布局的类**

  - **col-sm:默认width:100%，当屏幕>=576px该类启用（flexbox布局)，启用: flex-grow: 1，max-width: 100%。**
  - **col-md:默认 width:100%，当屏幕>=768px该类启用(（flexbox布局)，启用: flex-grow: 1，max-width: 100%,**

  - **col-g:默认width:100%，当屏幕>=992px该类启用(flexbox布局)，启用: flex-grow: 1，max-width: 100%,**

  - **col-xl:默认width:100%，当屏幕>=1200px该类启用(flexbox布局)，启用: flex-grow: 1，max-width: 100%。**

    

  - **col-sm-(num:默认width:100%，当屏幕>=576px该类启用(支持12列网格)，启用: flex: 0 0×%。**
  - **col-md-{num}:默认width:100%，当屏幕>=768px该类启用(支持12列网格)，启用: flex: 0 0 ×%。**

  - **col-lg-{num}默认width:100%，当屏幕>=992px该类启用(支持12列网格)，启用: flex: 0 0 x%**
  - **col-xl-{num}默认width:100%，当屏幕>=1200px该类启用(支持12列网格),启用:flex: 00x%。**

- **需求:开发响应式列表。**

   **在xl屏幕显示6列，在lg屏幕显示4列，在md屏幕显示3列，在sm屏幕显示2列，特小屏(none)显示1列。**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">
    <title>Document</title>
    <style>
        .container{
            background-color: pink;
            margin-top: 10px;
        }
        .item{
            height: 40px;
            border:1px solid black;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="row">
            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2 item">1</div>
            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2 item">2</div>
            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2 item">3</div>
            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2 item">4</div>
            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2 item">5</div>
            <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2 item">6</div>
        </div>
    </div>

</body>
</html>
```

## 11.响应式工具类Display

![1675501798506aeb3f675a8dc3813.png](https://img.picgo.net/2023/02/04/1675501798506aeb3f675a8dc3813.png)

![16755018104088bc94e84b4fd3403.png](https://img.picgo.net/2023/02/04/16755018104088bc94e84b4fd3403.png)

## 12.Bootstrap组件

> 参考地址：https://v4.bootcss.com/docs/components/alerts/