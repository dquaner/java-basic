---
description: >-
  https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Documented.html
---

# Documented

Annotation Interface `Documented`

```
@Documented
@Retention(RUNTIME)
@Target(ANNOTATION_TYPE)
public @interface Documented
```

如果注释 `@Documented` 出现在了注释接口 _A_ 的声明中，则元素上的任何 `@A` 注释都会被认为是元素公共契约（contract）的一部分。

更详细地说，当使用 `Documented` 对注释接口 _A_ 进行注释时，那么注释 _A_ 的存在和值会成为被 _A_ 所注释的元素的公共契约（contract）的一部分。相反，如果注释接口 _B_ 没有使用 `Documented` 进行注释，那么 _B_ 注释的存在和值就不是 _B_ 所注释的元素的公共契约（contract）的一部分。

具体地说，如果一个注释接口用 `Documented` 进行了注释，默认情况下，像 javadoc 这样的工具将在其生成的 API 文档中显示该接口的注释，而没有 `Documented` 的注释接口的注释将不显示。

### Since:

1.5
