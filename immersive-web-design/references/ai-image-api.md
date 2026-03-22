# AI图像生成集成

## NanoBanana Pro
用途：概念图、产品渲染、场景背景。集成：生成→下载WebP→嵌入项目 或 后端API代理。

提示词结构：`[主体], [风格], [光影], [色调], [技术参数]`

## 即梦（Jimeng）
用途：中文语境、国风视觉。提示词用中文自然语言。

## 嵌入最佳实践
- 格式优先：AVIF > WebP > JPEG
- Hero背景<400KB，辅助图<150KB
- 首屏外一律 `loading="lazy"`
- 占位：CSS渐变或低质量模糊图
- 必须有描述性alt文本；纯装饰用 `alt=""`
- 响应式：`srcset` + `sizes`

```html
<picture>
  <source srcset="bg.avif" type="image/avif">
  <source srcset="bg.webp" type="image/webp">
  <img src="bg.jpg" alt="[描述]" loading="lazy">
</picture>
```
