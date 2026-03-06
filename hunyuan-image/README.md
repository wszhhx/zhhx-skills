# Hunyuan Image

Tencent Hunyuan AI Image Generation - Text-to-image generation based on Hunyuan large model.

## Features

- 🎨 **Text-to-Image**: Generate images from text descriptions
- 🖼️ **Multiple Resolutions**: Support various aspect ratios
- 🎭 **Style Support**: Multiple painting styles (anime, oil painting, watercolor, etc.)
- 🔧 **Reference Image**: Generate with reference images
- ⚡ **Super Resolution**: x2/x4 upscaling support

## Quick Start

### 1. Install Dependencies

```bash
pip install tencentcloud-sdk-python
```

### 2. Configure Credentials

**Required Environment Variables**:
- `TENCENT_SECRET_ID` - Tencent Cloud SecretId
- `TENCENT_SECRET_KEY` - Tencent Cloud SecretKey

```powershell
# Windows PowerShell - Permanent
[Environment]::SetEnvironmentVariable("TENCENT_SECRET_ID", "your-secret-id", "User")
[Environment]::SetEnvironmentVariable("TENCENT_SECRET_KEY", "your-secret-key", "User")

# Or temporary (current session)
$env:TENCENT_SECRET_ID = "your-secret-id"
$env:TENCENT_SECRET_KEY = "your-secret-key"
```

**Get API Keys**: https://console.cloud.tencent.com/cam/capi

### 3. Verify Installation

```powershell
# Check if environment variables are set
if ($env:TENCENT_SECRET_ID -and $env:TENCENT_SECRET_KEY) {
    Write-Host "✅ Environment variables configured"
} else {
    Write-Host "❌ Please set TENCENT_SECRET_ID and TENCENT_SECRET_KEY"
}

# Test generation
python scripts/generate.py "a cute cat"
```

## Usage

### Basic Usage

```bash
# Generate image
python scripts/generate.py "a cute pig in the grass"

# Specify resolution
python scripts/generate.py "sunset" --resolution 1024:768

# Specify style
python scripts/generate.py "anime girl" --style 201

# Generate multiple images
python scripts/generate.py "landscape" --num 4
```

### Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `prompt` | Text description (required) | "a cute pig" |
| `--resolution` | Resolution | `1024:1024`, `768:1024` |
| `--style` | Style ID | `201` (anime) |
| `--num` | Number of images (1-4) | `2` |
| `--clarity` | Upscale | `x2`, `x4` |
| `--output` | Output directory | `./images` |

### Resolution Options

- `768:768` - 1:1 Square
- `768:1024` - 3:4 Portrait (mobile wallpaper)
- `1024:768` - 4:3 Landscape
- `1024:1024` - 1:1 Square (HD)
- `720:1280` - 9:16 Portrait (phone fullscreen)
- `1280:720` - 16:9 Landscape (desktop wallpaper)

### Style List (Common)

| ID | Style |
|----|-------|
| 101 | Ink Painting |
| 102 | Concept Art |
| 103 | Oil Painting |
| 104 | Watercolor |
| 201 | Anime |
| 202 | Japanese Animation |
| 301 | 3D Cartoon |
| 401 | Portrait |
| 501 | Cyberpunk |
| 601 | Vaporwave |

Full list: https://cloud.tencent.com/document/product/1729/105846

## Output

Generated images are saved to `{output}/{date}/{job_id}/`:
- `image_0.png` - Generated image
- `info.json` - Task information (including expanded prompt)

## Important Notes

1. **Async API**: The API is asynchronous, need to wait for task completion
2. **Concurrent Limit**: Default 1 concurrent task
3. **Region**: Only supports `ap-guangzhou`
4. **Prompt Expansion**: Enabled by default to improve generation quality
5. **Watermark**: API adds "AI Generated" watermark by default

## Troubleshooting

### Status Code Trap

API returns `JobStatusCode: 5` may actually be successful! Check `ResultDetails`:

```python
if status == '4' or (status == '5' and result.get('ResultDetails') == ['Success']):
    print('✅ Actually successful!')
```

### Common Errors

| Error | Solution |
|-------|----------|
| `UnauthorizedOperation` | Check SecretId/SecretKey |
| `FailedOperation.DownloadError` | Check image URL accessibility |
| `InvalidParameterValue.InvalidImageFormat` | Only jpg/png supported |

## Examples

```bash
# Generate anime avatar
python scripts/generate.py "cute girl, short hair, smile, cherry blossom" --style 201 --resolution 768:768

# Generate cyberpunk wallpaper
python scripts/generate.py "future city, neon lights, rainy night" --style 501 --resolution 1920:1080 --clarity x2

# Generate ink painting
python scripts/generate.py "mountain, waterfall, pine tree, mist" --style 101 --resolution 1024:768
```

## Links

- [API Documentation](https://cloud.tencent.com/document/product/1729/105969)
- [Tencent Cloud Console](https://console.cloud.tencent.com/cam/capi)
- [Style List](https://cloud.tencent.com/document/product/1729/105846)

## License

MIT License

---

[中文版本](./README_CN.md)
