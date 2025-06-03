
# Web Server Log Analysis  
**Python Take-Home Assessment | Calgary HTTP Dataset**

---

##  Overview

This project involves analyzing real-world HTTP web server logs from the University of Calgary’s Computer Science department. The dataset spans one year of access logs and is intended to test practical data analysis and Python skills.

---

##  Tools Used

- **Python 3**
- **Pandas** – Data manipulation
- **re (Regex)** – Log line parsing
- **datetime** – Time parsing and filtering
- **gzip** / **urllib** – Handling compressed data download
- **Google Colab** – Development environment

---

##  Dataset

- **Source**: [Calgary HTTP Dataset](https://ita.ee.lbl.gov/html/contrib/Calgary-HTTP.html)
- **Download URL**: `ftp://ita.ee.lbl.gov/traces/calgary_access_log.gz`
- **Format**: Apache Common Log Format (one request per line)
- **Compressed Size**: ~5.4 MB
- **Uncompressed Size**: ~52 MB

---

## Data Cleaning Steps

1. **Downloaded and decompressed** the `.gz` file using `urllib` and `gzip`.
2. **Parsed log lines** using regex to extract:
   - IP address (remotehost)
   - Timestamp
   - Request (method, file, protocol)
   - HTTP status code
   - Bytes sent
3. **Converted timestamps** to `datetime` objects.
4. **Extracted file extensions** from filenames.
5. **Handled missing/malformed data** (e.g., byte field as `-`).
6. Stored all data in a **pandas DataFrame** for further analysis.

---

##  Analysis Tasks & Results

| Question | Task | Output Type | Example |
|---------|------|-------------|---------|
| Q1 | Total log records | `int` | `214957` |
| Q2 | Unique hosts | `int` | `7611` |
| Q3 | Unique filenames per day | `dict[str, int]` | `{ '01-Jul-1995': 233, ... }` |
| Q4 | Number of 404 errors | `int` | `3982` |
| Q5 | Top 15 filenames with 404 errors | `list[tuple[str, int]]` | `[('/favicon.ico', 221), ...]` |
| Q6 | Top 15 file extensions with 404 errors | `list[tuple[str, int]]` | `[('html', 850), ('jpg', 310), ...]` |
| Q7 | Total bytes transferred per day in July 1995 | `dict[str, int]` | `{ '01-Jul-1995': 1234567, ... }` |
| Q8 | Hourly request distribution (0–23) | `dict[int, int]` | `{ 0: 456, 1: 239, ..., 23: 189 }` |
| Q9 | Top 10 most requested filenames | `list[tuple[str, int]]` | `[('/index.html', 1523), ...]` |
| Q10 | HTTP response code distribution | `dict[int, int]` | `{ 200: 150321, 404: 3982, 500: 45 }` |

---

##  Project Structure

```
calgary-http-assessment/
├── analysis.ipynb        # Notebook with all analysis & output
├── analysis.html         # Exported HTML version of notebook
├── transcript.txt        # Text transcript of code explanation video
└── README.md             # This file
```

---

##  Video Explanation

An accompanying video walks through the notebook code and results, hosted as **unlisted on YouTube**. The transcript is included in `transcript.txt`.

---

##  Notes

- All code outputs are included and reproducible.
- Assumptions made:
  - Log lines that fail to parse are ignored.
  - Bytes marked as `'-'` are treated as `0`.
- Analysis is case-insensitive where relevant (e.g., extensions).
