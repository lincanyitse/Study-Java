# JavaScript 进阶

## 操作CSS样式

### js与css属性命名上的区别

|CSS中写法|JS中的写法|说明|
|:---:|:---:|:---|
|color|color|如果样式名只有一个单词 , 写法相同|
|font-size|fontSize|如果有多个单词 , 去掉单词之间短横 , 并且使用驼峰命名法|

### js修改css样式

方式一：

```JAVASCRIPT
元素.style.样式名=样式值 //每条语句只能修改一个样式
```

方式二：

```JAVASCRIPT
元素.className="类名" //先创建好一个类样式 , 直接给这个元素设置一个类的属性 , 一条语句可以修改多个样式
```

## 正则对象

> 可以用来匹配或查找某个字符 , 如果字符串与指定的表达式匹配 , 返回true , 如果不匹配返回false;

### 规则

|符号|作用|
|:---:|:---|
|`[a-z]`|[] 表示一个字符 , - 表示一个区间。a到z之间的任何一个字符
|`[xyz]`|x或y或z , 三个中间的一个字符|
|`[\^xyz]`|在`[]`里面`\^` , 表示取反 , 除了`xyz`之外的字符|
|`\d`|代表数字|
|`\w`|代表单词 , 包含以下字符：`a-zA-Z0-9_`|
|`.`|代表任意字符 , 如果要使用匹配点号 , 要转义`\.`|
|`()`|`()`代表一个分组|
|`{n}`|前面的字符出现n次|
|`{n,}`|前面的字符出现大于等于n次|
|`{n,m}`|前面的字符出现n到m之间的次数 , 包头又包尾|
|`+`|前面的字符出现1~n次 , 或者说至少出现一次|
|`*`|前面的字符出现0~n次 , 或者说有可能出现一次或多次|
|`?`|前面的字符出现0~1次 , 或者说有可能出现|
|`|`|或|
|`\^`|出现在开头 , 表示必须匹配这个头|
|`$`|出现结尾 , 表示必须匹配这个结尾。|

### 正则表达式的使用

表达式举例

|正则表达式|匹配字符串|
|:---:|:---|
|`\d{3}`|包含3个数字即可：a123b|
|`\^\d{3}`|以3个数字开头：123b|
|`\d{3}$`|以3个数字结尾：a123|
|`\^\d{3}$`|必须是3个数字：123|
|`[a-d]`|小写的a到d中的一个字符 , 中括号表示匹配1个字符|
|`[xyz]`|x或y或z|
|`ab{2}`|a后面出现2次b：abb|
|`ab{2,}`|a后面出现2次及以上的b：abb或abbb或abbbb|
|`ab{3,5}`|a后面出现3~5次b：abbb或abbbb或abbbbb|
|`ab+`|a后面出现1~n次b：ab或abb或abbb|
|`ab*`|a后面出现0~n次b：a或ab或 abbb|
|`ab?`|a后面出现0~1次b：a或ab|
|`hi|hello`|字符串里有hi或者hello|
|`(b|cd)ef`|表示bef或cdef|
|`\^.{3}$`|表示有任意三个字符的字符串|
|`[\^a-zA-Z]`|中括号内部的`\^` , 表示不出现 , 即不出现：大小写字母|

使用正则表达式

+ 方式一

    ```JAVASCRIPT
    var 变量名 = new RegExp("正则表达式")
    document.write(变量名.test(字符串));
    ```

+ 方式二

    ```JAVASCRIPT
    var 变量名 = /正则表达式/
    document.write(变量名.test(字符串));
    ```

> 注：
>
> 1. 正则表达式是写在一个字符串中 , `\`符号需要转义 , 字符串可以定义成一个变量 , 灵活一些。
> 2. 固定的写法 , 就是正则表达式 , `\`不需要转义

+ 匹配模式

  + 方式一的匹配模式
  
    ```JAVASCRIPT
        var 变量名 = new RegExp("正则表达式", "匹配模式");
    ```

  + 方式二的匹配模式

    ```JAVASCRIPT
        var 变量名 = /正则表达式/匹配模式;
    ```

### 常用方法

|JS中正则表达式的方法|说明|
|:---:|:---|
|boolean test("字符串")|作用： 判断正则表达式是否与参数字符串匹配 参数：需要匹配的字符串 返回：匹配返回true，否则返回false|

## 日期对象

### 创建Date对象

```JAVASCRIPT
var 变量名 = new Date() // 创建一个当前的时间和日期对象
```

### 方法

|方法名|作用|
|:---:|:---|
|getFullYear()|从 Date 对象以四位数字返回年份|
|getMonth()|从 Date 对象返回月份 (0 ~ 11)|
|getDate()|从 Date 对象返回一个月中的某一天 (1 ~ 31)|
|getDay()|从 Date 对象返回一周中的某一天 (0 ~ 6) , 其中：0表示周日，1~6周一到周六|
|getHours()|返回 Date 对象的小时 (0 ~ 23)|
|getMinutes()|返回 Date 对象的分钟 (0 ~ 59)|
|getSeconds()|返回 Date 对象的秒数 (0 ~ 59)|
|getMilliseconds()|返回 Date 对象的毫秒(0 ~ 999)|
|getTime()|返回 1970 年 1 月 1 日至今的毫秒数 , 类似于Java中的System.currentTimeMillis()|
|toLocaleString()|根据本地时间格式，把 Date 对象转换为字符串|

## BOM编程

### 作用

> 对浏览器中的各种对象进行操作

### 常用对象

|BOM常用对象|作用|
|:---:|:---|
|window|表示浏览器窗体对象|
|location|浏览器地址栏对象|
|history|访问历史记录对象|

+ location 对象
    > 用于页面跳转
  + 常用属性

    |href属性|作用|
    |:---:|:---|
    |获取href属性|得到当前浏览器访问地址|
    |设置href属性|就可以进行页面跳转，跳转到新的页面|

  + 常用方法

    |location的方法|描述|
    |:---:|:---|
    |reload()|重新加载当前页面，相当于刷新功能|
  
+ history 对象
    > 代表浏览器访问过的历史记录，可以通过这个对象访问之前访问过的页面

  + 方法

    |方法|作用|
    |:---:|:---|
    |forward()|相当浏览器上前进按钮|
    |back()|相当于浏览器上后退按钮|
    |go(正数或负数)|正数相当于前进，负数相当于后退。1前进或后退1个页面|

+ window 对象
    > 注：没有应用于 window 对象的公开标准，不过所有浏览器都支持该对象
  + 属性

    |属性|描述|
    |:---:|:---|
    |closed|返回窗口是否已被关闭|
    |defaultStatus|设置或返回窗口状态栏中的默认文本|
    |document|对 Document 对象的只读引用。(请参阅对象)|
    |frames|返回窗口中所有命名的框架。该集合是 Window 对象的数组，每个 Window 对象在窗口中含有一个框架|
    |history|对 History 对象的只读引用。请参数 History 对象|
    |innerHeight|返回窗口的文档显示区的高度|
    |innerWidth|返回窗口的文档显示区的宽度|
    |localStorage|在浏览器中存储 key/value 对。没有过期时间|
    |length|设置或返回窗口中的框架数量|
    |location|用于窗口或框架的 Location 对象。请参阅 Location 对象|
    |name|设置或返回窗口的名称|
    |navigator|对 Navigator 对象的只读引用。请参数 Navigator 对象|
    |opener|返回对创建此窗口的窗口的引用|
    |outerHeight|返回窗口的外部高度，包含工具条与滚动条|
    |outerWidth|返回窗口的外部宽度，包含工具条与滚动条|
    |pageXOffset|设置或返回当前页面相对于窗口显示区左上角的 X 位置|
    |pageYOffset|设置或返回当前页面相对于窗口显示区左上角的 Y 位置|
    |parent|返回父窗口|
    |screen|对 Screen 对象的只读引用。请参数 Screen 对象|
    |screenLeft|返回相对于屏幕窗口的x坐标|
    |screenTop|返回相对于屏幕窗口的y坐标|
    |screenX|返回相对于屏幕窗口的x坐标|
    |sessionStorage|在浏览器中存储 key/value 对; 在关闭窗口或标签页之后将会删除这些数据|
    |screenY|返回相对于屏幕窗口的y坐标|
    |self|返回对当前窗口的引用。等价于 Window 属性|
    |status|设置窗口状态栏的文本|
    |top|返回最顶层的父窗口|
  
  + 方法

    |方法|描述|
    |:---:|:---|
    |alert()|显示带有一段消息和一个确认按钮的警告框|
    |atob()|解码一个 base-64 编码的字符串|
    |btoa()|创建一个 base-64 编码的字符串|
    |blur()|把键盘焦点从顶层窗口移开|
    |clearInterval()|取消由 setInterval() 设置的 timeout|
    |clearTimeout()|取消由 setTimeout() 方法设置的 timeout|
    |close()|关闭浏览器窗口|
    |confirm()|显示带有一段消息以及确认按钮和取消按钮的对话框|
    |createPopup()|创建一个 pop-up 窗口|
    |focus()|把键盘焦点给予一个窗口|
    |getSelection()|返回一个 Selection 对象，表示用户选择的文本范围或光标的当前位置|
    |getComputedStyle()|获取指定元素的 CSS 样式|
    |matchMedia()|该方法用来检查 media query 语句，它返回一个 MediaQueryList对象|
    |moveBy()|可相对窗口的当前坐标把它移动指定的像素|
    |moveTo()|把窗口的左上角移动到一个指定的坐标|
    |open()|打开一个新的浏览器窗口或查找一个已命名的窗口|
    |print()|打印当前窗口的内容|
    |prompt()|显示可提示用户输入的对话框|
    |resizeBy()|按照指定的像素调整窗口的大小|
    |resizeTo()|把窗口的大小调整到指定的宽度和高度|
    |scroll()|已废弃。 该方法已经使用了 scrollTo() 方法来替代|
    |scrollBy()|按照指定的像素值来滚动内容|
    |scrollTo()|把内容滚动到指定的坐标|
    |setInterval()|按照指定的周期（以毫秒计）来调用函数或计算表达式|
    |setTimeout()|在指定的毫秒数后调用函数或计算表达式|
    |stop()|停止页面载入|

## DOM编程

### 概述

+ 概念
    > Document Object Model 文档对象模型，整个网页就是一个文档对象，可以dom来操作网页中所有的标签元素;

+ 作用
    > + 通过 DOM模型，可以访问所有的 HTML 元素，连同它们所包含的文本和属性;
    > + 可以对其中的内容进行修改和删除，同时也可以创建新的元素;
    > + 新创建的元素对象，要挂到DOM树上才可以在网页上显示出来

### 节点

+ 查找节点
  + 查找方法

    |获取元素的方法|作用|
    |:---:|:---|
    |document.getElementById("id")|通过id得到唯一元素|
    |document.getElementsByName("name")|通过标签的name属性得到一组名字相同的元素|
    |document.getElementsByTagName ("标签名")|通过标签的名字得到一组相同的标签，如：input|
    |document.getElementsByClassName("类名")|通过标签class类名属性，得到一组标签

### DOM树

+ 创建元素

    ```JAVASCRIPT
    // 创建一个元素 参数：标签名字
    document.createElement("标签名")
    ```

+ 修改BOM树

    |将元素挂到DOM树上的方法|作用|
    |:---:|:---|
    |父元素.appendChild(子元素)|父元素是DOM树中已经存在元素 子元素是新创建的元素，把创建好的子元素挂到DOM树上，做为父元素的子元素|
    |父元素.removeChild(子元素)|将DOM树上某个元素的子元素删除|
    |元素.remove()|自己删除本身这个元素|

+ 通过关系找节点

    |遍历节点的属性|说明|
    |:---:|:---|
    |childNodes|返回当前元素所有的子元素|
    |firstChild|得到当前元素的第1个子节点|
    |lastChild|得到当前元素的最后1个子节点|
    |parentNode|得到当前元素的父节点|
    |nextSibling|得到当前元素的下一个兄弟节点|
    |previousSibling|得到当前元素的上一个兄弟节点|

---
[上一章](Day34.md) [目录](SUMMARY.md) [下一章](Day36.md)