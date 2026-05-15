---
name: prd:init
description: "阶段0：初始化配置检测"
---

# 阶段0：初始化配置检测

## 执行时机

**每次调用 `/prd-workflow` 时首先执行**

---

## 检测逻辑

### Step 1: 检测memory目录是否存在

检查路径：`~/.claude/projects/prd-workflow/memory/`

| 状态 | 处理 |
|------|------|
| 目录不存在 | 执行初始化流程 |
| 目录存在但prd_config.md未配置 | 执行配置引导 |
| 目录存在且已配置 | 跳过初始化，进入阶段1 |

---

## 初始化流程

### Step 2: 创建memory目录

使用Bash工具创建目录：

```bash
mkdir -p ~/.claude/projects/prd-workflow/memory/
```

### Step 3: 复制模板文件

将 `memory-templates/` 下的文件复制到 `projects/prd-workflow/memory/`：

| 模板文件 | 目标文件 |
|----------|----------|
| MEMORY.md | MEMORY.md |
| soul.md | soul.md |
| prd_config.md | prd_config.md |
| template_paths.md | template_paths.md |
| user_profile.md | user_profile.md |
| project_contacts.md | project_contacts.md |
| feedback_history.md | feedback_history.md |
| git_config.md | git_config.md |

使用Bash工具复制：

```bash
cp ~/.claude/skills/prd-workflow/memory-templates/*.md ~/.claude/projects/prd-workflow/memory/
```

---

## 配置引导流程

### Step 4: 引导用户填写必须配置

使用AskUserQuestion工具询问：

```
> 检测到PRD工作流首次运行，需要进行初始化配置。
> 
> 请填写以下信息：
```

**必须配置：**

| 配置项 | 说明 | 示例 |
|--------|------|------|
| 文档仓库根目录 | PRD文档存放的根路径 | `/Users/张三/Documents/Knowledge/development/` |

询问方式：

> **1. 文档仓库根目录**（必须）
> 
> 你的PRD文档存放的根目录路径是什么？
> 
> 例如：`/Users/张三/Documents/Knowledge/development/`
> 
> 请输入路径：

**可选配置：**

> ---
> 
> **2. 用户身份信息**（可选，可跳过）
> 
> - 你的角色：？（如：产品经理、需求分析师）
> - 你的职责：？（如：需求评估、原型设计）
> 
> 如需配置请填写，或输入"跳过"稍后配置：

---

### Step 5: 更新配置文件

用户输入后，使用Edit工具更新 `prd_config.md`：

将 `{待用户配置}` 替换为用户输入的路径。

如用户填写了身份信息，同时更新 `user_profile.md`。

---

### Step 6: 确认初始化完成

输出确认信息：

```markdown
## 初始化完成

**配置文件已生成：**
- 文档仓库根目录：`{用户输入的路径}`
- 模板路径：已自动配置

**下一步：**
- 在文档仓库创建 `projects/workflow/prd-workflow/` 目录
- 放入模板文件：`（简单版本）产品需求文档`、`（完整版本）产品需求文档`

现在开始进入需求澄清阶段...
```

然后自动进入阶段1（需求澄清）。

---

## 已初始化用户的处理

当memory目录已存在且已配置时：

直接读取 `prd_config.md` 获取配置信息，跳过初始化，进入阶段1。

---

## 快速模式处理

`/prd-workflow quick` 时：

- 仍需执行初始化检测
- 如未初始化，执行最小化初始化（仅配置必须项）
- 询问简化，直接要求输入文档仓库根目录