# 手账 · Techo

一个为喜欢手账的女生打造的数字拼贴日记 App。记录每一次出门值得被留下的瞬间——旅行、展览、citywalk、演出，都可以。

**Live demo:** [部署后填入 URL]

---

## 核心功能

- 导入手机照片 → 套索裁剪成贴纸素材 → 拖放到画布上排版
- 钢笔 / 荧光笔 / 马克笔手写批注
- 按「旅行/出门」分组，每次出门可有多页手账
- 页面缩略图自动生成，退出即保存

## 技术

单文件 HTML + Vanilla JS，数据存于 IndexedDB，无需服务器，可作为 PWA 添加到 iPad 主屏。

## 本地运行

直接用浏览器打开 `index.html` 即可，无需安装任何依赖。

## 文件结构

```
index.html          # App 主体（当前版本）
docs/
  PRD.md            # 产品需求文档
  ARCHITECTURE.md   # 技术架构
  TODO.md           # 待办 & 迭代计划
archive/
  techo_v1~v13.html # 历史版本备份
```
