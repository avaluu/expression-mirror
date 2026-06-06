# 表情镜 — 读书表情陪伴工具

一个纯前端、无需后端的 Web 应用。用户在看难书时，摄像头实时捕捉面部表情，通过视觉反馈让用户感知到"自己的表情被看见"，从而产生陪伴感和继续阅读的意愿。

## 核心特性

- 🎭 **实时表情识别**：基于 MediaPipe FaceMesh，本地识别皱眉、微笑、困惑、惊讶、中性 5 种表情
- 🎨 **视觉反馈系统**：根据表情在屏幕边缘绘制粒子氛围效果，不遮挡阅读区
- 📔 **读书日记总结**：阅读结束后自动生成情绪旅程总结，含分布图、最难时段、专注时长
- 🔒 **隐私优先**：摄像头数据永不离开设备，无需 API Key
- 📱 **响应式设计**：支持桌面端和移动端浏览器
- ⚡ **性能优化**：8-10fps 表情识别、640x480 摄像头、页面不可见时暂停

## 使用方法

1. 打开 `index.html`（需要浏览器支持 HTTPS 或 localhost，因为需要访问摄像头）
2. 等待面部表情校准完成（约 3 秒）
3. 粘贴文本、上传 TXT/PDF 文件
4. 点击"开始阅读"
5. 阅读过程中，表情变化会触发视觉氛围效果
6. 点击"结束阅读"，自动生成读书日记

## 推荐运行方式

```bash
# 使用 Python 启动本地服务器
cd expression-mirror
python3 -m http.server 8000

# 然后用 Python 启动本地服务器
# 访问 http://localhost:8000
```

> 注意：摄像头 API 需要安全上下文（HTTPS 或 localhost）。直接用 `file://` 协议打开可能无法访问摄像头。

## 技术栈

- HTML5 + CSS3 + JavaScript（零依赖运行时）
- MediaPipe FaceMesh（CDN 加载，468 个面部特征点）
- PDF.js（CDN 加载，PDF 文本提取）
- Canvas API（粒子系统和视觉反馈渲染）
- LocalStorage（日记和统计数据持久化）

## 日记数据结构

```json
{
  "id": "2026-06-06T14-30-00-000Z",
  "date": "2026-06-06 14:30",
  "timestamp": 1717684200000,
  "durationMinutes": 35,
  "emotionDistribution": {
    "frowning": 42,
    "smiling": 8,
    "confused": 25,
    "neutral": 25,
    "surprised": 0
  },
  "hardestMoment": {
    "timeOffsetMinutes": 12,
    "primaryEmotion": "confused",
    "intensity": 78
  },
  "feedbackTriggerCount": 47,
  "longestFocusMinutes": 18.5,
  "encouragementText": "..."
}
```

## 浏览器兼容性

- Chrome/Edge 90+
- Safari 15+
- Firefox 90+
- 移动端 Safari/Chrome

## 许可

MIT License
