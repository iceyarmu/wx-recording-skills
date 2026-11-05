# AI 录音笔核心组件库与代码范本 (Component Patterns)

本组件库直接逆向提炼自微信输入法 VoiceSummary 网页生成引擎，全部采用原生 CSS / SVG / Vanilla JS，无需任何外部依赖。

---

## 一、 顶部标题区 (Header)

```html
<header>
  <p class="kicker">分类领域 · 专题标签</p>
  <h1>【结论先行的一句话标题】</h1>
  <p class="sub">【导语：浓缩事件背景、核心矛盾或当前结论】</p>
</header>
```

```css
.kicker { font-size: 12px; font-weight: 700; letter-spacing: .12em; color: var(--accent); text-transform: uppercase; }
h1 { margin-top: 8px; font-size: clamp(22px, 5vw, 28px); line-height: 1.35; font-weight: 800; letter-spacing: -.01em; }
.sub { margin-top: 10px; font-size: 14.5px; color: var(--muted); line-height: 1.6; }
```

---

## 二、 基础容器卡片 (Card Section)

```html
<section class="card">
  <h2><span>01 核心模块标题</span><span class="idx">01</span></h2>
  <p class="lead">主旨阐述：<strong>关键要素</strong>的定义说明...</p>
  <!-- 模块内容 -->
</section>
```

```css
.card { margin-top: 22px; background: var(--card-bg); border: 1px solid var(--card-border); border-radius: 16px; padding: 22px 20px 24px; box-shadow: var(--shadow); }
.card h2 { display: flex; align-items: center; gap: 10px; font-size: 17px; font-weight: 750; }
.card h2::before { content: ""; flex: none; width: 4px; height: 16px; border-radius: 2px; background: var(--accent); }
.card h2 .idx { margin-left: auto; font-size: 12px; font-weight: 700; color: var(--faint); }
.lead { margin-top: 10px; font-size: 14.5px; color: var(--text); }
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

适用于录音中提到两条思路/方案的优劣取舍。

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
.badge { font-size: 11px; font-weight: 700; color: #fff; background: var(--accent); padding: 1px 8px; border-radius: 999px; }
.track-main { margin-top: 8px; font-size: 13.5px; font-weight: 600; line-height: 1.5; }
.track-sub { margin-top: 4px; font-size: 12.5px; color: var(--muted); }
```

---

## 五、 原生 JS 动态数据条形图 (Interactive Bar Chart)

当录音中口述了多个实体的一组指标数据时，采用原生纯 JS 实现 Tab 切换联动条形图。

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
    var max = rows.length ? rows[0].v[m] : 1;
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
.mbtn[aria-pressed="true"] { background: var(--accent); color: #fff; border-color: var(--accent); }
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

每个核心小节底部的定调总结：

```html
<div class="insight">
  <span class="tag">洞察</span>
  <strong>问题根源：</strong>需求本身不复杂，核心矛盾在于前置资质未核实，导致方案一改再改。
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
