# Gubernatorial Public Financing

Contained within this GitHub repo is the supporting data work to accompany the article.

## HOGAN DATA

The primary data for this report was sourced from the Maryland Board of Elections campaign finance system, also known as MDCRIS. The MDCRIS system went through an overhaul in late 2025 and the staff of the Board of Elections has been busy populating it with data from before the overhaul, but at the time of this reporting do not have data from before 2020.

As this report contains significant data work on the campaign finances of former Governor Larry Hogan, who ran for office in 2014 and 2018, data needed to be pulled from the old system manually by board employees. Over a series of emails, employees of the board shared manually pulled CSV files with Capital News Service. These CSV files were reviewed and examined for missing data by comparing them to another source which years ago had pulled the entire bulk data from the legacy system. Upon identifying missing data and querying the state board, mistakes were rectified and the missing data accounted for.

The legacy MDCRIS system as well as the current system are both vulnerable to minimal but inevitable inaccuracies stemming from the source of these records — campaign finance disclosures — which are subject to human error. Updating the legacy system to the new MDCRIS system is also an ongoing process and bugs are still being discovered and fixed.

These CSVs were read into R and saved in the repo by the date in which they were received. Within the RMD file you will find a detailed breakdown of all data cleaning and transformations.

## OTHER DATA CONTAINED

Campaign finance data regarding the committees of Wes Moore and his running mate Aruna Miller were pulled from the current MDCRIS system. As the current system has a download limit of 50,000 entries and Wes Moore's previous 2022 campaign was the subject of the data claim, the date field was limited to donations from before he was inaugurated in January of 2023. Aruna Miller's committee did not have more than 50,000 entries total, so her CSV file is complete as of the date the data was pulled during or soon after 2026.

Basic calculations were performed on current balances of Moore and Miller's candidate committees based on reports filed in MDCRIS; that information is contained in the RMD.

## TIDYCENSUS

One of the graphics on the page references the populations of every Maryland county. This information was pulled using a tidycensus query.

## NOT INCLUDED

Registered voters were included on the map graphic, sourced from https://elections.maryland.gov/voter_registration/stats.html.

**Candidates who ran using public financing / candidates who won:** The map includes a popup of how many candidates ran using public financing in each jurisdiction's previous election and how many are running now. Both numbers were sourced from MDCRIS (https://campaignfinance.maryland.gov/login).

Method:
1. Search Committees
2. Filter by Committee Type by Public Financing Committee
3. Filter Jurisdiction by each jurisdiction with previously ran/currently operating elections with publicly financed candidates one by one. Montgomery, Howard, and Baltimore City already had an election with their programs. Montgomery, Howard, Prince George's, Anne Arundel, and Baltimore County have candidates currently running.
4. Filter by election year for each (with the exception of Baltimore City, which was 2024, all former ones have 2022 and all current counties have 2026)
5. Ensure the "Active" filter is turned off
6. Count the total number of committees for previous elections
7. Count the total number of committees for the current election (omit terminated committees in the current one because they have dropped out or switched to traditional campaign financing)

## File Index

### `hogan final/`

- **`hogan_final.Rmd`** — Main R Markdown file containing all data cleaning, transformations, calculations, and analysis for the report.
- **`hogan_2014_cumulative_donations.png`** — Graphic showing cumulative donations for Hogan's 2014 campaign.
- **`hogan_2014_cumulative_flourish.csv`** — Cumulative donation data formatted for use in a Flourish graphic.
- **`md_county_pop.csv`** — Maryland county populations pulled via tidycensus (ACS 2024 5-year estimates), used in the county-level map graphic.

### `hogan final/input/` — Source CSVs

CSVs from the State Board of Elections, organized by the date Capital News Service received them via email from Nathan at the SBE.

#### `email_nathan_sbe_2.25.26/`
- **`Hogan 2018 Contributions.csv`** — Hogan 2018 gubernatorial campaign contributions.

#### `email_nathan_sbe_4.9.26/`
- **`Hogan Contributions_email2.csv`** — Additional Hogan contributions pull (follow-up to the 2.25 batch).
- **`Brown Contributions.csv`** — Anthony Brown 2014 gubernatorial campaign contributions (Hogan's 2014 opponent).
- **`Jealous Contributions.csv`** — Ben Jealous 2018 gubernatorial campaign contributions (Hogan's 2018 opponent).

#### `email_nathan_sbe_4.13.26/`
- **`Contributions (Hogan-Rutherford Committee to Change Maryland - General).csv`** — Contributions to the Hogan-Rutherford Committee to Change Maryland (General account).
- **`Contributions (Hogan-Rutherford Committee to Change Maryland).csv`** — Contributions to the Hogan-Rutherford Committee to Change Maryland (main account).

#### `email_nathan_sbe_4.14.26/`
- **`Hogan Contributions (1.15.15 forward).csv`** — Hogan committee contributions from January 15, 2015 onward.

#### `email_nathan_sbe_4.27.26/`
- **`ContributionsList.csv`**, **`ContributionsList(2).csv`**, **`ContributionsList(3).csv`**, **`ContributionsList(4).csv`** — Additional contribution pulls from the legacy system to fill identified gaps.

#### `email_nathan_sbe_4.28.26/`
- **`Hogan 2016 Pre-Gen2.csv`** — Hogan 2016 Pre-General report period contributions.
- **`Hogan 2016 Post-Gen.csv`** — Hogan 2016 Post-General report period contributions.
- **`Hogan 2016 Annual.csv`** — Hogan 2016 annual report contributions.
- **`Hogan - Rutherford Committee to change 2016 Annual.csv`** — Hogan-Rutherford Committee to Change Maryland 2016 annual report contributions.
- **`Hogan 2017 Annual.csv`** — Hogan 2017 annual report contributions.
- **`Hogan 2019 Annual.csv`** — Hogan 2019 annual report contributions.
- **`Hogan - Rutherford Inaugural Committee Inc. 2019.csv`** — Hogan-Rutherford Inaugural Committee Inc. 2019 contributions.
- **`Hogan 2020 Annual.csv`** — Hogan 2020 annual report contributions.

#### `moore_miller_mdcris_pull/`
- **`wes_moore_filtered_post_innauguration.csv`** — Wes Moore committee contributions pulled from current MDCRIS, date-filtered to donations before his January 2023 inauguration (due to the 50,000-row download cap).
- **`aruna_miller.csv`** — Aruna Miller committee contributions pulled from current MDCRIS (complete; under the 50,000-row cap).
