# 🎓 IETF 125 CATALIST BoF 参会笔记：AI Agent 网络协议体系(Coordinating Agent To Agent List of efforts)

> **会议**：CATALIST BoF（形成工作组前的议题讨论会）  
> **时间**：2026年3月18日  
> **地点**：中国 深圳  
> **主题**：AI Agent 网络协议体系  

---

## 一、会议背景

CATALIST 是一个 BoF（birds of a feather），目的是探讨是否需要在 IETF 成立新的工作组来标准化 AI Agent 相关的网络协议。本次会议共有 5 个演讲，从不同角度阐述 AI Agent 网络协议的需求、挑战和可能的解决方案。

---

## 二、演讲一：Network Architecture for AI Ecosystem

**演讲人**：Arashmid Akhavain (Huawei) 等  
**标题**：*Agents & AI ecosystem*

### 2.1 核心目的(画一个大框架)

提出一个消费者-提供者覆盖网络架构，支持智能体交互、AI训练工作流、AI推理工作流、生态组件发现、跨域互操作<br>
这个架构的目的是**识别需要标准化的领域**，而不是成为标准本身。

### 2.2 目标

<br>1. 识别AI生态中IETF可以标准化的机会<br>2. 识别共同工作项及其讨论场所<br>3. 区分智能体特有的工作项和与其他AI服务共有的工作项<br>4. 帮助建立专注于智能体的工作组 

### 2.3 IETF 内可能的工作


 **智能体特有工作**：标准化智能体通信协议、会话管理、多模态数据平面、API<br>**AI服务共有工作**：发现、注册、认证、授权等 

### 2.4 工作进展

- 已在 IETF 122、123、124 举办 side meeting；
- 已有多个 I-D；
- 讨论在 agent-2-agent 邮件列表；
- 计划推动成立智能体工作组 

---

## 三、演讲二：AI Agent Discovery

**演讲人**：Roland Schott (Telekom), Nic Williams (Infoblox)  
**标题**：*AI Agent Discovery*

### 3.1 核心问题

智能体之间如果不知道彼此的存在，就无法交互

### 3.2 目标与原则

 **目标**：去中心化的智能体间发现<br>
 **原则**：避免互联网碎片化，避免被围墙花园锁定，复用现有技术，最小化扩展 

### Tips（我的理解）
这思路挺巧的——DNS 已经跑了几十年，全世界都在用，直接拿来用比从头开始更靠谱。就像找网站用域名，以后找 AI 智能体也用域名。

### 3.3 技术方案

 **基于DNS的解决方案**：<br>- 组织内已知入口点：`index._agents.example.com`<br>- 智能体记录：`chat._agents.example.com` 的 SVCB 记录<br>- 通过参数表达智能体能力（JSON model card URI、成本、位置等） 

### 3.4 技术细节

将发现问题分为：-已知服务和域、仅已知服务、仅已知域、全未知<br>- 元数据：model card URI、成本、位置、模态等<br>- 需要 IANA 预留 `_agents` 子域和 SVCB 参数 

### 3.5 工作进展

 已有 draft-mozley-aidiscovery 和 draft-mozleywilliams-dnosp-bandaid；计划在 IETF 126 发起 BoF 

---

## 四、演讲三：DMSC (Dynamic Multi-agent Secured Collaboration)

**演讲人**：王爱俊 (中国电信) 等  
**标题**：*DMSC (Dynamic Multi-agent Secured Collaboration)*

### 4.1 核心目的

 标准化跨管理域的 AI 智能体协作架构和协议套件 

### 4.2 技术架构

**AI Agent Gateway (AGW)** 的基础设施架构，连接不同域的智能体 

### 4.3 技术要点

- 定义基于 AI Agent GW 的基础设施架构<br>- 定义端到端安全协作的协议套件<br>- 强调**语义路由/自然语言**在智能体协作中的应用

### 4.4 协议套件

 **MACP (Multi-agent Collaboration Protocol Suite)**：包含 ARP/AAAP/TIP/NLIP 等协议 

### 4.5 IETF 内可能的工作

 - 现有协议适用性：DNS<br>- 现有协议扩展：路由协议<br>- 全新协议：ARP/AAAP/TIP/NLIP 等

### Tips 我的理解
这有点像现在的电子邮件：我用 Outlook，对方用 Gmail，我们能互相发邮件是因为有 SMTP 协议。DMSC 想做智能体界的 SMTP——不管我的智能体是哪个公司做的，只要接了这个网关，就能和其他域的智能体聊天。

他们特别强调**语义路由**和**自然语言**。意思是智能体之间不一定用严格的 API 格式，可能直接发一段自然语言，网关负责理解、转发。这个挺前卫的——以后智能体聊天可能像人一样，“你能帮我订个酒店吗”这种话直接发过去，对方智能体自己理解。

### 4.6 工作进展

已有 10+ 个 I-D；讨论在 dmsc@ietf.org 邮件列表；计划在 IETF 126 发起 BoF

---

## 五、演讲四：Agent Communications (private) Internet Protocol - AC(p)IP

**演讲人**：Toerless Eckert (Futurewei) 等  
**标题**：*Agent Communications (private) Internet Protocol - AC(p)IP*

### 5.1 核心场景

参考场景：下一代金融科技（FinTech）——银行、支付网络、数字钱包、商户、ATM 等都有 AI 智能体

### 5.2 技术方案

 **ACIP**：基于智能体 ID/技能/任务的加密数据报层<br>- 功能：路由/负载分担、策略、过滤、日志、复制（组播）<br>- 支持数据报/事务和连接两种模式<br>- 控制平面：用 BGP 新 AF 分发智能体技能

### 5.3 与 HTTP 的区别

现有方案用 HTTP + 一堆中间件（forward proxy, firewall, load-balancer, cache...），ACIP 希望设计一个**轻量级、可被 Tbps 转发引擎处理**的新协议层 

### 5.4 IETF 内可能的工作

 - 新协议：定义 ACIP 协议/功能<br>- 现有协议扩展：BGP、HTTP 等 

### 5.5 工作进展

讨论在 enterprise@ietf.org；已有 I-D：draft-eckert-catalist-acip-framework 等 

---

## 六、演讲五：Agent Communications Gap Analysis and Way Forward

**演讲人**：姚柯晗 (中国移动) 等  
**标题**：*Agent Communications Gap Analysis and Way Forward*

### 6.1 核心目的

通过分析跨域智能体部署的协议需求，推导出 AI 协议的需求；考虑移动网络的动态性和架构要求 

### 6.2 关键用例

具身智能体协作、海量 IoT、自动驾驶、QoS 等 

### Tips 我的理解
相当于给智能体专门造了一个互联网，我发一个包，目的地址是拥有某项技能的智能体。

### 6.3 技术框架

将智能体通信分为四个层次：<br>1. **Agent Identity, AuthN, and AuthZ** (WIMSE/OAuth)<br>2. **Agent Discovery** (DNSOP, INTAREA)<br>3. **Session Management** (可能需要新 WG)<br>4. **Multi-modal Data Transport** (MoQ, WebTransport, MASQUE) 

### 6.4 工作进展

已有 gap analysis draft：draft-yao-catalyst-problem-space-analysis；讨论在 agent2agent@ietf.org 

---

## 七、五个演讲的对比与总结

| 演讲 | 核心提案 | 关键技术点 | 标准化方向 |
|------|---------|-----------|-----------|
| **Network Architecture for AI Ecosystem** | 消费者-提供者覆盖网络架构 | 智能体交互、训练/推理工作流、发现 | 识别标准化机会，推动新WG |
| **AI Agent Discovery** | 基于DNS的智能体发现 | `_agents` 子域、SVCB记录、model card | DNSOP/INTAREA 扩展或新WG |
| **DMSC** | 基于Agent Gateway的跨域协作 | AGW、语义路由、MACP协议套件 | 可能的新WG (DMSC) |
| **AC(p)IP** | 智能体专用私有互联网协议 | 基于技能的路由、轻量级协议层、BGP扩展 | 可能的新WG (INT/RTG) |
| **Gap Analysis** | 四层协议框架 | 身份、发现、会话管理、多模态传输 | 推动协议设计团队 |

---

## 八、我的观察与思考

### 8.1 五个演讲的内在联系

这五个演讲其实在讲同一件事的不同层面：

| 层面 | 解决的问题 | 对应演讲 |
|------|-----------|---------|
| **架构层** | 智能体网络应该长什么样 | Architecture, DMSC |
| **发现层** | 智能体怎么找到彼此 | Discovery |
| **协议层** | 智能体之间怎么通  | ACIP, DMSC (MACP) |
| **分析层** | 我们缺什么以及该做什么 | Gap Analysis |

### 8.2 关键共识

1. **DNS 是智能体发现的基础**——多个演讲都提到用 DNS 做智能体发现
2. **需要区分智能体特有和共有的工作**——身份认证（OAuth）可能是共有的，但智能体通信协议是特有的
3. **语义/自然语言很重要**——DMSC 明确强调语义路由
4. **跨域互操作是核心挑战**——所有演讲都在讨论跨管理域的智能体协作

### 8.3 我的思考：Network for AI 的又一维度

之前我整理过 **Network for AI**（为AI优化网络）和 **AI for Network**（用AI管理网络）的区别。今天的 CATALIST BoF 让我看到 **Network for AI** 的一个新维度：

**为 AI 智能体设计的网络协议**。

这不同于 Mooncake 那种“为AI训练/推理优化网络传输”，而是：
- 让智能体能**发现彼此**
- 让智能体能**安全通信**
- 让智能体能**跨域协作**
- 让智能体能**表达自己的能力和意图**

如果说 Mooncake 解决的是AI 怎么跑得更快，CATALIST 解决的是AI 怎么找到彼此、怎么协作。

### 8.4 Research Direction

| 研究方向 | 核心问题 |
|----------|---------|
| **智能体发现协议** | 如何基于 DNS 设计可扩展的去中心化智能体发现系统 |
| **语义路由协议** | 如何根据智能体的“意图”而不是 IP 地址做路由 |
| **智能体身份与委托链** | 如何让智能体代表用户行动时，权限可传递、可追溯 |
| **跨域智能体协作** | 不同组织的智能体如何安全地协作 |

**去中心化**：把原本由一个中心掌握的控制权（如数据、决策权），分散到网络中的多个参与者手中，让系统不再依赖单一节点就能运行。（我是腾讯/谷歌/阿里的用户，我的数据归它们管=>我是网络中的一个独立节点，我的数据归我管，我跟别人通过协议连接）

---

## My Thoughts

> 在 IETF 125 的 CATALIST BoF 会议上，我看到了互联网标准化社区对 AI 智能体网络协议的早期探索。五个演讲从不同角度阐述了同一个核心问题：**当万亿智能体出现时，它们如何发现彼此、如何安全通信、如何跨域协作？**
>
> 这让我对 **Network for AI** 有了更深的理解——它不仅包括为 AI 训练优化网络传输（如 Mooncake），更包括为 AI 智能体设计全新的网络协议体系。后者可能是更根本的挑战，因为它涉及命名、发现、身份、授权、语义路由等一系列基础问题。
>
> 我注意到几个关键共识正在形成：DNS 作为发现的基础、需要区分智能体特有和共有的工作、语义/自然语言的重要性。这些方向都可能成为我未来研究的切入点。
>
> 这次会议让我看到：互联网正在从“连接主机”走向“连接智能体”，而我正站在这个变革的起点。

---

> **整理时间**：2026年3月  
> **说明**：本笔记基于 IETF 125 CATALIST BoF 公开演讲内容整理。
