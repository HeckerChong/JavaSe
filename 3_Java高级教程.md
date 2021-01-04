# 第一章 Scanner类

**Scanner类**
一个可以解析基本类型和字符串的简单文本扫描器。 例如，以下代码使用户能够从 System.in 中读取一个数：

```java
Scanner sc = new Scanner(System.in); 
int i = sc.nextInt();
```

**引用类型使用步骤**

使用import关键字导包，在类的所有代码之前导包，引入要使用的类型，java.lang包下的所有类无需导入。
格式：
```java
import 包名.类名;
```
例如：
```java
java.util.Scanner;
```

**创建对象**

使用该类的构造方法，创建一个该类的对象。 格式：

```java
数据类型 变量名 = new 数据类型(参数列表);
```


**调用方法**

调用该类的成员方法，完成指定功能。格式：

```java
变量名.方法名();
```

举例：
```java
int i = sc.nextInt(); //接收一个键盘录入的整数
```

## 1.1 Scanner的使用步骤

**查看类**
* `java.util.Scanner`：该类需要import导入后使用。

**查看构造方法**
* `public Scanner(InputStream source)`：构造一个新的`Scanner`，它生成的值是从指定的输入流扫描的。

**查看成员方法**
* `public int nextInt()`：将输入信息的下一个标记扫描为一个`int`值。

使用Scanner类，完成接收键盘录入数据的操作，代码如下：

```java
//1. 导包 
import java.util.Scanner; 
public class Demo01_Scanner {

    public static void main(String[] args) { 
        //2. 创建键盘录入数据的对象 
        Scanner sc = new Scanner(System.in);

        //3. 接收数据 
        System.out.println("请录入一个整数："); 
        int i = sc.nextInt();
        
        //4. 输出数据 
        System.out.println("i:"+i);

    }
}
```

**取最值**

```java
import java.util.Scanner; 
public class Test02Scanner {
    public static void main(String[] args) { 
        // 创建对象 
        Scanner sc = new Scanner(System.in); 
        // 接收数据 
        System.out.println("请输入第一个数据："); 
        int a = sc.nextInt(); 
        System.out.println("请输入第二个数据："); 
        int b = sc.nextInt();
        System.out.println("请输入第三个数据：");
        int c = sc.nextInt();

        // 如何获取三个数据的最大值
        int temp = (a > b ? a : b);
        int max = (temp > c ? temp : c);

        System.out.println("max:" + max);
    }
}
```

## 1.2 匿名对象

**概念**
创建对象时，只有创建对象的语句，却没有把对象地址值赋值给某个变量。虽然是创建对象的简化写法，但是应用 场景非常有限。

* **匿名对象**：没有变量名的对象。

格式：

```java
new 类名(参数列表);
```

举例：

```java
new Scanner(System.in);
```

**应用场景**
1. 创建匿名对象直接调用方法，没有变量名。

```java
new Scanner(System.in).nextInt();
```

2. 一旦调用两次方法，就是创建了两个对象，造成浪费。

```java
new Scanner(System.in).nextInt(); 
new Scanner(System.in).nextInt();
```

> Tips:一个匿名对象，只能使用一次。

3. 匿名对象可以作为`方法的参数和返回值`

* 作为参数

```java
class Test {

    public static void main(String[] args) { 
        // 普通方式 
        Scanner sc = new Scanner(System.in); input(sc);
        //匿名对象作为方法接收的参数 
        input(new Scanner(System.in));
    }

    public static void input(Scanner sc){ 

        System.out.println(sc); 
    }

}
```

* 作为返回值

```java
class Test2 {

    public static void main(String[] args) { 
        // 普通方式
        Scanner sc = getScanner(); 
    }

    public static Scanner getScanner(){
        //普通方式 
        //Scanner sc = new Scanner(System.in); 
        //return sc;

        //匿名对象作为方法返回值 
        return new Scanner(System.in);

    }
}
```

# 第二章 Random类

**Random**：此类的实例用于生成伪随机数。

示例：

```java
//获取一个随机整数
Random r = new Random(); 
int i = r.nextInt();
```

## 2.1 Random使用步骤
