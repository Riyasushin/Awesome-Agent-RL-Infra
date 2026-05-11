Agent RL Paper Reading
> 
这里保存我看的相关文章

Rollout是 IO-intensive吧
Env/sandbox 和 LLM 要不要完全解耦，因为中间信息(文本、图像、视频、音频)走的是HTTP

# 技术报告
- [Deepseek v4](https://ycnq7fsv085f.feishu.cn/wiki/Tl4DdMOJuo5va8xuvj1ceyqSnSc)
- 

# 算法相关问题
- Adaptive Layerwise Perturbation: Unifying Off-Policy Corrections for LLM RL
  - off-policy 不稳定性

- PPO  4个模型
- DPO ，不要 Critic 和  Reward Mode, 拉大 好、坏的loss
- GRPO：group  relative
- DAPO: 动态 clip范围
- Breaking the Capability Ceiling of LLM Post-Training by Reintroducing Markov States
  - 经典RL与 LLM RL 的比较

- Tree-GRPO, ToT, ReST-MCTS ???
  - tree-structured rollout

- T²PO    （ICML'26 Spotlight）
  - token-level hesitation: 模型在生成到一定阶段后，继续生成的 token 已经很难带来新的信息
  - **turn-level hesitation**: 在多轮任务中，Agent 可能在某一轮已经进入失败方向，但仍然在后续 turn 中重复相似的 reasoning pattern 或 action pattern。这些 turn 在语义上看似合法，但对任务推进几乎没有帮助。它们不仅浪费环境交互预算，还会让 credit assignment 变得更加嘈杂。
  - 针对上面两个问题提供了: Token- and Turn-level Policy Optimization
    - 构造一个 self-calibrated uncertainty signal
      - 一个自定义的、既保留 entropy 对尾部分布的敏感性，也保留 confidence 对主导 token 的刻画能力，从而更好地反映模型生成过程中的局部分布稳定性的信号

    - Token-level Thinking Intervention
      - 当模型生成到一定长度后，我们持续监控不确定性变化。如果最近一段窗口内的不确定性变化已经低于阈值，就说明 predictive distribution 已经基本稳定，继续生成 CoT 的信息增益有限。此时 TTI 会强制输出 ，结束 reasoning phase，并进入 action generation。
      - 自适应地截断低信息量思考

    - Turn-level Dynamical Sampling
      - 将 token-level uncertainty signal 聚合成 turn-level observation signal，然后比较相邻 turn 之间的变化

# 有趣的训练场景

## Env
- EnterpriseBench / Corecraft

## GUI / VLM
- Thinking with Videos
  - 这里更多是在做AI，RL只是一个小部分

- UI-R1
  - 首个将 DeepSeek-R1 风格的基于规则的强化学习（RL）应用于 GUI 动作预测任务的框架。引入一种新颖的基于规则的动作奖励函数，并仅使用 136 个高质量训练样本

- ComputerRL
  - API-GUI Paradigm

- DART: Efficient Multi-turn RL for GUI Agents via Decoupled Training and Adaptive Data Curation
- A Subgoal-driven Framework for Improving Long-Horizon LLM Agents
  - 网页导航任务

## Code
- [Immersion in the GitHub Universe: Scaling Coding  Agents to Mastery](https://ycnq7fsv085f.feishu.cn/wiki/IJU3dXHtOox1Wqxj66ic9OOsnBm)
  - SWE, 造数据集的
  - 长上下文、多轮、多tool

- CodeScout
  - 关注的核心挑战：当智能体只有通用的终端工具（标准 Unix 终端）时，如何通过有效的强化学习配方训练出能够与使用专用工具的模型竞争甚至更优的代码定位智能体？

SWE-MiniSandbox
- 用 per-instance 挂载命名空间（mount namespace）和 chroot 文件系统隔离替代容器，对 Python 虚拟环境做预缓存（tarball）并用 Ray 控制并发解压，作为 SWE-Rex、SWE-agent 和 SkyRL 的 drop-in 替换。 这意味着可以在不维护 Docker runtime 的情况下进行大规模多节点 RL 训练。
- 如果是不开docker, 那么传哪些文件系统
SWE-World
- 用训练在真实 agent-环境交互数据上的 LLM 模型（SWE-World Transition Model, SWT）来预测中间执行结果和最终测试反馈，让 agent 无需与物理容器化环境交互即可学习，同时保留标准的 agent-environment 交互循环。 完全 Docker-free 的流水线使 Qwen2.5-Coder-32B 从 6.2% 提升到 SFT 52%、RL 55%，配合测试时缩放达到 68.2%，超越了需要真实 Docker 的基线
- ？？？？
LLM-in-Sandbox
- 让 LLM 在代码沙箱（虚拟计算机）中探索，通过仅使用结果奖励的在线 RL，使弱模型在 sandbox 模式下显著超越 LLM 模式。训练使用通用上下文数据，却能在 Long-Context、Math、Physics、SWE 等多个域上泛化。 底层用约 1.1GB 的轻量 Ubuntu Docker 镜像，预配置 Python 解释器和科学库。

## Memory
- MemGPT(letta)
- MemOS
- openViking
- Cognee
- supermemory
- graphiti
- Mem0
- Memory-R1
  - 通过强化学习增强大语言模型智能体的记忆管理与利用能力

## ?
- MetaClaw
  - Fast Adaptation（秒级技能注入）+ Slow Adaptation（分钟级梯度RL）

# infra
- AReaL
  - 异步

- [AgentRL](https://ycnq7fsv085f.feishu.cn/wiki/P3VGdkbeTo3hKrx7iiJcm94bnXb)
  - zhipu的框架

- [Slime](https://ycnq7fsv085f.feishu.cn/wiki/DSsIdx02nodHbRxameJcVAqdnGd)
- ARL-Tangram: Unleash the Resource Efficiency in Agentic Reinforcement Learning
- [Heddle](https://ycnq7fsv085f.feishu.cn/wiki/Mq3sd93ktoUOZbxxOMCcgjEXnte)
- [Roll-art](https://ycnq7fsv085f.feishu.cn/wiki/XGucdO52woSUuFx7tGYcf1xknHc)
  - 给 task 打一个 tag, 根据怼资源的需求和机器特征调度到不同的集群
  - 优化 同步（没看懂

- [Let It Flow](https://ycnq7fsv085f.feishu.cn/wiki/RxzddcvmPopYAixDWGncyk1AnNb)
- [Roll Flash](https://ycnq7fsv085f.feishu.cn/wiki/WeYldGVaYosUM4xnzJtc6fpvnsg)
- HetRL
  - 如何在异构 GPU 环境中高效地使用强化学习（RL）训练大语言模型（LLM）。随着高端 GPU 变得稀缺且地理分布化，组织需要能够利用不同区域中未充分利用的中端和前几代 GPU 的系统。

- Jet-RL
  - 在FP8环境下稳定的On-policy RL训练方案，解决常见BF16训练+FP8 rollout在长时域推理中出现的不稳定问题

- EARL
  - 基于上下文长度与系统负载动态自适应张量并行配置（有点无聊）
  - 在训练阶段间提供高效、布局感知的数据传输

- GEAR
  - 针对现有解决方案（特别是 Reverb）中的三大瓶颈：内存效率、轨迹选择的计算效率、轨迹收集的通信效率。通过新颖的 GPU 中心化设计选择

- MindSpeed RL
  - Ascend NPU集群

- ProRL Agen
  - 把agent rollout生命周期作为独立HTTP服务，与RL trainer完全解耦

- RL in the Wild
  - 首次对真实世界 LLM 部署场景中的**可验证奖励强化学习 (RLVR)** 训练系统进行了全面的特征刻画研究

- RLAX
  - TPU上RL

- RollArt
  - 智能体 RL 工作负载高度异构：包含计算密集的 prefill 阶段、带宽受限的解码、以及带状态的 CPU 重环境模拟

- RollPacker
  - 针对LLM rollout阶段长尾响应分布引发的GPU利用率低下问题。通过“尾部批处理”（tail batching）调度，将长尾样本集中到专门的“长轮次”

- SimpleTIR
  - 多轮 TIR 中的训练不稳定性源于**外部工具反馈引起的分布偏移**，这导致了低概率 token，并在连续轮次中累积，引发灾难性的梯度范数爆炸

- SortedRL
  - 优化rollout时候的长尾

- [Seer](https://ycnq7fsv085f.feishu.cn/wiki/Rzq8dYMBsoU4npx5VyfcyOMwnDf)
  - 优化 rollout的长尾, 预测同组剩余responses的长度

- [ROLLMUX](https://ycnq7fsv085f.feishu.cn/wiki/OkogdpLO2ovZxrxeoenc7ECfn9c): Phase-Level Multiplexing for Disaggregated RL Post-Training
- Asynchronous RLHF: Faster and More Efficient Off-Policy RL for Language Models
  - 24.10的老文章了

- [ReSpec](https://ycnq7fsv085f.feishu.cn/wiki/ZXOHdBaGHon1gPxlEqtcwTAhnLh): Towards Optimizing Speculative Decoding in Reinforcement Learning Systems
  - 又见投机解码

- [Tool Zero](https://ycnq7fsv085f.feishu.cn/wiki/QHcYdTg63oqDHExnOgCcS7vxndq): Training Tool-Augmented LLMs via Pure RL from Scratch
  - 纯 RL 从零学 tool use
  - 算法题

- [BudgetThinker](https://ycnq7fsv085f.feishu.cn/wiki/PXNPd6jZhoAfiPxpidbcAWTrnAe)
  - 动态控制 token + 课程式 RL 训练，精确控制推理长度

- [DualPath](https://ycnq7fsv085f.feishu.cn/wiki/KDnldnIz3ojS9RxgL2Bcqz5UnYg)
  - DpSk的
  - KV Cache存储I/O瓶颈优化
  - 专门针对Agentic场景的多轮推理优化

[XServ](https://ycnq7fsv085f.feishu.cn/wiki/KItRd9KP4oZo8axghhmcTNLgnGe)
- 将 OS 的 VFS/虚拟内存思想系统性地应用于 AI 推理，提出 Capability-centric API，解耦应用开发与模型演进
- [KUNSERVE](https://ycnq7fsv085f.feishu.cn/wiki/OdFIdX2NnowVZ9xkNHmcVgdKnqZ)
- [AdaServe](https://ycnq7fsv085f.feishu.cn/wiki/DB08dymIUoUzqwx86MOc4MtSnDh)
  - 投机解码

- 

# MARL 的 infra
- FlexMARL
  - 首个端到端训练框架，对大规模基于 LLM 的多智能体强化学习（MARL）的 rollout、训练及其编排进行整体优化

- [MARTI-MARS2](https://ycnq7fsv085f.feishu.cn/wiki/ItZ1dkpqFoEXZBxqu0ecVaeAnOg)

# Agent-aware Inference
- Continuum
  -  toll-use aware scheduling

# Env
- Prefill-as-a-service
  - 

# Env(todo)
- Deepseek 3fs

容器迁移与 Checkpoint/Restore
- **Layered Transfer: Stateful Container Migration with Lazy Volume Transfer**P.M. Lindner, University of Groningen, 2024来源：https://fse.studenttheses.ub.rug.nl/34290/1/mCS2024LindnerPM.pdf内容：Kubernetes + CRIU + DinD 容器迁移实测，包含 checkpoint 大小、迁移时间、与冷启动对比。
- **Container Migration over HTTP in Kubernetes**来自 ELTE 博士论文，Kubernetes 容器状态通过 HTTP POST 跨节点传输。来源：https://edit.elte.hu/xmlui/bitstream/10831/86122/1/Dissertation_Final.pdf
跨数据中心 / WAN 迁移
- **CloudNet: Dynamic Pooling of Cloud Resources by Live WAN Migration**University of Massachusetts Amherst / University of Utah, 2012来源：
  - https://users.cs.utah.edu/~kobus/docs/cloudnet.vee.pdf
  - https://web.cs.umass.edu/publication/docs/2012/UM-CS-2012-005.pdf内容：VM 跨 WAN 迁移优化，100 Mbps 链路 pause time 从 0.04s → 7.7s 的实测数据。

- **A Comprehensive Review of Live Migration Technologies**Springer, 2026来源：https://link.springer.com/article/10.1186/s13677-026-00883-9内容：VM/容器/UniKernel 迁移技术综述，含 RDMA、GPU、RDMA 迁移子秒级 downtime 数据。
数据中心网络与 RPC 延迟
- **Efficient Remote Procedure Calls for Datacenters (FaSST)**CMU CS-19-126, 2019来源：http://reports-archive.adm.cs.cmu.edu/anon/2019/CMU-CS-19-126.pdf内容：数据中心网络延迟演进（2009 vs 2019），kernel-bypass RPC 设计，RTT ~10 μs 级。
- **Evaluating the Impact of Inter-cluster Communications in Kubernetes**arXiv:2409.09278来源：https://arxiv.org/pdf/2409.09278内容：Kubernetes 跨集群通信延迟测试，HTTP payload 大小对延迟的影响。
分布式系统与负载均衡
- **Towards Performance-Driven System Support for Distributed Applications**Purdue University, JPDC 1999来源：https://www.cs.purdue.edu/nsl/jpdc99.pdf内容：进程迁移 vs 本地执行的完成时间对比，耦合度与迁移收益的关系。
- **Block: Balancing Load in LLM Serving with Context, Knowledge and Predictive Scheduling**arXiv:2508.03611v2来源：https://arxiv.org/html/2508.03611v2内容：stateless scheduler 设计，避免 live migration 的集中式调度开销。

- **Engineering Inference: KV Cache, Shared Storage, and the Economics of AI**
  - NetApp Tech Blog, 2026
  - vLLM + LMCache + 共享存储的多层级 KV Cache 设计。

# 胡看看到了的，无关

- https://mp.weixin.qq.com/s/QNXMq7vscUT4NByShv_Gpg
  - 编译器优化
  - 用编译器生成取代运行时解释?

- https://www.zhihu.com/question/2030224013700678490/answer/2030224773230360120
  - 离谱中又透露一种合理

# **Agentic Systems Canon: 30 Papers (Auto-imported)**
## **L0 基础与表示**
• The Latent Space: Foundation, Evolution, Mechanism, Ability, and Outlook — 隐空间作为 Agent 原生基底，从冗余语言接口向高维连续向量空间的范式转移。

## **L1 能力构建与推理自适应**
• Agentic 能力从哪里来？拆解基座大模型的训练过程 — 从预训练到 Mid-Training 到五层后训练，Agent 数据形态是“任务+环境+反馈+轨迹”。
• ICLR 26 Oral: In-Place Test-Time Training — 将 Transformer MLP 改造为可动态更新的快权重，分块并行 + LM-Aligned Objective，不改架构即可推理时自适应。

## **L2 系统架构与编排**
• Anthropic: Harness Design for Long-Running Application Development — 三角色架构（Planner/Generator/Evaluator）解耦生成与评估；Context Reset 解决长程任务的累计误差与上下文焦虑。
• OpenAI: Engineering with Codex in an Agent-First World — 100万行零人工代码实验；渐进式披露、环境可观测性、GC式重构；验证成本成为主矛盾。
• AEnvironment — An Environment System for the Agentic RL Era — “Everything as Environment”抽象，EnvHub+K8s Controller，环境服务化。
• When LLMs Grow Hands and Feet, How to Design our Agentic RL Systems? — Rollout 系统工程：Unified Data Interface、Remote Environment Pool、Partial Rollout、异步流水线。

## **L3 训练信号与优化（上）**
• Walk the Talk: MAPO — 语义锚定+CLIP裁判解决多模态 Reasoning-Action Gap；轨迹感知折扣因子防冗余刷分。
• Self-Distilled RLVR (RLSD) — 方向-幅度解耦：环境奖励定方向，自蒸馏信号调幅度；stop-gradient 防止特权信息泄漏。
• Agentic Proposing: Enhancing LLM Reasoning via Compositional Skill Synthesis — MGPO 双层 Advantage（轨迹级+阶段级），组合逻辑工程自动合成高难度训练题。
• Act Wisely: HDPO — 条件式效率 Advantage 只在正确答案集合内比较，实现准确率与效率的分层 SLO 解耦。

## **L3 训练信号与优化（下）**
• Learning beyond Teacher: G-OPD / ExOPD — 将 OPD 重解释为 KL 约束下的 dense reward RL；λ>1 的奖励外推可超越教师，但需警惕隐式 reward hacking。
• DeepMind: Reinforced Attention Learning (RAL) — 直接优化内部注意力分布而非输出 token；冻结视觉编码器仅更新 LM 主干即可提升细粒度感知。
• Composition-RL (混元) — Sequential Prompt Composition 将简单可验证题拼接为高难度组合题，延续 RL 训练信号。
• Intrinsic Credit Assignment for Long Horizon Interaction — 用每轮后模型对正确答案的置信度变化（∆Belief）作为内在奖励，无需 critic。
• SeeUPO (通义) — 基于 HAML 的多轮 Agentic RL 收敛保证；反向顺序更新（T→1）+ 两段重要性采样，实现 critic-free 稳定训练。
• On Robustness and CoT Consistency of RL-Finetuned VLMs — RL 提升准确率但降低 CoT 忠实性；文本偏见可压制视觉信息，需多维评估。
• Save, Load and Learn: Rollback-based Curriculum Learning — 从成功轨迹 checkpoint 逐步回滚到初始状态，时间维度的课程学习。

## **L4 环境 Scaling 总纲**
• Environment Scaling for Interactive Agentic Experience Collection: A Survey — GEF 循环（Generation-Execution-Feedback）；10 维度 Scaling；Generator-Verifier Asymmetry。

## **L5 环境合成实例**
• Tool-R0: Self-Evolving LLM Agents for Tool-Learning from Zero Data — Generator-Solver 自博弈，零人工数据；课程奖励动态适配模型能力边界。
• RLVE: Scaling Up RL for Language Models with Adaptive Verifiable Environments — 400 个程序化环境自适应难度；Scaling Law：环境多样性 > 同环境数据量。
• EnvScaler: Scaling Tool-Interactive Environments via Programmatic Synthesis — 终态验证代码（不看过程看结果）；支持无对话与对话双模式。
• Agent World Model (AWM): Infinity Synthetic Environments for Agentic RL — 代码+SQL 作为 IR，1000 环境；历史截断对齐训练-推理一致性。
• ScaleEnv: Scaling Environment Synthesis from Scratch — 可执行领域图（Domain Graph）+ 数据库状态规则校验；领域数与泛化正相关。
• TerminalTraj: Large-Scale Terminal Agentic Trajectory Generation — ScoreModel 筛选 + Docker + pytest 硬验证；终端场景工业级数据流水线。
• Gym-V: A Unified Vision Environment System for Agentic Vision Research — 179 个跨类别统一接口视觉环境；训练方法 > 参数规模。

## **L6 架构与系统效率**
• MiniCPM-SALA: Hybridizing Sparse and Linear Attention — 1:3 混合注意力 + HyPE 混合位置编码；渐进式训练转化长上下文高效架构。
• LatentMoE: Toward Optimal Accuracy per FLOP and Parameter in MoE — 低维潜空间投影做专家路由与计算；λ-MoE（降通信）与 k-MoE（扩组合空间）。
• Locas: Principled Initializers of Locally-Supported Parametric Memories — 测试时训练外挂模块；Top-K 活跃维度克隆初始化 + 权重范数剪裁防遗忘。

## **L7 评测基准**
• Gaia2: Benchmarking LLM Agents on Dynamic and Asynchronous Environments — 动态异步 Agent 评测；ARE Verifier 动作级可验证；Time/Noise/A2A 三大真实世界挑战。

# 小模型的趋势(garbage)

- 核心判断
- 大模型推理成本太高，1B-7B 小模型 + 垂直领域专业模型正在 resurgence。

- 现有 Infra（vLLM、SGLang、MuxServe 等）假设"单个大模型独占 GPU"，在小模型场景下出现CPU 开销占比过高、模型切换慢、资源碎片严重等系统性低效。
- 2025–2026 关键工作（按技术方向）
- 多模型共置与内存复用
- **MuxServe** (ICML'24)：Spatial-temporal 复用，CUDA MPS 动态分 SM，统一 KV Cache。
- BlockLLM：模型拆分为 block，多租户共享 block，per-block batching。
- S-LoRA / Punica (MLSys'24)：千级 LoRA adapter 共享基础权重。
- Oneiros / MIRAGE (arXiv'25)：动态参数重映射，将 inactive 模型参数内存 repurposed 给 KV cache。
- Prism (arXiv'25)：GPU sharing for cost-efficient multi-LLM serving。
- **Aegaeon** (SOSP'25)：GPU pooling for concurrent LLM serving on the market。
- Valve (arXiv'26)：Production online-offline inference colocation，联合限制抢占延迟和率。

- Serverless 与快速模型切换
- **ServerlessLLM** (OSDI'24)：多级存储快速 checkpoint 加载 + live migration。
- λScale (arXiv'25)：Fast scaling for serverless LLM inference。
- BlitzScale (OSDI'25)：O(1) Host Caching 的 live autoscaling。

- 异构硬件与混合负载调度
- Helix (arXiv'24)：异构 GPU 集群 Max-Flow 调度。
- GreenLLM (arXiv'24)：异构 GPU 上 disaggregated speculative decoding（大模型+小 draft 模型）。
- Inference without Interference (TetriInfer, arXiv'24)：Prefill-decode 分离，mixed downstream workloads。
- Dovetail (arXiv'24)：CPU/GPU 异构 speculative decoding。
- QEIL (arXiv'25)：边缘异构（CPU/GPU/NPU）小模型推理 scaling law。
- CoSense-LLM / EdgeShard / Jupiter / Galaxy：边缘协同推理。
- Cauchy (SoCC'25)：自适应异构部署，动态将模型部署在不同 GPU。
- BOUTE (MLSys'26)：异构模型路由 + 异构硬件部署的算法-系统协同设计。
- Jenga (SOSP'25)：异构显存管理。
- SuperServe (NSDI'25)：Fine-grained inference serving for unpredictable workloads，SubNetAct 动态路由。

- Agentic / 多模型流水线与可编程推理
- Halo (arXiv'26)：Agentic DAG 批处理优化，联合调度 GPU LLM + CPU tool，支持 0.4B–4B light models
- Orla (arXiv'26)：LLM-based multi-agent serving library。
- **ThunderAgent** (arXiv'26)：Program-aware agentic inference。
- Hive (arXiv'26)：Multi-agent infrastructure for test-time scaling。
- Pie (SOSP'25)：Programmable serving (Inferlet/Wasm)，细粒度控制生成循环和 KV cache。
- Murakkab：Resource-efficient agentic workflow orchestration。
- Aragog：Just-in-time model routing for agentic workflows。
- **DualPath** (arXiv'26)：Breaking storage bandwidth bottleneck in agentic LLM inference。

- KV Cache 与显存优化
- DiffKV (SOSP'25)：差异化 KV cache 压缩（K8V4 等）+ 并行 compaction。
- IC-Cache (SOSP'25)：In-context caching for efficient serving。
- FairKV / Mell / gLLM (arXiv'25)：多 GPU KV cache 管理。
- **CacheGen** (SIGCOMM'24)：KV cache 压缩与流式传输。
- MemServe：Disaggregated serving with elastic memory pool。
- RAGCache：RAG 场景知识缓存。

-  PD 分离与分布式 Serving
- **DistServe** (OSDI'24)：Prefill-decode disaggregation for goodput。
- Splitwise：Phase splitting for generative LLM inference。
- LoongServe (SOSP'24)：Elastic sequence parallelism for long-context。
- Llumnix (OSDI'24)：Dynamic scheduling for LLM serving。
- Sarathi-Serve (OSDI'24)：Chunked prefills + decode piggybacking。
- dLoRA (OSDI'24)：Dynamic request + adapter orchestration for LoRA serving。
- TokenScale (arXiv'25)：Token velocity based autoscaling for disaggregated serving。
- KTransformers (SOSP'25)：CPU/GPU hybrid inference for MoE。

- 小模型 / 边缘 / CPU 效率
- Towards Pareto Optimal Throughput in Small Language Model Serving (arXiv'24-25)：指出小模型在 vLLM 上 CPU overhead 可达 50%。
- Blink (arXiv'26)：CPU-free LLM inference，serving stack 卸载到 GPU/SmartNIC。
- Micro Language Models Enable Instant Responses (arXiv'26)：验证极小模型低延迟响应。
- Characterizing Mobile SoC (SOSP'25)：移动 SoC 加速异构 LLM 推理。
- PowerInfer (SOSP'24)：Consumer-grade GPU 快速 serving。
- Serving Hybrid LLM Loads with CPU-GPU Attention Piggybacking (arXiv'26)：CPU-GPU 混合负载。

- 仍存在的 Gap（2026.04 未被充分探索）？？？？？？
- Gap 1 — 单进程超高密度多模型（Single-Process Ultra-Dense）：现有系统（MuxServe / Prism / Aegaeon）基于多进程/MPS，单卡 2-10 个模型即遇瓶颈。缺乏单进程内 30-50 个小模型的亚毫秒级切换。
- **Gap 2 — 单卡零拷贝模型流水线（Intra-GPU Zero-Copy Pipeline）：Halo / Orla 支持 multi-agent DAG，但跨模型通信仍走网络/CPU。缺乏单卡 GPU 显存内直接传递 hidden states 的原语。**
- Gap 3 — CPU-Native Datacenter-Scale SLM Serving：llama.cpp 单机，vLLM CPU 仅为 fallback。缺乏面向 datacenter CPU 集群（AMX / AVX-512）的分布式 serving 系统。

# TODO: Memory
- Memory Intelligence Agent (MIA)
  - arXiv:2604.04503
  - Jingyang Qiao, Weicheng Meng, Yu Cheng 等 (华东师大、上海AI实验室)
  - 深度研究智能体的记忆能力
  - Manager-Planner-Executor 三层架构
    - Memory Manager: 存储压缩的历史搜索轨迹（非参数化记忆）
    - Planner: 参数化记忆代理，生成搜索计划（可动态演化）
    - Executor: 执行搜索和分析（ReAct 循环）

- MemFactory
  - arXiv:2603.29493
  - Memory-RL-infra
  - 四层架构
    - Trainer Layer (GRPO 优化)
    - Environment Layer (MemoryBankEnv / LongcontextEnv)
    - Agent Layer (策略执行器)
    - Module Layer (Extractor / Updater / Retriever / Agent Module)

  - 原子记忆操作: extractor, update, retriever, agent module
  - 实验跑在单卡 A800, 似乎可以复线一下

- MemEvolve
  - arXiv:2512.18746
  - Guibin Zhang 等 (清华、OPPO)
  - 双层优化
    - 智能体在给定架构下优化行为
    - 基于反馈优化记忆架构

  - 四模块: Encode / Store / Retrieve / Manage

- Agentic Memory
  - arXiv:2601.01885
  - Yi Yu 等 (阿里巴巴、武汉大学)
  - 工具化记忆操作
    - LTM 工具: ADD / UPDATE / DELETE
    - STM 工具: RETRIEVE / SUMMARY / FILTER

  - 三阶段渐进式 RL 训练
    - LTM 学会记忆
    - STM 学会抗干扰
    - 统筹阶段

- Memory-R1
  - arXiv:2508.19828
  - Sikuan Yan 等 (LMU Munich, TUM, Cambridge)
  - 什么都没有开源

-