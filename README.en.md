# Cloud GPU Cost Comparison — Free Tiers vs Per-Second Rentals (2026-11)

> **Verified 2026-11-22.** Prices and free-tier quotas change constantly — re-check each vendor's own page before you buy.

**Read it online (shareable)**: https://feng20100326.github.io/cloud-gpu-cost-compare/
**中文版**: [README.md](README.md) · **Cheat sheet**: [docs/gpu-cost-cheatsheet.md](docs/gpu-cost-cheatsheet.md)

---

## TL;DR

| If you need… | Use… | Because |
|---|---|---|
| to validate an idea, a notebook, a small experiment | **Colab / Kaggle free tier** | $0, but *"not guaranteed"* — see the quotes below |
| a job that must run to completion | **per-second rental (RunPod etc.)** | billed by the second, so an interruption costs cents |
| the lowest possible price and you can resume | **SaladCloud "Lowest" tier** | $0.015/hr — but it is *also the most interruptible tier* |
| 48–80 GB VRAM | compare at that tier | the real price spread lives here, not in the entry card |
| multi-vendor price comparison, on/off flexibility | **hourly marketplaces (e.g. Clore.ai)** | live supply pricing — but machines are third-party, so no vendor SLA |

---

## The official quotes (so you can check me)

**Google Colab — [FAQ](https://research.google.com/colaboratory/faq.html)**

> "Colab is a hosted Jupyter Notebook service that requires no setup to use and provides free of charge access to computing resources, including GPUs"

> "Colab resources are **not guaranteed and are not unlimited**, and usage limits sometimes fluctuate."

> "In the version of Colab that is free of charge, access to expensive resources like GPUs is **heavily restricted**."

**SaladCloud — [pricing](https://salad.com/pricing)**

> "SaladCloud Pricing — GPUs from **$0.015 per hour, billed per second**"

> "**Lowest is the lowest cost and the most interruptible**"

> "May be preempted by higher-priority groups. **Minimum run before reallocation is roughly 30 minutes.**"

**RunPod — [pricing](https://www.runpod.io/pricing)** (per-second billing, published rates as of 2026-11-22)

> RTX 4090 24 GB — **$0.89/hr** · L4 24 GB — **$0.69/hr** · A6000 48 GB — **$0.69/hr** · RTX 6000 Ada 48 GB — **$1.09/hr** · L40S 48 GB — $1.09/hr · H100 PCIe 80 GB — $2.89/hr (Secure)

**Clore.ai — [referral docs](https://docs.clore.ai/getting-started/deposit-withdrawal/referral-program.md)**

> `renter_referral = (renter_base_fee + renter_extra_fee) × commission_rate`

---

## Full comparison table

| Option | Cost | How capacity is supplied | Good for | Main catch |
|---|---|---|---|---|
| Colab free tier | $0 | Official free quota | Learning, notebooks, small experiments | *"not guaranteed / not unlimited"*; GPU access *"heavily restricted"*; can disconnect at any time |
| Kaggle free quota | $0 (quota hours: see the official page) | Official free quota | Notebooks, Kaggle-dataset experiments | Weekly quota and card type vary; interrupted runs restart |
| SaladCloud | **from $0.015/hr**, per-second billing | Distributed idle consumer GPUs | Batch inference, data processing, pipeline dry-runs | **Cheapest *and* most interruptible** — see the footnote below |
| RunPod (per-second) | RTX 4090 24G **$0.89/hr** · L4 24G **$0.69/hr** · A6000 48G **$0.69/hr** · RTX 6000 Ada 48G **$1.09/hr** · H100 PCIe 80G **$2.89/hr** | Hosted GPUs, per-second billing | Training, fine-tuning, jobs needing a stable machine | Storage/volumes billed separately; H100/A100 jump a bracket |
| Clore.ai (hourly marketplace) | floats with live supply; GPUs owned by third-party compute providers | Decentralised marketplace bidding | Price shopping, mid-size jobs, on/off flexibility | **Third-party machines → reliability varies. Load-test it yourself; it is not a vendor-grade SLA** |

### Footnote — read this before you quote $0.015

SaladCloud's `$0.015/hr` is the official **"Lowest" priority** starting price (RTX 3060 / 3070 / 3070 Ti class). The same official page states, in its own words:

- *"Lowest is the lowest cost and the most interruptible"*
- *"May be preempted by higher-priority groups. Minimum run before reallocation is roughly 30 minutes."*
- **Billed per second.**

Comparing `$0.015/hr` against a `$0.69+/hr` hosted card is comparing **the cheapest-and-most-likely-to-be-killed tier** with **a stable hosted machine**. If you run a long 4090-class job on the $0.015 tier, being preempted is expected behaviour. It suits batch work you can resume — not a job that must finish in one go.

All prices and quotas: captured **2026-11-22**, and they will change. Check the vendor page on the day you buy.

---

## How I decide

| Situation | What I do |
|---|---|
| Writing code, validating an idea | Run it on the free tier first; record the VRAM and wall-clock you actually need |
| Steady demand, must run for days | Switch to per-second billing; stop it when idle |
| Training / fine-tuning needing 48–80 GB | Compare at that VRAM tier — that is where the real spread is |
| Want multi-vendor comparison and easy on/off | Try an hourly marketplace; Clore.ai is one of them |

## The honest summary

There is no such thing as a *stable free* cloud GPU. Free quotas answer **"can I start?"**; metered per-second rentals answer **"can I finish on time?"**. Validate on the free tier, then run production on metered capacity. That is cheaper than an annual plan up front and safer than living on free quota throughout.

---

## Affiliate disclosure

The Clore.ai link below is my **affiliate link**. **I earn a commission only if you pay — not if you sign up.** The commission comes out of the platform fee Clore already charges on a paid marketplace purchase, and the base is that fee, *not* your total spend:

```
referral = (base_fee + extra_fee) × commission_rate
```

**My current rate is 15% of that fee.** This is not "15% of what you spend", and not "15% the moment you refer someone" — if the person you refer never pays for compute, the commission is **$0**. The payout threshold on my account is **$20** (shown in the dashboard as CLORE 10000 / BTC 0.0002 / USD 20), so small earnings accumulate before they can be withdrawn.

If you'd rather not use an affiliate link, just go to `clore.ai` directly. Every number above comes from the vendors' own published pages, with or without a referral code.

→ https://clore.ai/register?ref_id=1zyqnh0c&utm_source=github&utm_medium=repo&utm_campaign=cloud-gpu-cost-compare

---

## Sources

| Claim | Source |
|---|---|
| Colab free tier is free of charge but not guaranteed / not unlimited; GPUs heavily restricted | https://research.google.com/colaboratory/faq.html |
| Kaggle free GPU quota (hours: see the page) | https://www.kaggle.com/docs/efficient-gpu-usage |
| SaladCloud pricing, per-second billing, "Lowest" tier wording, preemption rules | https://salad.com/pricing |
| RunPod per-second hourly prices | https://www.runpod.io/pricing |
| Clore.ai commission formula, tier structure, payout thresholds | https://docs.clore.ai/getting-started/deposit-withdrawal/referral-program.md |

**Not verified:** Kaggle's exact weekly GPU-hour figure (the official docs page renders client-side and no citable number could be extracted), and live Clore.ai marketplace prices (they float with supply). Both are marked "see the official page" rather than filled with guessed numbers.

---

*This is a cost comparison, not investment advice, and it makes no earnings promise. Compute availability and pricing are not guaranteed by any vendor named here. All figures carry a capture date and a source link.*
