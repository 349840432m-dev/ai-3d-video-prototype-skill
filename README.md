# AI 3D / Video Prototype Skill

一个把视觉概念转成 **交互式 3D 原型** 或 **AI 视频概念片** 的 Agent Skill。

An agent skill for turning visual concepts into either **interactive 3D prototypes** or **AI-generated video showcases**.

## 能做什么 / What it does

这个 Skill 提供两条可独立使用、也可组合的制作路径：

This skill supports two independent or combined production paths:

### Path A — Hunyuan3D → Interactive 3D

- 从单图或多视图生成可复用的 3D 资产
- 优先输出适合浏览器加载的 `GLB`
- 使用 React、Vite、Three.js、React Three Fiber 与 Drei 构建交互原型
- 支持旋转、检查、标注、缩放、配置、截图与导入导出等交互设计
- 在模型不可用时使用程序化几何体或占位 GLB，保持原型可运行

- Generate reusable 3D assets from single or multi-view images
- Prefer browser-ready `GLB` output
- Build interactive prototypes with React, Vite, Three.js, React Three Fiber, and Drei
- Design interactions such as rotate, inspect, annotate, zoom, configure, capture, and import/export
- Keep prototypes runnable with procedural geometry or placeholder GLBs when generation is unavailable

### Path B — Seedance 2.0 → Video

- 从首帧、尾帧或关键帧设计短视频
- 明确镜头运动、主体运动、时长、节奏与视觉风格
- 约束身份漂移、多余结构、文字伪影与背景突变
- 输出视频提示词、关键帧清单、镜头表、封面和发布文案

- Design short videos from first, end, or key frames
- Specify camera movement, subject motion, duration, pacing, and visual style
- Constrain identity drift, invented geometry, text artifacts, and background morphing
- Deliver prompts, keyframe lists, shot lists, cover guidance, and launch copy

## 适用场景 / Use cases

- 作品集与概念验证 / Portfolio pieces and proofs of concept
- 产品配置器与交互展示 / Product configurators and interactive showcases
- 科学或机械可视化原型 / Science or mechanical visualization prototypes
- 营销视觉、预告片与社交短视频 / Marketing visuals, teasers, and social clips
- 先用视频验证概念，再开发 3D 应用 / Video-first validation before building a 3D app

## 安装 / Installation

使用 Skills CLI：

Using the Skills CLI:

```bash
npx skills add 349840432m-dev/ai-3d-video-prototype-skill -g -y
```

也可以手动克隆到 Codex Skills 目录：

Or clone it manually into the Codex skills directory:

```bash
git clone https://github.com/349840432m-dev/ai-3d-video-prototype-skill.git \
  ~/.codex/skills/ai-3d-interactive-app
```

安装后重启 Codex，使其重新扫描本地 Skills。

Restart Codex after installation so it can rescan local skills.

## 使用 / Usage

直接描述要制作的概念、参考图和目标交付形式，并点名 Skill：

Describe the concept, reference image, and target output, then invoke the skill:

```text
Use $ai-3d-interactive-app to turn this product concept into an interactive
Hunyuan3D prototype with orbit controls, annotations, and GLB export.
```

```text
Use $ai-3d-interactive-app to create a Seedance 2.0 product hero video from
this first frame. Use a slow orbit reveal and keep the product geometry stable.
```

中文示例：

```text
使用 $ai-3d-interactive-app，把这张概念图做成可旋转、可标注、支持截图的
Hunyuan3D 交互式产品原型。
```

## 工作流 / Workflow

1. 锁定概念、交付路径和核心交互或镜头。
2. 生成主视觉，以及所需的多视图或视频关键帧。
3. 选择 Hunyuan3D、Seedance 2.0，或同时使用两者。
4. 构建 3D Web 原型或编写视频运动提示词。
5. 检查几何一致性、加载状态、交互、响应式表现或时间稳定性。
6. 按需准备演示录屏、镜头表、封面和工具链说明。

1. Lock the concept, delivery path, and core interaction or shot.
2. Generate the hero visual and any required multi-view or video keyframes.
3. Choose Hunyuan3D, Seedance 2.0, or both.
4. Build the 3D web prototype or write the video motion prompt.
5. Verify geometry, loading, interaction, responsiveness, or temporal stability.
6. Prepare recordings, shot lists, covers, and toolchain disclosure when needed.

## Hunyuan3D 本地依赖 / Local dependencies

参考 Skill 中的 Hunyuan3D 2.1 基线：

- Python 3.10
- PyTorch 2.5.1 + CUDA 12.4
- `torchvision==0.20.1`
- `torchaudio==2.5.1`
- Shape 生成约需 10 GB VRAM
- Texture 生成约需 21 GB VRAM
- Shape + Texture 同时运行约需 29 GB VRAM

完整的编译依赖、纹理管线和 Real-ESRGAN checkpoint 说明见 [`SKILL.md`](./SKILL.md)。

See [`SKILL.md`](./SKILL.md) for build dependencies, the texture pipeline, and the Real-ESRGAN checkpoint.

## 仓库结构 / Repository structure

```text
.
├── SKILL.md           # 完整工作流、决策规则与验收要求
└── agents/
    └── openai.yaml    # Skill 的显示名称、简介与默认提示词
```

## 边界 / Limitations

- AI 生成的生物、医学、分子、机械或工程几何体不能默认视为准确。
- 正式教育、医疗、工程和生产资产必须使用权威资料或专业流程复核。
- 高面数模型可能导致浏览器性能问题，加载前应减面或重新拓扑。
- Seedance 适合视频交付；需要可复用、可检查几何体时应优先选择 3D 路径。

- AI-generated biological, medical, molecular, mechanical, or engineering geometry is not accurate by default.
- Formal education, medical, engineering, and production assets require authoritative validation.
- High-poly meshes may overwhelm browser rendering and should be decimated or retopologized.
- Seedance is suited to video delivery; choose the 3D path when reusable geometry matters.

## License

本仓库暂未包含许可证文件。使用或分发前，请先确认项目及所调用模型、资产和依赖的授权条款。

This repository does not currently include a license file. Confirm the terms of the project and all models, assets, and dependencies before use or redistribution.
