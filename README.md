# 表情镜 — 读书表情陪伴工具

纯前端、无需后端的 Web 应用。你在看书时，摄像头实时捕捉面部表情，通过视觉反馈让你感知到"自己的表情被看见"，从而产生陪伴感和继续阅读的意愿。阅读结束后自动生成读书日记。

## 🎭 核心特性

- **7 种表情识别**：中性 / 皱眉 / 微笑 / 困惑 / 惊讶 / 专注 / 难过
- **眼镜自适应**：校准阶段自动检测眼镜，调整眉毛特征权重，防止镜框误判
- **互斥规则**：微笑与皱眉不会同时出现，微笑优先级更高
- **隐私优先**：基于 MediaPipe FaceLandmarker GPU 加速，摄像头数据永不离开设备
- **圆形摄像头 / 表情映射切换**：不想露脸时，一键切换为 emoji 表情映射
- **全屏粒子视觉反馈**：表情变化触发不同颜色和风格的粒子效果
- **读书日记**：阅读结束后自动生成情绪分布、最难时段、专注时长、个性化鼓励语
- **三款主题**：暗夜 / 明亮 / 暖棕
- **日记导出**：JSON / Markdown 双格式

## 🌐 在线使用

**直接打开：[avaluu.github.io/expression-mirror](https://avaluu.github.io/expression-mirror/)**

## 🚀 本地运行

```bash
git clone https://github.com/avaluu/expression-mirror.git
cd expression-mirror
python3 -m http.server 8000
# 打开 http://localhost:8000
```

> 摄像头 API 需要安全上下文（localhost 或 HTTPS），不支持 `file://` 协议。

## 🏗️ 技术栈

- HTML5 + CSS3 + JavaScript（零运行时依赖）
- MediaPipe FaceLandmarker（`@mediapipe/tasks-vision`，GPU WebGL 加速，478 个关键点）
- Canvas API（粒子系统渲染）
- LocalStorage（日记和统计数据持久化）
- 校准帧数 15，运行帧率 10fps，摄像头 640×480

## 📔 日记数据结构

```json
{
  "date": "2026-06-07 16:30",
  "durationMinutes": 42,
  "emotionDistribution": {
    "neutral": 25, "frowning": 12, "smiling": 18,
    "confused": 15, "surprised": 3, "focused": 22, "sad": 5
  },
  "hardestMoment": { "time": 12, "emotion": "confused", "pct": 65 },
  "feedbackTriggerCount": 47,
  "longestFocusMinutes": 22,
  "encouragementText": "有 22% 的时间高度专注，你进入了心流状态。"
}
```

## 🌐 浏览器兼容

Chrome/Edge 90+ · Safari 15+ · Firefox 90+ · 移动端 Safari/Chrome

## 📄 许可

MIT License
