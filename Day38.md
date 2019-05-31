# BootStrap

## 介绍

### 什么是BootStrap

> bootstrap是一个框架 , 框架是由第三方厂商或其他的程序已经制作好的半成品 , 已经提供了很多公共的功能;
> bootstrap中文官网：[地址](http://www.bootcss.com)

### BootStrap的作用

1. 简洁、直观、强悍的前端开发框架 , 让Web开发更迅速、简单;
2. 只要有HTML、CSS、JavaScript基础知识就可以使用这个框架;

### BootStrap的优势

1. 自 BootStrap 3 起 , 框架包含了了贯穿于整个库的移动设备优先的样式;
2. 并且 BootStrap 支持所有的主流浏览器;
3. 因为以上的优势 , 所以只需要具备 HTML 和 CSS 的基础知识 , 就可以学习使用 BootStrap ;
4. BootStrap 的响应式 CSS 能够自适应于台式机、平板电脑和手机;

### 响应式设计

+ 响应式布局的特点：同一个网页在不同的设备上可以自动适配屏幕宽度 , 显示不同的布局;

+ 四类设备：BootStrap 栅格系统中一共分成四种设备类型 , 如：大型设备lg , 中型设备md , 小型设备sm , 微型设备xs;

## BootStrap 的使用

### 准备使用 Bootstrap

在 BootStrap 的官网中有着功能介绍和使用案例 , 方便我们查询和使用 , 功能分类有三大类：

1. 全局CSS：基本的 HTML 元素均可以通过 class 设置样式并得到增强效果;
2. 组件：可复用的组件 , 包括字体图标、下拉菜单、导航、警告框、弹出框等更多功能;
3. JavaScript 插件：可能增强用户体验 , 有一些可以动态交互的功能 , 我们只需要导入插件即可;

### Bootstrap 的目录结构

`bootstrap/`
├── `css/` 全局的CSS样式 , 如果要使用Bootstap增强样式 , 导入这个文件夹
│ ├── `bootstrap.css` 标准版
│ ├── `bootstrap.min.css` 导入这个CSS文件即可 , 压缩版
│ ├── `bootstrap-theme.css`
│ ├── `bootstrap-theme.min.css`
├── `js/` JavaScript插件
│ ├── `bootstrap.js` 标准版
│ └── `bootstrap.min.js` 压缩版 , 导入这个JS文件。功能是一样的
└── `fonts/` 字段图标 , 用于在网页上使用一些小图标
├── `glyphicons-halflings-regular.eot`
├── `glyphicons-halflings-regular.svg`
├── `glyphicons-halflings-regular.ttf`
├── `glyphicons-halflings-regular.woff`
└── `glyphicons-halflings-regular.woff2`

> 压缩版与标准版的区别
>
> + 标准版：代码可读性强 , 有注释;
> + 压缩版：功能是一样的 , 没有注释 , 没有缩进 , 变量名短;

### Bootstrap 导入使用

```HTML
<!-- 1. 导入bootstrap的css样式 -->
<link href="css/bootstrap.min.css" rel="stylesheet">
<!-- 2. 导入jquery框架 -->
<script type="text/javascript" src="js/jquery-3.4.1.min.js"></script>
<!-- 3. 导入bootstrap框架文件 -->
<script type="text/javascript" src="js/bootstrap.min.js"></script>
```

## 栅格系统

### 组成

> Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统 , 随着屏幕或视口(viewport)尺寸的增加 , 系统会自动分为最多12列 , 栅格系统用于通过一系列的行(row)与列(column)的组合来创建页面布局 , 你的内容就可以放入这些创建好的布局中;

Bootstrap 栅格系统的特点：

+ “行(row)” 必须包含在 `.container` (固定宽度)或 `.container-fluid` (100% 宽度)中 , 以便为其赋予合适的 “排列(aligment)” 和 “内间距(padding)” ;
+ 通过“行(row)”在水平方向创建一组 “列(column)” ;
+ 你的内容应当放置于 “列(column)” 内 , 并且 , 只有 “列(column)” 可以作为 “行(row)” 的直接子元素
+ 栅格系统中的列是通过指定1到12的值来表示其跨越的范围;
+ 例如 , 三个等宽的列可以使用三个 `.col-xs-4` 来创建
+ 如果一 “行(row)” 中包含了的 “列(column)” 大于 12 , 多余的 “列(column)” 所在的元素将被作为一个整体另起一行排列;

### 网页布局的两种容器

|两种容器的类样式名|说明|
|:---:|:---|
|`container`|在不同的设备上有不同的固定宽度|
|`container-fluid`|在所有的设备上都显示100%宽度|

### 媒介查@media

> @media 是 CSS3 新增特性，通过不同的媒介类型和条件定义样式表规则;
> 媒介(设备)查询让 CSS 可以更精确作用于不
同的媒介(设备)类型和同一媒介的不同条件;
> 媒介查询的大部分媒介特性都接受 min 和 max 用于表达 “大于或等于” 和 “小于或等于” ;

+ 结论： 通过 `@media` 指令 `container` 容器可以自动适配设备宽度

### 基本写法

|栅格系统|描述|类似于表格
|:---:|:---|:---:|
|`.container` 或 `.containerfluid`|表示两种容器|table
|`.row`|放在容器下一级元素中，表示一行|tr
|`.col-xx-n xx` 有四个取值|表示1格占多少列，每行最多12列 xx：有四个取值，表示不同的设备。 lg大型 md中型 sm小型 xs微型 n表示1格占多少列 如： `.col-sm-3` 表示在小型设备上这一格占3列 `.col-lg-2` 表示在大型设备上这一格占2列|td|

### 栅格的参数

<table class="table table-bordered table-striped"><thead><tr><th></th><th>超小屏幕<small>手机 (&lt;768px)</small></th><th>小屏幕<small>平板 (&ge;768px)</small></th><th>中等屏幕<small>桌面显示器 (&ge;992px)</small></th><th>大屏幕<small>大桌面显示器 (&ge;1200px)</small></th></tr></thead><tbody><tr><th class="text-nowrap" scope="row">栅格系统行为</th><td>总是水平排列</td><td colspan="3">开始是堆叠在一起的，当大于这些阈值时将变为水平排列C</td></tr><tr><th class="text-nowrap" scope="row"><code>.container</code> 最大宽度</th><td>None （自动）</td><td>750px</td><td>970px</td><td>1170px</td></tr><tr><th class="text-nowrap" scope="row">类前缀</th><td><code>.col-xs-</code></td><td><code>.col-sm-</code></td><td><code>.col-md-</code></td><td><code>.col-lg-</code></td></tr><tr><th class="text-nowrap" scope="row">列（column）数</th><td colspan="4">12</td></tr><tr><th class="text-nowrap" scope="row">最大列（column）宽</th><td class="text-muted">自动</td><td>~62px</td><td>~81px</td><td>~97px</td></tr><tr><th class="text-nowrap" scope="row">槽（gutter）宽</th><td colspan="4">30px （每列左右均有 15px）</td></tr><tr><th class="text-nowrap" scope="row">可嵌套</th><td colspan="4">是</td></tr><tr><th class="text-nowrap" scope="row">偏移（Offsets）</th><td colspan="4">是</td></tr><tr><th class="text-nowrap" scope="row">列排序</th><td colspan="4">是</td></tr></tbody></table>

### 栅格系统中类名的小结

|类样式名|作用|
|:---:|:---|
|`.container`|容器，固定宽度容器|
|`.container-fluid`|不同的设备上都是以100%宽度显示|
|`.row`|代表一行|
|`.col-xs-n`|在微型设备上一格占几列|
|`.col-sm-n`|在小型设备上一格占几列|
|`.col-md-n`|在中型设备上一格占几列|
|`.col-lg-n`|在大型设备上一格占几列|
|`.hidden-lg/md/sm/xs`|在某种设备上隐藏|
|`.visible-lg/md/sm/xs`|只在某种设备上显示|

## 全局 CSS 样式

### 按钮

+ 普通按钮

    <h2>按钮组件</h2><a href="#" style="border:1px solid black;border-radius:5px;color:black;background:#fff;margin-right:5px;margin-bottom:10px;" class="btn">我是链接</a><input type="button" value="普通按钮" class="btn" style="border-radius:5px;color:black;background:#fff;border:1px solid black;margin-right:5px;margin-bottom:10px;"><button class="btn btn-default" style="border-radius:5px;color:black;background:#fff;border:1px solid black;margin-bottom:10px;">提交按钮</button><br>

    ```HTML
    <h2>按钮组件</h2>
    <a href="#" class="btn btn-default">我是链接</a>
    <input type="button" value="普通按钮" class="btn btn-default">
    <button class="btn btn-default">提交按钮</button>
    ```

+ 预定义样式的按钮：

    <h2>预定义按钮</h2><a href="#" class="btn btn-primary" style="border:1px solid #0066ff;border-radius:5px;color:#fff;background:#0066ff;margin-right:5px;margin-bottom:10px;" >我是链接</a><input type="button" value="普通按钮" class="btn btn-danger" style="border:1px solid #00aa00;border-radius:5px;color:#fff;background:#00aa00;margin-right:5px;margin-bottom:10px;" ><button class="btn btn-success" style="border:1px solid #00bbff;border-radius:5px;color:#fff;background:#00bbff;margin-right:5px;margin-bottom:10px;" >提交按钮</button>

    ```HTML
    <h2>预定义按钮</h2>
    <a href="#" class="btn btn-primary">我是链接</a>
    <input type="button" value="普通按钮" class="btn btn-danger">
    <button class="btn btn-success">提交按钮</button>
  ```

### 响应式图片

通过为图片添加 `.img-responsive` 类可以让图片支持响应式布局;
如果需要让使用了 `.img-responsive` 类的图片水平居中，请使用 `.center-block` 类;

    ```HTML
    <img src="img/01.jpg" class="img-responsive">
    ```

### 图片形状

|图片形状|类样式名|
|:---:|:---:|
|圆角|img-rounded|
|圆或椭圆|img-circle|
|有边框|img-thumbnail|

<h2>响应式图片</h2><img src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9InllcyI/PjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjE0MCIgdmlld0JveD0iMCAwIDE0MCAxNDAiIHByZXNlcnZlQXNwZWN0UmF0aW89Im5vbmUiPjwhLS0KU291cmNlIFVSTDogaG9sZGVyLmpzLzE0MHgxNDAKQ3JlYXRlZCB3aXRoIEhvbGRlci5qcyAyLjYuMC4KTGVhcm4gbW9yZSBhdCBodHRwOi8vaG9sZGVyanMuY29tCihjKSAyMDEyLTIwMTUgSXZhbiBNYWxvcGluc2t5IC0gaHR0cDovL2ltc2t5LmNvCi0tPjxkZWZzPjxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+PCFbQ0RBVEFbI2hvbGRlcl8xNmIwYmQ1MTE0ZiB0ZXh0IHsgZmlsbDojQUFBQUFBO2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1mYW1pbHk6QXJpYWwsIEhlbHZldGljYSwgT3BlbiBTYW5zLCBzYW5zLXNlcmlmLCBtb25vc3BhY2U7Zm9udC1zaXplOjEwcHQgfSBdXT48L3N0eWxlPjwvZGVmcz48ZyBpZD0iaG9sZGVyXzE2YjBiZDUxMTRmIj48cmVjdCB3aWR0aD0iMTQwIiBoZWlnaHQ9IjE0MCIgZmlsbD0iI0VFRUVFRSIvPjxnPjx0ZXh0IHg9IjQ0LjA1NDY4NzUiIHk9Ijc0LjUiPjE0MHgxNDA8L3RleHQ+PC9nPjwvZz48L3N2Zz4=" class="img-responsive img-rounded" style="border-radius:6px;margin: 0 20px;" alt="140x140"><img src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9InllcyI/PjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjE0MCIgdmlld0JveD0iMCAwIDE0MCAxNDAiIHByZXNlcnZlQXNwZWN0UmF0aW89Im5vbmUiPjwhLS0KU291cmNlIFVSTDogaG9sZGVyLmpzLzE0MHgxNDAKQ3JlYXRlZCB3aXRoIEhvbGRlci5qcyAyLjYuMC4KTGVhcm4gbW9yZSBhdCBodHRwOi8vaG9sZGVyanMuY29tCihjKSAyMDEyLTIwMTUgSXZhbiBNYWxvcGluc2t5IC0gaHR0cDovL2ltc2t5LmNvCi0tPjxkZWZzPjxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+PCFbQ0RBVEFbI2hvbGRlcl8xNmIwYmQ0Zjg1YiB0ZXh0IHsgZmlsbDojQUFBQUFBO2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1mYW1pbHk6QXJpYWwsIEhlbHZldGljYSwgT3BlbiBTYW5zLCBzYW5zLXNlcmlmLCBtb25vc3BhY2U7Zm9udC1zaXplOjEwcHQgfSBdXT48L3N0eWxlPjwvZGVmcz48ZyBpZD0iaG9sZGVyXzE2YjBiZDRmODViIj48cmVjdCB3aWR0aD0iMTQwIiBoZWlnaHQ9IjE0MCIgZmlsbD0iI0VFRUVFRSIvPjxnPjx0ZXh0IHg9IjQ0LjA1NDY4NzUiIHk9Ijc0LjUiPjE0MHgxNDA8L3RleHQ+PC9nPjwvZz48L3N2Zz4=" class="img-responsive img-circle" style="border-radius:50%;margin: 0 20px;" alt="140x140"><img src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9InllcyI/PjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjE0MCIgdmlld0JveD0iMCAwIDE0MCAxNDAiIHByZXNlcnZlQXNwZWN0UmF0aW89Im5vbmUiPjwhLS0KU291cmNlIFVSTDogaG9sZGVyLmpzLzE0MHgxNDAKQ3JlYXRlZCB3aXRoIEhvbGRlci5qcyAyLjYuMC4KTGVhcm4gbW9yZSBhdCBodHRwOi8vaG9sZGVyanMuY29tCihjKSAyMDEyLTIwMTUgSXZhbiBNYWxvcGluc2t5IC0gaHR0cDovL2ltc2t5LmNvCi0tPjxkZWZzPjxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+PCFbQ0RBVEFbI2hvbGRlcl8xNmIwYmQ0OWU5ZSB0ZXh0IHsgZmlsbDojQUFBQUFBO2ZvbnQtd2VpZ2h0OmJvbGQ7Zm9udC1mYW1pbHk6QXJpYWwsIEhlbHZldGljYSwgT3BlbiBTYW5zLCBzYW5zLXNlcmlmLCBtb25vc3BhY2U7Zm9udC1zaXplOjEwcHQgfSBdXT48L3N0eWxlPjwvZGVmcz48ZyBpZD0iaG9sZGVyXzE2YjBiZDQ5ZTllIj48cmVjdCB3aWR0aD0iMTQwIiBoZWlnaHQ9IjE0MCIgZmlsbD0iI0VFRUVFRSIvPjxnPjx0ZXh0IHg9IjQ0LjA1NDY4NzUiIHk9Ijc0LjUiPjE0MHgxNDA8L3RleHQ+PC9nPjwvZz48L3N2Zz4=" class="img-responsive img-thumbnail" style="display: inline-block;max-width: 100%;height: auto;padding: 4px;line-height: 1.42857143;background-color: #fff;border: 1px solid #ddd;border-radius: 4px;-webkit-transition: all .2s ease-in-out;-o-transition: all .2s ease-in-out;transition: all .2s ease-in-out;margin: 0 20px;" alt="140x140"><br>

```HTML
<h2>响应式图片</h2>
<img src="img/01.jpg" class="img-responsive img-rounded"><br>
<img src="img/01.jpg" class="img-responsive img-circle"><br>
<img src="img/01.jpg" class="img-responsive img-thumbnail"><br>
```

### 表单

|样式名|作用|
|:---:|:---|
|`form-control`|`<input>`、`<textarea>` 和 `<select>` 元素都将被默认设置宽度属性为 width: 100%;|
|`form-group`|将 label 元素和前面提到的控件包裹在一行中进行分组|
|`form-inline`|多个表单元素在同一行|

### 表格

+ 与表格有关的类样式

    |类名|表格的样式|
    |:---:|:---|
    |`table`|基本实例：少量的内边距和水平方向的分隔线;
    |`table-striped`|条纹状表格：可以给 `<tbody>` 之内的每一行增加斑马条纹样式;|
    |`table-bordered`|带边框的表格：为表格和其中的每个单元格增加边框;|
    |`table-hover`|鼠标悬停：可以让 `<tbody>` 中的每一行对鼠标悬停状态作出响应;|

+ 表格中的状态类

    |Class|描述|
    |:---:|:---|
    |`active`|鼠标悬停在行或单元格上时所设置的颜色|
    |`success`|标识成功或积极的动作|
    |`info`|标识普通的提示信息或动作|
    |`warning`|标识警告或需要用户注意|
    |`danger`|标识危险或潜在的带来负面影响的动作|

## 组件

### 字体图标

```HTML
<h2>字体图标</h2>
<span class="glyphicon glyphicon-trash"></span> 回收站
<button class="btn btn-default">
<span class="glyphicon glyphicon-zoom-in"></span>
放大镜
</button>
<span class="glyphicon glyphicon-camera"></span> 照相机
```

### 导航条

+ 作用
    > 导航条：您的应用或网站中作为导航页头的响应式基础组件;
    > 它们在移动设备上可以折叠（并且可开可关），且在视口（viewport）宽度增加时逐渐变为水平展开模式;

+ 组成
  + 整个导航条就是一个nav标签，nav与div功能相同，它是一个语义标签

    |导航条的类样式|描述|
    |:---:|:---|
    |`navbar` `navbar-default`|指定为导航条，并设置为默认的颜色白色|
    |`navbar-header`|指定最左边商标和开关按钮的样式，它在手机上有更好的显示|
    |`collapse` `navbar-collapse`|可以折叠的所有项：包括链接、表单、下拉菜单等|
    |`dropdown`|下拉菜单|
    |`navbar-left`|元素在导航条中左对齐|
    |`navbar-right`|元素在导航条中右对齐|
    |`navbar-inverse`|将颜色反转，其实就是设置成黑色|

  + 相关属性

    |相关的属性|说明|
    |:---:|:---|
    |`data-开头`|表示这有一个激活的事件，会激活相应的功能，不能删除|
    |`aria-开头`|给残障人士使用的功能，通常可以删除|
    |`sr-only`|屏幕阅读的功能，也是给残障人士使用，可以删除|

### 略缩图

+ 作用
    > 扩展 Bootstrap 的 栅格系统，可以很容易地展示栅格样式的图像、视频、文本等内容;

    |缩略图的类样式|说明|
    |:---:|:---|
    |`thumbnail`|将元素设置成缩略图，内部可以包含图片、文字等其它元素，这个缩略图放置在div栅格布局的容器中|
    |`caption`|缩略图中的标题|

## JavaScript 插件

> 注：Javascript插件必须要使用到jQuery框架

### 轮播图

这个组件用于轮播显示一组图片，类似于旋转木马，页面加载就自动运行，也可以通过点击左右的两个箭头向左或向右翻页;

+ 组成的类样式名

    |类样式名字|描述|
    |:---:|:---|
    |`carousel` `slide`|轮播图的容器|
    |`carousel-indicators`|中间的小白色圆点，每个圆点都可以点击，显示指定的图片|
    |`carousel-inner`|要轮播的图片，每张图片用一个div包裹|
    |`carousel-caption`|图片上显示的名字|
    |`carousel-control`|向左向右的控制按钮|

+ 相关的属性

    |属性名|作用|
    |:---:|:---|
    |`data-ride="carousel"`|指定当前是一个轮播图，加载时自动运行|
    |`data-interval="2000"`|间隔的时间间隔，单位是毫秒|
    |`data-target="#myPic"`|指定轮播图div容器的id值|
