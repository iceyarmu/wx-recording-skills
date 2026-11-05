---
name: wx-recording-skills
version: 1.0.0
display_name: 微信录音笔风格视觉化纪要
display_name_en: WeChat-style Recording Recap
description: Use when converting voice notes into visual HTML recaps.
author: Hermes整理自 duzhilei951/ha-recording-recap
license: MIT (upstream)
metadata:
  hermes:
    tags: [recording, transcript, html, infographic, meeting-notes]
    related_skills: [html-design, humanizer]
---

# wx-recording-skills：AI 录音笔视觉化纪要

将口述、会议转写和碎片笔记整理成自然、清楚、有图解表现力的单文件 HTML。学习微信录音笔总结的编辑与视觉特点，不宣称掌握其内部实现。

## 使用范围

适用于用户要求结构化、可视化的网页纪要。若只要求普通摘要或 Markdown，不强制生成 HTML。

## 工作流程

1. 读取输入，明确材料范围、表达目的与核心关系。
2. 读取 [内容与风格规范](references/prompt-spec.md)，先完成内容选择，再写页面。多主题长材料分两步执行：先形成可复查的内容清单（可存临时文件），再将清单与原始输入共同用于生成；不要用一段全篇主旨代替清单。
3. 按清单安排主线与信息层级，精简表达，规划分组和色彩职责。
4. 按语义选择表达方式，参考 [组件范本](references/component-library.md) 和 [移动安全样式](references/recording-agent-mobile-safety.css)。范本是实现参考，不是内容或版式配额。
5. 输入涉及设计或方案取舍时，另读 [设计讨论规则](references/design-recap.md)。
6. 生成并保存完整 HTML，检查内容忠实性，再在浏览器中验收视觉和交互。

## 材料与内容边界

- 用户提供链接时读取精确目标，核对正文完整性。摘要、评论、作者回应和外部资料应区分来源；无法取得的部分明确说明，不用相似材料替代。
- 排名、数量、日期与结论的范围不得超过已取得证据。引用外部事实时按任务需要核实，不能将来源观点直接升级为事实。
- 去掉噪音，保留否定、条件、修正、不确定性和有辨识度的表达。按内容组织，不套用固定章节数量、领域配色或样例叙事。
- 图形应帮助解释关系，交互应帮助理解变化。具体物件、图表、状态和控件均从当前输入推导。
- 测试输入、原版成品和评审记录只用于评估。不得把某个用例的实体、数字、布局或结论变成所有输入必须满足的要求。

## HTML 交付约束

- 单文件、自包含、离线可读：CSS、SVG 与必要的 Vanilla JS 内联，不使用外部字体、CDN 或外部脚本。
- head 包含 charset、viewport、`content-status=substantive`、`artifact-kind=doc`；title 与正文主标题一致。
- 嵌入 `<style id="recording-agent-mobile-safety">`；使用 CSS 变量和 `prefers-color-scheme: dark`。主题样式可覆盖基础样式，窄屏图表不得撑破页面。
- 图表与机制示意用 figure 包裹，提供唯一的小写 kebab-case `data-visual-id`，以及 `data-visual-title`、`data-visual-type`、`data-visual-relation`、`data-visual-source`。
- source 从原始输入截取能支持图形关系的短而完整的连续片段，并进行 HTML 转义；不在引文中删除语气词、合并句子或替换字形。示意假设就近说明，证据不足时缩小图解范围。
- body 尾部包含 `<template id="share-cover">`，内置与本次主题相关的 512×512 SVG；不作为正文大幅封面显示。
- 无 JavaScript 时主要内容仍可阅读。控件具备语义与键盘操作，动画兼顾减少动态效果偏好。

## 验收与交付

- 内容：对照输入检查关键事实、代表案例、正反差异与约束的覆盖，没有新增决定、混淆主体、改变承诺强度或把歧义数字精确化；标题和章节清楚，图文不重复。
- 视觉：实际查看桌面与窄屏、深浅色效果。检查层级、密度、文字可读性、图形关系与溢出；不能只凭源码声称风格达标。
- 行为：操作每个主要控件与必要边界，确认实际状态变化、关闭/恢复行为及无 JS 回退。
- 结构：检查完整 HTML、元信息、图表属性、来源片段、分享封面与外部依赖。修订后重新检查，避免遗漏非可见结构。
- 用户要求文件时保存到指定目录或当前工作目录，返回绝对路径并简要说明结果与未完成的验收项；要求源码时输出完整 HTML。

## 来源

最初整理自 `duzhilei951/ha-recording-recap` 的提交 `84c07fd`，本地规则与组件已调整。原作者与 MIT 许可见 `references/upstream-MIT-LICENSE.txt`。参考代码不构成对其示例内容的事实背书。
