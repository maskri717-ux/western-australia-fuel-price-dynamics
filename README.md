# Western Australia Fuel Price Dynamics

A descriptive analysis of unleaded petrol prices across Western Australia using FuelWatch records. The project explores how prices change over time, differ across regions and brands, and vary between individual stations.

**[Read the full report](fuel_price_analysis.html)** | [View the Quarto source](fuel_price_analysis.qmd)

Download the HTML file and open it in a browser to view the rendered report.

## Analytical question

How do unleaded petrol prices vary across Western Australia, and what patterns distinguish regions, brands, time periods, and petrol stations?

## Dataset

- **Source:** FuelWatch monthly retail-price files.
- **Period:** 1 October 2024 to 30 September 2025.
- **Scope:** Unleaded petrol (`ULP`), with prices in cents per litre.
- **Coverage:** 264,035 usable station-day records across 365 dates and 823 station proxies. A proxy combines trading name, region, and area.
- **Complete panel:** 613 station proxies observed on every study date, used for station, regional, brand, and clustering comparisons.

Obtain the twelve monthly files for October 2024 through September 2025 from [FuelWatch historical prices](https://www.fuelwatch.wa.gov.au/retail/historic). The download pattern recorded in the original project is:

```text
https://warsydprdstafuelwatch.blob.core.windows.net/historical-reports/FuelWatchRetail-MM-YYYY.csv
```

Use months `10-2024`, `11-2024`, `12-2024`, and `01-2025` through `09-2025`, and save the files unchanged in `data/raw/`. CSV redistribution permission has not been established from the project materials; obtain the source files directly from FuelWatch. Raw FuelWatch CSV files are intentionally not included in the public repository, in accordance with the course instructions.

## Key findings

- **Timing matters locally.** Metro and Peel had their lowest weekday averages on Tuesday and highest on Wednesday, with gaps of 31.3 and 28.6 cents/L respectively. Other regions showed much smaller weekday differences.
- **Regional averages describe different price environments.** Among complete stations, Metro averaged 173.8 cents/L and Kimberley 222.2 cents/L. These comparisons cover different sample sizes and do not explain the causes of the differences.
- **Brand comparisons need local context.** BP averaged below its regional benchmark in Gascoyne and Goldfields-Esperance, but above it in Kimberley. A statewide brand ranking would obscure those differences.
- **High prices do not necessarily mean high variability.** Three descriptive clusters separated 305 higher-variability stations, 30 high-price stations with low variability, and 278 stations with lower prices and lower variability.

## Methodology

1. Combine twelve monthly files, select ULP records, and check dates, prices, missing identifiers, duplicates, and conflicting station-date records.
2. Audit regional coverage, then calculate daily, monthly, and regional weekday averages.
3. Compare fully observed stations over common dates and assess brands against their regional averages.
4. Summarize stations using mean price and daily price standard deviation.
5. Standardize both features and apply k-means clustering. Compare two to five groups using average silhouette width; three groups scored highest at 0.608.

## Tools

R, tidyverse, lubridate, knitr, Quarto, k-means clustering, and the cluster package for silhouette assessment.

## Important limitations

- Station proxies are not verified physical outlets. Multiple trading names occur at 85 address combinations, so renamed stations may be split or excluded from the complete panel.
- Requiring complete coverage can change the regional and brand mix. Statewide averages also give more influence to regions with more reporting stations.
- Posted prices are not purchase-weighted and cannot establish household spending, sales, margins, or profits.
- Regional and brand differences do not establish causes. Clusters summarize price level and variability, not retailer strategies or the timing of price movements.
- Findings describe this study period. Cluster stability across other samples or periods has not been tested.

## Project structure

Main project files:

```text
western-australia-fuel-price-dynamics/
|-- README.md                   Project summary and course notice
|-- INSTRUCTIONS.md             Original course instructions (unchanged)
|-- .gitignore                  Publication exclusions
|-- fuel_price_analysis.qmd     Portfolio analysis and narrative
|-- fuel_price_analysis.html    Rendered full report
|-- fuel_portfolio.css          Portfolio styling
`-- data/
    `-- raw/                    Locally acquired monthly CSVs (not published)
```

To reproduce the report, install R, Quarto, and the R packages `tidyverse`, `lubridate`, `knitr`, and `cluster`. Keep the monthly files in `data/raw/` with names such as `FuelWatchRetail-10-2024.csv`, then run from the project folder:

```sh
quarto render fuel_price_analysis.qmd
```

## Course attribution and portfolio adaptation

Jan Lorenz created the original course project and instructional framework for Data Science Concepts and Tools. This repository is Meriam El Askri's portfolio adaptation. The analysis, interpretation, presentation, and portfolio report were developed as part of her work based on that course project; they build on its guidance rather than representing a wholly independent project framework.

The original [course instructions](INSTRUCTIONS.md) are included unchanged.

The complete original course notice follows, with its wording and example declarations preserved unchanged.

## License and Academic Integrity Notice

I encouage usage and adaptations of this by anyone. I encourge students
of me to build a data science portfolio and this Homework Projekt can be
part of it.

The intention of this license is to

1.  ensure that students do not accidentially or purposeful hide away
    that a large part of the work is guided by the instructions. Even
    when the instructions are open, the work you did can show mastery of
    skills.
2.  help students to be transparent about what their own original work
    is.
3.  alert future students to not blindly copy from public work of others
    to ensure learning and avoid breaching academic integrity policies.

When you worked through this project, you can keep it in its finished
form as a public repository in your portfolio or publish the HTML from
the repository, when you keep the *License and Academic Integrity* part
in the README and the INSTRUCTIONS in the repository.

### Original Work Declaration

You can replace the content of the section *Information* above by a
statement like:

*I, \[Your Name\], worked through this project using the
[INSTRUCTIONS](INSTRUCTIONS.md) in my own way. Beyond the concrete
instructions I did original work: \[…\]*

### Usage Terms for a finished project for future students

This code is made available for educational reference only. Students
currently enrolled in similar courses having this as a Homework project
must respect: - Do NOT copy code blindly for their own homework. Follow
your instructions and do it yourself. - There is nothing wrong reading
this. - Be aware that this project may differ from current assignments,
and blindly copying code not fitting to your instructions can serve as
evidence for plagiarism. - Follow your institution’s **academic
integrity policy**!

### For teachers

Feel free to use this project in your own teaching. If you modify it,
please change the first line somehow like:

*This repository is a Data Science Homework Project made by \[YOUR
NAME\] based on \[LINK TO THIS REPOSITORY\].*

The main purpose is that it does not look that I am responsible for your
version.

I am happy to hear about your usage and modifications if you like to
notify me.
