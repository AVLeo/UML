# 彻底看懂 UML 类图

>  官方解释为：类图用于描述系统中所包含的类以及它们之间的相互关系，帮助人们简化对系统的理解，它是系统分析和设计阶段的重要产物，也是系统编码和测试的重要模型依据 

## 一、基本定义

![](https://github.com/yaoxingle/UML/tree/master/images/20191024135404845.png)

>  在UML中，类使用包含类名、属性和操作且带有分隔线的长方形来表示，如定义一个Employee类，它包含属性name、age和email，以及操作modifyInfo()，在UML类图中该类如图1所示： 

![](E:\work\2020\learning\UML\images\617148-20160612221055090-339746853.jpg)

 对应的代码如下：

```java

public class Employee {
	private String name;
	private int age;
	private String email;
	
	public void modifyInfo() {
		......
	}
}
```

类图分三层，

1. 第一层显示类的名称，如果是抽象类，就用斜体显示

2. 第二层，为类的特性，通常就是字段和属性

3. 第三层是类的操作，通常是方法或者行为。


## 二、方法详解

第三层是类的操作(Operations)：操作是类的任意一个实例对象都可以使用的行为，是类的成员方法。
UML规定操作的表示方式为：

> 可见性 名称(参数列表) [ : 返回类型]

其中：

-  可见性”的定义与属性的可见性定义相同，  “ + ” 表示 public “ - ” 表示 private  “ # ” 表示 protected 。
-  名称”即方法名，用一个字符串表示。 
-  “参数列表”表示方法的参数，其语法与属性的定义相似，参数个数是任意的，多个参数之间用逗号“，”隔开。 
-  “返回类型”是一个可选项，表示方法的返回值类型，依赖于具体的编程语言，可以是基本数据类型，也可以是用户自定义类型，还可以是空类型(void)，如果是构造方法，则无返回类型。 

![](E:\work\2020\learning\UML\images\2012112312.jpg)

## 三、关系

|    关系    | 说明                                                         | 图例                                                         |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 泛化 | 继承关系，指向方(符号左)子类，被指向方(符号右)为父类。       | <img src="E:\work\2020\learning\UML\images\1589857084924.png" alt="1589857084924" style="zoom:50%;" /> |
| 实现 | 接口的实现关系，指向方（符号左）实现类，被指向方(符号右)为接口类。 | ![1589857070426](E:\work\2020\learning\UML\images\1589857070426.png)    |
| 关联 | 关联关系是类与类之间的联结，使一个类知道另一个类的属性和方法。 | ![1589857120783](E:\work\2020\learning\UML\images\1589857120783.png)    |
| 聚合 | 整体和部分的关系，指向方(符号左)整体类，被指向方(符号右)为部分类。[可以独立存在] | ![1589857235187](E:\work\2020\learning\UML\images\1589857235187.png)    |
| 组合 | 整体和部分的关系，指向方(符号左)整体类，被指向方(符号右)为部分类。如果整体没有，部分也不存在[同生共死]。 | ![1589857257757](E:\work\2020\learning\UML\images\1589857257757.png)    |
| 依赖 | 使用关系，指向方(符号左)使用类，被指向方(符号右)为被使用类   | ![1589857282633](E:\work\2020\learning\UML\images\1589857282633.png)    |



### 3.1泛化、继承关系

如下图所示：Student类与Teacher类继承了Person类 （ 非抽象类 ）。

![](E:\work\2020\learning\UML\images\617148-20160612233246199-1404301867.jpg)

代码示例：

```java
//父类
public class Person {
protected String name;
protected int age;
 
public void move() {
        ……
}
 
    public void say() {
    ……
    }
}
 
//子类
public class Student extends Person {
private String studentNo;
 
public void study() {
    ……
    }
}
 
//子类
public class Teacher extends Person {
private String teacherNo;
 
public void teach() {
    ……
    }
}
```

### 3.2实现、接口关系

如下图所示：Car类与Ship类都实现了Vehicle接口或抽象类。 

![](E:\work\2020\learning\UML\images\617148-20160612233430777-736506858.jpg)

代码示例：

```java
public interface Vehicle {
public void move();
}
 
public class Ship implements Vehicle {
public void move() {
    ……
    }
}
 
public class Car implements Vehicle {
public void move() {
    ……
    }
}
```

### 3.3关联关系

#### 3.3.1单项关联

它描述不同类的对象之间的结构关系；它是一种静态关系， 通常与运行状态无关，一般由常识等因素决定的；它一般用来定义对象之间静态的、天然的结构； 所以，关联关系是一种“强关联”的关系；

如下图所示：顾客(Customer)拥有地址(Address)，则Customer类与Address类具有单向关联关系。 

![](E:\work\2020\learning\UML\images\2012112316.jpg)

代码示例：

```java
public class Customer {
private Address address;
……
}
 
public class Address {
……
}
```

#### 3.3.2双向关联

如下图所示：顾客(Customer)购买商品(Product)并拥有商品，反之，卖出的商品总有某个顾客与之相关联。因此，Customer类和Product类之间具有双向关联关系 

![](E:\work\2020\learning\UML\images\2012112315.jpg)

代码示例：

```java
public class Customer {
private Product[] products;
……
}
 
public class Product {
private Customer customer;
……
}
```

#### 3.3.3自关联

如下图所示：Node类包含类型为Node的成员变量，也就是“自己包含自己”。  

![](E:\work\2020\learning\UML\images\2012112317.jpg)

### 3.4聚合关系

如下图所示：汽车发动机(Engine)是汽车(Car)的组成部分，但是汽车发动机可以独立存在，因此，汽车和发动机是聚合关系 。

![](E:\work\2020\learning\UML\images\2012112319.jpg)

在代码实现聚合关系时，成员对象通常作为构造方法、Setter方法或业务方法的参数注入到整体对象中

代码如下：

```java
public class Car {
	private Engine engine;
 
    //构造注入
	public Car(Engine engine) {
		this.engine = engine;
	}
    
    //设值注入
    public void setEngine(Engine engine) {
        this.engine = engine;
    }
    ……
}
 
public class Engine {
	……
}
```

### 3.5组合关系

如下图所示：人的头(Head)与嘴巴(Mouth)，嘴巴是头的组成部分之一，而且如果头没了，嘴巴也就没了，因此头和嘴巴是组合关系 。

![](E:\work\2020\learning\UML\images\20121123110.jpg)

代码如下：

```java
public class Head {
	private Mouth mouth;
 
	public Head() {
		mouth = new Mouth(); //实例化成员类
	}
……
}
 
public class Mouth {
	……
}
```

3.6依赖关系

 如下图所示：Driver的drive方法只有传入了一个Car对象才能发挥作用，因此我们说Driver类依赖于Car类。 

![](E:\work\2020\learning\UML\images\617148-20160612232951746-9292157.jpg)
