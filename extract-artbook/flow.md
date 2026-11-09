# Get_Artbook
> Description: Scrape books in the Art category with a rating of 3 stars or higher from Books to Scrape and save them to Artbook.csv.
> Version: 1.0.0
> Requires: kinenix>=1.0.0rc4

## Variables
- `artbooks`: []
- `open_result`: {}
- `has_more_pages`: true
- `has_next_page`: false

## Steps

### 1. Open Books Website (`web.open`)
- **url:** `${config.url}`
- **headless:** `${config.headless}`
- **timeout:** 30000
- **output_var:** `open_result`
- **max_retries:** 2
- **retry_interval:** 3
- **on_error:** continue

### 2. Report When Website Cannot Be Opened (`flow.fail`)
- **condition:** `${open_result} is empty`
- **message:** เปิดเว็บไม่ได้: ${error.message}
- **category:** technical

### 3. Open Art Category (`web.click`)
- **selector:** `.side_categories a:text-is('${config.category}')`
- **timeout:** 15000
- **max_retries:** 2
- **retry_interval:** 2

### 4. Scrape Art Books Across All Pages (`logic.loop`)
- **items:** `${config.max_pages}`
- **item_var:** `page_num`
- **item_label:** Page ${page_num}
- **Sub-steps:**
  - Process Current Page (`logic.if`):
    - **condition:** `${has_more_pages} == true`
    - **Sub-steps:**
      - Read Books On Current Page (`web.get_list`):
        - **selector:** `article.product_pod`
        - **fields:** {"title": "h3 a@title", "rating_class": "p.star-rating@class", "price": "p.price_color", "availability": "p.instock.availability"}
        - **required_fields:** ["title", "rating_class", "price", "availability"]
        - **min_rows:** 1
        - **timeout:** 15000
        - **output_var:** `page_books`
        - **max_retries:** 2
        - **retry_interval:** 2
        - **on_error:** continue
      - Filter Books By Rating (`logic.loop`):
        - **condition:** `${page_books} is not empty`
        - **items:** `${page_books}`
        - **item_var:** `book`
        - **item_label:** ${book.title}
        - **Sub-steps:**
          - Keep Book With 3 Stars Or Higher (`logic.append`):
            - **condition:** `${part(book.rating_class, ' ', 1)} in ${config.min_ratings}`
            - **target:** `artbooks`
            - **item:** {"title": "${book.title}", "rating": "${part(book.rating_class, ' ', 1)}", "price": "${book.price}", "availability": "${book.availability}"}
            - **on_error:** next_item
      - Check If Next Page Button Is Visible (`web.is_visible`):
        - **selector:** `li.next a`
        - **timeout:** 2000
        - **output_var:** `has_next_page`
        - **on_error:** continue
      - Go To Next Page (`web.click`):
        - **condition:** `${has_next_page} == true`
        - **selector:** `li.next a`
        - **timeout:** 15000
        - **max_retries:** 2
        - **retry_interval:** 2
        - **on_error:** next_item
      - Mark End Of Pages (`logic.set_variable`):
        - **condition:** `${has_next_page} != true`
        - **name:** `has_more_pages`
        - **value:** false

### 5. Write Art Books To CSV (`csv.write`)
- **file_path:** `${config.output_csv}`
- **data:** `${artbooks}`
- **columns:** ["title", "rating", "price", "availability"]
- **max_retries:** 2
- **retry_interval:** 2

## On Error

### 1. Capture Error Screenshot (`web.screenshot`)
- **path:** `output/errors/error_screenshot.png`
- **full_page:** true
- **on_error:** continue

## Finally

### 1. Close Browser (`web.close`)
- **on_error:** continue
