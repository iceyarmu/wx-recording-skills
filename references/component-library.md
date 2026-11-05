# AI 录音笔核心组件库与代码范本 (Component Patterns)

本组件库基于上游范本与用户提供的原版总结样本调整，采用原生 CSS / SVG / Vanilla JS。它描述可观察的版式，不代表微信内部实现。按内容选择组件，不必全部使用。基础变量和容器见移动安全 CSS；本文件样式放在其后。

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

## 三、 时间线与交涉节点 (Timeline)

适用于沟通来回、流程推进、交涉反悔等场景。

```html
<figure data-visual-id="progress-timeline" data-visual-title="交涉脉络示意" data-visual-type="时间线" data-visual-relation="各阶段口径与状态演变" data-visual-source="从录音引用的原话...">
  <ol class="timeline">
    <li>
      <span class="step-tag tag-promise">初答应</span>
      <p class="t">对方先表示<strong>没问题</strong>，套餐已定好，约定明日办理。</p>
    </li>
    <li class="flip">
      <span class="step-tag tag-flip">突然改口</span>
      <p class="t">随即改口无法按期办理，最快需要推迟至<strong>后天</strong>。</p>
    </li>
    <li class="pending">
      <span class="step-tag tag-open">未决</span>
      <p class="t">现场应对：明天能办几张算几张，后续<strong>等待确认回复</strong>。</p>
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
.timeline li.flip::after { border-color: #c0392b; }
.timeline li.pending::after { border-color: #9a6b00; }
.step-tag { display: inline-block; font-size: 11.5px; font-weight: 700; padding: 2px 8px; border-radius: 99px; margin-bottom: 4px; }
.tag-promise { background: var(--accent-soft); color: var(--accent); }
.tag-flip { background: rgba(192, 57, 43, 0.12); color: #c0392b; }
.tag-open { background: rgba(154, 107, 0, 0.12); color: #9a6b00; }
.timeline .t { font-size: 14px; color: var(--text); }
```

---

## 四、 决策对比矩阵 (Comparison Matrix)

适用于录音中提到两条思路/方案的优劣取舍。只有原文明示采用时才保留“本页采用”徽标；旧新机制比较优先使用后面的双流程范式。

```html
<figure data-visual-id="approach-compare" data-visual-title="双轨方案取舍" data-visual-type="对照矩阵" data-visual-relation="方案 A 与方案 B 的策略权衡" data-visual-source="从录音引用的原话...">
  <div class="tracks" data-grid>
    <div class="track track-a">
      <div class="track-name">思路一 · 全量铺开</div>
      <div class="track-main">试图满足所有非核心诉求，导致资源分散。</div>
      <div class="track-sub">边际收益递减，耗时周期长。</div>
    </div>
    <div class="track track-b">
      <div class="track-name">思路二 · 聚焦核心 <span class="badge">本页采用</span></div>
      <div class="track-main">锁定最核心主目标，其他席位灵活适配。</div>
      <div class="track-sub">资源高度集约，见效最快。</div>
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

多个实体有多组可比较指标、切换确实有助于阅读时，才使用 Tab；单一维度优先静态图。此处展示交互逻辑，生成时必须先在 HTML 放入默认指标的完整静态内容，确保无 JS 也可读。缺失值不填零，空数据或最大值为零时不做除法。

```html
<figure data-visual-id="stat-chart" data-visual-title="核心指标量化对比" data-visual-type="可切换指标条形图" data-visual-relation="各实体指标对比与排序" data-visual-source="从录音引用的具体数值语句...">
  <div class="chart-box">
    <!-- 切换 Tab -->
    <div class="mbtns" role="tablist">
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
  <strong>关键在复用：</strong>每个人的药不同，背后的设计与制造流程可以复用。
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

技术步骤用箭头表达先后依赖，不套交涉时间线。旧新对照用上下两组流程，旧组中性、新组主题色。以下仅为结构示例；替换为输入中实际出现的步骤、数量及字面证据，不照抄医学结论。

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

在核心图解里加 1–2 处局部小物件，让抽象概念更可感。以药物为例：旧路径中同色药丸表达重复生产，新路径中多色药丸表达各不相同。它们是图解内的辅助行，不额外开一张“装饰卡”。其他主题换成与内容相关的物件，不把药丸当成所有总结的通用装饰。

```html
<!-- 放入对应流程节点内部；图形数量仅为示意，不代表患者或产品数量 -->
<div class="micro-visual">
  <span class="pill-row" aria-hidden="true"><i class="pill"></i><i class="pill"></i><i class="pill"></i><i class="pill"></i></span>
  <small>同一种药，重复生产</small>
</div>
<div class="micro-visual">
  <span class="pill-row varied" aria-hidden="true"><i class="pill"></i><i class="pill"></i><i class="pill"></i><i class="pill"></i><i class="pill"></i></span>
  <small>不同的药，共用一套流程</small>
</div>
```

```css
.micro-visual { display: flex; flex-wrap: wrap; align-items: center; gap: 6px; margin-top: 6px; }
.micro-visual small { font-size: 11.5px; color: var(--muted); }
.pill-row { display: inline-flex; align-items: center; gap: 5px; padding: 4px 0; }
.pill { display: block; width: 18px; height: 8px; border-radius: 6px; background: var(--accent); transform: rotate(-24deg); }
.varied .pill:nth-child(1) { background: #3b82f6; }
.varied .pill:nth-child(2) { background: #d99a32; }
.varied .pill:nth-child(3) { background: #d65a8a; }
.varied .pill:nth-child(4) { background: #8b5cf6; }
.varied .pill:nth-child(5) { background: #14b8a6; }
@media (prefers-color-scheme: dark) { .varied .pill { filter: brightness(1.2); } }
```

配色仅区分示意物件，不赋予颜色未经原文支持的药物类别；文字承担意义，不能只靠颜色传达信息。kicker 可配一个小型描边胶囊 SVG，保持装饰尺寸，避免将 512×512 分享封面直接显示为正文主图。

## 十一、 定性趋势的紧凑对照

原文只有“很多年 / 可能几个月甚至几天”这类宽泛时间时，使用两行短对照，避免复用一整套“输入→处理→结果”的双流程，也不画暗示精确倍数的比例条。只在图注限定一次，正文不把图中文字再解释一遍。

```html
<!-- 放在具备五项证据属性的 figure 内；替换为输入原话支持的标签和内容 -->
<div class="trend-row"><span>过去</span><strong>很多年，持续推进</strong></div>
<div class="trend-row is-new"><span>原文展望</span><strong>可能几个月，甚至几天</strong></div>
<figcaption>原文的趋势性预测，非已验证周期或精确比例。</figcaption>
```

```css
.trend-row { display: flex; gap: 12px; align-items: baseline; padding: 10px 12px; border-radius: 8px; background: var(--surface-2); font-size: 13px; }
.trend-row + .trend-row { margin-top: 8px; }
.trend-row > span { flex: 0 0 5em; color: var(--muted); }
.trend-row.is-new { background: var(--accent-soft); color: var(--accent); }
```
