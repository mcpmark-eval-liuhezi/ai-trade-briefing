# The Paper That Started the AI Trade — Thematic Briefing (Draft)

**Working title:** "The paper that started the AI trade"
**Purpose:** Factual spine for research meeting next week. All company figures below are reported exactly as returned by the Yahoo Finance data service (no rounding or conversion). Paper facts are verified against the paper's own abstract and body (arXiv:1706.03762).

---

## 1. Company Snapshot — NVIDIA (NVDA)

| Field | Value (as reported by data service) |
| --- | --- |
| Ticker / Exchange | NVDA, NasdaqGS (NMS) |
| Sector | Technology |
| Industry | Semiconductors |
| Market cap | 4195058188288 USD (nonDilutedMarketCap: 4078186830000) |
| Shares outstanding | 24147000000 |
| Float shares | 23133590000 |
| InsidersPercentHeld | 0.04006 (4.006%) |
| InstitutionsPercentHeld | 0.71384 (71.384%) |
| InstitutionsFloatPercentHeld | 0.74364 (74.364%) |
| Institutions count | 7753 |
| Current price | 173.73 USD (previousClose 168.796; day range 170.77 – 177.54) |
| 52-week range | 164.27 – 243.37 (all-time high 243.37) |
| Trailing PE / Forward PE | 21.963337 / 10.92035 |
| Profit margins | 0.63663 |
| Revenue growth (YoY) | 1.059 |
| Earnings quarterly growth | 1.259 |
| Analyst consensus | strong_buy (recommendationMean 1.32258, 57 opinions; targetMeanPrice 319.98773, targetMedianPrice 315.0, targetHighPrice 515.0) |
| Employees | 42000 (full-time) |
| CEO | Jen-Hsun Huang (Co-Founder, CEO & Director); CFO: Colette M. Kress |
| HQ | Santa Clara, California (incorporated 1993) |
| Business description | Operates as a data center scale AI infrastructure company through Compute & Networking and Graphics segments; Compute & Networking provides data center accelerated computing, networking platforms and AI solutions/software; Graphics offers GeForce GPUs and Quadro/NVIDIA RTX enterprise workstation graphics. |

---

## 2. Institutional Ownership Table (Top 3 Holders by Reported Share Count)

Institutional ownership as reported by the data service: **heldPercentInstitutions = 0.71384 (71.384%)** of shares outstanding; institutionsFloatPercentHeld = 0.74364 (74.364%) of float; **institutionsCount = 7753**; heldPercentInsiders = 0.04006.

All three entries below share the same Date Reported (1782777600000, i.e. 2026-06-29).

| # | Holder (as reported) | Shares (reported) | pctHeld (as reported) | Reported value (as reported) | pctChange (as reported) |
| --- | --- | --- | --- | --- | --- |
| 1 | Blackrock Inc. | 1941918386 | 0.0806 | 337369472903 | 0.0085 |
| 2 | Vanguard Capital Management LLC | 1540816358 | 0.0639 | 267686019292 | 0.0015 |
| 3 | State Street Corporation | 1009783437 | 0.0419 | 175429672195 | 0.016 |

---

## 3. Paper Facts — "Attention Is All You Need" (arXiv:1706.03762)

**Headline machine-translation results (stated in the abstract):**
- **28.4 BLEU** on the **WMT 2014 English-to-German** translation task, improving over the existing best results (including ensembles) by over 2 BLEU.
- **41.8 BLEU** on the **WMT 2014 English-to-French** translation task — a new single-model state-of-the-art, achieved after training for 3.5 days on eight GPUs, a small fraction of the training costs of the best models from the literature.
- The paper also reports that the Transformer generalizes well to other tasks, applied successfully to English constituency parsing both with large and limited training data.

**Base model stack depth:**
- The encoder is a stack of **N = 6 identical layers** (each with two sub-layers: multi-head self-attention and a position-wise fully connected feed-forward network).
- The decoder is also a stack of **N = 6 identical layers** (with a third sub-layer performing multi-head attention over the output of the encoder stack).
- Residual connections around each sub-layer followed by layer normalization: LayerNorm(x + Sublayer(x)); all sub-layers and embedding layers produce outputs of dimension d_model = 512.

**Scaled dot-product attention (the paper's own formulation):**
- Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V.
- Queries and keys have dimension d_k; values have dimension d_v.
- **How the dot products are scaled:** the dot products of the query with all keys are **divided by sqrt(d_k)** (scaling factor 1/sqrt(d_k)). The paper's rationale: for large d_k, dot products grow large in magnitude, pushing the softmax into regions where it has extremely small gradients (if the components of q and k are independent random variables with mean 0 and variance 1, their dot product has mean 0 and variance d_k); scaling counteracts this effect.

**Multi-head attention (how it works, and head count):**
- Instead of a single attention function with d_model-dimensional keys/values/queries, the queries, keys and values are **linearly projected h times with different, learned linear projections** to d_k, d_k and d_v dimensions; attention is performed in parallel on each projected version, yielding d_v-dimensional outputs that are concatenated and once again projected: MultiHead(Q, K, V) = Concat(head_1, ..., head_h)W^O.
- This allows the model to jointly attend to information from different representation subspaces at different positions.
- **Number of parallel heads in the base model: h = 8** parallel attention layers (heads); for each, d_k = d_v = d_model/h = 64. Due to the reduced dimension of each head, total computational cost is similar to that of single-head attention with full dimensionality.
- Multi-head attention is used in three ways: encoder-decoder attention layers (queries from the previous decoder layer, keys/values from the encoder output); encoder self-attention layers (keys, values and queries all from the previous encoder layer); and decoder self-attention layers (masked to prevent leftward information flow and preserve the auto-regressive property).

---

## 4. Sources

- Paper: "Attention Is All You Need", arXiv:1706.03762 — abstract and Section 3 "Model Architecture" (Encoder and Decoder Stacks; Scaled Dot-Product Attention; Multi-Head Attention) verified directly from the paper source.
- Company / institutional ownership data: Yahoo Finance data service (stock info, institutional holders, major holders) for ticker NVDA.
- This briefing is a draft for internal circulation; commentary to be added by the research team before the meeting.

---

## 5. Knowledge base records

The verified facts above have been recorded in the team knowledge graph (canonical entity names). The following entities and relations were created:

**Entities (6):**

| Entity name | Type | Key observations recorded |
| --- | --- | --- |
| NVIDIA | Company | Sector Technology / Industry Semiconductors; market cap 4195058188288 USD; institutionsPercentHeld 0.71384 (71.384%), institutionsFloatPercentHeld 0.74364 (74.364%), institutionsCount 7753, heldPercentInsiders 0.04006; top institutional holders Blackrock Inc. 1941918386 shares, Vanguard Capital Management LLC 1540816358 shares, State Street Corporation 1009783437 shares (all Date Reported 1782777600000); 42000 employees; CEO Jen-Hsun Huang; 52-week range 164.27 – 243.37; analyst consensus strong_buy (recommendationMean 1.32258, 57 opinions). |
| Attention Is All You Need | Paper | arXiv 1706.03762; 28.4 BLEU on WMT 2014 English-to-German (over 2 BLEU better than existing best including ensembles); 41.8 BLEU single-model state-of-the-art on WMT 2014 English-to-French after 3.5 days on eight GPUs; generalizes to English constituency parsing. |
| Transformer | Architecture | N=6 identical encoder layers and N=6 identical decoder layers; scaled dot-product attention Attention(Q,K,V) = softmax(QK^T / sqrt(d_k))V with dot products divided by sqrt(d_k); multi-head attention with h=8 parallel heads (d_k = d_v = d_model/h = 64); FFN inner dimension d_ff = 2048; sinusoidal positional encodings. |
| Blackrock Inc. | Institutional Holder | Top institutional holder of NVIDIA (ranked #1 by reported share count); reported share count 1941918386 shares (Date Reported 1782777600000); pctHeld 0.0806; reported value 337369472903; pctChange 0.0085. |
| Vanguard Capital Management LLC | Institutional Holder | Top institutional holder of NVIDIA (ranked #2 by reported share count); reported share count 1540816358 shares (Date Reported 1782777600000); pctHeld 0.0639; reported value 267686019292; pctChange 0.0015. |
| State Street Corporation | Institutional Holder | Top institutional holder of NVIDIA (ranked #3 by reported share count); reported share count 1009783437 shares (Date Reported 1782777600000); pctHeld 0.0419; reported value 175429672195; pctChange 0.016. |

**Relations (5), with exact labels:**

| From | Relation type | To |
| --- | --- | --- |
| Blackrock Inc. | is a top institutional holder of | NVIDIA |
| Vanguard Capital Management LLC | is a top institutional holder of | NVIDIA |
| State Street Corporation | is a top institutional holder of | NVIDIA |
| Attention Is All You Need | introduces | Transformer |
| Transformer | underpins | NVIDIA (data-center AI business) |

These records were read back from the knowledge graph after writing and match the source data exactly. The graph is now ready for team members to extend with commentary entities linking to NVIDIA, "Attention Is All You Need", and the Transformer.
