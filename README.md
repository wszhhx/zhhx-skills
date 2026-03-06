# OpenClaw Skills Repository

[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-blue.svg)](https://openclaw.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A curated collection of OpenClaw skills for AI-powered automation and productivity, focusing on Tencent Hunyuan AI services.

## 📦 Available Skills

| Skill | Description | Auth Type | Version |
|-------|-------------|-----------|---------|
| [hunyuan-image](./hunyuan-image) | Tencent Hunyuan AI Image Generation | Tencent Cloud SecretId/SecretKey | 1.0.0 |
| [hunyuan-video](./hunyuan-video) | Tencent Hunyuan AI Video Generation | Tencent Cloud SecretId/SecretKey | 1.0.0 |
| [hunyuan-3d](./hunyuan-3d) | Tencent Hunyuan AI 3D Generation | Hunyuan 3D API Key (sk-xxxxx) | 1.0.0 |

## 🚀 Quick Start

### Method 1: Install from ClawHub (Recommended)

```bash
# List available skills
openclaw skills search

# Install a specific skill
openclaw skills install hunyuan-image
```

### Method 2: Tell Your Agent to Install

Simply tell your OpenClaw agent:

> "Install the hunyuan-image skill from https://github.com/wszhhx/zhhx-skills"

The agent will automatically:
1. Clone the repository
2. Install dependencies
3. Configure the skill
4. Verify installation

### Method 3: Manual Installation

```bash
# Clone the repository
git clone https://github.com/wszhhx/zhhx-skills.git

# Navigate to specific skill
cd zhhx-skills/hunyuan-image

# Follow skill-specific instructions in SKILL.md
cat SKILL.md
```

## 🔑 API Credentials Guide

### Tencent Cloud Skills (hunyuan-image, hunyuan-video)

**Required**: Tencent Cloud SecretId + SecretKey

**Get Credentials**:
1. Visit https://console.cloud.tencent.com/cam/capi
2. Click "Create Key"
3. Copy SecretId and SecretKey

**Configure**:
```powershell
$env:TENCENT_SECRET_ID = "your-secret-id"
$env:TENCENT_SECRET_KEY = "your-secret-key"
```

### Hunyuan 3D Skill (hunyuan-3d)

**Required**: Hunyuan 3D API Key (format: `sk-xxxxx`)

**⚠️ Important**: This is different from Tencent Cloud credentials!

**Get API Key**:
1. Visit https://console.cloud.tencent.com/ai3d/api-key
2. Click "Create API Key"
3. Copy the API Key (format: `sk-xxxxx`)

**Configure**:
```powershell
$env:HUNYUAN_3D_API_KEY = "sk-xxxxx"
```

## 📁 Repository Structure

```
zhhx-skills/
├── hunyuan-image/          # Tencent Hunyuan Image Generation
│   ├── scripts/
│   ├── SKILL.md
│   ├── README.md
│   └── README_CN.md
├── hunyuan-video/          # Tencent Hunyuan Video Generation
│   ├── scripts/
│   ├── SKILL.md
│   ├── README.md
│   └── README_CN.md
├── hunyuan-3d/             # Tencent Hunyuan 3D Generation
│   ├── scripts/
│   ├── SKILL.md
│   ├── README.md
│   └── README_CN.md
├── README.md               # This file (English)
└── README_CN.md            # Chinese version
```

## 🎯 Skill Highlights

### Hunyuan Image
- Text-to-image generation
- Multiple resolutions and styles
- Reference image support
- Super resolution (x2/x4)

### Hunyuan Video
- Text-to-video generation
- Image-to-video generation
- Video stylization (2D anime, 3D cartoon, etc.)

### Hunyuan 3D
- Text-to-3D generation
- Image-to-3D generation
- OpenAI-compatible API
- Outputs GLB and OBJ formats

## 🛠️ For Skill Developers

### Adding a New Skill

1. Create a new directory: `your-skill-name/`
2. Add required files:
   - `SKILL.md` - OpenClaw skill documentation
   - `README.md` - English documentation
   - `README_CN.md` - Chinese documentation
   - `scripts/` - Implementation scripts
3. Update this README to include your skill
4. Submit a pull request

### Skill Requirements

- Must include `SKILL.md` with proper metadata
- Should have clear installation instructions
- Must handle errors gracefully
- Should include usage examples
- Must document API credentials requirements

## 📖 Documentation

Each skill contains:
- **SKILL.md** - OpenClaw-specific documentation with metadata
- **README.md** - English project documentation
- **README_CN.md** - Chinese project documentation
- **scripts/** - Implementation code

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-skill`)
3. Commit your changes (`git commit -m 'Add amazing skill'`)
4. Push to the branch (`git push origin feature/amazing-skill`)
5. Open a Pull Request

## 📄 License

All skills in this repository are licensed under the MIT License.

## 🙏 Acknowledgments

- [OpenClaw](https://openclaw.ai) - The AI agent framework
- [Tencent Cloud](https://cloud.tencent.com) - Hunyuan API services
- All contributors and skill developers

## 📞 Support

- GitHub Issues: [Report a bug](https://github.com/wszhhx/zhhx-skills/issues)
- OpenClaw Docs: [Documentation](https://docs.openclaw.ai)
- Community: [Discord](https://discord.com/invite/clawd)

---

**Maintained by [@wszhhx](https://github.com/wszhhx)**

[中文版本](./README_CN.md)
