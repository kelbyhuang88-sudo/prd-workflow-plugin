---
name: template_paths
description: "PRD模板路径"
type: reference
---
# PRD模板路径

## 模板位置

模板文件存放在用户的文档仓库中，使用相对路径：

| 类型 | 相对路径 | 说明 |
|------|----------|------|
| 简单版本 | `projects/workflow/prd-workflow/（简单版本）产品需求文档` | 内部优化、功能增强 |
| 完整版本 | `projects/workflow/prd-workflow/（完整版本）产品需求文档` | 商业化产品、新项目 |

## 文档仓库根目录

用户需要在Memory中配置文档仓库根目录（绝对路径），例如：

```markdown
# prd_config.md
文档仓库根目录：/Users/{用户名}/WorkFile/Knowledge/development/
```

Skill读取模板时会拼接：
`{文档仓库根目录} + {相对路径}`

---

**How to apply:** 
同事下载Skill后，只需：
1. 在自己的文档仓库创建 `projects/workflow/prd-workflow/` 目录
2. 放入两个模板文件（（简单版本）产品需求文档、（完整版本）产品需求文档）
3. 在 `prd_config.md` 配置自己的文档仓库根目录