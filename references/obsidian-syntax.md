---
name: obsidian-syntax
description: "Obsidian笔记特性语法参考"
---

# Obsidian特性语法

## 1. 双链 [[]]

```markdown
[[文件名]]           # 基础
[[文件名|显示名]]     # 自定义显示
[[文件名#章节]]       # 链接章节
```

**应用：** 引用历史需求、技术方案

## 2. Dataview查询

```markdown
```dataview
TABLE priority, status
FROM "projects/tms/ETMS"
WHERE contains(file.path, "需求")
SORT priority ASC
```
```

**字段需在frontmatter定义：**
```markdown
---
priority: P0
status: 进行中
---
```

## 3. Callout

```markdown
> [!warning] 注意
> 重要提示

> [!tip] 建议
> 操作建议

> [!note] 说明
> 补充说明
```

## 4. Frontmatter

```markdown
---
name: 文档名称
priority: P0
status: 待评审
created_time: 2026-05-12
owner: 负责人
---
```

## 5. 标签

```markdown
#需求文档 #ETMS #P0
```

## 6. 任务列表

```markdown
- [ ] 未完成
- [x] 已完成
- [/] 进行中
```

## 7. Mermaid渲染

Obsidian原生支持：
- flowchart
- sequenceDiagram
- stateDiagram-v2
- gantt
- timeline