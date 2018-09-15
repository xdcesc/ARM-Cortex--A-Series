# 第五章：ARM/Thumb 统一汇编语言指令

这一章是 ARM/Thumb 汇编语言的一般介绍。它没有提供每条指令的详细内容，单独一条指令的描述可以在附录 A 指令摘要中找到。

指令大致可以放在以下几个类中:

* Data processing operations \(ALU operations such as ADD\).
* Memory access \(load and stores to memory\).
* Control flow \(for loops, goto, conditional code and other program flow control\)
* System \(coprocessor, debug, mode changes and so forth\).

我们会简单的对每一个按顺序简介，在这之前，先让我们查看不同的指令类所共有的功能。

