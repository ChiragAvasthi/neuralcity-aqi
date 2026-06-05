# NEURAL CITY: Air Quality Intelligence Layer
**Product Engineering Intern Assignment | Dashboard Enhancement**

**By:** [Chirag Avasthi](https://github.com/ChiragAvasthi)

---

## 1. Prototype Link
* **Live Prototype URL:** [https://chiragavasthi.github.io/neuralcity-aqi/](https://chiragavasthi.github.io/neuralcity-aqi/)

## 2. Public Dataset Used

| Attribute | Details |
| :--- | :--- |
| **Dataset Name** | CPCB Annual City-Level Air Quality Data (AQI) |
| **Source / Authority** | Central Pollution Control Board (CPCB), Ministry of Environment, Forest and Climate Change, Government of India |
| **Access URL** | [cpcb.nic.in](https://cpcb.nic.in/) / [app.cpcbccr.com](https://app.cpcbccr.com/) / [data.gov.in](https://data.gov.in) |
| **Pollutants Covered** | PM2.5, PM10, $NO_{2}$, $SO_{2}$, $O_{3}$, CO Annual city averages (AQI scale 0-500) |
| **Licence** | Government Open Data Licence (GODL) - freely usable for research and non-commercial applications |

## 3. Data Selection Note
> Air quality shapes urban liveability yet is absent from Neural City's current ranking. CPCB's annual AQI dataset offers city-wise PM2.5, PM10, and $NO_{2}$ data structured, public, and updated yearly. Integrating it creates a pollution-adjusted composite rank, giving citizens and municipal officers a more complete, scientifically grounded measure of true habitability.

*(Word count: exactly 50)*

## 4. Data Cleaning & Transformation
The following pipeline was applied to the raw CPCB AQI data using Python and pandas:

* **Step 1: Ingestion**
  Raw CPCB city AQI values (annual averages) were loaded into a pandas DataFrame. Missing or null values were identified and imputed using the column median for that pollutant, preserving data integrity without distorting distributions.
* **Step 2: Validation**
  All AQI values were validated against the 0-500 CPCB-defined scale. Pollutant concentrations (PM2.5, PM10, $NO_{2}$) were clipped to CPCB-defined plausible upper bounds. A monthly-vs-annual consistency check was run with a tolerance threshold of $\pm20$ AQI units to flag measurement anomalies.
* **Step 3: Derived Features**
  Five new columns were computed:
  1. **AQI Category:** Using the official 6-tier CPCB scale (Good / Satisfactory / Moderate / Poor / Very Poor / Severe).
  2. **Seasonal Swing:** Winter minus summer AQI, indicating how variable pollution is across seasons.
  3. **AQI National Rank:** Ranking of the city based on AQI values.
  4. **NAAQS PM2.5 Exceedance Flag:** A boolean value indicating whether annual PM2.5 exceeded the national standard of $40~\mu g/m^{3}$.
  5. **Composite Rank:** Combining Neural City's existing urban score (70% weight) with the city's pollution rank (30% weight).
* **Step 4: Output**
  The final cleaned and enriched DataFrame was exported as a UTF-8 CSV (`city_aqi_final.csv`) ready for direct consumption by the prototype dashboard.

## 5. Tools & Libraries Used

| Tool | Version | Purpose |
| :--- | :--- | :--- |
| **Python** | 3.11 | Core scripting language |
| **pandas** | 2.x | Data loading, cleaning, transformation |
| **NumPy** | 1.26 | Numerical clipping & validation |
| **HTML/CSS/JS** | N/A | Prototype front-end (static, GitHub Pages) |
