---
name: ai-3d-interactive-app
description: Build AI-assisted 3D or video prototypes from visual concepts. Use when the user wants to turn generated multi-view images into either an interactive 3D browser asset via Hunyuan3D, React/Vite, Three.js, React Three Fiber, and Drei, or a short cinematic/product video via Seedance 2.0. Also use for viral 3D demos, science visualizations, product configurators, portfolio prototypes, and video-first concept showcases.
---

# AI 3D Or Video Prototype

Use this skill to turn an idea or reference into either a reusable interactive 3D asset/app or a video-first concept showcase.

## Core Workflow

1. Lock the concept.
   - Identify the domain: science visualization, mechanical object, architecture, product, consumer item, or abstract explorable scene.
   - Define the final output path: `3D shape/app`, `Seedance 2.0 video`, or both.
   - For 3D, define the interaction loop in one sentence: rotate, inspect, explode, zoom, annotate, configure, compare, or generate.
   - For video, define the shot in one sentence: orbit reveal, transformation, product hero, explainer sequence, microscopic journey, assembly, or cinematic teaser.
   - If no visual exists, create or request a concept image before writing much code.

2. Generate source images.
   - First generate a clean hero/concept image that fixes the subject, style, materials, and intended mood.
   - For 3D, also generate consistent `front`, `back`, and `left` views when the object has meaningful unseen sides.
   - For video, generate a first frame and optionally an end frame or keyframe set for Seedance 2.0.
   - Keep scale, lighting, pose, silhouette, materials, and camera distance consistent across related images.
   - Use transparent, white, or simple solid backgrounds for 3D conversion; use richer staging only for video frames.

3. Choose the downstream path.
   - Path A: Hunyuan3D to create reusable 3D shape/assets.
   - Path B: Seedance 2.0 to create a short video directly from generated image frames.
   - Use both when the user wants an interactive app and a marketing/launch video from the same concept.

## Path A: Hunyuan3D To 3D Shape

1. Create 3D assets with Hunyuan3D.
   - Prefer browser-ready `GLB`.
   - Default to Hunyuan3D for local, cost-controlled image-to-3D generation when the environment and license fit.
   - Prefer Hunyuan3D multi-view shape generation when multiple view images are available; use single-image generation only for simple or symmetrical objects.
   - Use the shape-only path when VRAM is limited; use shape + texture/PBR only when enough GPU memory is available.
   - If no generator is available, use placeholder GLB primitives or procedural geometry so the app remains runnable.

2. Convert the concept into a web app plan.
   - Default stack: `React + Vite + Three.js + React Three Fiber + Drei`.
   - Add `Framer Motion` only for panels, transitions, or polished UI motion.
   - Keep the first version narrow: one main 3D object, one control surface, and one clear export/share action.

3. Build the interaction.
   - Use `Canvas`, `OrbitControls`, `Environment`, `Stage`, `Html`, `Bounds`, and `ContactShadows` from Drei where useful.
   - Add inspectable annotations, selection states, screenshots, and GLB export/import only when they serve the concept.
   - Keep model loading resilient with `Suspense`, visible loading states, and fallback geometry.

4. Verify the prototype.
   - Run the local dev server.
   - Open the app in a browser and check that the canvas is nonblank, framed, animated or interactive, and responsive on desktop and mobile.
   - Check asset size and polygon count if multiple GLBs are used.

5. Prepare launch material when requested.
   - Capture a short screen recording or provide a shot list.
   - Summarize the stack openly: concept image model, coding model/tool, 3D asset generator, and web stack.
   - Keep the post format simple: screen recording, one-line result, disclosed toolchain, and a link or repo path.

## Path B: Seedance 2.0 To Video

Use this path when the user mainly needs a publishable clip rather than a reusable 3D asset.

1. Prepare video inputs.
   - Use a strong first frame; add an end frame when the motion needs a precise transformation or reveal.
   - For product/object videos, keep the subject readable and avoid hiding key geometry with dramatic shadows.
   - For character or creature videos, keep identity, clothing, proportions, and markings stable across keyframes.

2. Write the Seedance 2.0 motion prompt.
   - Specify camera motion: slow orbit, dolly in, macro push-in, turntable, vertical reveal, handheld, crane, or zoom through.
   - Specify subject motion only when needed: assemble, unfold, glow, pulse, transform, open, rotate, breathe, or demonstrate.
   - Specify duration, pacing, visual style, and what must remain unchanged.
   - Add negative constraints for common failures: no extra parts, no identity drift, no background morphing, no text artifacts, no sudden cuts unless intended.

3. Review and iterate.
   - Check temporal stability, geometry consistency, camera path, motion clarity, and whether the first/end frames are respected.
   - If the model invents wrong unseen geometry, generate clearer side/back references or use Path A instead.
   - If only the clip matters, do not spend time building a 3D mesh.

4. Deliver video support assets when requested.
   - Provide the final prompt, keyframe list, shot list, cover image, caption copy, and disclosed toolchain.

## Tool Selection

- Choose Hunyuan3D when cost, local processing, or data control matters more than hosted convenience.
- Choose Seedance 2.0 when the target is a polished short video, social post, teaser, or motion concept and no interactive asset is needed.
- Choose both when the 3D app needs a launch trailer or when the video validates demand before building the 3D app.
- Choose a hosted fallback only when the user lacks a usable GPU or needs quick remote output.
- Choose placeholders first when the user mainly needs frontend interaction, layout, or proof of concept.
- Do not present AI-generated biological, molecular, medical, or engineering geometry as accurate unless it has been validated against authoritative sources.

## Hunyuan3D Local Dependencies

Baseline from the official Hunyuan3D-2.1 setup:

- Python 3.10
- PyTorch 2.5.1 with CUDA 12.4 for NVIDIA GPU workflows
- `torchvision==0.20.1` and `torchaudio==2.5.1`
- repository `requirements.txt`
- build tools needed for editable/custom rasterizer installs
- texture/PBR path: compile `hy3dpaint/custom_rasterizer` and `hy3dpaint/DifferentiableRenderer`
- Real-ESRGAN checkpoint at `hy3dpaint/ckpt/RealESRGAN_x4plus.pth`

VRAM planning:

- Shape generation: about 10 GB VRAM
- Texture generation: about 21 GB VRAM
- Shape + texture together: about 29 GB VRAM

Use generated `GLB` assets in the web app. If the mesh is too heavy, decimate or retopologize before loading multiple models in the browser.

## Multi-View Image Generation Rules

When Codex is responsible for creating the source images:

- Generate an orthographic-style design sheet when possible: front, back, left side, and optionally right side or top.
- Avoid dramatic perspective, cropped edges, busy backgrounds, shadows hiding geometry, or pose changes between views.
- Preserve distinctive markings across views so Hunyuan3D can infer continuity.
- For characters, use a neutral A-pose or straight standing pose unless the final asset specifically needs another posture.
- For products or props, align the object to the same vertical axis and keep proportions unchanged.
- If a multi-view generator/API accepts only three views, provide `front`, `back`, and `left` first.

## Implementation Heuristics

- Optimize 3D assets before adding more UI. High-poly image-to-3D output can overwhelm browser rendering.
- Use low-poly or decimated variants for multi-object scenes.
- Keep UI dense and tool-like for production/configurator demos; use more expressive motion for portfolio or viral demos.
- Make the first screen the usable 3D experience, not a marketing landing page.
- Avoid blocking the project on paid APIs. Stub the asset pipeline and document the environment variable if keys are missing.

## Starter Prompt Shape

For a 3D app, ask the model or coding agent for:

```text
Build a React + Vite + React Three Fiber + Drei interactive 3D web app from this concept image/reference. The main object should load as GLB when available, fall back to procedural geometry, include OrbitControls, annotations, a compact control panel, screenshot/export affordances, and responsive desktop/mobile framing.
```

For Seedance 2.0 video, shape the prompt like:

```text
Create a short cinematic video from this first frame and optional end frame. Keep the subject identity, proportions, materials, and markings consistent. Camera: [motion]. Subject motion: [motion]. Style: [visual style]. Duration: [seconds]. Avoid extra parts, text artifacts, identity drift, and sudden background changes.
```

## Suitability Check

Best fits:
- portfolio demos
- interactive prototypes
- visual explainers
- product configurators
- marketing visualizations
- short video showcases
- social launch clips

Use extra caution for:
- formal science education
- medical or biological accuracy
- production game assets
- commercial use with uncertain 3D model licenses
