# Australian Olympic Sports Analytics

## Youth Participation × Media Visibility Ahead of Brisbane 2032

This project explores how data analytics can help identify Australian Olympic sports that have an established youth participation base but comparatively limited media visibility ahead of the Brisbane 2032 Olympic Games.

The analysis combines structured participation data from AusPlay with semi structured text data from Guardian Australia. The aim is not to produce a definitive funding ranking, but to identify patterns that could help the Australian Sports Commission (ASC) investigate opportunities for youth engagement, fan development and stronger connections between young participants and Australian Olympic athletes.

---

## Project Question

Which Olympic sports present promising opportunities for youth fan development based on participation levels, participation growth and media visibility?

The project focuses particularly on sports that already have a meaningful base of young Australian participants but may not receive the same level of media attention as the country's most dominant sports.

---

## Project Approach

The analysis is divided into two stages.

### 1. Participation Exploration

The first notebook analyses AusPlay participation data to understand:

- Youth participation across Olympic sports
- Absolute numbers of participants aged 5–14
- Youth participation rates
- Year on year participation trends
- Sports that sit between the largest and smallest participation groups

This stage identifies a group of mid tier Olympic sports that have a substantial youth participation base without the scale of the most dominant sports.

The analysis also examines which of these sports are growing or declining between 2023–24 and 2024–25.

### 2. Strategic Sports Analysis

The second notebook combines participation data with Guardian Australia media coverage.

The analysis includes:

- Guardian Australia article collection through the Guardian API
- Text preprocessing
- TF IDF vectorisation
- Sport specific media visibility measurement
- Integration of media and participation data
- A composite opportunity score
- K Means clustering for strategic segmentation
- Ethical and methodological analysis

The final Guardian dataset contains 170 articles after deduplication.

---

## Data Sources

### AusPlay

The participation analysis uses the Australian Sports Commission's AusPlay sport by sport participation data.

The dataset contains participation rates and estimated participant numbers across Australian sporting activities.

The analysis uses:

- Overall child participation rates
- Participation for children aged 5–14
- Participation for the 12–14 age group
- Year on year participation changes

The 0–4 age group is excluded from the main youth analysis because the project focuses on school age children and potential fan development leading towards Brisbane 2032.

### Guardian Australia

Guardian Australia articles are collected using the Guardian Content API.

The final strategic analysis uses a targeted collection of sport related articles from the Australian Guardian production office and focuses on coverage from 2025 onwards.

The collected articles are used to examine the relative media visibility of Olympic sports within the analysed corpus.

Media visibility is therefore a relative measure within this dataset rather than a measure of total Australian media coverage.

---

## Analytical Methods

### Participation Analysis

AusPlay's supplied participation rates are used directly rather than calculating rates from participant counts.

The analysis combines:

- Participation counts
- Participation rates
- Age specific participation
- Year on year participation changes

This allows sports to be compared using both absolute reach and population adjusted participation rates.

### TF IDF

TF IDF is used to identify important terms within the Guardian article corpus.

The vocabulary is refined by removing common English stop words and additional generic journalism terms that were dominating the initial results.

This helps focus the text analysis on terms that are more useful for understanding the media landscape.

### Media Visibility

Media visibility is calculated using sport specific keywords.

The analysis counts articles containing the relevant sport terms rather than treating the frequency of generic words as an indicator of sports coverage.

Word boundary matching is used for terms where partial matches could create false positives.

For example, sport specific variations such as canoe, canoeing and kayak can be grouped together.

### Opportunity Score

A composite opportunity score is calculated using four dimensions:

| Dimension | Weight |
|---|---:|
| Overall child participation | 40% |
| 12–14 participation | 25% |
| Year on year growth | 20% |
| Low media visibility | 15% |

The variables are normalised using min max scaling before the weighted score is calculated.

The score is intended as a decision support measure rather than a definitive investment ranking.

Small sports can produce unusually high percentage growth from very small starting bases, so the analysis also applies a minimum participation threshold when interpreting strategic opportunities.

### K Means Clustering

K Means clustering is used to group Olympic sports according to their combined:

- Child participation
- 12–14 participation
- Year on year growth
- Media visibility

Four clusters are used to create an interpretable segmentation of the sports landscape.

The resulting groups broadly represent:

1. High participation and high visibility sports
2. Moderate participation and moderate visibility sports
3. Lower visibility sports with positive participation growth
4. Smaller sports experiencing declining participation

---

## Key Findings

### Youth participation is not evenly distributed

A small group of sports accounts for a large share of youth participation, while many Olympic sports have much smaller participation bases.

The mid tier analysis provides a useful middle ground between highly dominant sports and sports with very small youth participation bases.

### Participation growth and media visibility do not always move together

Several sports show positive youth participation trends while receiving relatively limited coverage within the analysed Guardian dataset.

This creates a participation visibility gap that may be relevant for youth fan development.

### Hockey and Volleyball show useful growth signals

Hockey and Volleyball both show positive year on year participation trends while having substantially lower media visibility than the largest sports.

Their existing youth participation bases provide a potential audience for stronger connections between junior participants, Australian athletes and Olympic competition.

### Gymnastics combines a substantial youth base with limited coverage

Gymnastics has one of the larger youth participation rates among the analysed sports while appearing relatively infrequently in the Guardian corpus.

This makes it an important example of the difference between participation and media visibility.

### High media visibility does not necessarily indicate an unmet opportunity

Football/soccer and Swimming have both high youth participation and strong media visibility.

The clustering analysis separates these sports from lower visibility sports, showing why participation alone is not sufficient for identifying strategic opportunities.

---

## Strategic Interpretation

The main insight from the project is that participation and media visibility provide different pieces of information.

A sport can have:

- A large participation base but limited media exposure
- Strong media exposure but a smaller participation base
- Strong participation growth from a small base
- Both strong participation and strong media visibility

Combining these dimensions provides a more useful picture than examining any single measure independently.

The results suggest that youth fan development could be investigated through approaches such as:

- School based athlete engagement
- Digital content targeted at young participants
- Connections between junior clubs and national teams
- Athlete ambassador programmes
- Content that connects participation pathways with Olympic competition

These are strategic opportunities for further investigation rather than final funding recommendations.

---

## Ethical Considerations and Limitations

### AusPlay uncertainty

AusPlay participation data is survey based and contains uncertainty, particularly for smaller sports.

Small changes in participation rates should therefore not automatically be interpreted as meaningful changes in participation.

### Media sample bias

The media analysis uses Guardian Australia as a single media source.

Guardian's editorial priorities do not represent the entire Australian media landscape. Sports that receive limited coverage in this dataset may still receive substantial coverage through television, specialist sporting media, social media or other publications.

### Media visibility is not cultural value

Low media visibility does not mean that a sport is less important, less valuable or less popular within its community.

The opportunity score should therefore not be interpreted as a measure of the social or cultural value of a sport.

### Small base effects

Percentage growth can be misleading for sports with very small participation bases.

A large percentage increase from a small starting point can represent only a small absolute change in the number of participants.

### Equity and access

Participation patterns can be influenced by factors such as:

- Cost
- Geography
- Availability of facilities
- School programmes
- Disability access
- Cultural factors
- Access to sporting clubs

These factors are not fully captured by the quantitative analysis.

### Scope of the analysis

The project uses two evidence streams and should not be used as a standalone basis for funding decisions.

Further analysis could incorporate broader media sources, qualitative research, stakeholder consultation and more detailed participation pathway data.

---

## Repository Structure

```text
australian-olympic-sports-analytics/
│
├── notebooks/
│   ├── 01_participation_exploration.ipynb
│   └── 02_olympic_sports_strategy.ipynb
│
├── src/
│   ├── C4S-AusPlay-By-Sport-Data-Tables-13-November-2025.xlsx
│   ├── brisbane_2032_sport_articles.json
│   └── guardian_sports_articles.json
│
├── private/
│   └── guardian_key.txt
│
├── .gitignore
├── readme.md
└── requirements.txt
