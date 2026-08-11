<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/cairn-dark.svg">
    <img alt="石堆 Cairn" src="assets/cairn-light.svg" width="760">
  </picture>
</p>

# 石堆 Cairn

**一套让多智能体工作在跨会话、跨工具、跨机器后仍可恢复的模式语言。**

<p>
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-3d7a5a"></a>
  <img alt="状态：早期预览" src="https://img.shields.io/badge/status-early%20preview-6b7280">
</p>

[先做自诊断](docs/02-signs-you-need-this.md) · [浏览失败模式](docs/04-failure-modes.md) · [复制交接模板](templates/handoff-frontmatter.md) · [English](README.md)

## 为什么需要石堆

长周期工作经常能在一次会话里推进，却在交给下一次会话时失效：

- 真实状态只存在于聊天记录和人的记忆里；
- 必要产物还不存在，状态却已经写成“完成”；
- 多份文件同时声称自己代表当前状态；
- 审批结论随着承载它的聊天一起消失；
- 更换工具或机器后，项目必须从头解释。

石堆把这些视为架构问题，而不是文档没写好的偶发问题。它提供共享词汇、常见失败目录和协议骨架；具体角色、文件格式和工具仍由你决定。

> 石堆不是运行时，也不是多智能体编排器。它是你设计自己工作套件时使用的图纸。

如果你听说过 **The Twelve-Factor App**——那份文档不运行任何应用，只讲一个应用该具备哪些特质。石堆做的是同一件事，只是把对象从 Web 应用换成了跨会话的多智能体工作。

## 10 分钟开始采用

1. **先做诊断。** 用 [Signs you need Cairn](docs/02-signs-you-need-this.md) 勾选当前真实存在的症状。
2. **只选一个代价最高的失败。** 在[失败模式目录](docs/04-failure-modes.md)中找到它的根因和修复方向。
3. **先采用一种共享工件。** 可以从[交接模板](templates/handoff-frontmatter.md)，或 [PS-02 冷读面](docs/07-protocol-skeletons.md#ps-02--cold-read-surface-current-file)开始。
4. **测试一次真实换班。** 让一个新会话在没有人工复述的情况下恢复状态。
5. **只增加被实际失败证明有必要的部分。** 石堆不要求一次性全量采用。

完整的小型示例见 [First adoption](examples/first-adoption.md)。

## 你会得到什么

| 入口 | 提供什么 | 什么时候使用 |
|---|---|---|
| [自诊断](docs/02-signs-you-need-this.md) | 16 个可观察的连续性信号 | 判断问题是局部摩擦还是结构性风险 |
| [词汇表](docs/03-glossary.md) | 9 个状态词、6 个关键区分、4 个证据等级 | 不同角色对“完成”“阻塞”“已验证”理解不一致 |
| [失败模式](docs/04-failure-modes.md) | 12 类触发、症状、根因和修复方向 | 在重新设计流程前先准确命名问题 |
| [协议骨架](docs/07-protocol-skeletons.md) | 交接、冷读面、决策队列、角色契约、限定范围复议 | 一个持久工件需要跨领域可复用的形状 |
| [交接模板](templates/handoff-frontmatter.md) | 可复制 frontmatter、正文轮廓、detached anchor 验证 | 工作要跨越会话、工具、机器或受众 |
| [采用示例](examples/first-adoption.md) | 从 chat-only 状态到可验证冷启动的一次增量采用 | 想看最少几个组件如何协作 |

## 核心思想

浮筏时代的工作流把工作真相留在房间里：

```text
会话 → 对话状态 → 会话结束 → 人工重建
```

可恢复的工作流把关键真相移入可检查工件：

```text
会话 → 持久证据 + 派生当前视图 → 独立验证 → 下一会话
```

石堆不规定文件格式、工具链或角色名。它要求保留让独立恢复成为可能的关键区分：

- 已分派不等于已实现；
- 文件存在不等于它具有权威；
- 流程跑完不等于结果有效；
- 消息是传输方式，不是永久记录；
- 只打印数值不等于验证，值不符时必须失败退出。

## 项目状态

石堆目前是早期公开预览版。可用核心已经存在，更完整的指南仍在扩展。

| 现在可用 | 下一步计划 |
|---|---|
| 自诊断、词汇表、失败模式、协议骨架 | 入门定义与症状指南 |
| 交接模板与首次采用示例 | 记录纪律与反模式指南 |
| 贡献和公开材料隐私规则 | 更多模板与实现检查清单 |

“早期预览”表示目录仍可能调整，不表示主导航会把读者带到空占位页。

## 文档

- [判断是否需要石堆](docs/02-signs-you-need-this.md)
- [共享词汇](docs/03-glossary.md)
- [失败模式目录](docs/04-failure-modes.md)
- [协议骨架](docs/07-protocol-skeletons.md)
- [交接模板](templates/handoff-frontmatter.md)
- [首次采用示例](examples/first-adoption.md)

## 石堆不是什么

- 不是 agent runtime、工作流引擎或提示词框架。
- 不是每个项目都必须完整采用的统一流程。
- 不替你决定角色名、存储格式和技术栈。
- 与 Raft 共识算法无关。

## 参与贡献

欢迎提交 issue 和 pull request。请先阅读 [CONTRIBUTING.md](CONTRIBUTING.md)，特别是公开示例的隐私与来源规则；也可以直接[创建 issue](https://github.com/LolerPanda/cairn/issues/new)，描述一个可重复出现的失败类别。

适合入手的贡献包括：改进虚构示例、修复可访问性或链接、报告模式冲突。请描述可重复出现的失败类别，不要公开私有事故细节。

## License

[MIT](LICENSE) © 2026 LolerPanda。
