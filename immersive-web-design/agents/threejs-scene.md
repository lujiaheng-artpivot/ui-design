# Three.js 场景 Agent

## 骨架

```js
const scene=new THREE.Scene(), camera=new THREE.PerspectiveCamera(60,w/h,.1,100);
const renderer=new THREE.WebGLRenderer({alpha:true,antialias:true});
renderer.setPixelRatio(Math.min(devicePixelRatio,2));
renderer.setSize(w,h); container.appendChild(renderer.domElement);
```

## 光照方案

**产品三点布光**：主DirectionalLight(1) + 补DirectionalLight(0.4,偏色) + 背PointLight(0.3) + AmbientLight(0.4)

**氛围背景**：AmbientLight(0.3) + 2个PointLight(不同色相,衰减距离15-20)

## 几何体选择

| 效果 | 几何体 | 参数提示 |
|------|--------|---------|
| 科技球 | IcosahedronGeometry | (r, detail:1-3) |
| 流体环 | TorusGeometry | (R,r, 32+, 64+) |
| 抽象结 | TorusKnotGeometry | (R,r, 100, 16) |
| 粒子云 | BufferGeometry+Points | Float32Array position |
| 波浪面 | PlaneGeometry | (w,h, 64+,64+) + vertex位移 |

## 材质速查

- wireframe科技：`{wireframe:true, roughness:.3, metalness:.8}`
- 发光：`{emissive:0xa855f7, emissiveIntensity:.5, roughness:.2, metalness:.9}`
- 粒子：`PointsMaterial({size:.05, transparent:true, blending:AdditiveBlending, depthWrite:false})`

## 鼠标交互（缓动跟随）

```js
let mx=0,my=0; document.addEventListener('mousemove',e=>{mx=(e.clientX/w-.5)*2;my=(e.clientY/h-.5)*2});
// animate内：target.x+=(mx*.5-target.x)*.05; camera.position.x=target.x; camera.lookAt(scene.position);
```

## 粒子系统

```js
const pos=new Float32Array(count*3);
for(let i=0;i<count*3;i++) pos[i]=(Math.random()-.5)*10;
const geo=new THREE.BufferGeometry(); geo.setAttribute('position',new THREE.BufferAttribute(pos,3));
const pts=new THREE.Points(geo, pointsMaterial); scene.add(pts);
// animate: pts.rotation.y+=.0005;
```

## 与GSAP集成

```js
gsap.to(mesh.rotation,{y:Math.PI*2,duration:5,ease:'none',repeat:-1});
gsap.to(camera.position,{z:2,scrollTrigger:{trigger:'.s2',start:'top bottom',end:'top top',scrub:1}});
```

## 必须：dispose清理

遍历scene.traverse，dispose所有geometry+material+texture，renderer.dispose()。
