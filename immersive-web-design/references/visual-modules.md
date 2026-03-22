# 视觉模块代码模板

> 目录——仅阅读当前任务需要的模块，不要全部加载到思考中。

- §1 光柱动画（CSS）
- §2 Canvas粒子
- §3 Three.js悬浮几何体
- §4 GSAP入场编排
- §5 霓虹发光系统
- §6 数据看板卡片
- §7 流光按钮
- §8 reduced-motion方案

---

## §1 光柱动画

```css
.light-pillar {
  position:absolute; top:-20%; bottom:-20%;
  width:var(--w,200px);
  background:linear-gradient(180deg,transparent,var(--c,rgba(168,85,247,.1)) 50%,transparent);
  filter:blur(var(--blur,50px));
  transform:rotate(var(--angle,-15deg));
  animation:pillar var(--speed,12s) ease-in-out infinite alternate;
  mix-blend-mode:screen;
}
@keyframes pillar {
  0%{transform:rotate(var(--angle)) translateX(-30%);opacity:.5}
  100%{transform:rotate(var(--angle)) translateX(30%);opacity:1}
}
```

用法：4-5个 `.light-pillar` 叠加，各设不同 `--w/--c/--angle/--speed/--blur`。

---

## §2 Canvas粒子

核心逻辑：创建N个粒子对象(x,y,vx,vy,r)，每帧更新位置+边界反弹+鼠标吸引，粒子间距<阈值时画连线。

```js
// 关键参数
count: 80, lineDistance: 120, speed: 0.5
// 鼠标吸引：dist<150时 p.x += dx*0.01
// 连线透明度：0.3*(1 - dist/lineDistance)
```

---

## §3 Three.js背景

```js
// 基础骨架
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(60, w/h, 0.1, 100);
const renderer = new THREE.WebGLRenderer({alpha:true, antialias:true});
renderer.setPixelRatio(Math.min(devicePixelRatio, 2));
// 几何体选择：IcosahedronGeometry / TorusGeometry / TorusKnotGeometry
// 材质：MeshStandardMaterial({wireframe:true, roughness:.3, metalness:.8})
// 鼠标：缓动跟随 target.x += (mouseX*0.5 - target.x)*0.05
// 必须：resize监听 + dispose()清理
```

---

## §4 GSAP入场

```js
gsap.set('.tag,.title,.desc,.buttons,.card', {opacity:0, y:40});
const tl = gsap.timeline({defaults:{duration:.8, ease:'expo.out'}, delay:.3});
tl.to('.tag',{opacity:1,y:0})
  .to('.title',{opacity:1,y:0},'-=-.5')
  .to('.desc',{opacity:1,y:0},'-=.5')
  .to('.buttons',{opacity:1,y:0},'-=.4')
  .to('.card',{opacity:1,y:0,duration:1.1},'-=.3');
```

---

## §5 霓虹发光

```css
.neon{box-shadow:0 0 5px rgba(168,85,247,.5),0 0 15px rgba(168,85,247,.25),0 0 35px rgba(168,85,247,.1)}
.neon-text{text-shadow:0 0 7px rgba(168,85,247,.8),0 0 20px rgba(168,85,247,.4)}
/* 脉冲 */
@keyframes neon-pulse{
  0%{box-shadow:0 0 5px rgba(168,85,247,.4),0 0 15px rgba(168,85,247,.2)}
  100%{box-shadow:0 0 12px rgba(168,85,247,.7),0 0 35px rgba(168,85,247,.35)}
}
```

---

## §6 数据看板卡片

要素：玻璃态背景(`rgba(255,255,255,.04)`) + `backdrop-filter:blur(20px)` + 斜纹理(`repeating-linear-gradient(-45deg,...)`) + 顶部渐变线(`linear-gradient(90deg,transparent,accent,transparent)`)。

数字跳动：用 `requestAnimationFrame` + ease-out-expo 插值 + `toLocaleString` 格式化。

---

## §7 流光按钮

```css
.btn-glow{position:relative;overflow:hidden;background:linear-gradient(135deg,#a855f7,#3b82f6);border-radius:12px}
.btn-glow::after{
  content:'';position:absolute;top:-50%;left:-50%;width:200%;height:200%;
  background:linear-gradient(90deg,transparent,rgba(255,255,255,.15),transparent);
  transform:rotate(45deg) translateX(-100%);
  animation:shimmer 3.5s ease-in-out infinite;
}
@keyframes shimmer{0%{transform:rotate(45deg) translateX(-100%)}100%{transform:rotate(45deg) translateX(100%)}}
```

---

## §8 prefers-reduced-motion

```css
@media(prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.01ms!important;transition-duration:.01ms!important}
  .light-pillars,.particles-canvas,.three-bg{display:none!important}
  .tag,.title,.desc,.buttons,.card{opacity:1!important;transform:none!important}
}
```
