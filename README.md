# UrbanBotaniks → Temu pots

The scraper reads **only** `https://www.urbanbotaniks.com/category/62/saksii-i-podlozhki.html`, including its own pagination. It does not crawl parent categories, sister categories, or unrelated products. Products shown under its three subcategories are included through the parent category's 4 listing pages. The workbook keeps the original Temu template and its dropdown validations.

## Run in GitHub

1. Upload all files, including the `.github/workflows/scrape.yml` directory, into a GitHub repository.
2. Open **Actions → UrbanBotaniks to Temu → Run workflow**.
3. Download the `urbanbotaniks-temu-results` artifact. It contains the completed workbook and the `.review.json` report.

The action takes the current price in EUR, product code, title, brand, images, weight, stated origin, and stated material from each product page. It sets the Temu category to **25104 (Pots)**. The exact manufacturer value is selected from the original template's dropdown only when supported by the brand or an identifiable product mark. The EU responsible person **Shteryo Shterev** is selected only when the item's stated production country is outside the EU. If origin is missing, both origin and responsible person are left empty for review. A brand headquarters is not proof of production country.

The workflow defaults to an **assumed quantity of 100** per item shown as in stock. This is a placeholder; verify actual quantities before import. Items marked out of stock get quantity 0. Package dimensions are left blank because the site generally gives product dimensions, which need not equal shipping package dimensions. No invented manufacturer, material, weight, or origin is written. These omissions and out of stock items appear in the review report. Every item's detail page is linked in column `FV`.

To run locally: `pip install -r requirements.txt` then `python urbanbotaniks_scraper.py`. Use `--limit 2` for a sample, `--quantity N` to change the assumed stock and `--workers N` to control the load on the site. If any product page fails, the action fails but still uploads any partial workbook and report; check the `failed` list and rerun.
