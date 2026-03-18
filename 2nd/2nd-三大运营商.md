# 📡 IETF 125 参会笔记：中国三大运营商的前沿视野

> **会议**：IETF 125 OPSAREA 分会  
> **时间**：2026年3月  
> **地点**：中国 深圳    
> **说明**：这是我参加 IETF 125 会议时的学习笔记。中国三大运营商（电信、移动、联通）分享了他们在 AI 时代网络运营的实践与思考。以下是我从演讲 PPT 和现场讲话中梳理的要点，以及作为一个参会者学到的东西。

---

## 📌 重点关注

**不要只看他们做了什么，要听他们遇到了什么瓶颈、想改变什么**。

---

# 中国电信（China Telecom）

## 📍 演讲人
- 孙琼、付英（Qiong Sun, Yu Fu）

## 📍 演讲主题
*OPS Practices and Challenges in the AI Era*

---

## ✅ 一、已落地的关键技术

| 技术 | 说明 | Slide 来源 | 讲话匹配 |
|------|------|------------|----------|
| **云网操作系统（CNOS）** | 自研的智能云网操作系统，支撑云网融合战略 | Slide 5 | "With the help of our Co-OS, we have achieved enormous level from L3 to L4" |
| **数字孪生** | 实时存储运营数据，建立虚实关联 | Slide 5, 9 | "the device will send to our digital twin system immediately" |
| **网络大模型（Network LLM）** | 面向云网运维的领域大模型，覆盖规划、建设、维护、优化全生命周期 | Slide 5, 10 | "we have developed a specific large model" |
| **智能体（Agent）** | 生产网络中已部署 **1000+ 智能体** | Slide 12 | "we already have over one thousand agents in our production network" |
| **数字员工平台（DEP）** | 管理智能体的平台，定义职责、权限、协作 | Slide 13 | "Digital Employee Platform- DEP" |
| **智能体通信系统（ACS）** | 智能体之间的寻址、命名、协作基础设施 | Slide 13 | "Agent Communication System- ACS" |
| **小启（Xiaoqi）App** | 5万员工日常使用的 AI 入口，统一运维助手 | Slide 16 | "An application app named Xiaoqi... over 50,000 employees are using it" |

---

## ⚠️ 二、遇到的挑战

| 挑战 | 具体问题 | Slide 来源 | 讲话匹配 |
|------|----------|------------|----------|
| **智能体质量** | 缺乏统一命名和寻址、缺乏全生命周期管理、职责边界不清 | Slide 12 | "We need to define the agent quality" |
| **智能体安全** | 数据泄露风险、工具滥用、提示词注入、合规审计 | Slide 12 | "we need to get the risk of the security" |
| **多智能体通信** | 流式包性能、重要指令的可靠性、可追溯性 | Slide 12 | "among API communication is also very important" |
| **应用使用门槛** | 用户不熟悉 App 操作、菜单层级深、无法精准排障 | Slide 18 | "Users are not familiar with the operation of the app" |
| **流程固化** | 无法提供个性化的排障方案 | Slide 18 | "The process is fixed and can't provide personalized troubleshooting" |

---

## 🔭 三、前沿视野（他们在推动什么）

| 方向 | 核心思想 | Slide 来源 | 讲话匹配 |
|------|----------|------------|----------|
| **Agent 通信协议** | 需要定义智能体之间如何共享任务、知识、消息，以及如何命名和寻址 | Slide 20 | "Protocols for how agents share tasks, knowledge, messages, naming and addressing" |
| **Agent 可观测性** | 智能体的日志、追踪、指标、全生命周期管理、多智能体评估 | Slide 14, 20 | "Observability: Quality of agent, Logging, Tracing, Metrics" |
| **人机权限边界** | 智能体的权限边界需要明确定义，不能模糊 | Slide 12 | "blurred boundaries of human-machine authority" |
| **AI 原生网络** | 从经典 AI 走向 AI+Data，构建 AI 原生机制 | Slide 5 | "AI native mechanisms are constructed" |

---

## 🧠 四、我可以学到什么？

### 🔹 前沿概念
- **智能体不是单一工具，而是一个需要管理的“员工”**——需要入职、授权、考核、离职
- **智能体之间需要“语言”**——就像人类需要共同语言，智能体也需要通信协议
- **数字员工平台 = 智能体的 HR + 行政 + 协作工具**

### 🔹 新知识
- 智能体的可观测性不仅仅是技术指标，还包括职责边界、授权范围
- AI 运维的下一步不是“更强的模型”，而是“更好的智能体协作”

### 🔹 国际视野
- 中国电信已经在生产网络中部署 **1000+ 智能体**，这个规模在全球范围内都是领先的
- 他们现在遇到的“智能体管理”问题，3-5 年后全球运营商都会遇到
- IETF 未来可能需要制定 **Agent Communication Protocol** 这样的标准

---

# 中国移动（China Mobile）

## 📍 演讲人
- 詹（Zhan，音译）

## 📍 演讲主题
*Challenges and practices of AIOPS for carrier IP network*

---

## ✅ 一、已落地的关键技术

| 技术 | 说明 | Slide 来源 | 讲话匹配 |
|------|------|------------|----------|
| **AI 运维系统** | 60%+ 故障由 AIOps 系统自动处理，大多数几分钟内完成 | Slide 7 | "More than 60% faults are handled by AIOps system, most of them are processed within several minutes" |
| **私有模型训练** | 针对 IP 网络故障运维，训练专用私有模型 | Slide 7 | "we build dedicated private models, and train specialized skills" |
| **SRv6 路径智能规划** | 基于实时时延、丢包率、链路状态等数据，计算最优 SRv6 路径，支持每秒 1000 条路径计算 | Slide 8 | "Calculating 100% SRv6 path at rate of 1000/s" |
| **性能预测** | 基于历史时间序列数据，构建路径质量预测模型 | Slide 8 | "Build path quality prediction models based on historical time-series SRv6 path information" |
| **人在回路验证** | AI 给出的路径需人工确认后才生效 | Slide 8 | "paths take effect only after manual confirmation" |
| **数据蒸馏** | 为路径计算提供最优路径信息，支持短时预测和动态优化 | Slide 8 | "data distillation is an important process to feed optimal path information" |

---

## ⚠️ 二、遇到的挑战

| 挑战 | 具体问题 | Slide 来源 | 讲话匹配 |
|------|----------|------------|----------|
| **数据质量与体量** | 数据碎片化、格式不一致、时间戳缺失、PB 级数据处理成本高 | Slide 4 | "data comes from the different standards... inconsistent... overwhelming" |
| **多厂商数据标准** | 不同厂商设备上报的数据难以标准化 | Slide 4 | "Multi-Vendor: hard to standardize data across different hardware vendors" |
| **通信效率低** | 传的是“数据”而不是“信息”，比如流量突增要多次迭代才能定位 | Slide 4 | "communicate data rather than information" |
| **AI 黑盒与幻觉** | 只给结果不解释原因，担心自动操作导致业务中断 | Slide 4 | "Lack of Explainability... Fear of auto-disruption" |
| **数据采集开销大** | Telemetry 数据采集和处理消耗巨大带宽和算力 | Slide 9 | "enormous bandwidth and computational overhead incurred by telemetry data collection" |

---

## 🔭 三、前沿视野（他们在推动什么）

| 方向 | 核心思想 | Slide 来源 | 讲话匹配 |
|------|----------|------------|----------|
| **语义通信（Semantic Communication）** | 设备和控制器之间从“数据传输”转向智能“对话”，传“意思”而不是原始数据 | Slide 9 | "Should we consider a new 'semantic communication' protocol between devices and controllers — shifting from 'data transfer' to intelligent 'dialogue'?" |
| **设备端智能** | 网络设备本身可以运行小模型（如 iBNG），实现边端智能 | Slide 9 | "Considering that network devices are able to run small models, e.g. iBNG" |
| **运维网络框架** | 是否需要重新定义 AI 时代的运维网络整体架构 | Slide 9 | "Should we consider defining entire O&M network framework in AI Era" |
| **语义数据格式** | 上述语义通信需要什么样的数据格式 | Slide 9 | "Should we define the data format for the aforementioned semantic communication?" |

---

## 🧠 四、我可以学到什么？

### 🔹 前沿概念
- **语义通信**——这是非常前卫的思想：未来的网络设备之间不传“字节”，而传“意思”。比如不说“端口23流量100Mbps”，而说“链路快堵了”。
- **数据蒸馏**——不是所有数据都有用，要从海量数据中提取“精华”给 AI 用。
- **边端智能**——网络设备也可以像手机一样，本地跑小模型，不用什么都上报。

### 🔹 新知识
- AIOps 的瓶颈往往不在算法，而在**数据治理**——数据格式统一、时间戳对齐、去重压缩。
- 即使 AI 再强，**人在回路**（human-in-the-loop）在高风险操作中仍然是必须的。
- Telemetry 数据采集不是越多越好，要考虑成本和效率的平衡。

### 🔹 国际视野
- 中国移动拥有 **全球最大的 5G 网络**（265万基站）和 **61.3 EFLOPS 的 AI 算力**，他们的实践有极强的规模效应。
- 他们提出的“语义通信”，如果成为标准，将彻底改变网络管理和控制的面貌。
- 这是对现有“数据上报-中心决策”模式的挑战，走向“分布式智能-语义协作”。

---

# 中国联通（China Unicom）

## 📍 演讲人
- 赵静（Jing Zhao）

## 📍 演讲主题
*Intelligent Operation and Maintenance: Practices and Reflections*

---

## ✅ 一、已落地的关键技术

| 技术 | 说明 | Slide 来源 | 讲话匹配 |
|------|------|------------|----------|
| **数字孪生网络** | 数值仿真 + 模拟仿真融合的数字孪生架构 | Slide 4, 9 | "We propose a digital twin network architecture driven by integrated numerical simulation and emulation" |
| **割接仿真与回滚** | 配置级仿真，支持原子操作提取、堆栈式回滚 | Slide 9 | "Cutover simulation requires configuration-level simulation... stack-based rollback" |
| **智能流量预测** | 基于时空深度神经网络的端到端流量分析与预测 | Slide 9 | "Build a spatio-temporal deep neural network for end-to-end traffic analysis" |
| **IP 网络流量监控平台** | 覆盖家庭宽带、移动网络、承载网、应用的端到端 IP 流量监控 | Slide 10 | "provide an end-to-end IP traffic monitoring and analyzing system covering home broadband, mobile networks, bearer networks and applications" |
| **IPv6 能力评估** | 对比 IPv4/IPv6 现网性能，识别部署瓶颈 | Slide 10 | "Compare IPv4/IPv6 live-network performance, identify deployment bottlenecks" |
| **智能计算中心运维智能体** | 基于强化学习 + 大模型的运维控制智能体 | Slide 12 | "develop an in-house operation and control intelligent agent based on reinforcement learning and AI large models" |
| **负载均衡优化** | AI-DCQCN 负载均衡与拥塞控制优化 | Slide 11 | "AI-DCQCN-based load balancing and congestion control optimization" |

---

## ⚠️ 二、遇到的挑战

| 挑战 | 具体问题 | Slide 来源 | 讲话匹配 |
|------|----------|------------|----------|
| **跨层协同仿真难** | 物理-IP-应用三层无法协同仿真，无法构建全栈孪生模型 | Slide 4 | "Difficulty in 'Physical-IP-Application' collaborative simulation" |
| **仿真规则生成慢** | 无法快速自动生成多场景、动态需求的仿真规则 | Slide 4 | "Cannot rapidly and automatically generate simulation rules" |
| **宏微观割裂** | 宏观业务预测与微观设备验证之间存在断层 | Slide 4 | "Gap between macro-level business forecasting and micro-level device validation" |
| **实时性与精度矛盾** | 大规模网络无法实现实时同步和“零误差”验证 | Slide 4 | "Cannot meet the requirements for real-time synchronization and 'zero-error' validation" |
| **端到端定位难** | iFIT 等随流检测技术因多厂商支持不足，无法实现端到端监测 | Slide 5 | "current in-situ telemetry techniques such as iFIT fail cannot achieve end-to-end monitoring due to insufficient multi-vendor support" |
| **海量流量实时分析** | 无法实现海量流量的实时高维分析 | Slide 5 | "Real-time multi-dimensional analysis of massive traffic remains unachievable" |
| **流量变化检测盲区** | 跨域 IP 变化和 NAT 转换导致监控失效 | Slide 5 | "IP-based monitoring suffers from header attribute degradation caused by cross-domain IP changes and NAT translation" |
| **应用感知缺失** | 网络监控以 IP 为中心，无法感知具体应用 | Slide 5 | "current methods are IP-centric monitoring, not application-aware" |
| **割接后长尾风险** | 配置错误或代码缺陷可能在数月后引发故障 | Slide 6 | "Improper label configurations or code defects often cause periodic faults weeks or even months after deployment" |
| **跨部门协同成本高** | 故障排查仍依赖人工跨专业、跨部门协调 | Slide 6 | "Complex fault troubleshooting still relies on manual cross-speciality and cross-department coordination" |

---

## 🔭 三、前沿视野（他们在推动什么）

| 方向 | 核心思想 | Slide 来源 | 讲话匹配 |
|------|----------|------------|----------|
| **网络韧性（Resilience）** | 网络需要具备事前-事中-事后全生命周期的韧性能力 | Slide 7 | "networks must be equipped with comprehensive resilience capabilities across the full lifecycle" |
| **深度感知与预测** | 从流量可视化走向智能风险预测 | Slide 7 | "From traffic visualization to intelligent risk forecasting" |
| **闭环仿真与验证** | 操作前进行推演，将风险控制在事前 | Slide 7 | "Pre-operation deduction to contain risks upfront" |
| **自适应控制** | 从固定控制走向弹性控制，实现自动调优和自愈 | Slide 7 | "Shift to elastic control for auto-tuning and recovery" |
| **全场景任务支持** | 计算网络融合层支持大规模训练、大模型微调等全场景任务 | Slide 11 | "Cover the entire process of task executions including large-scale training and large-model fine-tuning" |

---

## 🧠 四、我可以学到什么？

### 🔹 前沿概念
- **网络韧性（Resilience）**——不仅仅是“稳定”，而是能感知、能预测、能自适应、能自愈的完整能力。
- **数字孪生不是“一张图”**——联通强调的“数值仿真+模拟仿真融合”，意味着孪生要能算、能推演，不仅仅是可视化。
- **割接仿真是“外科手术级”的**——要能原子化操作、要能回滚，这才是可落地的数字孪生。

### 🔹 新知识
- 故障定位难的本质往往是**元数据不一致**——跨厂商、跨域的数据对不上，神仙也难定位。
- 流量监控的盲区来自**IP 变化和 NAT**——应用层感知才是出路。
- 割接后的长尾风险是最可怕的——配置错误可能几个月后才爆发，需要长期监控。

### 🔹 国际视野
- 中国联通强调的“全生命周期韧性”，是对传统“故障响应”模式的升维。
- 他们遇到的“跨厂商 iFIT 支持不足”问题，正是标准化滞后的体现——这正是 IETF 需要工作的方向。
- 智能计算中心运维是下一个战场——当网络开始为 AI 训练服务，运维逻辑也要重构。

---

## 📌 总结：三大运营商对比

| 维度 | 中国电信 | 中国移动 | 中国联通 |
|------|----------|----------|----------|
| **核心关键词** | 智能体、数字员工、Agent 协议 | 语义通信、数据治理、边端智能 | 网络韧性、数字孪生、全生命周期 |
| **已落地规模** | 1000+ 智能体、5万员工使用 | 60%+ 故障自动处理、1000条路径/秒 | 端到端流量监控平台、智能计算中心 |
| **最大挑战** | 智能体管理、安全、通信 | 数据质量、多厂商、AI 黑盒 | 仿真精度、跨域协同、长尾风险 |
| **最前沿的思想** | Agent 需要通信协议 | 设备与控制器要“语义对话” | 网络要有全生命周期韧性 |

---

## 🎯 参会收获总结

参加 IETF 125，我从三大运营商的演讲中学到：

1. **中国运营商已经在 AI 运维的前沿**——他们的规模和实践深度，远超我之前的想象
2. **未来的网络不是“设备联网”，而是“智能体协作”**——电信的 1000+ 智能体就是证明
3. **标准化正在向智能化延伸**——语义通信、Agent 协议、数字孪生仿真接口，都可能成为下一波 IETF 工作项
4. **规模暴露问题，问题定义标准**——他们现在遇到的挑战，正是未来全球网络都要面对的问题
5. **IETF 的角色在变化**——不仅要定义“设备怎么连”，还要定义“智能怎么聊”

---

> 如果你也在研究 AIOps、网络自动化、未来网络架构，希望这份笔记对你有帮助。  
> 欢迎讨论、指正、补充。
