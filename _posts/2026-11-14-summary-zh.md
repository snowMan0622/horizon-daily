---
layout: default
title: "Horizon Summary: 2026-11-14 (ZH)"
date: 2026-11-14
lang: zh
---

> 从 138 条内容中筛选出 6 条重要资讯。

---

**科技新闻**
1. [llama.cpp 与 ggml 库版本升至 1.0.0，明确 API 兼容规则](#item-tech-news-1) ⭐️ 8.0/10
2. [TorchTitan 在 384 块 GH200 上训练 1T MoE](#item-tech-news-2) ⭐️ 8.0/10
3. [OpenAI 推出 ChatGPT Wallet，智能体凭支付令牌代购](#item-tech-news-3) ⭐️ 8.0/10
4. [研究发现 Granzyme K 驱动组织衰老而不引发全身炎症](#item-tech-news-4) ⭐️ 7.0/10
5. [SDR 与双 4090 实时监听全频段航空波段](#item-tech-news-5) ⭐️ 7.0/10
6. [World Labs 正式开放 Atlas 世界模型及开发者 API](#item-tech-news-6) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [llama.cpp 与 ggml 库版本升至 1.0.0，明确 API 兼容规则](https://www.ithome.com/1/027/019.htm) ⭐️ 8.0/10

开发者 Georgi Gerganov 于 11 月 13 日宣布，开源推理项目 llama.cpp 及其底层张量库 ggml 的库版本（libllama、libggml）进入 1.0.0。官方同时给出语义化版本规则：公共 C API 出现破坏性变更时升主版本号，向后兼容的功能、后端更新、模型支持或 API 新增升次版本号，不改变 API 的 bug 修复升补丁号。公告称 llama.cpp 已支持超过 150 种模型架构变体及主流推测解码方法，并计划借助英伟达、AMD、高通、Arm、IBM、英特尔提供的硬件扩大自托管测试覆盖。

rss · IT之家 · 11月14日 00:14

**「背景」** llama.cpp 是 Georgi Gerganov 发起的开源 C/C++ 大模型推理项目，底层依赖同属 ggml-org 的张量库 ggml，两者此前长期以未定义语义化版本规则的方式迭代。据 Hugging Face 官方博客，此次 1.0.0 是项目约三年半历史中首次正式承诺语义化版本，今后 API/ABI 不兼容将通过主版本号体现。

**「对开发者的影响」** 依赖 libllama 或 libggml 的应用今后可依据主版本号判断升级是否可能带来 API/ABI 不兼容，从而决定是否同步修改代码；次版本和补丁升级则预期保持向后兼容。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://huggingface.co/blog/ggml-org/llama-cpp-v1">llama . cpp v 1 . 0 . 0 : A stronger foundation for the local AI ecosystem</a></li>
<li><a href="https://ailookout.news/blog/llama-cpp-v1-0-0-semantic-versioning-local-ai/">llama . cpp v 1 . 0 . 0 API stability local AI | AiLookout.news</a></li>

</ul>
</details>

**标签**: `#llama.cpp`, `#local inference`, `#open source`, `#ggml`, `#LLM tooling`

---

<a id="item-tech-news-2"></a>
### [TorchTitan 在 384 块 GH200 上训练 1T MoE](https://www.reddit.com/r/MachineLearning/comments/1xvce5h/scaling_to_1t_moe_on_torchtitan_p/) ⭐️ 8.0/10

作者团队与 TorchTitan、PyTorch 维护者合作，在 JUPITER 超算的 GH200 上把约 1T 参数的 MoE 训练推到每 GPU 约 1,300 tokens/s，使用 384 块 GPU，相比起点提升 14 倍。方案采用 384 路 FSDP 加 4 路专家并行（EP 限制在节点内），放弃流水线并行以缩短迭代周期。文章还给出多项具体优化：全量激活检查点带来 4 倍提升，用 Muon 替代 Adam 以支持 64k token 序列，把 Newton-Schulz 放到 GPU 执行使优化器步从 42 秒降到约 2 秒、吞吐提升 35%。这些是实践者自述的工程结果，并非同行评审结论。

reddit · r/MachineLearning · /u/f14-bertolotti · 11月13日 16:28

**「背景」** TorchTitan 是 PyTorch 原生的开源分布式训练框架，旨在把 FSDP、张量并行、流水线并行、专家并行等大规模训练技术整合到同一套实现中，减少组合这些技术时的工程开销。该框架的论文与代码库将其定位为面向大语言模型预训练的模块化平台，而本次实践正是在这一框架上验证 GH200 集群的扩展上限。

**「对训练系统的影响」** 文中指出 JUPITER 的 InfiniBand 每 GPU 约 25 GB/s，比 NVLink 慢 6 倍，基线单步 84 秒中有 68 秒耗在网络上，因此优化重点放在减少跨节点通信：专家梯度改用 bf16 all-to-all 后在本地以 fp32 累加，FP8 专家 all-gather 带来 18% 提升，节点内重分片让反向重聚集走 NVLink。作者还报告一次 OOM 实为缓存分配器按 CUDA 流分池导致约 21 GiB 被占用，改用 FSDP2 的 unshard\_async\_op 后重试归零、峰值显存降 13.5 GiB、吞吐提升 21%。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://arxiv.org/abs/2410.06511">[2410.06511] TorchTitan : One-stop PyTorch native solution for...</a></li>
<li><a href="https://github.com/pytorch/torchtitan">GitHub - pytorch / torchtitan : A PyTorch native platform for training ...</a></li>
<li><a href="https://www.emergentmind.com/topics/torchtitan-training-framework">TorchTitan Training Framework</a></li>

</ul>
</details>

**标签**: `#mixture-of-experts`, `#distributed-training`, `#PyTorch`, `#GPU-systems`, `#model-scaling`

---

<a id="item-tech-news-3"></a>
### [OpenAI 推出 ChatGPT Wallet，智能体凭支付令牌代购](https://openai.com/index/introducing-chatgpt-wallet/) ⭐️ 8.0/10

OpenAI 发布 ChatGPT Wallet，让 dot 智能体代替用户购物，并与美国运通、万事达卡和 Visa 合作。用户录入一次银行卡信息后，智能体可代为寻找商品，但每笔交易都需用户核对商品与金额，并通过 Face ID 或指纹确认。支付网络为每笔交易生成限定用途的支付令牌，包含替代真实卡号的卡号、安全码和有效期，智能体不接触真实银行卡信息。该功能自 11 月 13 日起仅向美国 18 岁以上 ChatGPT Pro 订阅用户开放，且需使用美国发行的银行卡；OpenAI 称初期不收取交易佣金。

telegram · zaihuapd · 11月13日 15:43

**「背景」** OpenAI 表示，越来越多消费者开始用个人 AI 智能体管理日程、预订旅行和处理日常事务，ChatGPT Wallet 正是在这一趋势下推出。据 IT 之家报道，截至今年第三季度末，ChatGPT 每周活跃用户超过 12 亿，付费用户接近 1 亿。

**「影响」** 对符合条件的美国 Pro 用户而言，使用现有信用卡付款仍可保留原有积分奖励和权益保障，但需逐笔人工确认，尚不能实现完全自动下单。OpenAI 同时推出面向企业的工具和指南，包括如何检查网站是否误拦截 OpenAI 的智能体，商家需据此排查自身站点对智能体访问的兼容性。

**标签**: `#AI agents`, `#payments`, `#OpenAI`, `#security`, `#product launch`

---

<a id="item-tech-news-4"></a>
### [研究发现 Granzyme K 驱动组织衰老而不引发全身炎症](https://www.nature.com/articles/d41586-026-03638-3) ⭐️ 7.0/10

《自然》的一篇新闻稿报道了一项研究，该研究将 Granzyme K（GzmK）确定为一种组织特异性的机体衰老驱动因素，且不会引发全身性炎症。据评论者引用的《Immunity》论文摘要，GzmK 缺失显著减轻了器官衰老，尽管免疫衰老表型持续存在，从而“有效解耦了免疫衰老与组织衰老”；作者将 GzmK 描述为机体衰老的组织特异性驱动因素，而非免疫衰老或全身性炎症的驱动因素。这些发现来自小鼠实验，评论者指出该论文位于付费墙之后。

hackernews · gumby · 11月13日 19:25 · [社区讨论](https://news.ycombinator.com/item?id=50488470)

**「背景」** Granzyme K（GzmK）是一种由免疫细胞分泌的丝氨酸蛋白酶，通常表达水平较低，但在组织损伤和疾病状态下会升高。此前研究已在类风湿关节炎滑膜等炎症器官的 CD8+ T 细胞中发现其表达，但其具体功能长期不明确。此次研究的新意在于把 GzmK 与组织衰老直接联系起来，同时将其与免疫衰老和全身性炎症区分开。

**「影响与限制」** 该结果将组织衰老与全身性炎症区分开来，提示针对 GzmK 的干预可能旨在减缓器官衰老，而不必抑制全身免疫信号。由于证据来自小鼠，且论文受付费墙限制，在得出任何临床相关性结论之前，仍需独立验证。

**「社区讨论」** 评论者强调，论文摘要比新闻标题更为谨慎：GzmK 被描述为组织衰老的驱动因素，而非免疫衰老或全身性炎症的驱动因素。多位评论者还指出，该研究是在小鼠中进行的，并调侃“终于有不衰老的小鼠了”。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.frontiersin.org/journals/immunology/articles/10.3389/fimmu.2025.1620670/full">Frontiers | Pro-inflammatory granzyme K contributes extracellularly to...</a></li>
<li><a href="https://www.nature.com/articles/s41586-025-08713-9?error=cookies_not_supported&amp;code=db5a9b43-0514-42d3-8226-1b5ae67491ac">Granzyme K activates the entire complement cascade | Nature</a></li>

</ul>
</details>

**标签**: `#biomedical research`, `#aging`, `#immunology`, `#science communication`

---

<a id="item-tech-news-5"></a>
### [SDR 与双 4090 实时监听全频段航空波段](https://orcasairband.com/) ⭐️ 7.0/10

一个名为 orcasairband.com 的业余项目用 Ettus B210 软件定义无线电配合双 RTX 4090 显卡，对整段航空波段做 GPU 多相信道化、解调与发射检测，并实时输出未经编辑的 ATC 通话转录。项目作者在 Hacker News 评论中说明，当天温哥华地区发生地面停飞（ground stop），该系统意外派上用场，记录到维多利亚地面台 126.400 和温哥华区调 134.800 的相关通话。作者同时贴出了 2143Z、2151Z 等时间点的原始转录片段，其中部分信号较弱、内容不完整。

hackernews · mmaunder · 11月13日 22:04 · [社区讨论](https://news.ycombinator.com/item?id=50490593)

**「背景」** 该项目由作者自建，使用 Ettus B210 软件定义无线电接收机配合双 RTX 4090 显卡，通过 CUDA 编写的多相信道化器把整个航空波段切分为多个信道，再解调并检测发射信号。据社区评论，2026 年 11 月 13 日温哥华地区发生地面停飞（ground stop），作者称这次意外事件让该监听站显得格外有用，并公开了当时截取的原始通话转录。

**「实际影响」** 对关注 SDR 与信号处理的开发者而言，该项目展示了用消费级 GPU 对整段航空波段并行信道化的可行路径，而非只监听单个频率；但转录质量受信号强弱影响明显，作者贴出的片段中就有“弱信号”和无法辨识的内容，说明结果尚不能当作可靠记录使用。

**「社区讨论」** 有评论者指出，在链接发布当天的 14:03 左右，频道中有人询问温哥华方向是否有地面停飞，并得到“目前没有航班起飞前往温哥华降落”的确认回复。另有评论者表示许多通话听起来相当模糊，自己只能听懂约一半，并询问航空通信是否仍为模拟制式；还有人提到一个类似项目，通过公共 KiwiSDR 接收器解码船舶 DSC 信号并尝试多站定位。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.newsmax.com/us/faa-ground-stop-spreads-to-international-flights/2026/11/13/id/1276264/">FAA Ground Stop Spreads to International Flights | Newsmax.com</a></li>

</ul>
</details>

**标签**: `#software-defined-radio`, `#GPU-computing`, `#signal-processing`, `#air-traffic-control`, `#hobby-projects`

---

<a id="item-tech-news-6"></a>
### [World Labs 正式开放 Atlas 世界模型及开发者 API](https://www.ifanr.com/1689379?utm_source=rss&amp;utm_medium=rss&amp;utm_campaign=) ⭐️ 7.0/10

李飞飞创办的 World Labs 正式向公众开放其世界模型 Atlas，同步上线网页应用和开发者 API，新用户注册赠送 10000 积分。网页端提供四款工具：Viewfinder 从单张图片生成可延展场景，Chisel 用自然语言指挥智能体搭建 3D 白模，Relight 为 splat 场景重新打光，Splat to mesh 将点云转为带贴图的 GLB 网格。平台采用积分计费，例如 Viewfinder 渲染一帧 50 积分、Chisel 整组渲染 160 积分、生成完整 Splat 需 5000 积分；官方还提供 Blender 集成。上述能力来自媒体上手体验报道，并非独立性能评测。

rss · 爱范儿 · 11月13日 10:04

**「背景」** World Labs 由李飞飞联合创办，此前已推出 Marble 系列世界模型。据外部报道，Atlas 于 2026 年 9 月 1 日首次发布，被描述为从零预训练、原生处理文本、图像、视频和 3D 的多模态自回归扩散 Transformer 世界模型。此次是 Atlas 从发布走向面向公众开放网页应用与开发者 API 的节点。

**「对使用者的影响」** 对独立开发者和不熟悉三维建模的用户而言，Atlas 把从图片或文本到可分镜、可渲染、可导出到 Blender 或游戏引擎的流程整合成一条带明确计价的工具链，但导出的场景仍需自行处理交互规则、角色行为和资产检查。免费积分足以做简单体验，而视频生成和完整 Splat 等大额操作会快速消耗积分，使用前需评估成本。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://temperature2.com/p/2026-09-01-world-labs-atlas-world-model-launch/">Fei - Fei Li &#x27;s World Labs launches Atlas world model</a></li>
<li><a href="https://aicoder.com/news/world-labs-atlas-20260901">World Labs launches Atlas , an omni world model for... — AICoder</a></li>

</ul>
</details>

**标签**: `#世界模型`, `#3D生成`, `#World Labs`, `#生成式AI`, `#开发者API`

---