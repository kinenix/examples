# Get Artbook

Reads the books of the Art category on [Books to Scrape](https://books.toscrape.com/), page by page, keeps the books rated 3 stars or more, and writes their title, rating, price, and availability to `output/Artbook.csv`.

Books to Scrape is "a demo website for web scraping purposes" whose prices and ratings are made up; Kinenix is not affiliated with it. `tests/pages` holds saved copies of two of its pages, so the flow can be tried without internet.

```bash
kinenix run extract-artbook                            # the live website
kinenix run extract-artbook --config config/test.json  # the saved pages in tests/pages
```

Written by an AI assistant from [`requirements.md`](requirements.md), following [`AGENTS.md`](AGENTS.md). Building it showed what Kinenix still lacks for paging through results; see kinenix/kinenix#191, #192, and #194.

## Configuration (`config/config.json`)

| Key | Purpose |
| :--- | :--- |
| `url` | The start page |
| `category` | The category link to open |
| `min_ratings` | The ratings to keep, as the site writes them |
| `max_pages` | The pages to read at most, as a list |
| `output_csv` | The result file |
| `headless` | `false` shows the browser window |
