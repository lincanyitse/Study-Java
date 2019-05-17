<h1 id="topbar">Junit、反射、注解</h1>

## Junit单元测试

---

### Junit的概述

> Junit是一个Java语言的单元测试框架，简单理解为可以用于取代java的main方法。Junit属于第三方工具，一般情
况下需要导入jar包。不过，多数Java开发环境已经集成了JUnit作为单元测试工具。

---

### Junit的使用

+ 下载
  + [Junit官网](http://www.junit.org)

+ 步骤
  1. 编写业务类
  2. 创建测试类
     + 编写测试方法

+ 测试方法
  1. 特点
     + 方法命名规则：以test开头，使用驼峰命名法。方法声明上：必须使用注解：@Test，必须使用 public修饰符，没有返回值，方法没有参数。

  2. 运行测试方法
     + 选中方法名：右键 --> Run 测试方法名，则运行选中的测试方法比如测试方法名为 method ，则右键 --> Run method
     + 选中类名：右键 --> Run 类名，则运行该类的所有测试方法比如类名为 Demo1 ，则右键 --> Run Demo1
     + 选中模块名或项目名：右键 --> Run 'All Tests'，则运行整个模块中所有类的所有测试方法。
  3. 查看测试结果
     + 绿色：表示测试通过
     + 红色：表示失败或出现错误

+ 常用注解
  + @Before：在每个测试方法之前都会运行一次
  + @After：在每个测试方法运行以后运行的方法
  + @BeforeClass：在所有的测试方法运行之前，运行一次，而且必须用在静态方法上面。
  + @AfterClass：所有的测试方法运行以后，运行一次，必须用在静态方法上面。

---

## 反射

---

### 反射基本概念

+ 反射是一种机制，利用该机制可以在程序运行过程中对类进行解剖并操作类中的方法，属性，
  构造方法等成员。
+ 常用的IDE内部都大量使用了反射机制，我们在使用这些IDE写代码也无时无刻的使用着反射机制，
  一个常用反射机制的地方就是当我们通过对象调用方法或访问属性时，开发工具都会以列表的形式显示出该对象所有的方法或属性，以供方便我们选择使用。
+ 这些开发工具之所有能够把该对象的方法和属性展示出来就使用利用了反射机制对该对象所有类进行了
  解剖获取到了类中的所有方法和属性信息，这是反射在IDE中的一个使用场景。

---

### 获取Class对象

+ 通过类名.class获取

  ```Java
  Class c = 类名.class;
  ```

+ 通过对象的getClass()方法获取

  ```Java
  Object obj = new Object;
  Class c = obj.getClass();
  ```

+ 通过Class.forName("全类名")方法获取

  ```Java
  Class c = Class.forName("java.lang.String");
  ```

---

### 获取Class对象信息

+ Class对象相关方法

  + `String getSimpleName()`: 获得简单类名，只是类名，没有包;

    ```Java
    Class c = Class.forName("java.lang.String");
    // 获得简单类名
    String name = c.getSimpleName();
    // 打印输出：name = String
    System.out.println("name = " + name);
    ```

  + `String getName()`: 获取完整类名，包含包名 + 类名;

    ```Java
    Class c = Class.forName("java.lang.String");
    // 获得完整类名
    String name = c.getName();
    // 打印输出：name = java.lang.String
    System.out.println("name = " + name);
    ```

  + `T newInstance()`: 创建此 Class 对象所表示的类的一个新实例。要求：类必须有public的无参数构造方法;

    ```Java
    Class c = Class.forName("java.lang.String");
    // 获得完整类名
    String str = (String) c.newInstance();
    // 打印输出空字符串
    System.out.println(str);
    ```

---

### 获取Class对象的Constructor信息

+ Constructor类概述
  > Constructor是构造方法类，类中的每一个构造方法都是Constructor的对象，通过Constructor对象可以实例化对象。

+ Class类中与Constructor相关方法
  1. `Constructor getConstructor(Class... parameterTypes)`：根据参数类型获取构造方法对象，只能获得public修饰的构造方法。如果不存在对应的构造方法，则会抛出 java.lang.NoSuchMethodException 异常。

     ```Java
     Class clazz = Class.forName("java.lang.String");
     // 获取类所有public修饰的构造方法，返回对应的Constructor的对象
     Constructor constructor = clazz.getConstructor();
     ```

  2. `Constructor getDeclaredConstructor(Class... parameterTypes)`：根据参数类型获取构造方法对象，能获取所有的构造方法，包括private修饰的构造方法。如果不存在对应的构造方法，则会抛出 java.lang.NoSuchMethodException 异常。

     ```Java
     Class clazz = Class.forName("java.lang.String");
     // 获取类所有的构造方法，返回对应的Constructor的对象
     Constructor constructor = clazz.getDeclaredConstructor();
     ```

  3. `Constructor[] getConstructors()`：获取所有的public修饰的构造方法

     ```Java
     Class clazz = Class.forName("java.lang.String");
     // 获取类所有public修饰的构造方法，返回对应的Constructor对象数组
     Constructor[] constructors = clazz.getConstructors();
     ```

  4. `Constructor[] getDeclaredConstructors()`：获取所有构造方法，包括public、privat、默认、protected修饰的

     ```Java
     Class clazz = Class.forName("java.lang.String");
     // 获取类所有的构造方法，返回对应的Constructor的对象数组
     Constructor[] constructors = clazz.getDeclaredConstructors();
     ```

+ Constructor类中常用方法
  1. `T newInstance(Object... initargs)`：根据指定参数创建对象。

     ```Java
     Class clazz = Class.forName("java.lang.String");
     // 获取一个Constructor对象
     Constructor constructor = clazz.getConstructor();
     // 使用Constructor对象创建一个String对象
     String str = (String) constructor.newInstance();
     // 打印输出空字符串
     System.out.println(str);
     ```

  2. `void setAccessible(true)`：暴力反射，除public修饰的构造方法外，其他构造方法反射都需要暴力反射。

     ```Java
     Class clazz = Class.forName("java.lang.String");
     // 获取一个对应构造函数的Constructor对象
     Constructor constructor = clazz.getDeclaredConstructor(char[].class,boolean.class);
     // 暴力反射
     constructor.setAccessible(true);
     // 使用Constructor对象带参数创建一个String对象
     String str = (String) constructor.newInstance(new char[]{'h','e','l','l','o'},false);
     // 打印输出：hello
     System.out.println(str);
     ```

---

### 获取Class对象的Method信息

+ Method类概述
  > Method是方法类，类中的每一个方法都是Method的对象，通过Method对象可以调用方法。

+ Class类中与Method相关方法
  1. `Method getMethod("方法名", 方法的参数类型... 类型)`：根据方法名和参数类型获得一个方法对象，只能是获取public修饰的;

     ```Java
     Class clazz = Class.forName("java.lang.String");

     // 获取String类里一个函数名为charAt并且是pulic修饰的Method对象
     Method method = clazz.getMethod("charAt", int.class);
     ```

  2. `Method getDeclaredMethod("方法名", 方法的参数类型... 类型)`：根据方法名和参数类型获得一个方法对象，包括private修饰的;

     ```Java
     Class clazz = Class.forName("java.lang.String");

     // 获取String类里一个函数名为checkBounds的Method对象
     Method method = clazz.getDeclaredMethod("checkBounds", byte[].class, int.class, int.class);
     ```

  3. `Method[] getMethods()`：获取所有的public修饰的成员方法，包括父类中;

     ```Java
     Class clazz = Class.forName("java.lang.String");

     // 获取String类里所有是pulic修饰的函数对应的Method对象数组
     Method[] methods = clazz.getMethods();
     ```

  4. `Method[] getDeclaredMethods()`：获取当前类中所有的方法，包含私有的，不包括父类中。

     ```Java
     Class clazz = Class.forName("java.lang.String");

     // 获取String类里所有函数对应的Method对象数组
     Method[] methods = clazz.getDeclaredMethods();
     ```

+ Method类中常用方法
  1. `Object invoke(Object obj, Object... args)`：根据参数args调用对象obj的该成员方法如果obj=null，则表示该方法是静态方法;
  
     ```Java
     Class clazz = Class.forName("java.lang.String");
     // 使用Class对象创建一个String对象
     String str = (String) clazz.newInstance();
     // 设置str的值
     str = "hello";
     // 获取String类里一个函数名为charAt并且是pulic修饰的Method对象
     Method method = clazz.getMethod("charAt", int.class);
     // 传入对象和参数，执行反射对应的方法
     Object invoke = method.invoke(str,4);
     // 打印输出：o
     System.out.println(invoke);
     ```
  
  2. `void setAccessible(boolean flag)`：暴力反射，设置为可以直接调用私有修饰的成员方法

     ```Java
     Class clazz = Class.forName("java.util.ArrayList");
     // 使用Class对象创建一个String对象
     ArrayList str = (ArrayList) clazz.newInstance();
     // 添加元素
     str.add(1);
     // 获取ArrayList类里一个函数名为outOfBoundsMsg的Method对象
     Method method = clazz.getDeclaredMethod("outOfBoundsMsg", int.class);
     // 开启暴力反射
     method.setAccessible(true);
     // 传入对象和参数，执行反射对应的方法
     Object invoke = method.invoke(str,1);
     // 打印输出：Index: 1, Size: 1
     System.out.println(invoke);
     ```

---

### 获取Class对象的Field信息

+ Field类概述
  > Field是属性类，类中的每一个属性(成员变量)都是Field的对象，通过Field对象可以给对应的成员变量赋值和取值。

+ Class类中与Field相关方法
  1. `Field getField(String name)`：根据属性名获得属性对象，只能获取public修饰的;

     ```Java
     Class clazz = Class.forName("java.lang.Math");

     // 获取一个对应Math类里面变量名为PI且修饰符为public的Field对象
     Field field = clazz.getField("PI");
     ```
  
  2. `Field getDeclaredField(String name)`：根据属性名获得属性对象，包括private修饰的;

     ```Java
     Class clazz = Class.forName("java.lang.String");

     // 获取一个对应String类里面变量名为value的Field对象
     Field field = clazz.getDeclaredField("value");
     ```
  
  3. `Field[] getFields()`：获取所有的public修饰的属性对象，返回数组;

     ```Java
     Class clazz = Class.forName("java.lang.Math");

     // 获取Math类里面所有修饰符为public的Field对象
     Field[] fields = clazz.getFields();
     ```
  
  4. `Field[] getDeclaredFields()`：获取所有的属性对象，包括private修饰的，返回数组;

     ```Java
     Class clazz = Class.forName("java.lang.String");

     // 获取一个对应String类里面变量名为value的Field对象
     Field[] fields = clazz.getDeclaredFields();
     ```

+ Field类中常用方法
  1. `void set(Object obj, Object value);` ：设置Field对象对应的属性值;
  2. `void setInt(Object obj, int i);` ：设置Field对象对应的整数类型属性值;
  3. `void setLong(Object obj, long l);` ：设置Field对象对应的长整数类型属性值;
  4. `void setBoolean(Object obj, boolean z);` ：设置Field对象对应的布尔值类型属性值;
  5. `void setDouble(Object obj, double d);` ：设置Field对象对应的浮点数类型属性值;
  6. `Object get(Object obj);` ：获取Field对象对应属性的内容;
  7. `int getInt(Object obj);` ：获取Field对象对应属性的整数内容;
  8. `long getLong(Object obj);` ：获取Field对象对应属性的长整数内容;
  9. `boolean getBoolean(Object ob);` ：获取Field对象对应属性的布尔值内容;
  10. `double getDouble(Object obj);` ：获取Field对象对应属性的浮点数内容;
  11. `void setAccessible(true);` :暴力反射，设置为可以直接访问私有类型的属性。
  12. `Class getType();` : 获取属性的类型，返回Class对象。
  13. 总结：
      + setXxx方法都是给对象obj的属性设置使用，针对不同的类型选取不同的方法；
      + getXxx方法是获取对象obj对应的属性值的，针对不同的类型选取不同的方法。

---

## 注解

---

### 注解的概述

1. 注解的概念
   + 注解是JDK1.5的新特性;
   + 注解相当一种标记，是类的组成部分，可以给类携带一些额外的信息;
   + 标记(注解)可以加在包，类，字段，方法，方法参数以及局部变量上;
   + 注解是给编译器或JVM看的，编译器或JVM可以根据注解来完成对应的功能;
   > 注解(Annotation)相当于一种标记，在程序中加入注解就等于为程序打上某种标记，以后，javac编译器、开发工具和其他程序可以通过反射来了解你的类及各种元素上有无何种 标记，看你的程序有什么标记，就去干相应的事，标记可以加在包、类，属性、方法，方法的参数以及局部变量上。

2. 注解的作用
   + 注解的作用就是给程序带入参数。
     1. 生成帮助文档：@author和@version
        + @author：用来标识作者姓名。
        + @version：用于标识对象的版本号，适用范围：文件、类、方法。
        > 使用@author和@version注解就是告诉Javadoc工具在生成帮助文档时把作者姓名和版本号也标记在文档中。
     2. 编译检查：@Override
        + @Override：用来修饰方法声明。
        > 用来告诉编译器该方法是重写父类中的方法，如果父类不存在该方法，则编译失败。
     3. 框架的配置(框架=代码+配置)

        ```Java

        ```

3. 常见注解
   1. @author：用来标识作者名，eclipse开发工具默认的是系统用户名。
   2. @version：用于标识对象的版本号，适用范围：文件、类、方法。
   3. @Override ：用来修饰方法声明，告诉编译器该方法是重写父类中的方法，如果父类不存在该方法，则编译失败。

---

### 自定义注解

+ 定义格式
  
  ```Java
  public @interface 注解名{

  }
  ```

+ 注解的属性
  1. 属性的作用
     > 可以让用户在使用注解时传递参数，让注解的功能更加强大。
  2. 属性的格式
     + 格式1：数据类型 属性名();
     + 格式2：数据类型 属性名() default 默认值;
  3. 属性定义示例

      ```Java
      public @interface Student {
          String name(); // 姓名
          int age() default 18; // 年龄
          String gender() default "男"; // 性别
      }
      // 该注解就有了三个属性：name，age，gender
      ```

  4. 属性适用的数据类型
     + 八种基本数据类型（int,float,boolean,byte,double,char,long,short)  
     + String类型，Class类型，枚举类型，注解类型  
     + 以上所有类型的一维数组  

---

### 自定义注解的使用

+ 定义注解
  1. 定义一个注解：Book
     + 包含属性：String value() 书名
     + 包含属性：double price() 价格，默认值为 100
     + 包含属性：String[] authors() 多位作者
  2. 代码实现

     ```Java
     public @interface Book {
        // 书名
        String value();
        // 价格
        double price() default 100;
        // 多位作者
        String[] authors();
     }
     ```

+ 使用注解
  1. 定义类在成员方法上使用Book注解
  
     ```Java
     public class BookShelf {
         @Book(value = "西游记",price = 998,authors = {"吴承恩","白求恩"})
         public void showBook(){

         }
     }
     ```

     > 使用注意事项：  
     > + 如果属性有默认值，则使用注解的时候，这个属性可以不用赋值。  
     > + 如果属性没有默认值，那么在使用注解时一定要给属性赋值。
+ 特殊属性value
  1. 当注解中只有一个属性且名称是value，在使用注解时给value属性赋值可以直接给属性值，无论value是单值元素还是数组类型。
  2. 如果注解中除了value属性还有其他属性，且至少有一个属性没有默认值，则在使用注解给属性赋值时，value属性名不能省略。

+ 自定义注释的问题
  1. 默认情况下，注解可以用在任何地方，比如类，成员方法，构造方法，成员变量等地方；
  2. 如果要限制注解的使用位置怎么办？那就要学习一个新的知识点：元注解。

---

### 注解之元注解

+ 元注解的概述
  + Java API提供的注解;
  + 专门用来定义注解的注解;
  + 任何Java官方提供的非元注解的定义中都使用到了元注解。

+ 常用元注解

  + `@Target`：指明此注释用在哪个位置， 如果不写默认是任何地方都可以使用 。
    > 可选的参数值在枚举类ElemenetType中包括：
    > + TYPE： 用在类,接口上 FIELD：用在成员变量上  
    > + METHOD： 用在方法上  
    > + PARAMETER：用在参数上  
    > + CONSTRUCTOR：用在构造方法上  
    > + LOCAL_VARIABLE：用在局部变量上  
    > + ANNOTATION_TYPE：用在注解上  
  + `@Retention`：定义该注解的生命周期(有效范围)。
    > 可选的参数值在枚举类型RetentionPolicy中包括
    > + SOURCE：注解只存在于Java源代码中，编译生成的字节码文件中就不存在了。
    > + CLASS：注解存在于Java源代码、编译以后的字节码文件中，运行的时候内存中没有，默认值。
    > + RUNTIME：注解存在于Java源代码中、编译以后的字节码文件中、运行时内存中，程序可以通过反射获取该注解。

---

### 注解解析

+ 什么是注解解析
  > 通过Java技术获取注解数据的过程则称为注解解析。
+ 与注解解析相关的接口
  + Anontation：所有注解类型的公共接口，类似所有类的父类是Object。
  + AnnotatedElement：定义了与注解解析相关的方法，常用方法以下四个：
    + `boolean isAnnotationPresent(Class annotationClass);` 判断当前对象是否有指定的注解，有则返回true，否则返回false。
    + `T getAnnotation(Class<T> annotationClass);`  获得当前对象上指定的注解对象。
    + `Annotation[] getAnnotations();` 获得当前对象及其从父类上继承的所有的注解对象。
    + `Annotation[] getDeclaredAnnotations();` 获得当前对象上所有的注解对象，不包括父类的。
+ 获取注解数据的原理
  + 注解作用在那个成员上，就通过反射获得该成员的对象来得到它的注解。如注解作用在方法上，就通过方法(Method)对象得到它的注解;

    ```Java
    // 得到方法对象
    Method method = clazz.getDeclaredMethod("方法名");
    // 根据注解字节码对象得到方法上的注解对象
    Compute compute = method.getAnnotation(Compute.class);
    ```

  + 如注解作用在类上，就通过Class对象得到它的注解;

    ```Java
    // 获得Class对象
    Class c = 类名.class;
    // 根据注解字节码对象得到类上的注解对象
    Compute compute = c.getAnnotation(Compute.class);
    ```

+ 注解解析的问题
  > 获取注解数据时默认处理不够严谨，所以在获取注解对象时，先判断是否有使用注解，如果有，才获取，否则就不用获取。

---

<span style="float:left;display:inline-block;">[上一章](Day24.md)</span>
<span style="margin-left:43%">[目录](SUMMARY.md)</span>
<span style="float:right;">[下一章](Day26.md)</span>