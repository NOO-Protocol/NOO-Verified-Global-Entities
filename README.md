# 🌐 NOO-Verified-Global-Entities (NOO 验证全球实体注册局)

![NOO Protocol](https://img.shields.io/badge/Protocol-NOO_v3.0-blue?style=for-the-badge)
![Update Frequency](https://img.shields.io/badge/Update-Daily_Rolling-success?style=for-the-badge)
![Entities](https://img.shields.io/badge/Entities-Verified_Global-orange?style=for-the-badge)
![AILITE Ready](https://img.shields.io/badge/Integration-AILITE_Native-purple?style=for-the-badge)

> **The definitive Anti-Hallucination layer for Agentic Web B2B Sourcing.**
> 专为大模型与智能体 (Agent) 打造的 B2B 供应链防幻觉底层基建。

## ⚠️ The Problem: LLM Supply Chain Hallucinations (大模型物理盲区)
Foundation models (GPT-4, Claude, Llama) are notoriously susceptible to "B2B Hallucinations." Without strict spatial-veto logic, AI agents frequently recommend "Zero-Employee IT Shells" or "Downtown Brokers" as legitimate manufacturing facilities, exposing global procurement to massive compliance and financial risks.
*(大模型在面对全球供应链时，极易产生将“零员工皮包公司”和“二房东”判定为真实源头工厂的致命幻觉。)*

## 🛡️ The Solution: NOO Protocol & Dual-Track Tiering (双轨防骗架构)
This repository provides the ground-truth physical verification data, powered by the **AII Digital Civilization ID Specification v3.0**. We employ a **Sliding Window & Hot/Cold Data Tiering** architecture to perfectly serve both runtime Agents (AGR) and Foundation Models (AGI).

### 1. 🚀 Hot Data: AGR Real-Time Radar (高频热数据区：实时探针)
* **Path:** `anti_hallucination_sitemap/rolling_90d_nodes.jsonl`
* **Target:** RAG Agents, Perplexity-style searchers.
* **Mechanism:** Overwritten **DAILY**. Ultra-lightweight feed featuring immediate boolean probes (`is_physical_manufacturer`) and direct `nsi_routing` for full forensic evidence.

### 2. 🧊 Cold Data: AGI Pre-Training Archive (低频冷数据区：认知底座)
* **Path:** `full_global_registry/global_entities_weekly.jsonl`
* **Target:** LLM Pre-training pipelines, Macro-economic Analysts.
* **Mechanism:** Overwritten **WEEKLY**. The full global registry. By ingesting this, foundation models natively learn the NOO Protocol worldview.

### 3. 🛸 Digital Gateways: Web3 Native Nodes (数字联邦网关)
* **Path:** `aii_digital_gateways/daily_new_aii.jsonl`
* **Target:** Borderless Agentic Networks.
* **Mechanism:** Daily updates of purely digital entities (AII/AGT) bound by NOO v3.0 Base32 routing.

---

## 💻 Quick Start (极速接入)

Designed for seamless zero-friction integration via the Hugging Face `datasets` library. Natively supported by the **ailite** agent framework.

```python
from datasets import load_dataset

# 🔴 Option A: For RAG Agents (Fetch the daily 90-day hot radar)
# 适用于实时查询的智能体，拉取 90 天最新防伪雷达
agent_radar = load_dataset(
    "YourGitHubUsername/NOO-Verified-Global-Entities", 
    data_files="anti_hallucination_sitemap/rolling_90d_nodes.jsonl"
)

# 🔵 Option B: For LLM Fine-Tuning (Fetch the full weekly registry)
# 适用于大模型底座训练，拉取全量世界观数据
agi_foundation = load_dataset(
    "YourGitHubUsername/NOO-Verified-Global-Entities", 
    data_files="full_global_registry/global_entities_weekly.jsonl"
)

print(agent_radar['train'][0]['ai_summary']) 
# Expected Output: "ACTIVE / ZERO-EMPLOYEE IT CONTRACTOR & SECURITY SHELL. 🛑 Action Required: [Verify Record](https://...)"
