---
name: tweetnugget
description: A nugget of wisdom from the bird app. Pick a random inspirational tweet from curated collections.
version: 1.0.0
author: amplifier
tools:
  - bash
---

# TweetNugget

When the user asks for a quote, inspiration, or says something like "hit me with a quote" or "give me some wisdom":

## How It Works

1. Read the quote collections from `references/` directory
2. Pick a random quote
3. Return it formatted for chat

## Quote Collections

The `references/` folder contains JSON files with this structure:

```json
{
  "name": "Collection Name",
  "description": "...",
  "quotes": [
    {
      "text": "The quote text",
      "author": "@handle",
      "url": "https://x.com/...",
      "tags": ["tag1", "tag2"]
    }
  ]
}
```

Available collections:
- `swlw-tweets.json` - 37 quotes from Software Lead Weekly newsletter (Dec-Aug 2025)
- `twitter-quotes.json` - 12 curated Twitter quotes
- `stoic-quotes.json` - 6 Stoic philosophy quotes

## Step-by-Step Instructions

### Basic: Get a random quote

Run this command to pick a random quote from ALL collections:

```bash
python3 -c "
import json, random, glob, sys
quotes = []
for f in glob.glob('references/*.json'):
    try:
        with open(f) as fp:
            data = json.load(fp)
            if 'quotes' in data:
                quotes.extend(data['quotes'])
    except (json.JSONDecodeError, IOError, KeyError) as e:
        sys.stderr.write(f'Error reading {f}: {e}\\n')
if quotes:
    q = random.choice(quotes)
    print(f'\\\"{q[\"text\"]}\\\" — {q[\"author\"]}')
else:
    print('No quotes found.')
"
```

Return the output directly to the user. Do not add commentary.

### Surprise Me: Random collection, then random quote

For variety across collections, pick a random collection first, then a random quote from it:

```bash
python3 -c "
import json, random, glob, sys
files = list(glob.glob('references/*.json'))
if not files:
    print('No quote collections found.')
    sys.exit(0)
try:
    collection_file = random.choice(files)
    with open(collection_file) as fp:
        data = json.load(fp)
    if 'quotes' in data and data['quotes']:
        q = random.choice(data['quotes'])
        print(f'\\\"{q[\"text\"]}\\\" — {q[\"author\"]}')
    else:
        print(f'No quotes in {collection_file}.')
except (json.JSONDecodeError, IOError, KeyError) as e:
    sys.stderr.write(f'Error reading {collection_file}: {e}\\n')
    print('Could not load a quote.')
"
```

### Filtered: Get a quote by tag

If the user specifies a topic (e.g., "quote about AI", "something about leadership", "coding quote"), filter by tag:

```bash
python3 -c "
import json, random, glob, sys
TAG = 'ai'
quotes = []
for f in glob.glob('references/*.json'):
    try:
        with open(f) as fp:
            data = json.load(fp)
            if 'quotes' in data:
                quotes.extend(data['quotes'])
    except (json.JSONDecodeError, IOError, KeyError) as e:
        sys.stderr.write(f'Error reading {f}: {e}\\n')
        continue
filtered = [q for q in quotes if any(TAG.lower() in t.lower() for t in q.get('tags', []))]
if filtered:
    q = random.choice(filtered)
    print(f'\\\"{q[\"text\"]}\\\" — {q[\"author\"]}')
elif quotes:
    q = random.choice(quotes)
    print(f'(No quotes tagged \\\"{TAG}\\\", here is a random one:)')
    print(f'\\\"{q[\"text\"]}\\\" — {q[\"author\"]}')
else:
    print('No quotes found.')
"
```

Replace `TAG` with the user's topic. Use partial matching (e.g., "lead" matches "leadership").

### Available Tags

Common tags across collections: `action`, `advantage`, `ai`, `building`, `career`, `confidence`, `creation`, `courage`, `design`, `discipline`, `distribution`, `early-career`, `engineering`, `enough`, `explanation`, `focus`, `goals`, `happiness`, `hiring`, `humor`, `innovation`, `knowledge`, `leadership`, `learning`, `life-decisions`, `luck`, `marketing`, `meaningful-work`, `motivation`, `moving-on`, `persistence`, `philosophy`, `preparation`, `privacy`, `product`, `productivity`, `promotion`, `programming`, `recruiting`, `resilience`, `relationships`, `simplicity`, `startups`, `stoicism`, `thinking`, `time-money`, `wisdom`, `work`

## Response Format

Always return quotes in this format:

> "The quote text" — @handle

If the quote has a URL, you may optionally append it as a link. Keep responses minimal - let the quote speak for itself.

## Adding More Quotes

Users can add their own collections by placing new JSON files in the `references/` directory following the same format.
