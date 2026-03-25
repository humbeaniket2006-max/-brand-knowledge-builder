# 🌲 Brand Knowledge Base Auto-Builder

[Open In Colab][(https://github.com/humbeaniket2006-max/-brand-knowledge-builder/blob/main/Brand_Knowledge_Builder_(1).ipynb)](https://colab.research.google.com/drive/17rxm7vwbNMdXZwkrD2_fGjzyvAlQaHcc)

> Built for **PineOS** — the AI operating system for brand intelligence.

---

## The Problem

When a D2C brand onboards onto an AI intelligence platform, someone has to **manually** enter:

- Product catalog & categories
- FAQs & customer queries
- Return & shipping policies
- Brand tone of voice
- Contact info

For a 2-person founding team onboarding multiple brands, this doesn't scale.

---

## The Solution

```
paste any brand URL → structured AI-ready knowledge pack in seconds
```

```bash
# Input
mamaearth.in

# Output → mamaearth_brand_knowledge.json
{
  "brand_name": "Mamaearth",
  "tagline": "Goodness Inside",
  "tone_of_voice": ["natural", "trustworthy", "clinical"],
  "products_and_categories": [...],
  "faqs": [...],
  "shipping_policy": "Free shipping on orders above ₹299...",
  "return_policy": "7-day easy returns...",
  "contact": { "email": "...", "phone": "..." }
}
```

**Ready to plug into any AI pipeline** — RAG, chatbot grounding, fine-tuning datasets, brand intelligence reports.

---

## Demo

| Brand | Pages Crawled | Products | FAQs | Time |
|-------|--------------|----------|------|------|
| mamaearth.in | 8 | 12 | 9 | ~18s |
| bewakoof.com | 7 | 10 | 6 | ~15s |
| nykaa.com | 8 | 14 | 11 | ~20s |

---

## Quickstart

**Run in Colab (no setup needed):**

Click the badge above → run cells top to bottom → done.

```
Cell 1 — Install dependencies
Cell 2 — Paste your Gemini API key
Cell 3 — Load core functions
Cell 4 — Enter brand URL → Extract
Cell 5 — View full JSON output
Cell 6 — Download the knowledge pack
Cell 7 — Batch mode (multiple brands at once)
```

---

## How It Works

```
URL input
   ↓
Crawl up to 8 pages (homepage + FAQ, about, policy, contact pages)
   ↓
Extract clean text (removes scripts, nav, footer, ads)
   ↓
Gemini 2.0 Flash Lite — structured extraction
   ↓
Rule-based fallback (if no API key or rate limit hit)
   ↓
JSON knowledge pack output
```

**Smart crawling** — prioritises high-signal pages (FAQ, about, returns, shipping, contact) over product listing pages. Discovers them automatically from the homepage's link graph.

**Retry logic** — handles Gemini rate limits with exponential backoff (up to 4 retries, 10s base delay).

**Rule-based fallback** — works without a Gemini key. Detects tone of voice, price patterns, policy snippets, and contact info via heuristics.

---

## Output Schema

```json
{
  "brand_name": "string",
  "website": "string",
  "tagline": "string",
  "tone_of_voice": ["list of detected tones"],
  "products_and_categories": [
    { "name": "string", "description": "string", "price": "string|null" }
  ],
  "faqs": [
    { "question": "string", "answer": "string" }
  ],
  "shipping_policy": "string|null",
  "return_policy": "string|null",
  "contact": {
    "email": "string|null",
    "phone": "string|null"
  },
  "pages_crawled": ["list of URLs"],
  "extraction_method": "gemini-2.0-flash-lite | rule-based"
}
```

---

## Pipeline Integration

The output JSON is designed to be directly usable as:

- **RAG grounding** — embed into Pinecone, Chroma, or Weaviate as brand context chunks
- **Chatbot system prompt** — inject as brand knowledge for AI customer support agents
- **Fine-tuning pairs** — use FAQ Q&A pairs as training data
- **Brand analytics** — structured data ready for dashboards or comparisons

---

## Stack

| Layer | Tech |
|-------|------|
| Scraping | `requests` + `BeautifulSoup4` |
| AI extraction | `Gemini 2.0 Flash Lite` via `google-genai` |
| Fallback | Rule-based heuristics (regex + keyword matching) |
| Runtime | Python 3.10+ · Google Colab compatible |

---

## Get a Free Gemini API Key

1. Go to [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
2. Sign in with Google → Create API key
3. Paste into Cell 2 of the notebook (or store in Colab Secrets as `GEMINI_API_KEY`)

Free tier is sufficient for dozens of brand extractions per day.

---

## Batch Mode

Extract multiple brands at once via Cell 7:

```
mamaearth.in, bewakoof.com, nykaa.com, boat-lifestyle.com
```

Outputs a single `all_brands_knowledge.json` with all results. Includes automatic 15s rate-limit buffer between brands.

---

## Built By

**Aniket Humbe** — Intel OpenVINO™ Contributor · AI/ML Developer · BS Data Science @ IIT Madras

[Portfolio](https://humbeaniket2006-max.github.io/my-portfolio/) · [LinkedIn](http://www.linkedin.com/in/aniket-ankush-humbe-26124b384) · [GitHub](https://github.com/humbeaniket2006-max)
