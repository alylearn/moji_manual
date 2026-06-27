# MOJi 全产品说明书

MOJi 产品矩阵内部说明手册，供新人 / 实习生 / 跨部门同事了解产品功能。

---

## 本文档包含

- 文件结构与部署说明
- 截图命名规范与操作步骤
- 样式改动指引
- 版本管理规则
- AI 操作规范与提示词
- UI 维度参考
- 开发维度参考

---

## 文件结构

```
仓库根目录/
├── index.html                 # 主文件（入口，GitHub Pages部署用）
├── manual_style.css           # 样式文件
├── images/                    # 截图文件夹（按产品分子目录）
│   ├── dict/                  # MOJi辞書
│   ├── read/                  # MOJi阅读
│   ├── kana/                  # MOJiKana
│   ├── test/                  # MOJiTest
│   ├── kaiwa/                 # MOJi会话
│   ├── school/                # MOJi小课堂
│   └── kori/                  # Kori辞书
└── README.md                  # 本说明
```

部署方式：把整个根目录上传到静态服务器（GitHub Pages / 公司服务器都行），入口 `index.html`。

---

## 视觉布局说明

每个功能模块卡片的结构是：

```
┌─────────────────────────────────────┐
│ 🎯 功能标题                          │
│   功能副标题                         │
│   📍 入口：xxx                       │
├─────────────────────────────────────┤
│ 项目1   说明文字...                  │
│ 项目2   说明文字...                  │
├─────────────────────────────────────┤
│ [图1] [图2] [图3] →（多图横向滚动）  │
└─────────────────────────────────────┘
```

- 文字部分全宽展开，阅读优先
- 截图作为底部图条横向排列，宽度 110px
- 多图溢出时自动出现横向滚动条，右侧渐变蒙层提示还能继续看
- 点击任意缩略图弹窗放大原图

---

## 截图命名规范

格式：`images/{产品前缀}/{产品前缀}-{功能}-{序号}.png`

### 产品前缀

| 产品 | 前缀 / 文件夹 |
|---|---|
| MOJi辞書 | `dict` |
| MOJi阅读 | `read` |
| MOJiKana | `kana` |
| MOJiTest | `test` |
| MOJi会话 | `kaiwa` |
| MOJi小课堂 | `school` |
| Kori辞书 | `kori` |

### 示例

- `images/dict/dict-citiao-01.png` → 辞書词条详情第1张
- `images/read/read-yuedujihua-01.png` → 阅读计划功能第1张
- `images/kana/kana-game-01.png` → Kana游戏页第1张

### 约束

- 每个功能模块 1 张以上，不设上限
- 截图建议保持 iPhone 全屏比例（9:16），视觉统一
- 文件名只用小写字母、数字、连字符，不要中文、空格、下划线
- 后缀 `.png`（清晰度优先）或 `.jpg`（体积优先）都行
- 单张图建议 200KB 以内（上限 500KB）

---

## 如何给一个功能加图

### 第 1 步：放截图

按命名规范放进对应产品子文件夹，上传到 GitHub。

### 第 2 步：找到对应模块

打开 `index.html`，搜索 `id="block-XXX"`。

### 第 3 步：改两处

**1. 在 class 里加 `has-thumbs`：**

```html
<div class="module-block section-block has-thumbs" id="block-citiao">
```

**2. 用 `module-content` 包裹原有内容，并插入 `module-thumbs`：**

```html
<div class="module-block section-block has-thumbs" id="block-citiao">
  <div class="module-content">
    <div class="module-header">...原有内容...</div>
    <div class="module-body">...原有内容...</div>
  </div>
  <div class="module-thumbs">
    <img class="thumb" src="images/dict/dict-citiao-01.png" onclick="openModal(this.src)">
    <img class="thumb" src="images/dict/dict-citiao-02.png" onclick="openModal(this.src)">
  </div>
</div>
```

---

## 如何换图

保持文件名不变，直接用新图覆盖旧图上传到 GitHub。HTML 不用改，刷新即生效。

---

## 如何加一个新功能模块

复制现有的 `module-block` 整个块，修改：
- `id`（如 `block-newfeature`）
- 模块标题、副标题、入口路径、功能列表
- 如有图，按上方步骤加 `module-thumbs`

同步在左侧导航对应产品的 `nav-group` 里加一条 `<a class="nav-sub nav-sub2">`。

---

## 如何改样式

样式都在 `manual_style.css`，常见改动位置：

| 位置 | 作用 |
|---|---|
| `:root` 顶部变量 | 品牌色、文字色、背景色 |
| `.module-block` / `.module-title` | 卡片样式 |
| `.thumb` | 缩略图大小（桌面 110px） |
| `.modal-overlay` | 弹窗样式 |
| `@media (max-width: 768px)` | 移动端覆盖样式 |

---

## 版本记录

详见 `CHANGELOG.md`。

---

## 产品版本号同步规则

每个产品介绍段末尾标注「当前版本 vX.X.X」，和 App 实际版本保持一致。

| 产品 | 版本 |
|---|---|
| MOJi辞書 | v8.40.0 |
| MOJi阅读 | v3.4.5 |
| MOJiKana | v3.2.4 |
| MOJiTest | v5.11.0 |
| MOJi会话 | v3.8.3 |
| Kori辞书 | v2.0.6 |

更新时机：产品发版后功能有变动时同步更新；仅 bug 修复且说明书内容无变化可不更新。

---

## 给 AI 的操作规范

### 可直接复制的提示词

改动较小（1-3 处文字或图片）时，无需上传 PDF，直接说明改动内容即可。涉及新模块或大范围内容核对时再上传 PDF。

```
我在更新 moji_manual 产品手册（GitHub：alylearn/moji_manual），需要更新「[产品名]」模块。

请先执行以下步骤：
1. 读 README：https://raw.githubusercontent.com/alylearn/moji_manual/main/README.md
2. fetch 最新 index.html：https://raw.githubusercontent.com/alylearn/moji_manual/main/index.html
3. 如需查看已有图片列表：https://api.github.com/repos/alylearn/moji_manual/contents/images/[产品前缀]

我会上传产品说明书 PDF，请你：
1. 提取 PDF 截图，按命名规范重命名
2. 对比 PDF 文字和 HTML 现有内容，列出差异
3. 输出更新后的 index.html 和 CHANGELOG.md
```

将「[产品名]」和「[产品前缀]」替换为实际产品即可。

### AI 操作原则

- 永远从 GitHub raw URL 抓最新文件，不使用任何缓存版本
- 内容以 PDF 文字为准，截图用于补充验证；两者矛盾时以截图为准
- 不伪造内容：PDF 没有明确描述的功能不得自行添加
- 改完必须同步更新 CHANGELOG.md
- 导航 id 和内容 block id 必须一一对应，改完用 grep 验证锚点

---

## UI 维度

本网站为内容原型，UI 同事以此为参考出设计稿，无需直接修改代码。

### 产品色值参考

| 产品 | Class | 色值 |
|---|---|---|
| MOJi辞書 | `dict` | 红色系 `#E8003D` |
| MOJi阅读 | `read` | 绿色系 `#00B26B` |
| MOJiKana | `kana` | 蓝色系 `#3B82F6` |
| MOJiTest | `test` | 红色系 `#E8003D` |
| MOJi会话 | `kaiwa` | 橙色系 `#F07D00` |
| MOJi小课堂 | `school` | 红色系 `#E8003D` |
| Kori辞书 | `kori` | 绿色系 `#00B26B` |

### 移动端现状

当前已做基础移动端适配（断点 768px），待优化：
- 极窄屏（< 360px）部分长文字溢出
- 移动端整体视觉体验待设计稿确认后跟进

---

## 开发维度

### 定性说明

本网站为内容原型，内容结构和功能描述需保留，交互实现和视觉样式可按设计稿重写。

### 内容数据结构

每个功能模块对应一个 `module-block`：

| 字段 | HTML 对应 | 说明 |
|---|---|---|
| 模块 ID | `id="block-xxx"` | 导航锚点 |
| 图标 | `module-icon` | emoji |
| 标题 | `module-title` | 功能名 |
| 副标题 | `module-subtitle` | 一行标签描述 |
| 入口路径 | `path-chain > path-step` | 面包屑 |
| 功能列表 | `feature-list > li` | `feature-name` + `feature-desc` |
| 截图 | `module-thumbs > img` | 横向滚动图条 |

### 当前交互逻辑（可替换）

| 函数 | 作用 |
|---|---|
| `showSection(id)` | 切换产品（display none/block） |
| `toggleNav(groupId)` | 展开/收起左侧导航组 |
| `scrollToBlock(blockId)` | 跳转到指定模块（instant，无动画） |

### 部署

纯静态，无后端依赖。GitHub Pages 托管，入口 `index.html`，保持目录结构不变即可。
