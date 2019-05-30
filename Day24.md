# Stream流

## 函数式接口

### Predicate接口

> 作用：对某种类型的数据进行判断，从而得到一个boolean值结果
> 包全名：`java.util.function.Predicate<T>`

+ test 方法
    > `Predicate` 接口中包含一个抽象方法： `boolean test(T t)` ;

    例：

    ```JAVA
    import java.util.function.Predicate;

    public class Demo1 {
        private static void passScore(Predicate<Integer> predicate,int score){
            if(predicate.test(score)){
                System.out.println(score + "分在及格线上！");
            }else{
                System.out.println(score + "分不及格！");
            }
        }
        public static void main(String[] args){
            passScore(s->s>60,75);
            passScore(s->s>60,59);
        }
    }
    ```

+ and 方法
    > 中将两个`Predicate`条件使用“与”逻辑连接起来实现“并且”的效果时，可以使用默认方法`and`;

    例：

    ```JAVA
    import java.util.function.Predicate;

    public class Demo2 {
        // sd
    }

    ```
