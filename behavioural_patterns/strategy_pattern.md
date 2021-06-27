# 策略模式（Strategy Pattern）

- 定义
  - 定义一系列的算法，把它们一个个封装起来，并且使它们可相互替换

- 主要解决
  - 在有多种算法相似的情况下，使用 if...else 所带来的复杂和难以维护

- 现实例子：旅行的出游方式，选择骑自行车、坐汽车，每一种旅行方式都是一个策略

## 优缺点

- 优点
  - 可以在运行时切换对象内的算法
  - 将算法的实现和使用算法的代码隔离开来
  - 免使用多重条件判断
  - 扩展性良好
    - 开闭原则。 你无需对上下文进行修改就能够引入新的策略。

- 缺点
  - 客户端必须知晓策略间的不同——它需要选择合适的策略。
  - 如果你的算法极少发生改变， 那么没有任何理由引入新的类和接口。 使用该模式只会让程序过于复杂
  - 策略类会增多
  - 所有策略类都需要对外暴露

## 角色

<img src="./img/strategy_pattern_1.png"/>

- 上下文 （Context） 
  - 维护指向具体策略的引用， 且仅通过策略接口与该对象进行交流。
- 策略 （Strategy） 
  - 具体策略的通用接口
- 具体策略 （Concrete Strategies） 
  - 实现了上下文所用算法的各种不同变体。
- 客户端 （Client） 
  - 会创建一个特定策略对象并将其传递给上下文。 上下文则会提供一个设置器以便客户端在运行时替换相关联的策略。

Notes:

Difference between strategy, command and chain of responsibility: At the end of the day, strategy pattern represents that the strategies are doing the same thing.

Expansion - if need to use if-else can use factory method
Interesting discussion between strategy pattern; esp about People from the US are addressed as Mr/Ms/Mrs, People from Mexico are addressed as Senor/Senorita/Senora: https://softwareengineering.stackexchange.com/questions/418391/advantages-of-strategy-design-pattern-versus-simple-if-else

Interesting usage: each strategy controls a variable and abstract class does the calculation, can prevent re-writing the same calculation logic: https://www.jetbrains.com/help/idea/replace-conditional-logic-with-strategy-pattern.html

Interesting fix ifelse method: https://betterprogramming.pub/chain-of-responsibility-to-the-rescue-2288471c783b
