## 2026-06-30（六续）
### index.html + manual_style.css — 补全试卷库首页第四级导航 + 修正nav-sub3视觉层次
- 对照飞书原文档大纲（Aly提供截图），发现「试卷库首页」下还有4个子标题未还原：顶部筛选/学习记录/试卷列表/鼠标悬停（电脑端特有），其余模块层级核对无误
- 这4个子标题对应同一张试卷库首页截图，不新拆模块/不新加图，仅新增4条`nav-sub4`导航锚点，全部指向已有的`test-web-papers-home`区块
- 新增CSS class `.nav-sub4`（缩进72px，字号9.5px，颜色#cfcfcf，延续nav-sub→nav-sub2→nav-sub3→nav-sub4的缩进+变浅递进）
- 同时修正前一轮`.nav-sub3`的视觉问题：原先跟`.nav-sub2`同色（#999），只差12px缩进，肉眼难以分辨层级；改为56px缩进+更浅的`#b8b8b8`，层级区分更明显
- 已校验：div标签闭合平衡，34个scrollToBlock锚点与正文id全部一一对应

## 2026-06-30（五续）
### index.html — 电脑端模块按PDF三层分级拆分（9个合并模块 → 16个独立模块）
- 原电脑端导航是9条平铺nav-sub2，与PDF实际H2/H3标题层级不符，且与APP端三层结构（nav-sub2→nav-sub3）不一致
- 按PDF标题拆分以下5个H2模块为多个独立module-block，新增nav-sub3子锚点：
  - 搜题解析 → 主界面（test-web-search-main）/ 搜索结果与详情（test-web-search-detail）
  - 试卷库 → 试卷库首页（test-web-papers-home）/ 做题页（test-web-papers-exam）
  - 专项练习 → 文字词汇/语法/阅读Tab（test-web-zhuanxiang-tab）/ 听力Tab（test-web-zhuanxiang-listening）
  - 题目册 → 题目册首页（test-web-timuce-home）/ 智能分析（test-web-timuce-smart）/ AI问答（test-web-timuce-ai）
  - 备考资讯 → 资讯分类导航（test-web-zixun-nav）/ 文章详情页（test-web-zixun-article）/ 专栏列表页（test-web-zixun-column）
- 首页/看解析/小课堂/我的 4个模块PDF中无H3子标题，保持单一module-block不变
- 26张图片按拆分后的模块重新分配引用，无新增/删除图片
- 导航新增12条nav-sub3锚点，9个nav-sub2父级中5个指向其首个子模块，4个为叶子直接链接
- 已校验：17个block id（16模块+1nav容器）、26张图片引用、nav锚点与正文id全部一一对应，div标签闭合平衡

## 2026-06-30（四续）
### index.html — MOJiTest电脑端命名规范修正：pc → web
- 因该部分实为浏览器网页版（非PC客户端），全部命名前缀由`test-pc-`改为`test-web-`，共47处（含9个block id、9条nav锚点、26个图片引用）
- 图片路径同步改为`images/test/test-web/test-web-xxx.png`，对应Aly重命名后即将重新上传的文件夹与文件
- 已核验：div标签闭合数量平衡，nav中27个scrollToBlock锚点与正文block id全部一一对应
- ⚠️待办：Aly需将`images/test/test-pc/`下26张图重命名为`test-web-`前缀，文件夹改名为`test-web`后重新上传，旧的`test-pc`文件夹届时需删除

## 2026-06-30（三续）
### index.html + manual_style.css — 修复图片路径 + MOJiTest导航新增APP端/电脑端两级分组
- 修复图片路径：实际上传路径为`images/test/test-pc/`子文件夹，原引用`images/test/test-pc-xxx.png`漏了`test-pc/`一层，已批量改为`images/test/test-pc/test-pc-xxx.png`，26张图全部核验200可访问
- 导航重构：MOJiTest左侧导航新增「APP端」「电脑端」两个可折叠大分组（各自独立展开/收起，互不影响，可同时展开）
  - APP端分组下：对策/背词/考试/设置 降一级为nav-sub2，原有子项再降一级为nav-sub3（新增CSS class `.nav-sub3`，缩进52px）
  - 电脑端分组下：原9个子模块保持nav-sub2不变
  - 新增JS函数`toggleSubNav()`，独立于现有`toggleNav()`，不影响其他产品折叠逻辑
- 正文新增「APP端」分隔线（位于stats-row之后、「对策」分隔线之前），与已有的「电脑端」分隔线对应
- 已校验：nav中27个scrollToBlock锚点与正文block id全部一一对应，div标签闭合数量平衡

## 2026-06-30（再续）
### index.html + images/test/ — MOJiTest新增「电脑端」模块（依《MOJiTest产品说明书.pdf》页23-34）
- 新增9个功能模块：首页 / 搜题解析 / 试卷库 / 专项练习 / 看解析 / 题目册 / 备考资讯 / 小课堂 / 我的
- 插入位置：MOJiTest「购买中心」之后、「使用场景」之前；左侧导航test-nav同步新增「电脑端」分组及9条子链接
- 从PDF提取26张电脑端截图，以pdftoppm逐页栅格化核对内容后命名，统一前缀`test-pc-`：
  - test-pc-home-01（首页）
  - test-pc-search-01~06（搜题解析：主界面/文章Tab/智能分析/AI问答/筛选示例）
  - test-pc-papers-01~03（试卷库：首页/鼠标悬停/做题前置页）
  - test-pc-zhuanxiang-01~03 + test-pc-tingli-01（专项练习：入口/连续滚动/答题卡，听力Tab单列）
  - test-pc-jiexi-01~03（看解析：入口/智能分析/AI问答）
  - test-pc-timuce-01~03（题目册：首页/智能分析/AI问答）
  - test-pc-zixun-01~03（备考资讯：首页/文章详情页/专栏列表页）
  - test-pc-xiaoke-01（小课堂跳转页，⚠️属主站mojidict.com非test子域）
  - test-pc-wode-01~02（我的：个人资料/钱包）
- 原图分辨率过高的2张（3840×1907）等比压缩至1280/1480宽度，全部控制在300KB以内
- 导航锚点id、内容block id、图片引用三者已逐一核验一致

## 2026-06-30（续）
### index.html — MOJi辞書内容更新（依《MOJi辞書产品说明书.pdf》v8.40.0核对修正）
- 趣味游戏/测试：模块顺序调整为「消消乐 → 词汇水平测试 → 日语人格测试」
- 消消乐：入口补充为「背词首页→快捷功能区『玩游戏·消消乐』、MOJi圈→顶部功能区『玩游戏·消消乐』」（原仅背词首页一条）；图片补至2张
- 词汇水平测试：入口补充为「背词首页→快捷功能区『词汇量测试』、MOJi圈→顶部功能区『词汇水平·去评估』」（原仅背词首页一条）；图片补至3张
- 词条详情：顶部信息描述按PDF原文顺序修正，词源（仅外来语）调整至词类标签与JLPT等级标签之间
- 设置（我的）：功能设置文案由「搜索页定制」修正为「功能区定制 / 悬浮窗」，对齐PDF配图实际功能项

## 2026-06-30
### index.html + images/test/ — MOJiTest全量截图替换（以PDF为准重新提取命名）
- 从《MOJiTest产品说明书.pdf》提取全部68张嵌入截图，按模块重新命名，统一为.png格式
- 选择词书：`test-cishu-*` → `test-xuanze-01~03`
- 学习列表：`test-kuaisu-*` → `test-liebiao-01~06`
- 新学：`test-xinxue-01~06` → `test-xinxue-01~07`（新增第7张）
- 复习：`test-fuxi-01~05` → `test-fuxi-01~08`（新增06~08，对应进阶练习拼写挑战截图）
- 听词：`test-tingci-01~02` 内容修正（单词详情页+听词卡片模式，原误判为科学背词机制）
- 科学背词机制：`test-jizhi-*` → `test-kexue-01~04`（选择词书列表+背词帮助FAQ三张）
- 打卡日历：`test-daka-01~02` 内容修正（背词主页打卡周历+打卡日历详情页）
- 历年真题：`test-zhenti-01~03` → `test-linian-01~05`（新增2张）
- 答题界面：`test-dati-01~03`（含.jpeg）→ `test-dati-01~08`（全.png，新增04~08，含专项模式答题截图）
- 统计：`test-tongji-01~02`（含.jpeg）→ 全.png，内容修正为历年真题统计入口+折线图/正确率
- 题目册：`test-timuce-01~04`（含.jpeg）→ 全.png，内容修正为题目册列表+答案解析
- 购买中心：`test-pro-01~03` → `test-pro-01~05`（新增04~05）
- index.html 同步更新对应11处模块的`<img>`标签引用

## 2026-06-29
### index.html — MOJiTest内容更新（依PDF产品说明书）
- 复习模块：新增「进阶练习」条目——当日复习完成后顶部出现"拼写挑战"入口，可进行假名拼写与例句拼写
- 答题界面：新增「点击试卷宫格图进入试卷界面」独立说明
- 答题界面：重构内容层级——新增「真题模式」一级分区（含答题区/答题卡/标记/收藏/更多设置/阅读题高亮标记子说明）
- 答题界面：新增「专项模式」一级分区（点击蓝字"专项"进入）
- 答题界面：新增「答题模式的区别」说明（真题模式vs专项模式）
- 题目册：新增「右上角列表图标：切换题目列表视图」
- 购买中心：「单独购买·官方合作」更新为绿宝书词条分组+新增宵寒词条考研/宵寒模拟卷N1-N2；新增「右上角问号：使用帮助/恢复购买/联系客服」
- 个人中心：功能设置新增「标准日文字体（开关，仅安卓）」，位于主题与显示和发音设置之间

## 2026-06-26
### index.html + manual_style.css — 移动端适配 + 锚点滚动修复

**滚动定位修复（index.html）**
- `showSection` 不再主动 `scrollTo(0,0)`，避免与 `scrollToBlock` 竞争
- `scrollToBlock` 改用 `scrollTo(0,0)` 瞬间回顶 + 双 `requestAnimationFrame` 确保布局完成后再平滑滚动，彻底解决点击「日语人格测试」「消消乐」等跳转落点错误的问题

**移动端适配（index.html + manual_style.css）**
- index.html：新增移动端顶部 header（`.mobile-header`）含汉堡菜单按钮；新增 sidebar 遮罩层（`.sidebar-overlay`）；sidebar 加 `id="mainSidebar"` 供 JS 操作
- index.html：新增 `toggleMobileSidebar()` / `closeMobileSidebar()` 函数；点导航项时自动关闭抽屉
- manual_style.css：新增 `@media (max-width: 768px)` 响应式规则：sidebar 变为 80vw 宽抽屉式 overlay、主内容全宽、顶部 header sticky、各间距收窄适配手机屏幕

## 2026-06-26
### index.html — MOJi辞書内容修订（依PDF v8.40.0）
- 搜索页「搜索方式」：删除无依据的「语音输入」
- 词条详情「顶部信息」：修正为「词条条目 + 读音 + 声调 + 词类标签 + JLPT等级标签」，补「词源标注（仅外来语）」和「声优朗读设置（点击小头像进入）」
- 词条详情「释义」：补语法词条专项字段（中、日文使用语境及接续），「自定义」范围改为「释义与例句」
- 收藏主页「顶部快捷入口」：补「回顾」「笔记」两项
- 导航：「词汇水平测试/日语人格测试/消消乐」前新增「趣味游戏/测试」父级导航项（block-youxi）
- 内容区：在词汇水平测试前新增「趣味游戏/测试」content-divider，与导航结构对齐

## 2026-06-26
### index.html — MOJi阅读「阅读器」板块拆分重写
- 将原单一「阅读器」模块拆分为6个独立模块卡片：阅读器（书架主页）、本地文件导入、青空文库、浏览网页、短篇辅助阅读、拍照提取
- 各子模块新增独立id（read-bendiwenjian / read-qingkong / read-liulanwangye / read-duanpian / read-paizhao）、入口路径、功能描述
- 内容依据《MOJi阅读产品说明书》PDF及实机截图核对，补充两条导入路径、OCR编辑页、书签保存为书架卡片等细节
- 导航栏与页面id完全对齐：补充缺失的「常驻播放条」(read-bofang)、「设置」(read-shezhi)，修正顺序（阅读计划移至圈子后、句子解析改名、文章详情页改名），所有锚点经过验证无失效项
- 学习页图片从1张更新为4张（read-xuexi-1 ~ read-xuexi-4）
- 新增截图引用共27张（本地文件导入×6、青空文库×6、浏览网页×9、短篇辅助阅读×3、拍照提取×4）

## 2026-06-25
### index.html — MOJi辞書「背词」板块截图补全
- 为9个模块添加has-thumbs + module-thumbs截图引用：背词首页(×2)、更多计划(×3)、背词设置(×5)、新学(×3)、复习(×3)、听词(×2)、打卡日历(×3)、累计学词(×2)、词汇水平测试(×2)
- 学习列表、日语人格测试、消消乐暂无截图，保持纯文字版

## 2026-06-25
### index.html — MOJi辞書「背词」板块内容补全
- 新增12个模块卡片（原section仅有content-divider占位，内容全部缺失）：背词首页、更多计划、背词设置、学习列表、新学、复习、听词、打卡日历、累计学词、词汇水平测试、日语人格测试、消消乐
- 内容依据《MOJi辞書产品说明书》PDF p25-37，与现有导航id（block-beici-home-detail等）完全对齐
- 所有模块暂无截图（无has-thumbs），待截图上传后补充

## 2026-06-23
### index.html — MOJiTest更新
- 插入55张MOJiTest截图（images/test/），覆盖对策、专项试题、背词全流程、考试、设置、Pro购买共16个模块
- 新增独立block：学习列表（test-xuexilie）、新学（test-xinxue）、复习（test-fuxi），还原PDF原有层级
- 背词设置：还原每组词数为「滑动条5~100」、生成词序为「五十音序开关」、题型结构按PDF三层展开（选择题/回忆式/快速自测 → 官方/自选 → 各题型）
- 听词-进度与倍速：还原完整倍速档位（0.6x/0.8x/1.0x/1.2x/1.4x）
- 背词主页：新增「横幅」条目（近期主推活动快捷入口），移除非PDF来源的「词汇量测试」横幅条目
- 打卡日历-分享：还原为PDF原文（微信/朋友圈），移除HTML中多余的QQ/QQ空间
- 答题界面：还原标记（第二按钮）/收藏（第三按钮）顺序
- 导航新增：学习列表、新学、复习三个nav-sub2链接
- 所有test模块block添加has-thumbs + module-content + module-thumbs结构
