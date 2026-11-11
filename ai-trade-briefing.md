# The Paper That Started the AI Trade — Thematic Briefing

**Working title:** "The paper that started the AI trade"
**Purpose:** Factual spine verification for next week's research meeting; commentary to be added separately.
**Primary sources:** arXiv:1706.03762 ("Attention Is All You Need") and Yahoo Finance market data for NVDA.

---

## 1. Company Snapshot — NVIDIA Corporation (NVDA)

| Field | Value (as reported by data service) |
| --- | --- |
| Ticker / Exchange | NVDA, NasdaqGS (NMS) |
| Sector | Technology |
| Industry | Semiconductors |
| Market cap | 4195058188288 USD |
| Current price | 173.73 USD (regularMarketPrice) |
| Beta | 2.247 |
| Trailing P/E | 21.963337 |
| Forward P/E | 10.92035 |
| Dividend yield | 0.59% |
| Analyst opinions | 57 (recommendationKey: strong_buy; mean target price 319.98773) |
| Employees | 42000 (fullTimeEmployees) |
| HQ | Santa Clara, California, United States (incorporated 1993) |
| Business description (as reported) | NVIDIA Corporation operates as a data center scale AI infrastructure company... through Compute & Networking and Graphics segments. The Compute & Networking segment provides data center accelerated computing and networking platforms and artificial intelligence solutions and software, and automotive platforms and autonomous and electric vehicle solutions, including software. The Graphics segment offers GeForce GPUs for gaming and PCs; Quadro/NVIDIA RTX GPUs for enterprise workstation graphics. |

**Notable market data points:** enterprise value 4046640119808; total revenue (TTM) 302970011648; total cash 62469001216; total debt 38860001280; profit margins 0.63663; trailing annual dividend rate 0.28 with payout ratio 0.0354; 52-week range 164.27–243.37.

---

## 2. Institutional Ownership Table

| Metric (as reported) | Value |
| --- | --- |
| institutionsPercentHeld | 0.71384 (71.384% of shares held by institutions) |
| institutionsFloatPercentHeld | 0.74364 |
| institutionsCount | 7753 |
| insidersPercentHeld | 0.04006 |

**Top 3 institutional holders by reported share count** (Date Reported epoch: 1782777600000 unless noted):

| Holder (as reported by data service) | Shares | pctHeld | Reported Value (USD) | pctChange |
| --- | --- | --- | --- | --- |
| Blackrock Inc. | 1941918386 | 0.0806 | 337369472903 | 0.0085 |
| Vanguard Capital Management LLC | 1540816358 | 0.0639 | 267686019292 | 0.0015 |
| State Street Corporation | 1009783437 | 0.0419 | 175429672195 | 0.016 |

*Also reported just behind the top three: FMR, LLC (932807820 shares, reported 1790726400000), Geode Capital Management, LLC (613740577 shares), and Vanguard Portfolio Management LLC (517816949 shares).*

---

## 3. Paper Facts — "Attention Is All You Need" (arXiv:1706.03762)

**Headline machine-translation results (from the abstract):**
- **28.4 BLEU** on the WMT 2014 English-to-German translation task — improving over the existing best results, including ensembles, by over 2 BLEU.
- **41.8 BLEU** on the WMT 2014 English-to-French translation task — a new single-model state-of-the-art, achieved after training for 3.5 days on eight GPUs (a small fraction of the training costs of the best models from the literature).
- The abstract also notes the Transformer generalizes well, applying it successfully to English constituency parsing with both large and limited training data.

**Model architecture (per the paper's "Model Architecture" section):**
- **Encoder:** a stack of **N = 6 identical layers**, each with two sub-layers: (1) multi-head self-attention, and (2) a simple, position-wise fully connected feed-forward network. Residual connections around each sub-layer followed by layer normalization: LayerNorm(x + Sublayer(x)); all sub-layers and embedding layers produce outputs of dimension d_model = 512.
- **Decoder:** also a stack of **N = 6 identical layers**. In addition to the two encoder sub-layers, the decoder inserts a third sub-layer performing multi-head attention over the output of the encoder stack. Decoder self-attention is masked to prevent positions from attending to subsequent positions, preserving the auto-regressive property.

**Attention mechanism (as described in the paper):**
- **Scaled Dot-Product Attention:** The input consists of queries and keys of dimension d_k, and values of dimension d_v. Dot products of the query with all keys are computed, **divided by √d_k**, and a softmax is applied to obtain the weights on the values. Formally: Attention(Q, K, V) = softmax(QK^T / √d_k) V. The scaling by 1/√d_k counteracts large dot products that would push the softmax into regions with extremely small gradients (for components with mean 0 and variance 1, the dot product q·k has mean 0 and variance d_k).
- **Multi-Head Attention:** Instead of a single attention function with d_model-dimensional keys/values/queries, queries, keys and values are linearly projected h times with different learned linear projections to d_k, d_k and d_v dimensions; attention is performed in parallel on each projected version, and the outputs are concatenated and projected again with W^O. **The paper employs h = 8 parallel attention layers (heads)**, with d_k = d_v = d_model/h = 64. Due to the reduced dimension of each head, total computational cost is similar to single-head attention with full dimensionality. Multi-head attention is used in three ways: encoder-decoder attention layers, encoder self-attention layers, and masked decoder self-attention layers.
- Supporting detail: position-wise feed-forward network FFN(x) = max(0, xW_1 + b_1)W_2 + b_2, with input/output dimensionality d_model = 512 and inner-layer dimensionality d_ff = 2048. Since the model contains no recurrence or convolution, sinusoidal positional encodings (PE(pos,2i) = sin(pos/10000^(2i/d_model), PE(pos,2i+1) = cos(pos/10000^(2i/d_model)) are added to the input embeddings.

---

## 4. Sources

- Paper: **"Attention Is All You Need"**, arXiv identifier **1706.03762** — https://arxiv.org/abs/1706.03762 (abstract and Model Architecture section verified via arXiv LaTeX source).
- Company data: Yahoo Finance market data for **NVDA** (stock profile, institutional ownership, and institutional holder breakdowns as returned by the data service; figures reported exactly as returned, not rounded or converted).
