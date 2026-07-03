+++
date = '2026-07-03'
draft = false
title = '文档模板功能指南'
tags = ["模板", "指南", "飞书风格"]
categories = ["教程"]
+++

本文档展示了所有可用的飞书风格文档组件及其调用方式。

---

## 1. 提示框 Callout

4 种类型：提示(info)、警告(warning)、注意(caution)、技巧(tip)

{{< callout type="info" >}}
这是一条**提示信息**，用于补充说明重要内容。
{{< /callout >}}

{{< callout type="warning" >}}
这是一条**警告信息**，提醒你注意潜在问题。
{{< /callout >}}

{{< callout type="caution" >}}
这是一条**注意事项**，表示需要特别小心的地方。
{{< /callout >}}

{{< callout type="tip" >}}
这是一条**技巧提示**，帮助你更高效地完成任务。
{{< /callout >}}

**调用方式：**

```
{{</* callout type="info" */>}}
提示内容
{{</* /callout */>}}

{{</* callout type="warning" title="自定义标题" */>}}
警告内容
{{</* /callout */>}}
```

**参数：** `type`（info/warning/caution/tip）、`title`（可选，默认根据类型自动显示）

---

## 2. 标签页 Tabs

{{< tabs >}}
{{< tab name="Python" >}}
```python
print("Hello from Python!")
```
{{< /tab >}}
{{< tab name="JavaScript" >}}
```javascript
console.log("Hello from JavaScript!");
```
{{< /tab >}}
{{< tab name="Go" >}}
```go
fmt.Println("Hello from Go!")
```
{{< /tab >}}
{{< /tabs >}}

**调用方式：**

```
{{</* tabs */>}}
{{</* tab name="Python" */>}}
Python 内容
{{</* /tab */>}}
{{</* tab name="JavaScript" */>}}
JS 内容
{{</* /tab */>}}
{{</* /tabs */>}}
```

---

## 3. 折叠区域 Details

{{< details title="点击展开查看详情" >}}
这是折叠起来的内容，默认收起。你可以在这里放置补充说明、详细步骤等不需要立即展示的信息。
{{< /details >}}

{{< details title="默认展开的折叠区域" open="true" >}}
这个区域默认就是展开的，适合放重要的补充信息。
{{< /details >}}

**调用方式：**

```
{{</* details title="点击展开" */>}}
折叠内容
{{</* /details */>}}

{{</* details title="默认展开" open="true" */>}}
已展开内容
{{</* /details */>}}
```

---

## 4. 多列布局 Columns

{{< columns >}}
{{< column >}}
**左列**

可以放置文字、代码、图片等任何内容。
{{< /column >}}
{{< column >}}
**右列**

多列布局让信息排列更整齐美观。
{{< /column >}}
{{< /columns >}}

**调用方式：**

```
{{</* columns */>}}
{{</* column */>}}
左列内容
{{</* /column */>}}
{{</* column */>}}
右列内容
{{</* /column */>}}
{{</* /columns */>}}
```

支持 2-3 列，内容自动等宽分配。

---

## 5. 功能卡片 Card

{{< card title="PyTorch" link="https://pytorch.org" >}}
开源深度学习框架，支持动态计算图和 GPU 加速。
{{< /card >}}

**调用方式：**

```
{{</* card title="标题" link="https://..." */>}}
卡片描述内容
{{</* /card */>}}
```

**参数：** `title`（标题）、`link`（可选链接）、`image`（可选图片路径）

---

## 6. 时间线 Timeline

{{< timeline >}}
{{< step title="项目启动" date="2026-07" >}}
完成技术选型和项目初始化
{{< /step >}}
{{< step title="核心开发" date="2026-08" >}}
完成主要功能模块开发
{{< /step >}}
{{< step title="正式上线" date="2026-09" >}}
部署并发布上线
{{< /step >}}
{{< /timeline >}}

**调用方式：**

```
{{</* timeline */>}}
{{</* step title="第一步" date="2026-07" */>}}
步骤描述
{{</* /step */>}}
{{</* step title="第二步" date="2026-08" */>}}
步骤描述
{{</* /step */>}}
{{</* /timeline */>}}
```

---

## 7. 徽章 Badge

{{< badge text="新功能" color="green" >}} {{< badge text="重要" color="red" >}} {{< badge text="进行中" color="blue" >}} {{< badge text="待定" color="yellow" >}} {{< badge text="已归档" color="gray" >}}

**调用方式：**

```
{{</* badge text="新功能" color="green" */>}}
{{</* badge text="重要" color="red" */>}}
{{</* badge text="进行中" */>}}
```

**参数：** `text`（文字）、`color`（blue/green/red/yellow/gray，默认 blue）

---

## 8. 按钮 Button

{{< button text="查看学习笔记" link="/learn/" >}} {{< button text="下载文档" link="#" style="outline" >}}

**调用方式：**

```
{{</* button text="查看文档" link="/learn/" */>}}
{{</* button text="下载" link="/files/guide.pdf" style="outline" */>}}
```

**参数：** `text`（文字）、`link`（链接）、`style`（filled/outline，默认 filled）

---

## 9. 进度条 Progress

{{< progress value="75" label="课程学习进度" >}}

{{< progress value="30" label="项目完成度" >}}

**调用方式：**

```
{{</* progress value="75" label="学习进度" */>}}
```

**参数：** `value`（0-100）、`label`（可选标签）

---

## 10. 引用块 Quote

{{< quote author="Linus Torvalds" source="Linux" >}}
Talk is cheap. Show me the code.
{{< /quote >}}

**调用方式：**

```
{{</* quote author="作者名" source="来源" */>}}
引用内容
{{</* /quote */>}}
```

**参数：** `author`（可选作者）、`source`（可选来源）

---

## 11. 画廊 Gallery

用于多图网格展示（需要先在 `static/images/` 放置图片）。

**调用方式：**

```
{{</* gallery */>}}
![描述1](/images/pic1.jpg)
![描述2](/images/pic2.jpg)
![描述3](/images/pic3.jpg)
{{</* /gallery */>}}
```

---

## 12. 代码分组 CodeGroup

{{< codegroup >}}
{{< codefile name="main.py" >}}
```python
def hello():
    print("Hello World")

if __name__ == "__main__":
    hello()
```
{{< /codefile >}}
{{< codefile name="config.json" >}}
```json
{
  "name": "my-project",
  "version": "1.0.0"
}
```
{{< /codefile >}}
{{< /codegroup >}}

**调用方式：**

```
{{</* codegroup */>}}
{{</* codefile name="main.py" */>}}
```python
代码内容
```
{{</* /codefile */>}}
{{</* codefile name="config.json" */>}}
```json
代码内容
```
{{</* /codefile */>}}
{{</* /codegroup */>}}
```

---

## 13. 分割线 Divider

{{< divider text="以上是基础组件" >}}

**调用方式：**

```
{{</* divider text="分割文字" */>}}
```

不加 `text` 参数则为纯分割线。

---

## 14. 嵌入 Embed

**调用方式：**

```
{{</* embed url="https://example.com" title="示例网站" height="400px" */>}}
```

**参数：** `url`（嵌入地址）、`title`（标题）、`height`（高度，默认 400px）

---

## 已有功能（之前已实现）

以下功能继续可用：

| 功能 | 调用方式 |
|------|---------|
| 3D 模型预览 | `{{</* model src="/models/model.glb" */>}}` |
| 文件下载 | `{{</* download src="/files/file.zip" */>}}` |
| 视频播放 | `{{</* video src="/videos/demo.mp4" */>}}` |
| Godot 游戏 | `{{</* game src="/games/mygame/" title="游戏名" */>}}` |
| Mermaid 图表 | `{{</* mermaid */>}} 图表代码 {{</* /mermaid */>}}` |
