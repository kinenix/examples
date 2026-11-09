# Kinenix examples

Flows that show what [Kinenix](https://github.com/kinenix/kinenix) can do with real websites and data. Each folder is a Kinenix project: `requirements.md` says what the automation must do, and `flow.md` does it.

| Example | What it does | Needs |
| :--- | :--- | :--- |
| [`extract-artbook`](extract-artbook/) | Reads the books of one category on Books to Scrape, page by page, keeps those rated 3 stars or more, and writes a CSV | Internet, or the saved pages in `tests/pages` |
| [`rpa-challenge`](rpa-challenge/) | Downloads the RPA Challenge's Excel file and fills its web form ten times while the fields move | Internet |
| [`rpa-challenge-ocr`](rpa-challenge-ocr/) | Downloads an invoice image and reads its fields with a local AI model through Ollama | Internet, Ollama |

The examples that ship with Kinenix itself, such as `hello` and `quote_requests`, run without internet: `kinenix init demo --example hello` (see [docs/examples.md](https://github.com/kinenix/kinenix/blob/main/docs/examples.md)).

## Run an example

```bash
pip install --pre "kinenix"
kinenix install-browsers
git clone https://github.com/kinenix/examples.git
cd examples
kinenix validate rpa-challenge
kinenix run rpa-challenge
```

Results are written to each example's `output/` folder.

## Websites

These examples open websites made for practicing automation. The sites belong to their owners, who are not affiliated with Kinenix, and they may change or go offline; a weekly check in this repository's Actions shows when an example stops working.

| Example | Website |
| :--- | :--- |
| `extract-artbook` | [Books to Scrape](https://books.toscrape.com/), "a demo website for web scraping purposes" |
| `rpa-challenge` | [RPA Challenge](https://rpachallenge.com/) |
| `rpa-challenge-ocr` | [Automation Challenge - OCR](https://rpachallengeocr.azurewebsites.net) |

## Add an example

1. Create the project with `kinenix init "Task name"` and move its folder here, named in lowercase with hyphens.
2. Fill in `requirements.md`, write `flow.md`, and check it with `kinenix validate <folder>`.
3. Name the website in the table above, and use only sites that allow automation.
4. Add the folder to the table at the top.

## License

Apache License 2.0, the same as Kinenix. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
