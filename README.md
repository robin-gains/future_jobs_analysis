# Future Jobs Dataset — SQL Analysis

Exploratory data analysis of a synthetic **10,000-row future job postings dataset** using Python, pandas, and SQLite. The notebook loads the data, runs a series of SQL queries to extract business insights, and presents the results as clean DataFrames.

---

## Dataset

**File:** `future_jobs_dataset.csv`

| Column | Type | Description |
|---|---|---|
| `job_id` | int | Unique identifier for each job posting |
| `job_title` | string | Role title (e.g. AI Engineer, Quantum Researcher) |
| `industry` | string | Sector: AI, Blockchain, Green Tech, Quantum Computing |
| `location` | string | City: Berlin, Dubai, London, New York, Singapore, Tokyo |
| `salary_usd` | int | Annual salary in USD |
| `skills_required` | string | Comma-separated list of required skills |
| `remote_option` | string | Whether the role is remote-eligible (`Yes` / `No`) |
| `company_size` | string | Small, Medium, or Large |
| `posting_date` | string | Date the job was posted (YYYY-MM-DD) |

- **Rows:** 10,000
- **Missing values:** None
- **Salary range:** $50,013 – $249,990

---

## Requirements

```
pandas
numpy
scikit-learn
seaborn
matplotlib
ipython-sql
sqlite3  # standard library
```

Install dependencies:

```bash
pip install pandas numpy scikit-learn seaborn matplotlib ipython-sql
```

---

## How to Run

1. Clone the repository and place `future_jobs_dataset.csv` in the same directory as the notebook.
2. Open `future_jobs.ipynb` in Jupyter.
3. Run all cells top to bottom.

The notebook creates an in-memory SQLite database (`new_sql_db`) and loads the CSV into a `jobs` table automatically.

---

## Analysis Performed

### 1. Data Overview
- Load CSV with `pd.read_csv`
- Inspect with `.head()`, `.dtypes`, and `.isnull().sum()`
- Confirm no missing values across all 9 columns

### 2. Database Setup
- Load data into a local SQLite database using `df.to_sql`
- All subsequent analysis runs via `pd.read_sql` queries

### 3. SQL Queries & Key Findings

#### Distinct Job Titles
9 unique roles identified: Quantum Researcher, Renewable Energy Engineer, Sustainability Analyst, Smart Contract Engineer, Quantum Software Developer, Blockchain Developer, AI Engineer, Data Scientist, ML Researcher.

#### Total Jobs per City
Jobs are distributed fairly evenly across all 6 cities (~1,640–1,689 postings each), with New York having the most (1,689) and Berlin the fewest (1,640).

#### Average Salary by Industry
All four industries show similar average salaries (~$149K–$151K USD):

| Industry | Avg Salary (USD) |
|---|---|
| Quantum Computing | $151,130 |
| AI | $150,672 |
| Blockchain | $149,384 |
| Green Tech | $149,330 |

#### Average Salary by Job Title (ranked)
Quantum Software Developer and ML Researcher lead with ~$151,500 and ~$151,285 respectively. Renewable Energy Engineer sits at the bottom (~$147,689).

#### Salary Range by Industry and Job Title
Every industry and role spans nearly the full salary range ($50K–$250K), indicating that experience, location, and company size matter more than the specific role or sector.

#### Remote vs. On-site Salary Gap
Minimal difference overall: on-site roles average $150,469 vs. remote $149,805. However, at the per-role level some titles (e.g. Data Scientist, AI Engineer) pay notably more on-site, while others (e.g. Quantum Software Developer, ML Researcher) pay more remotely.

#### Highest-Paid City per Location
New York tops the list with a maximum recorded salary of $249,990.

#### Industry Distribution by City
Jobs across all four industries are spread fairly evenly across all six cities. London leads in Quantum Computing postings (444 jobs).

#### Top 10 In-Demand Skills by Average Salary
Skills are ranked by average salary of associated roles:

| Rank | Skill | Demand Count | Avg Salary |
|---|---|---|---|
| 1 | Qiskit | 1,682 | $152,261 |
| 2 | Python | 1,657 | $151,655 |
| 3 | Quantum Algorithms | 1,690 | $150,687 |
| 4 | Linear Algebra | 1,666 | $150,439 |
| 5 | PyTorch | 1,637 | $150,204 |
| 6 | TensorFlow | 1,690 | $150,162 |
| 7 | Rust | 1,646 | $149,623 |
| 8 | Solidity | 1,669 | $149,483 |
| 9 | Energy Modeling | 2,490 | $149,330 |
| 10 | Climate Data Analysis | 2,490 | $149,330 |

---

## Project Structure

```
.
├── future_jobs.ipynb          # Main analysis notebook
├── future_jobs_dataset.csv    # Source dataset (required)
└── README.md                  # This file
```

---

## Notes

- The SQLite database is created in-memory (file `new_sql_db`) and is not committed to the repository.
- The `skills_required` column contains comma-separated values; the skills analysis uses SQLite's `json_each` function to unnest them per row.
- An unused `load_diabetes` import from scikit-learn is present in the notebook but not used in the analysis.
