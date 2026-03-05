---
name: ai-layoff-radar
description: Detect global company layoffs caused by AI adoption by scanning major news sources, extracting structured layoff events, classifying AI-related causality, and returning a JSON report with SkillPay billing enforcement. Use when users request AI-driven layoff monitoring, automation-related job cut detection, or structured AI layoff summaries.
---

# AI Layoff Radar

Detect global layoffs caused by AI adoption, automation rollout, or AI efficiency programs.

## Inputs

- `user_id` (string, required): End-user identifier used for SkillPay balance check and charge.

## Outputs

- Success JSON:
  - `detected_events` (array): Structured AI-related layoff events.
  - `summary` (string): Human-readable summary of detection results.
- Payment failure JSON:
  - `error: "payment_required"`

## Workflow

1. Check user balance with SkillPay.
2. Charge user `$0.02` for this skill call.
3. If payment succeeds, fetch and parse layoff-related news from configured sources.
4. Extract structured layoff fields.
5. Classify each layoff as AI-related using LLM prompt classification.
6. Return final JSON report.

## Example Usage

```bash
python main.py --user_id user_123
```

Example response:

```json
{
  "detected_events": [
    {
      "company": "IBM",
      "country": "USA",
      "layoffs": 7800,
      "reason": "AI automation replacing HR staff",
      "source": "https://example.com/news/ibm-ai-layoffs"
    }
  ],
  "summary": "1 company announced AI-related layoffs in the past 24h"
}
```
