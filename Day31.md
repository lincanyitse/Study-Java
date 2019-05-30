# HTML5

## 简介

---

+ 开发工具

  + 浏览器 ：渲染HTML代码展示网页的工具;

  + 编辑器 ：编辑HTML代码;

+ web标准

    > 好处：
    1. 让Web的发展前景更广阔
    2. 内容能被更广泛的设备访问
    3. 更容易被搜寻引擎搜索
    4. 降低网站流量费用
    5. 使网站更易于维护
    6. 提高页面浏览速度

    > 构成：
  + 结构（Structure）：结构用于对网页元素进行整理和分类 , 咱们主要学的是HTML;
  + 表现（Presentation）：表现用于设置网页元素的版式、颜色、大小等外观样式 , 主要指的是CSS;
  + 行为（Behavior）：行为是指网页模型的定义及交互的编写 , 咱们主要学的是 `Javascript` ;

+ 什么是HTML

  + HTML 是用来描述网页的一种语言。
  + HTML 指的是超文本标记语言: HyperText Markup Language
  + HTML 不是一种编程语言 , 而是一种标记语言
  + 标记语言是一套标记标签 (markup tag)
  + HTML 使用标记标签来描述网页
  + HTML 文档包含了HTML 标签及文本内容
  + HTML文档也叫做 web 页面

+ HTML 标签
    > HTML 标记标签通常被称为 HTML 标签 (HTML tag)。

  + HTML 标签是由尖括号包围的关键词 , 比如 `<html>`

  + HTML 标签通常是成对出现的 , 比如 `<b>` 和 `</b>`, 也有单标签, 比如 `<br>` 和 `<img>`

  + 标签对中的第一个标签是开始标签 , 第二个标签是结束标签

  + 开始和结束标签也被称为开放标签和闭合标签

  + 标签关系分两种：一种嵌套关系, 比如 `<html><head></head></html>` ; 另一种并列关系, 比如 `<head></head><body></body>`
  + html 5 需要在html文档的头部使用 `<!DOCTYPY html>` 来声明使用的是html 5版本
  + 所谓标签语义化 , 就是指标签的含义
        > 语义化的好处
        > 1. 方便代码的阅读和维护
        > 2. 同时让浏览器或是网络爬虫可以很好地解析 , 从而更好分析其中的内容
        > 3. 使用语义化标签会具有更好地搜索引擎优化
        >
        > 核心：合适的地方给一个最为合理的标签;  
        >
        > 语义是否良好： 当我们去掉CSS之后 , 网页结构依然组织有序 , 并且有良好的可读性
        >
        > 遵循的原则：先确定语义的HTML  , 再选合适的CSS。

+ 常用标签
  + `<head></head>` ：头部区域;
  + `<title></title>` ：网页的标题;
  + `<hn></hn>` ：内容的标题, n是数字, n的范围[1-6];
  + `<p></p>` ：内容的段落;
  + `<hr>` ：水平线;
  + `<br>` ：换行;
  + `<span></span>` ：内联元素, 一般用作文本容器;
  + `<div></div>` ：区块元素, 定义了文档的区域;
  + |标签|显示效果|
      |:---:|:---:|
      |`<b></b>和<strong></strong>`|文字以粗体方式显示(xhtml 推荐使用strong)|
      |`<i></i>和<em></em>`|文字以斜体方式显示(xhtml 推荐使用em)|
      |`<s></s>和<del></del>`|文字以加删除线方式显示(xhtml 推荐使用del)|
      |`<u></u>和<ins></ins>`|文字以加下划线方式显示(xhtml 不赞成使用u)|
    + `<img>` : 显示图片, `src`指定图片路径, `alt` 设置文件不存在时显示的内容, `title` 设置鼠标悬停显示的内容;
    + `<a></a>` ：超链接, `href`指定链接目标地址, `target` 指定链接页面的打开方式, 其取值有self和blank两种 , 其中self为默认值 , blank为在新窗口中打开方式;
    + `<base>` ：设置整个文档超链接的打开方式;
    + `<!-- 注释内容 -->` ：html的注释
    + |特殊字符|描述|字符的代码|
      |:---:|:---:|:---:|
      |&nbsp;|空格符|`&nbsp;`|
      |&lt;|小于号|`&lt;`|
      |&gt;|大于号|`&gt;`|
      |&amp;|和号|`&amp;`|
      |&yen;|人民币|`&yen;`|
      |&copy;|版权|`&copy;`|
      |&reg;|注册商标|`&reg;`|
      |&deg;|摄氏度|`&deg;`|
      |&plusmn;|正负号|`&plusmn;`|
      |&times;|乘号|`&times;`|
      |&divide;|除号|`&divide;`|
      |&sup2;|平方2(上标2)|`&sup2;`|
      |&sup3;|立方3(上标3)|`&sup3;`|

  + 无序列表

    ```HTML
    <ul>
        <li>列表项1</li>
        <li>列表项2</li>
        <li>列表项3</li>
        ......
    </ul>
    ```

    > 注：
    > 1. `<ul></ul>`中只能嵌套`<li></li>` , 直接在`<ul></ul>`标签中输入其他标签或者文字的做法是不被允许的。
    > 2. `<li>`与`</li>`之间相当于一个容器 , 可以容纳所有元素。
    > 3. 无序列表会带有自己样式属性 , 放下那个样式 , 一会让CSS来！

  + 有序列表

    ```HTML
    <ol>
        <li>列表项1</li>
        <li>列表项2</li>
        <li>列表项3</li>
        ......
    </ol>
    ```

    > 注：与无序列表的区别是有序列表带序号

  + 自定义列表
    > 定义列表常用于对术语或名词进行解释和描述 , 定义列表的列表项前没有任何项目符号

    ```HTML
    <dl>
        <dt>名词1</dt>
        <dd>名词1解释1</dd>
        <dd>名词1解释2</dd>
        ...
        <dt>名词2</dt>
        <dd>名词2解释1</dd>
        <dd>名词2解释2</dd>
        ...
    </dl>
    ```

  + 表格

    ```HTML
    <table>
        <caption>我是表格标题</caption>
        <thead>
            <tr>
                <th>单元格的表头</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>单元格内的文字</td>
            ...
            </tr>
            ...
        </tbody>
    </table>
    ```

    > 代码解析:
    > 在使用表格进行布局时 , 可以将表格划分为头部、主体和页脚（页脚因为有兼容性问题 , 我们不在赘述） , 具体 如下所示：
    > + `<thead></thead>`：用于定义表格的头部 , 必须位于`<table></table>` 标签中 , 一般包含网页的logo和导航等头部信息;
    > + `<tbody></tbody>`：用于定义表格的主体。位于`<table></table>`标签中 , 一般包含网页中除头部和底部之外的其他内容。
    > + `<caption></caption>`：用于定义表格的标题, 每个表格只能定义一个标题;

  + `<input>` ：标签为单标签 , 其常用属性如下表所示：
    <table><thead><tr><th>属性</th><th>属性值</th><th>描述</th></tr></thead><tbody><tr><td rowspan="9">type</td><td>text</td><td>单行文本输入框</td></tr><tr><td>password</td><td>密码输入框</td></tr><tr><td>radio</td><td>单选按钮</td></tr><tr><td>checkbox</td><td>复选框</td></tr><tr><td>button</td><td>普通按钮</td></tr><tr><td>submit</td><td>提交按钮</td></tr><tr><td>reset</td><td>重置按钮</td></tr><tr><td>image</td><td>图像形式的提交按钮</td></tr><tr><td>file</td><td>文件域</td></tr><tr><td>name</td><td>由用户自定义</td><td>控件的名称</td></tr><tr><td>value</td><td>由用户自定义</td><td>默认文本值</td></tr><tr><td>size</td><td>正整数</td><td>input控件在页面中显示宽度</td></tr><tr><td>checked</td><td>checked</td><td>定义复选框的默认被选中项</td></tr><tr><td>maxlength</td><td>正整数</td><td>控件允许输入的最长字符数</td></tr></tbody></table>
  + `<label></label>` ：用于绑定一个表单元素, 当点击label标签的时候, 被绑定的表单元素就会获得输入焦点 , 绑定元素：

    ```HTML
    <label for="male">Male</label>
    <input type="radio" name="sex" id="male" value="male">
    ```

  + `<textarea></textarea>` ：多行文本输入框;
  + 下拉菜单

    ```HTML
    <select>
        <option>选项1</option>
        <option>选项2</option>
        <option>选项3</option>
    </select>
    ```

    > 注：
    > 1. `<select></select>`中至少应包含一对`<option></option>`;
    > 2. 在option 中定义selected =" selected "时，当前项即为默认选中项;
  + 表单域

    ```HTML
    <form action="url地址" method="提交方式" name="表单名称">
        各种表单控件
    </form>
    ```

    > 常用属性：
    > 1. Action 在表单收集到信息后，需要将信息传递给服务器进行处理，action属性用于指定接收并处理表单数据的服务器程序的url地址;
    > 2. method 用于设置表单数据的提交方式，其取值为get或post;
    > 3. name 用于指定表单的名称，以区分同一个页面中的多个表单;
    >
    > 注意： 每个表单都应该有自己表单域;

## HTML 5新增属性

+ `<input>` ：新增内容如下表：
    |属性名|用法|描述|
    |:---:|:---:|:---|
    |placeholder|`<input type="text" placeholder="请输入用户名">`|占位符 , 在输入框显示提示文字|
    |autofocus|`<input type="text" autofocus>`|当夜幕打开时, 该input框自动获取焦点|
    |multiple|`<input type="text" multiple>`|多文件上传|
    |autocomplete|`<input type="text" autocomplete="on" name="name">`|启动控件的自动完成功能,on/off, 默认为off， 使用该控件必须要有name值, 并且要提交过一次的表单|
    |required|`<input type="text" required>`|必填项|
    |accesskey|`<input type="text" accesskey="s">`|激活控件的快捷键, 采用 ALT + 字母 的形式|

+ `<canvas>` 新元素
    |标签|描述|
    |:---:|:---|
    |`<canvas>`|标签定义图形，比如图表和其他图像。该标签基于 JavaScript 的绘图 API|

+ 新多媒体元素
    |标签|描述|
    |:---:|:---|
    |`<audio>`|定义音频内容|
    |`<video>`|定义视频（video 或者 movie）|
    |`<source>`|定义多媒体资源 `<video>` 和 `<audio>`|
    |`<embed>`|定义嵌入的内容，比如插件|
    |`<track>`|为诸如 `<video>` 和 `<audio>` 元素之类的媒介规定外部文本轨道|

+ 新表单元素
    |标签|描述|
    |:---:|:---|
    |`<datalist>`|定义选项列表。请与 input 元素配合使用该元素，来定义 input 可能的值|
    |`<keygen>`|规定用于表单的密钥对生成器字段|
    |`<output>`|定义不同类型的输出，比如脚本的输出|

+ 新的语义和结构元素
    > HTML5提供了新的元素来创建更好的页面结构：

    |标签|描述|
    |:---:|:---|
    |`<article>`|定义页面独立的内容区域|
    |`<aside>`|定义页面的侧边栏内容|
    |`<bdi>`|允许您设置一段文本，使其脱离其父元素的文本方向设置|
    |`<command>`|定义命令按钮，比如单选按钮、复选框或按钮|
    |`<details>`|用于描述文档或文档某个部分的细节|
    |`<dialog>`|定义对话框，比如提示框|
    |`<summary>`|标签包含 details 元素的标题|
    |`<figure>`|规定独立的流内容（图像、图表、照片、代码等等）|
    |`<figcaption>`|定义 `<figure>` 元素的标题|
    |`<footer>`|定义 section 或 document 的页脚|
    |`<header>`|定义了文档的头部区域|
    |`<mark>`|定义带有记号的文本|
    |`<meter>`|定义度量衡, 仅用于已知最大和最小值的度量|
    |`<nav>`|定义导航链接的部分|
    |`<progress>`|定义任何类型的任务的进度|
    |`<ruby>`|定义 ruby 注释（中文注音或字符）|
    |`<rt>`|定义字符（中文注音或字符）的解释或发音|
    |`<rp>`|在 ruby 注释中使用，定义不支持 ruby 元素的浏览器所显示的内容|
    |`<section>`|定义文档中的节（section、区段）|
    |`<time>`|定义日期或时间|
    |`<wbr>`|规定在文本中的何处适合添加换行符|

+ 已移除的元素
    > 以下的 HTML 4.01 元素在HTML5中已经被删除:

  + `<acronym>`
  + `<applet>`
  + `<basefont>`
  + `<big>`
  + `<center>`
  + `<dir>`
  + `<font>`
  + `<frame>`
  + `<frameset>`
  + `<noframes>`
  + `<strike>`
  + `<tt>`
