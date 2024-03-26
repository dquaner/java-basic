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

## 2. <? extends T>： 上界通配符

https://zhuanlan.zhihu.com/p/249187830