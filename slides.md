---
marp: true
theme: ai-share
paginate: true
title: AI 工具的使用分享
---

# 从打通 aisbench 测试说起

<div class="flow">
<span class="step">①</span><span class="node">运行 aisbench<small>人</small></span><span class="arrow">→</span><span class="node">提取数据<small>人手动抠</small></span><span class="note">起点：全手动</span>
<span class="step">②</span><span class="node">运行 aisbench<small>人</small></span><span class="arrow">→</span><span class="node ai">提取数据<small>独立 py，人来跑</small></span><span class="note">agent 写独立 py，替换<strong>提取数据</strong></span>
<span class="step">③</span><span class="node script">运行 aisbench<small>人</small></span><span class="arrow">→</span><span class="node ai">提取数据<small>脚本末尾自动跑</small></span><span class="note">agent 把 py 整合到测试脚本末尾，替换<strong>人来跑 py</strong></span>
<span class="step">④</span><span class="node ai script">运行 aisbench<small>agent</small></span><span class="arrow">→</span><span class="node ai">提取数据<small>脚本末尾自动跑</small></span><span class="note">稳定后交给 agent，替换<strong>运行 aisbench</strong></span>
</div>

---

# AI：执行力极强的新同事

<svg class="diagram" viewBox="0 0 1160 500" width="1160" height="500">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-arrow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<path class="ai" d="M190 270C240 270 240 110 288 110"/><path d="M190 270H290"/><path d="M190 270C240 270 240 430 290 430"/>
<path class="ai" d="M520 110C565 110 565 60 608 60"/><path d="M520 110C565 110 565 160 610 160"/>
<path d="M520 270C565 270 565 235 610 235"/><path d="M520 270C565 270 565 305 610 305"/>
<path d="M520 430C565 430 565 395 610 395"/><path d="M520 430C565 430 565 465 610 465"/>
<path class="ai" d="M740 60C785 60 785 25 828 25"/><path d="M740 60C785 60 785 95 830 95"/>
<path class="ai more" d="M960 25H1010"/><text class="ai-note" x="1020" y="25" text-anchor="start">…</text>
<g><rect x="0" y="242" width="190" height="56" rx="8"/><text x="95" y="270">遇到问题</text></g>
<g class="ai"><rect x="290" y="82" width="230" height="56" rx="8"/><text x="405" y="110">① 业界最常见</text></g>
<g><rect x="290" y="242" width="230" height="56" rx="8"/><text x="405" y="270">② 次常见</text></g>
<g class="hit"><rect x="290" y="402" width="230" height="56" rx="8"/><text x="405" y="430">③ 我们实际的问题</text></g>
<g class="ai small"><rect x="610" y="38" width="130" height="44" rx="8"/><text x="675" y="60">第一条</text></g>
<g class="small"><rect x="610" y="138" width="130" height="44" rx="8"/></g>
<g class="small"><rect x="610" y="213" width="130" height="44" rx="8"/></g>
<g class="small"><rect x="610" y="283" width="130" height="44" rx="8"/></g>
<g class="small"><rect x="610" y="373" width="130" height="44" rx="8"/></g>
<g class="small"><rect x="610" y="443" width="130" height="44" rx="8"/></g>
<g class="ai small"><rect x="830" y="3" width="130" height="44" rx="8"/><text x="895" y="25">第一条</text></g>
<g class="small"><rect x="830" y="73" width="130" height="44" rx="8"/></g>
<text class="note ai-note" x="810" y="170">没有上下文规定时，</text><text class="note ai-note" x="810" y="204">AI 永远走第一条</text>
<text class="note hit-note" x="810" y="414">我们实际的问题</text><text class="note hit-note" x="810" y="448">在第三条</text>
</svg>

---

# 逐步把任务流程节点交给 AI

<svg class="diagram" viewBox="0 0 1160 545" width="1160" height="545">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<g transform="translate(60 0)">
<path class="bracket" d="M0 112V104H350V112"/><text class="label ai-note" x="175" y="80">已交给 AI</text>
<path class="bracket" d="M400 112V104H550V112"/><text class="label ai-note" x="475" y="80">正在交</text>
<path class="bracket" d="M810 112V104H960V112"/><text class="label" x="885" y="80">还没交</text>
<path class="flow" d="M150 182H198"/><path class="flow" d="M350 182H398"/><path class="flow" d="M550 182H594"/><path class="flow" d="M744 182H808"/><path class="flow" d="M960 182H1000"/><text x="1022" y="182">…</text>
<path class="flow" d="M670 236C670 330 730 380 809 380"/><path class="flow" d="M959 380H1000"/><text x="1022" y="380">…</text>
<g class="ai"><rect x="0" y="150" width="150" height="64" rx="8"/><text x="75" y="182">执行</text></g>
<g class="ai"><rect x="200" y="150" width="150" height="64" rx="8"/><text x="275" y="182">执行</text></g>
<g class="doing"><rect x="400" y="150" width="150" height="64" rx="8"/><text x="475" y="182">执行</text></g>
<g class="human"><polygon points="670,128 744,182 670,236 596,182"/><text x="670" y="182">决策</text></g>
<g><rect x="810" y="150" width="150" height="64" rx="8"/><text x="885" y="182">执行</text></g>
<g class="human"><polygon points="885,326 959,380 885,434 811,380"/><text x="885" y="380">决策</text></g>
<path class="bracket" d="M596 112V104H744V112"/><text class="label human-note" x="670" y="80">留给人</text><text class="label human-note" x="885" y="462">留给人</text>
<text class="caption" x="520" y="520">执行节点一个个<tspan class="ai-note">交给 AI</tspan>，决策节点<tspan class="human-note">留给人</tspan></text>
</g>
</svg>

---

# 编程 Agent: 哪些能替换成 AI

把编码交给 AI：上下文影响智力，提示词影响方向；决策留给人。

<svg class="diagram" viewBox="0 0 1160 350" width="1160" height="350">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<path class="bracket" d="M0 100V92H140V100"/><text class="label ai-note" x="70" y="68">能替换成 AI</text>
<path class="bracket" d="M180 100V92H500V100"/><text class="label ai-note" x="340" y="68">一次做不对，要人给上下文</text>
<path class="bracket" d="M540 100V92H860V100"/><text class="label ai-note" x="700" y="68">能替换成 AI</text>
<path class="bracket" d="M900 100V92H1060V100"/><text class="label human-note" x="980" y="68">要人决策</text>
<path class="flow" d="M140 182H178"/><path class="flow" d="M320 182H358"/><path class="flow" d="M500 182H538"/><path class="flow" d="M680 182H718"/><path class="flow" d="M860 182H898"/><path class="flow" d="M1060 182H1098"/><text x="1128" y="182">合入</text>
<path class="flow" d="M980 238C980 320 250 320 250 216"/><text class="label" x="615" y="322">打回</text>
<g class="ai"><rect x="0" y="150" width="140" height="64" rx="8"/><text x="70" y="182">代码拉取</text></g>
<g class="doing"><rect x="180" y="150" width="140" height="64" rx="8"/><text x="250" y="182">修改代码</text></g>
<a href="https://github.com/tu10ng/ai-tool-share/blob/main/skills/lwd-code-walkthrough/SKILL.md" target="_blank"><g class="doing"><rect x="360" y="150" width="140" height="64" rx="8"/><text x="430" y="182">代码串讲 ↗</text></g></a>
<g class="ai"><rect x="540" y="150" width="140" height="64" rx="8"/><text x="610" y="182">代码提交</text></g>
<g class="ai"><rect x="720" y="150" width="140" height="64" rx="8"/><text x="790" y="182">gh 提 PR</text></g>
<g class="human"><polygon points="980,126 1060,182 980,238 900,182"/><text x="980" y="182">代码检视</text></g>
</svg>

---

# 编程 Agent: 上下文影响智力

<svg class="diagram" viewBox="0 0 1160 550" width="1160" height="550">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-arrow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<text class="note" x="0" y="40">上下文用到 50%</text>
<rect x="190" y="18" width="360" height="44" rx="6"/><g class="ai"><rect x="190" y="18" width="180" height="44" rx="6"/></g>
<path class="flow" d="M560 40H598"/><g><rect x="610" y="12" width="180" height="56" rx="8"/><text x="700" y="40">问同一个问题</text></g><path class="flow" d="M800 40H838"/><text class="note hit-note result" x="850" y="40">✗ 可能说错</text>
<path class="ai more-arrow" d="M280 68V142"/><text class="note ai-note" x="296" y="105">压缩上下文</text>
<text class="note" x="0" y="170">压缩之后</text>
<rect x="190" y="148" width="360" height="44" rx="6"/><g class="ai"><rect x="190" y="148" width="44" height="44" rx="6"/></g>
<path class="flow" d="M560 170H598"/><g><rect x="610" y="142" width="180" height="56" rx="8"/><text x="700" y="170">问同一个问题</text></g><path class="flow" d="M800 170H838"/><text class="note ai-note result" x="850" y="170">✓ 分析正确</text>
<text class="label note" x="0" y="430">每轮发给 api</text><text class="label note" x="0" y="460">的上下文</text>
<g class="ai"><rect x="190" y="493" width="48" height="22" rx="3"/></g><text class="label small-label" x="214" y="534">第1轮</text>
<g class="old"><rect x="266" y="493" width="48" height="22" rx="3"/></g><g class="ai"><rect x="266" y="468" width="48" height="22" rx="3"/></g><text class="label small-label" x="290" y="534">第2轮</text>
<g class="old"><rect x="342" y="493" width="48" height="22" rx="3"/></g><g class="old"><rect x="342" y="468" width="48" height="22" rx="3"/></g><g class="ai"><rect x="342" y="443" width="48" height="22" rx="3"/></g><text class="label small-label" x="366" y="534">第3轮</text>
<g class="old"><rect x="418" y="493" width="48" height="22" rx="3"/></g><g class="old"><rect x="418" y="468" width="48" height="22" rx="3"/></g><g class="old"><rect x="418" y="443" width="48" height="22" rx="3"/></g><g class="ai"><rect x="418" y="418" width="48" height="22" rx="3"/></g><text class="label small-label" x="442" y="534">第4轮</text>
<g class="old"><rect x="494" y="493" width="48" height="22" rx="3"/></g><g class="old"><rect x="494" y="468" width="48" height="22" rx="3"/></g><g class="old"><rect x="494" y="443" width="48" height="22" rx="3"/></g><g class="old"><rect x="494" y="418" width="48" height="22" rx="3"/></g><g class="ai"><rect x="494" y="393" width="48" height="22" rx="3"/></g><text class="label small-label" x="518" y="534">第5轮</text>
<g class="old"><rect x="570" y="493" width="48" height="22" rx="3"/></g><g class="old"><rect x="570" y="468" width="48" height="22" rx="3"/></g><g class="old"><rect x="570" y="443" width="48" height="22" rx="3"/></g><g class="old"><rect x="570" y="418" width="48" height="22" rx="3"/></g><g class="old"><rect x="570" y="393" width="48" height="22" rx="3"/></g><g class="ai"><rect x="570" y="368" width="48" height="22" rx="3"/></g><text class="label small-label" x="594" y="534">第6轮</text>
<g class="old"><rect x="646" y="493" width="48" height="22" rx="3"/></g><g class="old"><rect x="646" y="468" width="48" height="22" rx="3"/></g><g class="old"><rect x="646" y="443" width="48" height="22" rx="3"/></g><g class="old"><rect x="646" y="418" width="48" height="22" rx="3"/></g><g class="old"><rect x="646" y="393" width="48" height="22" rx="3"/></g><g class="old"><rect x="646" y="368" width="48" height="22" rx="3"/></g><g class="ai"><rect x="646" y="343" width="48" height="22" rx="3"/></g><text class="label small-label" x="670" y="534">第7轮</text>
<text class="note" x="760" y="360">每一轮都把整个上下文发给 api</text>
<text class="note hit-note" x="760" y="400">decode 线性变慢，更花钱</text>
<g class="ai"><rect x="760" y="440" width="340" height="56" rx="8"/><text x="930" y="468">尽量用 subagent + spec plan</text></g>
<text class="label small-label note" x="760" y="534">紫色是这一轮新增的，灰色是之前的又发一遍</text>
</svg>

---

# 编程 Agent: 提示词影响方向

## 反向表述不适合主流模型，要**正着写**

- 不要写成：“不要用 powershell 处理文本”
- 要写成：“请你用 python 处理文本而不是 powershell”
- “不是……而是……”这类句式可以参考

---

# 验证 Agent: 最不可信的执行者

<style scoped>section { font-size: 24px; } section h1 { font-size: 40.3px; }</style>

把验证一步步交给 AI：AI 不可信，要用工程手段控制它；脚本化仍是重点，经验写成 markdown 最简洁。

## 每一步跑完，谁来验？

- 软件工程一直默认开发者不可信：“单元测试过了，应该没问题吧”

## AI 是最不可信的执行者

- 和人天生不对齐
- 在细枝末节上疯狂出力，对要紧的视而不见
- 对说不清的结论很自信
- 你希望它传输 docker 镜像时空间不足就询问你该怎么办，它可能为了快速完成任务，直接把 docker 服务的存储空间搬位置了
- 配置环境和服务器信息要写到记忆文件里

---

# 验证 Agent: 用工程手段控制它

## 每一步都这样要求它

> 先检查当前状态，只推进一个明确的步骤，然后验证并评估结果。

- 靠上下文防止走偏，不过就打回

## 检查要它自己做得了

- 配置环境、拉取代码，上环境拉起服务并测试
- dsh、terminal、蓝区黄区信息传输
- 这叫**工具化**
- 例子：反向代理配置

---

# 验证 Agent: 脚本化仍是重点

## 古法编程

- 重复的步骤写成脚本，不靠人记、不靠人守

## 交给 AI 也一样

- 检查写进脚本，跑完就知道过没过
- 不同的是 AI 改脚本很快，流程一变马上跟上
- 恭喜，你发明了**脚本化**
- 测试脚本要能把关键参数指定为命令行参数，并且输出是固定的、可直接获取的

---

# 验证 Agent: skill 和 markdown

## 叮嘱写在对话里会被稀释

- 把验证过程的经验总结下来
- 写到它每次都看得见的地方

## skill 是个假大空的概念

- 落地就是一份 markdown
- 与其追概念，不如直接写 markdown：最简洁快速
- 这就是**规范化**
- 我的验证用 CLAUDE.md

---

# 实际例子: 回顾

逐步替换人工流程。

## 前两章

- 上下文喂对，它才做得对
- 验证看得见摸得着，它才知道自己对不对

## 两样都有了

- 如何将已有的流程转化为 AI 操作？

---

# 实际例子: 一个全套流程

## 一截一截从我手里交出去

- 代理配置
- 容器拉取
- scp 和 sshpass
- 写进 claude.md
- 【例子】

## 交出去以后，我只在分叉上说一句话

> 直接重启容器，别定位了，这样最干净；如果重启容器了仍然有 vllm 进程或者显存占用，就停下来找我做决定。

---

# 当真的都交给 AI

## 回到 aisbench

- 每长一截，都是把一个人工节点交给 AI
- AI 能提升人处理任务的效率：逐步把人处理的任务流程节点交给 AI

## 人手里只剩决策

- 一个人同时推进好几条任务，效率到一个恐怖的程度
- 最后的限制是**环境数量**：每条任务都要上环境验证

---

# 多 agent 并行时，人怎么管

## 并行的任务、并行的上下文

- 哪条走到哪、哪条停在分叉上等我，要一眼看到
- 在几条线之间来回切，人的上下文也成了瓶颈
- 管道多了，用 todo 工作树当 dashboard
- worktree、隔离

## 要不要开发专门的软件？

- dsh、todo 工作树

回去挑一个自己的重复流程，转成 AI 操作。
