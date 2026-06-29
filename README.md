# How Income Shapes 311 Complaints in New York City

## Project overview

This project explores whether income is related to how often New York City neighborhoods file 311 complaints, and whether different income groups report different kinds of problems.

Using one year of NYC 311 service request data, along with ZIP-code-level income and population data from the American Community Survey, this project asks two main questions:

1. **Does income decide how much a neighborhood complains?**
2. **Does income decide what a neighborhood complains about?**

The final story combines data analysis, maps, charts, and a scrollytelling webpage to examine how complaint patterns vary across New York City.

## Data sources

#### 1. NYC 311 service request data:

The main dataset comes from **NYC Open Data** and includes 311 service requests made between **June 1, 2025 and June 1, 2026**.

#### 2. Income data:

Income data comes from the **American Community Survey (ACS)**. For this project, I used ZIP-code-level median household income as the proxy for neighborhood wealth.

- **_The American Community Survey is an ongoing survey conducted by the United States Census Bureau. Unlike the decennial census, which aims to count everyone in the United States every 10 years, the ACS surveys a sample of households continuously and provides more detailed demographic, social, economic, and housing data._**

#### 3. Population data:

Population data also comes from the **American Community Survey (ACS)**. I used: **B01003 — Total Population** **2024 ACS 5-Year Estimates Detailed Tables**

- **\*I used **ACS 5-year estimates** instead of 1-year estimates because this project works at a smaller geographic level (zip-code). ACS 1-year estimates are more current, but they are only available for geographies with populations of 65,000 or more. ACS 5-year estimates pool 60 months of data, making them more reliable and available for smaller geographies, including neighborhood-level analysis.\***

---

## Data processing

### Handling missing ZIP codes

The original 311 complaints dataset had:

- **3,864,047 total rows**
- **33,000 rows with missing ZIP codes**

This means that about **1% of the complaints data** had missing ZIP codes.

Because the missing ZIP codes made up a small share of the dataset, and because ZIP code was necessary for merging complaints with income and population data, I excluded these rows instead of imputing ZIP codes.

### Handling unmatched ZIP codes

After removing missing ZIP codes, I checked which complaint ZIP codes could be matched with the ACS income data.

The complaint data had **2,170 complaint records (97 unmatched ZIP codes out of a total of 352 unique ZIP codes)** with ZIP codes that could not be matched with ACS income data These unmatched rows made up about **1% of the total complaint records**. The same 97 ZIP codes were also missing from the ACS population data, so these rows were excluded from the final analysis.

### Validating ZIP codes with Datawrapper

I also validated ZIP codes against the New York City ZIP boundary dataset available in Datawrapper. Records with ZIP codes outside the city’s ZIP geography were excluded from the analysis. This affected **215 unique complaints**, which was less than **0.01%** of all complaint records

### Handling missing income after merging

After merging the complaints, income, and population datasets, income was still missing for another small share of rows. These rows made up around **1% of the total records** and were also dropped from the final analysis.

---

## How income categories were created

For income categories, I used **ZIP-level income**, not complaint-level income. This was important because if I had created income categories at the complaint level, ZIP codes with more complaints would have influenced the income cutoffs more heavily. Instead, each ZIP code was treated as one unit when deciding income groups.

I divided ZIP codes into four income groups based on median household income.

The ZIP-level income cutoffs were:

```text
0.00     24086.00
0.25     74184.75
0.50     95344.50
0.75    127955.75
1.00    250000.00
```

Based on these cutoffs, the income groups were:

| Income group        | Median household income range |
| ------------------- | ----------------------------: |
| Lowest income       |             $24,086 – $74,185 |
| Lower-middle income |             $74,185 – $95,345 |
| Upper-middle income |            $95,345 – $127,956 |
| Highest income      |           $127,956 – $250,000 |

---

## Complaint categories

While analyzing complaint types, I also looked into what some broad categories actually meant in the 311 data. The details of this can be found within the analysis itself. However, after inspecting what the original 311 complaint categories referred to, I merged closely related complaint types into broader categories to make the analysis easier to interpret.

- Different kinds of noise complaints, such as residential noise, street noise, commercial noise, and vehicle noise, were grouped into a broader **noise category.**
- Complaints related to heat, hot water, water systems, plumbing, water leaks, and sewers were grouped as **drainage, water and plumbing** because many of these categories overlapped in meaning and often referred to basic building or water-related services.
- Complaints about unsanitary conditions, dirty conditions, illegal dumping, and missed collection were grouped as **dirty or unsanitary conditions**.
- Complaints about illegal parking, blocked driveways, abandoned vehicles, and derelict vehicles were grouped as **parking and vehicles**.
- Complaint types that did not fall into these broader groups were kept as separate categories.

---

## Methodology

- **Neighborhood** is approximated using **ZIP code**.
- **Wealth** is approximated using **median household income** at the ZIP-code level.
- Complaint rates are normalized using **population**, so neighborhoods can be compared more fairly.

The analysis broadly followed these steps:

1. Downloaded NYC 311 service request data for June 1, 2025 to June 1, 2026.
2. Cleaned the ZIP code field in the 311 dataset.
3. Removed rows with missing ZIP codes.
4. Removed complaint records with ZIP codes that could not be matched with ACS income or population data.
5. Validated ZIP codes against the New York City ZIP geography in Datawrapper.
6. Merged 311 complaints with ACS median household income data.
7. Merged the combined dataset with ACS population data.
8. Grouped ZIP codes into four income categories based on ZIP-level median household income.
9. Calculated complaints per 100,000 residents for each ZIP code.
10. Compared complaint rates across income groups.
11. Compared complaint categories across income groups.
12. Made a wireframe with visual references on Canva.
13. Built maps and charts for the final story using datawrapper, illustrator.

I first made the maps in Datawrapper. Datawrapper was useful for quickly creating a choropleth map, but I wanted more control over the legend and visual styling than Datawrapper allowed. Because of that, I exported the map as an SVG and edited it in Adobe Illustrator.

14. Designed the final webpage using HTML, CSS, and exported visuals.

---

## Methodological notes and limitations

- 311 complaints are not an objective measure of city conditions
- ZIP code is an imperfect definition of neighborhood. This project uses ZIP codes as a proxy for neighborhoods. This is practical because the 311, income, and population datasets can all be connected through geography.
- Income is only one measure of neighborhood wealth. This project uses median household income as a proxy for neighborhood wealth.
- Population and income are measured differently. Income is measured at the household level, using median household income. Population is measured as the total number of individuals. This means that the income variable describes households, while the denominator for complaint rates describes people. This is not perfect, but it allows complaint counts to be normalized by the number of residents in each ZIP code.

---

## What I would do next

If I had more time, I would improve the project in the following ways:

- I would spend more time designing the maps, charts, and tables so they feel more cohesive as part of one story and the color schemes work better.
- Because ZIP codes are not always intuitive, I would add more context about which neighborhoods each ZIP code roughly corresponds to.This would help readers connect the maps and charts to places they recognize.

- Build a “What does your neighborhood complain about?” tool: A useful next step would be an interactive dropdown where readers could select their ZIP code or neighborhood and see the most common 311 complaints in that area.

- Explore response times: This project focuses on complaint volume and complaint type. Another important question would be whether the city responds differently across income groups. For example, do complaints in higher-income ZIP codes get resolved faster than complaints in lower-income ZIP codes?
- Add interviews or qualitative reporting: The data can show patterns, but it cannot fully explain them. Interviews with residents, housing organizers, city officials, or 311 users could help explain why some neighborhoods report certain problems more than others.

---

## Files in this repository

├── README.md
├── index.html
├── style.css
├── coverphoto.svg
├── map1.svg
├── map2.svg
├── barchart1.svg
├── barchart2.svg
├── barchart3.svg
├── table1.svg
└── Data Files/
├── data_processing.ipynb
├── data_analysis.ipynb
├── data_viz.ipynb
└── Data Dictionaries/

```

- `index.html` contains the structure of the final webpage.
- `style.css` contains the styling for the webpage.
- The `.svg` files are the exported visuals used in the story.
- `Data Files/data_processing.ipynb` contains the data cleaning and merging process.
- `Data Files/data_analysis.ipynb` contains the main analysis.
- `Data Files/data_viz.ipynb` contains the chart and visualization work.
- `Data Files/Data Dictionaries/` contains reference files used to understand the datasets.

---

## How to view the project

Click the link in the description for the published version.

---

## Tools used

- Python
- pandas
- jupyter notebook
- excel
- Datawrapper
- Adobe Illustrator
- HTML
- CSS
- JavaScript
- NYC Open Data
- American Community Survey
- LLM

---

## Credits

Created by **Ananya Chaba** for **The Lede Program for Data Journalism, 2026**.

---

## Acknowledgements

This project was created as part of my learning process in data journalism, data visualization, and web-based storytelling.

It reflects not only the final analysis, but also the process of learning how to clean real-world data, make methodological decisions, design visuals, and communicate uncertainty clearly.

```

```

```
