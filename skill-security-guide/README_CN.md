# Skill Security Guide - 技能安全指南

帮助你的技能通过 ClawHub 安全审查，获得 "Benign" 评级的完整指南。

## 为什么重要

ClawHub 对所有上传的技能进行自动安全扫描。不符合安全标准的技能会被标记为 "Suspicious"，用户在安装前会收到警告。

## 快速开始

### 黄金法则

**SKILL.md 中的 metadata 必须使用 JSON 格式：**

```yaml
---
name: your-skill
description: 技能描述
metadata: {"clawdbot":{"emoji":"🔧","requires":{"bins":["python"],"env":["API_KEY"]},"primaryEnv":"API_KEY"}}
---
```

### 常见错误及修复

| 错误 | 影响 | 修复方法 |
|------|------|----------|
| YAML 格式 metadata | "Required env vars: none" 错误 | 使用 JSON 格式 |
| 禁用 SSL 验证 | "Insecure practices" 警告 | 使用标准 HTTPS |
| 打印敏感信息 | "Sensitive material" 警告 | 只检查变量是否存在 |
| 功能描述误导 | "Behavioral mismatch" 警告 | 准确描述功能 |

## 安全检查清单

提交技能前请检查：

- [ ] Metadata 是 JSON 单行格式
- [ ] 声明了所有需要的 `bins`
- [ ] 声明了所有需要的 `env` 变量
- [ ] 设置了 `primaryEnv`
- [ ] 没有禁用 SSL 验证
- [ ] 没有在日志/输出中打印敏感信息
- [ ] 文档描述与实际行为一致

## 示例

### 优秀示例（Benign 评级）

参考 `tavily-search` 技能：
- 干净的 JSON metadata
- 声明了所有依赖
- 无不安全实践
- 准确的文档

### 问题示例（Suspicious 评级）

常见问题：
- 多行 YAML metadata
- 缺少 env 声明
- 禁用 SSL 验证
- 误导性功能声明

## 与 skill-creator-2 的关系

本技能与 [skill-creator-2](https://clawhub.ai/yixinli867/skill-creator-2) 是**互补关系**，不是替代关系：

| 内容 | skill-creator-2 | clawhub-security-guide |
|------|-----------------|------------------------|
| 技能结构设计 | ✅ 详细指南 | 不涉及 |
| 渐进式披露原则 | ✅ 详细指南 | 不涉及 |
| **ClawHub 安全审查** | ❌ 未涉及 | ✅ **专门讲解** |
| **Metadata JSON 格式** | ❌ 未涉及 | ✅ **核心内容** |
| **SSL/安全规范** | ❌ 未涉及 | ✅ **详细讲解** |
| **安全检查清单** | ❌ 未涉及 | ✅ **完整清单** |

**建议同时使用两个技能**：
1. 使用 `skill-creator-2` 设计和构建技能结构
2. 使用 `clawhub-security-guide` 确保通过 ClawHub 安全审查

## 许可证

MIT
