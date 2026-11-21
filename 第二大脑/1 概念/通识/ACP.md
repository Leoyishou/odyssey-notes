---
uid: 02c6690f-d9ff-4fee-8974-24ed1ddd2886
date created: 2026-11-21
aliases: []
date modified: 2026-11-21
---
#  💡Summary  

> [!Info]
> **ACP 是 Agent Client Protocol**，可以理解为“Agent 界的 [[LSP]]”。
> 



# 🧩 Cues



# 🪞Notes



### **它解决什么问题**

编辑器或客户端（Zed、JetBrains、Neovim、T3 Code 等）想接入编程 Agent（Gemini CLI、Claude Code、Codex 等）时，如果每一对都单独写一套对接代码，工作量就是 N × M。

ACP 定了一套统一的“对话规则”：

- 只要客户端支持 ACP，就能接入任何支持 ACP 的 Agent；
- 只要 Agent 支持 ACP，就能被任何支持 ACP 的客户端使用。

这和 LSP（语言服务器协议）让任何编辑器都能获得各种语言的补全、跳转是同一个思路。

### **基本情况**

- **发起者**：Zed 编辑器团队，2025 年推出。
- **原理**：客户端把 Agent 作为子进程启动，双方通过标准输入输出用 JSON-RPC 通信。内容包括发送提示词、流式返回结果、请求执行命令或修改文件的权限、展示 diff 等。
- **支持情况**：Gemini CLI 原生支持；Claude Code、Codex 等一般通过社区或官方的**适配器**（adapter）接入。

### **作者为什么说别用**

主要有两个原因（结合上一段原文推断）：

1. **中间多了一层翻译**：Agent 原生的很多能力（各自特有的功能、状态、事件）在协议里没有对应字段，转换时会丢失或变形。
2. **只能取“最大公约数”**：协议只覆盖各家都有的通用功能，体验通常不如 T3 Code 对 Codex 或 Claude 的原生直连。

所以他的意思是：在 T3 Code 里直接用它原生支持的 Agent，不要通过 ACP 去接别的 Agent。

NOTE

还有一个同名缩写 **Agent Communication Protocol**（IBM 发起，用于 Agent 之间互相通信），和这里说的不是一个东西。