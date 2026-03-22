# 技术栈速查

## CDN地址

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/parallax/3.1.0/parallax.min.js"></script>
```

## Three.js r128 要点

- `renderer.setPixelRatio(Math.min(devicePixelRatio, 2))` — 防高DPI过载
- **无 CapsuleGeometry**（r142才有），用 Cylinder+Sphere 替代
- OrbitControls 不在核心包——手写鼠标缓动跟随即可
- 常用几何体：`SphereGeometry` `TorusGeometry` `TorusKnotGeometry` `IcosahedronGeometry` `PlaneGeometry`
- 常用材质：`MeshStandardMaterial`(PBR) `MeshBasicMaterial`(无光) `PointsMaterial`(粒子) `ShaderMaterial`(自定义)
- **必须**：resize监听更新camera.aspect + renderer.setSize；组件卸载时dispose所有geometry/material

## GSAP缓动速查

| 用途 | 缓动 | 体感 |
|------|------|------|
| 默认推荐 | `expo.out` | 果断减速 |
| 精致 | `quart.out` | 平滑 |
| 戏剧 | `quint.out` | 略夸张 |
| 微回弹 | `back.out(1.2)` | 仅此可接受 |
| 禁用 | `bounce` `elastic` | 廉价过时 |

时长：反馈100-150ms / 状态200-300ms / 布局300-500ms / 入场500-800ms。退出=入场×0.75。

## Parallax.js

```html
<div id="scene">
  <div class="layer" data-depth="0.00"><!-- 静止 --></div>
  <div class="layer" data-depth="0.15"><!-- 慢 --></div>
  <div class="layer" data-depth="0.40"><!-- 中 --></div>
</div>
<script>new Parallax(document.getElementById('scene'),{relativeInput:true,frictionX:.1,frictionY:.1,scalarX:25,scalarY:15})</script>
```

depth参考：0=静止, 0.05-0.15=远景, 0.2-0.4=内容, 0.5-0.8=前景, 1.0=完全跟随。

## Spline嵌入

```html
<script type="module" src="https://unpkg.com/@splinetool/viewer@1.9.82/build/spline-viewer.js"></script>
<spline-viewer url="https://prod.spline.design/xxxxx/scene.splinecode"></spline-viewer>
```

## 字体加载

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=FONT:wght@400;600;700&display=swap" rel="stylesheet">
```

替代字体表见 `references/typography-palette.md`。
