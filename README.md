# TikTok Influencer Finder

A skill for Claude Code / OpenClaw that helps you discover and research TikTok creators for brand collaborations and influencer marketing campaigns.

## What It Does

Give it a product description or niche category, and it will:

1. **Analyze your brief** — Understand your product, target market, and ideal creator profile
2. **Generate smart search keywords** — Multi-language (English + Chinese), multi-angle keyword strategy
3. **Find relevant creators** — Search across influencer databases, ranking sites, TikTok Creative Center, and content aggregators
4. **Compile organized results** — Output a professional spreadsheet (.xlsx + .csv) with full creator profiles

## Data Collected Per Creator

| Category | Fields |
|----------|--------|
| **Basic** | Name, Username, Profile URL, Niche, Follower Count |
| **Engagement** | Engagement Rate, Average Views, Posting Frequency |
| **Business** | Contact Info, Estimated Pricing, Brand Collaboration History |
| **Audience** | Demographics, Language, Top Markets |
| **Content** | Content Style, Bio, Top Performing Videos, Other Platforms |

## Installation

### Method 1: Tell your bot to install (Recommended)

Send this message to your Claude Code or OpenClaw bot:

```
帮我安装一个TikTok博主搜索的skill，GitHub仓库地址是：
https://github.com/mukiiiina/tiktok-influencer-finder
请克隆到你的skills目录下，然后安装依赖 openpyxl
```

Or in English:

```
Please install a TikTok influencer finder skill from this repo:
https://github.com/mukiiiina/tiktok-influencer-finder
Clone it into your skills directory and install the openpyxl dependency.
```

The bot will figure out the correct skills directory and handle the installation automatically.

### Method 2: Clone from GitHub manually

Clone the repo into your bot's skills directory (the exact path depends on your platform):

```bash
git clone https://github.com/mukiiiina/tiktok-influencer-finder.git
pip install openpyxl
```

Then restart your bot session. The skill will be auto-loaded.

### Method 3: Download and copy

Download this repository as a ZIP, extract it, and place the `tiktok-influencer-finder` folder into your bot's skills directory. Make sure `SKILL.md` is at the root of the folder.

### Dependencies

The spreadsheet generation script requires `openpyxl`:

```bash
pip install openpyxl
```

## Usage Examples

### English

```
Find me TikTok influencers who review skincare products, 
targeting the US market, preferably micro to mid-tier creators
```

```
I'm launching a new fitness app. Help me find TikTok creators 
who make workout and health content, any follower size
```

```
Find TikTok food bloggers who do restaurant reviews in New York
```

### Chinese / 中文

```
帮我找TikTok上做美妆测评的博主，主要针对美国市场，粉丝量10万到100万之间
```

```
我想推广一款宠物食品，帮我找TikTok上的宠物博主
```

```
找一些TikTok上的科技数码博主，要经常做开箱视频的那种
```

## Output

The skill generates two files:

- **`tiktok_influencers.xlsx`** — Formatted Excel file with:
  - Color-coded rows by follower tier (Macro/Mid/Micro/Nano)
  - Clickable profile URLs
  - Auto-sized columns
  - Summary sheet with search brief and tier breakdown
  
- **`tiktok_influencers.csv`** — Plain CSV for Google Sheets import

## Project Structure

```
tiktok-influencer-finder/
├── SKILL.md                    # Core skill instructions
├── LICENSE.txt                 # MIT License
├── README.md                   # This file
├── scripts/
│   └── create_spreadsheet.py   # Spreadsheet generator
└── references/
    └── search_strategy.md      # Keyword templates by niche
```

## How the Search Works

The skill uses a multi-source search strategy:

1. **Influencer ranking sites** — Curated lists from marketing platforms
2. **TikTok Creative Center** — Official trending creator data
3. **Content aggregator sites** — Blog posts and articles listing top creators
4. **Cross-platform discovery** — Find creators through their YouTube/Instagram presence

Keywords are generated across 6 dimensions:
- Direct niche keywords
- Sub-niche keywords
- Audience-aligned keywords
- Platform-specific keywords
- Cross-platform discovery keywords
- Chinese/bilingual keywords

## Customization

### Appending to existing lists

If you already have a spreadsheet and want to add more creators:

```
I already have an influencer list at influencer_list.xlsx. 
Find more gaming TikTok creators and add them to the existing file.
```

The skill will deduplicate by username automatically.

### Adjusting search scope

Specify any of these in your request:
- **Follower tier**: nano, micro, mid-tier, macro, or all
- **Target market**: US, UK, global, specific countries
- **Content style**: reviews, tutorials, vlogs, unboxing, etc.
- **Language**: English, Chinese, bilingual

## Contributing

Contributions are welcome! Feel free to:

1. Fork the repository
2. Add new niche keyword templates to `references/search_strategy.md`
3. Improve the spreadsheet formatting in `scripts/create_spreadsheet.py`
4. Submit a pull request

## License

MIT License - see [LICENSE.txt](LICENSE.txt) for details.
