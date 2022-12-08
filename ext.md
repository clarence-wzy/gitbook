### Ext

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





















​    


















​    


答案：
```java
Singleton1 value1:1
Singleton1 value2:0
Singleton2 value1:1
Singleton2 value2:1
```

 分析：
 - Singleton1
 1. 首先执行main中的Singleton singleton = Singleton.getInstance(); 
 2. 类的加载：加载类Singleton 
 3. 类的验证 
 4. 类的准备：为静态变量分配内存，设置默认值。这里为singleton(引用类型)设置为null,value1,value2（基本数据类型）设置默认值0 
 5. 类的初始化（按照赋值语句进行修改）： 
    - 执行private static Singleton singleton = new Singleton(); 
    - 执行Singleton的构造器：value1++;value2++; 此时value1，value2均等于1 
    - 执行：public static int value1; public static int value2 = 0; 
    - 此时 value1=1，value2=0
- Singleton2
1. 首先执行main中的Singleton2 singleton2 = Singleton2.getInstance2(); 
2. 类的加载：加载类Singleton2 
3. 类的验证 
4. 类的准备：为静态变量分配内存，设置默认值。这里为value1,value2（基本数据类型）设置默认值0,singleton2(引用类型)设置为null, 
5. 类的初始化（按照赋值语句进行修改）： 
    - 执行：public static int value2 = 0; 
    - 此时 value2=0 (value1不变，依然是0); 
    - 执行：private static Singleton singleton = new Singleton(); 
    - 执行Singleton2的构造器：value1++;value2++; 
    - 此时value1，value2均等于1,即为最后结果
