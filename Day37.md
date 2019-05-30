# jQuery 进阶

## jQuery 动画

### 隐藏与显示

+ 显示元素方法

    ```JAVASCRIPT
    jQuery对象.show([speed], [easing], [fn])
    /*
        参数解析：
            1. speed 可以使用预定速度的字符串(("slow","normal", "fast")
            或动画时长的毫秒数值(如：1000);
            2. easing 用来切换效果, 默认是“swing”, 可用参数“linear”;
            3. fn 在动画完成时执行的函数, 每个元素执行一次;
    */
    ```

+ 隐藏元素方法

    ```JAVASCRIPT
    jQuery对象.hide([speed], [easing], [fn])
    // 参数效果如显示方法一样
    ```

+ 切换元素方法

    ```JAVASCRIPT
    jQuery对象.toggle([speed], [easing], [fn])
    // 参数效果如显示方法一样
    ```

### 滑动效果

|方法名称|解释|
|:---:|:---|
|slideDown([speed,[easing],[fn]])|向下滑动方法|
|slideUp([speed,[easing],[fn]])|向上滑动方法|
|slideToggle([speed],[easing],[fn])|切换元素方法 , 显示的使之隐藏 , 隐藏的使之显示|

|参数名称|解释
|:---:|:---|
|speed|三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)|
|easing|用来指定切换效果 , 默认是"swing" , 可用参数"linear"|
|fn|在动画完成时执行的函数 , 每个元素执行一次|

### 淡入淡出效果

|方法名称|解释|
|:---:|:---|
|fadeIn([speed,[easing],[fn]])|淡入显示方法|
|fadeOut([speed,[easing],[fn]])|淡出隐藏方法|
|fadeToggle([speed],[easing],[fn])|切换元素方法 , 显示的使之隐藏 , 隐藏的使之显示|

> 注：参数的使用同上述几种一样

## jQuery遍历

### 原始方法遍历

```JAVASCRIPT
for(var i=0;i<元素数组.length;i++){
    元素数组[i];
}
```

### 对象方法遍历

```JAVASCRIPT
jQuery对象.each(function(index,element){
    // 代码内容
});
/*
注：
    1. index 就是元素在集合中的索引;
    2. element 就是集合中的每一个元素对象
*/
```

### 全局方法遍历

```JAVASCRIPT
$.each(jQuery对象, function(index,element){
    // 代码内容
});
/*
注：
    1. index 就是元素在集合中的索引;
    2. element 就是集合中的每一个元素对象
*/
```

### jQuery3.0的for of语句遍历

```JAVASCRIPT
for(变量 of jquery对象){
    变量；
}
/*
注：
    1. 变量：:定义变量依次接受jquery数组中的每一个元素;
    2. jquery对象：要被遍历的jquery对象
*/
```

## 事件的绑定与解绑

### 绑定事件

```JAVASCRIPT
jQuery元素对象.on(事件名称,function(){
    //逻辑代码
});
/*
注：
    1. 事件名称: jQuery的事件方法的方法名称(如：click、mouseover、mouseout、focus、blur等)
*/
jQuery元素对象.on({
    事件名称1:function(){
        //逻辑代码
    },
    事件名称2:function(){
        //逻辑代码
    },
    ...
});
/*
多个事件同时绑定*/
```

### 解绑事件

```JAVASCRIPT
jQuery元素对象.off(事件名称);
/*
注：
    参数事件名称如果省略不写 , 会解绑该jQuery对象上所有事件;
*/
```

### 事件切换

+ 普通写法

    ```JAVASCRIPT
    // 事件名方式
    jQuery元素对象.mouseover(function () {
        // 逻辑代码
    });
    jQuery元素对象.mouseout(function () {
        // 逻辑代码
    });

    // 以on方式
    jQuery元素对象.on({
        mouseover:function(){
            // 逻辑代码
        },
        mouseout:function(){
            // 逻辑代码
        }
    });
    /*
    注：
        1. 原始方法分别绑定相对事件, 实现切换效果;
        2. 在on绑定中使用花括号, 同时绑定相对事件, 实现切换效果
    */
    ```

+ 链式写法

    ```JAVASCRIPT
    jQuery元素对象.mouseover(function(){
        // 逻辑代码
    }).mouseout(function(){
        // 逻辑代码
    });
    ```

+ 切换函数写法

    ```JAVASCRIPT
    jQuery元素对象.hover([over, ]out);
    /*
    注：
        1. over 代表鼠标移入事件触发的函数;
        2. out 代表鼠标移出事件触发的函数;
        3. hover这个函数只有2个参数 , 第一个必须鼠标移入事件函数 , 第二个必须是鼠标移出事件
    */
    ```

## jQuery 插件

> 以jquery为基础进行扩展具有特定功能的代码

### jQuery的插件机制

> 利用jQuery提供的jQuery.fn.extend()和jQuery.extend()方法 , 扩展jQuery的功能, 或是重写jQuery功能;

+ 语法

|语法|解释|
|:---:|:---|
|jQuery.fn.extend(object)|对jQuery对象进行方法扩展|
|jQuery.extend(object)|对jQuery全局进行方法扩展|

+ 扩展

    ```JAVASCRIPT
    // 对jq对象扩展
    $.fn.extend({
        事件名称1:function(){
            /*
            注：
                对jQuery对象扩展, 这时的this就是当前的jQuery对象, 而不再是js对象(只有这里是jQuery对象)
            */
            // 逻辑代码
        },
        事件名称2:function(){
            // 逻辑代码
        },
        ...
    });
    // jQuery全局方法扩展
    $.extend({
        全局方法1:function(){
            // 逻辑代码
        },
        全局方法2:function(){
            // 逻辑代码
        },
        ...
    });
    ```

### 表单校验插件validator

+ 语法

    ```JAVASCRIPT
    $("form表单的选择器").validate({
        rules:{
            表单项name值:校验规则 ,
            表单项name值:校验规则... ...
        },
        messages:{
            表单项name值:错误提示信息 ,
            表单项name值:错误提示信息... ...
        }
    });
    /*
    注：
        rules是对表单项校验的规则;
        messages是对应的表单项校验失败后的错误提示信息;
        当错误提示信息不按照我们预想的位置显示时, 行设置自定义错误显示标签放在我们需要显示的位置, jQuery验证插件会自动帮助我们控制它的显示与隐藏, 设置了错误lable标签就不必在messages中设置此表单项错误提示信息
        (<lable for="html元素name值" class="error" style="display:none">错误信息</lable>)
    */
    ```

+ 校验规则

|字段名|介绍|
|:---:|:---|
|`required:true`|必输字段|
|`remote:"check.php"`|使用ajax方法调用check.php验证输入值|
|`email:true`|必需输入正确格式的电子邮件|
|`url:true`|必须输入正确格式的网址|
|`date.true`|必须输入正确格式的日期|
|`dateISO:true`|必须输入正确格式的日期(ISO), 例如：2009-06-23, 1998/01/22 (只验证格式, 不验证有效性)|
|`number:true`|必须输入合法的数字(负数, 小数)|
|`digits:true`|必须输入整数|
|`creditcard:true`|必须输入合法的信用卡号|
|`equalTo:"#field"`|输入值必须和`#field`相同|
|`accept:true`|输入拥有合法后缀名的字符串(上传文件的后缀)|
|`maxlength:5`|输入长度最多是5的字符串(汉字算一个字符)|
|`minlength:10`|输入长度最小是10的字符串(汉字算一个字符)|
|`rangelength:[5,10]`|输入长度必须介于5和10之间的字符串(汉字算一个字符)|
|`range:[5,10]`|输入值必须介于5和10之间|
|`max:5`|输入值不能大于5|
|`min：10`|输入值不能小于10|

+ 自定义校验方法

> 自定义校验规则步骤如下：
>
> + 使用
>
>   ```JAVASCRIPT
>   // 校验时调用
>    $.validator.addMethod("校验规则名称",function(value,element,params) {});
>   ```
>
> + 在rules中通过校验规则名称使用校验规则
> + 在messages中定义该规则对应的错误提示信息
>
> 注： value是校验组件的value值 , element是校验组件的节点对象 , params是校验规则的参数;