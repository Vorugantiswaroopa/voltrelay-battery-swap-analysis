VoltRelay Battery-Swap Analytics

Analysis of a synthetic battery-swapping network for electric two- and three-wheelers: about 3.9 million swap events across six Indian cities (Bengaluru, Delhi NCR, Hyderabad, Pune, Mumbai, Jaipur), January 2024 to June 2025. Built for the Gradient Learnings hackathon.

The project cleans nine planted data-quality issues, then answers six business questions: trends, service failures, stations and geography, batteries and equipment, pricing and partners, and new-rider retention.

Headline findings
Failures are seasonal and heat-driven, not rising with growth. The failure rate is 3.8–4.0% in every month outside April to June, while completed swaps tripled (103,508 to 303,196 a month). It spikes to 10–12% in the hot season.
Gen1 chargers are the problem. Gen1 fails at 6.80% overall against 4.4% for Gen2 and Gen3. Above 40°C it is 19.0% (Gen2 9.4%, Gen3 5.5%); below 35°C all three are about 4%. Gen1 stations have no charged battery in 69% of hours above 40°C, because charge time doubles from 88 to 174 minutes.
Peak/off-peak pricing is a revenue lever, not a demand shifter. A difference-in-differences test (Bengaluru and Pune versus four control cities) shows about +₹7.3 margin per independent swap before battery wear, but only about 2.5 percentage points of swaps moved out of peak hours. Partners who were never billed the surcharge did not change, which supports price as the cause.
Three Kyron battery lots are defective. Lots KY-2407, KY-2408 and KY-2409 lose 9.65 health points per 100 swaps against about 3.0 for other suppliers. This holds in hot and cool cities alike, so heat does not explain it. Estimated extra wear: ₹434.7 lakh.
The largest partner is not the most valuable. ZipDrop is 15.3% of swaps but 9.7% of margin, and its margin per swap fell after its discount rose from 12% to 28%.
A bad first month drives new riders away. Riders with three or more failed attempts in their first week lapsed at 57.2% against 39.1% with none, and the effect holds after controlling for rider activity.

The full write-up, with recommendations (Now / Next / Later), a budget decision across the four proposals and limitations, is in the report.

Repository contents
File	What it is
one_cleaning.ipynb	The full analysis: loading, cleaning, Q1 to Q6 and chart code
charts/	Saved figures used in the report
report.pdf	The written report
.gitignore	Keeps the large data files out of the repo
Data cleaning summary
Issue	Decision
Test stations (STN-TST-01/02): 62,031 swap rows	Dropped
Firmware clock bug (v3.2.0, 10 Mar to 14 Apr 2025): 139,490 events	Shifted +5:30, verified against unaffected stations
21 city spellings for 6 cities	Mapped to six cities, 0 unmatched
15,287 invalid distance readings; 9,684 SoH/SoC values above 100%	Distances set to missing; SoH/SoC capped at 100
Telemetry gaps (poor-connectivity stations only 89.1% ok)	Kept as missing; telemetry-ok rows only for stockout and temperature metrics
Near-duplicate offline-batch events	Strict test found none; nothing dropped
Event types	All attempts for failure rates; completed swaps only for revenue, margin and battery metrics
CSAT and ticket category	Treated as unreliable; not used as headline evidence
How to run

The data are not included, because of their size and the hackathon's terms. To reproduce the analysis:

Put these files in the same folder as the notebook: swap_events.csv, stations.csv, riders.csv, batteries.csv, support_tickets.csv, city_daily_context.csv, fleet_partners.csv and station_hourly_status.csv.
Install the requirements:
pip install pandas numpy matplotlib scikit-learn jupyter
Open one_cleaning.ipynb and run the cells from top to bottom. Loading 3.8 million rows needs several GB of RAM.
Limitations
The data are synthetic and observational, so findings show association and effect sizes, not proof of cause (the pricing pilot is the exception, using a control group).
Margin is before battery wear, so it overstates profitability.
Retention uses several definitions (lapsed, no-return, low-use), and rider activity partly confounds failure exposure.
The pricing result covers Bengaluru and Pune over a 3-month baseline and 6-month window, with the hot season excluded on purpose.
The link between the weak Kyron lots and swap failures, and the effect of the surcharge on churn, were not tested.
Team
Your name: Voruganti Jyothi Swaroopa
Contributor's name: Pushkar Dutta
