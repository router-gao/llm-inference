# 完整范围与里程碑排期 v0.6

状态：待用户review。全部明确要求纳入20项稳定需求，不因后续补充而遗漏。以下为交付顺序与依赖排期；尚未估算工作量或承诺日历日期。当前M0设计，没有页面实现。M1–M3构成主站第一版（视频已独立），M1仅是首个增量。

## 逐项排期与责任

“—”表示该阶段无新增交付，不表示从项目删除。可选阅读是呈现方式，仍需交付。

| 需求 | M1：基础旅程 | M2：机制/容量/源码 | M3：部署/运维 | 主责 / 验收配合 | 实现任务 |
| --- | --- | --- | --- | --- | --- |
| REQ-01 酒店Agent | 八步及正常/异常路径 | — | — | inference + experience / quality | DEV-02 |
| REQ-02 点击/四视角 | 同步、回退、复位、两层阅读 | 复用于新场景 | 全课程同步与链接 | experience / product + quality | DEV-01/02 |
| REQ-03 token/prefill/QKV/KV | 词汇与基础生成 | 缓存与资源深化 | 联系通信 | inference + infra / quality | DEV-03/08 |
| REQ-04 模型参数/张量/Dense/MoE | 数组、形状、配置基础 | 配置与容量联动 | 专家路由与通信 | inference + infra / quality | DEV-10/06 |
| REQ-05 延迟/并发/吞吐指标 | 可点击时间线 | 完整口径、分位数与SLO | 运维指标联动 | inference + infra / quality | DEV-08/05/11 |
| REQ-06 单卡并发/ GPU数量 | 单卡多请求队列 | 连续batch、KV与每卡预算 | 分片每卡预算/副本取舍 | infra + experience / quality | DEV-03/05/06 |
| REQ-07 embedding/reranker/RAG | — | 入库/查询/引用/无证据全流程 | 运维案例复用 | inference + experience / quality | DEV-04 |
| REQ-08 GPU代际与参数 | — | 参数与代际对照 | 平台、互联和体验权衡 | infra + experience / quality | DEV-09 |
| REQ-09 UCS支持GPU | — | 官方支持/规格/生产体验表 | 卡数与整机拓扑 | infra / quality | DOC-09、DEV-09 |
| REQ-10 多卡/AI网络/DPU | 请求/工具网络路径 | RAG/存储/加载路径 | TP/PP/副本、RDMA/RoCE、流量/拓扑/拥塞、DPU | infra + experience / quality | DEV-06/12 |
| REQ-11 多模型/虚拟GPU | — | — | 分配/隔离、直通/vGPU/MIG/时间共享、Pod语义 | infra + experience / quality | DEV-07/15 |
| REQ-12 运维定位 | 基础慢请求 | 高峰与知识更新 | 争用/通信/节点故障 | infra + inference / quality | DEV-11 |
| REQ-13 GPU起源/架构 | 历史可选入口、CPU/GPU与显存 | 计算单元/矩阵加速/缓存/算与搬 | 互联关系 | infra + experience / quality | DEV-13 |
| REQ-14 NVIDIA认证 | — | 学习方向概览 | 官方核验后的考试/课程对照 | infra + 技术编辑 / quality | DOC-15、DEV-14 |
| REQ-15 NVIDIA/AMD/TPU | — | 硬件/软件生态概览 | 兼容、移植、平台/成本取舍 | infra + experience / quality | DEV-15 |
| REQ-16 K8s GPU原理 | — | — | 驱动/插件/声明/分配/Ready/故障与调度边界 | infra + experience / quality | DEV-16 |
| REQ-17 车辆Demo/PyTorch/源码 | 车辆颜色/车型流程可选入口 | PyTorch、逐步源码与shape/device | 服务/K8s运维联动 | inference + experience / quality | DEV-17、DEMO-01 |
| REQ-18 文生视频 | — | 已转移独立项目 | 已转移独立项目 | video-studio团队 | 原DEV-18转移 |
| REQ-19 友好/寓教于乐首页 | 故事首屏、可点击酒店、兴趣路线与小挑战 | RAG/视频场景入口 | 方案/运维入口，不增加认知负担 | product + experience / quality | DOC-19、DEV-19 |
| REQ-20 视频独立首页 | — | 已转移独立项目 | 已转移独立项目 | video-studio团队 | 原DEV-20转移 |

## 阶段退出条件

- **M0**：PRD、角色、课程、体验、架构、排期和验证文档齐全；全部要求可追踪；用户review意见落实；未知事实标明，不当作批准或测试结果。
- **M1**：友好故事首页、兴趣路线和小挑战，以及酒店八步/四视角、基础推理/指标/配置/GPU和车辆流程可访问；确认/异常/重置正确，鼠标键盘、窄屏和减少动效验证，目标读者及非IT访客试读记录。
- **M2**：RAG、容量并发、模型配置、GPU/UCS及加速器对照、PyTorch源码、学习方向完成对应交付；公式/单位/边界正确，真实规格与源码有依据；未核验项不称完成。
- **M3**：多卡网络/DPU、多模型/vGPU/K8s、专家路由、完整运维及认证信息交付；主站18项活跃需求验收闭环，2项转移到独立项目，来源与限制可追溯。
- **发布准备**：每阶段可准备静态产物、运行说明、测试证据与版本记录；实际发布位置/公开范围由用户决定。未完成内容不可因发布标为完成。

## 依赖与阻塞

| 依赖 | 影响 | 处理方式 |
| --- | --- | --- |
| 官方来源访问 | UCS支持表及认证/具体设备参数核验 | Cisco曾返回代理403；允许域名草稿已保存但未证明生效。核验前保留未知，不凭记忆填兼容数据 |
| 原车辆Demo代码、权重与许可 | 原Demo真实源码导读/复现 | 尚未提供；可独立设计教学样例，必须另标来源。原Demo复现DEMO-01单独阻塞 |
| 模型/框架/平台版本 | 张量、量化、分片、vGPU、DRA等真实能力 | 专业负责人固定算例、读取来源并记录版本；设计可独立推进 |
| 目标读者试读 | 教学可理解性验收 | 尚未开展；AI代理审查不能替代真实目标读者反馈 |
| 发布位置与公开范围 | 发布实施 | 对应阶段决定，不阻塞本地静态设计 |

阶段内先补内容与来源→状态/公式/页面→专业交叉审校→QA与试读→用户关键产物review。精确日期待设计review和工作量拆分后给出，不将未获凭证/代码的事项默默延期或删除。

[灵感随手记](ideas.md)不进入本矩阵，除非用户明确转为要求。范围变化同步[PRD](../product/requirements.md)、[任务板](tasks.md)、课程与验收，保留编号。

最新决定：REQ-18/20从主站M1–M3交付移出，历史描述不再作为当前承诺。主学习站18项活跃需求+2项转移记录；独立项目维护V0/V1/V2。
