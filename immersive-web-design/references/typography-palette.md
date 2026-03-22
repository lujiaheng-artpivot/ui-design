# 字体与配色速查

## 字体配对

**科技未来**：Space Grotesk(标题) + DM Sans(正文) + IBM Plex Mono(数据)
**编辑奢华**：Cormorant Garamond(标题) + Source Sans 3(正文)
**极简力量**：Outfit 全场景，字重差异(900/400/200)创造层级
**中文品牌**：Noto Serif SC(标题) + Noto Sans SC(正文) + Sora(英文) + JetBrains Mono(数据)

替代通用字体：Inter→Instrument Sans/Outfit | Roboto→Onest/Figtree | 标题→Space Grotesk/Sora/Fraunces

## 配色方案

**深空科技**：bg #0A0B0E / text #E8E8ED / accent #A855F7+#3B82F6 / gray带冷紫色调(oklch 0.01 chroma 280)
**液态未来**：bg #0D0D12 / accent #F472B6+#818CF8+#34D399
**暖光奢华**：bg #F5F0EB / text #1A1614 / accent #D4A574(金)+#2D3436(墨)
**赛博朋克**：bg #0A0A0F / accent #00FFC8+#FF0080+#FFE600 / 网格线rgba(0,255,200,.03)
**自然有机**：bg #FAFAF5 / accent #4A7C59(森绿)+#D4956A(陶土)+#6B8EA5(雾蓝)

## 排版层级

```css
--hero:  clamp(3rem,6vw+1rem,5.5rem);  /* 标题与正文≥3:1 */
--h1:    clamp(2rem,4vw+.5rem,3.5rem);
--body:  clamp(1rem,1vw+.5rem,1.125rem);
--small: clamp(.75rem,.8vw+.3rem,.875rem);
--leading-tight:1.1; --leading-normal:1.6; --leading-relaxed:1.8;
```

暗底降字重(350替400)。数字用`tabular-nums`。最大行宽`65ch`。用`clamp()`代替断点。
