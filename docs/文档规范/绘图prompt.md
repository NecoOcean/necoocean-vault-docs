# 绘图 prompt

**版本**：v1.0
**生效日期**：2026-09-21
**来源**：自长期记忆（`~/.workbuddy/MEMORY.md` §「技术文档插图 Prompt 库」）提取同步，原始出处为 `D:\Data\code\开发技术文档插图 Prompt 统一手册（流程图_架构图_时序图）.md`
**适用范围**：技术文档、PPT、Word 中需要**位图插图**的流程图、架构图、时序图

---

## 零、本文档的定位与边界

### 0.1 与 `文档图表绘制规范.md` 的分工

| 项 | 本文档（`绘图prompt.md`） | `文档图表绘制规范.md` |
|---|---|---|
| 输出形态 | **位图**（PNG / JPG） | **矢量文本**（ASCII 框图 / Mermaid） |
| 生产手段 | AI 绘图工具（Midjourney / Stable Diffusion / 文心一格 / 通义万相等） | 手工绘制或代码块 |
| 使用场景 | PPT 配图、Word 正式文档配图、封面插图 | 仓库内 Markdown 文档内嵌图表 |
| 可版本控制 | 否（二进制） | **是**（纯文本，可 diff） |
| 可编辑性 | 需重新生成 | 直接改文本 |

> ⚠️ **二者不可互相替代**。仓库内文档一律使用 `文档图表绘制规范.md` 的形态（可版本控制、可评审）；本文档仅用于需要**位图插图**的对外交付物。

### 0.2 触发条件

当任务需要生成**流程图 / 架构图 / 时序图**类插图时，自动按下表检索对应 Prompt 并应用，**不另行询问风格**。

### 0.3 共用视觉基调

**所有图类共用**：扁平矢量风（flat vector）、无 3D、无渐变、无阴影、无装饰元素、蓝绿商务配色（blue-green）、无衬线字体工整、节点对齐规整、高可读性。

> 该基调与 `文档图表绘制规范.md` §六 一致——**同一项目的所有图表应可被识别为同一套视觉体系**。

---

## 一、通用负面 Prompt

**全图类通用，原文照用，不修改。**

```
photorealistic, 3d render, gradient, texture, photo, clutter, messy lines, overlapping text, watermark, hand drawn, sketch, cartoon, blur, glowing effect, heavy border, color noise, decorative elements
```

---

## 二、提示词条目

| 编号 | 适用图表类型 | 背景 | 正向 Prompt（原文） |
|---|---|---|---|
| **P-FLOW-STD** | 技术流程图（标准版，设计文档/PPT 主推） | 浅灰底 | `technical workflow flow chart, flat vector illustration, light gray background, rounded rectangle nodes, diamond decision nodes, thin solid connecting arrows, complete logic branches, success and failure paths, clean sans-serif typography, consistent blue-green color palette, neatly aligned layout, high readability, software system diagram, for developer documentation, no shadows, no decorative ornaments` |
| **P-FLOW-WHITE** | 技术流程图（纯白底极简版，适配 Word/WPS 粘贴） | 纯白底 | `technical system flow chart, flat vector diagram, pure white background, rounded rectangular process nodes, diamond decision boxes, thin black arrows, clear branch logic, data flow logic, clean simple sans-serif font, neat layout, software development document illustration, minimalist style, high definition text` |
| **P-FLOW-SWIM** | 泳道流程图（多角色/多系统协同专用） | 浅灰底 | `swimlane technical flow chart, flat vector illustration, light gray background, independent divided swimlane columns, rounded rectangle action nodes, diamond decision nodes, thin uniform connecting arrows, cross-system collaborative workflow, clear text labels, clean sans-serif font, neat overall alignment, professional developer design document illustration` |
| **P-ARCH-STD** | 系统组件架构图（标准版，微服务/组件架构通用） | 浅灰底 | `system component architecture diagram, flat vector illustration, light gray background, rounded rectangle service boxes, solid thin dividing lines, thin connecting arrows for data communication, layered layout, clear module grouping, clean sans-serif typography, consistent blue-green color palette, neatly aligned, high readability, technical design document illustration, no shadows, no decorative ornaments` |
| **P-ARCH-WHITE** | 软件组件架构图（纯白底极简版，Word 正式文档专用） | 纯白底 | `software component architecture diagram, flat vector diagram, pure white background, rounded rectangular component boxes, thin solid arrows, module dependency relationship, neat layered arrangement, clean simple sans-serif font, minimalist style, for developer documentation, clear text labels, uniform spacing` |
| **P-ARCH-LAYER** | 分层架构图（三层架构/多层系统专用） | 浅灰底 | `layered system architecture diagram, flat vector illustration, light gray background, grouped subgraph modules with subtle bounding boxes, rounded rectangle components, thin arrows for request and response, clear layer separation, presentation layer, business layer, data layer, clean sans-serif typography, blue-green color scheme, well-aligned layout, technical document illustration` |
| **P-SEQ-STD** | 时序图（标准版，开发对接/接口文档主推） | 浅灰底 | `system sequence diagram, flat vector illustration, light gray background, vertical participant lifelines, horizontal thin message arrows, clear time sequence order, synchronous and asynchronous call marking, rectangular message nodes, clean sans-serif typography, uniform blue-green tone, neat vertical and horizontal alignment, high readability, software interface interaction document, no shadows, no redundant decoration` |
| **P-SEQ-WHITE** | 时序图（纯白底极简版，正式报告/归档文档） | 纯白底 | `technical sequence diagram, flat vector minimalist diagram, pure white background, standard lifeline structure, thin black message arrows, clear interaction logic, ordered time sequence, simple and neat layout, clear text labels, professional software development document illustration, no decorative elements` |
| **P-SEQ-MULTI** | 多服务交互时序图（微服务多角色调用） | 浅灰底 | `multi-service interaction sequence diagram, flat vector illustration, light gray background, multiple participant lifelines including client, gateway, backend service, database, horizontal request and response arrows, clear call sequence, synchronous invocation and async notification distinction, standardized technical diagram layout, clean typography, unified blue-green color system` |

---

## 三、自定义替换规则

| # | 规则 | 说明 |
|---|---|---|
| 1 | **业务场景替换位** | P-FLOW-STD 开头可替换为 `<业务场景> workflow flow chart`；P-ARCH-STD 开头可替换为 `<架构类型> architecture diagram`（例：`microservice architecture diagram`） |
| 2 | **尺寸比例** | PPT 配图追加 `--ar 16:9`；Word 配图追加 `--ar 4:3` |
| 3 | **同步/异步区分** | 追加 `solid arrow for sync call, dashed arrow for async message` |
| 4 | **配色替换** | 默认蓝绿；商务蓝橙风替换 `consistent blue-green color palette` → `blue and orange color palette` |
| 5 | **文字优化** | 文字模糊时追加 `text labels clear and legible, high resolution text` |
| 6 | **排版优化** | 元素重叠时追加 `reasonable spacing between all nodes, no overlapping elements` |

---

## 四、选用优先级（默认约定）

| 场景 | 选用 |
|---|---|
| 未指定用途 · 设计文档 / PPT | 首选 `*-STD` |
| 未指定用途 · Word 正式文档 / 归档 | 首选 `*-WHITE` |
| 多角色协同流程 | `P-FLOW-SWIM` |
| 三层/多层系统 | `P-ARCH-LAYER` |
| 微服务多参与方调用 | `P-SEQ-MULTI` |

---

## 五、使用示例

**场景**：为架构文档生成一张 PPT 配图用的系统分层架构图。

```
layered system architecture diagram, flat vector illustration, light gray background,
grouped subgraph modules with subtle bounding boxes, rounded rectangle components,
thin arrows for request and response, clear layer separation, presentation layer,
business layer, data layer, clean sans-serif typography, blue-green color scheme,
well-aligned layout, technical document illustration
--ar 16:9
```

**负面 Prompt**（附加）：

```
photorealistic, 3d render, gradient, texture, photo, clutter, messy lines, overlapping text,
watermark, hand drawn, sketch, cartoon, blur, glowing effect, heavy border, color noise,
decorative elements
```

---

## 六、注意事项

### 6.1 本文档面向位图输出

本 Prompt 库面向 AI 绘图工具的**位图**输出。若任务实际要求的是内嵌 SVG / HTML 可视化（Visualizer 渲染），则**遵循 Visualizer 自身的主题与尺寸约束**，仅沿用本库的**视觉基调**（扁平矢量、蓝绿配色、无渐变阴影装饰、对齐规整）。

### 6.2 与项目约束的冲突检查

本项目的两项硬约束会与位图插图产生交互，使用前须检查：

| 约束 | 影响 |
|---|---|
| **首屏 gzip ≤163 KB** | 位图体积大，**不得用于网页首屏**；仅限 PPT / Word / 归档场景 |
| **3 Mbps 带宽** | 若插图需在线分发，须先压缩至合理体积或改为矢量形态 |

### 6.3 内容准确性的责任边界

AI 绘图工具**无法可靠生成准确的文字标签**——中文尤其容易出现错字、漏字、乱码。

> **纪律**：**生成的是构图与风格，不是内容**。文字标签须在生成后用图片编辑工具覆写，或改用 Mermaid / ASCII 形态重新绘制。**不得将含错字的 AI 生成图直接放入交付文档。**

### 6.4 与图表规范的交叉引用

- 技术文档内嵌图表 → `文档图表绘制规范.md`
- 图表命名与图例 → `文档图表绘制规范.md` §三
- 视觉基调 → `文档图表绘制规范.md` §六

---

## 七、修订记录

| 版本 | 日期 | 说明 |
|---|---|---|
| v1.0 | 2026-09-21 | 初版。自长期记忆提取 Prompt 库并同步至本目录；补充与 `文档图表绘制规范.md` 的分工说明、与项目约束的冲突检查、内容准确性责任边界 |
