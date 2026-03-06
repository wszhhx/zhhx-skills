# Hunyuan Image - 腾讯混元生图

基于腾讯混元大模型的AI图像生成服务。

## 功能

- 🎨 **文生图**：根据文本描述生成图像
- 🖼️ **多分辨率**：支持多种宽高比
- 🎭 **风格支持**：多种绘画风格（动漫、油画、水彩等）
- 🔧 **参考图**：支持参考图引导生成
- ⚡ **超分增强**：支持2倍/4倍超分

## 快速开始

### 1. 安装依赖

```bash
pip install tencentcloud-sdk-python
```

### 2. 配置密钥

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

### 3. 验证配置

```powershell
# 检查环境变量是否已设置
if ($env:TENCENT_SECRET_ID -and $env:TENCENT_SECRET_KEY) {
    Write-Host "✅ 环境变量已配置"
} else {
    Write-Host "❌ 请设置 TENCENT_SECRET_ID 和 TENCENT_SECRET_KEY"
}

# 测试生成
python scripts/generate.py "一只可爱的小猫"
```

## 使用方法

### 基础用法

```bash
# 生成图片
python scripts/generate.py "一只可爱的小猪在草地上"

# 指定分辨率
python scripts/generate.py "日落" --resolution 1024:768

# 指定风格
python scripts/generate.py "动漫女孩" --style 201

# 生成多张
python scripts/generate.py "山水画" --num 4
```

### 参数说明

| 参数 | 说明 | 示例 |
|------|------|------|
| `prompt` | 文本描述（必填） | "一只可爱的小猪" |
| `--resolution` | 分辨率 | `1024:1024`, `768:1024` |
| `--style` | 风格编号 | `201`（动漫） |
| `--num` | 生成数量（1-4） | `2` |
| `--clarity` | 超分选项 | `x2`, `x4` |
| `--output` | 输出目录 | `./images` |

### 分辨率选项

- `768:768` - 1:1 方形
- `768:1024` - 3:4 竖版（手机壁纸）
- `1024:768` - 4:3 横版
- `1024:1024` - 1:1 方形（高清）
- `720:1280` - 9:16 竖版（手机全屏）
- `1280:720` - 16:9 横版（电脑壁纸）

### 风格列表（常用）

| 编号 | 风格 |
|------|------|
| 101 | 水墨画 |
| 102 | 概念艺术 |
| 103 | 油画 |
| 104 | 水彩画 |
| 201 | 动漫 |
| 202 | 日本动画 |
| 301 | 3D卡通 |
| 401 | 肖像画 |
| 501 | 赛博朋克 |
| 601 | 蒸汽波 |

完整列表：https://cloud.tencent.com/document/product/1729/105846

## 输出

生成的图片保存在 `{output}/{date}/{job_id}/` 目录下：
- `image_0.png` - 生成的图片
- `info.json` - 任务信息（包含扩写后的描述）

## 注意事项

1. **异步接口**：API是异步的，需要等待任务完成
2. **并发限制**：默认1个并发
3. **地域限制**：仅支持 `ap-guangzhou`
4. **Prompt扩写**：默认开启，可提升生成效果
5. **水印**：默认不添加水印。使用 `--logo` 参数可添加"图片由AI生成"水印

## 踩坑记录

### 状态码陷阱

API返回 `JobStatusCode: 5` 可能是成功！需要检查 `ResultDetails`：

```python
if status == '4' or (status == '5' and result.get('ResultDetails') == ['Success']):
    print('✅ 实际生成成功！')
```

### 常见错误

| 错误 | 解决方案 |
|------|----------|
| `UnauthorizedOperation` | 检查SecretId/SecretKey |
| `FailedOperation.DownloadError` | 检查图片URL是否可访问 |
| `InvalidParameterValue.InvalidImageFormat` | 只支持jpg/png格式 |

## 示例

```bash
# 生成动漫风格头像
python scripts/generate.py "可爱女孩, 短发, 微笑, 樱花背景" --style 201 --resolution 768:768

# 生成赛博朋克壁纸
python scripts/generate.py "未来城市, 霓虹灯, 雨夜" --style 501 --resolution 1920:1080 --clarity x2

# 生成水墨画
python scripts/generate.py "山水, 瀑布, 松树, 云雾" --style 101 --resolution 1024:768
```

## 相关链接

- [API文档](https://cloud.tencent.com/document/product/1729/105969)
- [腾讯云控制台](https://console.cloud.tencent.com/cam/capi)
- [风格列表](https://cloud.tencent.com/document/product/1729/105846)

## 许可证

MIT License

---

[English Version](./README.md)
