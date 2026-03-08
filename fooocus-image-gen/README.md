# Fooocus Image Generation Skill

🎨 Local AI image generation using Fooocus (Stable Diffusion XL)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Fooocus](https://img.shields.io/badge/Powered%20by-Fooocus-blue)](https://github.com/lllyasviel/Fooocus)
[![SDXL](https://img.shields.io/badge/Model-SDXL-orange)](https://stability.ai/stable-diffusion)

> **🙏 Acknowledgment**: This skill is built on top of [Fooocus](https://github.com/lllyasviel/Fooocus) by [lllyasviel](https://github.com/lllyasviel). All credit for the amazing image generation capabilities goes to the Fooocus team and the open-source community.

## 🔗 Quick Links

| Resource | Link | Description |
|----------|------|-------------|
| **🏠 Fooocus GitHub** | [github.com/lllyasviel/Fooocus](https://github.com/lllyasviel/Fooocus) | Official repository |
| **📖 Fooocus Wiki** | [Wiki](https://github.com/lllyasviel/Fooocus/wiki) | Official documentation |
| **💬 Discussions** | [Discussions](https://github.com/lllyasviel/Fooocus/discussions) | Community support |
| **☁️ Google Colab** | [Colab](https://colab.research.google.com/github/lllyasviel/Fooocus/blob/main/fooocus_colab.ipynb) | Free GPU (no install) |
| **🤗 Hugging Face** | [HF Spaces](https://huggingface.co/spaces/stabilityai/stable-diffusion-xl-base-1.0) | Free online demo |

## Overview

This skill integrates with [Fooocus](https://github.com/lllyasviel/Fooocus), a powerful offline, open-source image generation tool based on Stable Diffusion XL. It provides a user-friendly interface to Fooocus's Gradio API, hiding complexity while exposing all powerful features.

### Key Features

- 🖼️ **Text-to-Image**: Generate images from text prompts
- 🔄 **Image-to-Image**: Create variations, upscale, or transform existing images
- ✏️ **Inpainting/Outpainting**: Edit specific regions or extend images
- 🎭 **Style Control**: Apply presets (anime, realistic, etc.) and custom styles
- 📦 **Batch Generation**: Generate multiple images at once
- 👤 **Face Swap**: Replace faces in images
- 🎨 **IP-Adapter**: Use reference images for style transfer
- 🔍 **Describe**: Reverse engineer prompts from images
- ⬆️ **Upscale**: Super-resolution image enlargement
- 📊 **Real-time Progress**: WebSocket-based live progress updates

### What's New

- 🗺️ **Decision Flowchart**: Step-by-step guide for choosing correct configuration based on user request type
- 📚 **Complete Interface Encyclopedia**: Comprehensive documentation of all Fooocus UI elements, options, and parameters
- 🎨 **Style Grouping Guide**: Based on pure 2D anime style experience, inferring configurations for 6+ other styles
- ⚡ **Performance Defaults**: Quality mode as default (unless user explicitly requests speed)
- 📐 **Resolution Guide**: Aspect ratio recommendations for different use cases
- 🔧 **Inpaint Best Practices**: Including model download requirements and browser automation limitations
- 🚨 **Error Quick Reference**: Common mistakes and solutions with pre-generation checklists
- ✅ **Enhanced Checklists**: Every feature has detailed pre-generation checklists

## System Requirements

- **OS**: Windows 10/11, Linux, or macOS
- **GPU**: NVIDIA GPU with 4GB+ VRAM (recommended)
- **RAM**: 8GB+ (16GB+ for CPU mode)
- **Storage**: 10GB+ free space for models
- **Python**: 3.10 or higher

⚠️ **Note**: CPU mode is supported but extremely slow (10-30 minutes per image). We strongly recommend using Google Colab or Hugging Face for free GPU access if you don't have an NVIDIA GPU.

## ⚠️ Key Usage Tips

### Style Configuration (Critical!)
**Different style groups should NOT be mixed!**

| Style Group | Styles | Effect |
|-------------|--------|--------|
| **Pure 2D Anime** | SAI Anime, MRE Anime | Clean 2D anime style |
| **Realistic Enhancement** | Fooocus V2, Semi Realistic, Masterpiece | 3D/realistic effects |
| **Photographic** | Fooocus Photograph, Photo series | Photo-realistic |

**Example**: Using `run_anime.bat` with `Fooocus V2` checked will produce mixed 3D/2D results. Use **only** `SAI Anime + MRE Anime` for pure 2D anime.

### Performance Default
- **Default**: Use `Quality` mode for best results
- **Speed**: Only use `Speed` or faster modes when explicitly requested

### Inpaint Requirements
- **First Use**: Downloads ~500MB model automatically (requires stable internet)
- **Prompt Location**: Fill in **Inpaint Additional Prompt**, NOT main prompt
- **Manual Steps**: Image upload and masking require user manual operation (browser automation cannot do this)

## Quick Start

### 1. Check Environment

```bash
python scripts/check_env.py
```

### 2. Install Fooocus (if needed)

```bash
python scripts/install_fooocus.py --path ~/Fooocus
```

### 3. Start Fooocus Service

```bash
cd ~/Fooocus
python entry_with_update.py
```

### 4. Generate Your First Image

```bash
# Basic generation
python scripts/generate.py --prompt "a beautiful sunset over mountains" --output sunset.png

# With real-time progress
python scripts/generate_with_progress.py --prompt "cyberpunk city" --output city.png

# Anime style (use run_anime.bat first!)
python scripts/generate.py --prompt "anime character" --preset anime --output anime.png
```

## Usage Examples

### Text-to-Image

```bash
python scripts/generate.py \
  --prompt "a majestic dragon flying over mountains, fantasy art" \
  --preset realistic \
  --aspect-ratio 16:9 \
  --output dragon.png
```

### Image Variations

```bash
python scripts/generate.py \
  --input-image original.png \
  --prompt "same composition, different lighting" \
  --variation-strength 0.7 \
  --output variation.png
```

### Upscaling

```bash
python scripts/generate.py \
  --input-image small.png \
  --upscale 2 \
  --output upscaled.png
```

### Inpainting

```bash
python scripts/generate.py \
  --input-image photo.png \
  --mask-image mask.png \
  --prompt "remove the object" \
  --mode inpaint \
  --output inpainted.png
```

## Available Presets

| Preset | Description | Best For |
|--------|-------------|----------|
| `default` | Balanced settings | General purpose |
| `anime` | Anime/cartoon style | Anime, manga, cartoons |
| `realistic` | Photorealistic | Photos, portraits |
| `lcm` | Latent Consistency Model | Fast generation |
| `lightning` | SDXL Lightning | Very fast generation |
| `playground_v2.5` | Playground v2.5 | Artistic images |
| `pony_v6` | Pony Diffusion V6 | Versatile styles |
| `sai` | Stable AI style | Professional look |

## No GPU? Use Cloud Alternatives!

If you don't have an NVIDIA GPU, we strongly recommend:

### 1. Google Colab (Free GPU)
- **Speed**: 10-30 seconds per image
- **Cost**: Free
- **Setup**: None required
- **Link**: [Open in Colab](https://colab.research.google.com/github/lllyasviel/Fooocus/blob/main/fooocus_colab.ipynb)

### 2. Hugging Face Spaces
- **Speed**: 10-20 seconds per image
- **Cost**: Free tier available
- **Setup**: None required
- **Link**: [Try on Hugging Face](https://huggingface.co/spaces/stabilityai/stable-diffusion-xl-base-1.0)

### 3. Replicate API
- **Speed**: 10-20 seconds per image
- **Cost**: Pay per use
- **Link**: [Replicate SDXL](https://replicate.com/stability-ai/sdxl)

## Quick Start

### Common Use Cases

| Use Case | Method | Key Parameters |
|----------|--------|----------------|
| **Text to Image** | Direct generation | Preset + Styles + Prompt |
| **Character Design** | Multi-step workflow | Seed + Vary + Consistent Prompt |
| **Style Transfer** | Image Prompt or Text | Image weight 0.8-1.2 + Style keywords |
| **Image Restoration** | Inpaint/Modify Content | Mask + Method selection |
| **Remote Assistance** | Pure text generation | Detailed Prompt + Negative Prompt |

### Quick Prompt Templates

```bash
# Scientist/Researcher
"[Name], human scientist, [age] years old, [hair color] hair, wearing white lab coat, professional portrait, laboratory background, realistic, detailed face, masterpiece, best quality"

# Anime Character
"[Name], 1[gender], [hair color] hair, [eye color] eyes, [outfit], anime style, detailed face, looking at viewer, kawaii, moe, cel shaded, masterpiece, best quality"

# Fantasy Scene
"[Subject], fantasy art style, magical atmosphere, detailed background, vibrant colors, masterpiece, best quality, SAI Fantasy Art"
```

## Documentation

- [SKILL.md](SKILL.md) - Complete skill documentation with:
  - 📚 **Interface Encyclopedia**: Complete UI element reference
  - 🎨 **Style Configuration Guide**: 6+ style groups with compatibility rules
  - ⚡ **Performance & Resolution Guides**: Best practices for settings
  - 🔧 **Advanced Features**: Inpaint, Outpaint, Upscale, Describe detailed guides
  - 🎯 **Real-world Scenarios**: Practical workflows for common use cases
  - 📝 **Prompt Templates**: Ready-to-use templates for various subjects
  - 🧪 **Real-world Experience**: Tested configurations and pitfalls
- [AGENT_QUICKREF.md](AGENT_QUICKREF.md) - Quick reference for agents
- [TEST_REPORT.md](TEST_REPORT.md) - Testing results and findings
- [CPU_MODE_TEST_REPORT.md](CPU_MODE_TEST_REPORT.md) - CPU mode analysis
- [references/fooocus_api.md](references/fooocus_api.md) - API documentation
- [references/parameters_guide.md](references/parameters_guide.md) - Parameter reference
- [references/presets.md](references/presets.md) - Preset configurations

## File Structure

```
fooocus-image-gen/
├── SKILL.md                          # Main documentation
├── README.md                         # This file
├── README_CN.md                      # Chinese README
├── AGENT_QUICKREF.md                 # Agent quick reference
├── TEST_REPORT.md                    # Test report
├── CPU_MODE_TEST_REPORT.md           # CPU mode analysis
├── scripts/
│   ├── check_env.py                  # Environment checker
│   ├── generate.py                   # Image generation with fallback
│   ├── generate_image.py             # Basic generation
│   ├── generate_with_progress.py     # WebSocket progress
│   ├── install_fooocus.py            # Installation script
│   ├── list_models.py                # List presets/models
│   └── test_cpu_mode.py              # CPU mode tester
├── references/
│   ├── fooocus_api.md                # API documentation
│   ├── parameters_guide.md           # Parameter guide
│   └── presets.md                    # Preset documentation
└── assets/
    └── prompt_templates.json         # Prompt templates
```

## Troubleshooting

### Fooocus Not Running

```bash
# Start Fooocus
cd ~/Fooocus
python entry_with_update.py

# Or use the check script
python scripts/check_env.py --start
```

### Out of Memory

```bash
# Reduce image size
python scripts/generate.py --prompt "test" --width 512 --height 512

# Use low VRAM mode
cd ~/Fooocus
python entry_with_update.py --always-low-vram
```

### Slow Generation

```bash
# Use lightning preset for fastest generation
python scripts/generate.py --prompt "test" --preset lightning --steps 4
```

## Performance Expectations

| Hardware | Preset | Steps | Time per Image |
|----------|--------|-------|----------------|
| RTX 4090 | default | 30 | ~5-10 seconds |
| RTX 3060 | default | 30 | ~15-30 seconds |
| GTX 1060 | default | 30 | ~60-120 seconds |
| CPU only | lightning | 4 | ~5-10 minutes |
| CPU only | default | 30 | ~30-60 minutes |

## 🙏 Acknowledgments

This skill is built upon the incredible work of the open-source community. We are deeply grateful to:

### 🎯 Core Foundation
| Project | Author | Description |
|---------|--------|-------------|
| **[Fooocus](https://github.com/lllyasviel/Fooocus)** | [lllyasviel](https://github.com/lllyasviel) | 🌟 The foundation of this skill. An offline image generation tool that makes SDXL accessible to everyone. |
| **[Stable Diffusion XL](https://stability.ai/stable-diffusion)** | [Stability AI](https://stability.ai/) | The powerful diffusion model that powers Fooocus and revolutionized open-source AI art. |
| **[Gradio](https://gradio.app/)** | [Hugging Face](https://huggingface.co/) | The web interface framework that makes Fooocus's UI possible. |
| **[PyTorch](https://pytorch.org/)** | [Meta AI](https://ai.meta.com/) | The deep learning framework powering modern AI. |

### 🎨 Model & Resource Communities
| Platform | Description |
|----------|-------------|
| **[Civitai](https://civitai.com/)** | The largest community-driven AI model sharing platform. Thousands of SDXL models and LoRAs. |
| **[Hugging Face](https://huggingface.co/)** | Model hosting, inference platform, and open-source AI community hub. |
| **[OpenArt](https://openart.ai/)** | AI art community with prompt sharing and model discovery. |

### 🔧 Related Projects
| Project | Author | Description |
|---------|--------|-------------|
| **[Stable Diffusion WebUI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)** | AUTOMATIC1111 | The original web interface for Stable Diffusion. |
| **[ComfyUI](https://github.com/comfyanonymous/ComfyUI)** | comfyanonymous | Powerful node-based SD interface for advanced users. |
| **[WebUI Forge](https://github.com/lllyasviel/stable-diffusion-webui-forge)** | lllyasviel | Optimized SD WebUI with improved performance. |

---

## 🔗 Friendly Links

### 🏠 Official Fooocus Resources
| Resource | Link | Description |
|----------|------|-------------|
| **GitHub Repository** | [github.com/lllyasviel/Fooocus](https://github.com/lllyasviel/Fooocus) | ⭐ Star the project! Source code, releases, and main documentation. |
| **Official Wiki** | [Wiki](https://github.com/lllyasviel/Fooocus/wiki) | Comprehensive documentation and guides. |
| **GitHub Issues** | [Issues](https://github.com/lllyasviel/Fooocus/issues) | Bug reports and feature requests. |
| **Discussions** | [Discussions](https://github.com/lllyasviel/Fooocus/discussions) | 💬 Community support, tips, and showcases. |

### ☁️ Cloud Alternatives (No Installation Required)
| Platform | Link | Cost | Speed | Best For |
|----------|------|------|-------|----------|
| **Google Colab** | [Open in Colab](https://colab.research.google.com/github/lllyasviel/Fooocus/blob/main/fooocus_colab.ipynb) | Free | 10-30s | Quick testing, no GPU |
| **Hugging Face** | [HF Spaces](https://huggingface.co/spaces/stabilityai/stable-diffusion-xl-base-1.0) | Free tier | 10-20s | Simple generation |
| **Replicate** | [Replicate SDXL](https://replicate.com/stability-ai/sdxl) | Pay per use | 10-20s | API integration |
| **RunPod** | [runpod.io](https://www.runpod.io/) | Pay per hour | Fast | Heavy usage |
| **Vast.ai** | [vast.ai](https://vast.ai/) | Pay per hour | Fast | GPU rental |

### 📚 Learning Resources
| Resource | Link | Description |
|----------|------|-------------|
| **SDXL Prompt Guide** | [stable-diffusion-art.com](https://stable-diffusion-art.com/sdxl-prompt/) | 🎓 Comprehensive prompt engineering guide. |
| **OpenArt Prompt Book** | [openart.ai/promptbook](https://openart.ai/promptbook) | 📖 Extensive prompt techniques and examples. |
| **PromptHero** | [prompthero.com](https://prompthero.com/) | 🎨 Prompt examples and inspiration gallery. |
| **Civitai Articles** | [civitai.com/articles](https://civitai.com/articles) | 📰 Tutorials and guides from the community. |

### 💬 Community & Support
| Platform | Link | Description |
|----------|------|-------------|
| **Reddit r/StableDiffusion** | [reddit.com/r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/) | Active community for SD/SDXL discussion. |
| **Stable Diffusion Discord** | [Discord](https://discord.gg/stablediffusion) | 🎮 Real-time chat and support. |
| **Fooocus Discussion #117** | [Discussion](https://github.com/lllyasviel/Fooocus/discussions/117) | Advanced parameters guide. |
| **Fooocus Discussion #557** | [Discussion](https://github.com/lllyasviel/Fooocus/discussions/557) | Image Prompt best practices. |

---

## 💝 Support the Ecosystem

If you find this skill helpful, please consider supporting the projects that make it possible:

- ⭐ **Star [Fooocus](https://github.com/lllyasviel/Fooocus)** on GitHub
- 🐛 **Report bugs** or suggest features via [GitHub Issues](https://github.com/lllyasviel/Fooocus/issues)
- 💬 **Share your experience** in [Discussions](https://github.com/lllyasviel/Fooocus/discussions)
- 🎨 **Upload your models** to [Civitai](https://civitai.com/) or [Hugging Face](https://huggingface.co/)
- ☕ **Support the developers** via their GitHub sponsorship links

---

## 📜 Disclaimer

This skill is an independent wrapper for Fooocus and is **not officially affiliated** with lllyasviel or Stability AI. All trademarks belong to their respective owners.

The skill documentation incorporates learnings from the Fooocus community, including discussions, issues, and shared experiences. We are grateful to all community contributors.

---

## 📄 License

This skill is released under the MIT License. Fooocus itself is under GPL-3.0.

---

> **Last Updated**: 2026-03-08 | **Skill Version**: 2.0
> 
> Made with ❤️ for the open-source AI community
