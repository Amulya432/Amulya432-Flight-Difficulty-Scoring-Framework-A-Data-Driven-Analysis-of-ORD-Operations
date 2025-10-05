# SkyHack 3.0:Flight-Difficulty-Scoring-Framework-A-Data-Driven-Analysis-of-ORD-Operations

### Team: Maverick (Amulya Bhambri, Pankaj Raidas)

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Libraries](https://img.shields.io/badge/Libraries-Pandas%20%7C%20Seaborn%20%7C%20Scikit--learn-orange.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)

### An end-to-end data analysis of United's Chicago O'Hare hub, transforming raw operational data into a predictive scoring model and actionable strategic insights.

---

## 📂 Project Structure

This repository is organized to clearly separate data, code, outputs, and documentation.

```
├── 📁 Dataset/
│   ├── 📄 Flight Level Data.csv
│   ├── 📄 Bag+Level+Data.csv
│   ├── 📄 PNR+Flight+Level+Data.csv
│   ├── 📄 PNR Remark Level Data.csv
│   └── 📄 Airports Data.csv
│
├── ├── 📓 1_EDA.ipynb
│   ├── 📓 2_FlightDifficultyScore(Deliverable2).ipynb
│   └── 📓 3_PostAnalysisAndRecommendations.ipynb
│   
│
├── 📓team_Maverick.csv
│   
|── 📁 Charts/
│   ├── 📁EDA
│   ├── 📁Flight Difficulty Score
│   ├── 📁Post Analysis
│
├── 📁 report/
│   └── 📄 Final_Presentation.pdf
│
└── 📄 README.md
```

---


---

## 🎯 The Challenge

Frontline teams at United Airlines manage the challenge of ensuring every flight departs on time. However, certain flights are more operationally demanding due to tight ground times, large passenger loads, baggage transfer complexity, and special service requests (SSRs). Identifying such high-difficulty flights currently depends on team experience and lacks a data-driven approach.

Developed for **SkyHack 3.0**, this project establishes a consistent, scalable framework to measure and rank flight difficulty using historical data from ORD operations.

---

## Analytical Workflow

The project follows a three-phase structure — from exploration to prediction to strategic recommendation.

### 1️⃣ Exploratory Data Analysis (EDA) & Visualization
Comprehensive exploration of all five datasets was conducted to understand ORD’s operational dynamics and identify data relationships influencing complexity.

**Key Observations:**
- Flights with scheduled ground time close to the **minimum turn time** faced higher delay risk.
- Departure delays peaked between **4–8 PM**, marking the busiest operational window.
- Flights with **more transfer bags** exhibited increased turnaround difficulty.

Visual analyses like scatterplots, delay histograms, and correlation maps helped uncover dependencies between flight features and delays.

---

### 2️⃣ Flight Difficulty Score Development
The core component of this project is a **daily resetting Flight Difficulty Score (FDS)** that quantifies the operational challenge for each flight.

**Feature Engineering Highlights:**
- **Ground Operations:** Ground Time Pressure (`minimum_turn_minutes / scheduled_ground_time_minutes`)
- **Passenger Load:** Load Factor, Child Ratio
- **Baggage Complexity:** Transfer Bag Ratio, Bags per Passenger
- **Aircraft Characteristics:** Widebody flag, Haul Type
- **Service Requirements:** SSR Count, Hot Transfer Bags
- **Operational Scope:** International/ Domestic indicator

**Scoring Framework:**
1. **Daily Normalization:** Each day’s flights are independently normalized using `MinMaxScaler` to maintain fairness.
2. **Weighted Aggregation:** Weighted sum across engineered features creates a composite score (1–100).
3. **Ranking & Classification:**
   - Top 20% → **Difficult**
   - Next 50% → **Medium**
   - Bottom 30% → **Easy**

**Output Example:**
| Flight | Date | Departure | Arrival | Difficulty Score | Rank | Class |
|---------|------|------------|----------|------------------|------|--------|
| UA 1899 | 2025-08-01 | ORD | YYC | 91.4 | 3 | Difficult |
| OO 5564 | 2025-08-01 | ORD | SBN | 78.3 | 22 | Medium |
| G7 4590 | 2025-08-01 | ORD | MDT | 24.8 | 112 | Easy |

---

### 3️⃣ Post-Analysis & Actionable Insights
After ranking flights, the analysis focused on identifying patterns among consistently difficult routes and deriving actionable insights.

**Findings:**
- **High-Complexity Destinations:** ORD → DEN, SFO, LAX, and LHR were consistently ranked among the most difficult flights.
- **Core Drivers:** High **transfer bag ratios**, **SSR volume**, and **tight ground time** emerged as the strongest indicators of operational strain.
- **Load Factor Influence:** Although high passenger loads contribute to complexity, baggage and SSR interactions amplify it further.

**Recommendations:**
- 🧳 **Dedicated Baggage Teams:** Assign ground staff to flights with high transfer or connecting baggage volumes.
- 🧍‍♀️ **SSR Pre-Boarding Prep:** Deploy early customer support for high-SSR flights.
- ⏱️ **Dynamic Scheduling:** Prioritize crew or gate reallocation for flights flagged “Difficult” in real time.

---

## 🧠 Project Impact

- Created a **data-backed scoring mechanism** that objectively ranks flight complexity daily.
- Enabled **data transparency** in identifying high-risk operational zones.
- Provided **directly actionable insights** that can guide workforce and turnaround planning at ORD.

---
## 🛠️ How to Use This Repository

#### Prerequisites
-   Python 3.8+
-   Jupyter Notebook or any Python IDE
-   Required libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`

#### Setup & Execution
1.  **Clone the repository:**
    ```bash
    git clone [your-repository-url]
    cd [repository-name]
    ```

2.  **Install dependencies:**
    *(It is recommended to create a `requirements.txt` file by running `pip freeze > requirements.txt` in your terminal).*
    ```bash
    pip install -r requirements.txt
    ```

3.  **Run the analysis:**
    Execute the Jupyter Notebooks in the `/code` directory in numerical order:
    -   `1_EDA.ipynb`: To explore the data and see the initial charts.
    -   `2_FlightDifficultyScore(Deliverable2).ipynb`: To run the full pipeline and generate the final submission file.
    -   `3_PostAnalysisAndRecommendations.ipynb`: To analyze the results and generate the final insights.

The primary output, **`test_Maverick.csv`**, will be generated in the `/output` folder upon running the second notebook.
