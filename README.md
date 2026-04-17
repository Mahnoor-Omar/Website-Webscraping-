# Project Name: Nia Mia E-Commerce Catalog Scraper

### 1. Project Overview
* **Target Website:** [https://niamiaofficial.com](https://niamiaofficial.com)
* **Data Fields Extracted:** Product Name, Unified Price (sale or regular), Product Link, Collection Source.
* **Tools Used:** Python, Requests, BeautifulSoup4, Pandas.

### 2. Setup Instructions
1. Clone this repo: `git clone [Your Repository Link]`
2. Install dependencies: `pip install -r requirements.txt`
3. Run script: `python scraper.py`

### 3. Challenges & Solutions

* **Handling Price Ranges & Smashed Data:** One major hurdle was "Price Smashing" on Pre-Order items and items with variants, where the HTML structure caused the original and sale prices to be joined into a single long string (e.g., `3000038000`). 
    **Solution:** I implemented a specialized cleaning function that extracts the text from the price block using a space separator, splits the result, and selects the first valid numerical value. Furthermore, I added a filter to skip items labeled "(Pre-Order)" to ensure the final catalog contains only items with fixed, reliable pricing.

* **Character Encoding in Excel:** Standard CSV exports were corrupting special characters in product names (like the 'é' in Brulée).
    **Solution:** Used the `utf-8-sig` encoding during the Pandas export phase, which adds a Byte Order Mark (BOM) that forces Excel to recognize and display international characters correctly.

* **Handling Dynamic Collection Pages:** Shopify sites often use pagination that can lead to empty pages or infinite loops if not handled.
    **Solution:** Built a robust `while True` loop with a `new_found_count` tracker. If a page returns zero valid products or a non-200 status code, the script safely breaks the loop and moves to the next category.
