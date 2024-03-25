# 泛型中的 extends 和 super

## 简介：

`<? extends T>` 和 `<? super T>` 是Java泛型中的**“通配符(Wildcards)”**和**“边界(Bounds)”**的概念。

* `<? extends T>`：指 “上界通配符(Upper Bounds Wildcards)”
* `<? super T>`：指 “下界通配符(Lower Bounds Wildcards)”

## 1. 为什么要用通配符和边界？

使用泛型的过程中，经常出现一种很别扭的情况。例如，我们有 _Fruit_ 类，和它的派生类 _Apple_ 类。

```
class Fruit {}
class Apple extends Fruit {}
```

