---
name: prd_config
description: "PRD工作流配置"
type: project
---
# PRD工作流配置

**Why:** 避免每次重复询问已知信息

**How to apply:** 每次调用 `/prd-workflow` 先读取此配置

## 文档仓库路径

**根目录：** `{待用户配置}`

> ⚠️ 初始化时需用户填写，例如：`/Users/张三/Documents/Knowledge/development/`

模板相对路径会拼接此根目录：
- 简单版本：`{根目录}projects/workflow/prd-workflow/（简单版本）产品需求文档`
- 完整版本：`{根目录}projects/workflow/prd-workflow/（完整版本）产品需求文档`

**同事配置方式：** 将此路径改为自己的文档仓库根目录

## 项目集

| 项目集 | 系统 |
|--------|------|
| tms | ETMS、GPS、RMS、PRS |
| erpp | lsp、EAS、crm、OA |
| wms | wms、wcs、qps |

## 需求类型

- `主版本_功能优化/`
- `项目定制化功能/`

## 文件夹结构

```
{需求名称}/
├── 需求调研/
├── 需求文档/
├── 技术文档/
├── 测试文档/
├── 验收文档/
├── 其它文档/
└── HTML原型/
```

## 默认模板

简单版本