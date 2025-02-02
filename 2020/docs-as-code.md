# 文档代码化

> 文档代码化，将文档以类代码的领域特定语言的方式编写，并借鉴软件开发的方式（如源码管理、部署）进行管理。它可以借助于特定的工具进行编辑、预览、查看，又或者是通过专属的系统部署到服务器上。面向非技术人员的文档代码化的一种常见架构模式是：[编辑-发布-开发分离](https://www.phodal.com/blog/editing-publishing-coding-seperate/)』，

最近一个月里，我在开发一个基于 Git + Markdown 的全新文档系统。我定制了一个基于 markdown 的标记语言，以支持起雷达图、条形统计图、思维导图等图表的文档系统。这个系统将在未来几个月内发布。当然了，视进度而看，也可能是月底。

过去的几年里，我们一直在讨论各种各样的代码化，基础设施代码化、设计代码化、需求代码化……。在我的那一篇《[云研发：研发即代码](https://github.com/phodal/cloud-dev)》中，设计了一个完全代码化的软件开发流程。而今天我们将讨论另外一个有趣的存在：文档。

在《[架构金字塔](https://www.phodal.com/blog/architecture-pyramid/)》中，我将文档定义为支撑五层架构模型的一种存在。因为文档在一个系统中是非常重要的存在，我们用它来指导开发工作，用它来记录问题，用它来写下规范……。总而言之，它很重要，所以我们重新讨论一下这个话题。

## 引子 1：架构决策记录：格式化文档

三年前，当我第一次接触到『[架构决策记录](https://www.phodal.com/blog/documenting-architecture-decisions/)』的概念时，我被它的理念所吸引：

 - 使用轻量级文本格式化语言描述重大决策
 - 跟随代码一起版本化
 - 使用某种特定的文档格式（标题、上下文、决策、状态、后果）

随后，我使用 Node.js + TypeScript 写了一个 [ADR](https://github.com/phodal/adr) 工具。现在，在我的大部分开源荐中，我都会使用它来管理一些技术决策。因为基于这个理论设计的这个文档系统真非常棒，我可以查询到：

 - 一个技术决策发生的时间和架构改变，对应的修改人
 - 回溯所有的技术决策，从中整理出架构发展过程
 - 所有的决策都是记录在版本控制系统中，可恢复
 - 易于管理和维护

对于一个长期开发的系统来说，它真的非常有用。

## 引子 2：静态站点生成：数据代码化

> 静态站点生成是一种混合式的 Web 开发方法，它通过部署预先构建的静态文件进行部署，来让开发者在本地构建基于服务器的网站。

当 GitHub Pages 成为了程序员首选的 博客/内容/文档 服务器时，他/她也采用了静态站点生成这一项技术。静态站点生成有各种各样的优点：

 - 可靠性、安全性、稳定性、可用性等更好
 - 可版本控制
 - 易于测试
 - 易于实践持续部署。提交即可上线
 - 灵活，易于定制

而事实上，静态站点生成所做的最主要的一件事是：将数据库中的数据进行代码化。采用诸如 Wordpress 这样的 CMS 时，我们是将数据存储在数据库中，以实现对于数据的 CRUD。一篇文章变为数据库二进制文件中的一个片段。

随后，静态站点生成工具做了第二件事情便是将文本内容可视化出来，便于人们阅读。这样一来，我们便实现了发布-开发分离。

## 引子 3：定制的标记语言：扩充

将数据代码化时，我们面临了一个非常大的挑战：易于编写、阅读的标记语言（如 markdown）只设计了内容的形式，缺少了内容相关的其它信息，诸如于创建时间、作者、修改时间等等。

于是各个静态站点生成器定制了自己的 markdown，添加了一些额外的信息，如 hexo 采用 `:year-:month-:day-:title.md` 的形式来管理文章的日期和标题等。这样一来说，就不需要通过读取这个文章的 Git 信息来构建出整个信息。

我们所熟悉的 GitHub Flavored Markdown 也是如此，通过不明显破坏内容格式的兼容模式来扩展 markdown 数据字段。

除此，我们可以定制基于 markdown 数据的图表、思维导图等内容。

## 引子 4：编辑-发布-开发分离：面向非技术人员

面向非技术人员设计是代码文档化的一大挑战。作为一个程序员，我们觉得 markdown 语法再简单不过了，但是对于非技术人员来说并非如此。他/她需要：一个易于上手的可视化编程器。而要实现这样一个目的，我们需要在架构上做一些转变，我们可以尝试使用 『编辑-发布-开发分离』 模式来解决这个问题。

即，我们将过程拆为了三步：

 - 编辑人员，可以使用常用的编辑器或者是定制的编辑器
 - 开发人员，编写内容的展示
 - 发布的时候，集成这两部分代码

我们依旧可以选择用源码管理的方式来管理内容。只需要将数据库接口，转变为 Git 服务器接口即可 —— 当然它们是稍有不同的。不过呢，把本地的 Git 转换为 Git remote 那就基本一致了。

如此一来，最后我们的成本就落在改造出一个基于 Git 的 markdown 编辑器。

## 文档代码化

完美，我又一次在引子里，把中心思想表达完了。

### 为什么你需要将文档代码化？

主要原因有：文档不代码化，就没有重构的可能性。

剩下的原因有：

 - 二进制的文档难以进行版本管理。想象一下 `2020-02-30.docx` 和 `2020-02-31.docx`。
 - 无法准确地知道谁是文档的修改者，大家可能都是 admin，又或者是会议上的张三
 - 找不到哪个是最新的文档
 - 文档写得很烂，但是你没办法重构二进制文档
 - 供应商绑定
 - ……

应该还有更多。

### 什么是文档代码化？

回到正题上：

> 文档代码化，将文档以类代码的领域特定语言的方式编写，并借鉴软件开发的方式（如源码管理、部署）进行管理。它可以借助于特定的工具进行编辑、预览、查看，又或者是通过专属的系统部署到服务器上。

它具备这么一些特征：

 - 使用标记语言编写内容。如 markdown
 - 可通过版本控制系统进行版本控制。如 git
 - 与编程一致的编程体验（除了内容写不了测试）

而一个高效的文档代码化系统，还具备这么一些特征：

 - 持续部署，即修改完内容可自动发布。
 - 与特定的形式组织内容索引。如以知识库的形式来组织内容。
 - 特定的文本格式。如架构决策记录、静态内容生成，以用于以提供更好的用户体验
 - 可支持 REST API。以通过编辑器来修改内容
 - 可以支持多种方式的输出。如网站标准 HTML，又或者是 Docx、Latex 等
 - 支持编辑、校对工作流
 - 支持搜索
 - 多人协作

而事实上，大部分的团队并不需要上述的高级功能，而且它们都已经有了成熟的方案。

## 如何设计一个文档代码化系统？

事实上，我们在四个引子中标明了我们所需要的要素：

 1. 使用格式化的文档
 2. 借助静态站点生成技术来发布系统
 3. 通过定制标记语言扩充能力
 4. 面向非技术人员实现编辑器

设计一个标记语言及其扩展语法，然后实现它即可。

### 1. 确立关键因素

考虑到我和我的同事们最近实现了这么一个系统，我还是忍受一下手的痛楚，简单说一下怎么做这样一个系统。我们所考虑的主要因素是：

 - 图表渲染
 - 流程图渲染
 - 可视化展示

因为由 DSL 转换成的图表易于修改，并且可以索引。于是乎，我们：

 1. 通过 markdown 的 Code 语法来扩充这些能力
 2. 使用 markdown 的 table 和 list 来提供数据 
 3. 使用 D3.js 来支持流程图绘制
 4. 使用 Echarts 来进行图表绘制
 5. 尽量使用 SVG 图片
 6. ……

### 2. 实现一个 MVP

我们使用 Angular + GitHub，快速实现了一个 MVP：

1. 我们使用 Git 作为数据库.它就可以实现多人协作的目的，并且可以追踪所有的变化
2. 我们使用 GitHub Pages 作为服务器。只要一修改文档或者代码，就会部署最新的文档。
3. 我们使用 marked.js，它可以让我们快速扩展语法。
4. 使用 textarea 结合 markdown 制作了一个简易的编辑器。

随后，我们在这个基础上进行了快速的迭代。

### 3. 扩展语法

我们使用了 markdown 的 `code` 作为图表的 DSL，扩展了这么一些语法：

- echarts。直接渲染 Echarts 图表
- mindmap。Markdown List 转为思维导图
- radar。Markdown List 转为雷达图
- process-table。带流程的图表
- process-step。另外一种带流程的图表 
- pyramid。金字塔图形
- quadrant。四象限图
- class。直接调用 CSS 的 class
- graphviz。使用 Dot 渲染图片
- mermaid。使用 mermaid 可视化
- webcomponents。调用 WebComponents 组件
- toolset。调用 Toolset 相关的组件
  - slider。权衡滑块
  - line-chart。表图

所以，对于使用者来说，只需要编写下面的代码：

```
```radar
 - 质量成熟度评估模型
  - 质量内建: 3 -> 4
  - 优化业务价值: 2 -> 2
  - 质量统一，可视化: 1 -> 5
  - 全员参与: 3 -> 4
  - 快速交付: 4 -> 5
  - 测试作为资产: 2 -> 3
  - 快速反馈: 5 -> 5

config: {"legend": ["当前", "未来"]}
   ```
```

就可以生成对应的图表：

![RadarChart](https://www.phodal.com/static/media/uploads/ledge-star.png)

我们还通过 config 来输入 JSON，进行一定的懒惰化处理（不要累死自己）。

### 3.1 重写 markdown 渲染器

我们在这个过程中，遇到的最大的挑战是，随着我们对 markdown 语法的不断扩充，相关的代码已经变成了一坨大泥球。所以，我们不得不重写了这部分代码：

1. 借助于 marked.js 的 lexer 解析出 token
2. 根据 token 修改生成新的 token
3. 遍历新生成的 token，渲染出元素
4. 结合虚拟滚动，解决性能问题

已经开源在 GitHub，并发布对应的 npm 包：`@ledge-framework/render`。

### 4. 发布这个项目

我们已经在 GitHub 上发布了这个文档化系统，你可以参与到其中的使用和开发。

GitHub：https://github.com/phodal/ledge

项目首页：https://devops.phodal.com/

## 总结 

然后，你就成为了一个 Markdown 工程师，D3.js 设计师，Echart 配置管理员。

