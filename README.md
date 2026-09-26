# indian-railways-ticket-waste-analyzer
Data analysis quantifying seat waste in Indian Railways and making a data - driven case for passenger ticket transfer mechanism
 ## Problem Statement
 
 As a regular Indian Railways passenger, I have personally experienced the frustration of unavailable tickets whenever I had to book       tickets on very near date to the scheduled journey date during peak season and holidays, including losing Tatkal seats mid payment due    to website traffic as these tickets are booked within 2 to 5 mins on popular routes. while simultaneously observing empty confirmed       seats on the same trains I travelled on.

 This project investigates a specific inefficiency :
 - confirmed seats that go unused because passengers who can not travel due to change in journey plans and do not cancel the tickets due   to low refunds.
 - Under IRCTC's current refund policy, late cancellations result in penalties upto 100% of fare, this creates a financial disincentive to cancel.
 - These "Ghost Occupancy" seats remain blocked while waitlisted passengers cannot board - a failure of resource allocation that affects millions of Indian Railways passenger daily. 
- even though the TTE's Handheld terminal marks this as vacant but these vacant seats create opportunities for informal allocation by on-board staff, bypassing the waitlist queue and disadvantaging legitimate passengers.
 
 This analysis quantifies the scale of this problem across 1000 journey records and makes a data-driven case for a passenger-to-passenger  ticket transfer mechanism with identity verification through existing IRCTC passenger authentication systems.
 The proposed transfer mechanism operates within existing IRCTC infrastructure — transfers are processed through the standard IRCTC        booking system with PNR verification, Aadhaar-linked passenger authentication, and existing payment gateway. No new verification system   is required.
 
 ## Proposed Solution

A passenger-to-passenger ticket transfer mechanism operating within the existing IRCTC infrastructure : 

1. Non-travelling confirmed passengers flag their ticket as transferable through the flag seat
   booking window connected to IRCTC app before chart preparation.

2. Waitlisted passengers and last-minute travellers can view and book flagged seats at full fare.

3. IRCTC automatically splits the payment:
   -Original passenger receives full fare refund 
  minus IRCTC convenience fee (₹15-₹30 + GST)
  - consistent with standard booking processing cost

4. PNR updates automatically — new passenger details replace original passenger across all systems
   including TTE handheld terminals.

This requires no new verification infrastructure as the existing Aadhaar-linked IRCTC authentication and 
UPI payment gateway handle all transactions.

## Future Scope
- Transfer window closes at last chart preparation (30 minutes before the train's scheduled departure from its originating station). 
  The natural IRCTC system checkpoint for seat allocation freeze.
- Demand signaling feature: waitlisted passengers can 
  broadcast journey requirements and raise a need ticket flag allowing original passengers to make informed transfer decisions
  

## Key Findings

* Finding 1: Average occupancy 61% and average of 28.1 available seats go unused across 1000 journeys analyzed.
* Finding 2: Average of 28 vacant seats per journey across 1000 records, with 25% of journeys having 46 or more vacant seats.
* Finding 3: Railway Employee quota shows highest average occupancy (66.6%),while Ladies quota shows lowest (54.9%),the 11.7 percentile gap suggests that quota type is the stronger predictor of occupancy and removing ladies quota from the waste analysis reflecting deliberate reservation policy, not inefficiency .
* Finding 4: Scatter analysis reveals two distinct patterns
    - Routes that has High waitlisted passengers with zero available seats ,
       are prime candidates for transfer mechanism .
    - And routes with high available seats with zero waitlist are low demand 
       routes needing different intervention.
* Finding 5: - General Quota shows highest cancellation rate (0.110) among all quota types. GN's longer 60-day 
  booking window generates more plan changes than short-window quotas like Tatkal (0.104). Tatkal 1A
  shows highest combined cancellation rate at 0.316.
* Finding 6: 1A class shows highest cancellation rate (0.270) — 2.6x higher than 2A (0.103) and 6.4x higher than GN (0.042).
* Finding 7: Rajdhani (63.6%) and Shatabdi (63.8%) show highest occupancy across train types. Duronto lowest at 56.8%.
* Finding 8: 90 journeys (9%) show simultaneous high cancellations AND waitlisted passengers — SR Zone has 17 affected journeys shows highest impact and Express train category has 32 affected journeys.

## Visualizations
- Zone-wise Average Occupancy (Bar Chart)
- Available Seats vs Waitlisted Passengers (Scatter Plot)
- Cancellation Rate by Class (Bar Chart)
- Train Type Occupancy Comparison (Bar Chart)
- Looker Studio Dashboard — [link coming soon]

## Policy Recommendation

Data analysis of 1000 journey records identifies 90 journeys 
(9%) with simultaneous high cancellations AND waitlisted 
passengers — these are prime candidates for a passenger 
ticket transfer mechanism.

Recommended pilot: SR Zone Express trains
- SR Zone shows highest impact (17 affected journeys)
- Express category has widest demographic reach 
  with 32 affected journeys across passengers belonging to all income groups
- A phased pilot approach tests system load and passenger 
  behaviour at manageable scale before national rollout

At real IRCTC scale of 14.5 lakh daily transactions, even 
conservative 5% uptake = 72,500+ seats recovered daily, 
reducing ghost occupancy and eliminating informal seat 
allocation by on-board staff.

Note: Transfer pricing should follow existing IRCTC 
convenience fee structure (₹15-₹30 + GST) — NOT dynamic 
pricing, which risks replicating exploitation patterns 
already documented in the Tatkal and Premium Tatkal systems.

## Data Sources
- Indian Railways Passenger Reservation Chart Dataset — Kaggle (synthetic, 
  modeled on real IRCTC parameters)
- IRCTC Cancellation Policy 2026 —   https://contents.irctc.co.in/en/CancellationRulesforIRCTCTrain.pdf
  https://ncr.indianrailways.gov.in/print_section.jsp?lang=0&id=0%2C1%2C283%2C363%2C444
- PIB Release Feb 2020 — 86.3% flexi fare occupancy — 
  https://www.pib.gov.in/newsite/printrelease.aspx?relid=149606&reg=48&lang=2
- Indian Railways Year Book 2023-24 — 
  https://nfr.indianrailways.gov.in/railwayboard/uploads/directorate/stat_econ/2025/IR%20Year%20Book%202023-24-English.pdf
- IRCTC Convenience Fee Structure — irctc.co.in
  https://indianrailways.gov.in/railwayboard/uploads/directorate/coaching/TAG_2023-24/Advance_reservation_Internet.pdf
- Coach capacity reference: RDSO LHB Manual —   https://rdso.indianrailways.gov.in/uploads/files/Revised_LHB_Manual_Vol_II_Chapter_I_Introduction_Draft.pdf

 ## Limitations
- Dataset is synthetic — real IRCTC granular cancellation 
  data is not publicly available
- No no-show column is present in the dataset so ghost occupancy cannot be directly 
  measured, only inferred
- 1000 rows is small sample these findings are directional not 
  statistically conclusive at national scale
- Synthetic occupancy averages 61% versus real flexi 
  fare train average of 86.3% (PIB 2020) — gap confirms 
  synthetic nature of dataset
  
## Tech Stack
Python | Pandas | Matplotlib | Seaborn | Google Colab | 
GitHub | Google Looker Studio

## How To Run
1. Clone this repository
2. Install requirements:
   pip install -r requirements.txt
3. Open notebooks/indian_railways_analysis.ipynb 
   in Google Colab or Jupyter
4. Upload indian_railway_passenger_chart.csv from 
   data/ folder when prompted
 
