# Hunyuan 3D - 腾讯混元生3D

基于腾讯混元大模型的3D模型生成服务，使用OpenAI兼容接口，支持文生3D、图生3D。

## ⚠️ 重要说明

**本技能使用OpenAI兼容接口**，与传统的腾讯云API不同：
- 使用 **API Key** 认证（不是SecretId/SecretKey）
- 接口风格与OpenAI一致
- **仅支持专业版**（不支持极速版）

## 功能

- 🎨 **文生3D**：通过文本描述生成3D模型
- 🖼️ **图生3D**：通过图片生成3D模型
- 🎯 **多版本支持**：支持模型版本3.0和3.1

## 快速开始

### 第一步：开通混元生3D服务

**必须**先在腾讯云控制台开通服务：

1. 访问 [腾讯混元生3D控制台](https://console.cloud.tencent.com/ai3d)
2. 点击「立即开通」或「申请开通」
3. 阅读并同意服务协议
4. 等待服务开通（通常即时生效）

**常见问题**：
- 如果显示"资源不足"，说明服务正在初始化，请等待5-10分钟后再试
- 如果无法开通，可能需要实名认证或联系客服

### 第二步：获取API Key

1. 访问 [混元生3D API Key管理页面](https://console.cloud.tencent.com/ai3d/api-key)
2. 点击「创建API Key」
3. 输入名称（如：hunyuan-3d-key）
4. 复制生成的API Key（格式：`sk-xxxxx`）

**⚠️ 重要**：API Key只显示一次，请妥善保存！

**备用地址**：如果上述链接无法访问，也可在 [混元大模型API Key页面](https://console.cloud.tencent.com/hunyuan/start) 创建

### 第三步：配置环境变量

**⚠️ 重要区别**：
- hunyuan-image 和 hunyuan-video 使用 **腾讯云 SecretId/SecretKey**
- hunyuan-3d 使用 **混元3D专用 API Key**（格式：`sk-xxxxx`）

**需要的环境变量**：
- `HUNYUAN_3D_API_KEY` - 混元3D API Key

**Windows PowerShell**:
```powershell
# 临时设置（当前会话）
$env:HUNYUAN_3D_API_KEY = "sk-xxxxx"

# 永久设置（推荐）
[Environment]::SetEnvironmentVariable("HUNYUAN_3D_API_KEY", "sk-xxxxx", "User")
```

**Linux/Mac**:
```bash
# 临时设置
export HUNYUAN_3D_API_KEY="sk-xxxxx"

# 永久设置（添加到 ~/.bashrc 或 ~/.zshrc）
echo 'export HUNYUAN_3D_API_KEY="sk-xxxxx"' >> ~/.bashrc
source ~/.bashrc
```

### 第四步：验证配置

```powershell
# 检查环境变量
Write-Host "API Key: $($env:HUNYUAN_3D_API_KEY.Substring(0,15))..."

# 测试生成
python scripts/generate.py --mode text --prompt "一只小狗"
```

**如果报错"资源不足"**：服务正在初始化，等待5-10分钟后重试

## 使用方法

### 基础用法

```bash
# 文生3D
python scripts/generate.py --mode text --prompt "一只可爱的小猪"

# 图生3D
python scripts/generate.py --mode image --image-url "https://example.com/pig.jpg"

# 使用3.1版本模型
python scripts/generate.py --mode text --prompt "小狗" --model 3.1
```

### 参数说明

| 参数 | 说明 | 示例 |
|------|------|------|
| `--mode` | 生成模式 | `text`(文生3D), `image`(图生3D) |
| `--prompt` | 文本描述（文生3D） | "一只可爱的小猪" |
| `--image-url` | 图片URL（图生3D） | "https://example.com/pig.jpg" |
| `--model` | 模型版本 | `3.0`(默认), `3.1` |
| `--output` | 输出目录 | `./models` |

### 模型版本说明

| 版本 | 特点 |
|------|------|
| 3.0 | 默认版本，功能完整 |
| 3.1 | 新版本，但LowPoly和Sketch参数不可用 |

### 输入要求

**文生3D**：
- 文本描述：最多1024个utf-8字符
- 支持中文提示词

**图生3D**：
- 图片格式：jpg, png, jpeg, webp
- 图片大小：≤8MB
- 分辨率：128px ~ 5000px（单边）

## 输出

生成的3D模型保存在 `{output}/{date}/{job_id}/` 目录下：
- `model.glb` - 3D模型文件（GLB格式）
- `model.obj` - 3D模型文件（OBJ格式，在ZIP中）
- `preview.png` - 预览图
- `info.json` - 任务信息

**输出格式**：
- 同时返回 `.glb` 和 `.obj` 格式
- 包含纹理贴图
- 附带预览图

## 接口信息

- **Base URL**: `https://api.ai3d.cloud.tencent.com`
- **提交任务**: `POST /v1/ai3d/submit`
- **查询任务**: `POST /v1/ai3d/query`
- **认证方式**: API Key (Header: `Authorization: sk-xxxxx`)

## 踩坑记录与解决方案

### 1. 服务未开通

**错误**：`ResourceUnavailable.NotExist`

**解决**：
1. 访问 https://console.cloud.tencent.com/ai3d
2. 开通混元生3D服务
3. 等待几分钟让服务生效
4. 重试

### 2. 资源不足

**错误**：`ResourceInsufficient`

**解决**：
- 服务刚开通时可能出现，等待5-10分钟后重试
- 如果持续出现，联系腾讯云客服

### 3. API Key错误

**错误**：`Unauthorized`

**解决**：
- 确认使用的是 **API Key**（不是SecretId/SecretKey）
- API Key格式应为 `sk-xxxxx`
- 在 https://console.cloud.tencent.com/ai3d/api-key 创建

### 4. 响应格式问题

**发现**：OpenAI兼容接口返回格式为：
```json
{
  "Response": {
    "JobId": "xxx",
    "Status": "DONE",
    "ResultFile3Ds": [...]
  }
}
```

**注意**：状态字段是 `Status` 不是 `StatusCode`，成功状态是 `DONE` 不是 `SUCCESS`

## 示例

```bash
# 生成小猪3D模型
python scripts/generate.py --mode text --prompt "一只可爱的小猪，粉色，卡通风格"

# 通过图片生成3D
python scripts/generate.py --mode image --image-url "https://example.com/pig-photo.jpg"

# 使用3.1版本
python scripts/generate.py --mode text --prompt "小狗" --model 3.1
```

## 注意事项

1. **异步接口**：分为提交任务和查询任务两个步骤
2. **任务有效期**：24小时
3. **并发限制**：默认3个并发
4. **仅专业版**：OpenAI兼容接口不支持极速版
5. **生成时间**：3D生成需要较长时间（1-5分钟），请耐心等待

## 相关链接

- [OpenAI兼容接口文档](https://cloud.tencent.com/document/product/1804/126189)
- [API Key管理](https://console.cloud.tencent.com/ai3d/api-key)
- [混元生3D控制台](https://console.cloud.tencent.com/ai3d)
- [提交任务API文档](https://cloud.tencent.com/document/product/1804/123447)

## 许可证

MIT License

---

[English Version](./README.md)
