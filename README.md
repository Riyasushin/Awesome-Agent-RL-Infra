# Awesome Agent RL Infra [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

<p align="center">
  A curated list of awesome resources for <strong>Agent Reinforcement Learning Infrastructure</strong> — training frameworks, serving systems, evaluation platforms, and more. Feel free to fork this repo!
</p>

## Papers

### Current RL frameworks

Please refer to this [blog](https://huggingface.co/blog/async-rl-training-landscape) for detailed information.

| Library       | Organisation          | Repo                                   | GitHub ⭐ (Mar. '26) |
| ------------- | --------------------- | -------------------------------------- | -------------------- |
| AReaL         | inclusionAI/Ant Group | github.com/inclusionAI/AReaL           | 4,338                |
| ART           | CoreWeave             | github.com/OpenPipe/ART                | 8,952                |
| Atropos       | NousResearch          | github.com/NousResearch/atropos        | 878                  |
| MILES         | radixark              | github.com/radixark/miles              | 950                  |
| NeMo-RL       | NVIDIA                | github.com/NVIDIA-NeMo/RL              | 1,383                |
| OAT           | SAIL-SG               | github.com/sail-sg/oat                 | 637                  |
| open-instruct | AI2 (AllenAI)         | github.com/allenai/open-instruct       | 3,611                |
| PipelineRL    | ServiceNow            | github.com/ServiceNow/PipelineRL       | 374                  |
| PRIME-RL      | PrimeIntellect        | github.com/PrimeIntellect-ai/prime-rl  | 1,114                |
| ROLL          | Alibaba               | github.com/alibaba/ROLL                | 2,921                |
| SkyRL         | NovaSky-AI            | github.com/NovaSky-AI/SkyRL            | 1,664                |
| SLIME         | THUDM                 | github.com/THUDM/slime                 | 4,595                |
| TorchForge    | Meta                  | github.com/meta-pytorch/torchforge     | 632                  |
| Tunix         | Google                | github.com/google/tunix                | 2,175                |
| verl          | ByteDance             | github.com/verl-project/verl           | 19,673               |
| verifiers-rl  | PrimeIntellect        | github.com/PrimeIntellect-ai/verifiers | 3,876                |

这里保存我看的相关文章

# LLM RL Algorithm

- Adaptive Layerwise Perturbation: Unifying Off-Policy Corrections for LLM RL
  - off-policy 不稳定性
- DAPO， 比 GRPO更强？
- DGO
- Breaking the Capability Ceiling of LLM Post-Training by Reintroducing Markov States
  - 经典RL与 LLM RL 的比较
    有趣的训练场景
- Memory-R1
  - 通过强化学习增强大语言模型智能体的记忆管理与利用能力
- CodeScout
  - 关注的核心挑战：当智能体只有通用的终端工具（标准 Unix 终端）时，如何通过有效的强化学习配方训练出能够与使用专用工具的模型竞争甚至更优的代码定位智能体？
- ComputerRL
  - API-GUI Paradigm
- UI-R1
  - 首个将 DeepSeek-R1 风格的基于规则的强化学习（RL）应用于 GUI 动作预测任务的框架。引入一种新颖的基于规则的动作奖励函数，并仅使用 136 个高质量训练样本
- DART: Efficient Multi-turn RL for GUI Agents via Decoupled Training and Adaptive Data Curation
- MetaClaw
  - Fast Adaptation（秒级技能注入）+ Slow Adaptation（分钟级梯度RL）
- A Subgoal-driven Framework for Improving Long-Horizon LLM Agents
  - 网页导航任务
- 一系列的利用异步加速LLM RL 的工作
- Thinking with Videos
  - 这里更多是在做AI，RL只是一个小部分
    infra
- AReaL
  - 异步
- AgentRL
  - zhipu的框架
- ARL-Tangram: Unleash the Resource Efficiency in Agentic Reinforcement Learning
- Heddle
  - ？
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
  - 首次对真实世界 LLM 部署场景中的可验证奖励强化学习 (RLVR) 训练系统进行了全面的特征刻画研究
- RLAX
  - TPU上RL
- RollArt
  - 智能体 RL 工作负载高度异构：包含计算密集的 prefill 阶段、带宽受限的解码、以及带状态的 CPU 重环境模拟
- RollPacker
  - 针对LLM rollout阶段长尾响应分布引发的GPU利用率低下问题。通过“尾部批处理”（tail batching）调度，将长尾样本集中到专门的“长轮次”
- SimpleTIR
  - 多轮 TIR 中的训练不稳定性源于外部工具反馈引起的分布偏移，这导致了低概率 token，并在连续轮次中累积，引发灾难性的梯度范数爆炸
- SortedRL
  - 优化rollout时候的长尾

# infra for MARL

- FlexMARL
  - 首个端到端训练框架，对大规模基于 LLM 的多智能体强化学习（MARL）的 rollout、训练及其编排进行整体优化
- MARTI-MARS2

# Agent-aware Inference

- Continuum
  - toll-use aware scheduling
