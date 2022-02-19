# 第一章

## 1.1 函数式编程思想概述

- ![Overview](./images/Overview.png)

在数学中，**函数**就是有输入量、输出量的一套计算方案，也就是“拿什么东西做什么事情”。相对而言，面向对象过分强调“必须通过对象的形式来做事情”，而函数式思想则尽量忽略面向对象的复杂语法——**强调做什么，而不是以什么形式做**。

**面向对象的思想：**
做一件事情,找一个能解决这个事情的对象,调用对象的方法,完成事情。

**函数式编程思想：**
只要能获取到结果,谁去做的,怎么做的都不重要,重视的是结果,不重视过程。

## 1.2 冗余的Runnable代码

当需要启动一个线程去完成任务时，通常会通过`java.lang.Runnable`接口来定义任务内容，并使用`java.lang.Thread`类来启动该线程。

```java
public class RunnableDemo {

    public static void main(String[] args) {

        Runnable runnable = new Runnable() {
            @Override
            public void run() {
                System.out.println("多线程1");
            }
        };

        //启动线程
        new Thread(runnable).start();

    }
}
```

## 1.3 Lambda的更优写法

Java 8的全新语法，上述`Runnable`接口的匿名内部类写法可以通过更简单的Lambda表达式达到等效:

```java
public class ThreadDemo {

    public static void main(String[] args) {

        new Thread(()-> System.out.println("lambad初体验")).start();
    }
}
```

## 1.4 Lambda标准格式

* 一些参数
* 一个箭头
* 一段代码

Lambda表达式的**标准格式**为：

```java
(参数类型 参数名称) ‐> { 代码语句 }
```

**格式说明：**

* 小括号内的语法与传统方法参数列表一致：无参数则留空;多个参数则用逗号分隔。
* `->`是新引入的语法格式，代表指向动作。
* 大括号内的语法与传统方法体要求基本一致。

### 1.4.1 Lambda标准格式(无参无返回)

```java
public interface Cook {

    void makeFood();
}
```

```java
public class InvokeCook {

    public static void main(String[] args) {

        invokeCook(()-> System.out.println("吃饭！！！"));
    }

    private static void invokeCook(Cook cook) {
        cook.makeFood();
    }
}
```

### 1.4.2  Lambda的有参和返回值

```java
public class Person {

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

```java
public class ComparatorLambda {

    public static void main(String[] args) {

        Person arr[] = {
                new Person("二牛", 10),
                new Person("大朗", 21),
                new Person("狗剩", 19)};

        Arrays.sort(arr, (Person a, Person b) -> {
            return a.getAge() - b.getAge();
        });

        for (Person person : arr) {

            System.out.println(person);
        }
    }
}
```

### 1.4.3 Lambda省略格式

1. 小括号内参数的类型可以省略
2. 如果小括号内**有且仅有一个参**，则小括号可以省略
3. 如果大括号内**有且仅有一个语句**，则无论是否有返回值，都可以省略大括号、return关键字及语句分号

### 1.4.4 Lambda的使用前提

1. 使用Lambda必须具有接口，且要求**接口中有且仅有一个抽象方法**。无论是JDK内置的`Runnable`，`Comparator`接口还是自定义的接口，只有当接口中的抽象方法存在且唯一时，才可以使用Lambda。
2. 使用Lambda必须具有**上下文推断**。也就是方法的参数或局部变量类型必须为Lambda对应的接口类型，才能使用Lambda作为该接口的实例。

> 有且仅有一个抽象方法的接口，称为“**函数式接口**”。

