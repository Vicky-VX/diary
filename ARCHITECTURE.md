# 技术架构 · 手账 App

_最后更新：2026-07-03 | 当前版本：v13_

---

## 整体架构

```
单文件 HTML（~90KB）
├── CSS（内联 <style>）
├── HTML 结构（4个视图）
└── JavaScript（内联 <script>）
    ├── 数据层：IndexedDB
    ├── 画布层：Canvas 2D API
    └── DOM 层：照片/文字元素
```

**无外部依赖，无构建工具，无服务器。**

---

## 数据模型

```
IndexedDB
  db: "techodb"  version: 2
  store: "trips"

trips[]
  id: string (Date.now())
  title: string
  pages[]
    id: string
    title: string
    dateStr: string
    dateTs: number
    bgColor: string        // 背景色 key（cream/white/kraft...）
    bgPat: string          // 纹理 key（none/lines/dots/grid）
    canvasData: string     // PNG base64（笔迹）
    thumbnail: string      // JPEG base64（缩略图，300px宽）
    trayPhotos: string[]   // 原图 base64（最多9张）
    piItems: PhotoItem[]   // 画布上的图片元素
    tiItems: TextItem[]    // 画布上的文字元素
    stashItems: StashItem[] // 素材库（裁剪贴纸）

PhotoItem { src, l, t, w, h, rot, zi, locked }
TextItem  { text, l, t, fs, clr, rot, zi }
StashItem { src, w, h }
```

---

## 视图结构（4个 div 切换 display）

| ID | 说明 |
|----|------|
| `#home-view` | 首页：手账本列表 + 统计 |
| `#trip-view` | 旅行内页：2列页面缩略图网格 |
| `#editor-view` | 编辑器：画布 + 素材库 + 工具栏 + 原图库 |
| `#analytics-ov` | 分析页（底部弹出 sheet） |

---

## 关键技术决策

| 决策 | 原因 |
|------|------|
| 单 HTML 文件 | 零部署复杂度，GitHub Pages 直接托管 |
| IndexedDB 而非 localStorage | 能存 base64 图片（localStorage 5MB 限制太小）|
| Canvas PNG 保存（非 JPEG）| JPEG 会把透明像素压成黑色，重载后变黑 |
| 图片/文字用 DOM 元素而非 Canvas | 支持独立选中、移动、缩放、旋转、图层控制 |
| 素材库（stash）始终可见 | 用户核心工作流：裁剪 → 存素材 → 拖到画布 |

---

## 部署

- 平台：GitHub Pages（静态托管）
- 入口文件：`index.html`（即 techo_v13.html 重命名）
- 历史备份：`archive/techo_v1~v13.html`
- 更新方式：本地修改 → 替换 GitHub 上的 index.html → 自动重新部署
