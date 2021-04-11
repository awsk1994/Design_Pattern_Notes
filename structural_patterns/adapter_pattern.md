# 适配器模式（Adapter Pattern)
 - 定义：
   - 将一个类的接口转换成客户希望的另外一个接口，使得原本由于接口不兼容而不能一起工作的那些类能一起工作。
 - 主要解决在软件系统中，常常要将一些"现存的对象"放到新的环境中，而新环境要求的接口是现对象不能满足的。
 - 分为**类结构型**模式和**对象结构型**模式两种
   - 前者类之间的耦合度比后者高，且要求程序员了解现有组件库中的相关组件的内部结构，所以应用相对较少些。
   - 由于在 java 中不支 持多重继承，而且继承有破坏封装之嫌，众多的书中(包括《设计模式》)都提倡使用组合来代替继承
 - 例子：
   - 在 LINUX 上运行 WINDOWS 程序
   - JAVA 中的 jdbc

## 优缺点 （TODO）
 - 优点
   - 客户端通过适配器可以透明地调用目标接口。
   - 复用了现存的类，程序员不需要修改原有代码而重用现有的适配者类。
   - 将目标类和适配者类解耦，解决了目标类和适配者类接口不一致的问题。
   - 在很多业务场景中符合开闭原则。
 - 缺点
   - 适配器编写过程需要结合业务场景全面考虑，可能会增加系统的复杂性。
   - 增加代码阅读难度，降低代码可读性，过多使用适配器会使系统代码变得凌乱。

## 角色

 - 目标（Target）接口：定义 Client 使用的接口。
 - 适配者（Adaptee）类：这个角色有一个已存在并使用了的接口，而这个接口是需要我们适配的。
 - 适配器（Adapter）类：这个适配器模式的核心；转换器。它将被适配角色已有的接口转换为目标角色希望的接口。

## 实现

### 类适配器模式

<img src="./img/adapter_pattern_diagram_class.gif" height="200px"/>

```java
package adapter;
//目标接口
interface Target
{
    public void request();
}

//适配者接口
class Adaptee
{
    public void specificRequest()
    {       
        System.out.println("适配者中的业务代码被调用！");
    }
}

//类适配器类
class ClassAdapter extends Adaptee implements Target
{
    public void request()
    {
        specificRequest();
    }
}

//客户端代码
public class ClassAdapterTest
{
    public static void main(String[] args)
    {
        System.out.println("类适配器模式测试：");
        Target target = new ClassAdapter();
        target.request();
    }
}
```

```
类适配器模式测试：
适配者中的业务代码被调用！
```

### 对象适配器模式

<img src="./img/adapter_pattern_diagram_object.gif" height="200px"/>

```java
package adapter;

//适配者接口
class Adaptee
{
    public void specificRequest()
    {       
        System.out.println("适配者中的业务代码被调用！");
    }
}

//对象适配器类
class ObjectAdapter implements Target
{
    private Adaptee adaptee;
    public ObjectAdapter(Adaptee adaptee)
    {
        this.adaptee = adaptee;
    }
    public void request()
    {
        adaptee.specificRequest();
    }
}

//客户端代码
public class ObjectAdapterTest
{
    public static void main(String[] args)
    {
        System.out.println("对象适配器模式测试：");
        Adaptee adaptee = new Adaptee();
        Target target = new ObjectAdapter(adaptee);
        target.request();
    }
}
```
```
对象适配器模式测试：
适配者中的业务代码被调用！
```

### 复杂一点的例子

```java
package adapter;
//目标：发动机
interface Motor
{
    public void drive();
}
//适配者1：电能发动机
class ElectricMotor
{
    public void electricDrive()
    {
        System.out.println("电能发动机驱动汽车！");
    }
}
//适配者2：光能发动机
class OpticalMotor
{
    public void opticalDrive()
    {
        System.out.println("光能发动机驱动汽车！");
    }
}
//电能适配器
class ElectricAdapter implements Motor
{
    private ElectricMotor emotor;
    public ElectricAdapter()
    {
        emotor=new ElectricMotor();
    }
    public void drive()
    {
        emotor.electricDrive();
    }
}
//光能适配器
class OpticalAdapter implements Motor
{
    private OpticalMotor omotor;
    public OpticalAdapter()
    {
        omotor=new OpticalMotor();
    }
    public void drive()
    {
        omotor.opticalDrive();
    }
}
//客户端代码
public class MotorAdapterTest
{
    public static void main(String[] args)
    {
        System.out.println("适配器模式测试：");
        Motor motor=(Motor)ReadXML.getObject();
        motor.drive();
    }
}
```

```java
package adapter;
import javax.xml.parsers.*;
import org.w3c.dom.*;
import java.io.*;
class ReadXML
{
    public static Object getObject()
    {
        try
        {
            DocumentBuilderFactory dFactory=DocumentBuilderFactory.newInstance();
            DocumentBuilder builder=dFactory.newDocumentBuilder();
            Document doc;                           
            doc=builder.parse(new File("src/adapter/config.xml"));
            NodeList nl=doc.getElementsByTagName("className");
            Node classNode=nl.item(0).getFirstChild();
            String cName="adapter."+classNode.getNodeValue();   // !!: Here, we add adapter. so fetch the class adapter
            Class<?> c=Class.forName(cName);
              Object obj=c.newInstance();
            return obj;
         }  
         catch(Exception e)
         {
                   e.printStackTrace();
                   return null;
         }
    }
}
```

