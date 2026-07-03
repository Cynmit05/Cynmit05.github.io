# 飞书风格富文档模板实现计划

## 概述

为 Hugo + PaperMod 博客搭建一套飞书风格的暗色富文档组件系统，通过自定义 Shortcode + CSS 实现。用户在 Markdown 文章中调用 shortcode 即可使用各种文档块功能，保持黑色主色调和简约设计语言。

## 当前状态分析

- 已有 5 个 shortcode：video、model、mermaid、game、download
- CSS 统一风格：深色背景(#0a0a0a/#111)、细边框(1px solid #1e1e1e)、4px 圆角、hover 变亮
- 懒加载模式：`.Page.Store.Set/Get` + baseof.html 条件加载外部 JS
- Markup 已开启 `unsafe = true`，支持原始 HTML

## 新增组件清单（14 个 Shortcode）

### 1. 提示框 Callout — `callout.html`
飞书最核心的组件，4 种类型：提示(info)、警告(warning)、注意(caution)、技巧(tip)

**调用方式**：
```markdown
{{</* callout type="info" */>}}
这是一条提示信息
{{</* /callout */>}}

{{</* callout type="warning" title="注意" */>}}
警告内容
{{</* /callout */>}}
```

**参数**：
- `type`：info / warning / caution / tip（默认 info）
- `title`：可选标题（默认根据 type 显示对应标题）

**样式**：左侧彩色竖条 + 图标 + 内容，暗色背景微调

---

### 2. 标签页 Tabs — `tabs.html` + `tab.html`
内容分组切换，类似飞书的多标签页

**调用方式**：
```markdown
{{</* tabs */>}}
{{</* tab name="Python" */>}}
Python 代码内容
{{</* /tab */>}}
{{</* tab name="JavaScript" */>}}
JS 代码内容
{{</* /tab */>}}
{{</* /tabs */>}}
```

**实现**：纯 CSS + 少量内联 JS 切换，每个 tab 有唯一 ID

---

### 3. 折叠区域 Details — `details.html`
可折叠/展开的内容块

**调用方式**：
```markdown
{{</* details title="点击展开详情" */>}}
折叠的内容
{{</* /details */>}}

{{</* details title="默认展开" open="true" */>}}
已展开的内容
{{</* /details */>}}
```

**参数**：
- `title`：折叠标题（必填）
- `open`：是否默认展开（默认 false）

**实现**：基于 `<details>/<summary>` 原生 HTML，CSS 美化

---

### 4. 多列布局 Columns — `columns.html` + `column.html`
两列或三列并排布局

**调用方式**：
```markdown
{{</* columns */>}}
{{</* column */>}}
左列内容
{{</* /column */>}}
{{</* column */>}}
右列内容
{{</* /column */>}}
{{</* /columns */>}}
```

**实现**：CSS Grid 或 Flexbox 布局

---

### 5. 功能卡片 Card — `card.html`
带标题、描述和可选链接的卡片

**调用方式**：
```markdown
{{</* card title="PyTorch" link="https://pytorch.org" */>}}
开源机器学习框架
{{</* /card */>}}
```

**参数**：
- `title`：卡片标题
- `link`：可选链接
- `image`：可选图片 URL

---

### 6. 时间线 Timeline — `timeline.html` + `step.html`
步骤/时间线展示

**调用方式**：
```markdown
{{</* timeline */>}}
{{</* step title="第一步" date="2026-07" */>}}
完成基础搭建
{{</* /step */>}}
{{</* step title="第二步" date="2026-08" */>}}
发布上线
{{</* /step */>}}
{{</* /timeline */>}}
```

---

### 7. 徽章 Badge — `badge.html`
小标签/状态标记

**调用方式**：
```markdown
{{</* badge text="新功能" color="green" */>}}
{{</* badge text="重要" color="red" */>}}
{{</* badge text="进行中" */>}}
```

**参数**：
- `text`：徽章文字
- `color`：green / red / blue / yellow / gray（默认 blue）

---

### 8. 按钮 Button — `button.html`
美化的操作按钮

**调用方式**：
```markdown
{{</* button text="查看文档" link="/learn/" */>}}
{{</* button text="下载" link="/files/guide.pdf" style="outline" */>}}
```

**参数**：
- `text`：按钮文字
- `link`：链接地址
- `style`：filled / outline（默认 filled）

---

### 9. 进度条 Progress — `progress.html`
进度指示器

**调用方式**：
```markdown
{{</* progress value="75" label="学习进度" */>}}
```

**参数**：
- `value`：0-100 进度值
- `label`：可选标签文字

---

### 10. 引用块 Quote — `quote.html`
美化引用块，带作者和来源

**调用方式**：
```markdown
{{</* quote author="Linus Torvalds" source="Linux" */>}}
Talk is cheap. Show me the code.
{{</* /quote */>}}
```

**参数**：
- `author`：可选作者
- `source`：可选来源

---

### 11. 画廊 Gallery — `gallery.html`
多图网格展示

**调用方式**：
```markdown
{{</* gallery */>}}
![图片1](/images/pic1.jpg)
![图片2](/images/pic2.jpg)
![图片3](/images/pic3.jpg)
{{</* /gallery */>}}
```

**实现**：CSS Grid 自适应网格，图片可点击放大

---

### 12. 代码块 Code Group — `codegroup.html` + `codefile.html`
多文件代码分组（飞书常见的代码标签页）

**调用方式**：
```markdown
{{</* codegroup */>}}
{{</* codefile name="main.py" */>}}
```python
print("hello")
```
{{</* /codefile */>}}
{{</* codefile name="config.json" */>}}
```json
{"key": "value"}
```
{{</* /codefile */>}}
{{</* /codegroup */>}}
```

**实现**：复用 tabs 的切换逻辑，但样式针对代码块优化

---

### 13. 分割线 Divider — `divider.html`
带文字的分割线

**调用方式**：
```markdown
{{</* divider text="以上是背景介绍" */>}}
```

---

### 14. 嵌入 Embed — `embed.html`
嵌入外部网页（iframe 美化版）

**调用方式**：
```markdown
{{</* embed url="https://example.com" title="示例网站" */>}}
```

**参数**：
- `url`：嵌入 URL
- `title`：标题
- `height`：高度（默认 400px）

---

## 需要修改的文件

### 新建文件（Shortcodes）
1. `layouts/shortcodes/callout.html`
2. `layouts/shortcodes/tabs.html`
3. `layouts/shortcodes/tab.html`
4. `layouts/shortcodes/details.html`
5. `layouts/shortcodes/columns.html`
6. `layouts/shortcodes/column.html`
7. `layouts/shortcodes/card.html`
8. `layouts/shortcodes/timeline.html`
9. `layouts/shortcodes/step.html`
10. `layouts/shortcodes/badge.html`
11. `layouts/shortcodes/button.html`
12. `layouts/shortcodes/progress.html`
13. `layouts/shortcodes/quote.html`
14. `layouts/shortcodes/gallery.html`
15. `layouts/shortcodes/codegroup.html`
16. `layouts/shortcodes/codefile.html`
17. `layouts/shortcodes/divider.html`
18. `layouts/shortcodes/embed.html`

### 修改文件
1. `assets/css/extended/custom.css` — 添加所有新组件的暗色样式
2. `layouts/baseof.html` — 添加 tabs/codegroup 的轻量 JS 切换逻辑

### 新建文件（演示文档）
1. `content/learn/doc-template-guide.md` — 功能使用指南文档

## 样式设计原则

- 保持现有暗色设计语言：`#0a0a0a` 背景、`#111` 卡片、`#1e1e1e` 边框
- Callout 左侧彩色竖条：info=#3b82f6(蓝)、warning=#f59e0b(琥珀)、caution=#ef4444(红)、tip=#10b981(绿)
- 所有组件统一 `border-radius: 4px`，与现有风格一致
- hover 效果保持统一：边框变亮 + 文字变白
- 字重偏好 `font-weight: 300`，与现有风格一致
- 徽章颜色用半透明背景 + 对应色文字，避免在暗色主题下过于刺眼

## 实施步骤

1. 创建所有 18 个 shortcode 文件
2. 在 custom.css 中添加所有新组件样式
3. 在 baseof.html 中添加 tabs/codegroup 的切换 JS
4. 创建使用指南文档
5. 本地构建验证

## 验证步骤

1. `hugo server` 启动本地预览
2. 在指南文档中测试每个组件的渲染效果
3. 检查暗色主题下各组件的可读性
4. 检查移动端响应式布局
5. 构建成功后推送到 GitHub

## 假设与决策

- Tabs 切换使用轻量内联 JS（~20行），不引入前端框架
- Gallery 图片放大使用 CSS `:target` 或简单 JS，不引入 lightbox 库
- 代码块分组(codegroup)复用 tabs 切换逻辑，仅样式不同
- 所有 shortcode 的 Inner 内容支持 Markdown 渲染（使用 `.Inner` 而非 `.Inner | safeHTML`）
- Badge 是自闭合标签（无 Inner），Button 也是自闭合标签
