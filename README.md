# Project of Data Visualization (COM-480)

| Student's name | SCIPER |
| -------------- | ------ |
| Haodong Zheng  | 387661 |
| Youliang Zhu   | 415773 |
| Yueyang Pan    | 350575 |

[Milestone 1](#milestone-1) • [Milestone 2](#milestone-2) • [Milestone 3](#milestone-3)

---

## Milestone 1 (20th March, 5pm)

### Dataset

We construct a unified dataset of **~200 companies** across the full AI value chain, spanning US, China, Europe, and Taiwan/Japan, organized into five layers (~40 each):

- **Layer 0 — Physical Infrastructure:** Power & thermal (Vertiv, Eaton), interconnects (Amphenol, Lumentum, Fabrinet), memory & storage (Micron, SK Hynix), PCB (TTM Technologies).
- **Layer 1 — Compute & Silicon:** AI accelerators and ASICs (NVIDIA, AMD, Broadcom, Marvell, Cerebras, Groq).
- **Layer 2 — AI Infrastructure Software:** Cloud, MLOps, data platforms (CoreWeave, Databricks, Scale AI).
- **Layer 3 — Foundation Models & Middleware:** LLMs, agents, orchestration (OpenAI, Anthropic, DeepSeek, Mistral).
- **Layer 4 — AI-Enabled Applications:** E-commerce, companionship, vertical SaaS, robotics (Perplexity, Waymo, Klarna).

**Data sources:** Public companies (Layers 0–2) use **SEC EDGAR** (free XBRL API), **yfinance**, and **Financial Modeling Prep** for fundamentals, valuation metrics, and customer revenue breakdowns. Private companies (Layers 2–4) use **Crunchbase** (academic API), **Dealroom.co** (EU), and **ITJuzi** (China). Customer concentration is extracted from 10-K filings and investor press releases.

**Data quality & preprocessing:** Public SEC data is audited and standardized — low preprocessing burden. Private data faces three challenges: (1) *valuation opacity* — undisclosed valuations flagged with confidence levels; (2) *temporal misalignment* — funding data normalized to March 2026 cutoff; (3) *source fragmentation* — deduplication across Crunchbase, Dealroom, and ITJuzi required. Additional steps: USD normalization at funding date, headquarters geocoding, and XBRL parsing for customer segments. We include 10–15 failed/pivoted companies (e.g., Stability AI, 01.AI) to mitigate survivor bias. Schema: shared universal fields (name, layer, region, founding year, status, revenue) extended by layer-specific fields (EV/EBITDA for L0; burn multiple for L3; ARR for L4). Stored as JSON and CSV; no scraping required.

---

### Problematic

Global AI capex exceeded $300B in 2025, yet the investment landscape remains opaque: hyperscaler spending floods infrastructure suppliers, VC billions concentrate in a handful of model-layer startups, and AI-enabled applications receive massive coverage despite generating real revenue. Job seekers targeting high-growth roles face the same gap — which companies are scaling, which are burning cash toward irrelevance?

**Central question:** *Across the full AI value chain — from power infrastructure to consumer applications — where are the most compelling investment and career opportunities, and how do they differ by layers, geography and market access?*

We build an **interactive investor-facing dashboard** organized around two market types (primary/secondary) and five value chain layers, addressing four axes:

1. **Capital flow by layer** — Where does AI capex land? Which layers are overcrowded or underinvested relative to the opportunity?
2. **Layer-appropriate valuation** — Infrastructure trades on EV/EBITDA; model-layer startups on revenue multiples; applications on ARR growth. The dashboard applies the right lens per layer.
3. **Customer concentration risk** — A per-company "customer mesh" (donut chart) reveals whether revenues are hyperscaler-dependent or diversified — a critical but undervisualized investment signal.
4. **Capital efficiency & IPO pipeline** — Which private companies generate the most value per dollar raised, and which are approaching IPO readiness?

**Target audience:** Emerging fund managers and angel investors seeking structured cross-layer deal flow; high-skill job seekers evaluating growth and stability. Design follows Shneiderman's mantra: *overview first, zoom and filter, then details-on-demand*.

---

### Exploratory Data Analysis

Initial EDA on 36 Layer 3–4 companies plus 20 representative Layer 0–2 public names reveals cross-layer and cross-regional structural patterns:

**Regional capital concentration is extreme.** The US accounts for 87% of Layer 3–4 valuation ($1,193B) and 84% of funding ($109.7B), driven by three mega-caps (OpenAI $500B, Anthropic $380B, xAI $200B). Excluding these, the US average falls from $74.6B to $16.9B — far closer to China ($3.6B) and Europe ($4.2B).

**Value chain distributions differ by region.** China is 70% Foundation Models ("Hundred Model War"). The US uniquely dominates Layers 0–2. Europe focuses on Developer Tools (Lovable) and open-source models (Mistral).

**Capital pools by layer.** Layer 0–1 public companies dominate market cap; Layer 3 absorbs most VC dollars; Layer 4 is most fragmented (median funding <$500M, multiples varying 20×).

**Valuation metric divergence.** Layer 0 hardware trades at 30–50× forward earnings; Layer 3 startups at 15–100× ARR. A single metric would misrank companies across layers, validating the layer-aware scorecard.

**Customer concentration risk at Layers 0–1.** Fabrinet derives ~40% of revenue from one customer; Lumentum is weighted to two hyperscalers; Credo discloses Microsoft as dominant buyer. This motivates the customer mesh — a per-company revenue donut by buyer type (hyperscaler, telco, enterprise, diversified).

**Capital efficiency by region.** DeepSeek (CN) 20.0×; Lovable (EU) 17.4×; OpenAI (US) 12.5×; Mistral (EU) 4.7×; SenseTime (CN) 1.1×. Chinese and European startups achieve comparable outcomes with 5–20× less capital.

**Cohort analysis.** 2022–2023 is the modal founding year (ChatGPT catalyst). Post-2024 startups skew toward Layer 4. Companies founded 2019–2021 with $100M+ ARR are entering the IPO window.

**Open-source divergence.** China and Europe release open-weight models far more than US peers — a moat and trust-signaling difference that enriches each company's investment thesis card.

---

### Related work

**What others have done:**
Bloomberg and PitchBook provide institutional investment data but are paywalled, lack AI-specific cross-layer framing and growth model analysis. CB Insights' *State of AI* and Goldman Sachs' *AI Capex* notes offer strong macro analysis but as static PDFs — no filtering or company-level drill-down. SemiAnalysis delivers rigorous layer-by-layer infrastructure breakdowns in long-form text only. Matt Turck's *MAD Landscape* (FirstMark) maps the AI ecosystem visually but is a static infographic with no investment metrics. Lightspeed Venture Partners' sector maps cover AI applications but exclude hardware and infrastructure. Dealroom.co offers interactive European startup data but no cross-regional or cross-layer comparison. No existing tool unifies all five layers with investment-grade metrics in a single interactive interface.

**Why our approach is original:**
Existing tools either have the data but not the narrative (Bloomberg, PitchBook), or the narrative but not interactivity (CB Insights, Goldman). We sit at the intersection: an *analytical story delivered through interactive visualization*, covering the full stack from atoms to applications. The customer mesh — per-company revenue concentration by buyer type — has no direct precedent in public investment tools. The layer-aware metric system (EV/EBITDA at L0, ARR multiples at L3) is also novel in a unified interface.

**Visualization inspirations:**
Gapminder (animated bubble charts); The Pudding (narrative data essays); *Wealth Inequality in America* (Politizane) for visceral concentration storytelling — directly applicable to the customer mesh; D3 Zoomable Treemap (Bostock) for Layer → Region → Company hierarchy; Financial Times' *Visual Vocabulary* for metric-to-chart discipline.

This dataset has not been explored in any prior coursework.

---

## Milestone 2 (2nd May, 5pm)

**10% of the final grade**

## Milestone 3 (30th May, 5pm)

**80% of the final grade**
