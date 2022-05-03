# 第一章 XML解析

**概述**

xml解析就是从xml中获取到数据。

**常见的解析思想 **

DOM(Document Object Model)文档对象模型:就是把文档的各个组成部分看做成对应的对象。 会把xml文件全部加载到内存,在内存中形成一个树形结构,再获取对应的值。

![dom解析概述](./images/dom解析概述.png)

* **常见的解析工具**
	* JAXP: SUN公司提供的一套XML的解析的API
	* JDOM: 开源组织提供了一套XML的解析的API-jdom
	* DOM4J: 开源组织提供了一套XML的解析的API-dom4j,全称:Dom For Java
	* pull: 主要应用在Android手机端解析XML

**示例：**

```java
public class XMLDemo01 {

    public static void main(String[] args) throws DocumentException, IOException {

        // 获取一个解析器对象
        SAXReader reader = new SAXReader();

        // 利用解析器把xml文件加载到内存中,并返回一个文档对象
        Document document = reader.read(new File("./xmldemo/student.xml"));

        // 获取根标签
        Element rootElement = document.getRootElement();

        // 通过根标签来获取student标签
        List<Element> elements = rootElement.elements("student");

        ArrayList<Student> students = new ArrayList<>();

        for (Element element : elements) {
            // 获取id的属性值,然后获取id的属性值
            String id = element.attribute("id").getValue();
            // element("标签名"):获取调用者指定的子标签
            // getText获取这个标签的标签体内容
            String name = element.element("name").getText();
            String age = element.element("age").getText();
            Student s = new Student(id, name, Integer.parseInt(age));
            students.add(s);

        }

        for (Student student : students) {
            System.out.println(student);
        }
    }
}
```



