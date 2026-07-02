+++
date = '2026-07-02'
draft = false
title = 'Mermaid 思维导图示例'
tags = ["工具", "思维导图"]
categories = ["学习"]
+++

## 思维导图

在文章中使用 `{{</* mermaid */>}}` 短代码即可插入思维导图：

{{< mermaid >}}
mindmap
  root((学习路线))
    前端
      HTML/CSS
      JavaScript
      React/Vue
    后端
      Python
      Go
      数据库
    工具
      Git
      Docker
      Linux
{{< /mermaid >}}

## 流程图

Mermaid 也支持流程图：

{{< mermaid >}}
graph TD
    A[开始学习] --> B{选择方向}
    B -->|前端| C[HTML/CSS/JS]
    B -->|后端| D[Python/Go]
    C --> E[框架实战]
    D --> F[项目开发]
    E --> G[部署上线]
    F --> G
{{< /mermaid >}}
