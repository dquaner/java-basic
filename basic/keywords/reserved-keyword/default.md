# default

### 1. 用作访问控制修饰符

Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。

* **private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**
* **default** (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
* **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。
* **public** : 对所有类可见。使用对象：类、接口、变量、方法。

我们可以通过以下表来说明访问权限：

| 修饰符         | 当前类 | 同一包内 | 子孙类(同一包) | 子孙类(不同包)                                                                       | 其他包 |
| ----------- | --- | ---- | -------- | ------------------------------------------------------------------------------ | --- |
| `public`    | Y   | Y    | Y        | Y                                                                              | Y   |
| `protected` | Y   | Y    | Y        | Y/N（[说明](https://www.runoob.com/java/java-modifier-types.html#protected-desc)） | N   |
| `default`   | Y   | Y    | Y        | N                                                                              | N   |
| `private`   | Y   | N    | N        | N                                                                              | N   |

#### 默认访问修饰符 - 不使用任何关键字

如果在类、变量、方法或构造函数的定义中没有指定任何访问修饰符，那么它们就默认具有默认访问修饰符。

默认访问修饰符的访问级别是包级别（package-level），即只能被同一包中的其他类访问。

如下例所示，变量和方法的声明可以不使用任何修饰符。

#### 实例

```java
// MyClass.java
class MyClass {  // 默认访问修饰符
    int x = 10;  // 默认访问修饰符
 
    void display() {  // 默认访问修饰符
        System.out.println("Value of x is: " + x);
    }
}
 
// MyOtherClass.java
class MyOtherClass {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.display();  // 访问 MyClass 中的默认访问修饰符变量和方法
    }
}
```

以上实例中，`MyClass` 类和它的成员变量 `x` 和方法 `display()` 都使用默认访问修饰符进行了定义。`MyOtherClass` 类在同一包中，因此可以访问 `MyClass` 类和它的成员变量和方法。

### 2. 用做 switchLabel

```java
switch(expression){
    case value :
       //语句
       break; //可选
    case value :
       //语句
       break; //可选
    //你可以有任意数量的case语句
    default : //可选
       //语句
}
```

### 3. 修饰接口的方法

Java 8 中引入了一个新的特性：默认方法（Default Methods）。

默认方法是指接口中可以包含一些具体的方法实现，默认方法使用`default`关键字进行修饰。在 Java 8 之前，接口中只能声明方法的签名，而没有方法的实现。但是，随着 Java 8 的发布，我们可以在接口中定义默认方法，这样实现类就不再需要实现这些方法了。

#### 默认方法示例 <a href="#id-6" id="id-6"></a>

让我们通过一个简单的例子来理解`default`关键字的用法。假设我们有一个动物接口`Animal`，它声明了一个`sound()`方法：

```java
public interface Animal {
    void sound();
}
```

现在，我们可以创建一个实现类`Cat`，它实现了`Animal`接口：

```java
public class Cat implements Animal {
    @Override
    public void sound() {
        System.out.println("Meow!");
    }
}
```

在上面的例子中，我们必须在`Cat`类中实现`sound()`方法，因为它是`Animal`接口的一个抽象方法。

现在，让我们为`Animal`接口添加一个默认方法`defaultSound()`：

```java
public interface Animal {
    void sound();
    
    default void defaultSound() {
        System.out.println("Default sound!");
    }
}
```

在上面的代码中，我们在接口中定义了一个默认方法`defaultSound()`，它的实现打印出了一个默认的声音。

接下来，我们可以在`Cat`类中实现`Animal`接口的默认方法：

```java
public class Cat implements Animal {
    @Override
    public void sound() {
        System.out.println("Meow!");
    }

    @Override
    public void defaultSound() {
        System.out.println("Custom default sound!");
    }
}
```

在上面的代码中，我们重写了`defaultSound()`方法，并提供了自定义的实现。

现在，让我们在`main`方法中创建一个`Cat`对象，并调用接口的默认方法和抽象方法：

```java
public class Main {
    public static void main(String[] args) {
        Cat cat = new Cat();
        cat.sound(); // 输出：Meow!
        cat.defaultSound(); // 输出：Custom default sound!
    }
}
```

在上面的代码中，我们实例化了一个`Cat`对象，并调用了`sound()`和`defaultSound()`方法。`sound()`方法是从接口继承来的抽象方法，而`defaultSound()`方法是从接口继承来的默认方法。

#### 默认方法的用途 <a href="#id-75" id="id-75"></a>

默认方法的引入主要是为了解决接口的演化问题。在 Java 8 之前，如果我们向一个已经存在的接口中添加一个新的方法，那么所有实现该接口的类都必须实现这个新方法。这可能导致大量的代码修改，特别是当接口用作库或框架的一部分时。

通过使用默认方法，我们可以向接口中添加新的方法，而不会破坏已有的实现类。实现类可以选择是否覆盖默认方法，如果没有覆盖，默认方法将被继承和使用。

另一个使用默认方法的场景是在接口中提供一些通用的方法实现。例如，如果我们有一个集合接口`Collection`，我们可以为它添加一些默认方法，如`isEmpty()`、`size()`等。这样，实现`Collection`接口的类就不需要重复实现这些方法了。

#### 注意事项 <a href="#id-83" id="id-83"></a>

在使用默认方法时，需要注意以下几点：

1. 一个接口可以有多个默认方法。
2. 如果一个类实现了多个接口，并且这些接口有相同的默认方法，那么实现类必须提供自己的实现，以消除冲突。
3. 默认方法的调用是通过接口的实例进行的，而不是通过实现类的实例。
4. 默认方法不能是`static`和`final`的。
