# AI 录音笔核心组件库与代码范本 (Component Patterns)

本组件库基于上游范本与用户提供的原版总结样本调整，采用原生 CSS / SVG / Vanilla JS。它描述可观察的版式，不代表微信内部实现。按内容选择组件，不必全部使用。代码中的占位文字、演示数据、节点数量和配色仅说明实现方法，须按当前材料替换，不构成输出要求。基础变量和容器见移动安全 CSS；本文件样式放在其后。

---

## 一、 顶部标题区 (Header)

```html
<header class="hero">
  <p class="kicker">分类领域 · 专题标签</p>
  <h1>【具体对象与核心变化】</h1>
  <p class="sub">【导语：具体事件与值得关心的变化；必要限定就近注明】</p>
</header>
```

```css
.hero { padding: 40px 0 4px; }
.kicker { margin-bottom: 16px; font-size: 12.5px; font-weight: 700; letter-spacing: .12em; color: var(--accent); text-transform: uppercase; }
h1 { margin-top: 8px; font-size: clamp(26px, 6vw, 36px); line-height: 1.32; font-weight: 800; letter-spacing: -.01em; }
.sub { margin-top: 14px; font-size: 16px; color: var(--muted); line-height: 1.6; }
```

---

## 二、 信息分组与容器 (Content Groups)

按内容选择层级：分部统领主题，小节卡片回答具体问题，图解包围框组合相关节点与说明。短文可直接使用小节卡片。下列骨架展示可选的嵌套关系，不规定每节都有图；需要证据属性的 figure 见后面的完整范本。

```html
<section class="part" aria-labelledby="part-topic">
  <header class="part-head">
    <p class="part-label">【主题分类】</p>
    <h2 id="part-topic">【分部主题】</h2>
  </header>
  <section class="card">
    <h3>【本节结论或问题】</h3>
    <p>【必要背景或依据；图解中的信息不在此重复】</p>
    <!-- 需要组合图解时，在此放入带证据属性的 figure.visual-frame：标题、节点、连线、控件、图注同框 -->
  </section>
  <!-- 同一分部内可继续放置相关小节；数量取决于内容 -->
</section>
```

```css
.part { margin-top: 36px; }
.part-head { padding-bottom: 12px; border-bottom: 1px solid var(--card-border); }
.part-label { font-size: 12px; font-weight: 700; color: var(--secondary); margin-bottom: 6px; }
.part-head h2 { font-size: 22px; line-height: 1.4; }
.card > h3 { font-size: 17px; line-height: 1.5; margin-bottom: 10px; }
.visual-frame { padding: 16px; border: 1px solid var(--card-border); border-radius: 12px; background: var(--surface-2); }
.visual-frame figcaption { font-size: 12.5px; line-height: 1.6; color: var(--muted); }
@media (max-width: 560px) { .visual-frame { padding: 12px; } }
```

独立小节可以直接用以下卡片，不必添加分部：

```html
<section class="card">
  <div class="sec-tag">01 · 章节主题</div>
  <h2>【具体、自然的章节标题】</h2>
  <p class="lead">【先给<strong>关键事实</strong>，只补必要解释】</p>
  <!-- 模块内容 -->
</section>
```

```css
.card { margin-top: 20px; background: var(--card-bg); border: 1px solid var(--card-border); border-radius: 16px; padding: 26px 24px; box-shadow: var(--shadow); }
.sec-tag { display: inline-block; margin-bottom: 12px; padding: 3px 11px; border-radius: 999px; font-size: 12px; font-weight: 700; color: var(--accent); background: var(--accent-soft); }
.card h2 { font-size: 19.5px; line-height: 1.4; font-weight: 800; margin-bottom: 10px; }
.lead { font-size: 14.5px; color: var(--muted); line-height: 1.75; }
.lead strong { color: var(--text); }
@media (max-width: 560px) {
  .hero { padding-top: 24px; }
  .card { padding: 20px 16px; border-radius: 14px; margin-top: 16px; }
}
```

---

### 可选的色彩角色

基础样式提供主色、辅助色、提醒色与负向色的成组变量。按内容选用或覆盖；以下类名只示范如何把文字、底色和边线一起映射到同一角色，不要求每页全部使用。分类色不表示好坏，负向色不能仅因为“旧方案”就套用。

```css
.tone-secondary { --tone: var(--secondary); --tone-soft: var(--secondary-soft); --tone-border: var(--secondary-border); }
.tone-caution { --tone: var(--caution); --tone-soft: var(--caution-soft); --tone-border: var(--caution-border); }
.tone-negative { --tone: var(--negative); --tone-soft: var(--negative-soft); --tone-border: var(--negative-border); }
.color-note { color: var(--tone, var(--accent)); background: var(--tone-soft, var(--accent-soft)); border-inline-start: 3px solid var(--tone-border, var(--accent-border)); padding: 8px 12px; border-radius: 8px; }
.color-label { color: var(--tone, var(--accent)); background: var(--tone-soft, var(--accent-soft)); border: 1px solid var(--tone-border, var(--accent-border)); padding: 3px 9px; border-radius: 999px; font-size: 12px; }
```

## 三、 时间线与状态节点 (Timeline)

适用于具有明确时序或状态演变的材料；节点数量、状态标签和强调方式由内容决定。

```html
<figure data-visual-id="progress-timeline" data-visual-title="【事件或状态演变】" data-visual-type="时间线" data-visual-relation="【各阶段之间的关系】" data-visual-source="从录音引用的原话...">
  <ol class="timeline">
    <li>
      <span class="step-tag tag-stage">【初始状态】</span>
      <p class="t">【该阶段的事实、时间与<strong>关键条件</strong>】</p>
    </li>
    <li class="change">
      <span class="step-tag tag-change">【状态变化】</span>
      <p class="t">【发生的变化及其<strong>适用范围</strong>】</p>
    </li>
    <li class="pending">
      <span class="step-tag tag-open">【后续状态】</span>
      <p class="t">【材料支持的<strong>结果或待确认事项</strong>】</p>
    </li>
  </ol>
</figure>
```

```css
.timeline { list-style: none; margin-top: 14px; }
.timeline li { position: relative; padding: 0 0 20px 26px; }
.timeline li:last-child { padding-bottom: 4px; }
.timeline li::before { content: ""; position: absolute; left: 6px; top: 8px; bottom: -2px; width: 2px; background: var(--card-border); }
.timeline li:last-child::before { display: none; }
.timeline li::after { content: ""; position: absolute; left: 1px; top: 5px; width: 12px; height: 12px; border-radius: 50%; background: var(--card-bg); border: 3px solid var(--accent); }
.timeline li.change::after { border-color: #c0392b; }
.timeline li.pending::after { border-color: #9a6b00; }
.step-tag { display: inline-block; font-size: 11.5px; font-weight: 700; padding: 2px 8px; border-radius: 99px; margin-bottom: 4px; }
.tag-stage { background: var(--accent-soft); color: var(--accent); }
.tag-change { background: rgba(192, 57, 43, 0.12); color: #c0392b; }
.tag-open { background: rgba(154, 107, 0, 0.12); color: #9a6b00; }
.timeline .t { font-size: 14px; color: var(--text); }
```

---

## 四、 决策对比矩阵 (Comparison Matrix)

适用于录音中提到两条思路/方案的优劣取舍。只有原文明示采用时才添加“已选定”徽标；涉及流程差异时保持对应步骤可比较；并列特点不串成流程。面板可用短清单替代段落，原文确有优劣评价时才用带文字含义的勾叉。

```html
<figure data-visual-id="approach-compare" data-visual-title="【方案对比主题】" data-visual-type="对照矩阵" data-visual-relation="方案 A 与方案 B 的策略权衡" data-visual-source="从录音引用的原话...">
  <div class="tracks" data-grid>
    <div class="track track-a">
      <div class="track-name">【方案 A】</div>
      <div class="track-main">【方案 A 在共同维度下的特点】</div>
      <div class="track-sub">【原文支持的条件或代价】</div>
    </div>
    <div class="track track-b">
      <div class="track-name">【方案 B】</div>
      <div class="track-main">【方案 B 在共同维度下的特点】</div>
      <div class="track-sub">【原文支持的条件或代价】</div>
    </div>
  </div>
</figure>
```

```css
.tracks { display: grid; gap: 12px; margin-top: 14px; grid-template-columns: 1fr 1fr; }
@media (max-width: 600px) { .tracks { grid-template-columns: 1fr; } }
.track { border: 1px solid var(--card-border); border-radius: 12px; padding: 14px 15px; background: var(--card-bg); }
.track-a { border-top: 3px solid var(--secondary); }
.track-b { border-top: 3px solid var(--accent); }
.track-a .track-name { color: var(--secondary); }
.track-b .track-name { color: var(--accent); }
.track-name { font-size: 14px; font-weight: 750; display: flex; align-items: center; gap: 8px; }
.badge { font-size: 11px; font-weight: 700; color: var(--on-accent); background: var(--accent); padding: 1px 8px; border-radius: 999px; }
.track-main { margin-top: 8px; font-size: 13.5px; font-weight: 600; line-height: 1.5; }
.track-sub { margin-top: 4px; font-size: 12.5px; color: var(--muted); }
```

---

## 五、 对齐的比例条 (Proportional Bars)

适用于同口径数量或比例的直接对比。每行是名称、同一量尺的轨道、原始数值；用条长解释差距，用短图注交代量尺。单一指标无需切换按钮。以下为结构占位，必须用输入值计算宽度并替换全部占位内容；不能把未知值当零、把估计当精确值，或用视觉饱满程度决定条长。

```html
<!-- 放入带证据属性的 figure.visual-frame；共用量尺，宽度 = 值 / 量尺上限 * 100% -->
<div class="metric-rows" style="--scale-max:【量尺上限】">
  <div class="metric-row" style="--value:【原始数值】">
    <span>【对象】</span>
    <div class="metric-track" aria-hidden="true"><i></i></div>
    <strong>【数值与单位】</strong>
  </div>
  <!-- 按输入添加同口径的其他对象；数值与名称须在无 CSS 时仍可读 -->
</div>
<figcaption>【量尺及必要限定；不重复逐行读数】</figcaption>
```

```css
.metric-rows { display: grid; grid-template-columns: minmax(4em, .6fr) minmax(0, 3fr) minmax(4em, 1fr); gap: 12px 10px; }
.metric-row { display: grid; grid-column: 1 / -1; grid-template-columns: subgrid; align-items: center; }
.metric-row > span { font-size: 13px; color: var(--muted); }
.metric-row > strong { font-size: 14px; font-variant-numeric: tabular-nums; }
.metric-track { height: 18px; background: var(--card-bg); border: 1px solid var(--card-border); border-radius: 6px; overflow: hidden; }
.metric-track > i { display: block; width: calc(100% * var(--value) / var(--scale-max)); height: 100%; background: var(--tone, var(--accent)); border-radius: 5px; }
@media (max-width: 440px) {
  .metric-rows { grid-template-columns: minmax(0, 1fr) auto; }
  .metric-row { gap: 5px 10px; }
  .metric-track { grid-column: 1 / -1; grid-row: 2; }
}
```

各行共享网格列，保证轨道同宽、零点对齐；刻度轴与轨道共用同一列，不能把右侧数值标签列算入轴长，也不能让数值的文字长度改变每行量尺。量尺上限须明确显示，样式宽度由数值计算，不能手填“看起来合适”的百分比。

范围值用带起止刻度的区间带；只有下限时，将已知部分画到下限刻度，在该位置用箭头或开放端符号表示“超过此处”，不随意给未知部分一个条长。近似值紧邻标出“约”；原文没有上下界时，不人为造出区间。检查渲染后的条长是否与已知值比例相符，图注不能弥补错误几何编码。无法诚实映射的定性对照改用短清单。

---

## 六、 洞察卡片 (Insight Box)

按需使用的一句收束，不是每节标配。优先点明具体关键处，避免“洞察／底层根因”套话；新增分析才标注“分析”，原文未支持时不推断根因：

```html
<div class="insight">
  <strong>【关键点】：</strong>【材料支持、值得单独突出的理解或限制】
</div>
```

```css
.insight { margin-top: 14px; background: var(--accent-soft); border-left: 3px solid var(--accent); border-radius: 8px; padding: 10px 13px; font-size: 13.5px; color: var(--text); }
.insight .tag { font-size: 11px; font-weight: 800; letter-spacing: .08em; color: var(--accent); margin-right: 8px; }
```

---

## 七、 512×512 矢量 SVG 封面生成规范 (Share Cover)

在 `</body>` 闭合前必须附带：

```html
<template id="share-cover">
  <svg xmlns="http://www.w3.org/2000/svg" width="512" height="512" viewBox="0 0 512 512">
    <!-- 浅灰底板 -->
    <rect width="512" height="512" fill="#F8FAFC"/>
    <!-- 居中圆盘 -->
    <circle cx="256" cy="256" r="210" fill="#EEF2F6"/>
    <!-- 核心主体矢量图（根据主题抽象提炼，如麦克风、芯片、数据表、沟通气泡） -->
    <g transform="translate(156, 156)">
      <rect width="200" height="200" rx="36" fill="var(--accent, #1d63d8)"/>
      <!-- 图形细节 -->
    </g>
  </svg>
</template>
```


## 八、 路线节点与步骤条 (Milestones & Steps)

同一条主线的里程碑用细轨道和圆点，节点短标签直接可见；重要节点可以有光圈和旗标。下例节点等距只表示顺序，不代表真实时间或距离；节点数、标签、强调位置均由输入决定。无依据时不补造起点、终点、阶段数或“当前进度”。

```html
<!-- 放入带证据属性的 figure.visual-frame；本例仅展示结构 -->
<ol class="milestones" aria-label="【路线名称；必要时注明顺序示意】">
  <li><span class="route-flag"></span><i aria-hidden="true"></i><b>【节点】</b></li>
  <li class="is-emphasis"><span class="route-flag">【这个节点的关键变化】</span><i aria-hidden="true"></i><b>【节点】</b></li>
  <li><span class="route-flag"></span><i aria-hidden="true"></i><b>【节点】</b></li>
</ol>
<!-- 需要时在轨道下方补一条解释，勿把每个节点包成段落卡片 -->
```

```css
.milestones { display: grid; grid-auto-flow: column; grid-auto-columns: minmax(0, 1fr); list-style: none; padding: 0; margin: 12px 0; }
.milestones > li { display: grid; grid-template-rows: subgrid; grid-row: span 3; justify-items: center; gap: 10px; position: relative; min-width: 0; text-align: center; padding: 0 6px; }
.milestones i { position: relative; width: calc(100% + 12px); height: 14px; background: linear-gradient(var(--card-border), var(--card-border)) center / 100% 3px no-repeat; }
.milestones > li:first-child i { background-size: 50% 3px; background-position: right center; }
.milestones > li:last-child i { background-size: 50% 3px; background-position: left center; }
.milestones > li:only-child i { background: none; }
.milestones i::before { content: ""; position: absolute; width: 14px; height: 14px; left: 50%; transform: translateX(-50%); border: 3px solid var(--card-border); border-radius: 50%; background: var(--card-bg); box-sizing: border-box; }
.route-flag { align-self: end; max-width: 100%; padding: 3px 9px; border-radius: 999px; font-size: 12px; color: var(--secondary); background: var(--secondary-soft); overflow-wrap: anywhere; }
.route-flag:empty { visibility: hidden; }
.milestones b { font-size: 13px; font-weight: 500; color: var(--muted); }
.milestones .is-emphasis i::before { background: var(--secondary); border-color: var(--secondary); box-shadow: 0 0 0 5px var(--secondary-soft); }
@media (max-width: 560px) {
  .milestones { grid-auto-flow: row; grid-auto-columns: auto; }
  .milestones > li { grid-row: auto; grid-template: auto auto / 14px minmax(0, 1fr); gap: 4px 14px; justify-items: start; text-align: left; padding: 0 0 18px; }
  .milestones > li::before { content: ""; position: absolute; top: 7px; bottom: -7px; left: 6px; width: 2px; background: var(--card-border); }
  .milestones > li:last-child::before { display: none; }
  .milestones > li i { grid-area: 1 / 1 / 3 / 2; width: 14px; background: none; }
  .milestones .route-flag { grid-area: 1 / 2; }
  .milestones .route-flag:empty { display: none; }
  .milestones b { grid-area: 2 / 2; }
}
```

旗标和轨道各占共享行，`subgrid` 使各节点按最长旗标共同排布；不能改成各节点独立的 `auto` 行，否则有无旗标、长短文本会让圆点高低错位。也可用独立轨道层实现同样约束。手机切换为纵向点线，不靠 `nowrap`、缩小字号或强制横滚容纳路线。等距只表达顺序，需按真实间隔定位时另用数据计算位置。

简单操作顺序优先使用轻量编号步骤条，只有复杂依赖、分支或回退才画连接框。末项只是普通步骤时不加结果色；原文确有重点结果才使用 `.step-result`。

```html
<ol class="step-strip">
  <li><b>【动作】</b><span>【必要条件，可省略】</span></li>
  <li><b>【后续动作】</b><span>【必要条件，可省略】</span></li>
  <li class="step-result"><b>【重点结果】</b><span>【材料支持的结果说明】</span></li>
</ol>
```

```css
.step-strip { display: flex; gap: 16px; padding: 0; list-style: none; counter-reset: stage; }
.step-strip > li { flex: 1; min-width: 0; padding: 10px 8px 10px 0; border-top: 2px solid var(--card-border); counter-increment: stage; }
.step-strip > li::before { content: counter(stage); display: inline-grid; place-items: center; width: 24px; height: 24px; margin: 0 6px 6px 0; border-radius: 50%; background: var(--card-bg); color: var(--secondary); font-weight: 700; }
.step-strip b { font-size: 14px; }
.step-strip span { display: block; font-size: 13px; color: var(--muted); }
.step-strip .step-result { background: var(--accent-soft); border-color: var(--accent); border-radius: 0 0 10px 10px; padding-inline: 10px; }
@media (max-width: 560px) {
  .step-strip { flex-direction: column; gap: 10px; }
  .step-strip > li { border-top: 0; border-inline-start: 2px solid var(--card-border); padding-inline-start: 12px; }
}
```

## 九、 障碍清单与原话收尾

障碍清单适合解释“为什么难”，可以与后面的解决流程前后呼应；不要因此重复同一段正文。它是文本清单，无须伪装成统计图。

```html
<div class="hurdles">
  <div class="hurdle"><span class="h-no">1</span><p><strong>【动作短词】</strong>——【这一关为什么难】</p></div>
  <div class="hurdle"><span class="h-no">2</span><p><strong>【动作短词】</strong>——【这一关为什么难】</p></div>
</div>
<!-- 有原话时才用引用块；来源不明时不要补造署名 -->
<blockquote>【输入中的原话】<cite>【输入已给出的归属，可省略】</cite></blockquote>
```

```css
.hurdles { margin-top: 14px; }
.hurdle { display: flex; gap: 12px; align-items: flex-start; padding: 9px 0; font-size: 14.5px; }
.hurdle + .hurdle { border-top: 1px dashed var(--card-border); }
.h-no { flex: none; display: flex; align-items: center; justify-content: center; width: 24px; height: 24px; border-radius: 50%; background: var(--surface-2); color: var(--accent); font-weight: 800; }
blockquote { margin: 14px 0 12px; padding: 14px 16px; border-left: 3px solid var(--accent); border-radius: 0 10px 10px 0; background: var(--surface-2); font-size: 15.5px; font-weight: 700; line-height: 1.7; }
blockquote cite { display: block; margin-top: 6px; font-size: 12.5px; font-style: normal; font-weight: 400; color: var(--muted); }
```


## 十、 有含义的小图形（趣味细节）

让具象细节帮助读者识别对象、理解动作或记住区别。先确定图形承担的语义，再选择与本次内容相关的轮廓、纹理或简短动画；不规定物件种类与数量。

- 同类对象保持一致的视觉语法，有意义的差异才改变形状、颜色或排列。
- 图形放在相关内容附近，尺寸服从信息层级，避免独立堆放装饰卡片。
- 示意数量不冒充统计数据，颜色不暗示未经材料支持的分类；含义同时用文字表达。
- 纯装饰图形使用 `aria-hidden="true"`；承担信息的图形提供可读说明。

```html
<div class="micro-visual">
  <!-- 在此绘制与当前主题相关的内联 SVG 或 CSS 图形 -->
  <small>【图形帮助解释的关系】</small>
</div>
```

```css
.micro-visual { display: flex; flex-wrap: wrap; align-items: center; gap: 6px; margin-top: 6px; }
.micro-visual small { font-size: 11.5px; color: var(--muted); }
```

## 十一、 定性趋势的紧凑对照

只有方向性描述、没有可比数值时，可使用紧凑的文字对照，不画暗示精确倍数的比例条。保留原文的条件和不确定性，避免正文重复图中文字。

```html
<!-- 放在具备五项证据属性的 figure 内；替换为输入原话支持的标签和内容 -->
<div class="trend-row"><span>【条件 A】</span><strong>【原文支持的定性描述】</strong></div>
<div class="trend-row is-new"><span>【条件 B】</span><strong>【原文支持的定性描述】</strong></div>
<figcaption>【理解对照所必需的条件或限定，无则省略】</figcaption>
```

```css
.trend-row { display: flex; gap: 12px; align-items: baseline; padding: 10px 12px; border-radius: 8px; background: var(--surface-2); font-size: 13px; }
.trend-row + .trend-row { margin-top: 8px; }
.trend-row > span { flex: 0 0 5em; color: var(--muted); }
.trend-row.is-new { background: var(--accent-soft); color: var(--accent); }
```


## 十二、 胶囊选项卡与状态面板 (State Tabs)

同一机制存在多个备选条件或结果时使用。需要一眼比较两侧差异时优先并列，不为隐藏长文硬加选项卡。选中项用实色药丸，对应结果用同色浅底；状态数量随材料变化，面板可包含图形而不只换一句话。核心案例不只存在于隐藏面板：可在图前保留概括各状态差异的短句，面板展示对应细节。

下例为渐进增强：无 JS 时各面板连同标题全部可读，按钮隐藏；初始化完成后才启用 tabs。每个实例使用独立的 ID 前缀，事件限定在实例内，不能全局切换所有图。支持点击、左右方向键循环、Home/End；不要混用 `aria-pressed` 和 tabs 语义。

```html
<div class="state-tabs">
  <div class="state-controls" hidden aria-label="【切换主题】">
    <button type="button" id="choice-a" aria-controls="panel-a">【状态 A】</button>
    <button type="button" id="choice-b" aria-controls="panel-b">【状态 B】</button>
  </div>
  <section class="state-panel" id="panel-a" aria-labelledby="choice-a"><h4>【状态 A】</h4><p>【该条件下的内容或结果】</p></section>
  <section class="state-panel" id="panel-b" aria-labelledby="choice-b"><h4>【状态 B】</h4><p>【另一条件下的内容或结果】</p></section>
</div>
<script>
document.querySelectorAll('.state-tabs').forEach(root => {
  const list = root.querySelector('.state-controls');
  const tabs = [...list.querySelectorAll('button')];
  const panels = tabs.map(tab => root.querySelector('#' + tab.getAttribute('aria-controls')));
  if (!tabs.length || panels.some(panel => !panel)) return;
  function select(index, focus = false) {
    tabs.forEach((tab, i) => {
      tab.setAttribute('aria-selected', String(i === index));
      tab.tabIndex = i === index ? 0 : -1;
      panels[i].hidden = i !== index;
    });
    if (focus) tabs[index].focus();
  }
  tabs.forEach((tab, i) => {
    tab.setAttribute('role', 'tab');
    panels[i].setAttribute('role', 'tabpanel');
    panels[i].tabIndex = 0;
    tab.addEventListener('click', () => select(i));
    tab.addEventListener('keydown', event => {
      const next = { ArrowRight: (i + 1) % tabs.length, ArrowLeft: (i - 1 + tabs.length) % tabs.length, Home: 0, End: tabs.length - 1 }[event.key];
      if (next !== undefined) { event.preventDefault(); select(next, true); }
    });
  });
  list.setAttribute('role', 'tablist');
  select(0);
  list.hidden = false;
});
</script>
```

```css
.state-controls[hidden], .state-panel[hidden] { display: none; }
.state-controls { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 10px; }
.state-controls button { font: inherit; font-size: 13px; font-weight: 700; padding: 8px 14px; min-height: 40px; border: 1px solid var(--card-border); border-radius: 999px; background: var(--card-bg); color: var(--text); cursor: pointer; }
.state-controls button[aria-selected="true"] { background: var(--accent); border-color: var(--accent); color: var(--on-accent); }
.state-controls button:focus-visible, .state-panel:focus-visible { outline: 2px solid var(--accent); outline-offset: 3px; }
.state-panel { margin-top: 10px; padding: 12px 14px; background: var(--accent-soft); border-radius: 10px; }
.state-panel h4 { margin: 0 0 6px; font-size: 14px; }
```

## 十三、 标签组与重点短条 (Chips & Callouts)

组合图解可在主要关系上下放少量辅助信息，位置服从逻辑。分类标签、前置条件、追问、结果和后续行动各有形态，但无需每图集齐。短条承载新增的关键信息，不复述前面的图和正文。只有原文支持行动时才放行动药丸。

```html
<ul class="topic-chips" aria-label="【并列活动或特征】"><li>【短词】</li><li>【短词】</li></ul>
<!-- 以下按内容选用，不作为固定组合 -->
<p class="prerequisite">【前置条件】：<strong>【决定理解或执行的限制】</strong></p>
<p class="question-note"><strong>【原文明示的追问重点】</strong>【必要语境】</p>
<p class="result-note"><strong>【关键结果】</strong>【短说明】</p>
<div class="next-actions"><span>【明确的后续行动】</span></div>
```

```css
.topic-chips, .next-actions { display: flex; flex-wrap: wrap; gap: 8px; padding: 0; margin: 12px 0; list-style: none; }
.topic-chips li { padding: 5px 12px; border: 1px solid var(--card-border); border-radius: 999px; background: var(--card-bg); font-size: 13px; font-weight: 600; max-width: 100%; overflow-wrap: anywhere; }
.prerequisite { border: 1px dashed var(--secondary-border); border-radius: 10px; background: var(--card-bg); padding: 10px 12px; }
.question-note { background: var(--caution-soft); border-radius: 10px; padding: 10px 12px; }
.question-note strong { color: var(--caution); }
.result-note { background: var(--secondary-soft); border-inline-start: 3px solid var(--secondary); border-radius: 0 10px 10px 0; padding: 10px 12px; }
.next-actions > span { padding: 6px 12px; border-radius: 999px; background: var(--accent-soft); color: var(--accent); font-size: 13px; font-weight: 700; max-width: 100%; overflow-wrap: anywhere; }
```
