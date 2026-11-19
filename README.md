# 自由点 · 小益智能体 🌿

> 微信小程序风格的移动端交互原型 —— 自由点品牌 AI 经期健康管家「小益」
> **单文件 HTML 交付，双击即开，离线可用**

![页面](https://img.shields.io/badge/%E9%A1%B5%E9%9D%A2-3%20Tab-FFD700)
![技术](https://img.shields.io/badge/Vue-3.5-42b883)
![技术](https://img.shields.io/badge/Vant-4-B39DDB)
![大模型](https://img.shields.io/badge/%E5%A4%A7%E6%A8%A1%E5%9E%8B-%E5%85%8D%E8%B4%B9%E6%8E%A5%E5%85%A5-brightgreen)

## 📱 功能特性

### 1. 小益 AI 对话（真正能聊的智能体）
- **双模式切换**（输入框左侧按钮）：
  - 💬 **即时对话** —— 秒回，重点解决问题、科普经期知识
  - 🕯️ **树洞模式（延迟回复）** —— 发送后只显示「已送达 · 小益稍后回你」，过几分钟才像老朋友一样回你；回复**拆成 2~4 条短消息逐条直接弹出**（无「正在输入」动效），细碎口语化、像真人连着发微信，先共情再建议，更有陪伴感
- **真实大模型接入**（点右上角 ⚙ 滑杆按钮配置）：
  - 默认 **Pollinations**：免注册、免 Key，零配置直接聊
  - 可切换 **DeepSeek**（按量计费，一轮对话约几厘钱，中文强）/ **智谱 GLM-4-Flash**（免费）/ **Groq** / **硅基流动**（免费额度）
  - Key 按引擎分开保存在你自己的浏览器 localStorage
  - **多引擎自动降级链**：主引擎 → 其他已配置引擎 → Pollinations 兜底 → 本地模拟，永不冷场
  - Pollinations 匿名额度限流（402）时自动换模型重试、静默冷却 5 分钟后自动恢复，Toast 每会话只提示一次
- 规则内置：严重病痛温柔提醒就医、应急需求引导美团闪购、每轮带 emoji、绝不硬广

### 2. 经期日历
- 2026 年 11 月日历，**点击任意日期即可标记 / 取消经期**，图例实时显示「经期 N 天」
- 今日记录改为**自由文本框**，随手记下血块 / 气味 / 感受或任何想记的事
- 保存按钮 Toast「记录成功」

### 3. 我的抽屉
- 拟物抽屉卡片 + 三款自由点产品（益生菌LA88 / 有机纯棉 / 安心裤），角标显示「剩余 X 包」
- **点击角标可手动调整库存**（步进器弹层）
- 底部悬浮「一键补货」直达淘宝

## 🚀 打开方式

| 方式 | 说明 |
|---|---|
| 本地直接打开 | 双击 `index.html`（**完全离线可用**，依赖已内嵌到 `assets/vendor/`） |
| GitHub Pages | 推送后在仓库 Settings → Pages 开启，全球可访问 |
| 本地服务 | `python -m http.server 8000` 后访问 `http://localhost:8000` |

依赖加载策略：**本地 vendor 优先，CDN（unpkg / jsdelivr）自动兜底** —— 即使只拷贝一个 `index.html` 也能正常运行（需联网）。

## 📂 目录结构

```
├── index.html            # 主文件（全部页面 / 样式 / 逻辑 / 图片 base64 内嵌）
├── assets/               # 原始素材
│   ├── 益生菌LA88.jpg / 有机纯棉.jpg / 安心裤.jpg   # 产品图（已压缩内嵌）
│   ├── 小益智能体头像.jpg / 小益智能体头像2.png      # 管家头像（已内嵌）
│   └── vendor/           # 本地依赖：vue / vant / tailwind
└── demo/                 # 历史演示副本（可忽略）
```

## ⚙️ 自定义指南

| 想改什么 | 在 `index.html` 里搜什么 |
|---|---|
| 淘宝补货链接 | `TAOBAO_LINK` |
| 树洞模式等待时长 | `DELAYED_REPLY_MS`（演示 20 秒；真实产品改 `120000`~`300000` 即 2~5 分钟） |
| 大模型引擎 / 提示词 | `LLM_PROVIDERS` / `systemPrompt()` |
| 智能体人设与规则 | `systemPrompt()` |
| 本地兜底话术 | `getAgentReply()` |
| 主题色 | `<style>` 里的 `--gold: #FFD700`、`--lilac: #B39DDB` |
| 经期标记日期 | `store.periodDays` |
| 库存默认值 | `store.stock` |

## 🛠 技术栈

- **[Vue 3.5](https://github.com/vuejs/core)** —— 响应式全局 Store（类 Pinia），`v-show` 切换页面保留状态
- **[Vant 4](https://github.com/vant-ui/vant)** —— Tabbar / Field / Button / Badge / Toast / Popup / Radio
- **[Tailwind CSS](https://github.com/tailwindlabs/tailwindcss)**（Play CDN 本地化）—— 配色与布局
- **[Lucide Icons](https://github.com/lucide-icons/lucide)** —— 图标已全部内联为静态 SVG，零运行时依赖
- 智能体：OpenAI 兼容协议 `/chat/completions`，浏览器直连，无需后端

## ⚠️ 注意

- API Key 仅保存在浏览器 `localStorage`，**仅供个人演示，请勿用于生产环境**
- 大模型回复内容由 AI 生成，健康建议仅供参考，不能替代医生诊断

## 📄 开源致谢

[Vue](https://github.com/vuejs/core) · [Vant](https://github.com/vant-ui/vant) · [Tailwind CSS](https://github.com/tailwindlabs/tailwindcss) · [Lucide](https://github.com/lucide-icons/lucide) · [Pollinations](https://pollinations.ai)
