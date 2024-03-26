---
description: >-
  Package `java.lang.annotation`: https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/package-summary.html
---

# java.lang.annotation

为Java编程语言的注释功能提供库支持。

### Since:

1.5

{% tabs %}
{% tab title="Related Packages" %}
| Package                                                                                                  |  Description          |
| -------------------------------------------------------------------------------------------------------- | --------------------- |
| [java.lang](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/package-summary.html) | 提供对Java编程语言的设计至关重要的类。 |
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="All Classes and Interfaces" %}
| Class                                                                                                                                                     |  Description                                                                                                                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Annotation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Annotation.html)                                           | The common interface extended by all annotation interfaces.                                                                                                                                              |
| [AnnotationFormatError](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/AnnotationFormatError.html)                     | Thrown when the annotation parser attempts to read an annotation from a class file and determines that the annotation is malformed.                                                                      |
| [AnnotationTypeMismatchException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/AnnotationTypeMismatchException.html) | Thrown to indicate that a program has attempted to access an element of an annotation whose type has changed after the annotation was compiled (or serialized).                                          |
| [Documented](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Documented.html)                                           | If the annotation `@Documented` is present on the declaration of an annotation interface _A_, then any `@A` annotation on an element is considered part of the element's public contract.                |
| [ElementType](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/ElementType.html)                                         | The constants of this enumerated class provide a simple classification of the syntactic locations where annotations may appear in a Java program.                                                        |
| [IncompleteAnnotationException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/IncompleteAnnotationException.html)     | Thrown to indicate that a program has attempted to access an element of an annotation interface that was added to the annotation interface definition after the annotation was compiled (or serialized). |
| [Inherited](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Inherited.html)                                             | Indicates that an annotation interface is automatically inherited.                                                                                                                                       |
| [Native](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Native.html)                                                   | Indicates that a field defining a constant value may be referenced from native code.                                                                                                                     |
| [Repeatable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Repeatable.html)                                           | The annotation interface `java.lang.annotation.Repeatable` is used to indicate that the annotation interface whose declaration it (meta-)annotates is _repeatable_.                                      |
| [Retention](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Retention.html)                                             | Indicates how long annotations with the annotated interface are to be retained.                                                                                                                          |
| [RetentionPolicy](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/RetentionPolicy.html)                                 | Annotation retention policy.                                                                                                                                                                             |
| [Target](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/annotation/Target.html)                                                   | Indicates the contexts in which an annotation interface is applicable.                                                                                                                                   |
{% endtab %}
{% endtabs %}
