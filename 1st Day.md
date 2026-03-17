# 🎓 IETF 125 菁才计划大会：中国大学生与IETF领导们的问答环节记录

> **时间**：2026年3月16日  
> **地点**：中国 深圳  
> **提问者**：中国大学生（本、硕、博）  

---

## 一、问答记录

---

### **Q1：When we design a network protocol, we always consider security first or the efficiency first？**

**A：** For many years, no security. We thought about that later. Now we have to add it on. Security people go to all working groups. They say you need to consider security when you do the design. But there is a lot of legacy. We have many things that are not secure. The balance is not only efficiency, but also interoperability. If you insist I be completely secure immediately, it's a balance. We figure out compromises. Each working group has a charter. The charter lays out the requirements. We agree before the group starts how they'll deal with security. Security means many things: authentication, authorization, access control, privacy, confidentiality, integrity. HTTP first had no security. Then HTTPS came. Now QUIC builds security from the start.

---

### **Q2：How can Chinese teenagers integrate into the IETF more quickly and make some contribution？**

**A：** Getting involved in IETF work. In simple ways at the beginning. Go to a meeting and listen first. Do your homework before the meeting. Read the documents. Maybe first time you send a message to the mailing list. Make a suggestion. That's how you start. After the session, in the hallway, talk to people. Make relationships. Don't try to do it yourself. Collaborate with other people. Let them get to know you. Trust people. The best new participants listen first, see what's going on, understand how people discuss things.

---

### **Q3：How the Internet will look like after human beings are able to interstellar travel？**

**A：** That's the beauty of how we do things. We did not define everything. We did not bring a big blueprint. We defined protocols. We let people run with it. We have the Internet that we have today. I hope things will continue that. We believe in building blocks. These blocks will continue to be used when we go to moon, to Mars, and beyond.

---

### **Q4：How do the advances of technology affect the IT opportunity？(about AI)**

*（my question）*

**A：** The IETF does not like to standardize a concept. We standardize protocols that deal with pieces. At the moment, the industry hasn't figured out everything about AI. In the hackathon, people used IETF specifications, fed them into an algorithm, wrote code that implements the spec, had them interact. That's the benefit of interoperability testing. There are working groups that have pieces of AI. IETF work on AI is usually boring. AI PreF is about how to tell AI bots to collect data or not. Like robots.txt. But finer-grained. Agent-to-agent communication will be important for IETF.

---

### **Q5：How this bug was discovered and resolved？(about security bug)**

**A：** If the implementation fails, we go back to the spec and see how the protocol failed. Fixing it is like anything else IETF does. Somebody comes up with a proposal. The proposal is discussed. It becomes an Internet draft. It may update the existing spec or be a separate document. When something is exploited in the field, it's higher priority and runs through quickly.

---

### **Q6：I want to know how to expand the influence about it. (about DNN proposal)**

**A：** Make relationships with people in the DNS group. Help them write their document. Then go to those people. Say "I have this idea. I wrote a draft. Would you look at it for me?" Find someone else you've met. You need people interested in implementing, interested in writing code. They will work with you on the draft. Don't just throw a draft out and hope. Talk to people first.

---

### **Q7：Whether there have been any projects or investigations to evaluate it？(about standard impact)**

**A：** There are studies about what makes a successful protocol. There's an RFC about it. Look for RFC about success protocols. A lot of RFCs we publish are harmless but nobody cares. We do a lot of that because people want to get their idea out. You can't predict what will be successful. If we closed IETF because work wasn't interesting, we wouldn't publish anything. The rest of the world decides whether to use it. That's a feature. We write the best standard, but others make independent decisions.

---

## 二、我的观察与思考

| 问题 | 核心主题 | 给我的启发 |
|------|---------|-----------|
| Q1 | 安全 vs 效率 | 协议设计要兼顾安全、效率、互操作性，QUIC是“安全内建”的好例子 |
| Q2 | 如何参与IETF | 先听、先观察、先交朋友、再提草案——参与开源社区也是这个逻辑 |
| Q3 | 互联网的未来 | IETF不做大蓝图，只做“积木块”，让未来自己去组装 |
| Q4 | AI与network | AI对network的影响不是LLM，而是智能体通信、细粒度控制协议 |
| Q5 | 漏洞修复流程 | 从实现回溯到规范，提案-讨论-草案-更新，被利用的漏洞优先级最高 |
| Q6 | 如何推广提案 | 先帮别人写文档，再请别人看你的——技术社区的本质是协作 |
| Q7 | 标准的影响力 | 很多标准“无害但无人问津”，成功不可预测，交给市场决定 |

---

## 三、我的核心思考：Network for AI 与 AI for Network 的区别与联系

### 3.1 两个方向的定义

| 方向 | 定义 | 核心问题 |
|------|------|---------|
| **Network for AI** | 为AI设计和优化的网络 | 如何让网络更好地支撑AI训练和推理？ |
| **AI for Network** | 用AI来优化和管理网络 | 如何让网络更智能、更自动、更可靠？ |

### 3.2 从本次IETF看到的例子

| 方向 | 例子 | 来自哪个演讲 |
|------|------|-------------|
| **Network for AI** | Mooncake：KVCache传输优化，让大模型推理更快 | IRTF Open: Mooncake |
| **Network for AI** | 智能体通信：万亿级AI智能体需要新的命名和寻址体系 | IRTF Open: Agent Communication |
| **AI for Network** | NetOpsAI：用AI智能体自动诊断网络故障 | IRTF Open: Reliability Engineering |
| **AI for Network** | TSGuard：用AI诊断云上AI工作负载的故障 | IRTF Open: Reliability Engineering |
| **AI for Network** | 中国电信：1000+智能体用于网络运维 | OPSAREA: China Telecom |
| **AI for Network** | 中国移动：AI自动处理60%+网络故障 | OPSAREA: China Mobile |
| **AI for Network** | 中国联通：AI用于流量预测、数字孪生 | OPSAREA: China Unicom |

### 3.3 两者的关系

**它们是互为基础、互相促进的循环：**

1. **Network for AI 是前提**：只有网络足够强大（低延迟、高带宽、可扩展），才能支撑起大规模的AI训练和推理。Mooncake就是典型例子——没有高效的KVCache传输，大模型推理就卡在I/O上。

2. **AI for Network 是升华**：当网络足够复杂（10万GPU、多厂商设备、跨域协同），人工已经无法管理，必须让AI来管网络。三大运营商和可靠性工程演讲都在证明这一点。

3. **最终走向融合**：未来的网络，既是“为AI设计的网络”，也是“由AI管理的网络”。两者不是先后关系，而是螺旋上升的关系。

### 3.4 对我研究方向的意义

| 方向 | 可以研究的问题 |
|------|--------------|
| **Network for AI** | 如何优化RDMA网络传输KVCache？如何为万亿智能体设计命名和寻址系统？ |
| **AI for Network** | 如何让AI智能体自主诊断网络故障？如何让AI理解网络设备的“语义”？ |
| **交叉点** | 当AI用来管理为AI设计的网络时，如何形成闭环？ |

---

## 四、我的收获

> 在IETF 125第一天菁才计划大会上，我作为参会学生，记录了中国大学生与IETF领导层的问答，并提出了自己的问题（Q4）。这些回答让我更深入地理解了：
>
> 1. **IETF的文化**：不画大蓝图，只做积木块；先听、先交朋友、再贡献。
> 2. **AI与网络的双向关系**：通过本次会议的所有演讲，我看到了两个方向的实践——**Network for AI**（为AI优化网络，如Mooncake）和**AI for Network**（用AI管理网络，如三大运营商、NetOpsAI）。两者互为基础、互相促进。
> 3. **我感兴趣的研究方向**：我希望在两者交叉点上深耕——当AI用来管理为AI设计的网络时，如何形成智能闭环？
>
> 这次参会让我明白：技术不只是代码和协议，更是人与人的协作、思想与思想的碰撞。而AI+Network的未来，正在这里被定义。

---

> **整理时间**：2026年3月  
> **说明**：本笔记基于IETF 125第一天全体大会问答环节记录整理。
