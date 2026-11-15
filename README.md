# CMP 262 — Project 3: Web-Scraped Data Analysis

**Instructor: Prof. Amjed Hedhli | Due: Module 10 | Total: 100 points**

## Objective
Build a web scraping pipeline: collect information from at least **five distinct pages on one website**, combine the records into a pandas DataFrame, check and clean the data, and answer **at least four questions** using Python. Use **Seaborn** to visualize the answers to at least two of those questions.

Assignment 9 introduced HTML, Beautiful Soup, and planning. This project carries out a complete collection and analysis. You may reuse your Assignment 9 website plan if it meets these requirements.

## Getting Started
1. Open [the starter repository](https://github.com/ahedhli12/Project_3_Web-Scraped-Data-Analysis).
2. Select **Use this template → Create a new repository** if available; otherwise select **Fork**.
3. Choose your personal GitHub account. Name your repository **LastName-FirstName-CMP262-Project03-Web-Scraping** and set it to **Public**.
4. Clone **your own repository**, then open the entire folder in Visual Studio Code.
5. Install the recommended Python and Jupyter extensions if needed.
6. Open **WebScrapingProject.ipynb** and select your Python kernel.
7. Run its import cell. **If the imports work, no installation is needed.** If a package is missing, follow the optional installation directions in notebook Section 2.
8. Read [Student-Handout.md](Student-Handout.md), then complete every notebook TODO.
9. Complete **AI-Use-Report.md**, even if you did not use AI.
10. Replace the **Student Project Summary** at the end of this README with your own project details.

**Important:** Work in your own repository. Keep the starter instructions and supporting files.

## Requirements
### 1. Choose and document your source
- Choose one website with public HTML data suitable for your questions.
- Identify at least five **different data pages**. Reloading the same page five times does not count. Pagination pages or individual item pages may count if each contributes records.
- In the notebook, record the website name, five exact URLs, collection date, fields, and four research questions.
- Review the site's robots.txt and terms/scraping policy. Record the checked URLs, date, relevant rules, and decision. A missing robots.txt is not automatic permission.
- Use a source you can access appropriately. If blocked or prohibited, choose another source. Do not bypass restrictions or collect private information.

### 2. Build the scraping pipeline
- Use **requests** to retrieve pages and **Beautiful Soup** to find and extract the HTML data.
- Inspect one page first. Explain the tags/classes/IDs you use; selectors depend on your actual website.
- Use a loop to collect records from at least five pages, with a pause between requests and a timeout.
- Track which pages succeeded and how many records each contributed. Retain a **source_url** for each record.
- Save **data/raw_data.csv** and **data/page_log.csv**. The log must show at least five successfully scraped pages with records. Report failures honestly and replace failed pages if necessary.
- A downloaded ready-made CSV or the small handout example does not fulfill the scraping requirement.

### Saving directions
The notebook includes commented, runnable saving cells: **Section 5** saves the raw data and page log, **Section 6** explains reloading your CSV, and **Section 7** saves a separate cleaned copy.

### 3. Explore and clean
- Display the dataset's size, columns, data types, missing values, and duplicate checks.
- Convert numeric or date text as needed. Explain how you handle missing values, duplicate records, and inconsistent text.
- Do not delete valid repeated observations automatically. Decide what identifies a duplicate in your dataset.
- If no cleaning is needed, show the checks and explain why.
- Save **cleaned-data/cleaned_data.csv** without a pandas index.

### 4. Answer four questions
For **each** question, include:
1. A Markdown question and explanation of your approach.
2. Python calculations with visible, clearly labeled output.
3. A short Markdown conclusion using the actual result.

At least **two different questions** must also have a **Seaborn plot**. Every required plot must have:
- A title stating the conclusion, such as “Category A has the highest average price,” supported by your results.
- Clear axis labels and units where relevant.
- Data labels or useful numeric annotations, plus readable styling.
- A saved PNG in **charts/**. Save at least **two plots**.

Matplotlib may format or save Seaborn figures, but the required plots must be created with Seaborn. Do not use hard-coded answers or unsupported claims.

### 5. Explain and verify
- Use Markdown headings to organize the notebook and explain your work.
- Comment Python code so the reader understands the important steps.
- End with an overall conclusion, limitations, and source acknowledgment.
- Update the README summary and complete the AI-use report.
- Restart the kernel, select **Run All**, fix errors, and save the notebook **with outputs**. Requests may fetch the website again; use your saved CSVs while developing analysis to avoid unnecessary traffic. The final notebook must retain a working collection pipeline.

## Repository Files
| File or folder | Purpose |
|---|---|
| `WebScrapingProject.ipynb` | Student notebook: source plan, collection, cleaning, analysis, and conclusions |
| `README.md` | Instructions, file guide, and your completed project summary |
| `Student-Handout.md` | Simple explanations and small examples |
| `RUBRIC.md` | 100-point rubric based on the supplied project rubric |
| `AI-Use-Report.md` | Your AI-use reflection |
| `requirements.txt` | Python packages needed for the project |
| `data/` | Raw scraped CSV and page collection log |
| `cleaned-data/` | Cleaned CSV used for analysis |
| `charts/` | At least two saved Seaborn plots |
| `.github/` | Friendly tutoring instructions for Copilot |
| `.vscode/` | Editor settings and recommended extensions |

The empty folders contain `.gitkeep` files so GitHub retains them. Add your own CSVs and PNGs; placeholders are not completed work.

## Rubric — 100 Points
| Criterion | Points |
|---|---:|
| Project repository located on GitHub | 10 |
| Repository contains required files | 10 |
| Analysis demonstrates acquired skills | 40 |
| Study conclusions are clearly stated | 10 |
| Plot design strategies considered | 10 |
| Analysis is organized | 10 |
| Analysis is documented | 10 |
| **Total** | **100** |

See [RUBRIC.md](RUBRIC.md) for what each category checks.

## Saving and Submitting
Your repository must contain the completed notebook with outputs, updated README, AI-use report, raw CSV, page log, cleaned CSV, and at least two chart PNGs. Keep all starter support files.

```bash
git status
git add .
git commit -m "Complete Project 3 web-scraped data analysis"
git push
```

Open GitHub and confirm the latest files and notebook outputs appear. **Submit your public GitHub repository link in Blackboard Ultra by Module 10.** Uploading to GitHub alone does not count as submitting the project.

## Student Project Summary — TODO
Complete this section without removing the assignment instructions above.
- **Student name:**
- **Project title and website:**
- **What I collected and when:**
- **My four questions:**
- **Main findings:**
- **My output files:** Explain your CSV and chart filenames if you changed them.
- **How to run my notebook:** Include any website-specific setup or limitations. Never include credentials.
