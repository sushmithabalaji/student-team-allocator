# SC1003 — Team Allocation Simulator
> A Python program that automatically forms balanced and diverse student teams based on CGPA, gender, and school affiliation.

## Team Members (FCSH)

| Name | Email |
|---|---|
| Chong Zhi Yuan Yannis | ychong054@e.ntu.edu.sg |
| Daanish Jaaved Bin Jupri | DAAN0002@e.ntu.edu.sg |
| Ammar Harith Bin Shahizan | AMMARHAR001@e.ntu.edu.sg |
| Chua Chok Yang | C250196@e.ntu.edu.sg |
| Balaji Sushmitha | BALA0057@e.ntu.edu.sg |

---

## Overview

Manually forming fair student teams is a complex task, especially at scale. This program applies **computational thinking** to automate the process systematically and objectively, considering three key factors:

- **CGPA** — Academic performance balance across teams
- **Gender** — Alternating male/female assignment for gender diversity
- **School affiliation** — Maximising the number of unique schools per team

The program reads student data from a CSV file, groups students by tutorial, forms balanced teams, and outputs the results to a new CSV file. It also includes **interactive widgets** and **visualisation charts** so users can explore results dynamically.

---

## Features

- Reads and parses student data from a `.csv` file
- Groups students by tutorial group
- Sorts students by CGPA and gender
- Forms teams using a greedy CGPA-balancing algorithm with round-robin gender alternation
- Optimises school diversity across teams via a swap-based post-processing step
- Saves final team allocations to `team_assignments.csv`
- Interactive team size selector (4–10) using `ipywidgets`
- Data visualisations using `matplotlib`:
  - Overall gender distribution (pie chart)
  - Student CGPA spread (scatter plot)
  - Average CGPA per team (scatter plot)
  - Gender composition across all teams (pie chart)
  - Distribution of school diversity per team (bar chart)

---

## Project Structure

```
ntu-team-allocator/
│
├── FCSH_Team1_ChuaChokYang.ipynb   # Main Jupyter notebook
├── records.csv                      # Input student data (required)
├── team_assignments.csv             # Output file generated on run
├── assets/                          # Flowchart images used in the notebook
│   ├── read_csv.png
│   ├── group_by_tutorial.jpg
│   ├── sort_by_cgpa.jpg
│   ├── make_teams.jpg
│   ├── school_diversity.jpg
│   ├── balance_school.jpg
│   └── make_teams_for_all_groups.jpg
└── README.md
```

---

## Input Format

The program expects a `records.csv` file in the same directory as the notebook, with the following columns:

| TutorialGroup | StudentID | School | Name | Gender | CGPA |
|---|---|---|---|---|---|
| T01 | U2400001A | SCSE | John Tan | Male | 4.5 |
| T01 | U2400002B | NBS | Sarah Lim | Female | 4.2 |

---

## How to Run

### On Google Colab
1. Upload `records.csv` and the `assets/` folder to your Colab session
2. Open the notebook and run all cells
3. Use the interactive widget at the bottom to select team size (4–10)
4. Results are saved to `team_assignments.csv`

### On Jupyter Notebook / VS Code
1. Ensure the required packages are installed:
   ```bash
   pip install ipywidgets matplotlib
   ```
2. Place `records.csv` in the same folder as the notebook
3. Run all cells in order
4. Adjust team size using the widget and click **Submit**

---

## Algorithm Summary

1. **Read & parse** — Load student records from CSV into a list of dictionaries
2. **Group** — Bucket students by tutorial group
3. **Sort** — Within each group, sort students by descending CGPA, then split into male and female sublists
4. **Form teams** — Greedily assign students to the team with the lowest total CGPA, alternating gender with each pick
5. **Balance schools** — Iteratively swap same-gender students between teams (within a CGPA tolerance of 0.2) if the swap increases school diversity
6. **Save & visualise** — Write results to CSV and render summary charts

---

## Constraints & Limitations

- **Uneven gender/school ratios** — Some tutorial groups may have imbalanced demographics; the algorithm handles this with tolerance levels, prioritising CGPA and gender balance before school diversity
- **Remainder students** — When students don't divide evenly into teams, the first few teams receive one extra member
- **File paths** — The notebook expects `records.csv` in the same working directory; missing files trigger a clear error message

---

## Technologies Used

- Python 3
- `ipywidgets` — Interactive team size widget
- `matplotlib` — Data visualisation
- `re`, `collections` — Standard library utilities

---

## Output

A file called `team_assignments.csv` is generated with the following columns:

| TutorialGroup | StudentID | School | Name | Gender | CGPA | TeamAssigned |
|---|---|---|---|---|---|---|
