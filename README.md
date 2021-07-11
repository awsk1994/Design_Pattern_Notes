**优先读**

- 策略，观察，迭代，模板方法

# 设计模式笔记（Design Patterns Notes)

- 创建型模式 (Creational Pattern)
  - [单例模式（Singleton Pattern)](./creational_patterns/singleton_pattern.md)
  - [工厂模式（Factory Pattern)](./creational_patterns/factory_pattern.md)
  - [建造模式（Builder Pattern)](./creational_patterns/builder_pattern.md)
  - [原型模式（Prototype Pattern)](./creational_patterns/prototype_pattern.md)

- 行为模式（Behavioral Pattern）
  - [命令模式（Command Pattern)](./behavioural_patterns/command_pattern.md)
  - [责任链模式（Chain of Responsibility Pattern）](./behavioural_patterns/chain_of_responsibility_pattern.md)
  - [策略模式（Strategy Pattern）](./behavioural_patterns/strategy_pattern.md)
  - [状态模式（State Pattern）](./behavioural_patterns/state_pattern.md)

- 结构型模式（Structural Pattern）
  - [适配器模式（Adapter Pattern)](./structural_patterns/adapter_pattern.md)
  - [修饰器模式（Decorator Pattern)](./structural_patterns/decorator_pattern.md)
  - [代理模式（Proxy Pattern)](./structural_patterns/proxy_pattern.md)

## Introduction

### 设计模式是什么？

- 软件设计中常见问题的典型解决方案。
- 模式并**不是一段特定的代码**， 而是解决特定问题的**概念**。

### 模式和算法一样吗？

- 算法像是菜谱：提供达成目标的明确步骤
- 模式更像是蓝图：比较**高层次描述**。

### 类型

- 创建型模式 (Creational Patterns)
  - 这类模式把类的**实例化过程抽象化**
    - 意思是外界只需要知道它们的接口，不需要知道实现细节即可
    - 目的是把对象的创建和使用分离。
  - 例子：Singleton, Builder, Factory (simple, factory method, abstract factory)

- 结构型模式 (Structural Patterns)
  - 这类模式介绍**如何将类或者对象结合**在一起形成更大的结构。
  - 例子：Decorator

- 行为模式 （Behavioral Patterns）
  - 这类模式负责对象间的高效沟通和职责委派。
  - 例子：Observer

## Sources

- 《深入浅出设计模式》
- <https://www.runoob.com/design-pattern>
- <http://c.biancheng.net/design_pattern/>
- <https://www.runoob.com/design-pattern/design-pattern-tutorial.html>

# Other Sources

## General

- 这九种常用的设计模式你掌握了吗: <https://zhuanlan.zhihu.com/p/270188809>
- Nice-looking des patt site: <https://refactoringguru.cn/design-patterns/builder>
- C++ code des patt: <https://www.cnblogs.com/chengjundu/p/8473564.html>
- Java code des patt: <https://www.cnblogs.com/nov5026/p/8250464.html>

## Specific

- 简单工厂模式 工厂方法模式 抽象工厂模式 对多态的理解：<https://zhuanlan.zhihu.com/p/52076338>
- 工厂方法模式（Factory Method）- 最易懂的设计模式解析:<https://www.jianshu.com/p/d0c444275827>
- 抽象工厂模式（Abstract Factory）- 最易懂的设计模式解析:<https://www.jianshu.com/p/7deb64f902db>

## cannot open (VPN problem?)

- <https://design-patterns.readthedocs.io/zh_CN/latest/creational_patterns/factory_method.html>
