# Yiki：元微前端框架

PS：Yiki（YY + Wiki）是一些关于软件开发、软件架构新设计的原型思考的 wiki。它针对于一些即将出现的新模式而设计，但是在当前阶段又缺乏足够的时间进行设计。（主要是最近没时间造这个轮子）

在过去的一两年里，从我接受到的一些线上、线下咨询的情况来看，微前端架构被越来越多中大型系统所采用。它们被用于不同类型的问题：

 - 团队间协作
 - 遗留系统改造
 - 通过新技术创造价值（KPI）

这段时间里，也诞生了一个又一个优秀的微前端框架，如为 Angular 设计的 `ngx-planet`，还有适用于多种框架的 Umijs 的 `qiankun`……。

由于不同的微前端框架都源于它们的使用场景，也受限了它们不能满足于其它场景。受限于使用场景，这些微前端框架都需要不同程度的改造，才能满足各自的需要。

 - 支持去中心化架构。如，在不同的场景上，基座/Host 是会发生变化的。
 - 改造遗留系统。如，需要支持更多的框架，太老的框架甚至于需要使用 iframe 作为容器。
 - 对齐组织架构。如，使用前端类容器化技术来解决三方应用的需问题。
 - ……

基于这几种场景，我们原先设计的『基座-子应用』模式无法适用于所有的场景。人们始终需要按照自己的需要，来创建一个这样的框架，所以开发者们需要一个『元微前端框架』。这样一来，他/她们就可以根据自己的需要，组合出自己的微前端解决方案。

就我当前收集到的场景来看，它应该可以满足：

 - 主-从模式架构。传统模式
 - 自组模式。场景 1：基座可替换。场景 2：在基座应用崩溃时，替换基座应用。
 - 微前端框架的微前端框架加载器。场景：将一个基于微前端架构的应用运用环境两个不同团队，同时使用一个微前端框架来加载它们。
 - ……

当然了，还有一些场景，我并没有了解到，欢迎提出你们的场景。

Done!