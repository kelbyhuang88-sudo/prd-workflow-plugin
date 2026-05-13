---
name: prd:workflow
description: "产品需求文档工作流 - 从需求澄清到PRD、原型、甘特图的完整流程"
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - AskUserQuestion
---

# PRD Workflow - 产品需求文档工作流

## 角色定位

产品经理助理，协助完成需求文档的标准化输出。

## 调用方式

| 命令 | 功能 | 说明 |
|------|------|------|
| `/prd-workflow` | 完整流程 | 阶段0→1→2→3→4→5 |
| `/prd-workflow quick` | 快速模式 | 紧急需求，跳过可选阶段 |
| `/prd-workflow html` | 仅原型 | PRD已完成，绘制HTML原型 |
| `/prd-workflow gantt` | 仅甘特图 | 开发评审后，生成甘特图 |

### 参数处理

Skill接收参数后，按以下逻辑处理：

| 参数 | 处理方式 |
|------|----------|
| 无参数（空） | 执行完整流程：阶段0→1→2→3→4→5 |
| `quick` | 执行快速模式：阶段0→1→2→3→结束 |
| `html` | 跳转到阶段4（HTML原型） |
| `gantt` | 跳转到阶段5（甘特图） |

**注意：** 子命令（quick、html、gantt）不会在命令搜索中显示，直接输入完整命令即可使用。

### 快速模式说明

`/prd-workflow quick` 适用紧急需求场景：

| 正常模式 | 快速模式 |
|----------|----------|
| 阶段1~5全流程 | 阶段1→2→3→结束 |
| 每阶段等待确认 | 核心点确认后直接输出PRD |
| 详细询问 | 最小询问 |
| 询问模板版本 | 默认使用简单版本模板 |

快速模式自动跳过：
- 模板选择询问（默认简单版本）
- HTML原型阶段
- 甘特图阶段
- 详细现状材料读取

## 流程控制

### 智能询问

根据用户输入智能判断：
- 未得到答案 → 依次询问
- 已得到答案 → 自动识别跳过

### 回退与跳转

用户可在任意阶段说：

| 命令 | 效果 |
|------|------|
| "返回阶段X" | 回退到指定阶段重新处理 |
| "跳过原型" | 跳过阶段4，直接结束或进入甘特图 |
| "暂停" | 保存当前进度，提示下次继续方式 |
| "继续" | 从上次暂停处继续 |

## 前置检查

### 1. 初始化检测（首次运行）

**每次调用首先执行初始化检测：**

检查 `~/.claude/projects/prd-workflow/memory/` 是否存在：
- 不存在 → 执行初始化流程，引导用户配置
- 存在且已配置 → 直接进入阶段1

**初始化流程：**
1. 复制模板文件到 `projects/prd-workflow/memory/`
2. 引导用户填写文档仓库根目录（必须）
3. 询问用户身份信息（可选，可跳过）
4. 确认初始化完成，自动进入阶段1

### 2. 加载用户记忆

读取 `~/.claude/projects/prd-workflow/memory/MEMORY.md` 获取：
- 用户身份信息
- 文档仓库路径
- 模板配置
- 常用联系人
- 输出格式偏好

### 3. 确认工作目录路径

检查用户是否已提供需求文件夹路径：
- 已提供完整路径 → 直接进入阶段1
- 未提供或部分提供 → 通过 AskUserQuestion 询问

### 4. 文档仓库根目录

从 `~/.claude/projects/prd-workflow/memory/prd_config.md` 读取文档仓库根目录。

模板使用相对路径：
- 简单版本：`projects/workflow/prd-workflow/（简单版本）产品需求文档`
- 完整版本：`projects/workflow/prd-workflow/（完整版本）产品需求文档`

同事下载Skill后，需在各自文档仓库创建相同目录结构。

## 工作流程阶段

| 阶段 | 输出物 | 用户确认点 |
|------|--------|------------|
| 0. 初始化检测 | 配置文件 | 首次运行 |
| 1. 路径确认+需求澄清 | 信息汇总 | 必须 |
| 2. 核心点分析 | 核心点文档 | 必须 |
| 3. PRD文档编写 | PRD文档 | 必须 |
| 4. HTML原型 | 原型HTML | 询问确认 |
| 5. 甘特图 | 甘特图章节 | 可选（开发评审后） |

## 阶段引用

@$HOME/.claude/skills/prd-workflow/stages/00-init.md
@$HOME/.claude/skills/prd-workflow/stages/01-clarify.md
@$HOME/.claude/skills/prd-workflow/stages/02-core.md
@$HOME/.claude/skills/prd-workflow/stages/03-prd.md
@$HOME/.claude/skills/prd-workflow/stages/04-prototype.md
@$HOME/.claude/skills/prd-workflow/stages/05-gantt.md

## 输出规范

- 所有文档使用 Obsidian 兼容格式
- 流程图使用 Mermaid 语法
- 空章节填写"无"，不删除模板章节
- 支持双链语法 `[[文件名]]`
- 支持 Dataview 查询块

## 用户交互规范

- 每阶段输出后等待用户确认
- 简单修改：用户对话告诉AI，AI直接修改
- 复杂修改：用户在Obsidian编辑，完成后回复"已确认，继续"
- 不自动执行Git操作