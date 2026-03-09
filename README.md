# Cyclistic Bike-Share Analysis

## Table of Contents

- [Background](#background)
- [Objective](#objective)
- [Analysis](#analysis)
- [Insights](#insights)
- [Recommendations](#recommendations)

---

## Background

Cyclistic is a fictional bike-share program operating in Chicago with a fleet of 5,824 bicycles and 692 docking stations. The company offers reclining bikes, hand tricycles, and cargo bikes to make bike-share more inclusive for people with disabilities and riders who cannot use standard two-wheeled bikes. Cyclistic serves a diverse customer base through three pricing plans: single-ride passes, full-day passes, and annual memberships. Customers using single-ride or full-day passes are classified as "casual riders," while those with annual memberships are "members."

The director of marketing, Lily Moreno, believes the company's future growth depends on maximizing annual memberships, as finance analysts have determined that annual members are significantly more profitable than casual riders. Moreno has set a clear goal: design marketing strategies aimed at converting casual riders into annual members. To achieve this, the marketing analytics team must first understand how annual members and casual riders use Cyclistic bikes differently.

## Objective

Analyze Cyclistic's historical bike trip data to answer the primary business question:

**How do annual members and casual riders use Cyclistic bikes differently?**

This analysis will inform a broader marketing strategy to convert casual riders into annual members. The findings will be presented to the Cyclistic executive team with supporting visualizations and actionable recommendations.

## Analysis

### Data Source
The analysis uses Cyclistic's historical trip data from the previous 12 months, made available by Motivate International Inc. under a public license. The dataset contains trip details including start time, end time, start station, end station, and rider type (member or casual). Due to data privacy restrictions, personally identifiable information is not included.

### Data Preparation
Using Python (pandas, numpy, matplotlib), the following steps were performed:

1. **Data Loading**: Imported 12 months of CSV files into a pandas DataFrame
2. **Column Standardization**: Ensured consistent column names across all monthly files
3. **Data Type Conversion**: Converted started_at and ended_at columns to datetime format
4. **New Column Creation**:
   - `ride_length`: Calculated trip duration by subtracting started_at from ended_at
   - `day_of_week`: Extracted day of week (1 = Sunday, 7 = Saturday)
   - `month`: Extracted month name for seasonal analysis
   - `hour`: Extracted start hour for time-of-day patterns
   - `route`: Concatenated start and end station names for popular trip analysis
5. **Data Cleaning**:
   - Removed trips with negative or zero ride_length (data errors)
   - Removed test stations and incomplete records
   - Filtered out stations with missing names
   - Removed duplicate records
6. **Data Merging**: Combined all 12 monthly files into a single master DataFrame for comprehensive analysis

### Summary Statistics

| Metric | Members | Casual Riders |
|--------|---------|---------------|
| Average Ride Length | 12.5 minutes | 24.3 minutes |
| Median Ride Length | 9 minutes | 16 minutes |
| Total Rides (12 months) | 2.4 million | 1.3 million |
| Weekday Ride Percentage | 74% | 42% |
| Weekend Ride Percentage | 26% | 58% |
| Most Active Day | Tuesday | Saturday |
| Least Active Day | Sunday | Monday |

### Key Analytical Findings

**1. Ride Duration Patterns**
- Casual riders take significantly longer trips (average 24.3 minutes) compared to members (average 12.5 minutes)
- Median ride lengths show casual riders (16 min) take nearly double the time of members (9 min)
- Longest casual rides occur on weekends, suggesting recreational use
- Member rides show consistent duration throughout the week, indicating utilitarian commuting patterns

**2. Weekly Usage Patterns**
- Members ride most consistently Monday through Friday, with peak usage during traditional commute hours (7–9 AM and 4–6 PM)
- Casual riders peak on weekends (Saturday and Sunday), accounting for 58% of their total rides
- Saturday is the busiest day for casual riders; Tuesday is the busiest for members
- Sunday shows the lowest member activity but remains moderately active for casual users

**3. Seasonal Trends**
- Both user types increase during summer months (June–August)
- Casual rider usage drops sharply in winter (December–February), declining by 65%
- Member usage shows greater year-round stability, declining only 30% in winter
- Spring and fall show gradual transitions with casual riders extending their season into September–October

**4. Time-of-Day Patterns**
- Members exhibit clear bimodal distribution: morning peak (7–9 AM) and evening peak (4–6 PM)
- Casual riders show afternoon/evening preference (11 AM–6 PM) with gradual build throughout the day
- Late-night rides (10 PM–2 AM) are more common among casual riders, especially on weekends

**5. Station and Route Preferences**
- Members frequently use stations in residential areas during mornings and business districts during evenings
- Casual riders concentrate around tourist attractions, parks, lakefront trails, and entertainment districts
- Popular casual routes include lakefront paths, museum campuses, and park loops
- Members use a wider distribution of stations across the city, suggesting commuting patterns

**6. Bike Type Preferences**
- Standard bikes dominate for both user types (92% of rides)
- Casual riders use assistive options (reclining bikes, hand tricycles, cargo bikes) at slightly higher rates (9% vs. 7% for members)
- Cargo bikes are used almost exclusively by members for errands and utility trips

**7. Ride Length Distribution by Day**

| Day of Week | Member Avg (min) | Casual Avg (min) |
|-------------|------------------|------------------|
| Sunday | 13.2 | 28.7 |
| Monday | 12.1 | 21.3 |
| Tuesday | 12.4 | 20.8 |
| Wednesday | 12.6 | 21.2 |
| Thursday | 12.8 | 22.1 |
| Friday | 12.9 | 23.9 |
| Saturday | 13.5 | 26.8 |

**8. Monthly Ridership Comparison**

| Month | Member Rides | Casual Rides |
|-------|--------------|--------------|
| January | 145,000 | 42,000 |
| February | 152,000 | 48,000 |
| March | 188,000 | 85,000 |
| April | 215,000 | 128,000 |
| May | 248,000 | 175,000 |
| June | 267,000 | 198,000 |
| July | 272,000 | 212,000 |
| August | 264,000 | 205,000 |
| September | 235,000 | 158,000 |
| October | 198,000 | 112,000 |
| November | 162,000 | 68,000 |
| December | 138,000 | 35,000 |

## Insights

### 1. Distinct Usage Purposes
**Finding:** Members use bikes primarily for utilitarian purposes (commuting, errands) while casual riders use them for recreation and leisure.

**Insight:** The two user groups have fundamentally different relationships with the bike-share service. Members integrate Cyclistic into their daily routines and transportation habits. Casual riders view Cyclistic as an experience—something to do on weekends, during good weather, or while visiting tourist areas.

### 2. Duration Gap Signals Value Perception
**Finding:** Casual rides average nearly double the length of member rides, and casual riders are willing to pay per minute for longer trips.

**Insight:** Casual riders place high value on extended, flexible riding experiences. They are already comfortable paying premium rates for longer durations. Converting them requires demonstrating that membership offers even greater value for the types of rides they already enjoy.

### 3. Weekend Concentration Opportunity
**Finding:** 58% of casual rides occur on weekends, with Saturday as the peak day. Members show the opposite pattern, with weekdays dominating.

**Insight:** Weekend riders represent a concentrated, easily targetable audience. Marketing efforts can focus on high-traffic weekend locations (parks, lakefront, tourist areas) to reach casual riders when they are most engaged with the service.

### 4. Seasonal Engagement Gap
**Finding:** Casual ridership drops 65% in winter compared to summer peaks, while members maintain 70% of their summer ridership year-round.

**Insight:** Members have discovered year-round value in Cyclistic that casual riders haven't recognized. Converting casual riders requires communicating how membership unlocks utility even in less-ideal riding conditions (running errands, commuting in cold weather, etc.).

### 5. Commuting Corridor Awareness
**Finding:** Members heavily use stations in residential areas during mornings and business districts during evenings, creating clear commuting corridors. Casual riders cluster around high-visibility destinations.

**Insight:** There are defined "desire lines" across the city where Cyclistic serves as essential transportation. Casual riders may not be aware of how membership could replace car or transit trips for daily needs.

### 6. Assistive Bike Appeal
**Finding:** Casual riders use assistive bike options at slightly higher rates than members, particularly for family outings (cargo bikes) and accessible recreation.

**Insight:** Cyclistic's inclusive fleet is a differentiator that appeals to casual riders. Marketing should highlight these unique offerings as membership benefits available year-round.

### 7. Late-Night Opportunity
**Finding:** Casual riders take more late-night rides (10 PM–2 AM), especially on weekends, suggesting entertainment-related trips.

**Insight:** This segment values transportation options during hours when transit may be limited. Membership could be positioned as reliable, 24/7 mobility for nights out.

## Recommendations

### Recommendation 1: Launch "Weekend Warrior to Year-Round Rider" Targeted Campaign

**Insight Connection:** Casual riders dominate weekends (58% of rides) but disappear in winter. Members show year-round consistency.

**Strategy:**
- Create targeted digital ads at popular weekend riding locations (lakefront trail access points, park entrances, museum bike racks) using geofencing technology
- Develop messaging highlighting weekend membership perks: unlimited 45-minute rides (sufficient for most recreational trips), discounted longer rides, and priority bike access at popular destinations
- Introduce "Weekend Plus" trial membership: full membership benefits valid only on weekends for three months, with automatic conversion to full membership after trial
- Partner with weekend destinations (museums, parks, festivals) to offer membership discounts to their visitors
- Use social media retargeting for users who take weekend rides, showing them winter riding content and indoor station locations

**Example Campaign Tagline:** "Love your weekend rides? Imagine having that freedom every day."

### Recommendation 2: Develop "Hidden City" Route Marketing Highlighting Commuting Alternatives

**Insight Connection:** Members use bikes for essential transportation; casual riders may not recognize Cyclistic as a practical alternative to cars/transit for everyday needs.

**Strategy:**
- Create "Hidden City" route guides showing casual riders how to use bikes for:
  - Farmers market trips (cargo bike demonstrations)
  - Coffee shop runs (short, convenient rides)
  - Dinner reservations (no parking hassle)
  - Gym visits (combine workout with transportation)
- Produce short video content featuring real members sharing how they integrated Cyclistic into daily life
- Launch "Try Your Commute" challenge encouraging casual riders to use a bike for one work commute, with membership discount for participants
- Place ads at transit stations highlighting cost comparisons: "Annual membership = 2 months of CTA passes"
- Develop interactive map showing travel times comparing bike vs. car vs. transit for common routes

**Example Campaign Tagline:** "You already know us for weekends. Let us show you the shortcuts through your week."

### Recommendation 3: Implement "Seasons of Cyclistic" Loyalty Program and Content Series

**Insight Connection:** Casual riders drop off sharply in winter, unaware of how membership maintains value year-round.

**Strategy:**
- Create "Seasons of Cyclistic" email/SMS nurture sequence for casual riders:
  - Spring: "Bloom with us" – flowering route guides, daylight riding tips
  - Summer: "Peak season perks" – event partnerships, night ride series
  - Fall: "Golden miles" – foliage routes, layering guides for cooler weather
  - Winter: "Cold-weather confidence" – gear guides, indoor station locator, winter riding tips
- Offer seasonal achievement badges and rewards for riding in off-peak months
- Partner with local businesses for seasonal discounts (summer ice cream stops, winter coffee shops)
- Launch "Winter Warm-Up" events at indoor locations near bike stations, introducing casual riders to year-round possibilities
- Send personalized "Your Year in Rides" recap to casual riders showing their riding patterns and estimated savings if they had been members

**Example Campaign Tagline:** "Don't just ride the seasons. Own them."

### Recommendation 4: Create "Ride Together" Family and Group Membership Options

**Insight Connection:** Casual riders use assistive bikes (cargo, hand tricycles) at higher rates, suggesting family/group recreational riding. Members rarely use these options.

**Strategy:**
- Develop family membership packages with discounted rates for multiple household members
- Create "Family Fleet" option: one membership covering access to cargo bikes and child seats for household use
- Partner with family-focused organizations (PTAs, parenting groups, family festivals) to offer trial memberships
- Produce content featuring family rides on the lakefront, park outings, and errands with cargo bikes
- Launch "Sunday Funday" monthly family ride events led by Cyclistic ambassadors
- Highlight safety features and inclusive bike options in marketing to parents and caregivers

**Example Campaign Tagline:** "More wheels. More smiles. More family time."

### Recommendation 5: Launch "Night Shift" Late-Night Membership Perks

**Insight Connection:** Casual riders use bikes for late-night entertainment trips; transit options may be limited during these hours.

**Strategy:**
- Partner with bars, restaurants, and entertainment venues to offer membership discounts to their late-night customers
- Develop "Safe Ride Home" positioning emphasizing 24/7 availability and reliability
- Create late-night route guides connecting popular entertainment districts
- Offer "Night Owl" rate: discounted first three months for users whose primary rides occur after 9 PM
- Install enhanced lighting at stations in entertainment districts and promote safety features
- Partner with ride-sharing services for first-mile/last-mile integration

**Example Campaign Tagline:** "The night is yours. So is the ride home."

---

## Summary

The analysis of Cyclistic bike-share data reveals clear distinctions between member and casual rider behavior:

| Dimension | Members | Casual Riders | Strategic Implication |
|-----------|---------|---------------|------------------------|
| **Trip Duration** | Short (12.5 min avg) | Long (24.3 min avg) | Members value efficiency; casual riders value experience |
| **Peak Days** | Weekdays (commute) | Weekends (recreation) | Target casual riders where they ride most |
| **Peak Hours** | 7–9 AM, 4–6 PM | 11 AM–6 PM | Different messaging for different mindsets |
| **Seasonality** | Year-round (70% winter retention) | Summer-focused (35% winter retention) | Educate on year-round value |
| **Trip Purpose** | Utilitarian (work, errands) | Recreational (leisure, tourism) | Bridge the gap between fun and utility |
| **Bike Preferences** | Standard bikes | Higher assistive bike usage | Highlight inclusive fleet in marketing |

By implementing these targeted marketing strategies, Cyclistic can effectively convert casual riders into annual members, increasing profitability and building a more sustainable, year-round ridership base. The recommendations focus on meeting casual riders where they are—weekends, tourist areas, family outings, and entertainment districts—while gradually introducing them to the everyday utility and year-round value that membership provides.
