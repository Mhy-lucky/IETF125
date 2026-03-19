
# 🎙️ IETF 125 MOQ 工作组参会笔记：Media over QUIC 协议进展

> **会议**：MOQ（Media over QUIC）工作组会议  
> **时间**：2026年3月17日、19日  
> **地点**：中国 深圳  
> **主题**：下一代实时媒体传输协议的标准制定与落地实践  


## 一、MOQ简介

MOQ（Media over QUIC）是 IETF 正在标准化的**下一代实时媒体传输协议**，目标是解决现有方案的两难困境：

- **HLS/DASH**：能服务千万人，但延迟高（几秒到几十秒）
- **WebRTC**：延迟低（<500ms），但极其复杂，大规模分发成本高

MOQ 想**既要又要**——基于 QUIC 协议，用发布/订阅架构，实现**低延迟 + 大规模分发**。


## 二、MOQ 协议栈

```
应用层 (直播/云游戏/AI助手)
    ↓
媒体格式层 (LOC: Low Overhead Container)
    ↓
流格式层 (MSF/CMSF: 目录/清单)
    ↓
传输协议层 (MOQT: Media over QUIC Transport)
    ↓
QUIC 层 (基于UDP，多路复用+0-RTT+加密)
```

我画个表格理解每层的功能：

| 层级 | 协议 | 职责 | 类比 |
|------|------|------|------|
| 媒体格式 | LOC | 把视频帧装进包里 | 快递怎么打包 |
| 流格式 | MSF/CMSF | 描述流的结构（目录） | 快递单+菜单 |
| 传输协议 | MOQT | 怎么发、怎么订阅 | 快递公司怎么送货 |
| 底层传输 | QUIC | 可靠传输+加密 | 公路/铁路网 |


## 三、Session 1（3月17日）：没什么干货感觉

第一场主要是议程介绍和注意事项，真正的技术讨论在 Session 2。


## 四、Session 2（3月19日）：六大议题

### 4.1 Hackathon 报告

**讲者**：Mike English  
**关键词**：互操作性测试、实现进度

**Content**：
Hackathon 期间，多个团队测试了 MOQ 实现的互操作性。大家跑通了基本的发布订阅流程，验证了协议的可实现性。

**My Thought**：
标准不能只写在纸上，得有人真写代码。Hackathon 就是“纸上协议”和“真实代码”之间的桥梁。能跑通说明协议设计没太大问题。


### 4.2 MSF/CMSF 更新——流格式怎么描述

**讲者**：Will Law  
**关键词**：Catalog、URL fragment、SCTE-35、Init Tracks

**Content**：

1. **URL 格式定下来了**
   - 用 URI fragment（#后面的部分）传客户端参数
   - fragment 不发给 Relay，只给客户端自己用
   - 可以传时间范围、C4M token 等

   ```
   moqt://example.com/relay-app#app-live-catalog&token=123
   ```

2. **Catalog 支持变量替换**
   - 同一个 Catalog 可以服务所有用户，但参数（如广告 ID、水印）可以个性化
   - 用 `%id%` 这种变量，Relay 或客户端替换成真实值

3. **Init Tracks——动态更新解码器配置**
   - 以前：init 数据写在 Catalog 里，中途不能改
   - 现在：可以单独开一个 Init Track，中途更新分辨率/编码参数
   - 场景：1080p 电影播完切 2160p 体育，不用断流

4. **SCTE-35 广告信令**
   - 直播插广告需要信令
   - 用 Event Timeline Track 传 SCTE-35 数据

5. **字幕支持**
   - 支持 WebVTT、CEA-608/708 字幕
   - 可以定义 Track 里嵌了什么字幕

**My Thought**：
MSF/CMSF 是 MOQ 的“应用层语言”。如果说 MOQT 是快递公司，MSF/CMSF 就是快递单——定义怎么找到视频、怎么切广告、怎么加字幕。Init Tracks 的设计很实用，解决了直播中参数动态变化的问题。


### 4.3 阿里巴巴 MOQ 生产实践——成功落地

**讲者**：Minghui Jiang  
**关键词**：XQUIC、淘宝语音搜索、数字人、AI 助手、Multimodal Feedback

**Content**：

#### 4.3.1 落地场景

| 场景 | 业务 | 核心诉求 |
|------|------|----------|
| 淘宝语音搜索 | 语音采集+3A处理 | 快速响应 |
| 数字人云渲染 | 手势→云端渲染→视频反馈 | Motion-to-Photon 延迟 |
| 淘宝直播数字人 | 24小时AI主播 | 稳定、低延迟、可打断 |
| 支付宝AI助手 | 杭州导游、就业助手 | 流式响应、低延迟 |
| 多模态AI聊天 | 语音+视觉+文本 | <300ms，弱网适应性 |

#### 4.3.2 技术架构：XQUIC + MOQ

阿里巴巴自研了 **XQUIC**（跨平台 QUIC 库）：

- Android/iOS 编译产物 <400KB
- 已在淘宝核心导购、短视频链路大规模使用
- 支持 0-RTT 建连、连接迁移（WiFi/蜂窝切换不断）

#### 4.3.3 优化手段

| 优化点 | 具体手段 | 效果 |
|--------|----------|------|
| 拥塞控制 | SQP + Pudica 算法 | 最小化排队延迟 |
| FEC | 5%冗余保护关键帧 | 降低10%单向延迟 |
| 连接迁移 | CID 做连接标识 | 网络切换不断连 |
| 0-RTT建连 | 重连无需握手 | 连接耗时<50ms |
| 音频引擎 | 绕过高级API，直接 AudioUnit | 初始化从500ms→100ms |

#### 4.3.4 效果数据

| 指标 | 优化前 | 优化后 | 提升 |
|------|--------|--------|------|
| 连接耗时（首次） | ~300ms | 150ms | 50%↓ |
| 连接耗时（0-RTT） | 不支持 | <50ms | - |
| 短视频下载耗时 | HTTP/2基线 | -20% | 20%↓ |
| 卡顿率 | HTTP/2基线 | -10% | 10%↓ |

#### 4.3.5 核心洞察

> **单靠传输层的拥塞控制是不够的。**

因为编码器不知道网络变差了，还在猛发高清流，导致卡顿。需要 **应用层反馈（Multimodal Feedback）** 打通传输层和应用层的隔阂。

他们提出了草案，让客户端通过一个“反馈 Track”告诉服务器：哪些帧丢了、晚了，然后服务器让编码器降码率。

**My Thought**：
我个人认为这是这场session最硬的分享。不是理论推演，而是我们可以看到淘宝、支付宝真在用的技术。数据具体（50ms、20%、10%），问题真实（编码器不知道网络差），解决方案有原创性（Multimodal Feedback 草案）。


### 4.4 QMux over MOQT——UDP 被墙了怎么办

**讲者**：Suhas Nandakumar  
**关键词**：UDP 阻断、TCP fallback、QMux

**Content**：

- **问题**：MOQ 基于 QUIC（UDP），但很多企业网络会屏蔽 UDP
- **方案**：让 MOQ 也能跑在 TCP 上，通过 QMux 层模拟 QUIC 的多路复用
- **挑战**：ALPN 怎么协商？版本爆炸怎么处理？

**My Thought**：
这是现实主义的设计——理想很美好（全 QUIC），现实很骨感（UDP 被墙）。QMux 是逃生舱，保证连不上 QUIC 时还能用 TCP 降级，提高落地能力。


### 4.5 LOC 更新——媒体怎么打包

**讲者**：Mo Zanaty  
**关键词**：Low Overhead Container、Timescale、WebCodecs

**Content**：

LOC 是 MOQ 的媒体容器格式，负责把视频帧装进 MOQ Object 里。

- **元数据位置**：Public Properties 放 MOQT Header，Private Properties 放 Payload（可加密）
- **Timescale 属性**：定义时间戳的单位（音频 48kHz，视频 90kHz）
- **WebCodecs 问题**：`avc3`/`hev1` 格式的参数集可以在带内更新，LOC 需要支持

**My Thought**：
LOC 是 MOQ 的打包标准。视频编码格式很多（H.264/H.265/AV1），LOC 负责统一封装，让 MOQ 能兼容各种编码。


### 4.6 Filters——让 Relay 变聪明

**讲者**：Mo Zanaty  
**关键词**：Range Filters、Track Selection、Relay 保护

**Content**：

让订阅者可以**只接收一部分数据**，而不是整个 Track。

1. **Range Filters**（范围过滤）
   - 按 Subgroup ID、Object ID、Priority、Property 过滤
   - 例：只订阅关键帧（Object ID = 0）

2. **Track Selection Filter**（Track选择）
   - 在 Namespace 级别选 Top N 个 Tracks
   - 例：热度最高的前5个直播间

3. **Relay 保护**
   - 限制 `MAX_FILTER_RANGES`，防止恶意客户端搞死 Relay

**My Thought**：
Filters 让 Relay 从稳定转发变成智能分发。带宽有限时，只传关键帧就能让用户看到画面（虽然可能模糊）。Top N 选择对直播平台很有用——不用把所有直播间都传下来，只传热的就行。


### 4.7 编辑时间——协议还在重构

**讲者**：Alan Frindell  
**关键词**：协议大改、控制平面简化、多订阅问题

**Content**：

MOQT 自 IETF 124 以来经历大改，感觉像是一个全新的协议。

- **控制平面**：移除了 7 种控制消息，每请求用一对单向流
- **数据平面**：允许 Track 混用 Stream 和 Datagram
- **Rendezvous**：允许订阅者等还没上线的 Publisher
- **多订阅问题**：能不能多次订阅同一个 Track以及Relay 要不要去重的问题还在讨论

**My Thought**：
协议还在迭代，没完全定型。这说明 MOQ 不是写完就完事了，而是在真实反馈中不断优化，感觉这次参加的sessions都有这样的特点，所有的东西都是在不断升级优化而不是一锤定音，RFC定下来的标准也在不断更迭。


## 五、Keywords（术语 + 个人理解）

| 术语 | 个人理解 |
|------|---------|
| **MOQT** | MOQ 的传输协议层，负责怎么发、怎么订阅 |
| **MSF/CMSF** | MOQ 的流格式层，负责描述流的结构（目录、广告、字幕） |
| **LOC** | MOQ 的媒体容器格式，负责把视频帧装进包里 |
| **Object** | MOQ 传输的基本单位，可以是一个视频帧或音频片段 |
| **Track** | 一组 Object 的集合，相当于一个视频流 |
| **Group** | Track 里的逻辑分组，方便索引 |
| **Relay** | MOQ 的中继节点，负责转发数据 |
| **Publisher** | 发布者，发视频的人 |
| **Subscriber** | 订阅者，看视频的人 |
| **Multimodal Feedback** | 阿里巴巴提的反馈机制，让客户端告诉服务器接收状态 |
| **QMux** | 让 MOQ 跑在 TCP 上的适配层，解决 UDP 被墙问题 |
| **Filters** | 让订阅者只接收部分数据（如只收关键帧） |
| **Init Track** | 专门传解码器配置的 Track，支持中途更新 |
| **XQUIC** | 阿里巴巴自研的跨平台 QUIC 库 |


## 六、这次会议在解决的问题

我理解 MOQ 现在的状态是：**协议框架已定，正在解决落地会遇到的各种问题**。

| 问题 | 解决方案 |
|------|----------|
| 协议太复杂，实现困难 | 精简控制消息，简化流程 |
| UDP/QUIC 可能被防火墙屏蔽 | QMux（走 TCP 降级） |
| 中继节点能看到内容（隐私） | Secure Objects（端到端加密） |
| 视频格式太多，怎么统一封装 | LOC（轻量容器） |
| 中继节点只会傻转发 | Filters（只传需要的数据） |
| 编码器不知道网络变差，导致卡顿 | Multimodal Feedback（应用层反馈） |
| 解码配置中途要改 | Init Tracks（动态更新） |
| 直播要插广告 | SCTE-35 支持 |



## 七、我的收获


> “旁听了 MOQ（Media over QUIC）工作组的讨论。MOQ 是正在标准化的下一代实时媒体传输协议，想解决 WebRTC 太复杂、HLS 延迟高的问题。会上印象最深的是阿里巴巴分享的生产实践——他们在淘宝语音搜索、数字人、支付宝 AI 助手里用了自研的 XQUIC + MOQ，连接耗时从 300ms 降到 50ms，短视频下载耗时降低 20%。他们还发现单靠传输层拥塞控制不够，提出了 Multimodal Feedback 草案，让应用层能感知网络状态。这对我启发很大，因为我做 AI+Network，AI 实时交互同样需要这种跨层协同的思维。”

---

> **整理时间**：2026年3月  
> **说明**：本笔记基于 IETF 125 MOQ 公开演讲内容整理。仅用作学习。

