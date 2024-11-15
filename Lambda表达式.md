## Lambda表达式
先进行引入
```java
Arrays.sort(arr, new Comparator<Integer>() {
  @Override
  public int compare(Integer o1, Integer o2) {
    return o1 - o2;
  }
});
```
等价于
```java
Arrays.sort(arr,(Integer o1, Integer o2) -> {
  return o1 - o2;
})
```

函数式编程(Functional programming) 是一种思想特点。
面相对象：先找对象，让对象做事情。
而 **函数式编程思想，忽略面向对象的复杂语法，强调做什么，而不是谁去做**
JDK8才开始的一种新语法形式。

```
格式：
() -> {

}
() 对应方法的形参
-> 固定格式
{} 对应方法的方法体
```

### 注意点
- Lambda表达式可以用来简化匿名内部类的书写
- Lambda表达式只能简化**函数式接口**的匿名内部类的写法
- 函数式接口：
  有且仅有一个抽象方法的接口叫做**函数式接口**，接口上方可以加@FunctionalInterface注解


**示例**
```java
@FunctionalInterface
interface Swim{
  public abstract void swimming();
}

public class Test {
  public static void main(String[] args){
    public static void method(Swim s) {
      s.swimming();
    }
  }
}
```

先定义如上接口类和method方法


```java
method(new Swim() {
  @Override
  public void swimming() {
    System.out.println("正在游泳");
  }
})
```
以上内部类的视线方式如上

```java
method(
  () -> {
    System.out.println("正在划水");
  }
)
```

**lambda的省略规则：**
1. 参数类型可以省略不写
2. 如果只有一个参数，参数类型可以省略，同时()也可以省略
3. 如果Lambda表达式的方法体只有一行，大括号，分好，return可以省略不写，但是血药同时省略。

```java
Arrays.sort(arr, (Integer o1, Integer o2) -> {
  return o1 -o2;
})
```

```java
Arrays.sort(arr, (o1, o2) -> o1 - o2);
```