# 提案使用与提交说明

本版修订日期：2026-11-20（新加坡时间）；贡献流程沿用 2026-11-11 的核查结果。本包为供提案人审阅的草案，尚未提交。

## 当前贡献流程

1. 依据 https://fg-tida.github.io/.github/ 的新工作项流程，在自己的 GitHub 账号下使用 FG-TIDA/spec-template 创建草案仓库；将本包定制后的源文件放入该仓库。
2. 作者姓名、单位和联系邮箱已按提案人提供的信息填写。正式文号、工作组及批准状态仍未指定。
3. 如需网页发布，将仓库 Settings → Pages 的 Source 设为 GitHub Actions。模板自带流程构建 HTML 和 PDF。
4. 按贡献指南登录 TIDA DataTracker，打开 contribution form，填写标题、摘要，选择目标 Incubation，上传 PDF 或 Markdown（指南允许 PDF、DOCX、PPTX、TXT、Markdown、XML，文件上限 10 MB），并填写草案仓库链接。
5. 提交后的工作项初始状态是 Submitted；Incubation 是提交目标，不是工作项生命周期状态。是否接受及后续组织安排由该流程决定。

贡献指南目前描述了 DataTracker 提交过程，但本次访问的页面没有提供可核验的运行实例链接，因此本包不猜测提交网址。正式提交时应从 FG-TIDA 当前公布的入口或秘书处确认链接进入。

## Mermaid 支持结论

模板快照 7e237a018596e1779d31033464d701ed699c03d5 原生使用 reStructuredText，conf.py 启用 PlantUML，没有启用 Mermaid 扩展。不能直接把 Markdown 的 mermaid 围栏粘贴到 .rst 并期望模板自动画图。

本包采用 Mermaid 源码 → 高分辨率 PNG → RST figure 的兼容方案；HTML 和 PDF 使用同一张图，无须更改模板的图表扩展。源码位于 diagrams/，图位于 src/doc/images/。修改 Mermaid 后须重新渲染 PNG 再构建。Markdown 副本保留可编辑的 Mermaid 围栏，在支持 Mermaid 的阅读器中显示。

## 提案设计重点

- 三项核心要求分别是：权限逐级不扩大、身份与密钥绑定并证明私钥持有、无关授权信息选择性隐藏。
- 隐藏与本次无关的任务分支为基础要求；隐藏父级额度具体值但证明限缩关系为增强研究项。
- 选择性披露不能移除适用的全局约束、禁止项或转授权限制。
- 通用模型由授权主体建立根授权，再由获授权 Agent 向下级 Agent 委托；附录以用户→主 Agent→服务 Agent 示范，终端签名组件不增加授权层级。
- 现有方案已有多级限缩能力；提案聚焦跨域委托、身份及密钥绑定和选择性披露的组合需求，避免夸大创新性。

## 构建

按 CONTRIBUTING.md 安装 Python 和 LaTeX 依赖，执行：

```sh
pip install -r requirements.txt
sphinx-build -W --keep-going -b html src/doc target/html
sphinx-build -W --keep-going -b latex src/doc target/latex
make -C target/latex
```

主贡献文稿来源为 src/doc/frontmatter.rst 和 src/doc/chapters/（index.rst 管理目录）。authoring/ 内 Markdown 为本次编辑来源副本；后续修改应保持两者同步。
