# 第一章 File类

`java.io.File`类是文件和目录路径名的抽象表示，主要用于文件和目录的创建、查找和删除等操作。

## 1.1 构造方法

* `public File(String pathname)`：通过将给定的**路径名字符串**转换为抽象路径名来创建新的File实例。
* `public File(String parent, String child)`：从**父路径名字符串和子路径名字符串**创建新的File实例。
* `public File(File parent, String child)`：从**父抽象路径名和子路径名字符串**创建新的File实例。

## 1.2 常用方法

* `public String getAbsolutePath()`：返回此File的绝对路径名字符串。
* `public String getPath()`：将此File转换为路径名字符串。
* `public String getName()`：返回由此File表示的文件或目录的名称。
* `public long length()`：返回由此File表示的文件的长度。

**示例：**

```java
public static void main(String[] args) {

    //文件路径
    String pathname = "/Users/hechong/IdeaProjects/basic_code";

    File file = new File(pathname);

    ///Users/hechong/IdeaProjects/basic_code
    System.out.println(file.getAbsolutePath());
    ///Users/hechong/IdeaProjects/basic_code
    System.out.println(file.getPath());
    //basic_code
    System.out.println(file.getName());
    //576
    System.out.println(file.length());

}
```

## 1.3 绝对路径和相对路径

* **绝对路径**：从盘符开始的路径，这是一个完整的路径。
* **相对路径**：相对于项目目录的路径，这是一个便捷的路径，开发中经常使用。

## 1.4 判断功能的方法

* **public boolean exists()**：此File表示的文件或目录是否实际存在。
* **public boolean isDirectory()**：此File表示的是否为目录。
* **public boolean isFile()**：此File表示的是否为文件。

**示例：**

```java
public static void main(String[] args) {

    File file = new File("/Users/hechong/IdeaProjects/basic_code/a.java");

    System.out.println(file.exists());//false
    System.out.println(file.isFile());//false
    System.out.println(file.isDirectory());//false
}
```

## 1.5 创建删除功能的方法

* **public boolean createNewFile()**：当且仅当具有该名称的文件尚不存在时，创建一个新的空文件。
* **public boolean delete()**：删除由此File表示的文件或目录。
* **public boolean mkdir()**：创建由此File表示的目录。
* **public boolean mkdirs()**：创建由此File表示的目录，包括任何必需但不存在的父目录。

**示例：**

```java
public static void main(String[] args) throws IOException {

    File f1 = new File("/Users/hechong/IdeaProjects/basic_code/a.java");

    System.out.println(f1.exists());//false
    System.out.println(f1.createNewFile());//true
    System.out.println(f1.exists());//true

    File f2 = new File("/Users/hechong/IdeaProjects/basic_code/testjj");

    System.out.println(f2.exists());//false
    System.out.println(f2.mkdir());//true
    System.out.println(f2.exists());//true

    File f3 = new File("/Users/hechong/IdeaProjects/basic_code/testjj2");

    System.out.println(f3.exists());//false
    System.out.println(f3.mkdirs());//true
    System.out.println(f3.exists());//true

    System.out.println(f1.delete());//true
    System.out.println(f2.delete());//true
    System.out.println(f3.delete());//true

}
```

> Tips：
> delete方法，如果此File表示目录，则目录必须为空才能删除。

## 1.6 目录的遍历

**示例：**

```java
    public static void main(String[] args) {

        File f = new File("/Users/hechong/IdeaProjects/basic_code/FileDemo");
        result(f);

    }

    public static void result(File file) {

        File[] files = file.listFiles();

        for (File file1:files) {

            if (file1.isFile()){
                System.out.println(file1.getAbsolutePath());
            }else {
                result(file1);
            }
        }
    }
```




