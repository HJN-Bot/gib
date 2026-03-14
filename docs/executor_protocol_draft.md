# Executor Protocol Draft v0.1 (Dify + n8n + OpenClaw)

## 目标
统一最小执行边界与路由决策协议，让多Agent可复用、可审计、可扩展。

## A. 最小执行白名单（MVP）
### A1. 允许自动执行（无需人工确认）
1. 读取类：读取本地文档、读取已授权知识源、生成摘要
2. 转换类：转录、提炼、结构化卡片生成（不对外发布）
3. 同步类：写入内部仓库（GitHub私有/指定仓库）、写入Dashboard摘要
4. 通知类：向指定Agent频道发送进度回执

### A2. 需要人工确认（Approval Gate）
1. 外部发布（公开平台发布、外发邮件、外部群发）
2. 权限变更（新增密钥、修改账号权限）
3. 数据删除/覆盖（删除记录、批量覆盖）
4. 涉敏数据出域（导出或发送到外部系统）

### A3. 禁止自动执行（Denied）
1. 未授权目标系统写入
2. 绕过审批Gate直接执行高风险动作
3. 未记录审计日志的关键变更

## B. 路由决策草案（Decision Router）
### B1. 输入字段（统一）
- intentType: ingest | synthesize | decide | execute | report
- riskLevel: low | medium | high
- requiresApproval: true | false
- targetSystem: dify | n8n | openclaw | github | feishu | dashboard
- sla: fast(<2m) | normal(<10m) | deep(>10m)

### B2. 路由规则（v0）
1. low risk + fast => OpenClaw direct
2. ingest/schedule/retry => n8n
3. long-context reasoning / KB QA => Dify/NotebookLM
4. high risk OR requiresApproval=true => Human Gate first
5. multi-step with artifacts => n8n orchestrates + OpenClaw writeback

### B3. 输出字段（统一）
- routePlan: [step1, step2, ...]
- approverNeeded: yes/no
- expectedArtifacts: list
- rollbackPlan: one-line rollback

## C. 状态机（执行闭环）
selected -> running -> artifact_written -> status_updated -> reported

异常状态：blocked | timeout | failed

每个状态都必须回写：timestamp / ownerAgent / taskId(sessionId) / nextAction

## D. 明日执行清单（Draft）
1. 评审白名单条目（确认 A1/A2/A3）
2. 评审路由规则 B2（补充你的偏好）
3. 选 1 条真实任务做 E2E 冒烟
4. 固化为 `executor_contract.json` 并接入编排

## E. 验收口径
- 同一任务在 Dify/n8n/OpenClaw 的状态语义一致
- 高风险动作均触发人工确认
- 每次执行都有可追踪日志与可回滚说明
