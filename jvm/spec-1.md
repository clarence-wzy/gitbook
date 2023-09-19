### Ext

1. 静态方法为什么不能引用this？
2. 对象都是在"堆"中创建吗？所有对象都必须经历年轻代年龄阈值吗（排除大对象直接进入老年代的情况）？
3. try-catch是否会影响性能？
4. 

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
5. 

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





















​    


















​    
