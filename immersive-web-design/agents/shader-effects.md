# Shader效果 Agent

## ShaderMaterial骨架

```js
new THREE.ShaderMaterial({
  vertexShader:`varying vec2 vUv;void main(){vUv=uv;gl_Position=projectionMatrix*modelViewMatrix*vec4(position,1.);}`,
  fragmentShader:`uniform float uTime;varying vec2 vUv;void main(){vec3 c=vec3(vUv,.5+.5*sin(uTime));gl_FragColor=vec4(c,1.);}`,
  uniforms:{uTime:{value:0}},
  transparent:true
});
// animate: material.uniforms.uTime.value=performance.now()*.001;
```

## 常用片段

**噪点函数**：`float rand(vec2 st){return fract(sin(dot(st,vec2(12.9898,78.233)))*43758.5453);}`

**波浪顶点位移**：`pos.z+=sin(pos.x*2.+uTime)*amp+sin(pos.y*3.+uTime*.7)*amp*.5;`

**圆形粒子**：`float d=length(gl_PointCoord-.5);if(d>.5)discard;float g=1.-smoothstep(0.,.5,d);`

## CSS替代（无需WebGL）

- **渐变漂移**：`background-size:400% 400%;animation:shift 15s ease infinite`
- **SVG滤镜光晕**：`<filter><feGaussianBlur stdDeviation="8"/><feMerge>...</feMerge></filter>`
- **噪点叠加**：`<feTurbulence baseFrequency=".65" numOctaves="3"/>` 作为svg背景 + `mix-blend-mode:overlay;opacity:.3`

## 性能

- 片段着色器避免分支和长循环
- 粒子数：桌面<5000，移动端<1000
- 能CSS实现的不要上WebGL
