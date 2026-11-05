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

## 二、 基础容器卡片 (Card Section)

```html
<section class="card">
  <div class="sec-tag">01 · 章节主题</div>
  <h2>【具体、自然的章节标题】</h2>
  <p class="lead">主旨阐述：<strong>关键要素</strong>的定义说明...</p>
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

适用于录音中提到两条思路/方案的优劣取舍。只有原文明示采用时才添加“已选定”徽标；涉及流程差异时可参考后面的双流程范式。

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
.track-a { border-top: 3px solid var(--muted); }
.track-b { border-top: 3px solid var(--accent); }
.track-name { font-size: 14px; font-weight: 750; display: flex; align-items: center; gap: 8px; }
.badge { font-size: 11px; font-weight: 700; color: var(--on-accent); background: var(--accent); padding: 1px 8px; border-radius: 999px; }
.track-main { margin-top: 8px; font-size: 13.5px; font-weight: 600; line-height: 1.5; }
.track-sub { margin-top: 4px; font-size: 12.5px; color: var(--muted); }
```

---

## 五、 原生 JS 动态数据条形图 (Interactive Bar Chart)

多个实体有多组可比较指标、切换确实有助于阅读时，才使用 Tab；单一维度优先静态图。此处仅展示非负数指标的交互逻辑，数字均为虚拟演示数据；生成时必须先在 HTML 放入默认指标的完整静态内容，确保无 JS 也可读。缺失值不填零，空数据或最大值为零时不做除法。

```html
<figure data-visual-id="stat-chart" data-visual-title="核心指标量化对比" data-visual-type="可切换指标条形图" data-visual-relation="各实体指标对比与排序" data-visual-source="从录音引用的具体数值语句...">
  <div class="chart-box">
    <!-- 切换 Tab -->
    <div class="mbtns" role="group" aria-label="指标选择">
      <button class="mbtn" data-m="指标A" aria-pressed="true">指标 A</button>
      <button class="mbtn" data-m="指标B" aria-pressed="false">指标 B</button>
    </div>
    <!-- 图表容器 -->
    <div id="statChart" class="crows"></div>
    <div id="missNote" class="figure-note"></div>
  </div>
</figure>

<script>
(function(){
  var DATA = [
    { name: '实体一', group: 'p', v: { '指标A': 820, '指标B': 450 } },
    { name: '实体二', group: 'p', v: { '指标A': 760, '指标B': 620 } },
    { name: '实体三', group: 'f', v: { '指标A': 520, '指标B': 280 } }
  ];
  var chartEl = document.getElementById('statChart');
  var btns = Array.prototype.slice.call(document.querySelectorAll('.mbtn'));
  function render(m){
    var rows = DATA.filter(function(d){ return d.v[m] != null; }).sort(function(a,b){ return b.v[m] - a.v[m]; });
    var max = rows.length ? Math.max(1, rows[0].v[m]) : 1;
    chartEl.innerHTML = rows.map(function(d){
      var pct = (d.v[m] / max * 100).toFixed(1);
      return '<div class="crow" data-grid><span class="cname">' + d.name + '</span><span class="ctrack"><i class="bar ' + d.group + '" style="width:' + pct + '%"></i></span><span class="cval">' + d.v[m] + '</span></div>';
    }).join('');
  }
  btns.forEach(function(b){
    b.addEventListener('click', function(){
      btns.forEach(function(x){ x.setAttribute('aria-pressed', x === b ? 'true' : 'false'); });
      render(b.getAttribute('data-m'));
    });
  });
  render('指标A');
})();
</script>
```

```css
.mbtns { display: flex; gap: 8px; margin-bottom: 12px; }
.mbtn { padding: 4px 12px; font-size: 12.5px; font-weight: 700; border-radius: 999px; border: 1px solid var(--card-border); background: var(--card-bg); color: var(--muted); cursor: pointer; }
.mbtn[aria-pressed="true"] { background: var(--accent); color: var(--on-accent); border-color: var(--accent); }
.crows { display: flex; flex-direction: column; gap: 8px; }
.crow { display: grid; grid-template-columns: 80px 1fr 50px; align-items: center; gap: 10px; font-size: 13px; }
.cname { font-weight: 600; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.ctrack { background: rgba(0,0,0,.04); border-radius: 4px; height: 10px; overflow: hidden; }
@media (prefers-color-scheme: dark) { .ctrack { background: rgba(255,255,255,.08); } }
.bar { display: block; height: 100%; background: var(--accent); border-radius: 4px; transition: width .3s ease; }
.cval { text-align: right; font-weight: 700; font-variant-numeric: tabular-nums; color: var(--accent); }
```

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


## 八、 技术步骤与旧新对照流程

有先后依赖的步骤可以用箭头连接；流程对照应保持共同的比较维度。以下仅为结构示例，步骤、数量、方向和强调方式均由当前输入决定。

```html
<figure data-visual-id="process" data-visual-title="处理流程" data-visual-type="流程图" data-visual-relation="输入经过处理得到结果" data-visual-source="【输入中的字面证据】">
  <figcaption class="fig-title">【图解标题】</figcaption>
  <div class="pipe">
    <div class="step"><span class="step-no">1</span><strong>【动作】</strong><p>【一句解释】</p></div>
    <span class="pipe-arrow" aria-hidden="true">→</span>
    <div class="step"><span class="step-no">2</span><strong>【动作】</strong><p>【一句解释】</p></div>
    <span class="pipe-arrow" aria-hidden="true">→</span>
    <div class="step"><span class="step-no">3</span><strong>【结果】</strong><p>【一句解释】</p></div>
  </div>
</figure>
```

旧新比较时，在同一个 figure 内用两个 `.paradigm` 包裹各自的标题与 `.pipe`，新组添加 `.is-new`。步骤数量按材料调整，不必两组相等；箭头连接的是关系，不是装饰。

```css
figure { margin: 16px 0 2px; }
.fig-title { margin-bottom: 10px; font-size: 12.5px; font-weight: 700; color: var(--muted); }
.pipe { display: flex; align-items: stretch; gap: 8px; }
.step { flex: 1; min-width: 0; padding: 12px; border: 1px solid var(--card-border); background: var(--surface-2); border-radius: 12px; }
.step-no { display: inline-flex; align-items: center; justify-content: center; width: 24px; height: 24px; border-radius: 50%; margin-right: 6px; font-size: 12px; background: var(--accent); color: var(--on-accent); }
.step strong { font-size: 14px; }
.step p { margin-top: 6px; font-size: 12.5px; color: var(--muted); line-height: 1.65; }
.pipe-arrow { flex: none; align-self: center; color: var(--accent); }
.paradigm { padding: 14px 16px; border: 1px solid var(--card-border); border-radius: 12px; }
.paradigm + .paradigm { margin-top: 10px; }
.paradigm.is-new { background: var(--accent-soft); border-color: var(--accent-border); }
.paradigm .pipe { margin-top: 10px; }
.paradigm .step { background: var(--card-bg); }
@media (max-width: 639px) {
  .pipe { flex-direction: column; }
  .pipe-arrow { transform: rotate(90deg); }
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
