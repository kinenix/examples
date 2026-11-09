# RPA Challenge Solver

The requirements of this example, written the way you fill in `requirements.md` in a new project (`kinenix init`). `flow.md` does what they ask; compare the two to see how each section becomes steps, settings in `config/config.json`, and error handling.

## Goal

Solve the RPA Challenge (https://rpachallenge.com/): enter all ten people from the challenge's Excel file into its web form, whose fields move to a new place after every submit, and show the result. Also list the people whose role is not Programmer, for a separate review.

## Steps

1. Open https://rpachallenge.com/.
2. Download the challenge's Excel file from the site and read it (10 people: First Name, Last Name, Company Name, Role in Company, Address, Email, Phone Number).
3. Press Start to begin the timer.
4. For each of the ten people, fill the seven fields and press Submit. Find each field by its label, not by its position, because the fields move.
5. Add every person whose role is not Programmer to a list, with the first name and the role.
6. Save a screenshot of the result message.
7. Close the browser, also when a step failed.

## Settings that must change without editing the flow

- The challenge URL
- Where the Excel file is downloaded from and saved
- Where the screenshots are saved
- Whether the browser window is shown

## Secrets

- none

## Personal or confidential data

- none (the challenge data is made up); in a real form-filling task, the names, e-mails, and phone numbers would be listed here

## Output

- `output/screenshots/result_rpachallenge.png`: the challenge's result message
- The list of people who are not programmers, in the run's variables and log

## Errors and exceptions

- If the Excel file cannot be downloaded, try twice more, then stop and say so.
- If a field cannot be found by its label, stop at that person and keep a screenshot.

## Schedule

By hand, as a demonstration and a benchmark.
