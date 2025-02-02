# 从 0 到 #114，开源的 DevOps 知识平台 Ledge 经历了什么？ 

开源，开心就好。过去的半个月里，我们做了这么一些事情：

1. 用户体验增强
2. 提升系统的稳定性和质量
3. 测试智库
4. 新的 Ledge 渲染器
5. 新的工具
6. 新增 5 家 DevOps 解决方案
7. 更多的内容

还有 Ledge 2.0

## 数据小结

半个月前，我们在 GitHub 上开源了 Ledge （ https://github.com/phodal/ledge ） ，在这段期间里，我们的提交总数达到了 1157 次，收到了 39 个 pull request，75 个 issues（其中还有 10 个待解决）。在国内 996 常态的世界里，它已经是相当不错的成绩。[狗头]。

在过去的半个月里（04.02~至），GitHub 上的 Traffic 达到了 6000+。加上 04.02 之前的流量，已经有 10,000。我们还受到了 638 个开发者的收藏（star），还上了几次 GitHub Trending。


Google Analysis 上捕捉到流量也能稳定在 300 左右。


在这个项目里，我们有了 8 个核心的成员，我们在业余的时间贡献到了上面。


你可以在 GitHub 上看到所有的 `contributors`，我们也将他/她们加到 Ledge 的首页上：

还有一些优秀的小伙伴，在我们的微信群里为这个项目提出了宝贵的意见。

## 1. 用户体验增强

我们的优秀的 UX 小伙伴 郭晋，在业余时间，设计了全新的 Ledge Logo：


并设计了全新的首页，小伙伴王玲重新实现了导航栏：

受到了 Ledge 用户的夸奖（这个意思是我原来的设计太丑了）

顺带在广大小伙伴的要求之下，重新设计了侧边栏。（好吧，原来的菜单是真的丑）

在刘宇的强力支持下，我们拆出了 Ledge Render，并使用基于 Scully 框架的 SSG 技术，优化了整个网站的速度。

同时，我们在国内的服务器部署了一个镜像站：[https://ledge.wdsm.io/](https://ledge.wdsm.io/)

## 2. 提升系统的稳定性

毫无疑问，如果你关注 Ledge 项目的话，会发现上面有一个用户 ID 为 ConnieYXN（于晓南） 提了大量的 issue（虽然我不太想，但是能修的都修了）：



## 3. 测试智库

我司（ThoughtWorks）的资深咨询师于晓南，也在业余时间建了一个测试智库，丰富的测试体系相关的内容：


## 4. 全新的 Ledge 渲染器

我们在上周发布了全新的 Ledge Markdown 渲染器，基于 markdown 的 AST，我们构建了自己的 markdown 渲染器，并且发布成一个独立的库 `@ledge-framework/render` ，你可以在你的 Angular 项目中使用它：

在这个新的渲染器里，@giscafer、@HuJinNan1 更新了新的渲染器组件：

## 5. 新的工具

我们也发布了一些新的工具。可实时化编辑的 Ledge 编辑器（功能待进一步增强）：

还有新项目、敏捷实践、DevOps 检查清单，可以帮助你完善项目：

## 6. DevOps 解决方案

在过去的两周里，我们陆续和 Coding.net、腾讯云-云开发、Worktile、fir.im、禅道等达成了合作关系。它们会在 Ledge 平台上提供他们的 DevOps 方案：

还有相关对应的 DevOps 成功案例：


## 7. 更多的内容

大家都懂。

## Ledge 2.0

Ledge 作为一个开源的平台，人力、财力、物力和精力有限，但是我们相信开源的社区文化，会帮助 Ledge 建设得更好。

除了完善现有的案例、解决方案、工具，我们在 Ledge 2.0 里，计划引入这些新的能力：
 
 - 国际化支持
 - 基于微前端 + Web Components 的插件化架构
 - 流畅的、半自动化的 DevOps 可交互实施过程
 - Ledge 知识平台框架（沉淀开放现有的能力）
 - BizDevOps 流程设计
 - 研发代码化原型设计（3.0）

如果你对 DevOps、软件研发效能提升有兴趣，有前端开发能力等等。

欢迎来加入 https://github.com/phodal/ledge ，一个未来的知名 GitHub 加分项目。



