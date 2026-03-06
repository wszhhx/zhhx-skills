# Hunyuan 3D

Tencent Hunyuan AI 3D Generation (OpenAI-compatible API) - Text-to-3D and image-to-3D generation.

## ⚠️ Important

**This skill uses OpenAI-compatible API**, different from traditional Tencent Cloud API:
- Uses **API Key** authentication (not SecretId/SecretKey)
- OpenAI-style interface
- **Professional version only** (no rapid version)

## Features

- 🎨 **Text-to-3D**: Generate 3D models from text descriptions
- 🖼️ **Image-to-3D**: Generate 3D models from images
- 🎯 **Multi-version**: Support model versions 3.0 and 3.1

## Quick Start

### 1. Enable Hunyuan 3D Service

**Required**: Enable service in Tencent Cloud console first:

1. Visit [Tencent Hunyuan 3D Console](https://console.cloud.tencent.com/ai3d)
2. Click "Enable Now" or "Apply"
3. Read and agree to service agreement
4. Wait for service activation (usually instant)

**Common Issues**:
- If "Insufficient Resources" shows, service is initializing, wait 5-10 minutes
- If cannot enable, may need real-name verification or contact support

### 2. Get API Key

1. Visit [Hunyuan 3D API Key Management](https://console.cloud.tencent.com/ai3d/api-key)
2. Click "Create API Key"
3. Enter name (e.g., hunyuan-3d-key)
4. Copy the generated API Key (format: `sk-xxxxx`)

**⚠️ Important**: API Key is shown only once, please save it properly!

**Alternative**: If above link doesn't work, use [Hunyuan API Key page](https://console.cloud.tencent.com/hunyuan/start)

### 3. Configure Environment Variable

**Windows PowerShell**:
```powershell
# Temporary (current session)
$env:HUNYUAN_3D_API_KEY = "sk-xxxxx"

# Permanent (recommended)
[Environment]::SetEnvironmentVariable("HUNYUAN_3D_API_KEY", "sk-xxxxx", "User")
```

**Linux/Mac**:
```bash
# Temporary
export HUNYUAN_3D_API_KEY="sk-xxxxx"

# Permanent (add to ~/.bashrc or ~/.zshrc)
echo 'export HUNYUAN_3D_API_KEY="sk-xxxxx"' >> ~/.bashrc
source ~/.bashrc
```

### 4. Verify Installation

```powershell
# Check environment variable
Write-Host "API Key: $($env:HUNYUAN_3D_API_KEY.Substring(0,15))..."

# Test generation
python scripts/generate.py --mode text --prompt "a cute dog"
```

**If "Insufficient Resources" error**: Service is initializing, wait 5-10 minutes and retry

## Usage

### Basic Usage

```bash
# Text-to-3D
python scripts/generate.py --mode text --prompt "a cute pig"

# Image-to-3D
python scripts/generate.py --mode image --image-url "https://example.com/pig.jpg"

# Use version 3.1
python scripts/generate.py --mode text --prompt "dog" --model 3.1
```

### Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| `--mode` | Generation mode | `text` (text-to-3D), `image` (image-to-3D) |
| `--prompt` | Text description (text-to-3D) | "a cute pig" |
| `--image-url` | Image URL (image-to-3D) | "https://example.com/pig.jpg" |
| `--model` | Model version | `3.0` (default), `3.1` |
| `--output` | Output directory | `./models` |

### Model Versions

| Version | Features |
|---------|----------|
| 3.0 | Default, full features |
| 3.1 | New version, but LowPoly and Sketch parameters not available |

### Input Requirements

**Text-to-3D**:
- Text description: max 1024 UTF-8 characters
- Chinese prompts supported

**Image-to-3D**:
- Format: jpg, png, jpeg, webp
- Size: ≤8MB
- Resolution: 128px ~ 5000px (single side)

## Output

Generated 3D models are saved to `{output}/{date}/{job_id}/`:
- `model.glb` - 3D model file (GLB format)
- `model.obj` - 3D model file (OBJ format, in ZIP)
- `preview.png` - Preview image
- `info.json` - Task information

**Output Formats**:
- Both GLB and OBJ formats returned
- Includes texture maps
- With preview image

## API Information

- **Base URL**: `https://api.ai3d.cloud.tencent.com`
- **Submit Task**: `POST /v1/ai3d/submit`
- **Query Task**: `POST /v1/ai3d/query`
- **Authentication**: API Key (Header: `Authorization: sk-xxxxx`)

## Troubleshooting

### Service Not Enabled

**Error**: `ResourceUnavailable.NotExist`

**Solution**:
1. Visit https://console.cloud.tencent.com/ai3d
2. Enable Hunyuan 3D service
3. Wait a few minutes for activation
4. Retry

### Insufficient Resources

**Error**: `ResourceInsufficient`

**Solution**:
- Service just enabled, wait 5-10 minutes and retry
- Or contact Tencent Cloud support

### API Key Error

**Error**: `Unauthorized` or authentication failed

**Solution**:
- Ensure using correct API Key (not SecretId/SecretKey)
- API Key format should be `sk-xxxxx`
- Create at https://console.cloud.tencent.com/ai3d/api-key

### Response Format

OpenAI-compatible API returns:
```json
{
  "Response": {
    "JobId": "xxx",
    "Status": "DONE",
    "ResultFile3Ds": [...]
  }
}
```

**Note**: Status field is `Status` not `StatusCode`, success value is `DONE` not `SUCCESS`

## Important Notes

1. **Async API**: Divided into submit task and query task steps
2. **Task Validity**: 24 hours
3. **Concurrent Limit**: Default 3 concurrent
4. **Professional Only**: OpenAI-compatible API doesn't support rapid version
5. **Generation Time**: 3D generation takes longer (1-5 minutes), please be patient

## Examples

```bash
# Generate pig 3D model
python scripts/generate.py --mode text --prompt "a cute pig, pink, cartoon style"

# Image-to-3D
python scripts/generate.py --mode image --image-url "https://example.com/pig-photo.jpg"

# Use version 3.1
python scripts/generate.py --mode text --prompt "dog" --model 3.1
```

## Links

- [OpenAI-compatible API Docs](https://cloud.tencent.com/document/product/1804/126189)
- [API Key Management](https://console.cloud.tencent.com/ai3d/api-key)
- [Hunyuan 3D Console](https://console.cloud.tencent.com/ai3d)
- [Submit Task API Docs](https://cloud.tencent.com/document/product/1804/123447)

## License

MIT License

---

[中文版本](./README_CN.md)
