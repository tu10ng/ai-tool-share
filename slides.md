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

# 验证 Agent: 用 CLAUDE.md 和记忆持久维护

叮嘱写在对话里会被稀释：把验证过程的经验总结下来，写到它每次都看得见的地方

<svg class="diagram" viewBox="0 0 1160 370" width="1160" height="370">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<path class="flow" d="M232 110H308"/><path class="flow" d="M542 110H618"/><path class="flow" d="M852 110H928"/>
<path class="flow" d="M1045 152C1045 250 115 250 115 152"/><text class="label" x="580" y="264">每次被纠正，就更新一次</text>
<g class="ai"><rect x="0" y="70" width="230" height="80" rx="8"/><text x="115" y="110">会话</text></g>
<g class="human-box"><rect x="310" y="70" width="230" height="80" rx="8"/><text x="425" y="110">被纠正、踩坑</text></g>
<g class="doing"><rect x="620" y="70" width="230" height="80" rx="8"/><text x="735" y="97">写进 CLAUDE.md</text><text class="sub" x="735" y="126">和记忆文件</text></g>
<g class="ai"><rect x="930" y="70" width="230" height="80" rx="8"/><text x="1045" y="110">下次会话自动带上</text></g>
<text class="caption" x="580" y="335">记忆文件不是写一次就完，要<tspan class="hit-note" font-weight="700">持续维护</tspan></text>
</svg>

例子：我的验证用 CLAUDE.md

---

# 验证 Agent: skill 是个假大空的概念

- 落地就是一份 markdown
- 与其追概念，不如直接写 markdown：最简洁快速
- 这就是**规范化**

---

# 实际例子: 配置和使用 agent

逐步替换人工流程。

## 配置

- api 的设置
- 模型的切换

## 工具

- cc
- dsh
- cac

---

# 实际例子: 把流程节点一点点替换成 AI

<svg class="diagram" viewBox="0 0 1160 470" width="1160" height="470">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<path class="bracket" d="M300 88V80H500V88"/><text class="label ai-note" x="400" y="56">编程 agent</text>
<path class="bracket" d="M600 88V80H800V88"/><text class="label ai-note" x="700" y="56">验证 agent</text>
<path class="flow" d="M202 150H298"/><path class="flow" d="M502 150H598"/><path class="flow" d="M802 150H898"/>
<path class="flow" d="M1000 190C1000 270 100 270 100 192"/><text class="label" x="550" y="282">下一个节点</text>
<g><rect x="0" y="112" width="200" height="76" rx="8"/><text x="100" y="150">人做的节点</text></g>
<g class="doing"><rect x="300" y="112" width="200" height="76" rx="8"/><text x="400" y="139">喂上下文</text><text class="sub" x="400" y="166">先能做对</text></g>
<g class="doing"><rect x="600" y="112" width="200" height="76" rx="8"/><text x="700" y="139">写成脚本</text><text class="sub" x="700" y="166">再能自证</text></g>
<g class="ai"><rect x="900" y="112" width="200" height="76" rx="8"/><text x="1000" y="150">交给 AI</text></g>
<g class="ai"><rect x="75" y="360" width="100" height="44" rx="6"/></g><path class="flow" d="M177 382H203"/>
<g class="ai"><rect x="205" y="360" width="100" height="44" rx="6"/></g><path class="flow" d="M307 382H333"/>
<g class="ai"><rect x="335" y="360" width="100" height="44" rx="6"/></g><path class="flow" d="M437 382H463"/>
<g class="doing"><rect x="465" y="360" width="100" height="44" rx="6"/></g><path class="flow" d="M567 382H593"/>
<g><rect x="595" y="360" width="100" height="44" rx="6"/></g><path class="flow" d="M697 382H723"/>
<g><rect x="725" y="360" width="100" height="44" rx="6"/></g><path class="flow" d="M827 382H853"/>
<g><rect x="855" y="360" width="100" height="44" rx="6"/></g><path class="flow" d="M957 382H983"/>
<g><rect x="985" y="360" width="100" height="44" rx="6"/></g>
<text class="label" x="580" y="442">一条流程上的节点，一个个换掉</text>
</svg>

---

# 实际例子: 让 AI 改写 aisbench

<svg class="diagram" viewBox="0 0 1160 360" width="1160" height="360">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<text class="label note ai-note" x="230" y="96">测试脚本（AI 改写）</text>
<rect class="frame" x="230" y="120" width="480" height="140" rx="12"/>
<g><rect x="0" y="154" width="170" height="72" rx="8"/><text x="85" y="177">命令行参数</text><text class="sub" x="85" y="204">指定关键参数</text></g>
<path class="flow" d="M172 190H258"/>
<g class="ai"><rect x="260" y="154" width="180" height="72" rx="8"/><text x="350" y="190">运行 aisbench</text></g>
<path class="flow" d="M442 190H498"/>
<g class="ai"><rect x="500" y="154" width="180" height="72" rx="8"/><text x="590" y="177">提取数据</text><text class="sub" x="590" y="204">py 整合到脚本末尾</text></g>
<path class="flow" d="M712 190H758"/>
<g><rect x="760" y="154" width="180" height="72" rx="8"/><text x="850" y="177">固定输出</text><text class="sub" x="850" y="204">可直接获取</text></g>
<path class="flow" d="M942 190H978"/>
<g class="ai"><rect x="980" y="154" width="170" height="72" rx="8"/><text x="1065" y="190">AI 直接读取</text></g>
</svg>

---

# 实际例子: 让 AI 自己负责测试拉起 vllm

> 直接重启容器，别定位了，这样最干净；如果重启容器了仍然有 vllm 进程或者显存占用，就停下来找我做决定。

<svg class="diagram" viewBox="0 0 1160 330" width="1160" height="330">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<g class="ai"><rect x="0" y="54" width="190" height="72" rx="8"/><text x="95" y="77">直接重启容器</text><text class="sub" x="95" y="104">别定位了</text></g>
<path class="flow" d="M192 90H258"/>
<g class="check"><polygon points="370,20 480,90 370,160 260,90"/><text x="370" y="78">仍有 vllm 进程</text><text x="370" y="104">或显存占用？</text></g>
<path class="flow" d="M482 90H578"/><text class="label" x="530" y="68">没有</text>
<g class="ai"><rect x="580" y="58" width="180" height="64" rx="8"/><text x="670" y="90">拉起 vllm</text></g>
<path class="flow" d="M762 90H838"/>
<g class="ai"><rect x="840" y="58" width="180" height="64" rx="8"/><text x="930" y="90">测试</text></g>
<path class="flow" d="M370 162V238"/><text class="label note" x="386" y="200">有</text>
<g class="human-box"><rect x="260" y="240" width="220" height="64" rx="8"/><text x="370" y="272">停下来找我做决定</text></g>
<text class="label note human-note" x="500" y="272">决策留给人</text>
</svg>

---

# 实际例子: 让 AI 负责全套夜航流程

<svg class="diagram" viewBox="0 0 1160 400" width="1160" height="400">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<path class="moon" d="M488 95A13 13 0 0 0 488 121A7 13 0 0 1 488 95Z"/><text class="label ai-note" x="588" y="108">夜里 AI 自己跑完</text>
<path class="bracket" d="M141 148V140H1015V148"/>
<text class="label human-note" x="55" y="140">人</text><text class="label human-note" x="1101" y="140">人</text>
<g class="human-box small"><rect x="0" y="168" width="110" height="64" rx="8"/><text x="55" y="200">下班</text></g>
<path class="flow" d="M112 200H139"/>
<g class="ai small"><rect x="141" y="168" width="150" height="64" rx="8"/><text x="216" y="200">代理配置</text></g>
<path class="flow" d="M293 200H320"/>
<g class="ai small"><rect x="322" y="168" width="150" height="64" rx="8"/><text x="397" y="200">容器拉取</text></g>
<path class="flow" d="M474 200H501"/>
<g class="ai small"><rect x="503" y="168" width="150" height="64" rx="8"/><text x="578" y="200">scp 和 sshpass</text></g>
<path class="flow" d="M655 200H682"/>
<g class="ai small"><rect x="684" y="168" width="150" height="64" rx="8"/><text x="759" y="200">拉起 vllm</text></g>
<path class="flow" d="M836 200H863"/>
<g class="ai small"><rect x="865" y="168" width="150" height="64" rx="8"/><text x="940" y="200">aisbench 测试</text></g>
<path class="flow" d="M1017 200H1044"/>
<g class="human-box small"><rect x="1046" y="168" width="110" height="64" rx="8"/><text x="1101" y="200">看结果</text></g>
<path class="vline" d="M216 234V300"/><path class="vline" d="M397 234V300"/><path class="vline" d="M578 234V300"/><path class="vline" d="M759 234V300"/><path class="vline" d="M940 234V300"/>
<g class="doing"><rect x="141" y="300" width="874" height="56" rx="8"/><text x="578" y="328">claude.md</text></g>
</svg>

---

# 实际例子: 让 AI 帮忙检视代码

人类要关注：**侵入式修改**，没有最小化改动，不利于长期演进；可能要人类来识别出来

<svg class="diagram" viewBox="0 0 1160 420" width="1160" height="420">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
<clipPath id="venn-community"><circle cx="170" cy="210" r="140"/></clipPath>
</defs>
<circle class="community" cx="170" cy="210" r="140"/>
<circle class="mine" cx="340" cy="210" r="140"/>
<circle class="overlap" cx="340" cy="210" r="140" clip-path="url(#venn-community)"/>
<text x="105" y="210">社区代码</text>
<text class="ai-note" x="410" y="210">AI 的修改</text>
<text class="hit-note result" x="255" y="210">交集</text>
<text class="label" x="880" y="14">人类的识别方法</text>
<g class="ai"><rect x="620" y="40" width="520" height="72" rx="8"/><text x="880" y="76">① AI 把和社区有交集的地方全部整理出来</text></g>
<path class="flow" d="M880 114V168"/>
<g class="ai"><rect x="620" y="170" width="520" height="72" rx="8"/><text x="880" y="206">② AI 讲背景</text></g>
<path class="flow" d="M880 244V298"/>
<g class="human-box"><rect x="620" y="300" width="520" height="72" rx="8"/><text x="880" y="323">③ 人类来过一遍</text><text class="sub" x="880" y="352">识别侵入式修改</text></g>
</svg>

---

# 实际例子: 让 AI 分析方案

<svg class="diagram" viewBox="0 0 1160 450" width="1160" height="450">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<path class="flow" d="M342 100H408"/><path class="flow" d="M752 100H818"/>
<path class="flow" d="M990 162V211H170V258"/>
<path class="flow" d="M342 320H408"/><path class="flow" d="M752 320H818"/>
<g class="ai"><rect x="0" y="40" width="340" height="120" rx="8"/><text x="170" y="84">① AI 理解需求</text><text class="sub" x="170" y="118">拿到需求先让 AI 理解</text></g>
<g class="human-box"><rect x="410" y="40" width="340" height="120" rx="8"/><text x="580" y="76">② 找专家串讲</text><text class="sub" x="580" y="110">拿着你的理解和 AI 的输出</text><text class="sub" x="580" y="136">串讲视频录下来，让 AI 把视频转语音</text></g>
<g class="doing"><rect x="820" y="40" width="340" height="120" rx="8"/><text x="990" y="76">③ 调整 AI 的理解</text><text class="sub" x="990" y="110">串讲会议的全部内容输入给 AI</text><text class="sub" x="990" y="136">人作为中转站</text></g>
<g class="ai"><rect x="0" y="260" width="340" height="120" rx="8"/><text x="170" y="296">④ 编码，上环境测试</text><text class="sub" x="170" y="330">需求确认以后再编码</text><text class="sub" x="170" y="356">上环境测试并解决问题</text></g>
<g class="doing"><rect x="410" y="260" width="340" height="120" rx="8"/><text x="580" y="296">⑤ AI 带你串讲代码</text><text class="sub" x="580" y="330">一个一个 diff 全部理解</text><text class="sub" x="580" y="356">一般要一到两天</text></g>
<g class="human-box"><rect x="820" y="260" width="340" height="120" rx="8"/><text x="990" y="296">⑥ 找专家反串讲</text><text class="sub" x="990" y="330">拿着你的理解（不要带 AI 的输出）</text><text class="sub" x="990" y="356">落实成你自己的理解</text></g>
<g class="ai"><rect x="330" y="415" width="28" height="20" rx="4"/></g><text class="label note" x="368" y="425">AI 做</text>
<g class="doing"><rect x="480" y="415" width="28" height="20" rx="4"/></g><text class="label note" x="518" y="425">人和 AI 一起</text>
<g class="human-box"><rect x="680" y="415" width="28" height="20" rx="4"/></g><text class="label note" x="718" y="425">人找专家</text>
</svg>

---

# 实际例子: 定位问题参考流程

<svg class="diagram" viewBox="0 0 1160 340" width="1160" height="340">
<defs>
<linearGradient id="diagram-ai" x1="0" y1="0" x2="1" y2=".3"><stop offset="0" stop-color="#5c3197" stop-opacity=".94"/><stop offset=".52" stop-color="#8044ab" stop-opacity=".9"/><stop offset="1" stop-color="#5764a2" stop-opacity=".88"/></linearGradient>
<marker id="diagram-flow" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M0 0L10 5L0 10z"/></marker>
</defs>
<g><rect x="0" y="144" width="150" height="72" rx="8"/><text x="75" y="180">日志</text></g>
<path class="flow" d="M152 180H338"/><text class="label" x="245" y="156">400 行日志传输</text>
<g class="ai"><rect x="340" y="144" width="260" height="72" rx="8"/><text x="470" y="180">① ds 的官方对话网站</text></g>
<path class="flow" d="M602 180H668"/>
<g><rect x="670" y="140" width="270" height="80" rx="8"/><text x="805" y="166">② github 开一个 issue</text><text class="sub" x="805" y="198">记录定位过程</text></g>
<path class="flow" d="M942 180C965 180 965 110 988 110"/><path class="flow" d="M942 180C965 180 965 250 988 250"/>
<g><rect x="990" y="82" width="160" height="56" rx="8"/><text x="1070" y="110">后续查找</text></g>
<g><rect x="990" y="222" width="160" height="56" rx="8"/><text x="1070" y="250">分享</text></g>
<text class="label" x="805" y="250">比如 dsv41 的定位 issue</text>
</svg>

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
