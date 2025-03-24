# Property Damage Estimator: Trulia Data Analysis Tool

## Problem Statement

During a disaster, modeling and estimating forecasted damage is critical. This project enables users to input ZIP codes and retrieve detailed housing statistics such as:

- Last price sold
- Estimated values
- Bedrooms, bathrooms, square footage

The tool then computes:
- **Sum**, **Mean**, **Min**, **Max**, and **Median** values for each metric

**Focus**: NYC’s five boroughs — but easily extendable to any U.S. ZIP code on Trulia.

---

## Motivation: Navigation Shift from Zillow to Trulia

Zillow’s complex HTML made scraping infeasible, so we switched to **Trulia**, which offered a cleaner, more structured HTML. While we attached initial Zillow scraping attempts, Trulia enabled more efficient and reliable data collection.

---

## Preliminary Research: Hurricane Sandy Impact

We aimed to assess Hurricane Sandy’s effect on NYC real estate, using historical data starting Q3–Q4 2011. Surprisingly, Sandy’s market impact appeared minimal, even in flood-prone areas.

**Possible Reasons:**
- Insurance/FEMA payouts
- Trust in coastal real estate
- Resilient building codes (especially in high-rises)

The greatest impact was seen in low-rise residential areas, yet values mostly recovered within a year.

---

## Cleaning the Data

Scraped Trulia listings include price, address, and a 'qualities' field (beds, baths, square feet, studio). We:

1. Used **regex** to split qualities into separate fields
2. Converted object types to floats
3. Created a binary "studio" column
4. Assumed studios = 1 bathroom if data was missing

---

## US Zip Code Integration

Initially used `uszipcode` (https://uszipcode.readthedocs.io/) to fetch 2010 Census median values per ZIP. However, outdated data and null values led us to drop it. Still, this offered a basis for future comparison with more recent Trulia results.

---

## Implementation Details

Written as modular functions, the program lets users input ZIP codes and get instant summary stats.

### Libraries Used
- `requests`, `BeautifulSoup` for scraping
- `re`, `pandas`, `numpy` for parsing, structuring, and analysis

### Process Overview
1. Validate ZIP code input
2. Scrape and paginate through Trulia results
3. Build and clean a temp DataFrame
4. Compute summary statistics
5. Display or export results

All scraped data is discarded after use, aligning with legal and ethical standards.

---

## Data Flow Walkthrough

- Input: ZIP codes
- Output: Summary stats (mean, median, min, max, sum)
- Cleaned fields: price, bedrooms, bathrooms, square footage, studio (dummy)
- DataFrame generated per ZIP → merged → stats calculated
- Option to save as `.csv`

---

## Future Visualizations

Planned enhancements:
- Bar charts comparing ZIP code metrics
- Correlation heatmaps for feature importance (e.g., beds/baths → price)

Observations: In NYC, square footage correlated less with price vs. beds/baths.

---

## User Guide

1. Update Trulia request headers
2. Input ZIP codes
3. Run the script
4. Receive summary stats output

Even with typos or invalid ZIP codes:
- Duplicates are ignored
- Valid & invalid inputs are displayed separately

---

## Conclusions

This tool simplifies housing data aggregation to assess disaster impact by ZIP code. Use cases include:

- Estimating dollar value risk
- Identifying population exposure
- Measuring distribution skew using mean vs. median

---

## Future Development

### Short-Term Goals
- More robust Trulia scrapers with improved parsing
- Per-ZIP summary breakdowns in addition to cumulative stats

### Long-Term Goals
- Time Series from Zillow’s historical JS charts: e.g., [Zillow NYC 11224](https://www.zillow.com/new-york-ny-11224/home-values/)
- Integration with Census ACS datasets: [Census ACS](https://www.census.gov/programs-surveys/acs/data.html)

---

## Collaborators

Built at General Assembly & New Light Technologies:
- **Christopher Bratkovics** – cbratkovics@gmail.com
- **Sean Flanagan** – sflanagan94@gmail.com
- **Eric Liktiger** – elikhtiger@gmail.com
