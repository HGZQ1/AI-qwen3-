# 短视频灵感创作助手

基于阿里云百炼平台 **Qwen Plus** 大模型的短视频创意灵感生成 Web 应用，由 **小琴羽不是神明** 开发。参赛作品：第二届兴智杯全国人工智能创新应用大赛。

---

## 功能特性

- **个性化用户画像** — 根据性别、年龄、地域、粉丝量、创作者类型构建用户画像，生成定制建议
- **灵感内容分析** — 提取关键词、情感风格、用户意图，结合平台热点趋势进行深度分析
- **创意建议生成** — 多方向创意扩展，结合当前热门元素给出可落地的拍摄方案
- **数据可视化** — ECharts 播放量趋势折线图 + 互动指标饼图，直观呈现预测数据
- **优秀案例参考** — AI 推荐同类型高流量视频特点，辅助参考学习
- **灵感总结** — 整合所有分析，输出精简创作行动方案
- **沉浸式交互** — 多页面切换动效、浮动装饰图标、Loading 文案轮播

---

## 技术栈

| 层级 | 技术 |
|------|------|
| 前端 | 原生 HTML / CSS / JavaScript |
| UI 框架 | Tailwind CSS (CDN) |
| 图表库 | Apache ECharts 5.5 |
| Markdown 渲染 | marked.js |
| 图标 | Font Awesome 6 |
| 后端 | Node.js + Express 4 |
| AI 模型 | 阿里云百炼 `qwen-plus-2025-07-28` |
| 环境变量 | dotenv |

---

## 目录结构

```
AI-qwen3--main/
├── index.html      # 前端主页面（欢迎 / 输入 / 加载 / 结果 四个分镜）
├── script.js       # 前端交互逻辑、API 调用、图表渲染
├── style.css       # 自定义样式
├── server.js       # Express 后端，代理 DashScope API 请求
├── package.json    # 项目依赖
├── .env            # 环境变量（存放 API Key，不提交版本库）
└── 使用指南.txt    # 简易使用说明
```

---

## 前置条件

- [Node.js](https://nodejs.org/) >= 16
- 阿里云百炼平台账号及有效的 **DashScope API Key**（[申请地址](https://bailian.console.aliyun.com/)）

---

## 安装与启动

### 1. 安装依赖

```bash
npm install
```

### 2. 配置 API Key

在项目根目录创建（或编辑）`.env` 文件：

```env
DASHSCOPE_API_KEY=your_api_key_here
PORT=3000
```

> **注意**：`.env` 文件包含敏感信息，请勿上传至公开代码仓库。

### 3. 启动服务

```bash
npm start
```

启动成功后访问：[http://localhost:3000](http://localhost:3000)

开发模式（文件变更自动重启）：

```bash
npm run dev
```

---

## 使用流程

```
欢迎页 → 填写创作信息 → 提交灵感 → AI 分析中 → 查看结果报告
```

**输入信息说明：**

| 字段 | 是否必填 | 说明 |
|------|----------|------|
| 性别 | 必填 | 影响受众画像推断 |
| 年龄 | 选填 | 辅助难度与成本建议 |
| 地域 | 选填 | 区域热点参考 |
| 粉丝量 | 选填 | 影响涨粉策略推荐 |
| 创作者类型 | 必填 | 个人 / 团队 |
| 视频类型 | 必填 | 17 种类型可选 |
| 创作灵感 | 必填 | 自由描述你的想法 |

---

## API 说明

后端暴露一个代理接口，避免前端直接暴露 API Key：

```
POST /api/ai-inspire
Content-Type: application/json
```

请求体直接透传至阿里云 DashScope 文本生成接口，默认使用模型 `qwen-plus-2025-07-28`，参数：

```json
{
  "parameters": {
    "max_token_limit": 32768,
    "temperature": 0.9,
    "top_p": 0.7,
    "repetition_penalty": 1.1
  }
}
```

---

## 常见问题

### Windows PowerShell 执行 `npm install` 报错（脚本被禁止运行）

**原因**：系统执行策略为 `Restricted`，禁止运行 `.ps1` 脚本。

**解决步骤：**

1. 以**管理员身份**打开 PowerShell
2. 查看当前策略：
   ```powershell
   Get-ExecutionPolicy
   ```
3. 修改为 `RemoteSigned`：
   ```powershell
   Set-ExecutionPolicy RemoteSigned
   ```
4. 重新执行 `npm install`，然后 `npm start`

### 服务器返回"缺少API密钥"错误

检查项目根目录是否存在 `.env` 文件，且 `DASHSCOPE_API_KEY` 已正确填写（无多余空格或引号）。

### AI 返回内容显示异常

AI 响应会按 `###` 或数字列表分段解析并分别渲染到各卡片中。如遇显示问题，可打开浏览器控制台查看 `debug-response` 隐藏元素中的原始 AI 返回文本进行排查。

---

## 开发者

**小琴羽不是神明**（HolleWorld小琴羽）

参赛信息：第二届兴智杯全国人工智能创新应用大赛 · AI创意助手赛道
