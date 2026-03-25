---
name: tiktok-influencer-finder
description: "Find and research TikTok influencers/creators for brand collaborations and marketing campaigns. Use this skill whenever the user wants to find TikTok bloggers, creators, or KOLs for product promotion, influencer marketing, brand partnerships, or content collaboration. Triggers when: user mentions finding TikTok creators, searching for TikTok influencers, building a KOL list, influencer outreach, TikTok marketing, looking for bloggers to promote products, or wants to create a list of potential TikTok partners for their brand. Also triggers for Chinese terms like 找博主, TikTok达人, 网红推广, KOL列表, 博主合作. Works with any product category or niche - beauty, tech, food, fitness, fashion, gaming, pets, travel, etc. Outputs organized spreadsheets (.xlsx and .csv) with influencer profiles, engagement metrics, and contact information."
---

# TikTok Influencer Finder

A comprehensive tool for discovering and researching TikTok creators that match your brand's needs. Given a product description or niche category, this skill automatically generates optimal search keywords, finds relevant creators through multiple channels, and compiles a well-organized influencer list.

## How This Skill Works

The workflow has 4 phases:

1. **Understand the Brief** — Analyze the user's product/niche and determine the ideal creator profile
2. **Generate Search Strategy** — Create multi-language, multi-angle search keywords
3. **Research Creators** — Search across multiple sources to find matching TikTok creators
4. **Compile & Deliver** — Organize findings into a professional spreadsheet

## Phase 1: Understand the Brief

When the user describes their product or desired influencer type, extract and confirm:

- **Product/Brand**: What's being promoted?
- **Target Market**: Which countries/regions? (defaults to US + global if not specified)
- **Budget Tier**: Nano (<10K), Micro (10K-100K), Mid-tier (100K-1M), Macro (1M+), or all tiers
- **Content Style**: Educational, entertainment, review, unboxing, lifestyle, etc.
- **Language Preference**: English, Chinese, bilingual, or other
- **Output Language**: Whether the spreadsheet headers and labels should be in Chinese or English. Auto-detect from the user's input language — if they write in Chinese, use `--lang cn`; if English, use `--lang en`.

If the user's request is vague (e.g., "find me some beauty bloggers"), ask one clarifying question that covers the most critical gaps. Don't over-interrogate — make reasonable assumptions and state them.

**Example assumption statement:**
> "I'll search for beauty/skincare TikTok creators in the US market, across all follower tiers, focusing on review and tutorial-style content. Let me know if you'd like to adjust any of these."

## Phase 2: Generate Search Strategy

This is the core intelligence of the skill. Based on the brief, generate a comprehensive keyword strategy.

### Keyword Generation Rules

For each product/niche, generate keywords across these dimensions:

**1. Direct Niche Keywords** (the obvious ones)
- Product category + "TikTok creator/influencer/blogger"
- Example: "skincare TikTok influencer", "beauty TikTok creator"

**2. Sub-Niche Keywords** (more specific, higher relevance)
- Break the niche into sub-categories
- Example for skincare: "anti-aging skincare TikTok", "K-beauty TikTok creator", "acne skincare routine TikTok"

**3. Audience-Aligned Keywords** (who watches this content)
- Think about the target consumer, not just the product
- Example: "mom skincare routine TikTok", "college skincare TikTok", "men's grooming TikTok"

**4. Platform-Specific Keywords** (for searching ranking sites and databases)
- "top TikTok [niche] creators 2024/2025"
- "best TikTok [niche] accounts to follow"
- "TikTok [niche] influencer list"
- "[niche] TikTok creator database"

**5. Cross-Platform Discovery Keywords** (creators often have multi-platform presence)
- "best [niche] content creators" (they likely have TikTok too)
- "[niche] influencer marketing"

**6. Chinese Keywords** (if targeting Chinese-speaking creators or global market)
- "[产品类型] TikTok博主"
- "[产品类型] TikTok达人推荐"
- "TikTok [产品类型] 网红"
- "[产品类型] 海外网红"

### Search Sources Priority

Search these sources in order of reliability:

1. **Influencer ranking sites & databases**
   - Search for curated lists: "top [niche] TikTok creators 2025"
   - Influencer marketing platform listings (tokfluence, heepsy, modash, upfluence, collabstr)
   - Creator marketplace directories

2. **TikTok Creative Center** (ads.tiktok.com/business/creativecenter)
   - Trending creators by category
   - Top-performing content in the niche
   - Note: this is publicly accessible, no login required for basic browsing

3. **Content aggregator sites**
   - Articles listing "best TikTok creators in [niche]"
   - Social media marketing blogs
   - Industry-specific publications

4. **Social media cross-reference**
   - YouTube creators who also have TikTok
   - Instagram creators who cross-post to TikTok

Use the `WebSearch` tool for each search query. For each search, extract creator names, usernames, and any available metrics. Use `WebFetch` to visit promising links and extract detailed creator information.

## Phase 3: Research Creators

For each discovered creator, try to collect:

### Required Fields (must have)
| Field | Description |
|-------|-------------|
| Creator Name | Display name on TikTok |
| TikTok Username | @handle |
| Profile URL | Full TikTok profile link (https://www.tiktok.com/@username) |
| Niche/Category | Primary content category |
| Follower Count | Approximate follower count |

### Important Fields (try to find)
| Field | Description |
|-------|-------------|
| Engagement Rate | Average likes+comments / followers percentage |
| Average Views | Typical view count per video |
| Posting Frequency | How often they post (daily, weekly, etc.) |
| Content Style | What kind of content they make (reviews, tutorials, vlogs, etc.) |
| Contact Info | Email, business inquiry link, or agency |

### Bonus Fields (include if available)
| Field | Description |
|-------|-------------|
| Estimated Pricing | CPM or per-post rate if publicly listed |
| Audience Demographics | Age range, gender split, top countries |
| Brand Collab History | Known brand partnerships |
| Other Platforms | YouTube, Instagram handles |
| Bio Description | Their TikTok bio text |
| Top Performing Content | Links to viral/popular videos |
| Language | Primary language of content |

### Data Quality Standards

- **Minimum 10 creators** per search (aim for 15-30 for comprehensive results)
- **Verify usernames** — construct TikTok URLs as `https://www.tiktok.com/@username`
- **Note data freshness** — mark if metrics are from a ranking site (may be outdated) vs. profile check
- **Remove duplicates** — same creator found from multiple sources should appear once
- **Sort by relevance** — most relevant creators first, then by follower count within tiers

## Phase 4: Compile & Deliver

### Output Format

Generate both `.xlsx` and `.csv` files using the Python script at `scripts/create_spreadsheet.py`.

Read the script's help text first:
```bash
python scripts/create_spreadsheet.py --help
```

The script accepts a JSON file with the influencer data and produces a formatted spreadsheet.

### JSON Data Format

Prepare the data as a JSON file with this structure:

```json
{
  "search_brief": {
    "product": "organic skincare line",
    "target_market": "US",
    "budget_tier": "micro to mid-tier",
    "content_style": "reviews and tutorials",
    "date_generated": "2025-01-15"
  },
  "creators": [
    {
      "name": "Creator Display Name",
      "username": "tiktok_handle",
      "profile_url": "https://www.tiktok.com/@tiktok_handle",
      "niche": "Skincare & Beauty",
      "follower_count": "150K",
      "engagement_rate": "4.5%",
      "avg_views": "50K",
      "posting_frequency": "Daily",
      "content_style": "Product reviews, tutorials",
      "contact": "email@example.com",
      "estimated_pricing": "$200-500/post",
      "audience_demographics": "18-34, 70% female, US/UK",
      "brand_collabs": "CeraVe, The Ordinary",
      "other_platforms": "IG: @handle, YT: @handle",
      "bio": "Their bio text here",
      "top_content": "https://www.tiktok.com/@handle/video/123",
      "language": "English",
      "source": "Where this data was found",
      "notes": "Any additional notes"
    }
  ]
}
```

Fields can be empty strings `""` if information is not available — the script handles missing data gracefully.

### Running the Script

```bash
# English output (default)
python scripts/create_spreadsheet.py input_data.json --output influencer_list --format both

# Chinese output (中文表头)
python scripts/create_spreadsheet.py input_data.json --output influencer_list --format both --lang cn
```

This generates:
- `influencer_list.xlsx` — Formatted Excel file with colored headers, auto-sized columns, and a summary sheet
- `influencer_list.csv` — Plain CSV for easy import into Google Sheets or other tools

### Spreadsheet Structure

The Excel file contains two sheets:

**Sheet 1: "Influencer List"**
- All creator data in a formatted table
- Header row with colored background
- Columns auto-sized for readability
- Follower count sorted from high to low within each tier
- Hyperlinked profile URLs

**Sheet 2: "Search Summary"**
- Search brief details
- Date generated
- Total creators found
- Breakdown by follower tier
- Keywords used

### Appending to Existing Files

If the user wants to add results to an existing spreadsheet:

```bash
python scripts/create_spreadsheet.py input_data.json --output existing_file.xlsx --append
```

This preserves existing data and adds new creators, deduplicating by username.

## Language Handling

This skill works in both English and Chinese. Auto-detect the user's language from their input and respond accordingly.

- If user writes in Chinese: respond in Chinese, include Chinese keywords in search, format output headers bilingually
- If user writes in English: respond in English
- Search keywords should always include both English and Chinese variants for broader coverage, regardless of the user's language

## Tips for Best Results

- When searching, cast a wide net first (use many keyword variations), then filter for relevance
- Cross-reference creators found on multiple lists — they're likely more established and reliable
- Pay attention to engagement rate, not just follower count — micro-influencers (10K-100K) often have better engagement rates and ROI
- Check content recency — creators who posted in the last 30 days are actively creating
- Look for creators who have done brand deals in adjacent (not competing) categories — they're experienced with collaborations

## Error Handling

- If WebSearch returns limited results for a keyword, try alternative phrasings
- If a niche is very specific, broaden the search and then manually filter
- If follower counts or engagement data can't be verified, mark them as "estimated" in the notes
- Always inform the user how many creators were found and suggest next steps (e.g., "I found 18 creators. Want me to dig deeper into any specific tier or sub-niche?")
