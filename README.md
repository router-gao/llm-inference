# LLM Inference：交互式学习材料

以酒店预订等具体场景解释 LLM 推理、Agent、RAG、GPU 部署与通信。面向具有网络与IT背景、缺少AI背景的思科客户、合作伙伴、销售与售前工程师，采用直观解释加可展开工程细节的方式。

第一版是中文静态交互模拟，不执行真实预订、不调用真实模型 API。当前处于文档规划阶段，尚无可运行页面。

## 创意起点

[⚡ Spark Zero｜创意原点](docs/vision/spark-zero.md)：第一轮头脑风暴全景，记录两个项目的初衷、主题、待探索问题与推进约定。

## 重要文档 review

- [需求文档 HTML 阅读版](docs/review/requirements.html)

从[整体设计 review 入口](docs/project/review.md)开始，建议先看[需求](docs/product/requirements.md)和[角色分工](docs/project/team.md)，再看[课程地图](docs/content/curriculum.md)、[交互](docs/design/experience.md)与[架构](docs/design/architecture.md)。本版为v0.7待review设计，未获用户批准。

## 项目文档

- [遗留问题台账](docs/project/open-issues.md)
- [Release Notes](RELEASE_NOTES.md)

- [灵感随手记（不属于正式需求）](docs/project/ideas.md)

- [团队与开发流程](docs/project/workflow.md)
- [任务板](docs/project/tasks.md)
- [决策记录](docs/project/decisions.md)
- [需求与学习目标](docs/product/requirements.md)
- [目标读者与教学表达规范](docs/product/audience.md)
- [常见术语与性能指标](docs/content/glossary.md)
- [车辆识别Demo、PyTorch与源码导读](docs/content/vehicle-demo-pytorch.md)
- [文生视频](docs/content/text-to-video.md)
- [模型、Agent 与 RAG](docs/content/inference.md)
- [GPU起源与基础架构](docs/content/gpu-foundations.md)
- [NVIDIA/AMD/TPU、虚拟GPU与K8s](docs/content/accelerators-virtualization-k8s.md)
- [GPU、网络与资源规划](docs/content/infrastructure.md)
- [AI网络、数据路径与DPU](docs/content/ai-networking.md)
- [UCS GPU：参数与用户体验对照](docs/content/ucs-gpu-comparison.md)
- [交互设计与前端架构](docs/design/experience.md)
- [验收与事实核验](docs/quality/validation.md)
- [NVIDIA认证与继续学习](docs/content/nvidia-certifications.md)

先完成需求、内容与设计评审，再按任务板进入实现。运行与测试命令将在技术方案落地后补充。

## 预研与待讨论候选（不自动成为正式需求）

- [需求与功能预研入口](docs/research/README.md)：大需求处理流程及当前预研列表。

- [思科AI网络预研报告](docs/research/cisco-ai-networking.md)：官方资料、适合课程的候选与取舍建议。

- [网络知识库微调Demo预研](docs/research/network-knowledge-finetuning.md)：独立候选，尚未训练或加入站点实现排期。

- [文生视频：Seedance、本地部署与跨地区产业预研](docs/research/video-cloud-local-global.md)：VID候选待讨论，不自动扩展REQ-18排期。

- [初学者友好首页设计](docs/design/homepage.md)：REQ-19，故事与趣味互动优先。

- [文生视频独立炫酷首页设计](docs/design/video-homepage.md)：REQ-20，面向大众的作品入口。

## 项目拆分

文生视频与文生图由独立项目 [Omni Canvas](https://github.com/router-gao/omni-canvas) 管理，本地位于 `/workspace/omni-canvas`（原 video-studio）。主站 REQ-18/20 保留转移记录，不再承担视频首页发布。Omni Canvas 仓库已由用户创建，内容推送与公开站点尚未完成。
