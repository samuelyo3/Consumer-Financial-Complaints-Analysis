# Consumer-Financial-Complaints-Analysis
## Introduction
In this project, I stepped into the role of a data analyst at the Consumer Financial Protection Bureau (CFPB), a U.S. government agency ensuring fairness and accountability in the financial sector. The CFPB collects complaints from consumers across the United States regarding financial products and services, tracking each complaint from submission through company response. The goal was to identify patterns in complaints, evaluate company response performance, and highlight areas of concern for regulators and consumers.
## Dataset
The dataset contains 62,516 consumer complaint records spanning multiple years (2017 - 2023) across two related tables: a complaints fact table and a company dimension table.
### Complaints Table
- Complaint ID: Unique identifier for each complaint
- Submitted via: Channel used to submit the complaint (e.g., Web, Referral, Phone)
- Date submitted: Date the consumer filed the complaint
- Date received: Date the complaint was officially recorded
- State: U.S. state of the consumer
- State Latitude / State Longitude: Geographic coordinates for map visuals
- Product: Financial product category (e.g., Mortgage, Credit Card, Debt Collection)
- Sub-product: More specific product type within each category
- Issue: General problem reported by the consumer
- Sub-issue: More detailed problem description
- Company public response: Official public statement from the company
- Company response to consumer: Resolution outcome (e.g., Closed with explanation, Closed with monetary relief)
- Timely response?: Whether the company responded within the required timeframe (Yes/No)
- Census Region: U.S. Census region of the state
- Census Division: U.S. Census division of the state
- Company Response Date: Date the company responded
- Company ID: Unique company identifier linking to the company table
- Response Time Days: Days between complaint submission and company response
### Company Table
- Company ID: Unique company identifier
- Market Share Percent: Company's share of the overall financial market
- Reputation Score: Company reputation score (50–100)
- Enforcement History: Flag for past regulatory actions (Yes/No)
- Company Size Tier: Size classification based on market share rank
- Complaint Count: Total complaints linked to the company
- Timely Response Rate: Percentage of complaints with timely responses
- Avg Response Time Days: Average days to respond across all complaints
- Complaints per 1% Share: Complaint count normalized by market share — key fairness KPI
## Tools
Microsoft Power BI
## Data Preparation and Modelling
Cleaned and standardized complaint issue and product fields, fixing duplicates and inconsistently named labels in Power Query.

Built a custom DAX date table with time intelligence columns including Year, Quarter, Month, Week, Day, and Day Type
Modelled data into a star schema connecting the complaints fact table and company dimension table via Company ID, with three date relationships (active: Date received; inactive: Date submitted and Company Response Date)

Created calculated columns and DAX measures for KPIs such as:

Total Complaints,
Timely Response Rate,
Resolution Rate,
Average Response Time,
Unresolved Complaint Rate,
Complaints per 1% Market Share.

## Exploratory Data Analysis
### Pre-Analysis Questions
The analysis was guided by the following business questions:

- When do complaints rise or fall over time?
- Which states and regions are hotspots?
- Which products and sub-products drive the most complaints?
- Which issues and sub-issues are most common?
- How fast and how timely are company responses?
- Which companies show the highest complaint rates relative to market share?
- Do company traits (size tier, reputation, enforcement history) correlate with outcomes?
- Do submission channels differ in response speed or outcomes?
## Insights
- Seasonal Complaint Patterns
Across all years, complaint volumes consistently peak during the summer months (May–August), with Managing Account issues dominating at 24% of total complaints, driven primarily by deposits, withdrawals, and ATM/card problems.
The reason? Summer vacations and increased transaction activity. People are spending more, travelling more (to Califonia, Florida,etc), and using their accounts more heavily, leading to higher account usage and, naturally, more errors and delays.
This tells a powerful story: The biggest pain point for consumers is not fraud or complex financial products; it is the day-to-day management of basic accounts.

The top sub-issues confirm this:
- Deposits & withdrawals (money not going in or out correctly)
- Debit/ATM card issues.
These are not complex financial problems, but everyday banking failures affecting ordinary people.

The second most common issue is Incorrect Information on Credit Reports (8%). Most consumers don't discover credit report errors until they apply for a loan and get rejected. Since more people apply for credit in spring and summer, more errors surface during these months.

Supporting patterns also show:
- Most complaints are submitted via digital channels like web (especially during peak travel periods).
- Complaint hotspots are concentrated in high-activity states like California, Florida, and New York, with the South region leading overall.

- 2023 Performance Deterioration
From 2017 to 2022, complaint volumes grew steadily while performance remained consistently strong. Timely response rates stayed above 99% and resolution rates held near 100%. The industry was effectively managing rising demand.
Then came 2023.
At first glance, complaints appeared to drop from 13K (2022) to 9K, but this is misleading. The 2023 data only covers January to August. To ensure a fair comparison, I conducted a like-for-like analysis of January–August across both years.
The results are alarming:
📌 Complaints increased from 8K to 9K ( 12.5% increase).
📌 Timely response rate crashed from 96.82% to 77.95% (a nearly 19 percentage point collapse in a single year).
📌 Resolution rate fell from 100% to 83.72% (meaning 1 in 6 complaints in 2023 went unresolved, compared to virtually none in 2022).
📌 Approximately 16% of 2023 complaints remain in progress.
In just one year, the system went from near-perfect performance to a significant breakdown, while simultaneously receiving more complaints. Companies are handling a higher volume worse than before. That is a compounding problem that demands regulatory attention.
- Geographic Hotspots
The South Census Region recorded the highest complaint concentration overall, with the South Atlantic division leading across all nine U.S. Census divisions. California, Texas, and Florida were the top complaint states.
- Company Performance
Analysis of 1,081 companies using the Complaints per 1% Market Share KPI revealed that company size alone does not explain poor performance. Several companies with strong reputation scores showed disproportionately high complaint rates relative to their market presence, indicating that reputation does not always reflect actual complaint handling quality.
## Recommendations
- Financial institutions should increase support staff during peak months (May–August) when ATM access, deposits, and card issues are most prevalent, and invest in fundamental service reliability.
- Banks should proactively send travel tip notifications to customers during summer to prevent card disruptions.
- Regulators should investigate the sharp 2023 deterioration in timely response and resolution rates, as companies are now managing higher complaint volumes less effectively than in prior years.
- Companies with high Complaints per 1% Market Share and enforcement history should be prioritized for closer regulatory scrutiny.
