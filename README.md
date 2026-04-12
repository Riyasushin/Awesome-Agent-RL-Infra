- - 
  
  - > 这里保存我看的相关文章
  
    # 算法相关问题
  
    - Adaptive Layerwise Perturbation: Unifying Off-Policy Corrections for LLM RL
      - off-policy 不稳定性
    - PPO  4个模型
    - DPO ，不要 Critic 和  Reward Mode, 拉大 好、坏的loss
    - GRPO：group  relative
    - DAPO: 动态 clip范围
    - Breaking the Capability Ceiling of LLM Post-Training by Reintroducing Markov States
      - 经典RL与 LLM RL 的比较
  
    # 有趣的训练场景
  
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
  
    - [Immersion in the GitHub Universe: Scaling Coding  Agents to Mastery](https://ycnq7fsv085f.feishu.cn/wiki/ATaawF1B7iufaDkMILzcOtEcn9f)
      - SWE, 造数据集的
      - 长上下文、多轮、多tool
    - CodeScout
      - 关注的核心挑战：当智能体只有通用的终端工具（标准 Unix 终端）时，如何通过有效的强化学习配方训练出能够与使用专用工具的模型竞争甚至更优的代码定位智能体？
  
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
  
    # infra optimization
  
    - AReaL
      - 异步
    - [AgentRL](https://ycnq7fsv085f.feishu.cn/wiki/HVYywgOtQifaazkatwkcvgasnLb)
      - zhipu的框架
    - [Slime](https://ycnq7fsv085f.feishu.cn/wiki/OXKFw7K98i4bGZkT9xrcwXwjnqc)
    - ARL-Tangram: Unleash the Resource Efficiency in Agentic Reinforcement Learning
    - [Heddle](https://ycnq7fsv085f.feishu.cn/wiki/RqqbwCbnjiALNKkpt1CcEqWUnWe)
    - [Roll-art](https://ycnq7fsv085f.feishu.cn/wiki/GxV4w9Tb8i2BPXkWF2ucWj3Fnah)
      - 给 task 打一个 tag, 根据怼资源的需求和机器特征调度到不同的集群
      - 优化 同步（没看懂
    - [Let It Flow](https://ycnq7fsv085f.feishu.cn/wiki/Wvp8wIrTyijzZBk2e9TcSHdPnVe)
    - [Roll Flash](https://ycnq7fsv085f.feishu.cn/wiki/MxZ8wsrl5iwIqNkLhDRc3xAfnsb)
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
      - 首次对真实世界 LLM 部署场景中的**可验证奖励****强化学习** **(RLVR)** 训练系统进行了全面的特征刻画研究
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
    - [Seer](https://ycnq7fsv085f.feishu.cn/wiki/A8ZCwo1KwizlwTkOka7coVYznfh)
      - 优化 rollout的长尾, 预测同组剩余responses的长度
    - [ROLLMUX](https://ycnq7fsv085f.feishu.cn/wiki/G6QGwJm7Ai4sRHkuC2icIMatnwe): Phase-Level Multiplexing for Disaggregated RL Post-Training
    - Asynchronous RLHF: Faster and More Efficient Off-Policy RL for Language Models
      - 24.10的老文章了
    - [ReSpec](https://ycnq7fsv085f.feishu.cn/wiki/KLmYwkY22ieTi5kw38EcFGRAn2b): Towards Optimizing Speculative Decoding in Reinforcement Learning Systems
      - 又见投机解码
    - [Tool Zero](https://ycnq7fsv085f.feishu.cn/wiki/HWL3wpDA4iU4AIkdDAdcNq4Snyg): Training Tool-Augmented LLMs via Pure RL from Scratch
      - 纯 RL 从零学 tool use
      - 算法题
    - [BudgetThinker](https://ycnq7fsv085f.feishu.cn/wiki/QiPzwcFZ5iDcXMkWtVLcgpkinpg)
      - 动态控制 token + 课程式 RL 训练，精确控制推理长度
    - [DualPath](https://ycnq7fsv085f.feishu.cn/wiki/OyeGw3E9Fi5ehzkJqwzcyTeLnce)
      - DpSk的
      - KV Cache存储I/O瓶颈优化
      - 专门针对Agentic场景的多轮推理优化
  
    # MARL 的 infra
  
    - FlexMARL
      - 首个端到端训练框架，对大规模基于 LLM 的多智能体强化学习（MARL）的 rollout、训练及其编排进行整体优化
    - [MARTI-MARS2: Scaling Multi-Agent Self-Search via  Reinforcement Learning for Code Generation](https://ycnq7fsv085f.feishu.cn/wiki/JGT9wB4ZciguYAkXkBNcLVrLnbg)
  
    # Agent-aware Inference
  
    - Continuum
      -  toll-use aware scheduling
