# RPA Challenge Solver
> Description: Download the RPA Challenge's Excel file, fill its web form for all ten people while the fields move, and list who is not a programmer.
> Version: 2.0.0
> Requires: kinenix>=1.0.0rc4

## Variables
- `non_programmers`: []

## Steps

### 1. Download Challenge Excel File (`http.download`)
- **url:** `${config.excel_url}`
- **target_path:** `${config.excel_path}`
- **timeout:** 60
- **max_retries:** 2
- **retry_interval:** 5

### 2. Read Challenge Excel File (`excel.read`)
- **file_path:** `${config.excel_path}`
- **clean_headers:** true
- **output_var:** `challenge_data`

### 3. Open RPA Challenge Webpage (`web.open`)
- **url:** `${config.website}`
- **headless:** `${config.headless}`
- **max_retries:** 2
- **retry_interval:** 5

### 4. Click START Button to Begin Timer (`web.click`)
- **selector:** `button:has-text('Start')`

### 5. Fill The Form For Every Person (`logic.loop`)
- **items:** `${challenge_data}`
- **item_var:** `row`
- **item_label:** ${row.First Name} ${row.Last Name}
- **Sub-steps:**
  - Fill First Name (`web.type`):
    - **label:** `First Name`
    - **text:** `${row.First Name}`
  - Fill Last Name (`web.type`):
    - **label:** `Last Name`
    - **text:** `${row.Last Name}`
  - Fill Company Name (`web.type`):
    - **label:** `Company Name`
    - **text:** `${row.Company Name}`
  - Fill Role in Company (`web.type`):
    - **label:** `Role in Company`
    - **text:** `${row.Role in Company}`
  - Fill Address (`web.type`):
    - **label:** `Address`
    - **text:** `${row.Address}`
  - Fill Email (`web.type`):
    - **label:** `Email`
    - **text:** `${row.Email}`
  - Fill Phone Number (`web.type`):
    - **label:** `Phone Number`
    - **text:** `${row.Phone Number}`
  - Submit Form Round (`web.click`):
    - **selector:** `//input[@value='Submit']`
  - Collect Non-Programmer (`logic.append`):
    - **condition:** `${row.Role in Company} != Programmer`
    - **target:** `non_programmers`
    - **item:** `{"First Name": "${row.First Name}", "Role in Company": "${row.Role in Company}"}`

### 6. Take Screenshot of Result (`web.screenshot`)
- **path:** `${config.screenshot_path}`

## Finally

### 1. Close Browser (`web.close`)
- **on_error:** continue
