# Anatomy 速查表 | Anatomy Cheatsheet | Guía rápida de Anatomy

> 一页看懂 Anatomy：一个 Claude skill（智能体技能），让 AI 把抽象概念「造成一台能运转的实体机器」来讲给你听——缓存命中变成只有钥匙对了才转的弹子锁，限流变成往外漏水的令牌桶。产出是等距视角的交互图（SVG / WebGL / 3D），零件能动、数字实时读出，截图发到哪都吸睛。

- 上游项目：[wheresryan22/anatomy](https://github.com/wheresryan22/anatomy)（2026-10-19 实测 16,662 ★，MIT 协议）
- 运行环境：Claude Code 为主，也支持 Antigravity、OpenCode、Codex、MiniMax Code（遵循开放 Agent Skills 格式）
- 本页结构：中文主文 → English → Español → Português
- 本速查表为原创撰写（clean-room）：只参照上游公开文档的事实与命令，文字与编排均为重新创作；事实以官方 README 与一手来源为准。

---

## 核心概念

| 概念 | 一句话说明 |
|---|---|
| 概念即机器 | 你说要讲清什么概念，Anatomy 先替这个概念发明一台实体机器：概念的运作方式 = 机器的运转方式 |
| 等距图（isometric） | 统一的等距视角画法，机器像立体模型一样摆在卡片里，能拆开看每个总成 |
| 零件化构建 | 一台机器由几十个小而精确的实体零件拼成（Raptor 发动机约 11 个总成、街机约 240 个实体、15 根线缆） |
| 实时读数（live readout） | 图上显示的每个数字都来自驱动零件运动的同一个小模型，不是贴上去的假数字 |
| 自检审计 | 构建完它会自己放大检查每个接头（audit），3D 模式还有环绕审计 |
| 双主题 | 每张图都有浅色 / 深色两版，构建时可切换 |

## 安装

```bash
# 一行安装（全局）
npx skills add wheresryan22/anatomy -g

# 指定智能体（跳过交互提问）
npx skills add wheresryan22/anatomy -g -a claude-code   # 或 antigravity / opencode / codex / minimax-code
```

不需要 API key，不用 `npm install`：工具包只用 Node 自带模块，零依赖。

## 使用速查

在 Claude Code 里输入 `/anatomy` 并说明要讲什么（Codex 里是 `$anatomy`；Antigravity、OpenCode、MiniMax Code 同样用 `/anatomy`）：

```text
/anatomy explain how a token bucket rate limiter works, interactive
```

不点名也能触发：直接让智能体「画一张等距插图 / 给文档配一张讲解图 / 做一个交互式讲解页」时，它会自动加载这个 skill。

## 提示词写法对照（本页最值钱的部分）

| 你想要的 | 怎么写提示词 |
|---|---|
| 讲清一个机制 | 只说概念 + 给真实数字：「解释令牌桶限流，桶容量 10、每秒补 2 个」，机器让它自己发明 |
| 已有明确机器 | 直接点名实物 + 说清哪里要动：「一台本生灯，开空气环后黄色懒焰变蓝色怒焰」 |
| 用在文档里 | 说明场景 + 格式：「给 Next.js 文档画连接池图：10 条连接、借出归还、全忙时排队，React 组件 + 静态预览，深色」 |
| 用在落地页 | 说明媒介 + 主题：「一张等距 SVG 讲 CDN 边缘缓存，命中 vs 未命中、TTL 60 秒，深色落地页，只要 SVG 和 PNG 预览」 |
| 讲实体设备内部 | 点名设备 + 拆开视角：「半自动咖啡机侧板拆开：锅炉、热交换管、冲煮头、泵、蒸汽棒、压力表，拉杆出水时显示水流，单 HTML，浅色」 |

三条经验（上游官方总结）：

1. **说概念，别说画法**：给概念和真实数字（尺寸、数量、速率、阈值），发明机器是它最擅长、也最占工作量的部分，比你描述方框箭头效果好。
2. **或者直接点名实物**：你已经知道要哪台机器（咖啡机、本生灯、锁），就点名，并说清哪个部件要动。
3. **说清图要住在哪**：独立 HTML 页、单个 SVG 文件、还是 React/Next.js 组件；浅色还是深色——三种产出的构建方式完全不同。

## 现成示例（克隆仓库即可跑）

| 示例 | 讲什么 | 规模 |
|---|---|---|
| dial-indicator | 千分表架在量块车上测尺寸 | 最小示例，约 300 行，先跑这个 |
| desk-computer | 1984 年式台式电脑，键盘能真打字、CRT 显示、关机时画面收成一条线 | 约 85 个实体 |
| arcade-cabinet | 街机侧板拆开：投币滚过投币槽、脉冲沿线缆点亮主板、CRT 预热进演示模式 | 约 240 个实体、15 根线缆 |
| raptor-engine | Raptor 2 火箭发动机试车台：拆成 11 个总成，WebGL 尾焰夹在 SVG 前后层之间 | 参考级，构建要几分钟 |
| ripple-tank | 学校物理课的波纹槽：两层 WebGL 与等距平面对齐 | 教学场景 |

构建命令长这样：`node examples/dial-indicator/build.mjs`（加 `--light` 出浅色版）。

## 环境要求

| 需要 | 用途 | 备注 |
|---|---|---|
| Claude Code / Antigravity / OpenCode / Codex / MiniMax Code 之一 | 一切 | skill 本体 |
| Node.js 20.10+ | 构建与检查 | 只用内置模块，零 npm 依赖 |
| Chrome 或 Chromium | 自检截图 | 无头模式 + WebGL；找不到时设 `CHROME_PATH` |
| React 18+ | 仅 React 产出时 | 其他产出不需要 |

## 局限与常见坑

- **它不是图表库**：没有坐标轴、数据曲线；数字只以「实时读数」和零件的真实尺寸/数量出现。要画数据图请用别的工具。
- **只画机器、仪表、工具、家具**：不画人物和精确地图；一个概念如果没有可造的机制，成品会明显弱一截——先帮它想一个实体比喻再下单。
- **慢是故意的**：一张图要走完零件清单、几何、自检审计、双主题逐个接头特写；Raptor 那种要几分钟，全 3D 环绕审计 30 个零件要 15–20 分钟。别指望秒出。
- **着色器要 WebGL**：没有 WebGL 时 SVG 还能读；系统开了「减少动态」时所有图会静止。
- **3D 模式还是 beta**：只在示例和一张测试图上验证过；小图 60 fps，380 零件的压力图在 1440px 宽约 20 fps。
- **产出是源码不是图片文件**：你拿到的是 Node 构建脚本 + 它生成的页面（或 React 的几何模块 + 组件），图是你自己的资产，可改可商用（MIT）。

## 进阶提示

- 做好的图可以发到官方社区画廊：让智能体说「publish this figure to the Anatomy community gallery」，它会先给你看要发什么、你点头后替你向上游 anatomy-community 仓开 PR。
- 同一概念先跑小示例验证风格，再上大图：先用 dial-indicator 级别的小图确认视角和配色，再让它造复杂机器，返工成本低得多。
- 给工程/汽修类内容配图是它的甜点区：发动机、锁具、量具、泵阀这类「本来就是机器」的题材，概念和实物一对一，出图质量最高。

---

## English (summary)

Anatomy (by wheresryan22, MIT, ~16.7k stars as of 2026-10-19) is a Claude skill — also loadable by Antigravity, OpenCode, Codex and MiniMax Code — that explains an idea by building it as a real, working object: a cache that skips work becomes a pin-tumbler lock, a token bucket becomes an actual leaking bucket. It renders crafted, interactive isometric figures (SVG, WebGL, early-beta 3D) made of dozens of small precise parts, framed in a card with a live readout; every number shown comes from the same model that moves the parts, and the skill audits its own work by zooming into every joint.

Install with one line: `npx skills add wheresryan22/anatomy -g` (add `-a claude-code` etc. to skip the agent prompt). No API keys, nothing to npm install — Node 20.10+ built-ins only; Chrome/Chromium is needed for the screenshot checks. Then type `/anatomy explain how a token bucket rate limiter works, interactive` (in Codex: `$anatomy`).

Prompting rules that matter: name the idea, not the drawing — give the concept plus real numbers and let it invent the machine; or name the object directly and say what should move; and say where the figure will live (standalone HTML, a lone SVG, or a React component; light or dark), because the build differs each time. Eight committed examples include a dial indicator (~300 lines, start here), a 1984 desk computer you can type on, an arcade cabinet with its side panel off, a Raptor 2 engine on a test stand, and a school ripple tank.

Limits: it is not a chart library (no axes or data plots); it draws machines, instruments, tools and furniture — not people or exact maps; it is slow on purpose (minutes per figure, 15–20 min for a full 3D orbit audit of 30 parts); shaders need WebGL, and 3D mode is still beta. Output is source you own — a Node build script plus the page it writes.

---

## Español (guía rápida — traducción de estudio, pendiente de revisión por un hablante nativo)

Anatomy (de wheresryan22, licencia MIT, ~16,7 mil estrellas en octubre de 2026) es una skill de Claude — también cargable en Antigravity, OpenCode, Codex y MiniMax Code — que explica una idea construyéndola como un objeto real que funciona: una caché que evita trabajo se convierte en una cerradura de pines; un limitador de velocidad, en un cubo que gotea. Produce figuras isométricas interactivas (SVG, WebGL y 3D en beta) hechas con decenas de piezas pequeñas y precisas, enmarcadas en una tarjeta con lecturas en vivo; cada número sale del mismo modelo que mueve las piezas, y la propia skill revisa su trabajo ampliando cada unión.

Instalación en una línea: `npx skills add wheresryan22/anatomy -g` (añade `-a claude-code` u otro agente para saltarte la pregunta). Sin claves API y sin `npm install`: solo usa módulos internos de Node 20.10+; Chrome o Chromium hace falta para las capturas de verificación. Después escribe `/anatomy explain how a token bucket rate limiter works, interactive` (en Codex: `$anatomy`).

Cómo pedir bien la figura:

- **Nombra la idea, no el dibujo**: da el concepto y los números reales (tamaños, cantidades, tasas, umbrales) y deja que invente la máquina.
- **O nombra el objeto**: si ya sabes qué máquina quieres (una cafetera espresso, un mechero Bunsen, una cerradura), dilo y aclara qué parte debe moverse.
- **Di dónde vivirá la figura**: página HTML independiente, un SVG suelto o un componente React/Next.js; tema claro u oscuro. La construcción cambia en cada caso.

Ejemplos incluidos: un reloj comparador (el más pequeño, ~300 líneas; empieza por este), un ordenador de sobremesa de 1984 en el que se puede teclear, una máquina recreativa con el panel lateral quitado, un motor cohete Raptor 2 en su banco de pruebas y un tanque de ondas escolar.

Límites honestos: no es una librería de gráficos de datos (sin ejes ni curvas); dibuja máquinas, instrumentos, herramientas y muebles, no personas ni mapas exactos; es lento a propósito (minutos por figura; una auditoría 3D completa de 30 piezas tarda 15–20 minutos); los shaders necesitan WebGL y el modo 3D sigue en beta. El resultado es código fuente tuyo: un script de construcción en Node y la página que genera.

---

## Português (guia rápido — tradução de estudo, aguardando revisão de um falante nativo)

O Anatomy (de wheresryan22, licença MIT, ~16,7 mil estrelas em outubro de 2026) é uma skill do Claude — também carregável no Antigravity, OpenCode, Codex e MiniMax Code — que explica uma ideia construindo-a como um objeto real que funciona: um cache que pula trabalho vira uma fechadura de pinos; um limitador de taxa vira um balde que vaza. Ele gera figuras isométricas interativas (SVG, WebGL e 3D em beta) feitas de dezenas de peças pequenas e precisas, emolduradas num cartão com leituras ao vivo; cada número vem do mesmo modelo que move as peças, e a própria skill confere o trabalho ampliando cada junção.

Instalação em uma linha: `npx skills add wheresryan22/anatomy -g` (adicione `-a claude-code` ou outro agente para pular a pergunta). Sem chaves de API e sem `npm install`: usa só os módulos internos do Node 20.10+; o Chrome ou Chromium é necessário para as capturas de verificação. Depois digite `/anatomy explain how a token bucket rate limiter works, interactive` (no Codex: `$anatomy`).

Como pedir bem a figura:

- **Nomeie a ideia, não o desenho**: passe o conceito e os números reais (tamanhos, quantidades, taxas, limites) e deixe a máquina ser inventada.
- **Ou nomeie o objeto**: se você já sabe qual máquina quer (uma máquina de espresso, um bico de Bunsen, uma fechadura), diga e deixe claro qual parte deve se mover.
- **Diga onde a figura vai morar**: página HTML avulsa, um SVG solto ou um componente React/Next.js; tema claro ou escuro. A construção muda em cada caso.

Exemplos incluídos: um relógio comparador (o menor, ~300 linhas; comece por ele), um computador de mesa de 1984 em que dá para digitar, um fliperama com o painel lateral removido, um motor de foguete Raptor 2 no banco de testes e um tanque de ondas escolar.

Limites honestos: não é uma biblioteca de gráficos de dados (sem eixos nem curvas); desenha máquinas, instrumentos, ferramentas e móveis, não pessoas nem mapas exatos; é lento de propósito (minutos por figura; uma auditoria 3D completa de 30 peças leva 15–20 minutos); os shaders precisam de WebGL e o modo 3D ainda é beta. O resultado é código-fonte seu: um script de build em Node e a página que ele gera.
