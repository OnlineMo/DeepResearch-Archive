# DeepResearch Archive — Project B (Overview)
This repository stores AI-generated research reports and the display scaffolding. Project A (the automation pipeline) generates reports and updates navigation. Project B focuses on content storage and consumption (read-only for humans).

- Navigation file: NAVIGATION.md (idempotently updated by Project A)
- Today homepage: README.md (shows today's reports only; updated by Project A)
- Reports root directory: AI_Reports/
- Optional metadata index: history.json

简要说明（中文）：
- 本仓库仅负责“存储报告与展示”。报告由项目 A 自动生成并推送。
- README.md 只展示“当日最新报告”（由 A 自动更新）。
- NAVIGATION.md 展示全量分类导航（由 A 自动更新，幂等）。

## Repository Structure

```
DeepResearch-Archive/
├─ README.md                 # Today-only homepage (auto-updated by Project A)
├─ NAVIGATION.md             # Global navigation (auto-generated/updated)
├─ AI_Reports/
│  ├─ ai-ml/
│  ├─ llm/
│  ├─ software-dev/
│  ├─ cybersecurity/
│  ├─ cloud-devops/
│  ├─ data/
│  ├─ web-mobile/
│  ├─ consumer-tech/
│  ├─ gaming/
│  ├─ blockchain/
│  ├─ science/
│  ├─ healthcare/
│  ├─ energy-climate/
│  ├─ economy/
│  ├─ policy/
│  ├─ industry/
│  ├─ culture-media/
│  └─ uncategorized/
└─ (optional) history.json
```

Naming conventions:
- File: {title}-{date}--v{edition}.md (title uses title_en if provided, otherwise title; Chinese or English allowed; invalid characters will be normalized)
- Directory: use category_slug as URL-safe folder (lowercase hyphenated); display names are decoupled and managed in a mapping
- Encoding: UTF-8; Chinese/English filenames allowed; normalize illegal filesystem characters during generation

## Categories (Extensible)
- ai-ml — AI & Machine Learning
- llm — Large Language Models
- software-dev — Software Development & Engineering
- cybersecurity — Security
- cloud-devops — Cloud & DevOps
- data — Data & Databases
- web-mobile — Web & Mobile
- consumer-tech — Consumer Electronics & Hardware
- gaming — Gaming & Interaction
- blockchain — Blockchain & Crypto
- science — Science & Space
- healthcare — Healthcare & BioTech
- energy-climate — Energy & Climate
- economy — Economy & Markets
- policy — Policy & Regulation
- industry — Industry & Companies
- culture-media — Culture & Media
- uncategorized — Uncategorized (fallback)

注：显示名与 slug 的映射可由 Project A 维护（如 categories 映射文件），但非强依赖。

## README.md (Today Only)
README.md is reserved for today's reports. Project A will idempotently replace the content between the markers below:
- <!-- TODAY_REPORTS:START max=20 -->
- <!-- TODAY_REPORTS:END -->
Project A should also set the date using:
- 日期占位: <!-- DATE -->YYYY-MM-DD<!-- /DATE -->

## NAVIGATION.md (Global)
NAVIGATION.md lists all categories with collapsible sections and recent N entries per category (default 20), sorted by date desc. Project A rebuilds it by scanning AI_Reports, ensuring a pure-function style (idempotent) regeneration.

## Report File Template (Recommended)

Each report should include a YAML front matter for metadata and a structured body for consistent indexing and regeneration.

```md
---
title: AI 本地小模型优化
date: 2025-08-20
edition: v1
category_slug: ai-ml
category_display: AI 与机器学习
source: https://trends.google.com/...
slug: ai-ben-di-xiao-mo-xing-you-hua
---

# 摘要
- 核心发现/要点（3-5 条）

# 背景
- 背景信息与跨源验证

# 深度分析
- 论点 1
- 论点 2
- 论点 3

# 数据与引用
- [来源 1](...)
- [来源 2](...)

# 结论与建议
- 结论与可执行建议
```

## history.json (Optional)
A minimal index for idempotency and backtracking.

```json
{
  "version": 1,
  "updatedAt": "2025-08-20T00:00:00Z",
  "items": [
    {
      "slug": "ai-ben-di-xiao-mo-xing-you-hua",
      "display": "AI 本地小模型优化",
      "category_slug": "ai-ml",
      "category_display": "AI 与机器学习",
      "date": "2025-08-20",
      "edition": "v1",
      "path": "AI_Reports/ai-ml/AI 本地小模型优化-2025-08-20--v1.md",
      "source": "https://trends.google.com/...",
      "run_id": "20250820-xxxx",
      "status": "ok"
    }
  ]
}
```

## Slug Rules
- Slugs are used for directories and internal IDs only (e.g., category_slug and history.slug); not used in filenames
- category_slug: lowercase, hyphenated, URL-safe; keep stable across renames
- Filenames use title_en if provided, otherwise title; no pinyin required; normalize illegal characters during generation
- Keep a stable slug in front matter for de-duplication and history tracking

## Manual edits (Optional)
- You may manually refine report content, but keep filename and YAML key fields (slug/date/edition/category_slug) unchanged.
- New reports should follow the template; NAVIGATION.md/README.md will be updated by Project A automatically.

## License
MIT