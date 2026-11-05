---
uid: 98cc30ae-f711-46b6-bcb2-d5a1ea8c78e5
date created: 2026-11-04
aliases: []
date modified: 2026-11-04
---
#  💡Summary  

> [!Info]
> 一句话说清楚
> 


1. 主模型的一个 session 持续接力
	1. 健康上下文沿用原生压缩，默认阈值为 90%，允许按模型覆盖。
	2. 故障恢复时，交接内容由代码整理，不调用额外交接 Agent；**产品 session ID 保持不变，只重建底层模型线程**
2. 主模型一个 session路由到任务模型多个 subagent session
	1. **有 Bot–>Subagent Session 关联表**，主对话固定复用；后台工作靠明确任务 ID 续接。
3. Proactive
	1. 定时任务：如每天检查邮件、每周整理待办
	2. 事件驱动：如任务SubAgent 的 Session出错、卡住、等待回答、完成交付


# 🧩 Cues



# 🪞Notes

1. Cindy 里 MCP 的机制是两层：先把服务器加到 Cindy 里，再逐个伙伴决定挂不挂上。加进 Cindy 不等于所有伙伴都能用。