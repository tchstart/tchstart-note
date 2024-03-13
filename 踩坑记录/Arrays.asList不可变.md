### Arrays.asList()方法不能进行修改
![image](https://github.com/tchstart/tchstart-note/assets/127310524/e8cf5b2f-c398-417a-b01e-a3d7efc136e5)

```java
public class main {
    public static void main(String[] args) {
      String a = "a,b,c,d,e,ff";
        List<String> list = Arrays.asList(a.split(","));
        list.add("1");
        System.out.println(list);

    }
}
```

当时确实知道这个方法转换的List不能进行修改，否则会抛出`java.lang.UnsupportedOperationException`异常。
### 出现原因

![image](https://github.com/tchstart/tchstart-note/assets/127310524/949f5a41-39c6-47a3-8d5c-1b57fc61309f)

Arrays.asList返回的类型是ArrayList，这个类型不是List的实现类的那个，而是内部类ArrayList类型

![image](https://github.com/tchstart/tchstart-note/assets/127310524/f2873204-6b67-40a0-899f-7833d3928b34)

这个类继承了`AbstractList<E>`类，没有重写set,add,remove方法，故调用set,add,remove等方法的时候就去调用父类的set,add,remove方法，而父类的这些方法里面是直接抛出`java.lang.UnsupportedOperationException`异常。

![image](https://github.com/tchstart/tchstart-note/assets/127310524/979d3370-0c11-4599-b38c-3c187e5de8d3)

### 解决方案
1. 使用Array.stream()即可进行修改
```java
public class main {
    public static void main(String[] args) {
      String a = "a,b,c,d,e,ff";
        List<String> list = Arrays.stream(a.split(",")).collect(Collectors.toList());
        list.add("1");
        System.out.println(list);

    }
}
```

2. 使用List集合的构造函数
```java
public class main {
    public static void main(String[] args) {
      String a = "a,b,c,d,e,ff";
        List<String> list = new ArrayList<>(Arrays.asList(a.split(",")));
        list.add("1");
        System.out.println(list);

    }
}
```
![image](https://github.com/tchstart/tchstart-note/assets/127310524/25221a77-bada-4cba-9492-b8139b8ea0fe)

