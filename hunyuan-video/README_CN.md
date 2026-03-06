# Hunyuan Video - 腾讯混元生视频

基于腾讯混元大模型的视频生成服务，支持文生视频、图生视频、视频风格化三大核心功能。

## 功能

- 🎬 **文生视频**：文本描述生成视频
- 🖼️ **图生视频**：图片生成视频（支持URL和本地文件）
- 🎨 **视频风格化**：视频转2D动漫/3D卡通等风格

## 快速开始

### 1. 安装依赖

```bash
pip install tencentcloud-sdk-python
```

### 2. 开通服务

1. 登录 [腾讯混元生视频控制台](https://hunyuan.cloud.tencent.com/#/app/videoModel)
2. 阅读并同意服务协议
3. 单击开通服务

### 3. 配置密钥

**需要的环境变量**：
- `TENCENT_SECRET_ID` - 腾讯云SecretId
- `TENCENT_SECRET_KEY` - 腾讯云SecretKey

```powershell
# Windows PowerShell - 永久设置
[Environment]::SetEnvironmentVariable("TENCENT_SECRET_ID", "your-secret-id", "User")
[Environment]::SetEnvironmentVariable("TENCENT_SECRET_KEY", "your-secret-key", "User")

# 或临时设置（当前会话）
$env:TENCENT_SECRET_ID = "your-secret-id"
$env:TENCENT_SECRET_KEY = "your-secret-key"
```

**获取API密钥**：https://console.cloud.tencent.com/cam/capi

### 4. 验证配置

```powershell
# 检查环境变量
Write-Host "SecretId: $env:TENCENT_SECRET_ID"
Write-Host "SecretKey: $($env:TENCENT_SECRET_KEY.Substring(0,10))..."

# 测试生成
python scripts/generate.py text2video "一只可爱的小猪在奔跑"
```

## 使用方法

### 1. 文生视频

```bash
python scripts/generate.py text2video "一只可爱的小猪在草地上奔跑"

# 指定分辨率
python scripts/generate.py text2video "日落" --resolution 1080p
```

**参数**：
- `prompt`: 文本描述（必填）
- `--resolution`: 分辨率（720p, 1080p，默认720p）

### 2. 图生视频

```bash
# 使用图片URL
python scripts/generate.py image2video "https://example.com/pig.jpg"

# 使用本地图片
python scripts/generate.py image2video "./my_pig.png"

# 添加辅助描述
python scripts/generate.py image2video "./pig.png" --prompt "小猪在奔跑"
```

**参数**：
- `image`: 图片URL或本地路径（必填）
- `--prompt`: 辅助描述（可选）

**支持格式**：
- URL: `http://` 或 `https://` 开头
- 本地文件: 相对路径或绝对路径

### 3. 视频风格化

```bash
# 转为2D动漫风格
python scripts/generate.py stylization "https://example.com/video.mp4" --style 2d_anime

# 转为3D卡通风格
python scripts/generate.py stylization "https://example.com/video.mp4" --style 3d_cartoon
```

**风格选项**：
- `2d_anime`: 2D动漫
- `3d_cartoon`: 3D卡通
- `3d_china`: 3D国潮
- `pixel_art`: 像素风

**输入视频要求**：
- 格式：mp4、mov
- 时长：1～60秒
- 分辨率：540P~2056P
- 大小：不超过200M
- FPS：15～60fps

## 输出

生成的视频保存在 `{output}/{date}/{job_id}/` 目录下：
- `{command}_result.mp4` - 生成的视频
- `info.json` - 任务信息

## 注意事项

1. **异步接口**：所有功能都是异步的，需要轮询等待任务完成
2. **状态码陷阱**：不同接口状态字段不一致：
   - 文生/图生视频：`Status: DONE`
   - 视频风格化：`JobStatusCode: 4` 或 `5+Success`
3. **Image参数陷阱**：`Image` 是对象类型，不是字符串：
   ```python
   # ❌ 错误
   req.Image = image_url
   
   # ✅ 正确
   image = models.Image()
   image.Url = image_url  # 或 image.Base64 = base64_data
   req.Image = image
   ```
4. **并发限制**：风格化默认1个并发，其他3个并发
5. **生成时间**：通常1-5分钟，请耐心等待

## 踩坑记录

### 服务未开通

**错误**：`FailedOperation.ServiceNotOpen`

**解决**：先在控制台开通混元生视频服务

### 视频下载失败

**错误**：`FailedOperation.DownloadError`

**解决**：
- 检查视频URL是否可访问
- 确保格式为mp4或mov
- 确保大小不超过200M

### 状态码混淆

**问题**：`JobStatusCode: 5` 可能实际是成功

**解决**：检查 `ResultDetails` 字段

## 示例

```bash
# 文生视频
python scripts/generate.py text2video "一只可爱的小猪在草地上奔跑，阳光明媚"

# 图生视频（本地文件）
python scripts/generate.py image2video "./my_pig.png" --prompt "小猪在奔跑"

# 视频风格化
python scripts/generate.py stylization "https://example.com/video.mp4" --style 2d_anime
```

## 相关链接

- [API概览](https://cloud.tencent.com/document/product/1616/107795)
- [混元生视频控制台](https://hunyuan.cloud.tencent.com/#/app/videoModel)
- [腾讯云密钥管理](https://console.cloud.tencent.com/cam/capi)

## 许可证

MIT License

---

[English Version](./README.md)
