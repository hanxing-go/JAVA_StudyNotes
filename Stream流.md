## Stream 流

```java
public class Main {
    public static void main(String[] args) {

        ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list,"张旭","张洋","张一栋","王旭","王洋","王一栋");

        list.stream().filter(name -> name.startsWith("张")).filter(name -> name.length() == 3).forEach(name -> System.out.print(name + " "));

    }
}
```  

那些数据可以获得数据流，用上么方式获取？
1. 单列集合 default Stream<E> stream() 
   Collection中的默认方法
2. 双列集合 无  
   无法直接使用stream

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {

//        1. 创建双列集合
        HashMap<String, Integer> hm = new HashMap<>();
//        2. 添加数据1
        hm.put("aaa", 111);
        hm.put("bbb",222);
        hm.put("ccc",333);
        hm.put("ddd",444);

//        3. 第一种获取Stream流的方法
        hm.keySet().stream().forEach(s -> System.out.print(s));
        System.out.println();
//        4. 第二种获取Stream流的方法
        hm.entrySet().stream().forEach(s -> System.out.print(s));
    }
}
3. 数组 public static <T> Stream <T> stream(T[] array); 
   Arrays工具类中的静态方法
4. 一堆零散数据 public static Stream<T> of(T... values) 
   Stream 接口中的静态方法
```

### Stream流的常见中间方法
![alt text](image.png)
#### Stream流中的数据类型转换
注意1： 中间方法，返回新的Stream流，原来的Stream流只能使用一次，建议使用链式编程
注意2: 修改Stream流中的数据，不会影响原来集合或者数组中的数据

```java
ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list, "张无忌-15", "周芷若-14", "赵敏-13", "张强-20");

        //第一个类型：Steam流中原本的数据类型
        //第二个类型：要转成之后的类型

        // apply的形参s: 依次表示流里面的每一个数据
        //返回值：表示转换之后的数据

        //当map方法执行完毕之后，流上的数据就变成了整数
        //所以在下面forEach当中，s依次表示流里面的每一个数据，这个数据现在就是整数了。
        list.stream().map(new Function<String, Integer>() {

            @Override
            public Integer apply(String s) {
                String[] arr = s.split("-");
                String ageString = arr[1];
                int age = Integer.parseInt(ageString);
                return age;
            }
        }).forEach(s -> System.out.println(s));
    

     System.out.println("===========================");

        list.stream().map(s -> Integer.parseInt(s.split("-")[1])).forEach(s -> System.out.println(s));
```

### Stream流的终结方法
![alt text](image-1.png) 

```java
        List<String> list = new ArrayList<>();
        Collections.addAll(list, "1","2","3","4","5");

        // 1. forEach
        list.stream().forEach(s -> System.out.print(s + " "));

        // 2. count
        System.out.println();
        System.out.println(list.stream().count());

        //3. toArray
        String[] arrays = list.stream().toArray(new IntFunction<String[]>() {
            @Override
            public String[] apply(int value) {
                return new String[value];
            }
        });

        System.out.println(Arrays.toString(arrays));

        String[] array = list.stream().toArray(v -> new String[v]);
        System.out.println(Arrays.toString(array));
```

```java
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        Collections.addAll(list, "zhangxu-18","zx-18","zhang-18","xu-13","xixi-34");

        // 将18岁的人区分出来，收集到List集合当中
        List<String> newList1 = list.stream()
                .filter(s -> "18".equals(s.split("-")[1]))
                .collect(Collectors.toList());

        System.out.println(newList1);
        // 收集到Set集合当中
        // 把所有18岁的人区分开，收集到Set集合当中
        Set<String> newset = list.stream()
                .filter(s -> "18".equals(s.split("-")[1]))
                .collect(Collectors.toSet());
        System.out.println(newset);
        //收集到Map集合当中
        Map<String,Integer> newmap = list.stream()
                .filter(s -> "18".equals(s.split("-")[1]))
                /*
                toMap: 参数一表示键的生成规则
                        参数二表示值的生成规则

                参数一：
                    Function泛型一：表示流中每一个数据的类型
                    泛型二：表示Map集合中键的数据类型

                    方法apply形参：依次表示流里面的每一个数据
                    方法体：生成键的代码
                    返回值：已经生成的键

               参数二：
                    Function泛型一：表示流中每一个数据的类型
                    泛型二：表示Map集合中键的数据类型

                    方法apply形参：依次表示流里面的每一个数据
                    方法体：生成值的代码
                    返回值：已经生成的值
                 */
                .collect(Collectors.toMap(
                        new Function<String, String>() {
                            @Override
                            public String apply(String s) {
                                return s.split("-")[0];
                            }
                        },
                        new Function<String, Integer>() {
                            @Override
                            public Integer apply(String s) {
                                return Integer.parseInt(s.split("-")[1]);
                            }
                        }
                ));
        System.out.println(newmap);

        list.stream().filter(s -> "18".equals(s.split("-")[1]))
                .collect(Collectors.toMap(s -> s.split("-")[0], s -> Integer.parseInt(s.split("-")[1])))
                .forEach((s1, s2) -> System.out.print(s1 + "=" + s2));
    }
```

