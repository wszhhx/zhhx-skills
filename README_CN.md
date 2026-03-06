# OpenClaw 技能仓库

[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-blue.svg)](https://openclaw.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

精心策划的 OpenClaw 技能集合，专注于腾讯混元AI服务。

## 📦 可用技能

| 技能 | 描述 | 认证方式 | 版本 |
|------|------|----------|------|
| [hunyuan-image](./hunyuan-image) | 腾讯混元AI图像生成 | 腾讯云 SecretId/SecretKey | 1.0.0 |
| [hunyuan-video](./hunyuan-video) | 腾讯混元AI视频生成 | 腾讯云 SecretId/SecretKey | 1.0.0 |
| [hunyuan-3d](./hunyuan-3d) | 腾讯混元AI 3D生成 | 混元3D API Key (sk-xxxxx) | 1.0.0 |

## 🚀 快速开始

### 方法 1：从 ClawHub 安装（推荐）

```bash
# 列出可用技能
openclaw skills search

# 安装特定技能
openclaw skills install hunyuan-image
```

### 方法 2：告诉你的 Agent 安装

直接告诉你的 OpenClaw 智能体：

> "从 https://github.com/wszhhx/zhhx-skills 安装 hunyuan-image 技能"

智能体会自动：
1. 克隆仓库
2. 安装依赖
3. 配置技能
4. 验证安装

### 方法 3：手动安装

```bash
# 克隆仓库
git clone https://github.com/wszhhx/zhhx-skills.git

# 进入特定技能目录
cd zhhx-skills/hunyuan-image

# 按照 SKILL.md 中的说明操作
cat SKILL.md
```

## 🔑 API 认证指南

### 腾讯云技能（hunyuan-image、hunyuan-video）

**需要**：腾讯云 SecretId + SecretKey

**获取凭证**：
1. 访问 https://console.cloud.tencent.com/cam/capi
2. 点击「新建密钥」
3. 复制 SecretId 和 SecretKey

**配置**：
```powershell
$env:TENCENT_SECRET_ID = "your-secret-id"
$env:TENCENT_SECRET_KEY = "your-secret-key"
```

### 混元3D技能（hunyuan-3d）

**需要**：混元3D API Key（格式：`sk-xxxxx`）

**⚠️ 重要**：这与腾讯云凭证不同！

**获取API Key**：
1. 访问 https://console.cloud.tencent.com/ai3d/api-key
2. 点击「创建API Key」
3. 复制 API Key（格式：`sk-xxxxx`）

**配置**：
```powershell
$env:HUNYUAN_3D_API_KEY = "sk-xxxxx"
```

## 📁 仓库结构

```
zhhx-skills/
├── hunyuan-image/          # 腾讯混元图像生成
│   ├── scripts/
│   ├── SKILL.md
│   ├── README.md
│   └── README_CN.md
├── hunyuan-video/          # 腾讯混元视频生成
│   ├── scripts/
│   ├── SKILL.md
│   ├── README.md
│   └── README_CN.md
├── hunyuan-3d/             # 腾讯混元3D生成
│   ├── scripts/
│   ├── SKILL.md
│   ├── README.md
│   └── README_CN.md
├── README.md               # 英文版本
└── README_CN.md            # 本文件（中文）
```

## 🎯 技能亮点

### 混元图像 (Hunyuan Image)
- 文生图生成
- 多种分辨率和风格
- 参考图支持
- 超分增强（x2/x4）

### 混元视频 (Hunyuan Video)
- 文生视频生成
- 图生视频生成
- 视频风格化（2D动漫、3D卡通等）

### 混元3D (Hunyuan 3D)
- 文生3D生成
- 图生3D生成
- OpenAI兼容接口
- 输出GLB和OBJ格式

## 🛠️ 给技能开发者

### 添加新技能

1. 创建新目录：`your-skill-name/`
2. 添加必需文件：
   - `SKILL.md` - OpenClaw 技能文档
   - `README.md` - 英文文档
   - `README_CN.md` - 中文文档
   - `scripts/` - 实现脚本
3. 更新本 README 包含你的技能
4. 提交 Pull Request

### 技能要求

- 必须包含带有适当元数据的 `SKILL.md`
- 应有清晰的安装说明
- 必须优雅地处理错误
- 应包含使用示例
- 必须记录API认证要求

## 📖 文档

每个技能包含：
- **SKILL.md** - OpenClaw 特定文档（含元数据）
- **README.md** - 英文项目文档
- **README_CN.md** - 中文项目文档
- **scripts/** - 实现代码

## 🤝 贡献指南

1. Fork 本仓库
2. 创建你的功能分支 (`git checkout -b feature/amazing-skill`)
3. 提交你的更改 (`git commit -m '添加 amazing 技能'`)
4. 推送到分支 (`git push origin feature/amazing-skill`)
5. 打开 Pull Request

## 📄 许可证

本仓库中的所有技能均基于 MIT 许可证。

## 🙏 致谢

- [OpenClaw](https://openclaw.ai) - AI 智能体框架
- [腾讯云](https://cloud.tencent.com) - 混元API服务
- 所有贡献者和技能开发者

## 📞 支持

- GitHub Issues: [报告问题](https://github.com/wszhhx/zhhx-skills/issues)
- OpenClaw 文档: [文档](https://docs.openclaw.ai)
- 社区: [Discord](https://discord.com/invite/clawd)

---

**由 [@wszhhx](https://github.com/wszhhx) 维护**

[English Version](./README.md)
