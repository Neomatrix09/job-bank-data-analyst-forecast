# Canada Job Bank: Data Analyst Postings Analysis and 4-Month Forecast

Do Data Analyst job postings in Canada rise or fall over time, and what should we expect over the next four months? This project combines 20 monthly Government of Canada Job Bank files (Jan 2025 to Aug 2026) into one dataset, analyses the trend, and tests simple forecasting methods with a backtest.

## Key findings

- **The early-2025 peak was mostly one repeated posting.** A single government "informatics and systems" pool title inflated early-2025 counts. I split postings into `Total` and `Other_DA` (excluding that pool title) so the trend isn't driven by one campaign.
- **Postings look flat, not trending.** Over the last 12 months (Sep 2025 to Aug 2026) the average was about 22 postings per month in total (std 6.2) and about 9 excluding the pool title (std 3.5). One spike (March 2026) came from a campaign.
- **Simple beat clever in the backtest.** Holding out the last 4 months, "repeat the last month" had the lowest error for Total (MAE 1.5) and "average of past months" for Other_DA (MAE 2.0). A fitted trend line did worst (MAE 6.4 and 7.7).
- **Forecast, Sep to Dec 2026:** about 21 postings per month in total (normal range roughly 15 to 27) and about 9 excluding the pool title (roughly 6 to 13).

## Method

1. **Load and combine:** a reusable loader handles two file formats (UTF-8 comma-separated with a column-name bug on the first column; UTF-16 tab-separated), standardises month labels, and stacks 20 files.
2. **Define "Data Analyst":** job title contains "data analyst" (case-insensitive). Adjacent roles are not merged.
3. **Trend analysis:** monthly counts, a least-squares slope, and a check on how single months (like March) influence it.
4. **Pool vs organic split:** separated the repeated government pool title from other postings.
5. **Forecast backtest:** trained on 8 of the last 12 months, predicted the held-out 4, compared three methods by mean absolute error (naive, average, linear trend).
6. **Ranges:** shown two ways, the typical backtest miss (narrow) and one standard deviation of monthly swings (wide).

## Limitations

- Single source (Job Bank only). Job Bank is not the whole market, and LinkedIn/Indeed data was not available to me.
- Small monthly counts (4 to 38), so results are exploratory, not conclusive.
- The backtest used only 4 held-out months; method rankings could change with more data.
- The forecast is a level, not a trend, by design. Campaign-driven spikes cannot be predicted.
- Salary analysis (standardised to annual, outliers removed) was an early exploration on the first 11 months and has not been rerun on all 20.
- Experience Level was about 82% missing, so it was not used.

## Tools

Python, pandas, NumPy, Matplotlib, Jupyter.

## Reproduce

1. Download the monthly Job Bank posting files from the Government of Canada's open data portal and put them in one folder (check the dataset's licence and credit it).
2. Open `DA_Job_Market_Analysis (1).ipynb`, set `data_folder` to that folder, and run the cells in order.

## Data source

Government of Canada, Job Bank open data (monthly job posting files).
