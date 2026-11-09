# RPA Challenge Solver

Solves the classic [RPA Challenge](https://rpachallenge.com/): it downloads the challenge's Excel file, then fills the web form ten times while the form fields move around. It also collects the people who are not programmers into a list.

The RPA Challenge is a third-party website; Kinenix is not affiliated with it. The Excel file is downloaded from the site each time the flow runs and is not part of this repository.

Needs a browser and internet access. Install the browser once with `kinenix install-browsers`.

```bash
kinenix run rpa-challenge
```

A browser window opens; set `headless` to `true` in `config/config.json` to hide it, for example on a server. When it finishes, the challenge's result message, with the success rate and the time, is saved as a screenshot in `output/screenshots/`.

## How it works

| Step | What it does |
| :--- | :--- |
| 1-2 | Downloads the challenge's Excel file into `output/` and reads it |
| 3-4 | Opens the site and starts the timer |
| 5 | For all ten rows, fills the form by its labels, which keeps working when the fields move, and adds the rows with a role other than Programmer to a list |
| 6 | Saves a screenshot of the result |
| Finally | Closes the browser, also when a step failed |

## Configuration (`config/config.json`)

| Key | Purpose |
| :--- | :--- |
| `website` | The challenge URL |
| `excel_url`, `excel_path` | Where the Excel file is downloaded from, and where it is saved |
| `screenshot_path`, `error_dir` | Result screenshot and automatic failure screenshots |
| `headless` | `true` hides the browser window |
