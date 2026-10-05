# 思科AI网络预研报告 v0.1

日期：2026-10-04。状态：供用户讨论的预研，不自动转为正式需求。目标是筛选适合本项目的内容，而非采购建议或完整产品支持矩阵。

## 1. 结论与建议

建议把“网络如何让GPU少等待、如何定位AI服务慢、如何把已有云网络经验迁移到AI”作为主线。优先采用拥塞处理、可观测性、多租户GPUaaS和运维工作流；将Silicon One、Nexus、Hyperfabric、Secure AI Factory作为具体Cisco案例，避免课程变成SKU或营销名词目录。

本轮已实际读取8个Cisco官方页面，包括一篇VXLAN EVPN GPUaaS技术白皮书。网页证明的是官方定位和描述，不证明所有平台/版本都具备相关能力，也不是独立性能验证。此前官方访问受阻，本轮同域请求已成功；这不证明网络草稿已经发布，亦不等于先前所有UCS/认证核验已完成。

## 2. 研究方法与证据层级

通过HTTPS获取官方页面并阅读正文；先从AI入口定位有效产品链接，再读取技术白皮书。旧Silicon One路径返回404，已用入口页提供的新路径取得正文。链接与论断对应见第7节。

证据分为：A 官方技术文档描述，B 官方产品/方案页定位，C 团队教学建议。A/B均需实际平台与软件版本确认，未开展Cisco设备实验、独立benchmark或客户试读。所有性能提升、集群规模和“最快”等措辞保留为厂商声明，不当作本项目实测。

## 3. 候选方向及思科特色

| 方向 | 官方资料中实际看到什么 | 对读者的价值 | 边界 / 证据 |
| --- | --- | --- | --- |
| Nexus One与AI Networking | 将silicon、系统、光模块、软件与运维模型组织成统一方案；本地Nexus Dashboard与云端Hyperfabric是相关管理路径 | 建立从芯片到运维的分层图，识别每层职责 | 当前命名以读取页面为准，组件支持按具体型号核验；B/S2、S6 |
| Silicon One | 可编程网络芯片产品家族，覆盖不同网络角色；页面列G/P/Q等方向，不能仅视为GPU互联专用芯片 | 网络ASIC与GPU/DPU各负责什么；端口速率、总交换容量、缓冲的区别 | 不把芯片总容量当单服务器/单GPU带宽；代际/SKU不深入背诵；B/S4 |
| Intelligent Packet Flow | 官方说明live telemetry、congestion-aware load balancing及fault detection组成相关能力 | 用热点链路与通信等待解释AI fabric流量处理 | 具体算法/生效条件/版本仍需技术文档；不暗示交换机懂token或自动修复模型性能；B/S3、S6 |
| Nexus Dashboard | 官方介绍AI fabric配置模板、RoCEv2可见性、拥塞分析与自动化 | 与网络维护工作直接相连，建立指标到下一检查动作的流程 | 产品页与简介对job级、拓扑、NIC可见性采用不同当前/演进措辞，不能一概称已可用；B/S3、S6，A/S8示例 |
| Hyperfabric | 云管理fabric设计、部署、监控与生命周期；页面区分完整基础设施与BYO AI路径 | 对云维护读者解释“管理面在云中”与工作负载所在位置 | 云管理不等于模型计算在公有云；不承诺所有NX-OS功能同等开放；B/S7 |
| GPUaaS VXLAN EVPN | 白皮书以C885A M8 H26、Nexus 9300、Nexus Dashboard为例，说明rail优化、布线、PFC/ECN、分租户与配置 | 最接近读者已知的EVPN/VRF/QoS，解释怎样支撑GPU服务 | 单篇设计不是通用支持清单；网络隔离不等于GPU/VM显存隔离；A/S8 |
| Secure AI Factory / Cisco AI PODs | 官方定位为模块化参考设计，组合计算、网络、安全、可观测性及软件/存储生态 | 说明“能开机”到“能提供AI服务”的差距；Cisco AI POD不是K8s Pod | 参考架构验证不等于任意配置/负载性能保证；B/S5 |
| BlueField DPU与安全 | Secure AI Factory页列出Hybrid Mesh Firewall与NVIDIA BlueField DPUs的组合方向 | 将已有DPU概念连接到基础设施安全职责和卸载位置 | 没有因此证明每台UCS支持BlueField或任意DPU都等价；B/S5 |
| Spectrum-X与多厂商生态 | 官方方案区分Cisco芯片与NVIDIA交换芯片相关系统，描述跨伙伴验证方向 | 网络芯片、交换系统、GPU厂商不应一一绑定；选择需看整套支持 | 不能推出任意NVIDIA/AMD模型或网卡混搭都受支持；B/S5、S6 |
| Ultra Ethernet | 页面写“ready”与mandatory network-side requirements | 作为标准演进的可选解释 | 不等于当前所有设备/NIC已实现完整端到端能力；需标准、型号、版本另核验；B/S3、S6 |

## 4. 推荐入选内容与交互设计

以下为候选，尚未更新PRD或开发任务。现有REQ-10/12等可承接，减少重复课程。

| 候选ID | 建议与阶段 | 可点击内容 | 读者应该能解释 |
| --- | --- | --- | --- |
| CNET-01 AI网络分层与数据路径 | 优先，M2概览/M3深化；关联REQ-10 | 应用、GPU服务器、NIC、leaf/spine、管理/存储逐层点亮 | 链路带宽、交换容量和显存带宽为何不同 |
| CNET-02 拥塞与Intelligent Packet Flow | 优先，M3；REQ-10/12 | 两条路径/热点/遥测/反馈或流量选择，加入ECN/PFC独立机制说明 | GPU等待何时来自通信，何时不是；不能推导真实提速倍数 |
| CNET-03 Nexus Dashboard式运维定位 | 优先，M3；REQ-12 | TTFT/ITL、GPU等待、NIC和网络指标的关联时间线 | 看到拥塞证据后检查什么，而非看利用率猜结论 |
| CNET-04 EVPN多租户GPUaaS | 优先，M3；REQ-11/16 | 租户→VRF/VNI→节点/Pod→GPU分配，分别显示网络/计算隔离 | 网络分段、K8s资源与vGPU/MIG不是同一层隔离 |
| CNET-05 本地/云管理工作流 | 可选，M3；REQ-12 | 本地Dashboard与Hyperfabric部署/监控路径概念对照 | 管理位置与数据面位置不同，升级和权限责任需确认 |
| CNET-06 Secure AI Factory / AI POD与DPU | 概览建议，M3；REQ-09/10/11 | 网络、计算、存储、安全、软件、管理六块拼图 | Cisco AI POD不是K8s Pod，DPU/网络不能替代模型服务 |
| CNET-07 Silicon One/UEC/Spectrum-X深层产品比较 | 作为可展开资料，暂不做独立必修章 | 分层术语和来源卡，不做未经验证品牌性能榜 | 通用原理与厂商实现不同，能力按平台核验 |
| CNET-08 AI运维助手/AgenticOps | 后续候选，不建议挤入首版网络主线 | “AI帮助运维”与“网络支持AI”对照 | 二者是不同学习目标；自主变更需权限和控制 |

建议第一轮选择CNET-01—04，加CNET-06一页概览；CNET-05/07可展开，CNET-08后续考虑。它们覆盖网络维护、云维护、售前方案解释三类任务。不是全部增加独立章节，优先放进既有网络、多模型与运维章节。

## 5. 推理项目特别要避免的误导

- 厂商材料常同时讨论训练和推理。JCT不直接等于TTFT/ITL；大量训练通信优势不能无条件移植为单卡推理收益。
- 单卡多副本/普通RAG、TP/PP跨机、MoE专家并行、prefill/decode分离的数据路径不同，先选负载再谈网络能力。
- “无损”网络不是无拥塞/无延迟/永不丢包保证；PFC可能暂停传播，ECN/拥塞控制需端到端理解。
- 总交换容量与端口速率不是有效应用吞吐；“ready”不等于端到端所有功能已部署。
- 分租户VRF/VNI不是模型授权、GPU显存隔离或K8s配额；每层控制分别展示。
- 厂商案例图和演进能力可以教学，不能把页面截图当成已验证操作手册。避免未经许可复制完整UI或把静态模拟标为真实管理平台。

## 6. 预研限制与下一步

S8白皮书提供了具体工程依据，但正文不同位置出现节点/GPU规模表述差异；本报告不采用其总规模作为课程算例。S3与S6对可观测性当前与演进能力措辞不同，需发布说明/版本文档进一步核对。对“行业第一”“最快”“提升百分比”等未取得测试方法的宣传不引用为性能结论。

待与你确定范围后，再完成：目标交换机/NX-OS/Dashboard版本；IPF技术实现与适用平台；ECN/PFC/端点组合；Hyperfabric功能边界；对应CVD及DPU组合。将已批准候选映射到PRD、课程、排期，再写结构化场景与验证用例。本次没有自动新增REQ编号，也没有开展产品实现。

## 7. 已读取资料清单与论断用途

以下均于2026-10-04实际HTTPS读取成功。状态“已读取”指正文核对，不等于独立真实性能或机型兼容核验。

| 来源ID | 官方资料 | 支持范围 |
| --- | --- | --- |
| S1 | [Cisco AI入口](https://www.cisco.com/c/en/us/solutions/artificial-intelligence.html) | 产品方向与有效入口，不作为技术参数证据 |
| S2 | [AI Networking in Data Center](https://www.cisco.com/site/us/en/solutions/artificial-intelligence/ai-networking-in-data-center/index.html) | Nexus One、网络方案、芯片至管理定位 |
| S3 | [Nexus 9000系列](https://www.cisco.com/c/en/us/products/switches/nexus-9000-series-switches/index.html) | RoCE、IPF、Dashboard及UEC官方能力说明 |
| S4 | [Silicon One](https://www.cisco.com/site/us/en/products/networking/silicon-one/index.html) | 网络芯片家族与角色定位 |
| S5 | [Secure AI Factory with NVIDIA](https://www.cisco.com/site/us/en/solutions/artificial-intelligence/secure-ai-factory/index.html) | 参考方案组件、AI POD、DPU/安全组合方向 |
| S6 | [Nexus AI Networking At-a-Glance](https://www.cisco.com/c/en/us/products/collateral/networking/cloud-networking-switches/nexus-9000-switches/nexus-9000-ai-networking-aag.html) | IPF、管理、交换系统/芯片的官方简介 |
| S7 | [Nexus Hyperfabric](https://www.cisco.com/site/us/en/products/networking/data-center-networking/nexus-hyperfabric/index.html) | 云管理与BYO/整套基础设施定位 |
| S8 | [Building AI/ML Data Center Fabric using VXLAN EVPN for GPUaaS](https://www.cisco.com/c/en/us/td/docs/dcn/whitepapers/building-aiml-dc-fabric-using-vxlan-evpn-for-gpuaas.html) | rail/布线、QoS/PFC/ECN、EVPN租户与运维工程示例；具体配置不直接照搬 |

## 8. 供讨论的三个问题

1. 是否接受“拥塞/可观测性/租户与调度”为主线，以Cisco产品解释实现，而不是先做产品目录？
2. 是否把Hyperfabric和Secure AI Factory作为概览，还是需要完整操作工作流？
3. 是否有你最关注的Cisco产品/现网版本或典型客户场景？没有时按上述代表方向研究，不阻塞通用教学。

## 9. Cisco AI POD网络设计专题：待补预研

用户关注Cisco AI POD网络设计；本项属于RES-01，关联REQ-09/10/11/12/16。当前CNET-06仅为方案概览，不能视为完整网络设计预研已完成。研究本身与课程候选入选分开记录：可以补充研究，候选是否进入实现仍需讨论。

待补交付：选定具体AI POD参考架构/CVD及版本；区分推理负载、训练及混合负载；绘制GPU—NIC亲和性、rail/leaf-spine、业务/计算/存储/管理网络与故障域；说明布线、端口/链路预算、超售假设、RoCE端点/QoS/ECN/PFC条件；梳理EVPN租户隔离、DPU安全、Dashboard可观测性及验证方法。每个设计选择附官方来源、适用条件和未知项，不用产品概览推定任意组合支持。

完成标准：提供可追溯设计图、关键设计取舍、版本/支持证据表、未决问题和课程映射建议。当前未完成具体CVD、设备版本及配置组合核验，无设备实验或性能验证；不新增已批准开发承诺。
