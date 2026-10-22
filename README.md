---
license: cc-by-4.0
language:
- en
pretty_name: "AI shopping-answer sources for hand massager questions (ChatGPT and Perplexity, Oct 2026)"
tags:
- ai-search
- citations
- chatgpt
- perplexity
- consumer-products
size_categories:
- 1K<n<10K
configs:
- config_name: answer_sources
  data_files: ai-answer-sources.csv
- config_name: runs
  data_files: ai-runs.csv
- config_name: sub_queries
  data_files: ai-sub-queries.csv
---

# AI shopping-answer sources for hand massager questions (ChatGPT and Perplexity, Oct 2026)

Compiled by Wearmelly. We sell Melly, a heated hand massager (wearmelly.com); Melly is not included in this dataset.

## What this is

People increasingly ask AI assistants what to buy. This dataset records, for 39 shopping questions about hand massagers, **which web pages the assistants cited in their answers and which pages they inspected while answering.** It is a record of what happened in 137 runs, not a ranking of websites and not a measurement of answer quality. **AI answers vary run to run; counts are descriptive.**

The answers' text is not included. This dataset makes no medical claims and gives no medical advice. The questions are the questions that were asked, and the sources are what the assistants returned.

## Contents

| file | rows | one row is |
|---|---|---|
| `ai-runs.csv` | 137 | one run of one question on one assistant |
| `ai-answer-sources.csv` | 2900 | one source (cited or inspected) in one run |
| `ai-sub-queries.csv` | 296 | one search sub-query an assistant issued during a run |

- Runs: 2026-10-16: ChatGPT 54, Perplexity 54; 2026-10-19: ChatGPT 19, Perplexity 10.
- Sources: 472 cited rows and 2428 inspected rows; 456 distinct domains.
- Question groups (`angle`):

| angle | what the questions are | questions | runs |
|---|---|---|---|
| `crochet-knitting` | questions from people who knit or crochet | 7 | 26 |
| `desk-carpal` | questions from desk and computer users about hand and wrist strain | 9 | 36 |
| `arthritis` | questions from people with stiff or arthritic hands | 9 | 38 |
| `general` | general purchase questions | 4 | 8 |
| `product-kb` | product-knowledge questions (battery, noise, controls, auto shut-off, etc.) | 10 | 29 |

The `angle` value is the topic of the question, not a claim about any product.

## How it was collected

- Each question was typed into the assistant's normal web interface (browser, English, web search on). A browser-console script recorded the assistant's streamed response and search activity. Each question was run 1 to 3 times per assistant.
- 2026-10-16: 108 runs (54 ChatGPT, 54 Perplexity) on 29 questions in four topic groups.
- 2026-10-19: 29 runs (19 ChatGPT, 10 Perplexity) on 10 product-knowledge questions. Per-run timestamps were not recorded for these runs; the date is the collection day.
- `cited` = a page linked or referenced in the answer text. `inspected` = a page the assistant opened or retrieved while working, according to the capture. A page can be inspected without being cited.
- `rank_basis` says what `rank` means for that row; it differs by source type and engine. For ChatGPT inspected pages the order is alphabetical by URL, not the order shown. For cited pages it is the order of first mention in the answer. For Perplexity inspected pages it is the engine's result-list order, and the display order was not verified.
- Removed before publication: the answer text, account, plan and interface details, internal file names and tags, and 4 runs set aside because their question did not match the question list. Rows or questions mentioning the compiler's own brand or product: none were present. One access token was removed from one URL, and one broken character was removed from one page title.

## Columns

**ai-runs.csv**: `run_id` (R001 to R137, our numbering), `date`, `engine` (chatgpt or perplexity), `query_id`, `angle`, `cited_count`, `inspected_count`, `sub_query_count`, `location`, `location_note`, `query_text`.
**ai-answer-sources.csv**: `run_id`, `run_date`, `engine`, `query_id`, `query_text`, `angle`, `source_type` (cited or inspected), `rank`, `rank_basis`, `domain`, `url`, `title`. The title is empty when the capture did not record one (787 rows).
**ai-sub-queries.csv**: `run_id`, `position`, `sub_query`, `capture_origin`, `is_verbatim_user_query` (yes when the capture flags the sub-query as the user's question sent as is), `added_brand` and `site_operator` (none unless the sub-query added a brand name or a site: restriction).

Counts in `ai-runs.csv` match the row counts in the other two files.

## Location

The assistants' location and account state were **not recorded** for any run (`location` = "not recorded"), although many questions state a US location in their text. 17 runs (16 ChatGPT, 1 Perplexity) show traces of a collection environment outside the US in the answer text or sources (₺ prices, Türkiye or Turkey, or .com.tr / .tr domains); they are marked in `location_note`. For those runs, price and seller findings are unreliable for a US shopper. Runs with "not flagged" were not checked in any other way.

## Limits

- Few repeats per question; no control for account, location or time of day. Do not compare shares between assistants or between days as if they were measurements of a stable system.
- The capture shows what the interface exposed. It may not list every page an assistant used.
- Assistants change quickly; these are October 2026 snapshots.
- Titles and URLs belong to the sites that published them.
- The 2026-10-19 runs cover product-knowledge questions only; the 2026-10-16 runs cover the four topic groups. Groups are not balanced.
- query_text for query IDs Q1–Q8 and Q10 is truncated at about 80 characters in the source log; the full wording of the questions was longer. In `ai-runs.csv` and `ai-answer-sources.csv` these texts end with "…" to mark the cut.

## License

CC BY 4.0 (see `LICENSE`). The license covers our compilation; page titles and URLs belong to their publishers.

## Citation

See `CITATION.cff`. Suggested: Erin, M. V. (2026). *AI Shopping Answer Sources: Hand Massagers*. Wearmelly. https://wearmelly.com. CC BY 4.0.
