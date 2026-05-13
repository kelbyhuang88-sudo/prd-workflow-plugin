---
name: git_config
description: "内部Git仓库访问配置"
type: reference
private: true
---

# Git仓库配置

> ⚠️ 此文件包含敏感信息（个人访问令牌），请勿同步到GitHub！

## GitLab信息

**仓库地址：** `{待用户配置}`

**访问令牌：** `{待用户配置}`

## 用户信息

**用户名：** `{自动获取}`

**邮箱：** `{自动获取}`

**显示名称：** `{自动获取}`

## 可访问前端项目

> AI自动从GitLab API获取，列出可访问的前端项目

| 项目路径 | 项目名 | 说明 |
|----------|--------|------|
| {项目路径} | {项目名} | {项目描述} |

---

**配置时间：** `{自动记录}`

---

## 令牌获取方式

1. 登录 GitLab → **Settings** → **Access Tokens**
2. 点击 **Add new token**
3. 填写信息：
   - Token name：`prd-workflow`
   - Expiration date：选择有效期（建议1年）
   - Select scopes：勾选 `read_api`、`read_repository`
4. 点击 **Create personal access token**
5. 复制生成的令牌（只显示一次，请妥善保存）