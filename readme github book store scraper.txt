# 📚 automated-bookstore-scraper

An intelligent web scraping workflow built with **n8n** that fetches real-time book data, parses HTML content, and automatically identifies the best bargains based on custom logic.

## 🚀 Project Overview
This project demonstrates an automated ETL (Extract, Transform, Load) pipeline for web data. It autonomously visits a bookstore, scrapes product details, cleans the data, and filters for high-value deals.

**Key Features:**
* **Web Scraping:** Utilizes HTTP Request and HTML Extraction nodes to parse raw HTML.
* **Data Transformation:** Cleans dirty currency strings (e.g., `£17.93`) into usable numbers (Float).
* **Logic Gates:** Implements conditional logic (`IF` nodes) to filter products based on price thresholds.
* **Data Aggregation:** Splits array data into individual processable items.

## 🛠️ The Workflow
![Workflow Screenshot](path/to/your/screenshot.png) *[Upload your screenshot to the repo and link it here]*

### How It Works
1.  **Ingestion:** The workflow triggers manually and sends a `GET` request to `books.toscrape.com`.
2.  **Extraction:** Using CSS Selectors, it extracts three key arrays:
    * `book_title` (`h3 a`)
    * `book_price` (`.price_color`)
    * `stock_status` (`.instock.availability`)
3.  **Transformation (The "Split & Clean"):**
    * The **Split Out** node converts the arrays into individual book items.
    * A **Set** node uses JavaScript `parseFloat()` to convert string prices (e.g., "£51.77") into numbers (51.77).
4.  **Logic & Filtering:** An **IF** node checks: `Is price <= 20?`
5.  **Output:** The workflow generates a summary for all qualifying books: *"BARGAIN FOUND: [Title] is only [Price]"*.

## 🧩 Problem & Solution
* **Problem:** Raw web data is unstructured and "dirty" (containing symbols, whitespace, and HTML tags). Finding specific deals manually is time-consuming.
* **Solution:** This workflow standardizes the data structure, handles type conversion (String to Number), and automates the decision-making process.

## 📦 Installation & Usage
1.  **Prerequisites:** An instance of [n8n](https://n8n.io/).
2.  **Import:** Download the `workflow.json` file from this repository and import it into your n8n editor.
3.  **Run:** Click "Execute Workflow".

## 📄 License
This project is open source and available under the [MIT License](LICENSE).
