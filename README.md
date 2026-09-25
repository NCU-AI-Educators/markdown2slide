# markdown2slide

<p align="center">
  <strong>🚀 将任意 Markdown 长文自动化重构为高审美、自适应留白的精美 Marp 演示幻灯片</strong><br>
  <em>Transform any long-form Markdown document into exquisite, content-adaptive, production-ready Marp presentations.</em>
</p>

<p align="center">
  <a href="#核心痛点与解决思路">核心痛点</a> •
  <a href="#四大核心引擎特性">核心特性</a> •
  <a href="#系统架构全景">系统架构</a> •
  <a href="#使用场景">使用场景</a> •
  <a href="#架构设计规范草稿">设计规范</a> •
  <a href="#演进路线图">路线图</a>
</p>

---

## 💡 为什么需要 markdown2slide？

在数字化出版、技术演讲与知识传播中，**将 Markdown 长文（技术博客、项目文档、学术论文、行业研报、教材大纲）转换为演示幻灯片**是刚需，但传统方式存在极大的工程断层：

| 痛点场景 | 传统做法的致命缺陷 | markdown2slide 的破局之道 |
| :--- | :--- | :--- |
| **手工分片排版** | 人工反复剪裁文字、调试网格与外边距，改一讲耗费数天 | **智能语义解构**：按逻辑重心与认知负荷自动切片，秒级转换 |
| **大模型直接生成** | 大模型没有空间感，生成动辄 400 字的长文，文字冲出屏幕底边严重截断 | **视口刚性防御**：建立严格的单页容量阈值，从源头杜绝过载 |
| **开环打补丁** | 遇到超长文字盲目注入 `style="font-size:0.72em"`，字如密蚁、失去呼吸感 | **CDRD 逆向响应式**：容器查询与流体字号自愈，超限自动优雅拆页 |
| **内联 HTML 泥潭** | 页面塞满专有 `<div style="...">` 标签，彻底破坏 Markdown 纯净度 | **单一事实源 (SSOT)**：100% 阻断内联脏样式，基于语义类名装配 |

---

## ⚡ 四大核心引擎特性 (Core Features)

### 1. 智能语义切片与叙事编排 (Semantic Chunking & Pacing)
- 告别按固定字数机械切片的粗暴做法；
- 基于段落主题重心、论点推进节奏与认知负荷理论，自动将万字长文重组为符合演讲叙事逻辑的单页幻灯片。

### 2. 逆向内容响应式排版 (CDRD, Content-Density Responsive Design)
- 借鉴现代 Web 响应式设计思想，将“宽度断点”逆向映射为单页“容量密度断点” (`ds-sm` ~ `ds-xl`)；
- 依托 `@container` 容器查询与 `clamp()` 双向流体字号，容器高度受限时内部间距自动毫秒级紧致自愈，**彻底取缔手工猜测字号**。

### 3. 语义组件与视觉容器自动装配 (Semantic Component Assembly)
- 自动识别长文中的核心论点、分栏意图、流程推导与对等比较；
- 零内联 HTML，自动装配纯语义网格（`.split-layout.ratio-5-5`、`.ratio-4-6`、`.ratio-3-col`）；
- 将枯燥的扁平列表封装为高审美语义卡片（`.card.insight`、`.card.tip`、`.card.warning`、`.card.key-point`）。

### 4. 无头沙盒闭环自愈回路 (Closed-Loop Self-Healing Engine)
- 内置 Chromium 无头沙盒测量探针，毫秒级实测渲染后 DOM 的几何像素尺寸与底部呼吸留白；
- 遵循 `Max Loops = 3` 控制论闭环状态机：检测到视口溢出时，依次调度“标准包装 $\to$ 密度阶梯降级 $\to$ 结构化强制拆页”，**100% 杜绝底部截断与震荡死锁**。

---

## 📐 系统架构全景

```
[任意 Markdown 长文输入] 
       │ 
       ▼
 [ 语义解构与节奏切片 ] (Semantic Chunking)
       │
       ▼
 [ 容量密度审计与断点映射 ] (VWS Gauge & CDRD)
       │
       ▼
 [ 纯语义网格与卡片装配 ] (Zero-Inline CSS)
       │
       ▼
 [ 无头 Chromium 沙盒探针 ] (Headless DOM Measure)
       │
       ├── (未溢出) ───────────────────────────┐
       │                                       ▼
       └── (检测到溢出) ──> [ 3轮阶梯自愈/拆页 ] ──> [ 高审美精美 Marp 演示母本 ]
```

- **全景工作流架构图**：详见 [docs/figures/slide_adaptive_pipeline.clean.svg](./docs/figures/slide_adaptive_pipeline.clean.svg)
- **自愈状态机算法模型**：详见 [docs/figures/slide_loop_controller.clean.svg](./docs/figures/slide_loop_controller.clean.svg)

---

## 🎯 典型使用场景 (Use Cases)

- 🛠 **开发者与技术布道师**：将开源项目 README、技术博客、架构设计 RFC 一键转为技术大会/Meetup 高颜值演讲 PPT；
- 🎓 **高校学者与培训讲师**：将整本教材长文、学术讲义自动化批量重塑为现代化投影课件，彻底解放备课生产力；
- 📊 **研报分析师与咨询顾问**：将万字行业调研报告、商业计划书快速派生为高可读性的决策汇报幻灯片；
- 🤖 **AI Agent 开发者**：作为智能体流水线的标准“排版与视觉后处理插件”，让上游 LLM 专注内容创作，排版全由本引擎兜底保底。

---

## 📚 详细设计规范文档

详细的算法设计、数学公式推导、设计令牌体系与状态机转换契约，请参阅：
- 📖 [内容自适应幻灯片编译流水线架构设计与工程规范说明书（方案草稿）](./docs/content_adaptive_slide_pipeline_design.md)

---

## 🗺 演进路线图 (Roadmap)

- [x] **Phase 1: 理论建模与规范建立** (2026 Q3)
  - [x] 确立 CDRD 容量密度断点与流体排版算法
  - [x] 完成 Harness 围栏与 Loop 闭环自愈状态机理论推导
  - [x] 建立 4 套出版级架构图谱与系统规范草稿
- [ ] **Phase 2: 核心引擎与 CLI 工具实装** (2026 Q4)
  - [ ] 研发 `markdown2slide` 独立跨平台 CLI (`npm` / `pip`)
  - [ ] 集成 Playwright / Puppeteer 无头沙盒几何探针
  - [ ] 实现 AST 级长文自适应切片器与卡片装配器
- [ ] **Phase 3: 生态解耦与多端多主题支持** (2027 Q1)
  - [ ] 支持 Academic / Tech Dark / Clean Minimal 等多套官方设计主题
  - [ ] 扩展支持 Slidev、Reveal.js 与 Typst 跨端多目标编译输出
  - [ ] 提供 VS Code 实时预览自愈扩展插件

---

## 📄 开源许可证

本项目采用 [MIT License](./LICENSE) 开源许可协议。
