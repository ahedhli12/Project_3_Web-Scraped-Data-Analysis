# Project 3 — From Webpages to Answers

## What is a web scraping pipeline?
A **pipeline** is a sequence of steps. In this project:

**Choose pages → download HTML → extract values → build a DataFrame → clean → calculate → plot → explain.**

A webpage is written using **HTML**. Python can read the HTML and pick out the values you need. A spreadsheet-like table in Python is a pandas **DataFrame**.

| Tool | What it does |
|---|---|
| `requests` | Downloads a webpage's HTML |
| `BeautifulSoup` | Reads HTML and finds elements such as headings or product cards |
| `pandas` | Stores records in rows and columns and calculates answers |
| `seaborn` | Creates plots from the data |
| `matplotlib.pyplot` | Formats and saves the Seaborn figure |

## 1. Understand a small HTML example
This is **invented practice HTML**, not a source for your project:

```html
<h1>Campus Shop</h1>
<div class="product">
  <h2>Notebook</h2>
  <p class="price">$4.50</p>
</div>
<div class="product">
  <h2>Pen</h2>
  <p class="price">$1.25</p>
</div>
```

- `<h1>` stores the page heading, “Campus Shop.”
- Each `<div class="product">` groups one product's information.
- `<h2>` stores that product's name.
- `<p class="price">` stores its price as **text**, including the dollar sign.
- A **class** labels a kind of element; many elements can share it. An **id** identifies a specific element and should be unique within the page.

```python
from bs4 import BeautifulSoup

# A string containing the HTML from one practice product.
html = '<div class="product"><h2>Notebook</h2><p class="price">$4.50</p></div>'
soup = BeautifulSoup(html, "html.parser")

# product is one HTML element; name and price_text are strings.
product = soup.find("div", class_="product")
name = product.find("h2").get_text(strip=True)
price_text = product.find("p", class_="price").get_text(strip=True)
print(name, price_text)
```

`find()` returns the first match. `find_all()` returns a collection of matching elements. For example, `products = soup.find_all("div", class_="product")` stores all matching product elements, not just their names. A loop can read each one. `select()` is another way to find elements with CSS selectors; `.product` means a class and `#catalog` means an id. **Your website will have its own HTML. Inspect it before choosing a selector.**

## 2. Where does the HTML come from?
For a permitted live page, the general pattern is:

```python
import requests

# Replace this placeholder with a real page after reviewing its policy.
url = "https://YOUR-CHOSEN-SITE/PAGE"
response = requests.get(url, timeout=20)
response.raise_for_status()  # Stop if the server returns an unsuccessful status.
soup = BeautifulSoup(response.content, "html.parser")
```

This snippet is a pattern; the placeholder URL will not run. A timeout prevents waiting indefinitely for an unresponsive request. If the server blocks access or the expected data is absent, investigate or select another source. Some pages add their data using JavaScript after loading, so the HTML returned by requests may not contain it.

If HTML is in a **separate local file**, read it first:

```python
# Run from the folder that contains practice.html.
with open("practice.html", "r") as file:
    html = file.read()
soup = BeautifulSoup(html, "html.parser")
```

`with` closes the file automatically after the indented block. This local-file example is a reminder from Assignment 9; Project 3 requires actual collection from at least five website pages.

## 3. Collect several pages
Create a list of five or more exact page URLs. Use a loop to request each page, extract its records, and append them to one list. Use `time.sleep(1)` between requests as a starting point, or a longer delay if the site requires it. Record the page URL with every row so you can trace a value to its source.

First test **one page**, then extend your working extraction to the other pages. Check each page's number of extracted rows. A successful HTTP response with zero matches is not a successful scrape. Avoid repeatedly collecting the same pages while editing plots: use the saved raw CSV for analysis practice.

Check robots.txt and the site's terms before collection. Document actual rules, not assumptions. Do not bypass login, CAPTCHAs, or blocks. Missing or unreadable policies mean you should investigate and choose a clearly suitable source.

## Saving and reloading your data
Follow the commented cells directly in **WebScrapingProject.ipynb**:
- **Section 5:** Save raw data and the page log as CSV files.
- **Section 6:** Reload your CSV while working on analysis.
- **Section 7:** Save a separate cleaned copy.

The notebook explains file locations, `index=False`, and checking the saved files.

## 4. Clean before calculating
For the invented shop example:

```python
import pandas as pd

# Each dictionary is one row. These are practice values, not scraped project data.
practice = pd.DataFrame([
    {"name": "Notebook", "price": "$4.50"},
    {"name": "Pen", "price": "$1.25"}
])
# Remove the dollar sign, then convert text to numeric values.
practice["price"] = pd.to_numeric(
    practice["price"].str.replace("$", "", regex=False), errors="coerce"
)
print(practice)
print("Mean practice price:", practice["price"].mean())
```

`errors="coerce"` turns values that cannot be converted into missing values. Check those missing values and explain how you handle them. Do not blindly replace missing values with zero. Check duplicates using meaningful identifying fields; the same item may legitimately appear on two pages.

## 5. Make a Seaborn plot tell a clear story
The following plot uses **invented practice data**, not an answer to your project:

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.set_theme(style="whitegrid")
fig, ax = plt.subplots(figsize=(6, 4))
# There is one row per product in this practice table.
sns.barplot(data=practice, x="name", y="price", color="steelblue",
            errorbar=None, ax=ax)
ax.set_title("Notebook costs more than Pen in the practice shop")
ax.set_xlabel("Product")
ax.set_ylabel("Price ($)")
# Put the value above each bar.
for bars in ax.containers:
    ax.bar_label(bars, fmt="%.2f", padding=3)
ax.margins(y=0.2)
fig.tight_layout()
# Save before show; use your own filenames for the required project charts.
fig.savefig("charts/practice_price.png", bbox_inches="tight")
plt.show()
```

The title states the finding. Numeric labels show the values. Styling and readable axes make comparison easier. This practice chart does **not** count toward the two project plots. Choose plots appropriate for your questions: a bar plot compares categories, a histogram shows a distribution, and a scatter plot explores two numeric variables. Use annotations appropriate to the plot rather than labeling every point in a crowded figure.

## 6. Write answers using the evidence
Weak: “There are differences.”

Better: “Category A's average price is $12.40, compared with $9.10 for Category B in the collected sample.” Only write those numbers if your code produced them.

For each of your four questions, show the calculation **and** explain the output. Two questions also need plots. Discuss what your sample can and cannot show; five pages do not necessarily represent the whole website or prove cause and effect.

## Quick troubleshooting
| Problem | First check |
|---|---|
| `ModuleNotFoundError` | Install requirements in the same Python environment selected as the kernel |
| `FileNotFoundError` | Open the repository folder; check spelling and relative paths |
| `NoneType` error | Your selector may not match; inspect the retrieved HTML |
| Empty DataFrame | Print the number of elements found on each page |
| Prices will not average | Convert price strings to numeric values and inspect conversion failures |
| Website changed | Reinspect its HTML and update your selectors; explain the change |

## References
- [Requests quickstart](https://requests.readthedocs.io/en/stable/user/quickstart/)
- [Beautiful Soup documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Seaborn barplot](https://seaborn.pydata.org/generated/seaborn.barplot.html)
