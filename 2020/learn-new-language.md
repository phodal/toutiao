# 如何同时学会两门编程语言？

大概在五年前，我写了一篇文章《学习的艺术——如何学好一门技术、语言》，介绍了如何通过复写现有的系统来学习新的技术。而在最近的两次实践中，我发现了一种更高效（hard way）的方式来学习编程语言。因为高效（hard way），所以这并不是银弹。

当然了，这也是我和我的同事在一次讨论中得到的玩笑结论：你只要用 Go 写一个 C++ 的解析器，那么你就既学会了 Go，又学会了 C++。

只是呢，当我开始去做这样的事情的时候，我发现：``It works``。

## 故事 A：两门新语言 Go + Antlr

我在编写 [Coca](https://github.com/phodal/coca) 的时候，使用的是 Golang 作为开发语言，过程中采用了 Antlr 作为语法解析器生成器，解析 Java 语言生成代码的模型。于是乎，我从 hello, world 开始了我的 Go 学习生涯，将它作为编写应用的语言。与此同时，不断修改使用 Antlr 编写的不同语言的语法，以满足我的开发需要。于是，一来一往之间，我大抵对两个语言有了更深入的研究。

可能你对 Antlr 是否是一门语言有些看法。但是从我的角度来看，由于 Antlr 语言是用来声明语言的语法，所以可以称之为 “元语言” (meta-language)。

### 高效法则 1：为主语言编写测试

俗话说得好：测试，能反应一名程序员的真正水平：

1. 短小的函数易于测试
2. 高耦合的代码难以测试
3. 测试用例能体现出代码真正做了些什么。

当你面对一个新的语言，你还会学会对应的测试套装。

### 高效法则 2：修复主语言代码坏味道

对应的方式有多种多样：

1. 找到身边熟悉语言的大佬，一起 pair。
2. 查看一些开源项目的代码，学习如何应用
3. 寻找对应语言的 Design Patterns。如我找到了 [Go Patterns](https://github.com/tmrts/go-patterns)
4. 集成对应语言的 lint 工具，然后有时间就修复。
5. 集成 Code Climate（开源）/ Sonar 等工具，查看建议。
6. ……

### 附赠经验 1：完善元语言语法

大家都懂的，还是得看看使用 Antlr 编写的 AST 代码，这样才能一步步往下走。过程中，还会面对 AST 中的一些问题，查看并修复相关的问题。具体的修复示例可以看看我在 GitHub 上的代码，我就懒得贴代码了。

### 小结 1

尽管我已经用了多年的 Java，但是这次的解析之旅后，我体会最深的莫过于：

1. 中英文概念的统一的对齐。
2. 编程语言中存在一些不常用的语法。
3. 你永远不知道别人会用怎样的方式组织代码。

除此呢，当你习惯了 A 语言之后，初写 B 语言时，总会呈现出 A 语言的一些编程风格，如 OOP 风格的 C 语言，OOP 风格的 Go 语言。不过，我觉得**在我的场景之下**，它的益处可能大于坏处，一来，可以让你通过 Google / StackOverflow 快速上手语法，二来，你可以写出统一风格的不同语言代码（手动狗头），方便于你相互翻译 。

正是如此，才让我对成为代码专家有了一点兴致。

## 故事 B：一门新语言 Kotlin + 其它语言代码

我在编写 [Chapi](https://github.com/phodal/chapi) （一个通用的编程语言解析器，详见后续的文章，或者 GitHub）的时候，我采用的是 Kotlin 作为开发语言，对于我来说，它可以说是一个新语言。启动这个项目的原因是：为了解决 Coca 实现过程中，发现的 Antlr Go Runtime 下的 TypeScript 性能等各种问题，所以找了个 JVM 系的语言，以调用生成的 Antlr Java Runtime 代码。在这个项目中，我要支持 C#、Pascal 等我没用过的语言，为此便需要寻找对应的语言示例，并编写对应的示例。

因此过程中，你学会了 A 语言，然后能看懂了 B 语言，是不是很棒？

### 成长：重构主语言代码

Kotlin 比 Go 好重构的一个原因在于，它和 Java 类似，并且是 JetBrains 的新儿子，所以 IDEA 对它的重构支持非常得好。

重构不是这里的主要话题，在那篇《[项目初期的最优技术实践](https://www.phodal.com/blog/short-time-project-best-practise/)》中，我找到了项目的三个周期：

 - 技术准备期
 - 业务回补期
 - 成长优化期

重构是属于成长优化期要做的事件，你不能再放纵过去的烂代码了。

### 编译测试语言代码

在编写测试用例的过程中，不得不做的一件事情是：编译一下代码。

因为，我遇到过我怀疑这么写，它会编译失败的，然而这是编译成功的。

### 补齐测试语言用例

对于这样的项目来说，代码即测试数据：

```kolin
@Test
internal fun shouldIdentClassName() {
    val code = """
class Outer(i : Int) {
  def foo(x : Inner.type) = x.getI
}
"""

    val container = ScalaAnalyser().analysis(code, "hello.scala")
    assertEquals(container.DataStructures[0].NodeName, "Outer")
    assertEquals(container.DataStructures[0].Type, DataStructType.CLASS)
}
```

如上述代码中的 code 变量的值是 Scala 代码，我们要将其转为 Chapi 制作的数据结构。为此，我们需要一步步寻找每一种可能性，并编写对应的测试。

### 小结 1

故事，还告诉了我们另外一件事：通过应用语言，我们才会掌握一门语言。

## 所以，方法呢？

没有银弹！

使用一个新语言，编写另外一个语言的解析器。这样一来，你就一下子学会了两种新的语言。

你只需要用 Kotlin 写一个 Go 的解析器，那么你就既学会了 Go，又学会了 Kotlin。

你只需要用 Swift 写一个 Rust 的解析器，那么你就既学会了 Swift，又学会了 Rust。

怎么样，是不是赚到了，是不是很高效（hard way）？
