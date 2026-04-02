# TweetNugget

A nugget of wisdom from the bird app.

Curated collections of inspirational tweets and wisdom from Twitter/X, ready to brighten your day.

## Install

From ClawHub:

```bash
clawhub install tweetnugget
```

Or via OpenClaw CLI:

```bash
openclaw skills install tweetnugget
```

Or manually: copy this folder to `~/.openclaw/skills/tweetnugget/`

## Usage

In any chat where OpenClaw is active:

```
Give me a quote
Hit me with some wisdom
I need inspiration
Quote about AI
Something about leadership
Surprise me
```

## Example Output

> "The purpose of knowledge is action." — @RyanHoliday

> "Most of coding was never about writing code. AI is just making this more obvious. You no longer need to recall syntax, function structure, boilerplate code, or even API endpoints. The hard part was never typing. It was always thinking. And it still is." — @Prathkum

> "Waste no more time arguing about what a good man should be. Be one." — @dailystoic - Marcus Aurelius

## Collections

| Collection | Quotes | Source |
|---|---|---|
| `swlw-tweets.json` | 37 | Software Lead Weekly newsletter (issues #681-#663) |
| `twitter-quotes.json` | 12 | Curated Twitter wisdom |
| `stoic-quotes.json` | 6 | Stoic philosophy quotes |

**Total: 55 quotes across 3 collections**

## Available Tags

Filter quotes by topic: `action`, `advice`, `ai`, `anxiety`, `authorship`, `building`, `burnout`, `business`, `career`, `change`, `coding`, `confidence`, `creation`, `courage`, `decision-making`, `deliberate-practice`, `design`, `discipline`, `distribution`, `dopamine`, `early-career`, `engineering`, `excellence`, `explanation`, `finance`, `focus`, `goals`, `happiness`, `hiring`, `humor`, `identity`, `innovation`, `knowledge`, `leadership`, `learning`, `life`, `life-decisions`, `luck`, `marketing`, `meaningful-work`, `mindset`, `motivation`, `moving-on`, `passion`, `persistence`, `philosophy`, `planning`, `preparation`, `privacy`, `product`, `productivity`, `progress`, `programming`, `psychology`, `recruiting`, `relationships`, `resilience`, `satisfaction`, `simplicity`, `startups`, `stoicism`, `strategy`, `tech`, `thinking`, `time`, `time-money`, `tools`, `ux`, `vc`, `wisdom`, `work`

## Contributing

Add your own quote collections by placing new JSON files in the `references/` directory:

```json
{
  "name": "My Collection",
  "description": "A brief description",
  "quotes": [
    {
      "text": "The quote text",
      "author": "@handle",
      "url": "https://x.com/...",
      "tags": ["topic1", "topic2"]
    }
  ]
}
```

Fields:
- `text` (required): The quote text
- `author` (required): Twitter handle or attribution
- `url` (optional): Link to original tweet
- `category` (optional): Category label (e.g., "Software Engineering", "Philosophy")
- `tags` (optional): List of topic tags for filtering

## License

MIT
