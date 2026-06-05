# MOJi 全产品说明书

MOJi 产品矩阵内部说明手册，供新人 / 实习生 / 跨部门同事了解产品功能。

---

## 文件结构

```
仓库根目录/
├── moji_manual_v28.html      # 主文件（入口）
├── manual_style.css           # 样式文件
├── images/                    # 截图文件夹（按产品分子目录）
│   ├── dict/                  # MOJi辞书
│   ├── read/                  # MOJi阅读
│   ├── kana/                  # MOJiKana
│   ├── test/                  # MOJiTest
│   ├── kaiwa/                 # MOJi会话
│   ├── school/                # MOJi小课堂
│   └── kori/                  # Kori辞书（已完成）
└── README.md                  # 本说明
```

部署方式：把整个根目录上传到静态服务器（GitHub Pages / 公司服务器都行），入口 `moji_manual_v28.html`。

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
│ 项目3   说明文字...                  │
├─────────────────────────────────────┤
│ [图1] [图2] [图3] →（多图横向滚动）  │
└─────────────────────────────────────┘
```

- 文字部分**全宽展开**，阅读优先
- 截图作为**底部图条**横向排列，宽度 110px
- 多图溢出时自动出现横向滚动条，右侧渐变蒙层提示"还能继续看"
- 点击任意缩略图弹窗放大原图

---

## 截图命名规范

格式：`images/{产品}/{产品}-{功能}-{序号}.{png|jpg}`

### 产品前缀（同时也是子目录名）

| 产品 | 前缀 / 文件夹 |
|---|---|
| MOJi辞书 | `dict` |
| MOJi阅读 | `read` |
| MOJiKana | `kana` |
| MOJiTest | `test` |
| MOJi会话 | `kaiwa` |
| MOJi小课堂 | `school` |
| Kori辞书 | `kori` |

### 功能命名

用拼音或英文短词，能识别即可。建议参考 HTML 里现有的 `id="block-XXX"` 部分。

### 示例

- `images/kori/kori-fanyi-1.png` → Kori翻译页第1张
- `images/kori/kori-fanyi-2.png` → Kori翻译页第2张
- `images/dict/dict-citiao-1.png` → 辞书词条详情第1张
- `images/read/read-yuedujihua-1.png` → 阅读计划功能第1张
- `images/kana/kana-game-1.png` → Kana游戏页第1张

### 约束

- 每个功能模块**1 张以上不设上限**（多图横向滚动自动处理）
- 截图建议保持**iPhone 全屏比例**（9:16 左右），视觉统一
- 文件名只用**小写字母、数字、连字符**（不要中文、空格、下划线）
- 文件名保留产品前缀（即使已经在子文件夹里）——防止文件挪动后撞名
- 后缀 `.png`（清晰度优先）或 `.jpg`（体积优先）都行
- 单张图建议 **200KB 以内**（实在不行 500KB 上限，再大加载会慢）

---

## 如何给一个功能加图

### 第 1 步：放截图

把截图按命名规范放进对应的产品子文件夹，比如辞书的图就放 `images/dict/`。

### 第 2 步：找到对应的功能模块

打开 `moji_manual_v28.html`，搜索 `id="block-XXX"`，比如要给词条详情加图就搜 `id="block-citiao"`。

### 第 3 步：改两处

**1. 在 class 里加 `has-thumbs`**：

原：
```html
<div class="module-block section-block" id="block-citiao">
```
改：
```html
<div class="module-block section-block has-thumbs" id="block-citiao">
```

**2. 用 `<div class="module-content">` 包住 module-header 和 module-body，并在闭合后插入 module-thumbs**：

最终结构应该是：
```html
<div class="module-block section-block has-thumbs" id="block-citiao">
  <div class="module-content">
    <div class="module-header">...原有内容...</div>
    <div class="module-body">...原有内容...</div>
  </div>
  <div class="module-thumbs">
    <img class="thumb" src="images/dict/dict-citiao-1.png" onclick="openModal(this.src)">
    <img class="thumb" src="images/dict/dict-citiao-2.png" onclick="openModal(this.src)">
  </div>
</div>
```

注意：`module-content` 这层包裹是必需的——它和 `module-thumbs` 形成上下两块，没这层会布局错乱。

---

## 如何换图

**最方便的做法**：保持文件名不变，直接用新图覆盖旧图。HTML 完全不用改，刷新就是新图。

例：想换 `kori-fanyi-1.png`，把新截图重命名成 `kori-fanyi-1.png` 丢进 `images/kori/` 替换即可。

---

## 如何加一个新功能模块

复制现有的 `<div class="module-block section-block">...</div>` 整个块，改：
- `id` 改成新的（如 `block-newfeature`）
- 模块标题（`module-title`）、副标题（`module-subtitle`）、入口路径（`path-chain`）
- 功能列表（`feature-list` 里的 `<li>`）
- 如果有图，按上面"如何给一个功能加图"的方式加缩略图块

记得同步更新左侧导航：在对应产品的 `nav-group` 里加一条 `<a class="nav-sub2">`。

---

## 想改样式（颜色 / 字体 / 间距）

样式都在 `manual_style.css` 里，改这一个文件即可。

常见改动位置：
- 顶部颜色变量（`:root` 里的 `--moji-green` 等）— 改品牌色
- `.module-block` / `.module-title` — 改模块卡片样式
- `.thumb` — 改缩略图大小（当前桌面 110px，移动端 90px）
- `.modal-overlay` / `.modal-image` — 改弹窗样式
- `.module-block.has-thumbs > .module-thumbs` — 改图条的内边距、滚动条样式

---

## 版本记录

- **v28**（2026.06）：CSS 外置、Kori 截图入库、点击缩略图弹大图、目录按产品分子文件夹、图条改至文字下方横向排列（110px）
- **v27**（2026.06）：新增 Kori辞书产品、日语人格测试、MOJi圈顶部入口
- v26 及更早：单文件结构，所有样式内嵌

---

## 部署给前端

把整个文件夹（含 `images/` 子目录）上传到服务器同一目录。**保持目录结构不变**，相对路径会自动生效，不需要改任何代码。

如果只更新了文字内容（没改图、没改样式），可以只上传 `moji_manual_v28.html` 一个文件。

---

## 给 AI 干活时怎么扔文件

未来想让 AI 帮你改某个功能、加新模块、调样式，按下表准备：

| 任务 | 扔什么文件 |
|---|---|
| 改文字内容 / 加新功能模块 | 只扔 `moji_manual_v28.html` |
| 改样式（颜色、间距、字体） | 只扔 `manual_style.css` |
| 改结构 + 样式 | HTML + CSS 都扔 |
| 加图后调位置 | HTML 即可，图片本身不用扔 |
| 让 AI 看图判断视觉效果 | 单独扔那张图 |

**关键**：图片本身一般不用扔。AI 看 HTML 里的 `<img src="..."` 就知道这里有图，能处理布局、样式、命名等所有非视觉任务。

---

## 小提示

- GitHub 不追踪空文件夹。`dict/`、`read/` 等空子目录会在你上传时被忽略，等丢入第一张图后自然出现，不影响使用。
- 如果浏览器打开页面后图不显示，多半是路径写错。F12 打开控制台看 Network 报错信息能定位到具体哪个文件 404。
- 多图模块鼠标放到图条上滚滚轮就能横向滑动；右侧渐变蒙层提示"还有更多"。
