# Anatomy 典型用法示例 | Example Workflows

个人学习整理，配合主 README 使用。命令与示例名以官方 README 为准。

## 1. 给技术文档配一张讲解图

1. 先装好 skill：`npx skills add wheresryan22/anatomy -g -a claude-code`。
2. 在 Claude Code 里下单，只给概念和真实数字：

```text
/anatomy a figure for our Next.js docs on database connection pooling: a pool of 10 connections, requests borrow one and give it back, and when all 10 are busy new requests wait in a queue. A React component plus a static HTML preview, dark theme.
```

3. 等它走完构建与自检（小图也要几分钟），先看静态预览确认视角和配色，再让它微调数字或零件。
4. 产出是源码（构建脚本 + 页面 / React 组件），直接进你的仓库，不是临时图片。

English: Give the concept and real numbers, let it invent the machine, review the static preview, then ship the source it generates.

## 2. 先跑最小示例校准风格

1. 克隆上游仓库，进 `examples/dial-indicator` 跑 `node build.mjs`（约 300 行，最小示例）。
2. 加 `--light` 再跑一遍，对比双主题效果。
3. 风格对味了，再去跑 arcade-cabinet 或 raptor-engine 这种大图；不对味先别上大图，返工贵。

English: Build the tiny dial-indicator example first (both themes), calibrate the look, then spend minutes on the big figures.

## 3. 讲一台真机器的内部原理（工程/汽修题材）

```text
/anatomy a heat-exchanger espresso machine with the side panel off: boiler, heat-exchanger tube, group head, pump, steam wand and gauge. Show the water flowing when you pull a shot. Standalone HTML, light theme.
```

要点：点名实物 + 列全总成清单 + 说清哪个动作要动（拉杆出水）+ 指定产出形式和主题。这类「概念本身就是机器」的题材出图质量最高。

English: Name the real object, list its assemblies, say what should move, and pick the output format and theme.

## 4. 发到社区画廊

图做好后对智能体说「publish this figure to the Anatomy community gallery」：它会先展示要提交的标题与署名，你确认后它替你向上游 anatomy-community 仓开 PR，不用手动 fork。

English: Ask the agent to publish; it shows what it will send first and opens the PR only after your yes.
