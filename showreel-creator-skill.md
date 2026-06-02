---
name: showreel-creator
description: 把用户上传的 UI 界面截图（移动端 / PC 端 / 混合）打包成一张"杂志级 UI showreel 展示图"。当用户在上传 UI 图后说"帮我生成一套 showreel""帮我完成作品排版""生成全套作品集""生成 showreel 排版""做一张 showreel""创建一套 showreel""做一张作品集封面""做一张 UI 合集图""打包一下我的设计稿""portfolio 封面""做一张界面展示图"等任何"把多张界面排成一张展示图 / showreel"的同类同义请求时，立即使用本技能。技能内置一份经过反复打磨的中英双语创作 prompt（含中式美学语境与西方美学语境分支），覆盖画幅、配色、封面主视觉、氛围点缀、平铺展示、字体、留白等全部规则，最终直接调用可用的图像生成工具产出最终 showreel 图。
---

# Showreel Creator

把用户上传的一组 UI 截图（手机 App / Web / Desktop / 或混合）排成**一张高质量的作品集（showreel）展示图**。最终交付物是**一张图片**，不是网页、不是 PPT。

---

## 触发条件

用户上传自己的 UI 图后，说出以下任意一类（或同义）诉求即触发本技能：

- "帮我生成一套 showreel"
- "帮我完成作品排版"
- "生成全套作品集"
- "生成 showreel 排版"
- 以及任何"把多张界面排成一张展示图 / showreel / 作品集 / portfolio 封面 / UI 合集图"的同类同义说法。

如果用户没有附图，礼貌追问："请把 UI 截图（手机或 Web 都行，多张更好）发给我，我会拼成一张 showreel。"

---

## 使用流程

按这五步走，不要省略也不要颠倒。

### 1. 确认输入

- 列出用户上传的所有 UI 截图，分别数清"竖向（移动端）"和"横向（PC / Web）"各有几张。
- 不要凭空捏造界面。本技能只处理**用户上传的真实界面**。

### 2. 决定画幅

按多数派定：

| 输入主体 | 画幅 |
| --- | --- |
| 移动端为主（手机 App / 竖向截图） | **9:32 竖向** |
| PC 端为主（Web / Desktop 横向截图） | **9:16 竖向** |
| 数量打平 | 按用户偏好；不确定就用 9:16 |

把这个画幅写进最终 prompt 的第一句作为强约束。

### 3. 构造完整 prompt

把下方 `## Showreel Prompt（英文，交付给图像工具）` **整段**作为图像生成 prompt 的主体。开头加一句明确画幅，例如：

> Aspect ratio: **9:32 portrait** (mobile-end UIs dominate).

模板里的 7 条规则（基本原则 / 配色 / 封面主视觉 / 氛围点缀 / 平铺展示 / 字体 / 留白）都是经过打磨、互相咬合的——**不要删、不要简化、不要重写**。若用户对结果不满意，调整方向也是从这 7 条里挑一项做精修，而不是把模板砍短。

判断美学分支：

- 输入界面整体偏**中式美学**（水墨、禅意极简、新中式、国潮、赛博汉风、含中文为主的界面，或含朱砂红 / 松石绿 / 靛蓝 / 墨灰 / 烟灰 / 金等中式色）→ prompt 里关于"中式语境"的段落**保留并启用**（封面意象、装饰组件选择、中文字体系统、留白加权）。
- 输入界面整体偏**西方现代风**（纯英文、Material / iOS、Bento、Web3、SaaS dashboard 等）→ "中式语境"段落留在 prompt 里无害，模型会优先走西方分支，无需刻意删除。

### 4. 调用图像生成工具

- 用当前会话**实际可用的图像生成工具 / MCP**（例如 nano-banana、Gemini 2.5 Flash Image、其他已挂载的图像 MCP；不同环境名字不同，看可用工具列表）。若当前会话没挂任何图像工具，明确告诉用户："当前会话没有可用的图像生成工具，请先挂载一个支持 image-to-image / 多图参考的 MCP（例如 nano-banana），我再继续。"
- 把**用户上传的所有 UI 截图**作为参考图 / input images 一并传入——这是 image-to-image 任务，不是纯 text-to-image。
- 把第 3 步构造好的完整英文 prompt 作为 prompt 字段传入。
- 生成完把图返回给用户。

### 5. 迭代

- 用户不满意时，**先问清楚是哪一类问题**（配色不对？封面不够 hero？字体感觉？留白不够？某张界面没出现？），再有针对性地在 prompt 里加约束重跑。
- 不要默默改一堆地方再重跑——浪费时间且难定位。

---

## Showreel Prompt（英文，交付给图像工具）

> 下面这段从 "Please create…" 开始到末尾，就是要交给图像生成工具的完整 prompt。把第 2 步定好的画幅追加在最前面一句，然后整段发出去。中文原文见后一节，仅供对照，不要发给图像工具。

Please create a showreel for these user interfaces (UI), with a visual style referencing the interfaces shown in the images. Adapt the aspect ratio based on the interface type—if mobile-end (phone / portrait app) UIs dominate, use a 9:32 portrait ratio; if PC-end (Web / desktop) UIs dominate, use a 9:16 portrait ratio; if it is a mixed type, follow the device type with the greater quantity.

Please follow these guidelines:

### 1. Basic Principle

Only use the interfaces shown in the images; do not add or create any other unrelated interfaces, and preserve each interface's original aspect ratio and content proportions. Interface forms must conform to their device characteristics—mobile interfaces presented as vertical rectangles, PC interfaces as horizontal rectangles—and must not be rewritten or distorted into one another.

### 2. Color Scheme

Analyze the overall tonality of the UIs in the images. If the majority are dark (Dark Mode), the showreel should adopt a dark color scheme; if the majority are light (Light Mode), adopt a light color scheme. Extract the core brand color from the interfaces as the showreel's theme color, threading it through the background, text highlights, and accent elements—ensuring color functions as a narrative thread rather than mere decoration.

If the UI interfaces carry a distinctly Chinese cultural palette—such as vermillion red, turquoise green, indigo, ink grey, smoke ash, or gold—identify and continue their cultural tonality. Dark-mode versions may reference the aesthetic of "ink wash with deliberate negative space," using deep charcoal or near-black as the foundation; light-mode versions may reference the "unadorned rice paper" aesthetic, using warm off-white or cool ivory as the base. Gold and red, frequently used as accent colors in Chinese interfaces, should function as narrative threads rather than festive decorations, avoiding any cheap "celebratory" impression.

### 3. Cover Hero Visual

Select the interface with the least text and the most visually concise composition as the cover. Apply visual concepts corresponding to the device type:

- Mobile: "a hand holding a phone displaying the interface" or "a phone leaning against rough black rocks"
- PC: "a laptop (MacBook) floating in a dark environment displaying the interface," "a desktop monitor leaning against a workbench or stone backdrop," or "the interface floating as a browser window within a gradient mist of light"

The cover should evoke a deep, refined, and immersive atmosphere, and occupy a position of visual dominance. Such atmospheric imagery should appear only once throughout the entire showreel.

If the UI interfaces carry an overall Eastern aesthetic—such as ink wash, Zen minimalism, Chinese heritage style, Neo-Chinese, or Cyberpunk Hanfu—the cover hero visual may draw from the following atmospheric concepts:

- Mobile: "a phone tilted upright with its interface reflected faintly upon still water," "a phone standing on a weathered slate surface against an ink-washed negative space background," "the interface floating before misty mountain silhouettes"
- PC: "a laptop placed on a dark wooden scholar's desk, with light faintly visible through a window lattice cast onto a bamboo screen or wall in the background," "the interface floating as a browser window within ink-splash gradient mist," "a monitor leaning against a rough stone wall under warm, directional light evoking a lantern-lit Eastern atmosphere"

The overall cover should convey a visual tone of depth, restraint, and distant poetic atmosphere. Avoid piling on traditional patterns and ornaments—let the mood speak, not the symbols.

### 4. Atmospheric Accents

Extract visually striking UI components from the interfaces as auxiliary decorative elements:

- Mobile: icons, buttons, cards, tab bars, bottom navigation, etc.
- PC: top navigation bars, sidebars, data cards, button groups, chart modules, control panels, etc.

These components must follow the original UI style and must not have 3D textures, materials, or perspective transformations applied. Use a flat, planar layout—avoiding rotation or tilting—and create a rhythmic composition through contrast in component scale and balanced, staggered arrangement. Horizontal layouts especially require attention to left-right visual balance, while vertical layouts emphasize the tension and release of top-to-bottom rhythm.

If the original UI contains any of the following components characteristic of Chinese-context interfaces, prioritize their selection to reinforce cultural identity:

- Mobile: red dot notification badges, bottom navigation bars with Chinese character labels, floating card modules with Chinese typographic layouts, heritage-style line icon sets, calendar or lunar calendar components, hongbao (red envelope) or payment action buttons, etc.
- PC: data tables with Chinese column headers, sidebar navigation panels with Chinese characters, line or bar charts with Chinese-language legends, approval workflow node diagrams, decorative title modules incorporating seal script or calligraphic typefaces, etc.

All extracted components must maintain their original flat style—no perspective distortion or three-dimensional materials. When arranging Chinese-language elements, the interplay between vertical and horizontal text orientations may be used as a tool for rhythmic variation, but should remain restrained within the overall composition.

### 5. Tiled Display

Arrange the remaining UI interfaces in a grid layout without adding 3D textures, materials, or perspective transformations. These interfaces should be smaller in size than the interface in the cover hero visual (proportion approximately 1/2):

- Mobile: interfaces can be staggered vertically; a 2–3 column portrait grid is recommended
- PC: interfaces can be staggered horizontally or layered vertically; a 2-column landscape grid is recommended

Use a minimalist background such as a solid color or gradient to highlight the UI interfaces. If visual separation is needed between the grid area and the hero visual area, use rounded containers as dividers, maintaining a consistent corner radius (recommended 16–24px).

### 6. Typography

**Western Context**

The body text should use a Western sans-serif font with a distinctive modern aesthetic (such as Plus Jakarta Sans, Google Sans Flex, Inter, Söhne, or Neue Haas Grotesk—geometric or neo-grotesque typefaces). Use a vintage Western serif italic font (such as Instrument Serif, Libre Baskerville Italic, Caslon Italic, Garamond Italic, or Times Italic) to highlight key phrases or keywords. Through temporal contrast—the modern rationality of geometric sans-serif × the classical elegance of serif italic—generate strong creative tension, striking a balance between surreal futuristic concepts and refined literary elegance.

**Chinese Context**

When the interfaces are primarily Chinese-language, or when the overall showreel language is Chinese, the type system must be configured specifically:

Primary Chinese Typeface (Rational Skeleton) — recommended from the modern geometric Gothic (Hei) family:

- Smiley Sans (得意黑): a Chinese Gothic that seeks balance between humanist feel and geometric character; its body is narrow and slanted, with details drawing on the special forms of hand-drawn lettering
- PingFang SC / TC: screen-optimized, even stroke weight, quietly technological
- HYQiHei / Lantin Gothic: stronger design personality, suited to high-brand-recognition contexts

Accent Chinese Typeface (Classical Brushwork) — use a Sung (Song) or Fang Song typeface carrying classical literary resonance, mirroring the role of the serif italic in the Western context, applied to keywords or anchor phrases, creating a temporal tension of "rational restraint of modern Gothic × refined bookishness of classical Sung":

- Source Han Serif (思源宋体): restrained brush strokes, composed character; a refined modern interpretation of Sung
- Fang Song (仿宋): carries a scholar's manuscript quality; suited for atmospheric or poetic keyword accents
- Calligraphic type (use with extreme restraint): for contemporary art or streetwear-adjacent styles, calligraphic fonts may be considered—strictly limited to single-character or short-phrase scale

CJK / Latin Mixed Typesetting: when Chinese and Latin typefaces appear together, the Chinese font size should be slightly reduced (typically by 5–8%) to align optical weight. When Latin serif italics and Chinese Sung accent characters appear on the same line, ensure consistent baseline alignment and line-height to prevent visual imbalance.

**Recommended Font Sizes**

- Mobile portrait layout (9:32): titles recommended at 60–120px; subtitles 26–40px; body 16–22px
- PC portrait layout (9:16): titles may reach 80–160px to amplify visual impact; subtitles 32–48px; body 20–28px

### 7. White Space

The showreel layout must prioritize ample white space and breathing room. Do not crowd the screen with interfaces, text, or decorative elements—ensure no single element disrupts the overall rhythmic balance:

- Vertical layouts: maintain 60–100px of breathing distance between modules
- Horizontal layouts: since horizontal compositions tend to feel more crowded, module spacing should be widened to 80–120px

Allow each UI interface to occupy its own independent "stage." White space itself is part of the design language.

Chinese typography carries an inherent grid density from its square-form characters, making visual crowding more likely than with Latin text. In predominantly Chinese showreels, the priority of white space should be elevated further:

- Between Chinese title zones and UI screenshot areas, maintain a minimum spacing of 80px
- Vertical Chinese decorative phrases require at least 40px of breathing space on each side, preventing them from pressing against graphic elements
- Character-dense zones should have additional internal padding buffers outside the screenshot container—recommended 24–32px

In the Chinese aesthetic tradition, emptiness is never passive—the blank is given the same deliberate weight as the mark, the silence as much intention as the stroke. White space is an integral part of the design language, not wasted space.

---

## 中文原文（仅供对照，不要发给图像工具）

请为这些用户界面（UI）创建一个 showreel，视觉风格需参考图片中展示的界面。根据界面类型调整长宽比——如果以移动端（手机 / 竖屏应用）UI 为主，采用 9:32 的竖屏比例；如果以 PC 端（Web / 桌面）UI 为主，采用 9:16 的竖屏比例；如果是混合类型 UI，则遵循数量较多的设备类型。

请遵循以下准则：

### 1. 基本原则

- **仅使用**图片中展示的界面；不要添加或创建任何其他无关的界面，并保持每个界面的原始长宽比和内容比例。
- 界面形式必须符合其设备特征——移动端界面呈现为垂直矩形，PC 端界面呈现为水平矩形——不得将其重写或扭曲为另一种形态。

### 2. 色彩方案

- 分析图片中 UI 的整体色调。如果大多数为深色（Dark Mode），showreel 应采用深色方案；如果大多数为浅色（Light Mode），则采用浅色方案。
- 从界面中提取核心品牌色作为 showreel 的主题色，将其贯穿背景、文字高光和强调元素中——确保色彩作为叙事线索，而不仅仅是装饰。
- 如果 UI 界面带有鲜明的中式文化 palette（如朱砂红、松石绿、靛蓝、墨灰、烟灰或金色），请识别并延续其文化基调。
    - **深色模式**可参考"水墨留白"的美学，以深炭色或近黑色为基础；
    - **浅色模式**可参考"素雅宣纸"的美学，以暖米白或冷象牙白为基底。
- 金色和红色作为中式界面中常用的强调色，应作为叙事线索发挥作用，避免产生廉价的"节庆"印象。

### 3. 封面主视觉（Cover Hero Visual）

- 选择文字最少、构图最简洁可视化的界面作为封面。根据设备类型应用相应的视觉概念：
    - **移动端**："一只手握着显示该界面的手机"或"手机倚靠在粗粝的黑色岩石上"。
    - **PC 端**："一台在黑暗环境中悬浮并显示界面的笔记本电脑（MacBook）"、"一台倚靠在工作台或石质背景前的台式显示器"，或"界面作为浏览器窗口漂浮在渐变的光雾中"。
- 封面应营造深邃、精致且沉浸的氛围，并在视觉上占据主导地位。这种氛围感的 imagery 在整个 showreel 中仅出现一次。
- 如果 UI 界面整体具有东方美学特征（如水墨、禅意极简、国潮 heritage style、新中式或赛博汉服风），封面主视觉可借鉴以下氛围概念：
    - **移动端**："手机倾斜竖立，界面隐约倒映在静水中"、"手机立于风化石板表面，背景为水墨留白"、"界面漂浮在朦胧的山峦剪影前"。
    - **PC 端**："笔记本电脑置于深色木质书案上，背景隐约可见光线透过窗格映入竹屏或墙面"、"界面作为浏览器窗口漂浮在水墨飞溅的渐变雾气中"、"显示器倚靠在粗糙石墙旁，温暖的定向光营造出灯笼照明的东方氛围"。
- 整体封面应传达深度、克制和遥远诗意的视觉基调。避免堆砌传统图案和装饰——让氛围说话，而非符号。

### 4. 氛围点缀（Atmospheric Accents）

- 从界面中提取视觉上引人注目的 UI 组件作为辅助装饰元素：
    - **移动端**：图标、按钮、卡片、标签栏、底部导航等。
    - **PC 端**：顶部导航栏、侧边栏、数据卡片、按钮组、图表模块、控制面板等。
- 这些组件必须遵循原始 UI 风格，**不得**应用 3D 纹理、材质或透视变换。使用扁平、平面的布局——避免旋转或倾斜——并通过组件规模的对比和平衡、错落的排列来创造节奏感。
- 横向布局尤其需要注意左右视觉平衡，纵向布局则强调自上而下的节奏张力与释放。
- 如果原始 UI 包含以下具有中式语境界面特征的组件，优先选择它们以强化文化身份：
    - **移动端**：红点通知徽章、带中文标签的底部导航栏、具有中文排版布局的浮动卡片模块、heritage-style 线性图标集、日历或农历组件、红包或支付动作按钮等。
    - **PC 端**：带中文列标题的数据表、带中文字符的侧边导航面板、带中文图例的折线图或柱状图、审批工作流节点图、融入篆刻或书法字体的装饰性标题模块等。
- 所有提取的组件必须保持其原始扁平风格——无透视失真或 3D 材质。在排列中文元素时，可以利用竖排与横排文字的交错作为节奏变化的工具，但在整体构图中应保持克制。

### 5. 平铺展示（Tiled Display）

- 将剩余的 UI 界面以网格布局排列，不添加 3D 纹理、材质或透视变换。这些界面的尺寸应小于封面主视觉中的界面（比例约为 1/2）：
    - **移动端**：界面可以垂直错落排列；推荐 2–3 列竖屏网格。
    - **PC 端**：界面可以水平错落或垂直分层排列；推荐 2 列横屏网格。
- 使用极简背景（如纯色或渐变）以突出 UI 界面。如果需要在网格区域和主视觉区域之间进行视觉分隔，请使用圆角容器作为分隔符，保持一致的圆角半径（推荐 16–24px）。

### 6. 排版（Typography）

**西方语境：**

- 正文使用具有独特现代美学的西方无衬线字体（如 Plus_Jakarta_Sans、Google_Sans_Flex、Inter、Söhne 或 Neue Haas Grotesk——几何或新 grotesque 字体）。
- 使用复古西方衬线斜体字体（如 Instrument_Serif、LibreBaskerville Italic、Caslon Italic、Garamond Italic 或 Times Italic）来突出关键短语或关键词。
- 通过时间对比——几何无衬线的现代理性 × 衬线斜体的古典优雅——产生强烈的创意张力，在超现实未来概念与精致文学优雅之间取得平衡。

**中方语境：**

- 当界面主要为中文，或整体 showreel 语言为中文时，字体系统必须专门配置：
- **主要中文字体（理性骨架）**——推荐来自现代几何黑体家族：
    - **smiley-sans**：得意黑是一款在人文观感和几何特征中寻找平衡的中文黑体。整体字身窄而斜，细节融入了取法手绘美术字的特殊造型。
    - **PingFang SC/TC**：屏幕优化，笔画粗细均匀，科技感静谧。
    - **HYQiHei / Lantin Gothic**：设计个性更强，适合高品牌辨识度的场景。
- **强调中文字体（古典笔触）**——使用承载古典文学共鸣的宋体或仿宋字体，镜像西方语境中衬线斜体的角色，应用于关键词或锚点短语，创造"现代黑体的理性克制 × 古典宋体的 refined 书卷气"的时间张力：
    - **Source Han Serif（思源宋体）**：笔触克制，字形端庄；宋体的精致现代诠释。
    - **Fang Song（仿宋）**：承载学者手稿质感；适合氛围感或诗意关键词的强调。
    - **书法字体（极度克制使用）**：对于当代艺术或街头服饰相邻风格，可考虑书法字体——严格限制在单字或短句规模。
- **CJK / 拉丁混合排版**：当中文字体和拉丁字体同时出现时，中文字号应略微缩小（通常减少 5–8%）以对齐视觉重量。当拉丁衬线斜体和中文宋体强调字符出现在同一行时，确保基线对齐和行高一致，防止视觉失衡。

**推荐字号：**

- **移动端竖屏布局（9:32）**：标题推荐 60–120px；副标题 26–40px；正文 16–22px。
- **PC 端竖屏布局（9:16）**：标题可达 80–160px 以放大视觉冲击力；副标题 32–48px；正文 20–28px。

### 7. 留白（White Space）

- showreel 布局必须优先考虑充足的留白和呼吸感。不要用界面、文字或装饰元素拥挤屏幕——确保没有任何单一元素破坏整体的节奏平衡：
    - **纵向布局**：模块之间保持 60–100px 的呼吸距离。
    - **横向布局**：由于横向构图往往感觉更拥挤，模块间距应加宽至 80–120px。
- 让每个 UI 界面占据自己独立的"舞台"。留白本身就是设计语言的一部分。
- 中文排版因其方块字的固有网格密度，比拉丁文本更容易产生视觉拥挤感。在以中文为主的 showreel 中，留白的优先级应进一步提升：
    - 中文标题区域和 UI 截图区域之间，保持至少 80px 的间距。
    - 竖排中文装饰短语每侧需要至少 40px 的呼吸空间，防止其压迫图形元素。
    - 字符密集区域应在截图容器外部拥有额外的内部填充缓冲区——推荐 24–32px。
- 在中式美学传统中，空从未是被动的——空白被赋予与笔墨同等的刻意重量，沉默与笔触一样充满意图。留白是设计语言不可或缺的一部分，而非浪费的空间。
