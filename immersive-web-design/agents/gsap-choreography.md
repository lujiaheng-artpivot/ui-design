# GSAP 动画编排 Agent

## 入场模式

**瀑布式**（经典）：元素从上到下依次出现，每个重叠0.4-0.5s
```js
const tl=gsap.timeline({defaults:{ease:'expo.out',duration:.8},delay:.3});
tl.to('.tag',{opacity:1,y:0}).to('.title',{opacity:1,y:0},'-=.5')
  .to('.desc',{opacity:1,y:0},'-=.5').to('.btns',{opacity:1,y:0},'-=.4');
```

**分裂式**：左右两侧内容从两边滑入，重叠0.7s
**焦点爆炸**：核心元素scale 0.5→1，其他stagger从center向外扩散

## ScrollTrigger

```js
gsap.registerPlugin(ScrollTrigger);
// 固定+淡出
ScrollTrigger.create({trigger:'.hero',start:'top top',end:'+=100%',pin:true,
  onUpdate:s=>gsap.to('.hero-content',{opacity:1-s.progress,overwrite:true})});
// 滚动入场
gsap.utils.toArray('.section').forEach(s=>{
  gsap.from(s.querySelectorAll('.anim'),{scrollTrigger:{trigger:s,start:'top 80%',toggleActions:'play none none reverse'},
    opacity:0,y:60,stagger:.1,duration:.8,ease:'expo.out'});
});
```

## 微交互

- **悬停**：`gsap.to(btn,{scale:1.05,duration:.3,ease:'expo.out'})`
- **磁性按钮**：mousemove计算(x,y)偏移，`gsap.to(el,{x:x*.3,y:y*.3,duration:.3})`，mouseleave归零
- **数字计数**：`gsap.to(el,{innerText:target,duration:1.5,ease:'expo.out',snap:{innerText:1}})`

## Stagger

```js
stagger:.1                           // 基础
stagger:{amount:.5,from:'center'}    // 从中心扩散
stagger:{amount:.6,grid:[3,4],from:'center',axis:'both'}  // 网格
```

总时长<800ms，项目多时减小per-item delay。

## 缓动决策

果断→expo.out | 精致→quart.out | 戏剧→quint.out | 微回弹→back.out(1.2) | 循环→none

**禁止**：bounce、elastic。
