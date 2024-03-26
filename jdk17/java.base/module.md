---
description: >-
  https://docs.oracle.com/en/java/javase/17/docs/api/java.base/module-summary.html
---

# java.base

Module `java.base`

定义 Java SE Platform 的基础 APIs。

### Providers:

该模块 JDK 提供了 jrt [file system provider](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/nio/file/spi/FileSystemProvider.html) 的实现，用来列举和读取运行时映像中的类和资源文件。可以通过调用 [`FileSystems.newFileSystem(URI.create("jrt:/"))`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/nio/file/FileSystems.html#newFileSystem\(java.net.URI,java.util.Map\)) 来创建 jrt 文件系统。

### Module Graph:

[![Module graph for java.base](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/module-graph.svg)](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/module-graph.svg)

### Tool Guides:

[java launcher](https://docs.oracle.com/en/java/javase/17/docs/specs/man/java.html), [keytool](https://docs.oracle.com/en/java/javase/17/docs/specs/man/keytool.html)

### Since:

9

## Packages

{% tabs %}
{% tab title="Exports" %}
| Package                                                                                                  | Description              |
| -------------------------------------------------------------------------------------------------------- | ------------------------ |
| [java.io](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/package-summary.html)     | 通过数据流、序列化和文件系统提供系统输入和输出。 |
| [java.lang](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/package-summary.html) | 提供对Java编程语言的设计至关重要的类。    |
| [java.lang.annotation](../module/java.lang.annotation/)                                                  | 为Java编程语言的注释功能提供库支持。     |
| ...                                                                                                      | ...                      |
{% endtab %}
{% endtabs %}

## Services

{% tabs %}
{% tab title="Provides" %}
| Type                                                                                                                         | Description |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------- |
| [FileSystemProvider](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/nio/file/spi/FileSystemProvider.html) |             |
{% endtab %}

{% tab title="Uses" %}
| Type                                                                                                                                               | Description                                                                           |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| [AbstractChronology](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/chrono/AbstractChronology.html)                        | An abstract implementation of a calendar system, used to organize and identify dates. |
| [AsynchronousChannelProvider](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/nio/channels/spi/AsynchronousChannelProvider.html) | Service-provider class for asynchronous channels.                                     |
| ...                                                                                                                                                | ...                                                                                   |
{% endtab %}
{% endtabs %}
