# Whisper on Cloudflare AI

一个基于 Whisper 模型的在线音频转写工具，部署在 Cloudflare 上。该工具可以将音频文件转换为文字，并支持生成 SRT 格式的字幕文件。

实例：[https://whisper.ohen5pbf93.workers.dev/](https://whisper.ohen5pbf93.workers.dev/)

![index](https://github.com/user-attachments/assets/8818c6e9-8e4e-4cec-802e-16513de9f91e)

# 速度
使用一段时长为41分钟39秒的音频测试，用时1.9分钟

> 由于worker的资源限制，在使用时可能出现错误，重试即可

![example](https://github.com/user-attachments/assets/dac563ff-091f-479e-a750-d1f4ab1feafe)

## API 接口说明

### 1. `POST /raw`

返回未经处理的原始转写数据（JSON 格式）。

### 2. `POST /srt`

返回处理后的字幕数据（SRT 格式）。

#### 请求说明

* **请求方法**：`POST`
* **内容类型（Content-Type）**：`application/octet-stream`
* **请求体**：音频文件的二进制数据

#### 查询参数

| 参数名              | 类型      | 说明                                         |
| ---------------- | ------- | ------------------------------------------ |
| `task`           | string  | 任务类型，可选值：`transcribe`（转写）或 `translate`（翻译） |
| `language`       | string  | 目标语言代码，例如：`en`、`zh`、`ja` 等                 |
| `vad_filter`     | boolean | 是否启用 VAD（语音活动检测）过滤，`true` 或 `false`        |
| `initial_prompt` | string  | 初始提示词，用于引导模型理解语境（可选）                       |
| `prefix`         | string  | 前缀文本，用于增强上下文理解（可选）                         |
