//   >>有符号右移

//  >>>无符号右移

**求数组长度：使用length，length是数组的属性不是方法.**

**求字符串长度，用length()，返回值是char数组的长度**

**求容器的大小，用size（）**

------

**可变参数**

```java
public static int sum(int ...numbers){}
```

可变参数必须是方法最后的一个参数

#### 栈帧

*栈帧随着方法的调用而被创建，随方法的结束而销毁，存储了方法的局部变量信息*

##### java对象数组的内存存储

```java
objects []ob = new objects[10];
```

数组ob指向堆空间中开辟的一段连续的、储存地址值的空间

（即，对象数组储存的是新new出的对象的地址）

#### this

*this本质是一个隐藏的，位置最靠前的方法参数*

构造方法中执行同一类的其他构造方法时，用**this**替换方法名：

```java
public Cat(String name,int age){
	this.name=name;
	this.age=age;
}
public Cat(String name){
	this(name,0);
}
```

### 构造方法

构造方法中调用同一类的其他构造方法时，用**this**替换方法名，且构造方法必为第一条语句

子类调用构造方法时会先调用父类构造方法

不创造构造方法编译器自动创建无参构造函数

若子类构造方法没有显式调用构造方法，编译器将自动调用父类无参构造方法

### 访问控制

![image-20220429110753459](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220429110753459.png)  

**即使使用private修饰父类成员变量，子类中内存依旧存在该被修饰成员变量**

**访问控制只是编译器做的限制**

上述四个访问控制符无法修饰局部类、局部变量（“局部”即方法中定义的）

只有public\无修饰符可以修饰顶级类

## 嵌套类：

> 定义在“类”中的类

```java
public class A{//顶级类，B与C的外部类
	public class B{//C的外部类，A的内部类
		public class C{//A与B的内部类
		
		}
	}
}
```

**能使用静态嵌套类就使用静态嵌套类，尽量不用非静态嵌套类**

**所有内部类被销毁后才能销毁外部类**

### 内部类：（非静态嵌套类）

没有被static修饰的嵌套类

**创建对象时会自动、隐式地创建一个指向外部类的引用型成员变量**（内部类可直接访问外部类原因）

 ![image-20220507222545028](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220507222545028.png)

#### ***内部类实例应与外部类实例相关联：***

**需要先创建外部类实例，再由外部类实例创建内部类实例**

**内部类无法定义除编译时常量以外的任何static成员**

内部类可直接访问外部类所有成员（即使声明为private）

外部类可以直接访问内部类实例的成员变量、方法（即使声明为private）

### 静态嵌套类

> 被static修饰的嵌套类

**静态嵌套类在行为上相当于一个顶级类，只是定义的代码写在了另一个类中**

与顶级类相比，静态嵌套类多了一些特殊权限：

可直接访问外部类成员（即使被声明为private）

#### 继承内部类、静态嵌套类

> 内部类的继承上也需要外部类的协助：

```java
class WithInner{    
	class Inner{    
    } 
}  
public class test3 extends WithInner.Inner{    
    test3(WithInner wi){        
        wi.super();    
    }    
    public static void main(String[] args){        
        WithInner wi = new WithInner();    
        test3 t3 = new test3(wi);   
    }
}
```

**构造时注意：**

构造方法应注意调用**所属外部类构造方法**，且应含有所属外部类引用形参

#### 使用嵌套类的情况：

![image-20220507224401166](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220507224401166.png)

![image-20220507224431202](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220507224431202.png)

![image-20220507224529973](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220507224529973.png)

### 注解

@Override   *重写方法注解*

@SuppressWarnings("警告类别")    *使编译器不生成某类警告信息*

### 重写

*子类可重写父类方法*

子类重写方法访问控制符应大于或等于父类访问控制符权限

子类重写方法返回值应小于或等于父类方法返回值

### 方法签名**（Method Signature）**

方法签名由 2 部分组成：方法名、参数类型

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221106163722815.png" alt="image-20221106163722815" style="zoom:67%;" />

> 该段代码方法签名为sum(int, long, double)

**在同一个类中，不能定义 2 个方法签名一样的方法**

### 重载**（Overload）**

- Java 的方法支持重载：方法名相同，方法签名不同

- 重载与返回值类型、参数名称无关

## static

*可修饰成员变量，方法，内部类*

所有类对象共同占用一段固定内存（存储在方法区，无static修饰的储存在堆空间，**jdk1.8后储存在堆中**）

被修饰变量，方法，类被称为静态~~、类~

## 静态方法

静态方法（类方法）可通过实例对象或类名访问

*静态方法内部不可使用 this访问*

可直接访问类变量、类方法（**静态**）

不能直接访问实例变量，实例方法

*实例方法可直接访问静态变量与静态方法以及实例变量与实例方法*

*同一类中不能有同名的实例变量与类变量*，*不能有相同方法签名的实例方法与类方法*

## 静态导入

> import static 地址

*静态导入后，可省略类名直接访问类变量、类方法与嵌套类*

![image-20220503110223468](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220503110223468.png)

**嵌套类原访问方式：**

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220503110706890.png" alt="image-20220503110706890" style="zoom:50%;" />

**静态导入后嵌套类访问方式：**

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220503110824177.png" alt="image-20220503110824177" style="zoom:50%;" />

# 初始化

## 成员变量初始化

> 系统会自动为成员变量初始化（未初始化时），赋值为：0、false、null

### 手动为实例变量提供初始值

1.在声明时

> public int a = 1;

2.在构造方法中

3.在**初始化代码块**中（初始化块）

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220503113354755.png" alt="image-20220503113354755" style="zoom: 67%;" />

## 初始化块

**编译器会自动将初始化块中的代码复制到构造方法头部**

可有多个初始化块，编译器会按源码中出现顺序执行

#### 手动为类变量提供初始值

1.在声明时

> public static int a = 1;

2.在静态初始化块中

 ![image-20220503114746448](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220503114746448.png)

## 静态初始化块

##### 当一个类初始化时执行静态初始化块

> 当一个类**第一次**被主动使用时（先初始化父类），jvm会对类执行初始化

**可有多个静态初始化块，编译器会按源码中出现顺序执行**

## 单例模式

> 单例模式下，一个类只能创建一个实例（对象）

### 单例创建方式：

#### 饿汉式单例模式：  *推荐*

![image-20220503161432574](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220503161432574.png)

#### 懒汉式单例模式：（优点：延时加载        缺点：无法保证线程安全）*不推荐*

![image-20220503163649033](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220503163649033.png)

#### 懒汉式单例模式（改进）：

![image-20221016193912620](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016193912620.png)

## **双括号初始化（Double Brace Initialization）** 

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221106172354241.png" alt="image-20221106172354241" style="zoom:67%;" />

- 优点
  - 代码简洁

- ◼缺点
  - 本质是使用初始化块生成了一个匿名类（继承自构造方法所属类）
  - 可能会影响 equals 方法的正常使用

- 建议慎重使用

# final

1**.被final修饰的类无法被继承**

2.被final修饰的方法无法被重写

3.被final修饰的变量只能被赋值1次

##### **常量**

1.java中的常量一般指代被static final修饰的变量

2.常量名称一般全部使用大写字母表示

3.**常量**为**基本类型或字符串**时，且在**编译时就能决定值**时：

编译器会使用常量值代替各处的常量名（类似c宏替换）

一般称之为编译时常量

#### **由于编译时常量不依赖于类，所以对编译时常量的访问不会引发类的初始化。**

# 局部类

**定义在代码块{}内的类（如方法、for、if 中）**

1. 局部类不能定义除编译时常量以外的任何 static 成员

2. 局部类只能访问**final**或**有效final**的局部变量

   > 从 Java 8 开始，如果局部变量没有被第二次赋值，就认定为是有效 final

3. 局部类可以直接访问外部类中的所有成员（即使被声明为 private）

局部类只有定义在实例相关的代码块(**不被static修饰**）中，才能直接访问外部类中的**实例成员**（实例变量、实例方法）

# 抽象

> 被abstract修饰

#### 抽象方法

> 被abstract修饰的实例方法

- 只有方法声明，没有方法实现（参数列表后面没有大括号，而是分号）
- 不能是 private 权限（因为定义抽象方法的目的让子类去实现）
- 只能定义在抽象类、接口中

#### 抽象类

> 被 abstract 修饰的类

- 可以定义抽象方法
- 方法无法实例化（实例化交由子类实行）可自定义构造方法（只有方法声明）
- 子类必须实现抽象父类中的所有抽象方法（除非子类也是一个抽象类）
- 可以像非抽象类一样定义成员变量、常量、嵌套类型、初始化块、非抽象方法等

> 也就是说，抽象类也可以完全不定义抽象方法

![image-20220507232814759](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220507232814759.png)

# 接口

> 一系列方法声明的集合
>
> 用来定义规范、标准
>
> 通过implement关键字实现一个或多个接口

![image-20220508175217143](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220508175217143.png)

> 个人理解：引用为接口时相当于使用符合接口“规定”的类部分实例，类似投影与物体的关系

1.可以定义抽象方法，常量，嵌套类，Java8开始可定义：默认方法、静态方法（类方法）

**2.上述定义内容都是隐式public，可省略public**

3.Java9开始可定义private方法

4.不能自定义构造方法、不能定义（静态）初始化块、**不能实例化**

5.常量可以省略 static、final

6.抽象方法可以省略 abstract

7.实现接口的类必须实现接口中定义的全部抽象方法（抽象类除外）

8.可同时使用extends 和 implements，implements 必须写在 extends 的后面

9.如果一个类实现的多个接口中有相同的抽象方法，只需实现此方法一次

10. 一个接口可以通过 extends 关键字继承一个或者多个接口

**接口名称使用在类型名称位置**

**当父类、接口中的方法签名一样时，那么返回值类型也必须一样**

## 默认方法

> 以default修饰默认方法

- 默认方法只能是实例方法
- 当一个类实现的接口中有默认方法时
  - 沿用接口中默认实现
  - 接口实现类可重写接口中默认方法，优先调用重写后方法（接口实现类覆盖了默认方法）
  - 接口实现抽象类可以将接口中默认方法重新声明为抽象方法
- 当一个接口继承父接口中有默认方法时
  - 沿用父接口中默认实现
  - 子接口可重写默认方法，优先调用重写后方法（子接口覆盖了默认方法）
  - 子接口可以将父接口默认方法重新声明为抽象方法

**父类非抽象方法比接口中默认方法调用优先级高**

![image-20220510233649879](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220510233649879.png)

**父类抽象方法比接口中默认方法调用优先级高**

如果父类定义的抽象方法与接口的默认方法相同时，要求子类实现此抽象方法

- 可以通过 super 关键字调用接口的默认方法

![image-20220510233933498](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220510233933498.png)

**如果父接口定义的默认方法与其他父接口定义的方法相同时，要求子接口（实现类）实现此默认方法**

![image-20220510234348072](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220510234348072.png)

- **当父接口的父父接口的默认方法与其他父接口定义的方法相同时，不需子接口（实现类）实现此默认方法**

*程序不会执行该继承的默认方法*

![image-20220510234907615](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220510234907615.png)

## 静态方法

- 接口中定义的静态方法只能通过接口名调用，**不能被继承**

![image-20220510235111001](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220510235111001.png)

# 多态

> 同一操作作用于不同对象，产生不同的执行结果

- 父类（接口）引用类型指向子类对象
  - 会调用子类重写的方法（实例方法，类方法不会）
- **成员变量与类方法一样，调用时只看所属类，不会调用子类**

![image-20220511141658778](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511141658778.png)

**jvm会根据引用类型所指向的具体对象来调用相对应方法**（实例方法）

> 虚方法调用

### instanceof关键词使用

判断某种类型是否属于某种类型

![image-20220511143002146](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511143002146.png)

**具体应用**

![image-20220511143031459](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511143031459.png)

# 匿名类

> 匿名类属于是使用一次即丢弃的工具类

**接口与抽象类的实现**

当接口、抽象类的实现类，在整个项目中只用过一次，可以考虑使用匿名类

### 使用方式

**示例**1

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220717135951286.png" alt="image-20220717135951286" style="zoom:67%;" />

**示例**2

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220717140100290.png" alt="image-20220717140100290" style="zoom:67%;" />

*抽象类、接口的特殊实现？*

*单一实现类*

#### 注意

1. 匿名类不能定义除编译时常量以外的任何 static 成员
2. 匿名类只能访问**final**或**有效final**的局部变量
3. 匿名类可以访问外部类中的所有成员（即使被声明为private）
4. 匿名类只有定义在实例相关的代码块(**不被static修饰**）中，才能直接访问外部类中的**实例成员**（实例变量、实例方法）
5. 无构造方法，但有初始化块

### 用途、使用

##### 代码传递

##### 过滤器

##### 回调

## Lambda表达式

> 匿名类实现的是函数式接口时，可使用lambda表达式简化
>
> 但有区别：
>
> 当外部有变量与传入参数同名时判定为重复定义（lambda)
>
> 而匿名类允许重复
>
> this访问的区别：lambda表达式会访问lambda表达式所属类下成员
>
> **匿名类是一个类**，会访问匿名类下成员

### 函数式接口

*只包含1个抽象方法的接口*

#### **函数式接口注解：**

```Java
@FunctionalInterface
```

```java
(参数列表) ->{
	...//方法实现
	return ...// 返回值
}
```

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220718222032891.png" alt="image-20220718222032891" style="zoom:67%;" />

1. 参数列表可以省略参数类型
2. 内部只有一句语句可以省略大括号、分号、return

```java
() -> ...;
```

3. 只有一个参数可以省略小括号
4. 无参数时不能省略小括号和箭头

### 常用函数式接口

#### Supplier

传递数据，避免代码浪费执行，（将部分代码放在supplier的get方法中，延迟执行，可能会无需执行）

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221012232030204.png" alt="image-20221012232030204" style="zoom:67%;" />

#### **Consumer**

传入参数，在内部accept方法中实现（forEach）

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221012232012985.png" alt="image-20221012232012985" style="zoom:67%;" />

- andThen默认方法
  - 继续实现下一个Consumer接口的accept方法

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221012231911649.png" alt="image-20221012231911649" style="zoom:67%;" />

#### **Predicate**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221012231952242.png" alt="image-20221012231952242" style="zoom:67%;" />

> 判断接口

传入参数，在内部进行判断，传出布尔值

- and方法：&&
- or方法：||
- negate方法：取反

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221012232435592.png" alt="image-20221012232435592" style="zoom:67%;" />

#### **Function**

![image-20221012232525369](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221012232525369.png)

接受参数，内部实现，传出结果

- apply方法（具体实现）
- andThen
  - 继续实现下一个Function接口的apply方法
- compose方法
  - 将上一个Function的apply方法的结果作为参数接收到该Function的apply方法

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221012233221668.png" alt="image-20221012233221668" style="zoom:67%;" />



## 方法引用

>  若lambda表达式**仅**用来**调用某个方法**，可使用”方法引用“简化

![s](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220731150751337.png)

# 正则表达式 Regex Expression

### 单字符匹配 []

在字符串相应位置：

[...]内字符出现且仅出现一个

[^...]除出现字符以外任意一个

[...-...]...到...出现的字符

![image-20220827140338769](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220827140338769.png)

### 预定义字符

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002141403336.png" alt="image-20221002141403336" style="zoom:67%;" />

◼ 以 1 个反斜杠开头的字符会被当做转义字符处理

因此，为了在正则表达式中完整地表示预定义字符，需要以 2 个反斜杠开头，比如"\\\d"

#### 使用示例

![image-20220919141735939](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220919141735939.png)

### 量词

> X指定出现多少次

![image-20220919141945698](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220919141945698.png)

#### 示例

![image-20220919142001693](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220919142001693.png)

### **Matcher 常用方法**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002150146833.png" alt="image-20221002150146833" style="zoom: 67%;" />

> group输入捕获组编号也可传出捕获组内容

### 贪婪、勉强、独占

-  贪婪
  - 先吞掉整个 input 进行匹配
  - 若匹配失败，则吐出最后一个字符
  - 然后再次尝试匹配，重复此过程，直到匹配成功
- 勉强
  - 先吞掉 input 的第一个字符进行匹配
  - 若匹配失败，则再吞掉下一个字符
  - 然后再次尝试匹配，重复此过程，直到匹配成功
- 独占
  - 吞掉整个 input 进行唯一的一次匹配

### 捕获组

> 捕获组就是把正则表达式中子**表达式匹配的“内容”**，保存到内存中以数字编号或显式命名的组里，方便后面引用。这种引用既可以是在正则表达式内部，也可以是在正则表达式外部。
>
> (){x} 指定()内内容重复x次

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221001190421819.png" alt="image-20221001190421819" style="zoom:80%;" />

#### 反向引用（Backreference） 

> 可以使用反斜杠（\）+ 组编号（从 1 开始计数）来引用组的内容

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221001193200645.png" alt="image-20221001193200645" style="zoom:80%;" />

### **边界匹配符（ Boundary Matcher）**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002135308555.png" alt="image-20221002135308555" style="zoom:67%;" />

> 使用^、$需要开启多行模式

- **终止符**
  - \r、\n、\r\n
- **输入**
  - 指代整个字符串
- **一行**
  - 以终止符（或整个输入的结尾）结束的字符串片段

#### 单词？（\b\B）

> 英文大小写、阿拉伯数字、下划线、其他国家文字认为是此处“单词”含义

#### 示例

![image-20221002134842377](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002134842377.png)

![image-20221002134856394](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002134856394.png)

### 常用模式

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002140737607.png" alt="image-20221002140737607" style="zoom:67%;" />

DOTALL代表.(点号)可以匹配任意字符（本来点号无法匹配\r、\n）

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002140856500.png" alt="image-20221002140856500" style="zoom:50%;" />

#### 示例

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002141952001.png" alt="image-20221002141952001" style="zoom:67%;" />

正则表达式在线测试

https://c.runoob.com/front-end/854

#### String 类中接收正则表达式作为参数的常用方法：

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002142920636.png" alt="image-20221002142920636" style="zoom: 67%;" />

> String.replace无法接收正则，String.replaceAll可以
>
> replaceAll替换全部，replaceFirst只替换第一个
>
> split依据传入可匹配正则的字符串分割字符串传出字符串数组

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002144847100.png" alt="image-20221002144847100" style="zoom: 67%;" />



# 泛型

> 将类型变为参数，提高代码复用率

####  

## 泛型类型

> 使用了泛型的类或接口

**称<>中为类型参数**

#### **使用：**

添加类型占位符

![image-20220511151558516](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511151558516.png)

![image-20220511151743781](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511151743781.png)

#### **细节**

- Java7开始后，可以省略“右边”<>中的类型

![image-20220511152145795](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511152145795.png)

#### 泛型类型的类型参数只能用在实例方法与构造方法下，无法用在静态方法中

### 泛型类型的继承

- 所有泛型类型继承自object

- 泛型类型与普通的数据类型继承关系不同
- 子类可扩展泛型类型

![image-20220511154223682](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511154223682.png)

![image-20220511154256173](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511154256173.png)

## 原始类型

没有传递具体的类型给泛型的类型参数

![image-20220511190702826](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220511190702826.png)

- 使用原始类型编译器会给出rawtypes警告（可以用@SuppressWarnings消除）
- 将非原始类型赋值给原始类型时，编译器没有任何警告和错误
- 将原始类型赋值给非原始类型时，编译器会给出unchecked警告（可以用@SuppressWarnings消除）
- Box 是原始类型，Box<Object> 是非原始类型

## 泛型方法

独立使用了泛型的方法（非泛型类型的类或接口下使用了泛型的方法）（实例方法、静态方法、构造方法）

使用时应在返回值类型左侧添加泛型标识

e.g.![image-20221005195540090](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221005195540090.png)

泛型类型下使用其泛型的方法没有<>

## 类型推断

编译器可以根据输入值与返回值来推断泛型的具体类型

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221005201543022.png" alt="image-20221005201543022" style="zoom:67%;" />

## 限制类型参数

- 可以通过extends对泛型类型参数增加一些限制条件，如：<T extends A>

- extends后面可以跟类名、接口名，第一个必须为类名（且类名只能有一个）后面为接口名

  <T extends A &B &C>代表类型T必须是A类型或继承、实现A,实现B,实现C

![image-20221007144255737](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221007144255737.png)

示例+比较器的使用

![image-20221007151912860](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221007151912860.png)

## 泛型使用限制

- 基本类型不能做类型参数
- 无法构造类型参数实例，但可通过传入该泛型类型的Class对象使用Class的内部getInstance()方法获取实例
- 不能定义类型为类型参数的静态变量，也不能使用在静态方法上（static）
- 类型参数不能使用在instanceof中
- 不能创建带有类型参数的数组
- 泛型中不同的类型参数不构成重载
- 不能定义泛型的异常类（继承Exception）（但类型参数可以继承Exception）
- catch中的异常类型不能使用类型参数，但throws 可以

## 通配符——?

> 在泛型中，问号（?）被称为是通配符

- 通常用作变量类型、返回值类型的类型参数

- 不能用作泛型方法调用、泛型类型实例化、泛型类型定义的类型参数

### 上界

> 可以通过 extends 设置类型参数的上界

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221007153903400.png" alt="image-20221007153903400" style="zoom:67%;" />

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221007153957834.png" alt="image-20221007153957834" style="zoom:67%;" />

### 下界

> 可以通过 super 设置类型参数的下界

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221007154038567.png" alt="image-20221007154038567" style="zoom:67%;" />

### 无限制

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221007163554447.png" alt="image-20221007163554447" style="zoom:67%;" />

# 集合

> java.util 包中有个集合框架（Collections Framework），提供了一大堆常用的数据结构

ArrayList、LinkedList、Queue、Stack、HashSet、HashMap 等 

![image-20221013195337091](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013195337091.png)

## ArrayList

> java中的动态数组
>
> 非线程安全

### 常用方法

![image-20221002160638154](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221002160638154.png)

retainAll(list) 删掉除list中元素以外的全部元素

### 遍历注意

- 使用迭代器、forEach 遍历集合元素时，若使用了集合自带的方法修改集合的长度（比如 add、remove 等方法）
  - 那么会抛出 java.util.ConcurrentModificationException 异常

- 如果希望在遍历元素的同时删除元素
  - 请使用 Iterator 进行遍历
  - 然后使用 Iterator 的 remove 方法删除元素

#### **ListIterator**

> ListIterator 继承自 Iterator，在 Iterator 的基础上增加了一些功能，辅助list进行遍历时的其他操作

![image-20221005194919797](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221005194919797.png)

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221005194939624.png" alt="image-20221005194939624" style="zoom:67%;" />

## LinkedList

> 类

- LinkedList 是一个双向链表
  - 实现了 List 接口
  - API 跟 ArrayList 类似

### 与ArrayList不同操作的效率对比

> ArrayList性能主要消耗在元素的移动上
>
> LinkedList性能主要消耗在元素遍历查找上

- 1-查找元素
  - ArrayList:效率高LinkedList:效率低
- 2-往尾部添加元素
  - ArrayList、 LinkedList的效率都比较高
- 3-往头部添加元素
  - ArrayList:效率低LinkedList:效率高
- 4-往任意位置添加元紊
  - ArrayList、LinkedList的效率差不多
- 5-删除尾部元素
  - ArrayList、 LinkedList的效率都比较高
- 6-删除头部元素
  - ArrayList:效率低LinkedList:效率高
- 7-删除任意位置元素
  - ArrayList、LinkedList的效率差不多

#### ArrayList与LinkedList的不同效率优势

#### ArrayList优势

- 查找元素
- 尾部添加元素
- 删除尾部元素

#### LinkedList的优势

- 尾部添加元素
- 头部添加元素
- 删除尾部元素
- 删除头部元素

### ArrayList与LinkedList的内存方面差别

#### ArrayList内存方面优势

- ArrayList不会频繁申请、销毁内存空间

#### ArrayList内存方面劣势

- 会占用无用内存（较大量），造成内存浪费（缩容解决）

#### LinkedList内存方面优势

- 不会占用无用内存

#### LinkedList内存方面劣势

- LinkedList会频繁申请、销毁内存空间

### 添加删除操作选择LinkedList、查询操作选择ArrayList

## Stack

> “栈”与内存中的“栈空间”是两个不同的概念

- Stack，译为“栈”，只能在一端进行操作
  - 往栈中添加元素的操作，一般叫做 push，入栈
  - 从栈中移除元素的操作，一般叫做 pop，出栈（只能移除栈顶元素，也叫做：弹出栈顶元素）
  - 后进先出的原则，Last In First Out，LIFO

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013181402844.png" alt="image-20221013181402844" style="zoom:67%;" />

### **Stack – 常用方法**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013184350047.png" alt="image-20221013184350047" style="zoom: 67%;" />

## **Queue**

> java.util.Queue 是一个接口，它的常用实现是 LinkedList

- Queue，译为“队列” ，只能在头尾两端进行操作
  - 队尾（rear）：只能从队尾添加元素，一般叫做 入队
  - 队头（front）：只能从队头移除元素，一般叫做 出队
  - 先进先出的原则，First In First Out，FIFO

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013185859046.png" alt="image-20221013185859046" style="zoom:67%;" />

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013190007205.png" alt="image-20221013190007205" style="zoom:67%;" />

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013190023765.png" alt="image-20221013190023765" style="zoom:67%;" />

## HashSet

> 实现了Set接口

- 打印顺序与哈希值与添加顺序有关

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013194801696.png" alt="image-20221013194801696" style="zoom:67%;" />

### 遍历

> 与打印顺序一致

无法通过for i循环实现（set无索引）

- 通过迭代器遍历

   <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013192013073.png" alt="image-20221013192013073" style="zoom:67%;" />

- 使用forEach方法

### 常用方法

- add()
- remove()
- size()
- forEach()

## LinkedHashSet

> LinkedHashSet 在 HashSet 的基础上，记录了元素的添加顺序
>
> (打印顺序与添加顺序一致)

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013194736032.png" alt="image-20221013194736032" style="zoom:67%;" />

## TreeSet

> TreeSet 要求元素必须具备**可比较性**，**默认按照从小到大的顺序遍历元素**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013192742427.png" alt="image-20221013192742427" style="zoom:67%;" />

### 自定义比较方式

> 在构造方法中传入一个比较器

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013192926174.png" alt="image-20221013192926174" style="zoom:67%;" />

## HashMap

> HashMap 存储的是键值对（key-value），Map 译为“映射”，有些编程语言中叫做“字典”
>
> 可以存储重复value，但不能存重复key
>
> 

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013195005054.png" alt="image-20221013195005054" style="zoom:67%;" />

### 常用方法

- put()
  - put(value,key)
  - 在put中传入已有key会把新value将旧value覆盖掉
- size()
- get()
- remove()

### 遍历

- map.entrySet()方法**（推荐）**
  - entry类：entry代表键值对，一个entry代表一对键值对
  - map.entrySet()方法会返回一个set对象，将所有键值对保存进去
  - 之后通过遍历这个set对象完成遍历

![image-20221013201000223](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013201000223.png)

- map.forEach()方法**（推荐）**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013201122092.png" alt="image-20221013201122092" style="zoom:67%;" />

- map.values()（效率也不错）
  - 返回一个Collection对象，然后遍历这个Collection对象完成遍历

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013201346283.png" alt="image-20221013201346283" style="zoom:67%;" />

- map.keySet()（不推荐）
  - 通过map.keySet()获得一个set对象，存储有key值
  - 然后通过遍历key，得到value（效率低）

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013201824603.png" alt="image-20221013201824603" style="zoom:67%;" />

## LinkedHashMap

> LinkedHashMap 在 HashMap 的基础上，记录了元素的添加顺序

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013213102420.png" alt="image-20221013213102420" style="zoom:67%;" />

## TreeMap

> TreeMap 要求 key 必须具备可比较性，**默认按照从小到大的顺序遍历key**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013213327368.png" alt="image-20221013213327368" style="zoom:67%;" />

## **List Set Map的不同特点**

- List 的特点
  - 可以存储重复的元素
  - 可以通过索引访问元素

- Set 的特点
  - 不可以存储重复的元素
  - 不可以通过索引访问元素

- Map 的特点
  - 不可以存储重复的 key，可以存储重复的 value
  - 不可以通过索引访问 key-value

- **Set 的底层是基于 Map 实现的**
  - HashSet 底层用了 HashMap
  - LinkedHashSet 底层用了 LinkedHashMap
  - TreeSet 底层用了TreeMap

## **Collections**

> java.util.Collections 是一个常用的**集合工具类**，提供了很多实用的静态方法

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221013220045613.png" alt="image-20221013220045613" style="zoom:67%;" />

- addAll
  - 将元素全部添加到一个Collection中
- reverse
  - 将List反置
- reverseOrder
  - 提供一个比较器供给sort使用，进行倒序排序
- shuffle()
  - 打乱传入List的元素顺序
- swap()

  - 依据序列号交换List成员
- fill()
  - 用某个参数填满List
- copy()
  - 将?extends传给?super

# 迭代器

## Iterator与Iterable接口

iterator为Java中的迭代器对象，是能够对List这样的集合进行迭代遍历的底层依赖。而iterable接口里定义了返回iterator的方法，相当于对iterator的封装，同时实现了iterable接口的类可以支持for each循环。

## 自定义 Iterable、Iterator

![image-20221005194430793](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221005194430793.png)

# 比较器

## **Comparable**

如果数组元素本身具备可比较性（实现了 java.util.Comparable 接口）

可以直接使用 Arrays.sort 方法进行排序

## **Comparator**

可以在不修改类源代码的前提下，修改默认的比较方式（比如官方类、第三方类）

可以让一个类提供多种比较方式

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221007150729066.png" alt="image-20221007150729066" style="zoom:80%;" />



# 常用类型

## 日期

#### date类（java.util.Date)

```java
Date date1 =new Date(); /*()中可输入一个long型数字代表毫秒数,不输入默认为
						*1970-01-01 --:00:00:00 GMT 至今的毫秒数
						*默认操作调用了system.currentTimeMillis()
						*该操作输出为1970-01-01 --:00:00:00至今的毫秒数
						*/
System.out.println(date1); //可直接打印输出,输出为当前时间
Date date2 =new Date();
date1.after(date2); //比较时间,date1时间大于date2则返回true
date1.before(date2); //比较时间,date1时间小于date2则返回true
date1.compareTo(date2); //比较时间,date1时间大于date2则返回1,等于返回0,小于返回-1
```

#### Java.text.SimpDateFormat 进行日期的格式化处理

```Java
SimpDateFormat fmt =new SimpDateFormat("yyyy年MM月dd日 HH:mm:ss SSS"); //()括号中为格式
//生成格式字符串 format()
String str = fmt.format(new Date()); //str=对应时间格式
//解析字符串
Date date =fmt.parse(str); //date为上方new Date()数据
```

### **SimpleDateFormat 的模式字母**

![image-20220925095609157](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925095609157.png)

### Calendar

功能比 Date 更加丰富，Date 中很多过期的方法都迁移到了 Calendar 中

#### 获得Calendar实例对象

> Calendar为抽象类，无法通过new获得对象，可通过Calendar.getInstance()方法获得Calendar子类对象

```java
Calendar c = Calendar.getInstance();
```

#### 常用方法

- get方法

![image-20220925100750225](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925100750225.png)

- set方法

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925100835540.png" alt="image-20220925100835540" style="zoom:67%;" />

月份从0计数

- add方法

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925100927876.png" alt="image-20220925100927876" style="zoom:67%;" />

- 通过Date对象获取时间；转换为Date对象

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925101033022.png" alt="image-20220925101033022" style="zoom:67%;" />

- 设置毫秒数获取时间；获得毫秒数

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925101158813.png" alt="image-20220925101158813" style="zoom:67%;" />

#### 打印格式化

![image-20220925100526801](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925100526801.png)

## 枚举（enum)

> 由一组预定义字符组成

**本质为类**

- 所有枚举类型最终都隐式继承自 java.lang.Enum
- 枚举定义完常量后，可以再定义成员变量、方法等内容（这时最后一个常量要以分号结束）
- 枚举的构造方法权限必须是 无修饰符 或者 private
- 无法主动调用构造方法

#### 示例

![image-20220919143136502](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220919143136502.png)

### 自定义构造方法的枚举类型

![image-20220919143245911](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220919143245911.png)

### 内置常用方法

.name()返回对应常量的字符串类型值

.ordinal()返回对应常量在枚举类型中的相对位置序列（从0开始计数）

## 包装类

> Java内置基本类型包装类
>
> 数字类型的包装类（Byte\Short\Integer\Long\Float\Double）最终都继承自 java.lang.Number

#### 为什么使用包装类？

- 基本类型较引用类型有缺陷：
  - 无法表示不存在的值（null 值）
  - 不能利用面向对象的方式去操作基本类型（比如直接用基本类型调用方法）
  - 当方法参数是引用类型时，基本类型无法传递

### 自动装箱、拆箱（Autoboxing and Unboxing)

#### 自动装箱：Java 编译器会自动将基本类型转换为包装类（调用 valueOf 方法）

```java
Integer i1 = 10;
//等于：Integer i1 =Integer.valueof(10);
```

#### 自动拆箱：Java 编译器会自动将包装类转换为基本类型（调用 xxxValue 方法）

```java
void add(Integer num){}
add(20);
//等于（Integer.valueOf(20));
```

### 注意：

- 基本类型数组与包装类数组之间不能自动装箱、拆箱
- 包装类的判等，不要使用 ==、!= 运算符，应该使用 equals 方法
  - （引用类型==、!=判定的是地址）
- IntegerCache 类中缓存了 [-128, 127] 范围的 Integer 对象
- Integer.valueOf 方法会优先去 IntegerCache 缓存中获取 Integer 对象

```java
Integer i1 =88;
//i1指向将缓存中的对象，是i2写法的语法糖
Integer i2 = Integer.valueOf(88);
//i2指向将缓存中的对象
Integer i3 = new Ineger(88);
//新建了一个对象让值等于88，但地址与i1、i2不同
System.out.println(i1==i2);//true
System.out.println(i1==i3);//false
```



## Math

![image-20220923141121764](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220923141121764.png)

## Random

![image-20220923141224005](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220923141224005.png)

## UUID

> UUID（Universally Unique Identifier），通用唯一标识符

UUID 的目的是让分布式系统中的所有元素都能有唯一的标识符，而不需要通过中央控制端来做标识符的指定

### randomUUID

可以利用 java.util.UUID 类的 randomUUID 方法生成一个 128 bit（32 位 16 进制数）的随机 UUID

![image-20220923134909002](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220923134909002.png)

## 格式化输出

### System.out.printf or System.out.format 输出格式化字符串

### 可以使用 String.format 创建格式化的字符串

![image-20220923141343510](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220923141343510.png)

### 示例

![image-20220923141415211](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220923141415211.png)

## **DecimalFormat**

> 使用 java.text.DecimalFormat 可以更好地控制前 0、后 0、前缀、后缀、分组分隔符、十进制分隔符等

### 示例

![image-20220923141526900](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220923141526900.png)

## 字符串转数字

### 包装类的valueOf 、 parseXX 方法

使用包装类的 valueOf、parseXX 方法

![image-20220923141648259](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220923141648259.png)

## **数字转字符串**

### 字符串的valueOf  、包装类的 toString 方法

使用字符串的 valueOf 方法、包装类的 toString 方法

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220923141842542.png" alt="image-20220923141842542" style="zoom: 80%;" />

## 高精度计算（BigDicimal)

> float、double 存储的只是小数的近似值，并非精确值。因此不适合用来进行高精度计算
>
> 使用 java.math.BigDecimal 来进行高精度计算
>
> 本质为一个字符数组（字符串）

- 使用字符串初始化BigDecimal，若使用float、double初始化会使初始化值为float、double 存储的近似值

- 使用封装的内部方法进行计算

## 字符串

> 底层使用char[]数组进行储存
>
> java9开始使用byte[]存储
>
> String对象创建完成，本身的字符内容无法修改

### **字符串常量池（String Constant Pool）**

> 从 Java 7 开始属于堆空间的一部分（以前放在方法区）

**当遇到字符串字面量时，会去查看 SCP：**

- 如果 SCP 中存在与字面量内容一样的字符串对象 A 时，就返回 A
- 否则，创建一个新的字符串对象 D，并加入到 SCP 中，返回 D

### 字符串初始化

- 初始化指向为字面量时，对应String对象位于SCP，内部成员变量value指向的字符数组也位于SCP
- 主动调用构造方法，新创建String对象位于堆空间中：
  - 传入参数为String对象（包括字符串字面量），新创建对象的value成员与传入参数value指向相同字符数组
  - 传入参数为Char数组时，会复制一份传入字符数组，复制后的数组存放在堆空间，并被内部value成员指向

![image-20220924144952664](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220924144952664.png)

### intern方法

- A.intern 方法的作用：
  - 如果 SCP 中存在与 A 内容一样的字符串对象 C 时，就返回 C 
  - 否则，将 A 加入到 SCP 中，返回 A

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220924145113885.png" alt="image-20220924145113885" style="zoom:67%;" />

### 字符串常用方法

![image-20220924145452907](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220924145452907.png)

### **StringBuilder**

> 在大量进行字符串的拼接、替换时，务必使用**StringBuilder**（效率远高于String，节省内存）
>
> **StringBuilder不是String的子类或父类**
>
> **StringBuilder、String 都实现了 CharSequence 接口**(可在部分传入参数含CharSequence的方法中替换使用）

#### StringBuilder的append原理

-  StringBuilder内部有value成员，该成员指向一个字符数组（都储存于堆内存）

- 该字符数组默认容量为16,容量不足后会扩容，扩容后的新容量变为原来的2倍+2
- 扩容后数组为新开辟数组
- 对字符串进行拼接、替换等操作时，在原有字符数组中进行不会重新开辟、指向新数组（除非字符容量不足）

# 异常

> 运行时错误:
>
> 在程序运行过程中产生的意外，会导致程序终止运行,在 Java 中也叫做**异常**
>
> 没有主动去处理抛出的异常，会导致程序终止运行

继承自Java.lang.Throwable

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925101614405.png" alt="image-20220925101614405" style="zoom: 67%;" />

- 检查型异常
  - 这类异常难以避免，编译器会进行检查
    - 如果开发者没有处理这类异常，编译器会报错
  - 那些是检查型异常？
    - 除Error、RuntimeException以外的异常

### 常见检查型异常

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925105410297.png" alt="image-20220925105410297" style="zoom:80%;" />

### 非检查型异常

> Error
>
> RuntimeException

### 处理异常

> 检查型异常与非检查型异常都可以通过try-catch、throws处理

**示例**：

<img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925134346951.png" alt="image-20220925134346951" style="zoom: 67%;" />

#### try-catch

> 捕获异常

- try中抛出的异常被catch捕捉到会跳过try后续代码，直接执行catch内代码
- catch有先后执行顺序，父类型异常捕获要写在子类型异常之后

**一个catch捕获多种类型异常**

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925120256223.png" alt="image-20220925120256223" style="zoom: 67%;" />

- 若几个异常类型存在父子关系，保留父类型即可
- 从Java7开始支持
- 变量e是隐式final

#### throws

> 将异常上抛给上层方法
>
> 若方法内最终没有真正产生异常，程序正常执行

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925140116478.png" alt="image-20220925140116478" style="zoom:50%;" />

- **若异常最终抛给了jvm，那么整个Java程序将终止运行**
- 如果 throws 后面的异常类型存在父子关系，保留父类型即可

- 使用throws上抛异常，产生异常位置后面的代码将不再执行，直接结束当前方法

### throw

> 用于抛出一个新建的异常

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20220925145450518.png" alt="image-20220925145450518" style="zoom:80%;" />

- 若需要严格重视异常出现，可新建为检查型异常
- 若不需要严格重视异常出现，可新建为非检查型异常

### 自定义异常类型

![image-20220925150753365](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20220925150753365.png)



### Throwable常用方法

getMessage();//异常描述 

printStacktrace();//打印堆栈信息(用于调试，经常使用)

 <img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20220925115510222.png" alt="image-20220925115510222" style="zoom:67%;" />

### finally

> 与try-catch合用

- try 或 catch 正常执行完毕后，一定会执行 finally 中的代码
- finally 可以和 try-catch 搭配使用，也可以只和 try 搭配使用
- 经常会在 finally 中编写一些关闭、释放资源的代码（比如关闭文件）

- 若在执行try或catch时，jvm退出或当前线程被中断、杀死 ：finally可能不会执行

- 如果 try 或 catch 中使用了 return、break、continue 等提前结束语句：

  finally 会在 return、break、continue 之前执行

### 断言类

# 并发编程

## 进程

- 什么是进程？
  - 在操作系统中运行的一个应用程序

> 每个进程之间是独立的，每个进程均运行在其专用且受保护的内存空间内
>
> 在 Windows 中，可以通过“任务管理器”查看正在运行的进程

## 线程**（Thread）**

- 什么是线程？
  - 1 个进程要想执行任务，必须得有线程（每 1 个进程至少要有 1 个线程）
  - 一个进程的所有任务都在线程中执行

> Thread 类实现了 Runnable 接口

### 串行

- 1 个线程中任务的执行是串行的
  - 如果要在 1 个线程中执行多个任务，那么只能一个一个地按顺序执行这些任务
  - 在同一时间内，1 个线程只能执行 1 个任务

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016141745236.png" alt="image-20221016141745236" style="zoom:67%;" />

### 默认线程

> 每一个 Java 程序启动后，会默认开启一个线程，称为主线程（main 方法所在的线程）

每一个线程都是一个 java.lang.Thread 对象，可以通过 Thread.*currentThread* 方法获取当前的线程对象

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016153219205.png" alt="image-20221016153219205" style="zoom:67%;" />

### 开启新线程

-  在Thread构造 方法中传入一个Runnable实例，重写Run方法（run方法内部为新线程执行部分）<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016153326871.png" alt="image-20221016153326871" style="zoom:67%;" />
- 自定义线程类（继承Thread）重写Run方法<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016153640214.png" alt="image-20221016153640214" style="zoom:67%;" />

#### **注意**

- 直接调用线程的 run 方法并不能开启新线程

- 调用线程的 start 方法才能成功开启新线程

## 多线程

- 什么是多线程？
  - 1 个进程中可以开启多个线程，所有线程可以并行（同时）执行不同的任务
- 多线程技术可以提高程序的执行效率

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016141850676.png" alt="image-20221016141850676" style="zoom:67%;" />

### 多线程原理

**同一时间，CPU 的 1 个核心只能处理 1 个线程**（只有 1 个线程在工作）

多线程并发（同时）执行，其实是 CPU 快速地在多个线程之间调度（切换）

如果 CPU 调度线程的速度足够快，就造成了多线程并发执行的假象

**如果是多核 CPU，才是真正地实现了多个线程同时执行**

- **如果线程非常非常多，会发生什么情况？**
  - CPU 会在 N 个线程之间调度，消耗大量的 CPU 资源，CPU 会累死
  - 每条线程被调度执行的频次会降低（线程的执行效率降低）

### 多线程优缺点

- 优点
  - 能适当提高程序的执行效率
  - 能适当提高资源利用率（CPU、内存利用率）
- 缺点
  - 开启线程需要占用一定的内存空间，如果开启大量的线程，会占用大量的内存空间，降低程序的性能
  - 线程越多，CPU 在调度线程上的开销就越大
  - 程序设计更加复杂
    - 比如线程之间的通信问题、多线程的数据共享问题

### 多线程的内存布局

- PC 寄存器（Program Counter Register）：每一个线程都有自己的 PC 寄存器
- Java 虚拟机栈（Java Virtual Machine Stack）：每一个线程都有自己的 Java 虚拟机栈
- 堆（Heap）：多个线程共享堆
- 方法区（Method Area）：多个线程共享方法区
- 本地方法栈（Native Method Stack）：每一个线程都有自己的本地方法栈

#### **jdk1.8内存结构**

![image-20220503170348619](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20220503170348619.png)

## 线程的状态

通过 Thread.getState 方法获得线程的状态

> 线程一共有 6 种状态

- NEW（新建）：尚未启动

- RUNNABLE（可运行状态):正在JVM中运行或等待操作系统的其他资源（e.g.CPU)

- BLOCKED（阻塞状态）：等待监视器锁（内部锁）

- WATING（等待状态）：在等待另一个线程

  - 调用以下方法会处于等待状态

    ✓ 没有超时值的 Object.wait

    ✓ 没有超时值的 Thread.join

    ✓ LockSupport.*park*

- TIMED_WATING（定时等待状态）

  - 调用以下方法会处于定时等待状态

    ✓ Thread.*sleep*

    ✓ 有超时值的 Object.wait

    ✓ 有超时值的 Thread.join

    ✓ LockSupport.*parkNanos*

    ✓ LockSupport.*parkUntil*

- TERMINATED（终止状态）：已经执行完毕

### 线程的状态切换

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016171520911.png" alt="image-20221016171520911" style="zoom:67%;" />

### **sleep、interrupt**（扰乱干扰）

> 可以通过 Thread.*sleep* 方法暂停当前线程，进入WATING状态
>
> sleep为静态方法（类名调用）

在暂停期间，若调用线程对象的 interrupt 方法中断线程，会抛出 java.lang.InterruptedException 异常

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016172033790.png" alt="image-20221016172033790" style="zoom:%67;" />

### **join、isAlive**

- A.join 方法：等线程 A 执行完毕后，当前线程再继续执行任务。可以传参指定最长等待时间

- A.isAlive 方法：查看线程 A 是否还活着

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016172906328.png" alt="image-20221016172906328" style="zoom:67%;" />

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016173021088.png" alt="image-20221016173021088" style="zoom:67%;" />

## 线程安全问题

- 多个线程可能会共享（访问）同一个资源：
  - 比如访问同一个对象、同一个变量、同一个文件

- **当多个线程访问同一块资源时，很容易引发数据错乱和数据安全问题，称为线程安全问题**

- 什么情况下会出现线程安全问题？
  - 多个线程共享同一个资源
  - 且至少有一个线程正在进行写的操作

### 线程同步（同步异步）

> 可以使用线程同步技术来解决线程安全问题
>
> 对资源访问无先后要求（仅只需使用synchronized）

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016183008974.png" alt="image-20221016183008974" style="zoom:67%;" />

**使用了线程同步技术**：

- 虽然解决了线程安全问题，但是降低了程序的执行效率

- 所以在真正有必要的时候，才使用线程同步技术

#### 同步语句（Synchronized Statement）

**synchronized (obj) 的原理**

- 每个对象都有一个与它相关的内部锁（intrinsic lock）或者叫监视器锁（monitor lock）

- 第一个执行到同步语句的线程可以获得 obj 的内部锁，在执行完同步语句中的代码后释放此锁

- 只要一个线程持有了内部锁，那么其它线程在同一时刻将无法再获得此锁
  -  当其他试图获取此锁时，将会进入BLOCKED状态

**多个线程访问同一个 synchronized (obj) 语句时：**

**obj** 必须是**同一个对象**，才能起到同步的作用

#### 同步方法（Synchronized Method）

> synchronized 不能修饰构造方法

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221016182911019.png" alt="image-20221016182911019" style="zoom:67%;" />

**同步方法的本质**

- 实例方法：synchronized (this)

- 静态方法：synchronized (Class对象)

#### 同步语句与同步方法的比较

> 同步语句比同步方法更灵活一点

> 同步语句可以精确控制需要加锁的代码范围

### 常用类的线程安全问题

- 动态数组
  - ArrayList：非线程安全
  - Vector：线程安全

- 动态字符串

  - StringBuilder：非线程安全

  - StringBuffer：线程安全

- 映射（字典）

  HashMap：非线程安全

  Hashtable：线程安全

## 线程间通讯

> 可以使用 Object.wait、Object.notify、Object.notifyAll 方法实现线程之间的通信
>
> 对资源访问有先后顺序要求

若想在线程  中成功调用 obj.wait、obj.notify、obj.notifyAll 方法：

- 调用wait\notify的obj对象必须为同一个
- 调用wait\notify的线程必须拥有obj对象的内部锁



- obj.wait：释放obj的内部锁，当前线程进入WAITING或TIMED_WAITING状态
- obj.notifyAll：唤醒所有因为 obj.wait 进入WAITING或TIMED_WAITING状态的线程
- obj.notify：随机唤醒一个因为 obj.wait 进入WAITING或TIMED_WAITING状态的线程

### 生产者消费者模型

ppt-并发编程

## **ReentrantLock（可重入锁）**（类）

> java.util.concurrent.locks.ReentrantLock
>
> ReentrantLock ，译为“可重入锁”
>
> 具有跟同步语句、同步方法一样的一些基本功能，但功能更加强大

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221024214324486.png" alt="image-20221024214324486" style="zoom:67%;" />

### 可重入锁（递归锁）

> 单一线程重复获取锁，会使锁计数器加一，解锁也需要多次解锁

- 同一个线程可以重复获取同一个锁
- synchronized 也是可重入的

#### ReentrantLock.lock

> 获得锁

- 如果此锁没有被另一个线程持有，则将锁的持有计数设为 1，并且此方法立即返回

- 如果当前线程已经持有此锁，则将锁的持有计数加 1，并且此方法立即返回

- 如果此锁被另一个线程持有，并且在获得锁之前，此线程将一直处于休眠状态，此时锁的持有计数被设为 1

#### ReentrantLock.tryLock

> 仅在锁未被其他线程持有的情况下，才获取此锁；未成功获得锁不会等待而是返回false继续执行程序

- 如果此锁没有被另一个线程持有，则将锁的持有计数设为 1，并且此方法立即返回 true
- 如果当前线程已经持有此锁，则将锁的持有计数加 1，并且此方法立即返回 true。
- 如果锁被另一个线程持有，则此方法立即返回 false

#### ReentrantLock.unlock

> 尝试释放此锁

- 如果当前线程持有此锁，则将持有计数减 1
- 如果持有计数现在为 0，则释放此锁
- 如果当前线程没有持有此锁，则抛出 java.lang.IllegalMonitorStateException

#### ReentrantLock.isLocked

> 查看此锁是否被任意线程持有

## 线程池（**Thread Pool**）

> 线程对象占用大量内存，在大型应用程序中，频繁地创建和销毁线程对象会产生大量内存管理开销
>
> 使用线程池可以最大程度地减少线程创建、销毁所带来的开销

- 线程池由工作线程（Worker Thread）组成：

  - 普通线程：执行完一个任务后，生命周期就结束了

  - 工作线程：可以执行多个任务（任务没来就一直等，任务来了就干活）

    > 先将任务添加到队列（Queue）中，再从队列中取出任务提交到池中

#### 常用的线程池类型是固定线程池（Fixed Thread Pool）

> 具有固定数量的正在运行的线程

- 注意：**关闭线程池**
  - shutdown()

#### 基本使用

![image-20221024214716718](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221024214716718.png)

# I/O

## I/O流

> I/O 流 全称是 Input/Output Stream，译为“输入/输出流”

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221024223755000.png" alt="image-20221024223755000" style="zoom:67%;" />

## 常用类型

> 位于java.io包中

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221024225911999.png" alt="image-20221024225911999" style="zoom:67%;" />

## File(类)

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221025191609747.png" alt="image-20221025191609747" style="zoom:67%;" />

> 名字分隔符（name separator）：File.*separator*（/、\）
>
> - 在 UNIX、Linux、Mac 系统中：正斜杠（/）
> - 在 Windows 系统中：反斜杠（\）

> 路径分隔符（path separator）：File.*pathSeparator*
>
> - 在 UNIX、Linux、Mac系统中：冒号（:）
>
> - 在 Windows 系统中：分号（;）

> 在 Windows、Mac 系统中：
>
> 文件名、目录名不区分大小写

> 在 UNIX、Linux 系统中：
>
> 文件名、目录名区分大小写

### 常用方法

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221025202638820.png" alt="image-20221025202638820" style="zoom:67%;" />

- getParent()
  - 当获取相对路径的parent时会返回NULL，需先获得绝对路径形式文件对象再调用getParent

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221025203207531.png" alt="image-20221025203207531" style="zoom:67%;" />

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221025203243575.png" alt="image-20221025203243575" style="zoom:67%;" />

- FilenameFilter()
  - 函数式接口，过滤得到符合要求的Filename

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221025215447163.png" alt="image-20221025215447163" style="zoom:67%;" />

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221025215502505.png" alt="image-20221025215502505" style="zoom:67%;" />

## 字符集

> 由字符组成的集合

### 常见字符集

- ASCII：128个字符（包括了英文字母大小写、阿拉伯数字等）
- ISO-8859-1：支持欧洲的部分语言文字，在有些环境也叫 Latin-1
- GB2312：支持中文（包括了 6763 个汉字）
- BIG5：支持繁体中文（包括了 13053 个汉字）
- GBK：是对 GB2312、BIG5 的扩充（包括了 21003 个汉字），支持中日韩
- GB18030：是对 GBK 的扩充（包括了 27484 个汉字）
- Unicode：包括了世界上所有的字符

> ISO-8859-1、GB2312、BIG5、GBK、GB18030、Unicode 中都已经包括了 ASCII 中的所有字符

## 字符编码**（Character Encoding）**

> 每个字符集都有对应的字符编码，它决定了每个字符如何转成二进制存储在计算机中

**一般将【字符串】转为【二进制】的过程称为：编码（Encode）**

**一般将【二进制】转为【字符串】的过程称为：解码（Decode）**

> 编码、解码时使用的字符编码必须要保持一致，否则会造成乱码

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221026151423771.png" alt="image-20221026151423771" style="zoom:67%;" />

- ASCII：单字节编码，编码范围是 0x00 ~ 0x7F （0 ~ 127）
- ISO-8859-1：单字节编码，编码范围是 0x00 ~ 0xFF
- 0x00 ~ 0x7F 和 ASCII 一致，0x80 ~ 0x9F 是控制字符，0xA0 ~ 0xFF 是文字符号
- GB2312、BIG5、GBK：采用双字节表示一个汉字
- GB18030：采用单字节、双字节、四字节表示一个字符
- Unicode：有 Unicode、UTF-8、UTF-16、UTF-32 等编码，最常用的是 UTF-8 编码
  - UTF-8 采用单字节、双字节、三字节、四字节表示一个字符

### 字符编码比较

![image-20221026150727166](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221026150727166.png)

#### String.getBytes

如果 String.getBytes 方法没有传参，就使用 JVM 的默认字符编码（一般跟随 main 方法所在文件的字符编码）

---

可以通过 Charset.*defaultCharset* 方法获取 JVM 的默认字符编码

> Charset 类的全名是 java.nio.charset.Charset

## 字节流

- 一次只读写一个字节
- 最终都继承自Input Stream、OutputSteam
- 常用字节流：
  - FileInputStream、FileOutputStream

### **字节流结构预览**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221026184259484.png" alt="image-20221026184259484" style="zoom:67%;" />

### **FileOutStream**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221026184333923.png" alt="image-20221026184333923" style="zoom:67%;" />

### **FileInputStream**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221026184405857.png" alt="image-20221026184405857" style="zoom:67%;" />

- .read()
  - 返回读取到的字符数

## **try-with-resources**

> 用于自动关闭**资源**（类似python with）
>
> 实现了 java.lang.AutoCloseable 接口的实例，都可以称之为是**资源**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221101192407516.png" alt="image-20221101192407516" style="zoom:67%;" />

- 可以在后面的小括号中声明一个或多个资源（resource）

- 不管**try**中的语句是正常还是意外结束:
  - 最终都会自动按顺序调用每一个资源的 close 方法（close 方法的调用顺序与资源的声明顺序相反）
  - 调用完所有资源的 close 方法后，再执行 finally 中的语句

### 示例

![image-20221101192802767](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221101192802767.png)

## 字符流（**Character Streams**）

> 一次只读写一个**字符**
>
> 最终都继承自 Reader、Writer

常用的是字符流有 FileReader、FileWriter

- 注意：这 2 个类只适合文本文件，比如 .txt、.java 等这类文件

### **FileWriter**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221101210104605.png" alt="image-20221101210104605" style="zoom:67%;" />

### **FileReader**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221101210120035.png" alt="image-20221101210120035" style="zoom:67%;" />

## **缓冲流（Buffered Streams）**

> 每个读写操作通常会触发磁盘访问，因此大量的读写操作，可能会使程序的效率大大降低
>
> 为了减少读写操作带来的开销，Java 实现了缓冲的 I/O 流
>
> - 缓冲输入流：从缓冲区读取数据，并且只有当缓冲区为空时才调用本地的输入 API（Native Input API）
>
> - 缓冲输出流：将数据写入缓冲区，并且只有当缓冲区已满时才调用本地的输出 API（Native Output API）

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105204629033.png" alt="image-20221105204629033" style="zoom:67%;" />

### 使用

> 缓冲流的常见使用方式：将无缓冲流传递给缓冲流的构造方法（将无缓冲流包装成缓冲流）

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105205050670.png" alt="image-20221105205050670" style="zoom:67%;" />

### **close、flush**

- 只需要执行缓冲流的 close 方法，不需要执行缓冲流内部包装的无缓冲流的 close 方法

  > 缓冲输出流的 close 方法内部会调用一次 flush 方法

- 调用缓冲输出流的 flush 方法，会强制调用本地的输出 API，将缓冲区的数据真正写入到文件中

## InputStreamReader、OutputStreamWriter

> InputStreamReader 可以实现【字节输入流】转【字符输入流】

> OutputStreamWriter 可以实现【字节输出流】转【字符输出流】

## 格式化输入、标准输入

> 格式化：带基本类型格式及其他格式
>
> 标准输入：如控制台输入、键盘输入

### System.*in*

System.*in* 属于标准输入流，可以从键盘接收输入

### **Scanner**

> java.util.Scanner 是一个可以使用正则表达式来解析基本类型和字符串的简单文本扫描器
>
> 它默认利用空白（空格\制表符\行终止符）作为分隔符将输入分隔成多个 token

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105205509631.png" alt="image-20221105205509631" style="zoom:67%;" />

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105205537726.png" alt="image-20221105205537726" style="zoom:67%;" />

#### **useDelimiter**

> Scanner.useDelimiter 方法可以自定义分隔符

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105205810430.png" alt="image-20221105205810430" style="zoom:67%;" />

## 格式化输出、标准输出

> 格式化：带基本类型格式及其他格式
>
> 标准输出：控制台输出

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105210329830.png" alt="image-20221105210329830" style="zoom:67%;" />

### 常用方法

print、println、format、write

#### print、write 的区别

- write(97) 写入的是字符'a'

- print(97) 写入的是字符串"97"

### PrintStream

> 属于标准输出流（Standard Ouput Stream）
>
> 比如输出到屏幕、控制台（Console）

System.*out*、System.*err* 是 PrintStream 类型的实例

#### PrintStream 是字节流，但它内部利用字符流对象来模拟字符流的许多功能

### PrintWriter

> 平时若要创建格式化的输出流，一般使用 PrintWriter，它是字符流

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105211235387.png" alt="image-20221105211235387" style="zoom:67%;" />

- 可以通过构造方法设置 PrintWriter.autoflush 为**true**
  - 使其每次输入自动调用flush方法：

    即println、printf、format 方法内部就会自动调用 flush 方法

![image-20221105211224318](C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105211224318.png)

## **数据流、对象流结构预览** <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105212037823.png" alt="image-20221105212037823" style="zoom:67%;" />

## 数据流（Data Stream)

> 有：**DataInputStream**、**DataOutputStream**，支持**基本类型、字符串类型**的 I / O 操作 

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105211357681.png" alt="image-20221105211357681" style="zoom:67%;" />

#### 注意与使用格式化输出流（PrintWriter）有所不同：

PrintWriter写入的为字符，是“可视”的

数据流写入编码过的内容，是“不可视”的

## 对象流（Object Stream）

> 有：**ObjectInputStream**、**ObjectOutputStream**，支持**引用类型**的 I / O 操作

- 只有实现了 java.io.Serializable 接口的类才能使用对象流进行 I / O 操作

  否则会抛出 java.io.NotSerializableException 异常

- Serializable 是一个标记接口（Maker Interface），不要求实现任何方法


### **对象的序列化和反序列化**

#### 序列化（Serialization）

- 将对象转换为可以存储或传输的数据

- 利用 ObjectOutputStream 可以实现对象的序列化

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105215754760.png" alt="image-20221105215754760" style="zoom:67%;" />

#### 反序列化（Deserialization ）

- 从序列化后的数据中恢复出对象

- 利用 ObjectInputStream 可以实现对象的反序列化

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105215916834.png" alt="image-20221105215916834" style="zoom: 67%;" />

### **transient**

> 被**transient**修饰的实例变量不会被序列化

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105220247705.png" alt="image-20221105220247705" style="zoom:67%;" />

### **serialVersionUID**

每一个实现了Serializable接口的类都会生成一个**serialVersionUID**，相当于类的版本号

> 类内容改变，serialVersionUID也会改变

- 默认情况下会根据类的详细信息计算出serialVersionUID的值，根据编译器实现的不同可能千差万别

- 一旦类的信息发生修改，serialVersionUID的值就会发生变化

- 如果序列化、反序列时的serialVersionUID不一致：
  - 会认定为序列化、反序列时的类不兼容，会抛出 java.io.InvalidClassException 异常

**强烈建议每一个可序列化类都自定义serialVersionUID，不要使用它的默认值**

- 必须是**static final long**

- 建议声明为**private**
- 如果没有自定义serialVersionUID，编译器会发出“serial”警告

# GUI**（Graphical User Interface）**

> GUI（Graphical User Interface）：图形用户界面
>
> 指在计算机中采用图形方式显示的用户界面

Java 也可以开发 GUI 程序，常见的实现方案有 4 种

- AWT（Abstract Window Toolkit）

  Java 官方最早推出的 GUI 编程开发包，界面风格是跟随操作系统的

- **Swing**

  在 AWT 的基础上扩充了功能，灵活且强大，在不同操作系统中可以保持统一风格

- JavaFX

  Java 官方推出的最新一代 GUI 编程开发包，参考资料要比 Swing 少一些

## **Swing**

### **Swing 的常用组件**

 <img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105230920906.png" alt="image-20221105230920906" style="zoom:67%;" />

#### **Swing 组件预览**

<img src="C:\Users\Lenovo\OneDrive\桌面\1\java\java随笔.assets\image-20221105230954609.png" alt="image-20221105230954609" style="zoom:67%;" />

# 反射