# Hunyuan Video

Tencent Hunyuan AI Video Generation - Text-to-video, image-to-video, and video stylization.

## Features

- 🎬 **Text-to-Video**: Generate videos from text descriptions
- 🖼️ **Image-to-Video**: Generate videos from images (supports URL and local files)
- 🎨 **Video Stylization**: Convert videos to 2D anime, 3D cartoon, and other styles

## Quick Start

### 1. Install Dependencies

```bash
pip install tencentcloud-sdk-python
```

### 2. Enable Service

1. Visit [Tencent Hunyuan Video Console](https://hunyuan.cloud.tencent.com/#/app/videoModel)
2. Read and agree to the service agreement
3. Click to enable the service

### 3. Configure Credentials

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

### 4. Verify Installation

```powershell
# Check environment variables
Write-Host "SecretId: $env:TENCENT_SECRET_ID"
Write-Host "SecretKey: $($env:TENCENT_SECRET_KEY.Substring(0,10))..."

# Test generation
python scripts/generate.py text2video "a cute pig running"
```

## Usage

### 1. Text-to-Video

```bash
python scripts/generate.py text2video "a cute pig running on grass"

# Specify resolution
python scripts/generate.py text2video "sunset" --resolution 1080p
```

**Parameters**:
- `prompt`: Text description (required)
- `--resolution`: Resolution (720p, 1080p, default: 720p)

### 2. Image-to-Video

```bash
# Use image URL
python scripts/generate.py image2video "https://example.com/pig.jpg"

# Use local image
python scripts/generate.py image2video "./my_pig.png"

# Add auxiliary description
python scripts/generate.py image2video "./pig.png" --prompt "pig running"
```

**Parameters**:
- `image`: Image URL or local path (required)
- `--prompt`: Auxiliary description (optional)

**Supported Formats**:
- URL: starts with `http://` or `https://`
- Local file: relative or absolute path

### 3. Video Stylization

```bash
# Convert to 2D anime style
python scripts/generate.py stylization "https://example.com/video.mp4" --style 2d_anime

# Convert to 3D cartoon style
python scripts/generate.py stylization "https://example.com/video.mp4" --style 3d_cartoon
```

**Style Options**:
- `2d_anime`: 2D Anime
- `3d_cartoon`: 3D Cartoon
- `3d_china`: 3D Chinese Style
- `pixel_art`: Pixel Art

**Input Video Requirements**:
- Format: mp4, mov
- Duration: 1-60 seconds
- Resolution: 540P-2056P
- Size: ≤200MB
- FPS: 15-60fps

## Output

Generated videos are saved to `{output}/{date}/{job_id}/`:
- `{command}_result.mp4` - Generated video
- `info.json` - Task information

## Important Notes

1. **Async API**: All functions are asynchronous, need to wait for task completion
2. **Status Code Trap**: Different interfaces have different status fields:
   - Text-to-Video / Image-to-Video: `Status: DONE`
   - Video Stylization: `JobStatusCode: 4` or `5+Success`
3. **Image Parameter Trap**: `Image` is object type, not string:
   ```python
   # ❌ Wrong
   req.Image = image_url
   
   # ✅ Correct
   image = models.Image()
   image.Url = image_url  # or image.Base64 = base64_data
   req.Image = image
   ```
4. **Concurrent Limit**: 1 concurrent for stylization, 3 for others
5. **Generation Time**: Usually 1-5 minutes, please be patient

## Troubleshooting

### Service Not Enabled

**Error**: `FailedOperation.ServiceNotOpen`

**Solution**: Enable Hunyuan Video service in console first

### Video Download Failed

**Error**: `FailedOperation.DownloadError`

**Solution**:
- Check video URL accessibility
- Ensure format is mp4 or mov
- Ensure size ≤200MB

### Status Code Confusion

**Problem**: `JobStatusCode: 5` may actually be successful

**Solution**: Check `ResultDetails` field

## Examples

```bash
# Text-to-video
python scripts/generate.py text2video "a cute pig running on grass, sunny day"

# Image-to-video (local file)
python scripts/generate.py image2video "./my_pig.png" --prompt "pig running"

# Video stylization
python scripts/generate.py stylization "https://example.com/video.mp4" --style 2d_anime
```

## Links

- [API Overview](https://cloud.tencent.com/document/product/1616/107795)
- [Hunyuan Video Console](https://hunyuan.cloud.tencent.com/#/app/videoModel)
- [Tencent Cloud Key Management](https://console.cloud.tencent.com/cam/capi)

## License

MIT License

---

[中文版本](./README_CN.md)
