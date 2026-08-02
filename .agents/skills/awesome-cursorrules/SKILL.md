---
name: awesome-cursorrules
description: >
  Discover, search, fetch, and apply curated AI coding rulesets and .cursorrules configurations from github.com/patrickjs/awesome-cursorrules. Use whenever the user mentions "awesome-cursorrules", "cursorrules", "cursor rules", "apply cursor rules", or asks to fetch/install AI coding rules for a specific tech stack (Three.js, WebGL, React, Next.js, Python, TypeScript, Tailwind, Go, Rust, etc.).
argument-hint: "[stack-name|category]"
license: MIT
---

# Awesome Cursor Rules Skill

Curated collection and search tool for **awesome-cursorrules** (from [github.com/patrickjs/awesome-cursorrules](https://github.com/patrickjs/awesome-cursorrules)).

Use this skill to configure high-quality AI coding rules, coding style guidelines, and framework best practices for `.cursorrules`, `.cursor/rules/`, `AGENTS.md`, or AI system prompts.

## 1. Primary Rule Repositories & Sources

- **Official Repository**: [github.com/patrickjs/awesome-cursorrules](https://github.com/patrickjs/awesome-cursorrules)
- **Target File Locations**:
  - Root project file: `.cursorrules` or `AGENTS.md`
  - Cursor 0.45+ modular rules directory: `.cursor/rules/*.mdc`

## 2. Core Rule Catalogs by Technology Stack

### 🎮 Three.js / WebGL & Interactive 3D
- **Performance First**: Avoid allocating new `THREE.Vector3`, `THREE.Color`, or `THREE.Matrix4` instances inside the `requestAnimationFrame` loop. Preallocate and reuse working vectors.
- **Resource Lifecycle**: Always dispose of geometries (`geometry.dispose()`), materials (`material.dispose()`), and textures (`texture.dispose()`) when removing objects from the scene.
- **Object Pooling**: Use object pools (`acquire()` and `recycle()`) for high-frequency dynamic entities like particles, platforms, projectiles, and trail effects.
- **GPU Acceleration**: Prefer transform modifications (`position`, `rotation`, `scale`) over recalculating complex procedural mesh geometry every frame.

### ⚡ Modern Web & Vanilla HTML5 / CSS / JS
- **Design Tokens**: Standardize color palettes (HSL tailwind-style colors, dark mode defaults), typography from Google Fonts, and standard CSS variables.
- **Modern Web APIs**: Utilize native Web APIs (`AudioContext`, `BiquadFilterNode`, `IndexedDB`, `requestAnimationFrame`, `Fetch API`).
- **Responsive Layout**: Build liquid flex/grid layouts with CSS `clamp()`, `container queries`, and dynamic aspect ratios.

### 🔷 TypeScript & React / Next.js
- **Strict Typing**: Enforce strict TypeScript types without `any` assertions. Use generic constraints and exact interface definitions.
- **State Optimization**: Keep local state isolated; use `useCallback` and `useMemo` for heavy computations and sub-component rendering.
- **Component Design**: Keep component APIs shallow, single-responsibility, and reusable.

## 3. How to Apply Rules to a Project

1. **Detect Project Tech Stack**: Check workspace files (`package.json`, `.html`, `.ts`, `.py`, `.rs`).
2. **Generate / Update `.cursorrules`**:
   - Create or update `.cursorrules` in the root directory.
   - Or create modular rule files inside `.cursor/rules/` (e.g. `.cursor/rules/threejs.mdc`).
3. **Verify Compliance**: Ensure new code generated in the project follows the declared rulesets.
