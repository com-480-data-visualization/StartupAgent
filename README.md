# Project of Data Visualization (COM-480)

| Student's name | SCIPER |
| -------------- | ------ |
| Haodong Zheng  | 387661 |
| Youliang Zhu   | 416773 |
|                |        |

[Milestone 1](#milestone-1) • [Milestone 2](#milestone-2) • [Milestone 3](#milestone-3)

## Milestone 1 (20th March, 5pm)

### Dataset

We construct a unified dataset of **100+ AI startups** across the United States, China, and Europe by triangulating multiple public sources: [Crunchbase](https://www.crunchbase.com/) (global funding data, academic API access), [Dealroom.co](https://dealroom.co/) (strong European coverage), [ITJuzi/IT桔子](https://www.itjuzi.com/) (Chinese startup ecosystem), and news sources (TechCrunch, 36Kr, Sifted) for enrichment. Each company record contains 20+ variables: name, region (US/CN/EU), country, city, geocoded coordinates, founding year, value chain layer (Infrastructure / Foundation Model / Middleware / Application / Developer Tools), sub-category, total funding (USD), latest valuation, funding round stage, estimated ARR, employee count, operational status, business model, key investors, moat type, and open-source strategy.

**Data quality assessment:** The data is generally well-structured but presents three challenges. First, valuation opacity — many startups (especially Chinese ones) lack public valuation disclosures, so we use secondary estimates and flag confidence levels. Second, temporal misalignment — funding data arrives from different reporting dates; we normalize to the latest available point per company (cutoff: March 2026). Third, survivor bias — public databases over-represent funded, surviving companies; we deliberately include 10–15 failed or pivoted startups (e.g., Stability AI restructuring, 01.AI downsizing) to mitigate this.

**Preprocessing** involves: deduplication across sources, currency normalization to USD using exchange rates at funding date, geocoding headquarters for map visualizations, and manual verification of outlier values. The final dataset is stored as structured JSON and CSV for flexibility in both D3.js and Python-based exploration. No heavy scraping or NLP is required — the primary effort is cross-source reconciliation and manual curation of Chinese-language sources.

### Problematic

In February 2026, global AI venture investment hit $189 billion — the largest single month ever — yet 83% flowed to just three companies. Meanwhile, China's DeepSeek matched GPT-4 at a fraction of the cost, and Europe's Mistral AI raised €1.7B as the continent's AI champion. These developments reveal a fragmented, rapidly evolving global landscape that is difficult to understand from any single data source or static report.

**Central question:** *How do the AI startup ecosystems of the US, China, and Europe differ in structure, strategy, and trajectory — and what do these differences reveal about where future innovation will emerge?*

We develop an **interactive exploratory dashboard** addressing five axes:

1. **Capital concentration** — How is funding distributed across value chain layers and geographies? Is "winner-take-all" universal or region-specific?
2. **Ecosystem structure** — Do regions produce fundamentally different types of AI companies? (US: foundation models + infrastructure; China: model-layer concentration integrated into super-apps; Europe: regulation-aligned open-source)
3. **Capital efficiency** — Do Chinese/European startups systematically achieve comparable outcomes with less capital?
4. **Temporal dynamics** — How has startup creation shifted across layers from 2019–2026?
5. **Failure patterns** — Where do AI startups fail, and does value chain position correlate with survival?

**Target audience:** Aspiring AI entrepreneurs evaluating where to build; investors seeking structural cross-geographic comparison; policy researchers studying how regulation and compute access shape innovation. The design follows Shneiderman's mantra: *overview first, zoom and filter, then details-on-demand*.

### Exploratory Data Analysis

Initial EDA on 36 core companies reveals several structural patterns:

**Regional capital concentration is extreme.** The US accounts for 87% of total valuation ($1,193B) and 84% of funding ($109.7B), but this is driven almost entirely by three mega-caps (OpenAI $500B, Anthropic $380B, xAI $200B). Excluding the top 3, the US average drops from $74.6B to $16.9B — still higher than China ($3.6B) and Europe ($4.2B), but by a far smaller margin. This concentration is itself a key visualization target.

**Value chain distributions differ sharply by region.** China's ecosystem is 70% Foundation Model companies (the "Hundred Model War" effect). The US is most diversified and uniquely dominates Infrastructure (Cerebras, Groq, Scale AI, Databricks) — a layer near-absent in CN/EU. Europe is carving a niche in Developer Tools (Lovable, Poolside).

**Capital efficiency varies systematically.** Measured as Valuation/Funding ratio: DeepSeek (CN) achieves 20.0x, Lovable (EU) 17.4x, OpenAI (US) 12.5x, Mistral (EU) 4.7x, SenseTime (CN) 1.1x. Chinese and European startups achieve comparable technical outcomes with 5–20x less capital.

**Founding year analysis** shows 2022–2023 as the modal period (ChatGPT catalyst), but a structural shift: early startups are disproportionately model-layer; 2024+ startups skew toward specialized tools and vertical applications — suggesting ecosystem maturation from "build a model" to "build on models."

**Open-source strategy** shows regional divergence: CN/EU startups release open-weight models far more than US peers, reflecting cost-advantage (China) vs. sovereignty/trust signaling (Europe) vs. revenue protection (US).

We built a working React prototype (Recharts) with filterable overview, scatter plot, treemap, radar chart, and sortable table, validating feasibility.

### Related work

**What others have done:** CB Insights' *State of AI Report* provides comprehensive annual funding surveys but as static PDFs. Stanford HAI's *AI Index* offers macro-level cross-country statistics but focuses on aggregate metrics, not company-level exploration. Dealroom.co covers European startups interactively but lacks cross-regional comparison with China. Matt Turck's *"AI Landscape"* (FirstMark Capital) is an influential annual infographic mapping the ecosystem — visually dense but entirely static with no filtering or drill-down. Crunchbase and PitchBook offer company-searchable databases but lack analytical framing or research-question-driven design.

**Why our approach is original:** No existing visualization provides a **unified, cross-regional comparison** of US, China, and European AI startups at the company level with value-chain decomposition. The geographic fragmentation of data sources (Crunchbase for US, ITJuzi for China, Dealroom for EU) has historically prevented this integration. We fill the gap between static reports and neutral data browsers by providing an **analytical narrative delivered through interactive visualization**, with explicit research questions guiding design choices.

**Visualization inspirations:** Gapminder (Hans Rosling) for animated bubble charts comparing entities over time; Mike Bostock's D3 Zoomable Treemap for hierarchical decomposition (Region → Layer → Company); *"Wealth Inequality in America"* for making extreme concentration viscerally legible; and the Pudding's data essays for narrative-driven interactive storytelling.

This dataset has not been used in any prior coursework.


## Milestone 2 (2nd May, 5pm)

**10% of the final grade**


## Milestone 3 (30th May, 5pm)

**80% of the final grade**

