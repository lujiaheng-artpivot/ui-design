---
name: immersive-web-design
description: |
  沉浸式3D网页前端设计引擎——生成具有电影级视觉冲击力的Web前端界面。
  集成Three.js 3D场景、GSAP动画、Parallax.js视差、光柱/粒子动态背景、
  AI图像生成（NanoBanana Pro/即梦）调用。输出生产级HTML/CSS/JS或React JSX。
  强制触发词：3D网页、沉浸式设计、Three.js、GSAP动画、WebGL、parallax视差、
  光柱动画、粒子背景、流光效果、hero section、landing page、3D hero、
  动态背景、交互式网页、cinematic web、电影感网页、霓虹外发光、
  scroll animation、GSAP ScrollTrigger、Spline嵌入、shader、着色器、
  NanoBanana、即梦、AI生图嵌入、React Three Fiber
  当用户要求"炫酷网页""3D首页""带动画的landing page""沉浸式体验"时触发。
---

# 沉浸式3D网页设计引擎 v1.1

## 设计决策（编码前必答）

1. **场景**：Hero首屏 / 产品展示 / 数据看板 / 品牌故事 / 全屏体验？
2. **基调**（选一个极端方向）：深空科技 / 液态未来 / 极简奢华 / 赛博朋克 / 自然有机 / 编辑杂志
3. **技术栈**：纯HTML+JS / React JSX / Next.js？
4. **记忆点**：用户看完会记住什么？

## 技术选择矩阵

| 需求 | 方案 | 何时加载参考 |
|------|------|-------------|
| 3D场景 | Three.js r128 / Spline嵌入 | → 读 `agents/threejs-scene.md` |
| 动画编排 | GSAP 3.x + ScrollTrigger | → 读 `agents/gsap-choreography.md` |
| 自定义Shader | GLSL / ShaderMaterial | → 读 `agents/shader-effects.md` |
| 视差效果 | Parallax.js / CSS层叠 | → 读 `references/tech-stack.md` §Parallax |
| 背景系统 | 光柱CSS / Canvas粒子 / SVG | → 读 `references/visual-modules.md` 对应模块 |
| AI图像 | NanoBanana / 即梦 | → 读 `references/ai-image-api.md` |
| 配色/字体 | OKLCH体系 + 非通用字体 | → 读 `references/typography-palette.md` |

**重要**：不要一次加载所有 references/agents。根据任务只读需要的那一个。

## 反AI模板检查（编码前最后一关）

以下命中≥3条必须换方向：
- ❌ 紫蓝渐变 + 深黑背景（AI标配色）
- ❌ 到处毛玻璃 glassmorphism
- ❌ 相同圆角卡片网格无差异
- ❌ 渐变文字用于所有标题
- ❌ 居中一切 + 均匀间距
- ❌ Inter/Roboto/系统字体
- ❌ bounce/elastic缓动

如果用户明确要求命中项（如指定紫蓝色），通过排版/空间/纹理/动画差异化突破模板感。

## 代码规范（速查）

- **单文件输出**：HTML内联CSS+JS，CDN加载外部库
- **仅animate** `transform` + `opacity`（GPU加速）
- **必须响应** `prefers-reduced-motion`
- **Three.js必须有** `dispose()` 清理
- **缓动**：`expo.out` / `quart.out` / `quint.out`，禁止bounce/elastic
- **stagger**：50-100ms/item，总时长<800ms
- **r128注意**：无CapsuleGeometry，用Cylinder+Sphere替代

## CDN速查

```
Three.js r128:  cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js
GSAP 3.12:      cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js
ScrollTrigger:  cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js
Parallax.js:    cdnjs.cloudflare.com/ajax/libs/parallax/3.1.0/parallax.min.js
```

## 输出检查清单

- [ ] 有且仅有一个hero级视觉焦点
- [ ] 排版大小跳跃≥3:1
- [ ] 不超过3个色相 + 带色调的中性灰
- [ ] 每个动画回答"为什么动"
- [ ] 响应式覆盖 375px / 768px / 1200px
- [ ] `prefers-reduced-motion` + 键盘导航 + 对比度AA
- [ ] 通过反AI模板检查
