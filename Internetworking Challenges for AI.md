# 🎓 IETF 125 IRTF Open Meeting 参会笔记：Internetworking Challenges for AI

> **会议**：IRTF Open Meeting  
> **主题**：Internetworking Challenges for AI  
> **时间**：2026年3月17日  
> **地点**：中国 深圳  
> **难懂指数**：⭐⭐⭐⭐⭐
---

## 一、会议背景

IRTF（互联网研究任务组）是IETF的研究分支，聚焦于长期的、前瞻性的互联网技术研究。本次Open Meeting的主题是AI的互联网络挑战，探讨AI大模型、AI智能体对网络基础设施提出的新需求和新问题。

三位演讲者从不同角度切入：
1. **Mooncake项目**：大模型推理的分离式架构
2. **AI智能体通信**：万亿级智能体的网络与安全挑战
3. **AI可靠性工程**：AI基础设施的故障诊断与自愈

---

## 二、Mooncake：大模型推理的分离式架构

**演讲人**：Mingxing Zhang @ KVCache.AI  
**Slide 标题**：*Disaggregated Architecture for LLM Inference*

### 2.1 核心问题

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Challenge of Online Model as a Service System* | 更多数据 + 更大模型 + 更长上下文 = 更高智能，但GPU短缺、推理成本高、响应时间长 |
| *Different Hardware are Good at Different Dimension* | H800适合算力，H20适合带宽，CPU内存适合容量 |

**核心洞察**：大模型推理有两个阶段——**Prefill（预填充）**和**Decode（解码）**，它们对硬件需求完全不同。传统架构把两者绑在一起，造成资源浪费。

### 2.2 技术方案：Mooncake架构

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Mooncake：A KVCache-centric Disaggregated Architecture for LLM Serving* | 以KVCache为中心的分离式架构，将Prefill和Decode实例分离 |
| *Core Technologies of Mooncake* | KVCache-centric Conductor、分布式KVCache池、P/D分离调度 |

**核心思想**：
- **Prefill实例**：负责处理输入，需要高算力（H800）
- **Decode实例**：负责生成输出，需要高带宽（H20）
- **KVCache池**：在两者之间共享KV缓存，减少重复计算
- **效果**：Kimi吞吐量提升75%，同时满足SLO保证

### 2.3 技术实现

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Transfer Fast: Mooncake Transfer Engine* | 拓扑感知路径选择、多NIC池化、支持多种协议，RDMA下可达190GB/s |
| *Store More: Elastic Shared Multi-layer KV Cache* | 分布式KV缓存共享，动态扩缩容，支持内存→SSD分层卸载 |
| *Extensive APIs, Easy to Use* | Put/Get API，零拷贝传输，可配置的缓存放置策略 |

### 2.4 技术挑战与演进

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Hidden Risks of Mooncake TE* | 命令式路径选择的问题：静态绑定、状态盲区、无故障检测 |
| *Challenges from Imperative Path Selection* | 状态盲调度导致延迟增加、带宽浪费；执行脆弱，需要人工干预 |
| *Dynamic Orchestration* | 统一分段抽象、动态按需编排、自适应切片喷洒、弹性自愈 |

**演进方向**：
- **动态路径选择**：基于延迟预测选择最优NIC
- **自适应切片喷洒**：跨NIC分发数据切片，提高带宽利用率
- **弹性自愈**：链路故障时透明回退到TCP，恢复后重用

### 2.5 落地与影响

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Mooncake is Used in Various Scenarios of LLM* | Kimi使用Mooncake处理爆发流量 |
| *Cluster Scale Serving* | vLLM、SGLang、xAI、DeepSeek等采用Mooncake架构 |
| *NVIDIA Dynamo* | Jensen Huang在GTC 2025主题演讲中展示，其架构受Mooncake启发 |

---

## 三、AI智能体通信：万亿级智能体的网络挑战

**演讲人**：Lixia Zhang @ UCLA  
**Slide 标题**：*On AI Agent Networking*

### 3.1 核心问题

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *40 years of IETF: from networking hosts to networking AI agents* | IETF过去40年连接主机，未来要连接AI智能体 |
| *Networking: deliver packets, support different communication patterns* | 智能体通信模式：1×1、1×N、N×1、N×N |

**核心洞察**：智能体通信与主机通信有本质不同：
- **规模**：10⁹ - 10¹²个智能体
- **生命周期**：毫秒级到月级
- **通信模式**：多对多实时交互
- **委托链**：智能体代表用户行动，可生成子智能体
- **自主性**：无需人工批准即可行动

### 3.2 安全挑战

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Securing communications, today* | 当前安全方案碎片化：TLS、OAuth、DNSSEC、JWT各用各的标识 |
| *Current Security Practice: Infeasible at Agent Scale* | X.509证书慢、OAuth不适合智能体委托链、无统一命名空间 |

**核心问题**：现有安全方案无法支撑万亿级智能体：
- 证书颁发太慢
- 无统一命名空间
- 委托链无法表达权限范围
- 无跨域信任推理机制

### 3.3 解决方案方向

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Starting point: get naming right, then build security into agentic AI* | DNS作为统一命名空间，每个实体都有DNS名 |
| *Identity = Name + Key* | 名称提供语义上下文，密钥提供密码学可验证性 |
| *Global namespace, local trust* | 全局命名空间，本地化信任锚 |

**核心思想**：
- **DNS作为统一命名空间**：每个组织、用户、智能体管理自己的DNS切片
- **Name + Key作为身份**：名称可读，密钥可验
- **委托链原生支持**：深度、动态、可验证的委托链

### 3.4 研究方向

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *What the IRTF/DINRG Community Should Do* | 不要修补现有协议，以DNS为身份命名空间基础，设计去中心化信任管理 |
| *AI agent networking: Global Namespace, Local Trust* | 规模、动态性、多对多交互构成需求三角，需要全新的命名和信任体系 |

---

## 四、AI可靠性工程：AI基础设施的故障诊断与自愈

**演讲人**：Hong Xu @ CUHK  
**Slide 标题**：*Reliability Engineering Challenges in Networking for AI*

### 4.1 背景与挑战

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Scale: O(100k) GPU training* | 10万GPU规模训练已成现实，故障率极高 |
| *Server-level to Cluster-level Interconnects* | 从CXL、NVLink到RoCE、InfiniBand，互联复杂度爆炸 |

**核心问题**：大模型训练依赖大规模GPU集群，网络故障频繁，人工排障成本极高。

### 4.2 技术方案：智能故障诊断

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Vision: Autonomous Agentic Troubleshooting for Infra* | 构建OpenClaw for NetOps/InfraOps，用AI智能体自动排障 |
| *Three Key Questions* | Q1：如何评估智能体？Q2：如何设计智能体？Q3：如何运行智能体？ |

### 4.3 落地项目

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *TSGuard: Automated User-Centric Incident Diagnosis* | 面向云上AI工作负载的用户中心故障诊断，FSE'26 |
| *NetOpsAI: AI-Driven NetOps System* | 在国内某头部AI公司生产环境中运行的网络排障智能体 |
| *Mycroft: Tracing Dependencies in Collective Communication* | ByteDance生产环境部署的集体通信依赖追踪工具，SOSP'25 |

#### TSGuard

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *TSGuard Architecture & Key Ideas* | 离线知识库构建 + 在线三层诊断流水线 |
| *Historical Incident Database* | 基于Azure三年生产故障数据构建 |
| *Incident Taxonomy* | 将非结构化事后分析转化为结构化推理路径 |
| *Three-Tier Diagnosis* | Tier1：历史数据匹配；Tier2：分类树引导；Tier3：未知异常探索 |

**效果**：诊断准确率超过SOTA方案。

#### NetOpsAI

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *NetOpsAI: Running in A Leading AI Company in China* | 上下文感知元数据查询、端到端根因分析、高保真Telemetry分析、LLM驱动的排障自动化 |

#### Mycroft

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *Mycroft: Tracing Dependencies in Collective Communication* | 集体通信级别的追踪，实时异常检测，依赖驱动的根因分析 |
| *Deployment Stats* | 24/7运行，监控128+ GPU任务，10TB/天追踪数据，90%故障15秒内检测到 |

### 4.4 展望

| Slide 标题 | 核心内容 |
|-------------|-------------|
| *A great time to work on reliability engineering for networking and AI infra* | 欢迎合作、数据集共享，即将开源NetOpsArena |

---

## 五、总结与思考

### 5.1 三个演讲的内在联系

| 演讲 | 核心问题 | 解决方案方向 |
|------|---------|-------------|
| **Mooncake** | 大模型推理成本高、资源利用率低 | P/D分离架构、KVCache池化、动态传输优化 |
| **Agent Communication** | 万亿智能体的通信与安全 | DNS统一命名空间、Name+Key身份、本地化信任 |
| **Reliability Engineering** | AI基础设施故障频发、排障成本高 | AI智能体自动排障、依赖追踪、分类树诊断 |

### 5.2 我的理解

这三个演讲其实在讲同一件事的不同侧面：

**AI正在重塑网络，网络也在重塑AI。**

- **Mooncake**告诉我们：大模型推理需要网络传输KVCache，网络的性能直接影响推理效率
- **Agent Communication**告诉我们：未来网络连接的不再是主机，而是万亿智能体，需要全新的命名和安全体系
- **Reliability Engineering**告诉我们：AI基础设施的故障诊断不能靠人，要靠AI智能体

### 5.3 可切入的研究方向

| 研究方向 | 核心问题 | 对应演讲 |
|----------|---------|---------|
| **KVCache传输优化** | 如何在RDMA网络中实现高性能、高可靠的KVCache传输？ | Mooncake |
| **智能体命名与寻址** | 如何为万亿动态智能体设计可扩展的命名和寻址系统？ | Agent Communication |
| **AI排障智能体** | 如何让AI智能体自主诊断AI基础设施的故障？ | Reliability Engineering |

---

> **整理时间**：2026年3月  
> **说明**：本笔记基于IRTF Open Meeting公开演讲内容整理，供学习参考。
