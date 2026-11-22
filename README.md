# 云GPU到底要不要花钱？免费额度 vs 按秒租赁实测对比（2026-11）

> 数据抓取时点：**2026-11-22**。价格与额度会变，下单前请以各平台官方页面当日显示为准。

**在线阅读版（可直接分享）**：https://feng20100326.github.io/cloud-gpu-cost-compare/
**English version**: [README.en.md](README.en.md) · **速查表**: [docs/gpu-cost-cheatsheet.md](docs/gpu-cost-cheatsheet.md)

---

## 先说结论

1. **学习/实验阶段**，先把免费额度用满——不是为了省钱，是为了搞清楚自己到底需要多大显存、跑多久。
2. **免费额度的真实代价不是钱，是"不确定性"**。Google 官方 FAQ 原话：Colab 资源 *"not guaranteed and not unlimited, and usage limits sometimes fluctuate"*，免费版对 GPU 这类昂贵资源的访问 *"heavily restricted"*。翻译成人话：可能随时断、会排队、可能干脆不给你。
3. **要"能预测成本、能连续跑几天"的活**，按秒计费的按时租赁反而更划算——4090 这种消费级卡按小时也就 1 美元上下，断了不心疼。
4. **真正省钱的地方往往不在单价，在"选对卡"**。训练要大显存，推理和批量跑数据用 24G 级就够。

---

## 对比表

| 方案 | 大致成本 | 供给方式 | 适合什么 | 主要坑 |
|---|---|---|---|---|
| Colab 免费版 | 0 元 | 官方免费额度 | 学习、跑 notebook、小实验 | 官方原话 *"not guaranteed / not unlimited"*；GPU 访问 *"heavily restricted"*；随时可能断连 |
| Kaggle 免费额度 | 0 元（额度小时数以官方页面为准） | 官方免费额度 | notebook 实验、Kaggle 数据集 | 周额度与机型不固定，断了要重跑 |
| SaladCloud | **$0.015/小时起**，按秒计费 | 分布式闲置消费级 GPU | 批量推理、数据处理、跑通流程 | **见下方脚注——$0.015 那一档是"最便宜也最容易被中断"** |
| RunPod（按秒计费） | RTX 4090 24G **$0.89/hr** · L4 24G **$0.69/hr** · A6000 48G **$0.69/hr** · RTX 6000 Ada 48G **$1.09/hr** · H100 PCIe 80G **$2.89/hr**（Secure） | 托管 GPU，按秒计费 | 训练、微调、需要稳定机器的任务 | 存储/磁盘另计；H100/A100 这类高端卡单价跳一档 |
| Clore.ai（按小时撮合市场） | 随实时供给浮动，GPU 来自第三方算力所有者 | 分布式市场竞价 | 比价、中等规模任务、想随时开关 | **供给来自第三方机器，可靠性参差——必须自己压测验证，别当云厂商 SLA 用** |

### 脚注（引用 $0.015 之前必读）

SaladCloud 的 `$0.015/小时` 是官方 **"Lowest" 优先级**的起价（RTX 3060 / 3070 / 3070 Ti 级）。官方同一页写明：

- *"Lowest is the lowest cost and the most interruptible"* —— 这句是官方对这一档的自我描述。
- *"May be preempted by higher-priority groups. Minimum run before reallocation is roughly 30 minutes."*
- **按秒计费。**

所以：拿 `$0.015/hr` 去对比 `$0.69+/hr` 的托管机器，是拿"最便宜但最容易被踢"的档，对比"稳定的托管机"。如果你在 $0.015 档上跑一整段 4090 级别的长任务，**被抢占是预期内的事**——它适合能断点续跑的分批任务，不适合必须一口气跑完的活。

以上价格与额度均为 2026-11-22 抓取时点，会变化，购买前请看官方页面。

---

## 怎么选（我的实际做法）

| 场景 | 做法 |
|---|---|
| 只写代码、验证想法 | 先用免费额度跑通，把显存和时长需求记录下来 |
| 需求稳定、要连续跑几天 | 换按秒计费的按时租赁，用完就停，成本可控 |
| 训练/微调需要 48G–80G | 到这一档再比价，差价主要在这里 |
| 想省事又要多供应商比价、随时开关 | 试按小时撮合的市场型平台，Clore.ai 是其中一种 |

---

## 一句实话

云 GPU 没有"免费的稳定"这一说。免费额度回答的是**"我能不能开始"**，按秒付费回答的是**"我能不能按时跑完"**。先用免费额度把需求跑通，再用按时付费把生产跑稳——这比一上来包年包月省钱，也比全程蹭免费额度省钱。

---

## 披露（Affiliate Disclosure）

下面这个 Clore.ai 链接是我的 **affiliate（推广）链接**：**你付费我才有佣金，注册不给佣金。** 佣金来自 Clore 对买家付费订单已经收取的平台手续费，计提基数是那笔手续费，**不是你的总花费**：

```
referral = (base_fee + extra_fee) × commission_rate
```

**我的当前比例是这笔手续费的 15%。** 这既不是"你花费的 15%"，也不是"推荐一个人就立刻拿 15%"——被推荐的人如果没有付费买算力，佣金是 **$0**。提现门槛按高的算：官方文档公布的基础最低提现额是 $1 / 50 CLORE / 0.00005 BTC，但我这个账号的后台 Referral 页显示实际门槛为 **$20**（CLORE 10000 / BTC 0.0002 / USD 20，2026-11-22 读取），小额收益需累积到门槛才能提。

不想走推荐链接也没关系，直接去 `clore.ai` 就行——上面所有数字都来自各厂商自己发布的页面，有没有推荐码不影响判断。

→ https://clore.ai/register?ref_id=1zyqnh0c&utm_source=github&utm_medium=repo&utm_campaign=cloud-gpu-cost-compare

---

## 来源

| 结论 | 来源 |
|---|---|
| Colab 免费版"不保证、不限量、GPU 访问被严格限制" | https://research.google.com/colaboratory/faq.html |
| Kaggle 免费 GPU 额度（具体小时数见官方页） | https://www.kaggle.com/docs/efficient-gpu-usage |
| SaladCloud 定价、按秒计费、Lowest 档说明、抢占规则 | https://salad.com/pricing |
| RunPod 按秒计费的时价（4090 / L4 / A6000 / RTX 6000 Ada / H100 PCIe） | https://www.runpod.io/pricing |
| Clore.ai 佣金公式、档位结构（标准15% / Premium 20% / VIP 30%） | https://docs.clore.ai/getting-started/deposit-withdrawal/referral-program.md |
| Clore.ai 我这个账号的实际提现门槛（$20 / CLORE 10000 / BTC 0.0002） | 我的账户后台 Referral 页面显示（2026-11-22），非官方文档公开值 |

**未核实项**：Kaggle 每周 GPU 小时的确切数字（官方文档页为客户端渲染，未能取到可引用数值）、Clore.ai 市场实时租赁价（随供给浮动）。两者都写"见官方页面"，不填猜测数字。

---

*本文是成本对比，不是投资建议，也不构成任何收益承诺。文中各平台的算力可用性与价格均不作保证；所有数字均标注抓取日期并附官方来源。*
