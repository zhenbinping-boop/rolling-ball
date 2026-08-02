---
name: gsap
description: >
  Best practices and guidance for GSAP 3 (GreenSock Animation Platform). Use whenever the user asks to create, modify, add, or optimize web animations, page transitions, scroll animations, micro-interactions, or interactive visual effects using GSAP, ScrollTrigger, Flip, or TextPlugin.
argument-hint: "[basic|timeline|scrolltrigger]"
license: MIT
---

# GSAP (GreenSock Animation Platform) Skill

Expert guide for creating high-performance, modern, dynamic web animations using **GSAP 3**.

## 1. CDN Script Tags for HTML Projects

Include GSAP via CDNJS when working in Vanilla HTML/CSS/JS:

```html
<!-- GSAP Core -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>

<!-- GSAP Plugins (Optional as needed) -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/TextPlugin.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/Flip.min.js"></script>
```

## 2. Core API Usage & Best Practices

### Tweens
- `gsap.to(target, { duration: 1, x: 100, opacity: 1, ease: "power2.out" })`
- `gsap.from(target, { duration: 1, y: 50, opacity: 0, ease: "back.out(1.7)" })`
- `gsap.fromTo(target, { opacity: 0, scale: 0.8 }, { opacity: 1, scale: 1, duration: 0.8 })`
- `gsap.set(target, { x: 0, y: 0 })` (Instant state set)

### Transform Properties (Performant)
Always animate GPU-accelerated transform properties instead of layout properties (`top`, `left`, `width`, `height`):
- `x` / `y` (instead of `left` / `top`)
- `scale` / `scaleX` / `scaleY`
- `rotation` / `rotationX` / `rotationY`
- `opacity`
- `transformOrigin`: e.g., `"50% 50%"`

### Timelines (Chained Animations)
```javascript
const tl = gsap.timeline({ defaults: { duration: 0.8, ease: "power2.out" } });

tl.from(".title", { y: -30, opacity: 0 })
  .from(".subtitle", { y: 20, opacity: 0 }, "-=0.4") // Overlap by 0.4s
  .from(".card", { scale: 0.9, opacity: 0, stagger: 0.1 }, "-=0.2");
```

### Staggering Multiple Elements
```javascript
gsap.from(".card", {
  duration: 0.6,
  y: 40,
  opacity: 0,
  stagger: {
    amount: 0.5, // total time spread across elements
    from: "start", // "center", "end", "edges", "random"
    ease: "power1.inOut"
  }
});
```

### ScrollTrigger Animations
```javascript
gsap.registerPlugin(ScrollTrigger);

gsap.from(".feature-box", {
  scrollTrigger: {
    trigger: ".feature-box",
    start: "top 80%", // when top of trigger hits 80% viewport
    end: "top 30%",
    scrub: true, // smooth scrolling sync
    toggleActions: "play none none reverse"
  },
  y: 50,
  opacity: 0,
  duration: 1
});
```

## 3. Eases Quick Reference
- `power1.out`, `power2.out`, `power3.out`, `power4.out` (Smooth decelerate)
- `back.out(1.7)` (Overshoot bounce-back)
- `elastic.out(1, 0.3)` (Springy elastic response)
- `bounce.out` (Physical bounce effect)
- `sine.inOut` (Gentle wave motion)

## 4. Key Rules & Performance
1. **GPU Acceleration**: Animate `x`, `y`, `scale`, `rotation`, and `opacity`.
2. **Avoid Layout Thrashing**: Do not animate `width`, `height`, `margin`, `padding`, or `top`/`left` unless necessary (or use `Flip` plugin).
3. **Register Plugins**: Always call `gsap.registerPlugin(ScrollTrigger, TextPlugin)` before using plugins.
4. **Cleanup**: In Single Page Applications (React/Vue), kill timelines and ScrollTriggers on component unmount (`ctx.revert()`).
