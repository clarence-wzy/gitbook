### Ext

1. 
```java
class Singleton{
    private static Singleton singleton = new Singleton();
    public static int value1;
    public static int value2 = 0;

    private Singleton(){
        value1++;
        value2++;
    }

    public static Singleton getInstance(){
        return singleton;
    }
}
```

```java
class Singleton2{
    public static int value1;
    public static int value2 = 0;
    private static Singleton2 singleton2 = new Singleton2();

    private Singleton2(){
        value1++;
        value2++;
    }

    public static Singleton2 getInstance2(){
        return singleton2;
    }
}
```

```java
public static void main(String[] args) {
    Singleton singleton = Singleton.getInstance();
    System.out.println("Singleton1 value1:" + singleton.value1);
    System.out.println("Singleton1 value2:" + singleton.value2);

    Singleton2 singleton2 = Singleton2.getInstance2();
    System.out.println("Singleton2 value1:" + singleton2.value1);
    System.out.println("Singleton2 value2:" + singleton2.value2);
}
```
2. 静态方法中为什么不可用引用this？
3. 
```java
public class Demo {
    static abstract class Human {}
    static class Man extends Human {}
    static class Woman extends Human {}
 
    public void say(Human guy) {
        System.out.println("human!");
    }
    public void say(Man guy) {
        System.out.println("man!");
    }
    public void say(Woman guy) {
        System.out.println("woman!");
    }
 
    public static void main(String[] args) {
        Human man = new Man();
        Human woman = new Woman();
 
        Demo demo = new Demo();
        demo.say(man); // ？？？
        demo.say(woman); // ？？？
    }
}
```
```java
public class Demo {
    static abstract class Human {
        protected abstract void say();
    }
    static class Man extends Human {
        @Override
        protected void say() {
            System.out.println("man!");
        }
    }
    static class Woman extends Human {
        @Override
        protected void say() {
            System.out.println("woman!");
        }
    }
 
    public static void main(String[] args) {
        Human man = new Man();
        Human woman = new Woman();
 
        man.say(); // ？？？
        woman.say(); // ？？？

        man = new Woman();
        man.say(); // ？？？
    }
}
```
```java
public class Demo {
    static class Human {
        int type = 0;
    }
    static class Man extends Human {
        int type = 1;
    }

    public static void main(String[] args) {
        Human man = new Man();
        System.out.println(man.type); // ？？？
    }
}
```
4. try-catch是否会影响性能？




















​    


















​    


1. 答案：（类加载阶段）
```java
Singleton1 value1:1
Singleton1 value2:0
Singleton2 value1:1
Singleton2 value2:1
```

 分析：
 - Singleton1
 1). 首先执行main中的Singleton singleton = Singleton.getInstance(); 
     2). 类的加载：加载类Singleton 
     3). 类的验证 
     4). 类的准备：为静态变量分配内存，设置默认值。这里为singleton(引用类型)设置为null,value1,value2（基本数据类型）设置默认值0 
     5). 类的初始化（按照赋值语句进行修改）： 
    - 执行private static Singleton singleton = new Singleton(); 
    - 执行Singleton的构造器：value1++;value2++; 此时value1，value2均等于1 
    - 执行：public static int value1; public static int value2 = 0; 
    - 此时 value1=1，value2=0
- Singleton2
  1). 首先执行main中的Singleton2 singleton2 = Singleton2.getInstance2(); 
  2). 类的加载：加载类Singleton2 
  3). 类的验证 
  4). 类的准备：为静态变量分配内存，设置默认值。这里为value1,value2（基本数据类型）设置默认值0,singleton2(引用类型)设置为null, 
  5). 类的初始化（按照赋值语句进行修改）： 
    - 执行：public static int value2 = 0; 
    - 此时 value2=0 (value1不变，依然是0); 
    - 执行：private static Singleton singleton = new Singleton(); 
    - 执行Singleton2的构造器：value1++;value2++; 
    - 此时value1，value2均等于1,即为最后结果

2. 答案：（虚拟机栈）this变量不存在与当前方法的局部变量表中

3. 答案：（分派）多态的表现-静态分派与动态分派
```java
human!
human!
```
```java
man!
woman!
woman!
```
动态分派不涉及变量
```java
0
```

4. 答案：（异常表）区别于jdk版本，在jdk1.4及之前版本中，异常的处理是通过jsr和set指令来完成，这种方式则是会影响性能的；而jdk1.4之后的版本，异常的处理是采用堆-方法区-异常表的统一处理，这种方式就不会影响性能了
