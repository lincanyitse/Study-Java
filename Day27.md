# Oracle简单语句、常用函数

## 函数

---

### 单行函数

> 单行函数的一些特点
>
> + 操作数据对象
> + 接受一个参数返回一个结果
> + 只对一行进行变换
> + 每行返回一个结果
> + 可以转换数据类型
> + 可以嵌套
> + 参数可以是一列或一个值

### 多行函数
>
> + 输入多个参数,或者是内部扫描多次,输出一个结果
> + 处理的数据是多条的

---

## 数据类型

---

### 字符类型

+ char
  > char数据类型存储固定长度的字符,默认长度单位为字节,若某字符串长度比设置的固定长度短,将自动用空格填充;
+ varchar2
  > varchar2是oracle独有的数据类型,与标准sql里的varchar差不多,都是存储可变长度的字符串,需要设置最大长度,与char不同不会自动填充空格;
+ long
  > long数据类型可以存放2GB的字符数据,它是从早期版本中继承下来的。但是LONG类型有诸多限制,所以不建议使用
  > 每个表只能有一个LONG类型列:

  + 不能作为主键；
  + 不能建立索引；
  + 不能出现在查询条件中等
+ clob
  > 字符型大型对象（Character Large Object）,则与字符集相关,适于存贮文本型的数据（如历史档案、大部头著作等）

#### 字符函数

+ 字符控制函数
  + `length(char)` 用于返回参数字符串的长度,`varchar2` 返回的长度是字符个数,`char` 返回的长度包括后补的空格。

  + `concat(char1,char2)` 用于返回两个字符串连接后的结果,如果需要连接多个字符串,则需要多个 `concat` 函数内嵌,连接多个字符串一般使用 `||` 符号更为直观

+ 字符转换函数
  + `upper(char)` 用于将字符转换为大写形式
  + `Lower(char)` 用于将字符转换为小写形式
  + `Initcap(cahr)` 用于将字符串中每个单词的首字符大写,其余字符小写
  > 注:Oracle中命令语句不区分大小写,但是数据内容区分大小写

+ 字符截去函数
  + `trim(c2 from c1)` 用于从c1的前后截取c2
  + `ltrim(c1[, c2])` 用于从c1的左边截取c2
  + `rtrim(c1[, c2])` 用于从c1的右边截取c2
  > 注:`ltrim` 和 `rtrim` 没有参数c2的话,就去除多余空格;

+ 补位函数
  + `lpad(char1, n, char2)` 用于在char1的左端用char2补足到n位
  + `rpad(char1, n, char2)` 用于在char1的右端用char2补足到n位
  > 注:参数char2可重复多次

+ 字符截取函数
  + `substr(char, [m[, n]])` 用于返回char中从m位开始取n个字符的子串,字符串的首位计数从1开始;

+ 字符取引索函数
  + `instr(char1, char2[, m[, n]])` 用于返回子串char2在源字符串char1中的位置,从m的位置开始搜索,没有指定m,从第1个字符开始搜索n用于指定子串的第n次出现次数,如果不指定取值1如果在char1中没有找到子串char2,返回0

---

### 数值类型

+ Number
  + `NUMBER(p)` 表示整数
  + `NUMBER(p,s)` 可以用来表示整数和浮点数
    > 注:没有设置参数`s`,则默认取值`0`,即`NUMBER(p)`用来表示整数,`p`包括`s`的位数;
  + `NUMBER(P,S)`  表示浮点数
    > 如果`NUMBER(p,s)`的两个参数全部显式定义,则表示浮点数:
    > + p:NUMBER可以存储的最大数字长度（不包括左右两边的0）
    > + s:在小数点右边的最大数字长度（包括左侧0）
  > NUMBER的变种数据类型:内部实现是NUMBER,可以将其理解为NUMBER的别名,目的是与多种数据库及编程语言兼容
  > + `NUMERIC(p,s)` :等价于NUMBER(p,s)
  > + `DECIMAL(p,s)`或`DEC(p,s)` :等价于NUMBER(p,s)
  > + `INTEGER或INT` :等价于NUMBER(38)类型
  > + `SMALLINT` :等价于NUMBER(38)类型
  > + `FLOAT(b)` :等价于NUMBER类型
  >

#### 数值函数

+ `round(m[, m])` 用于将参数n按照m的数字要求四舍五入
  > 注:参数中的n可以是任何数字,指要被处理的数字
  > + m必须是整数
  > + m取正数则四舍五入到小数点后第m位
  > + m取负数,则四舍五入到小数点前m位
  > + m取0值则四舍五入到整数位
  > + m缺省,默认值是0

+ `trunc(n[, m])` 用于将参数n按照m的数字进行截取
+ `mod(m,n)` 用于返回m除以n后的余数,如果n为0者直接返回m
+ `ceil(n)` 用于向上取整,n可以是浮点数
+ `floor(n)` 用于向下取整

---

### 日期类型

+ Date
  > 可以保存定长的日期或时间数据,包括世纪,年,月,日,时,分和秒,`DATE`类型在数据库中的实际存储固定为7个字节,格式分别为:
  >
  > + 第1字节:世纪
  > + 第2字节:年
  > + 第3字节:月
  > + 第4字节:天
  > + 第5字节:小时
  > + 第6字节:分
  > + 第7字节:秒
  >
  > `Date`类型的数据可以显示到年月日,也可以显示到年月日时分秒,主要看存储数据的精确度
  > 1. 存储年月日只显示年月日
  > 2. 没有存时分秒,或者时分秒位00:00:00,也都只显示年月日
  > 3. 存储年月日时分秒才会显示年月日时分秒

+ Timestamp
  > `TIMESTAMP` 表示时间戳,与DATE的区别是不仅可以保存日期和时间,还能保存小数秒,可指定为0-9位,默认6位,最高精度可以到ns(纳秒)级别;
  > 数据库内部用7或者11个字节存储,精度为0时,用7字节存储,与DATE功能相同,精度大于0则用11字节存储,格式为：
  > + 第1字节-第7字节：和DATE相同
  > + 第8-11字节：纳秒

+ Sysdate
  > `SYSDATE` 本质是一个Oracle的内部函数，用来返回当前的系统时间，精确到秒,默认显示格式是 `DD-MON-RR` ,只有年月日并不显示时分秒;

+ Systimestamp
  > `SYSTIMESTAMP` 也是Oracle的内部日期函数，返回当前系统日期和时间，精确到毫秒;

#### 日期函数

+ `to_date(char[, fmt])` 用于将字符串按照定制格式转换为日期类型;

  > 常用的日期格式如下:
  >
  >>  | 格式 | 含义 |
  >>  | :---: | :---: |
  >>  | YY | 2位数的年份 |
  >>  | YYYY | 4位数的年份 |
  >>  | MM | 2位数的月份 |
  >>  | MON | 简拼的月份 |
  >>  | MONTH | 全拼的月份 |
  >>  | DD | 2位数的天 |
  >>  | DY | 周几的缩写 |
  >>  | DAY | 周几的全拼 |
  >>  | HH24 | 24小时制的小时 |
  >>  | HH12 | 12小时制的小时 |
  >>  | MI | 显示分钟 |
  >>  | SS | 显示秒 |
  >
  > RR日期格式：
  >> <table style="text-align:center"><tr><th style="min-width:100px;">当前年</th><th style="min-width:100px;">日期</th><th style="min-width:100px;">RR格式</th><th style="min-width:100px;">YY格式</th></tr><tr ><td>1995</td><td>27-OCT-95</td><td>1995</td><td>1995</td></tr><tr><td>1995</td><td>27-OCT-17</td><td>2017</td><td>1917</td></tr><tr><td>2001</td><td>27-OCT-17</td><td>2017</td><td>1917</td></tr><tr><td>2001</td><td>27-OCT-95</td><td>1995</td><td>2095</td></tr><tr><td rowspan="2" colspan="2"></td><td colspan="2">指定的年份：</td></tr><tr><td>0-49</td><td>50-99</td></tr><tr><td rowspan="2">当前的年份：</td><td>0-49</td><td>返回本世纪的日期</td><td>返回在当前世纪之前的日期</td></tr><tr><td>50-99</td><td>返回在当前日期之后的当前世纪的日期</td><td>返回本世纪的日期</td></tr></table>

+ `to_char(日期数据, 格式)` 用于把日期数据转换为字符数据，常用于格式化显示日期数据;

+ `months_between(date1, date2)` 用于获取date1与date2相差的月数,如果data2时间比date1时间晚,会得到负值,除非两个日期间隔是整数月，否则会得到带小数位的结果

+ `add_months(date, i)` 返回日期date加上i个月后的日期值,参数i可以是任何数字，大部分时候取正值整数;如果i是小数，将会被截取整数后再参与运算;如果i是负数，则获得的是减去i个月后的日期值

+ `last_day(date)` 返回日期date所在月的最后一天

+ `next_day(date, char)` 返回date日期数据的下一个周几,周几是由参数char来决定的,参数char需要根据环境来设置,也可以直接使用数字表示

+ `least(expr1[, expr2[, expr3]]…)` 返回多个日期对象中比较小的一个值

+ `greatest(expr1[, expr2[, expr3]]…)` 返回多个日期对象中比较大的一个值

+ `extract(date from datetime)` 从参数datetime中提取参数date指定的数据，比如提取年(YEAR)、月(MONTH)、日(DAY)

+ `round(date)` 对日期进行四舍五入

+ `trunc(date)` 对日期进行截断

#### 日期相减

  > 使用日期数据相减 , 得到两个日期之间的天数差 , 不足一天用小数表示
