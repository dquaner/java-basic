---
description: >-
  https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Target.html
---

# Target

Annotation Interface `Target`

```
@Documented
@Retention(RUNTIME)
@Target(ANNOTATION_TYPE)
public @interface Target
```

指明一个注释接口适用的上下文。JLS [9.6.4.1](https://docs.oracle.com/javase/specs/jls/se17/html/jls-9.html#jls-9.6.4.1) 指定了注释接口可能适用的声明上下文和类型上下文，在源代码中由 [`java.lang.annotation.ElementType`](elementtype.md) 的枚举常量表示。

如果 `@Target` 元注释没有出现在注释接口 `T` 上，则可以将注释 `T` 用做任何声明的修饰符。

如果存在 `@Target` 元注释，编译器将强制执行由 `ElementType` 枚举常量（与 JLS [9.7.4](https://docs.oracle.com/javase/specs/jls/se17/html/jls-9.html#jls-9.7.4) 一致）指示的使用限制。

例如，`@Target(ElementType.ANNOTATION_TYPE)` 元注释表明声明的接口（`MetaAnnotationType`）本身就是一个元注释接口。它（`MetaAnnotationType`）只能在注释接口声明中使用：

```
@Target(ElementType.ANNOTATION_TYPE)
public @interface MetaAnnotationType {
    ...
}
```

`@Target({})` 元注释表明声明的类或接口（`MemberInterface`）仅用做复杂的注释接口声明中一个成员类或接口。它（`MemberInterface`）不能直接用于注释任何内容：

```
@Target({})
public @interface MemberInterface {
    ...
}
```

同一个 `ElementType` 常量在 `@Target` 注释中出现多次会导致编译时错误。例如，下面的 `@Target` 元注释是非法的：

```
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.FIELD})
public @interface Bogus {
    ...
}
```

See _Java Language Specification_:

[9.6.4.1 @Target](https://docs.oracle.com/javase/specs/jls/se17/html/jls-9.html#jls-9.6.4.1)\
[9.7.4 Where Annotations May Appear](https://docs.oracle.com/javase/specs/jls/se17/html/jls-9.html#jls-9.7.4)\
[9.7.5 Multiple Annotations of the Same Interface](https://docs.oracle.com/javase/specs/jls/se17/html/jls-9.html#jls-9.7.5)

### Since:

1.5

## Required Element Summary

<table><thead><tr><th width="185">Modifier and Type</th><th width="171">Required Element</th><th>Description</th></tr></thead><tbody><tr><td><a href="elementtype.md">ElementType</a>[]</td><td><a href="target.md#value">value</a></td><td>返回可应用注释接口的元素类型数组。</td></tr></tbody></table>

## Element Details

### value

[ElementType](elementtype.md)\[] value

**Returns:**\
可应用注释接口的元素类型数组。
