# Fooocus 图像生成技能

🎨 基于 Fooocus (Stable Diffusion XL) 的本地 AI 图像生成

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 概述

本技能集成了 [Fooocus](https://github.com/lllyasviel/Fooocus)，一个强大的离线开源图像生成工具，基于 Stable Diffusion XL。它提供了用户友好的 Gradio API 接口，在隐藏复杂性的同时暴露所有强大功能。

### 主要功能

- 🖼️ **文生图**: 从文本提示生成图像
- 🔄 **图生图**: 创建变体、放大或转换现有图像
- ✏️ **局部重绘/扩展**: 编辑特定区域或扩展图像
- 🎭 **风格控制**: 应用预设（动漫、写实等）和自定义风格
- 📦 **批量生成**: 一次生成多张图像
- 👤 **人脸替换**: 替换图像中的人脸
- 🎨 **IP-Adapter**: 使用参考图像进行风格迁移
- 🔍 **Describe**: 从图像反推 Prompt
- ⬆️ **Upscale**: 超分辨率图像放大
- 📊 **实时进度**: 基于 WebSocket 的实时进度更新

### 新增内容

- 🗺️ **决策流程图**: 根据用户请求类型选择正确配置的逐步指南
- 📚 **完整界面百科**: 全面的 Fooocus UI 元素、选项和参数文档
- 🎨 **风格分组指南**: 基于纯2D动漫风格经验，推理出6+种其他风格的配置
- ⚡ **性能默认设置**: 默认使用 Quality 模式（除非用户明确要求速度）
- 📐 **分辨率指南**: 不同使用场景的宽高比推荐
- 🔧 **Inpaint 最佳实践**: 包括模型下载要求和浏览器自动化限制说明
- 🚨 **错误速查表**: 常见错误和解决方案，包含生成前检查清单
- ✅ **强化检查清单**: 每个功能都有详细的生成前检查清单

## 系统要求

- **操作系统**: Windows 10/11、Linux 或 macOS
- **显卡**: NVIDIA GPU，4GB+ 显存（推荐）
- **内存**: 8GB+（CPU 模式需要 16GB+）
- **存储**: 10GB+ 可用空间用于模型
- **Python**: 3.10 或更高版本

⚠️ **注意**: 支持 CPU 模式，但速度极慢（每张图 10-30 分钟）。如果没有 NVIDIA GPU，我们强烈建议使用 Google Colab 或 Hugging Face 免费 GPU。

## ⚠️ 关键使用提示

### 风格配置（重要！）
**不同风格组别之间不要混用！**

| 风格组别 | 包含样式 | 效果 |
|---------|---------|------|
| **纯2D动漫组** | SAI Anime, MRE Anime | 纯正2D动漫风格 |
| **写实增强组** | Fooocus V2, Semi Realistic, Masterpiece | 3D/写实效果 |
| **照片写实组** | Fooocus Photograph, Photo 系列 | 照片级写实 |

**示例**: 使用 `run_anime.bat` 启动但勾选了 `Fooocus V2` 会产生3D/2D混合效果。要获得纯正2D动漫，请**只**使用 `SAI Anime + MRE Anime`。

### 性能默认设置
- **默认**: 使用 `Quality` 模式获得最佳效果
- **速度**: 仅在用户明确要求时才使用 `Speed` 或更快的模式

### Inpaint 使用要求
- **首次使用**: 自动下载约500MB模型（需要稳定的网络）
- **Prompt 位置**: 填写在 **Inpaint Additional Prompt** 中，**不是**主 Prompt
- **手动步骤**: 图片上传和涂抹需要用户手动操作（浏览器自动化无法完成）

## 快速开始

### 1. 检查环境

```bash
python scripts/check_env.py
```

### 2. 安装 Fooocus（如需要）

```bash
python scripts/install_fooocus.py --path ~/Fooocus
```

### 3. 启动 Fooocus 服务

```bash
cd ~/Fooocus
python entry_with_update.py
```

### 4. 生成第一张图像

```bash
# 基础生成
python scripts/generate.py --prompt "美丽的山日落" --output sunset.png

# 带实时进度
python scripts/generate_with_progress.py --prompt "赛博朋克城市" --output city.png

# 动漫风格（先使用 run_anime.bat 启动！）
python scripts/generate.py --prompt "动漫角色" --preset anime --output anime.png
```

## 使用示例

### 文生图

```bash
python scripts/generate.py \
  --prompt "巨龙飞越山脉，幻想艺术" \
  --preset realistic \
  --aspect-ratio 16:9 \
  --output dragon.png
```

### 图像变体

```bash
python scripts/generate.py \
  --input-image original.png \
  --prompt "相同构图，不同光照" \
  --variation-strength 0.7 \
  --output variation.png
```

### 图像放大

```bash
python scripts/generate.py \
  --input-image small.png \
  --upscale 2 \
  --output upscaled.png
```

### 局部重绘

```bash
python scripts/generate.py \
  --input-image photo.png \
  --mask-image mask.png \
  --prompt "移除物体" \
  --mode inpaint \
  --output inpainted.png
```

## 可用预设

| 预设 | 描述 | 适用场景 |
|------|------|----------|
| `default` | 平衡设置 | 通用目的 |
| `anime` | 动漫/卡通风格 | 动漫、漫画、卡通 |
| `realistic` | 写实风格 | 照片、肖像 |
| `lcm` | 潜在一致性模型 | 快速生成 |
| `lightning` | SDXL Lightning | 极速生成 |
| `playground_v2.5` | Playground v2.5 | 艺术图像 |
| `pony_v6` | Pony Diffusion V6 | 多样风格 |
| `sai` | Stable AI 风格 | 专业外观 |

## 没有 GPU？使用云端替代方案！

如果你没有 NVIDIA GPU，我们强烈推荐：

### 1. Google Colab（免费 GPU）
- **速度**: 每张图 10-30 秒
- **成本**: 免费
- **设置**: 无需设置
- **链接**: [在 Colab 中打开](https://colab.research.google.com/github/lllyasviel/Fooocus/blob/main/fooocus_colab.ipynb)

### 2. Hugging Face Spaces
- **速度**: 每张图 10-20 秒
- **成本**: 免费额度可用
- **设置**: 无需设置
- **链接**: [在 Hugging Face 上试用](https://huggingface.co/spaces/stabilityai/stable-diffusion-xl-base-1.0)

### 3. Replicate API
- **速度**: 每张图 10-20 秒
- **成本**: 按使用付费
- **链接**: [Replicate SDXL](https://replicate.com/stability-ai/sdxl)

## 文档

- [SKILL.md](SKILL.md) - 完整技能文档，包含：
  - 📚 **界面百科**: 完整的 UI 元素参考
  - 🎨 **风格配置指南**: 6+ 种风格组别及兼容性规则
  - ⚡ **性能与分辨率指南**: 设置的最佳实践
  - 🔧 **高级功能**: Inpaint、Outpaint、Upscale、Describe 详细指南
  - 🧪 **实战经验**: 经过测试的配置和踩坑记录
- [AGENT_QUICKREF.md](AGENT_QUICKREF.md) - Agent 快速参考
- [TEST_REPORT.md](TEST_REPORT.md) - 测试结果和发现
- [CPU_MODE_TEST_REPORT.md](CPU_MODE_TEST_REPORT.md) - CPU 模式分析
- [references/fooocus_api.md](references/fooocus_api.md) - API 文档
- [references/parameters_guide.md](references/parameters_guide.md) - 参数参考
- [references/presets.md](references/presets.md) - 预设配置

## 文件结构

```
fooocus-image-gen/
├── SKILL.md                          # 主要文档
├── README.md                         # 英文 README
├── README_CN.md                      # 中文 README
├── AGENT_QUICKREF.md                 # Agent 快速参考
├── TEST_REPORT.md                    # 测试报告
├── CPU_MODE_TEST_REPORT.md           # CPU 模式分析
├── scripts/
│   ├── check_env.py                  # 环境检查器
│   ├── generate.py                   # 带回退的图像生成
│   ├── generate_image.py             # 基础生成
│   ├── generate_with_progress.py     # WebSocket 进度
│   ├── install_fooocus.py            # 安装脚本
│   ├── list_models.py                # 列出预设/模型
│   └── test_cpu_mode.py              # CPU 模式测试器
├── references/
│   ├── fooocus_api.md                # API 文档
│   ├── parameters_guide.md           # 参数指南
│   └── presets.md                    # 预设文档
└── assets/
    └── prompt_templates.json         # 提示词模板
```

## 故障排除

### Fooocus 未运行

```bash
# 启动 Fooocus
cd ~/Fooocus
python entry_with_update.py

# 或使用检查脚本
python scripts/check_env.py --start
```

### 内存不足

```bash
# 减小图像尺寸
python scripts/generate.py --prompt "test" --width 512 --height 512

# 使用低显存模式
cd ~/Fooocus
python entry_with_update.py --always-low-vram
```

### 生成速度慢

```bash
# 使用 lightning 预设获得最快速度
python scripts/generate.py --prompt "test" --preset lightning --steps 4
```

## 性能预期

| 硬件 | 预设 | 步数 | 每张图时间 |
|------|------|------|------------|
| RTX 4090 | default | 30 | ~5-10 秒 |
| RTX 3060 | default | 30 | ~15-30 秒 |
| GTX 1060 | default | 30 | ~60-120 秒 |
| 仅 CPU | lightning | 4 | ~5-10 分钟 |
| 仅 CPU | default | 30 | ~30-60 分钟 |

## 许可证

本技能基于 MIT 许可证发布。Fooocus 本身基于 GPL-3.0。

## 贡献

欢迎贡献！请确保：
1. 代码遵循 Python 最佳实践
2. 文档已更新
3. 遵循安全指南（不禁用 SSL 验证，无硬编码凭证）

## 致谢

本技能离不开这些优秀的开源项目：

### 核心技术
- **[Fooocus](https://github.com/lllyasviel/Fooocus)** by [lllyasviel](https://github.com/lllyasviel) - 本技能的基础。一个让每个人都能使用 SDXL 的出色离线图像生成工具。
- **[Stable Diffusion XL](https://stability.ai/stable-diffusion)** by [Stability AI](https://stability.ai/) - 为 Fooocus 提供支持的强大扩散模型。
- **[Gradio](https://gradio.app/)** by Hugging Face - Fooocus 使用的 Web 界面框架。
- **[PyTorch](https://pytorch.org/)** by Meta AI - 深度学习框架。

### 模型资源
- **[Civitai](https://civitai.com/)** - 社区驱动的 AI 模型分享平台
- **[Hugging Face](https://huggingface.co/)** - 模型托管和推理平台

### 相关项目
- **[Stable Diffusion WebUI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)** by AUTOMATIC1111 - SD 的替代 Web 界面
- **[ComfyUI](https://github.com/comfyanonymous/ComfyUI)** by comfyanonymous - 基于节点的 SD 界面
- **[WebUI Forge](https://github.com/lllyasviel/stable-diffusion-webui-forge)** by lllyasviel - 优化的 SD WebUI

## 友情链接

### 官方资源
- 🏠 [Fooocus GitHub 仓库](https://github.com/lllyasviel/Fooocus)
- 📖 [Fooocus Wiki](https://github.com/lllyasviel/Fooocus/wiki)
- 🐛 [Fooocus Issues](https://github.com/lllyasviel/Fooocus/issues)
- 💬 [Fooocus Discussions](https://github.com/lllyasviel/Fooocus/discussions)

### 云端替代方案（无需安装）
- ☁️ [Fooocus on Google Colab](https://colab.research.google.com/github/lllyasviel/Fooocus/blob/main/fooocus_colab.ipynb) - 免费 GPU
- 🤗 [SDXL on Hugging Face](https://huggingface.co/spaces/stabilityai/stable-diffusion-xl-base-1.0) - 免费额度
- 🔄 [SDXL on Replicate](https://replicate.com/stability-ai/sdxl) - 按量付费

### 学习资源
- 🎓 [SDXL Prompt Guide](https://stable-diffusion-art.com/sdxl-prompt/) - 学习提示词工程
- 📚 [OpenArt Prompt Book](https://openart.ai/promptbook) - 全面的提示词指南
- 🎨 [PromptHero](https://prompthero.com/) - 提示词示例和灵感

### 社区
- 💬 [r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/) - Reddit 社区
- 🎮 [Stable Diffusion Discord](https://discord.gg/stablediffusion) - 官方 Discord

## 支持

如果你觉得本技能有帮助，请考虑：
- ⭐ 给 [Fooocus 仓库](https://github.com/lllyasviel/Fooocus) 点星
- 🐛 通过 GitHub Issues 报告 bug 或建议功能
- 💬 与社区分享你的使用体验

## 免责声明

本技能是 Fooocus 的独立封装，与 lllyasviel 或 Stability AI 没有官方关联。所有商标属于其各自所有者。
