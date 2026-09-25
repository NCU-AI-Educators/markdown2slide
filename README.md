# markdown2slide

> 内容自适应 Markdown 幻灯片排版与自动化编译引擎 (Content-Adaptive Markdown-to-Slide Compiler)

`markdown2slide` 是面向高校数字化教学教材与课件打造的后处理排版引擎。其核心使命是：**彻底解耦上游“教学内容创作”与下游“幻灯片视觉排版”**，实现将大模型生成的粗糙、未考虑排版的 Markdown/Marp 初稿，在确定的工程安全围栏与闭环回路中，自动后处理重塑为高审美、自适应留白、零视口截断的专业级幻灯片母本。

---

## 核心设计哲学 (Core Paradigms)

1. **逆向内容响应式设计 (CDRD, Content-Density Responsive Design)**：
   - 借鉴现代 Web 响应式设计思想，将宽度媒体查询逆向映射为单页“容量密度断点” (`ds-sm` ~ `ds-xl`)；
   - 依托 `@container` 容器查询与 `clamp()` 流体排版，实现组件内部在受限高度下的毫秒级紧致自愈。
2. **Harness 确定性安全围栏 (Guardrails)**：
   - 静态代码过滤器 100% 拦截 `style="..."` 与局部 `<style scoped>`，捍卫纯净单一事实源 (SSOT)；
   - 字符与卡片容量硬指标约束，从源头阻断文字超载。
3. **Loop 控制论闭环自愈回路 (Self-Healing Loop)**：
   - 无头 Chromium 渲染探针精准测量 DOM 几何尺寸，拦截视口溢出；
   - 遵循 `Max Loops = 3` 状态机收敛机制，依次调度“语义组件包装 $\to$ 梯度密度降级 $\to$ 结构化强制分页”，杜绝震荡死锁。

---

## 项目导航与文档

- **架构设计方案说明书（草稿）**：[docs/content_adaptive_slide_pipeline_design.md](./docs/content_adaptive_slide_pipeline_design.md)
- **核心架构与流程图谱**：
  - [图 1-1 传统排版劣质化与死循环因果链](./docs/figures/slide_legacy_antipattern.clean.svg)
  - [图 3-1 自适应幻灯片编译流水线架构全景](./docs/figures/slide_adaptive_pipeline.clean.svg)
  - [图 4-1 Loop 工程排版闭环控制算法与熔断状态机](./docs/figures/slide_loop_controller.clean.svg)
  - [图 8-1 内容自适应幻灯片编译架构三阶段演进路线图](./docs/figures/slide_evolution_roadmap.clean.svg)

---

## 当前状态 (Status)

- **阶段**：方案草稿与工程原型验证 (Draft / Work in Progress)
- **目标产物**：独立 Python/Node CLI 工具与智能体流水线后处理插件
