# Gubernatorial Public Financing

Contained within this GitHub repo is the supporting data work to accompany the article.

## HOGAN DATA

The primary data for this report was sourced from the Maryland Board of Elections campaign finance system, also known as MDCRIS. The MDCRIS system went through an overhaul in late 2025 and the staff of the Board of Elections has been busy populating it with data from before the overhaul, but at the time of this reporting do not have data from before 2020.

As this report contains significant data work on the campaign finances of former Governor Larry Hogan, who ran for office in 2014 and 2018, data needed to be pulled from the old system manually by board employees. Over a series of emails, employees of the board shared manually pulled CSV files with Capital News Service. These CSV files were reviewed and examined for missing data by comparing them to another source which years ago had pulled the entire bulk data from the legacy system. Upon identifying missing data and querying the state board, mistakes were rectified and the missing data accounted for.

The legacy MDCRIS system as well as the current system are both vulnerable to minimal but inevitable inaccuracies stemming from the source of these records — campaign finance disclosures — which are subject to human error. Updating the legacy system to the new MDCRIS system is also an ongoing process and bugs are still being discovered and fixed.

These CSVs were read into R and saved in the repo by the date in which they were received, under `hogan final/input/`, in folders named for the date of the email (`email_nathan_sbe_2.25.26/`, `email_nathan_sbe_4.9.26/`, `email_nathan_sbe_4.13.26/`, `email_nathan_sbe_4.14.26/`, `email_nathan_sbe_4.27.26/`, `email_nathan_sbe_4.28.26/`).

The 2.25.26 email contained `Hogan 2018 Contributions.csv` (Hogan's 2018 gubernatorial campaign). The 4.9.26 email added `Hogan Contributions_email2.csv` along with contribution files for Hogan's two general election opponents — `Brown Contributions.csv` (Anthony Brown, 2014) and `Jealous Contributions.csv` (Ben Jealous, 2018). The 4.13.26 email contained two pulls for the Hogan-Rutherford Committee to Change Maryland: `Contributions (Hogan-Rutherford Committee to Change Maryland).csv` and `Contributions (Hogan-Rutherford Committee to Change Maryland - General).csv`. The 4.14.26 email contained `Hogan Contributions (1.15.15 forward).csv`, picking up Hogan committee contributions from January 15, 2015 onward. The 4.27.26 email contained four supplemental pulls — `ContributionsList.csv`, `ContributionsList(2).csv`, `ContributionsList(3).csv`, and `ContributionsList(4).csv` — used to fill identified gaps. The 4.28.26 email contained the remaining annual and report-period filings: `Hogan 2016 Pre-Gen2.csv`, `Hogan 2016 Post-Gen.csv`, `Hogan 2016 Annual.csv`, `Hogan - Rutherford Committee to change 2016 Annual.csv`, `Hogan 2017 Annual.csv`, `Hogan 2019 Annual.csv`, `Hogan 2020 Annual.csv`, and `Hogan - Rutherford Inaugural Committee Inc. 2019.csv`.

Within `hogan final/hogan_final.Rmd` you will find a detailed breakdown of all data cleaning and transformations applied to these CSVs. The cumulative-donation graphic for Hogan's 2014 race is exported to `hogan final/hogan_2014_cumulative_flourish.csv` (the data used in Flourish) and `hogan final/hogan_2014_cumulative_donations.png` (the rendered image).

## OTHER DATA CONTAINED

Campaign finance data regarding the committees of Wes Moore and his running mate Aruna Miller were pulled from the current MDCRIS system and saved in `hogan final/input/moore_miller_mdcris_pull/`. As the current system has a download limit of 50,000 entries and Wes Moore's previous 2022 campaign was the subject of the data claim, the date field was limited to donations from before he was inaugurated in January of 2023; that pull is `wes_moore_filtered_post_innauguration.csv`. Aruna Miller's committee did not have more than 50,000 entries total, so her file — `aruna_miller.csv` — is complete as of the date the data was pulled during or soon after 2026.

Basic calculations were performed on current balances of Moore and Miller's candidate committees based on reports filed in MDCRIS; that information is contained in `hogan final/hogan_final.Rmd`.

## TIDYCENSUS

One of the graphics on the page references the populations of every Maryland county. This information was pulled using a tidycensus query (the code is in `hogan final/hogan_final.Rmd`) and written to `hogan final/md_county_pop.csv`.

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
