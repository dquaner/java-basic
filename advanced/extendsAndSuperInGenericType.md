---
description: >-
  PECS（Producer Extends Consumer Super）原则
---

# 泛型中的 extends 和 super 关键字

## 简介

`<? extends T>` 和 `<? super T>` 是Java泛型中的 **“通配符(Wildcards)”** 和 **“边界(Bounds)”** 的概念。

* `<? extends T>`：指 “上界通配符(Upper Bounds Wildcards)”
* `<? super T>`：指 “下界通配符(Lower Bounds Wildcards)”

**PECS（Producer Extends Consumer Super）原则：**
* 频繁往外读取内容的，适合用上界 extends
* 经常往里插入内容的，适合用下界 super


## 1. 为什么要用通配符和边界？

使用泛型的过程中，经常出现一种很别扭的情况。例如，我们有 _Fruit_ 类，和它的派生类 _Apple_ 类。

```java
class Fruit {}
class Apple extends Fruit {}
```

然后有一个最简单的容器 _Plate_ 类，盘里可以放一个泛型的“东西”。我们可以对这个“东西”做简单的“放”和“取”的动作：`get()` 和 `set()` 方法。

```java
class Plate<T> {
    private T item;
    public Palte(T t) {item=t;}
    public void set(T t) {item=t;}
    public T get() {return item;}
}
```

现在我定义一个“水果盘子”，逻辑上“水果盘子”当然可以装“苹果”：

```java
Plate<Fruit> p = new Plate<Apple>(new Apple());
```

但实际上，Java 编译器不允许这个操作，会报错：

```
error: incompatible types: Plate<Apple> cannot be converted to Plate<Fruit>
```

所以，就算容器里装的东西之间有继承关系，但容器之间是没有继承关系的。所以我们不可以把 `Plate<Apple>` 的引用传递给 `Plate<Fruit>`。

为了让泛型用起来更舒服，Sun的大脑袋们就想出了 `<? extends T>` 和 `<? super T>` 的办法，来让“水果盘子”和“苹果盘子”之间发生关系。

## 2. <? extends T>：上界通配符


### 要点1

实例化时的类只能是定义时类本身或其子类，也就是说 `T` 是它的上界。

```java
import java.util.*;

class Food{
	String name = "Food";
}
class Fruit extends Food{
	String name = "Fruit";
}
class Apple extends Fruit {
	String name = "Apple";
}

// 定义时指定T为Fruit
List<? extends Fruit> list;

// 实例化时类只能是T本身或它的子类
list= new ArrayList<Fruit>(); //可以
list= new ArrayList<Apple>(); //可以
list= new ArrayList<Food>();  //报错
```

### 要点2
上界通配符 `add` 失效（只能 `add null`），可以 `get`

```java
list = new ArrayList<Fruit>();
list.add(new Fruit()); //报错
list.add(null);  //可以
list.get(0);     //可以
```

既然不能 `add`，那里面没东西又 `get` 什么呢？所以需要在**实例化**的时候就把东西都放进去：

```java
list = new ArrayList<Fruit>(){{
	    	add(new Fruit()); // Fruit及其子类都可以放进去
	    	add(new Apple()); // Fruit及其子类都可以放进去
	    	}};
```

### 要点3
能放进去的对象类型其上界为实例化时指定的 `T`：

```java
List<? extends Fruit> list list= new ArrayList<Apple>(){{
	    	add(new Fruit()); // 实例化时指定的T为Apple，放入Fruit对象会报错
	    	add(new Apple()); // Apple及其子类都可以放进去
	    	}};
```

所以能放进去的对象不是看定义时 `T` 指定的类，而是看实例化时 `T` 指定的类。


## 3. <? superT>：下界通配符

### 要点1

实例化时的类只能是定义时类本身或其父类，也就是说 `T` 是它的下界。

```java
// 定义时指定T为Fruit
List<? super Fruit> list2;

// 实例化时只能是T本身或它的父类
list2 = new ArrayList<Fruit>(); // 可以
list2 = new ArrayList<Food>();  // 可以
list2 = new ArrayList<Apple>(); // 报错
```

### 要点2

添加对象时，在实例化时添加和实例化后添加的对象限制不同（特别注意！）

1. 在实例化时添加的对象只有一个限制：上界为实例化时指定的 `T`。来看一个有趣的现象，即使定义时指定的 `T` 是 `Fruit`，但实例化时可以用 `Fruit` 的邻居类（都继承了实例化时指定的 `Food` ）：

```java
class Food{
	String name = "Food";
}
// 新定义一个Meat类，和Fruit都继承Food
class Meat extends Food{
	String name = "Meat";
}
class Fruit extends Food{
	String name = "Fruit";
}
class Apple extends Fruit {
	String name = "Apple";
}

List<? super Fruit> list2 = new ArrayList<Food>(){{
	    	add(new Object()); // 报错，上界为Food
	    	add(new Meat());   // 可以，是Food的子类，即使不是Fruit
	    	add(new Food());   // 可以
	    	add(new Fruit());  // 可以，是Food的子类
	    	add(new Apple());  // 可以，是Food的子类
	    	}};
```

2. 在实例化后添加的对象，其上界是定义时指定的 `T`：

```java
list2.add(new Meat());   // 报错，不是Fruit或其子类
list2.add(new Food());   // 报错，不是Fruit或其子类
list2.add(new Fruit());  // 可以
list2.add(new Apple());  // 可以
```

### 要点3

上界通配符 `get` 出来的对象默认是 `Object` 类型，可以做强制类型转换，可以 `add`

```java
Object object = list2.get(0);
Meat meat = (Meat)list2.get(0); // 如果不是Object，需要强制类型转换
System.out.println(meat.name); // 输出meat
```