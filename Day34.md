# JavaScript

## 介绍

---

### 作用

> HTML网页运行在浏览器端 , 与用户没有交互功能 , JavaScript就是可以让程序运行在网页上 , 提高客户访问网页时体验

### JavaScript与Java的区别

|特点|Java|JavaScript|
|:---:|:---|:---|
|面向对象|完全面向对象语言|基于对象 , 不完全面向对象|
|运行方式|编译型的语言 , 生成中间的文件class|解释型语言 , 不会生成中间 , 直接运行浏览器|
|跨平台|Java可以运行在不同系统上 , 安装虚拟机|运行浏览器上 , 只要操作系统有浏览器就可以执行|
|数据类型|强类型的语言 String str = 35; //错误|弱类型语言 , 同一个变量可以赋值为不同的数据类型 var str ="abc"; str = 35; //对|

### 基础语法

+ 组成
    |组成部分|作用|
    |:---:|:---|
    |ECMA|Script 这是一种脚本语言规范 , 构成了JavaScript的核心语法基础。 如：定义变量 , 控制结构|
    |BOM|Browser Object Model 浏览器对象模型 , 操作浏览器中的各种对象。如：window|
    |DOM|Document Object Model 文档对象模型 , 操作网页中标签元素。如：input, span|

+ 代码位置
    1. 放在HTML文件中
    2. 放在HTML文件名 , 单独的js文件存在 , 使用的时候需要导入

+ script 标签
    > 外部导入js文件

    ```JAVASCRIPT
    <script type="text/javascript" src="js/out.js"></script>
    // src：导入外部文件地址
    // type：可选 , 指定脚本的类型
    ```

    > 内部使用

    ```JAVASCRIPT
    <script type="text/javascript">
        // 代码内容...
    </script>
    ```

    > 注:
    > 1. 在一个网页可以同时出现多个标签 , 每个标签会依次执行;
    > 2. 可以出现在任意的位置 , 甚至出现在html标签外面 , 建议放在body或head中;
    > 3. 每行JS代码以分号结束 , 如果一条语句一行代码 , 分号可以省略;
    > 4. 保存JS指定为UTF-8的编码 , 与网页的编码一致;

+ 注释

    |语言|注释语法|
    |:---:|:---|
    |HTML|$\color{#0c8918}{<!-- 注释 -->}$|
    |CSS|$\color{#0c8918}{/* 注释 */}$|
    |JavaScript|$\color{#0c8918}{// 单行注释 /* 多行注释 */}$|

+ 变量

  + 定义

    |数据类型|Java中定义变量|JS中定义变量|
    |:---:|:---:|:---:|
    |整数|int i = 5;|var i = 5;|
    |浮点数|float f = 3.14; 或 double d=3.14;|var f = 3.14; 或 var d=3.14;|
    |布尔|boolean b = true;|var b = true;|
    |字符|char c = 'a';|var c = 'a';|
    |字符串|String str = "abc";|var str = "abc";|

    > 注：
    > + 什么是弱类型：定义一个变量可以赋值为不同的数据类型;
    > + 字符和字符串类型：没有字符串和字符之分 , 都叫字符串类型 , 既可以使用双引号又可以使用单引号;

  + 特点

    1. var关键字可以省略 , 建议加上;
    2. 变量可以重复定义：var a = 5; var a="abc";
    3. 在Java大括号变量的作用范围 , 在JS中不受这个限制;

+ 数据类型

    |关键字|说明|
    |:---:|:---|
    |number|数值型：包括整数浮点数|
    |boolean|布尔类型：true / false|
    |string|字符串：包含字符和字符串 , 可以使用双引号或单引号|
    |object|对象类型：JS内置对象或自定义对象|
    |undefined|未初始化 , 未知类型|

  + typeof操作符
    1. 作用： 用于判断某个变量数据类型 , 返回这种数据类型的名字
    2. 写法：typeof 变量名 或 typeof(变量名)

  |null与undefined的区别|说明|
  |:---:|:---|
  |null|是object对象类型 , 只是这个对象没有值|
  |undefined|变量未赋值 , 不知道它是什么类型|

  + 字符串转换成数字类型

    |转换函数|作用|
    |:---:|:---|
    |parseInt(变量)|将一个字符串类型的数字转成整数类型 , 如果转换失败 , 返回NaN = Not a Number 不是一个数字 , 将数字开头可以转一部分;|
    |parseFloat(变量)|将一个字符串类型的数字转成浮点数 , 如果转换失败 , 返回NaN|
    |isNaN(变量)|非数字返回true , 数字返回false。isNaN = is not a number 如："abc"返回true , "123abc"返回true, "123"返回false|

+ 流程控制语句

  + if判断
    > if ...

    ```JAVASCRIPT
    if(条件表达式) {
        // 代码块;
    }
    ```

    > if ... else ...

    ```JAVASCRIPT
    if(条件表达式) {
        // 表达式成立代码块;
    } else {
        // 表达式不成立代码块
    }
    ```

    > if ... else if ... else ...

    ```JAVASCRIPT
    if(条件表达式1) {
        // 表达式1成立代码块;
    } else if (条件表达式2) {
        // 表达式2成立代码块;
    } else {
        // 表达式1与表达式2都不成立代码块
    }
    ```

  > 注：条件判断可以使用非逻辑运算符

  |数据类型|为真|为假|
  |:---:|:---:|:---:|
  |number|1|0|
  |string|非空串|空串：""|
  |undefined||为假|
  |NaN(Not a Number)||为假|
  |object|非空|null|

  + swtich多分支
    > case后使用变量 , 与Java相同

    ```JAVASCRIPT
    switch(变量名) {
    case 常量值:
        break;
    case 常量值:
        break;
    default:
        break;
    }
    ```

    > case后使用表达式

    ```JAVASCRIPT
    switch(true) {
    case 表达式:
        break;
    case 表达式:
        break;
    default:
        break;
    }
    ```

  > 小知识：
  >
  > |window对象的方法名|作用|
  > |:---:|:---|
  > |string prompt("提示信息","默认值”)|在浏览器上出现一个输入框 参数1：提示信息 参数2：默认出现在输入框中的值 返回：字符串|
  > |alert("提示信息")|在浏览器上弹出一个信息框 , 只有一个确定按钮|
  >
  > 注：只要是window对象的方法 , 都可以省略window对象

+ 循环

  + while语句

    ```JAVASCRIPT
    while (条件表达式) {
        // 需要执行的代码;
    }
    ```

  + do-while语句

    ```JAVASCRIPT
    do {
        // 需要执行的代码;
    }
    while (条件表达式)
    ```

  + for 语句

    ```JAVASCRIPT
    for (var i=0; i<10; i++) {
        //需要执行的代码;
    }
    ```

  + break 和 continue
    + break: 结束整个循环
    + continue：跳过本次循环 , 执行下一次循环

+ 函数

  + 定义
    > 与Java中的方法类似。函数的关键字：function
    > 两种定义方式：
    > 1. 命名函数
    > 2. 匿名函数

  + 格式

    ```JAVASCRIPT
    function 函数名(参数列表) {
        // 代码块;
        [return 返回值]
    }
    ```

  + 注意的事项
    1. 形参的类型不能写 , 因为是弱类型 , 不用指定它的类型;
    2. 函数的返回值： 如果函数有返回值 , 加上return , 如果没有返回值 , 不写return;
    3. 关于函数的重载：在JS中没有函数的重载 , 后面定义的同名函数会覆盖前面的函数 , 与参数的个数无关;
    4. 隐藏数组：在每个函数的内部都有一个隐藏的数组 , 名字叫：arguments;

  + 隐藏数组的执行过程

    ```flow
    op1=>operation: "sum 2,3,4"
    op2=>operation: "function sum(a,b) {
        arguments[0]=2;
        arguments[1]=3;
        arguments[2]=4;
        }"
    op3=>operation: "执行的时候从arguments数组中取出值
    a=arguments[0];b=arguments[1];
    alter(a+b);"
    op1(right)->op2(right)->op3(right)
    ```

  + 匿名函数

    + 语法

        ```JAVASCRIPT
        var 变量名 = function(参数列表) {
            //代码块
            [return 返回值];
        }
        ```

    + 使用

        ```JAVASCRIPT
        变量名(参数列表)
        ```

### 事件

+ 概述
    > 网页上存在各种表单元素 , 每个元素会进行：点击 , 双击 , 失去焦点等操作 , 我们可以针对这些操作进行编程 , 在不同的操作中产生不同的效果;

+ 设置事件

  + 方式一：命名函数

    ```HTML
    <input type="button" onclick="被调用的函数()" >
    <!-- 当点击button的时候 , 调用指定的函数 -->
    ```

  + 方式二：匿名函数

    ```JAVASCRIPT
    得到元素对象.onclick = function() {
        // 代码
    }
    // 点击指定的对象 , 运行function中的代码
    ```

+ 常用事件

  + 加载完成事件
    > onload 元素或网页加载完毕以后运行

    ```JAVASCRIPT
    windows.onload = function () {
        // 代码内容
    }

    ```

  + 鼠标点击
    > onclick 单击事件

    ```JAVASCRIPT
    得到元素对象.onclick = function() {
        // 代码
    }
    ```

    > ondblclick 双击事件

    ```JAVASCRIPT
    得到元素对象.ondblclick = function() {
        // 代码
    }
    ```

  + 鼠标移动
    > onmouseover 鼠标移到某个元素的上面

    ```JAVASCRIPT
    得到元素对象.onmouseover = function() {
        // 代码
    }
    ```

    > onmouseout 鼠标移出某个元素

    ```JAVASCRIPT
    得到元素对象.onmouseout = function() {
        // 代码
    }
    ```
  
  + this关键字
    > 获取当前对象的属性

    ```JAVASCRIPT
    得到元素对象.onclick = function() {
        // 代码
        alert(this)
    }
    ```

    > 在html中作为参数

    ```HTML
    <input type="button" value="按钮1" id="b1" onclick="clickMe(this)">
    <script>
        //命名函数的调用方式
        function clickMe(obj) {
            alert(obj); //按钮对象
        }
    </script>
    ```

  + 焦点相关
    > 如果某个网页元素得到了光标 , 处于一种可以操作状态 , 得到焦点
    > onblur：失去焦点

    ```JAVASCRIPT
    得到元素对象.onblur = function() {
        // 代码
    }
    ```

    > onfocus: 得到焦点

    ```JAVASCRIPT
    得到元素对象.onfocus = function() {
        // 代码
    }
    ```

  + 改变事件
    > onchange ：某个元素的内容或选项发生变化的事件 , 文本框必须在失去焦点以后才会激活这个事件

    ```JAVASCRIPT
    得到元素对象.onchange = function() {
        // 代码
    }
    ```

  + 键盘相关

    > onkeyup: 松开按键

    ```JAVASCRIPT
    得到元素对象.onkeyup = function() {
        // 代码
    }
    ```

    > onkeydown： 按下按键

    ```JAVASCRIPT
    得到元素对象.onkeydown = function() {
        // 代码
    }
    ```

    + 键盘码

        > 大键盘

        |按键|键码|按键|键码|按键|键码|按键|键码|
        |:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
        |A|65|J|74|S|83|1|49|
        |B|66|K|75|T|84|2|50|
        |C|67|L|76|U|85|3|51|
        |D|68|M|77|V|86|4|52|
        |E|69|N|78|W|87|5|53|
        |F|70|O|79|X|88|6|54|
        |G|71|P|80|Y|89|7|55|
        |H|72|Q|81|Z|90|8|56|
        |I|73|R|82|0|48|9|57|

        > 小键盘

        |按键|键码|按键|键码|
        |:--:|:--:|:--:|:--:|
        |0|96|8|104|
        |1|97|9|105|
        |2|98|*|106|
        |3|99|+|107|
        |4|100|Enter|108|
        |5|101|-|109|
        |6|102|.|110|
        |7|103|/|111|

        > 功能键

        |按键|键码|按键|键码|
        |:--:|:--:|:--:|:--:|
        |F1|112|F7|118|
        |F2|113|F8|119|
        |F3|114|F9|120|
        |F4|115|F10|121|
        |F5|116|F11|122|
        |F6|117|F12|123|

        > 控制键

        |按键|键码|按键|键码|按键|键码|按键|键码|
        |:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
        |BackSpace|8|ESC|27|Right Arrow|39|`-_`|189|
        |Tab|9|Spacebar|32|Dw Arrow|40|`.>`|190|
        |Clear|12|Page Up|33|Insert|45|`/?`|191|
        |Enter|13|page Down|34|Delete|56|`~|192|
        |Shift|16|End|35|Num Lock|144|`[{`|219|
        |Control|17|Home|36|`:;`|186|`\|`|220|
        |Alt|18|Left Arrow|37|`=+`|187|`]}`|221|
        |Cape Lock|20|Up Arrow|38|`,<`|188|`'"`|222|
  + 小结

    |事件名|作用|
    |:---:|:---:|
    |onclick|单击|
    |ondblclick|双击|
    |onload|加载完毕|
    |onfocus|得到焦点|
    |onblur|失去焦点|
    |onchange|改变事件|
    |onmouseover|鼠标移上|
    |onmouseout|鼠标移出|
    |onkeyup|松开键盘按键|
    |onkeydown|按下按键|
    |onsubmit|表单提交事件|

### 内置对象

+ 数组对象
  + 创建方式
  
    |创建数组的方式|说明|
    |:---:|:---|
    |new Array()|创建一个长度为0的数组|
    |new Array(5)|创建一个指定长度的数组|
    |new Array(2,4,10,6,41)|指定数组中每个元素 , 创建数组|
    |[4,3,20,6]|指定数组中每个元素 , 创建数组|
  
  + 特点
    1. 数组中每个元素的类型是可以不同的。
    2. JS数组长度是可以动态变化
    3. 数组中包含各种方法

  + 常用方法

    |方法名|功能|
    |:---:|:---|
    |concat()|用于拼接一个或多个数组 , 返回拼接好的数组|
    |reverse()|用于数组的反转|
    |join(separator)|将一个数组通过分隔符 , 拼接成一个字符串。功能与java中split函数相反|
    |sort()|对字符串数组进行排序 如果要对数字进行排序 , 要指定比较器函数 , sort(function(m,n))数字两两比较 1) 如果m大于n , 则返回正整数 2) 如果m小于n , 则返回负整数 3) 如果m等于n , 则返回0|

---
[上一章](Day33.md) [目录](SUMMARY.md) [下一章](Day34.md)