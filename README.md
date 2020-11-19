**CURBING THE CURVE: Assessing Socioeconomic Factors in COVID-19 Risk Rates for the Purposes of Increased Resource Allocation**
<br><br>**Background**

On January 21, 2020, the COVID-19 virus first made landfall on American shores in a community just north of where I live in Seattle, Washington. Since then, over 246,000 lives have been lost, and over 11 million people have contracted the virus and could live with permanent health outcomes. Due to the current political climate in the United States-- and the fact the president himself is an adamant COVID denialist-- many activitites that impact the transmission of COVID-19 have been politicized.

The Roche Data Science Coalition (RDSC) is requesting the collaborative effort of the AI community to fight COVID-19, in what they are calling the UNCOVER challenge. UNCOVER, which stands for United Network for COVID Data Exploration and Research, in part seeks to identify which populations are at the greatest risk for COVID19.

Combining county-level data on health, socioeconomics, and weather can help us identify which populations are at risk for COVID19 and help prepare high-risk communities.

As such, in the spirit of the UNCOVER challenge, and in a sincere desire to help communities across this country, I am aiming to answer one question: what factors contribute to COVID transmission and death, and where are the populations most at risk?

**Methodology**

Data sources include:

* New York Times county-level COVID19 case and fatality data (part of UNCOVER data)
* 2016 CDC Social Vulnerability Data (part of UNCOVER data)
* 2020 Community Health Rankings Data (part of UNCOVER data)
* NOAA Global Surface Summary of the Day (GSOD) weather data for 2020
* Each county is paired with the nearest weather station. Most stations are within 50 km of the county center, and virtually all are within 100 km of the county center
* Kaiser Family Foundation Data on state-level stay-at-home orders

In order to properly sort counties into low-, medium-, and high-risk categories, I first had to define whether infection or death was the more negative outcome. Ultimately, I decided that neither exists in a vacuum, and both pose their own unique risks to a population:

* Living in a county with high TRANSMISSION can lead to inundation of hospitals and clinics, ultimately putting a squeeze on the health resources of the county. This can lead to an increase in non-COVID deaths. Further, even those who do not die from COVID don't escape many long-term effects.
* Living in a county with high DEATH rates could suggest an especially vulnerable population. Further, it could also suggest that a hospital system is already inundated.

As a result, I chose to look at the intersection of both metrics to determine the overall risk that COVID presents to a community. Because when we are discussing the impacts of transmission and death we are looking at exceedingly small percentages, I instead chose to use the equations:

* Infection Rate: Population/Infections
* Death Rate: Population/Deaths

These equations produce a result that could be framed as "1 out of every X citizens." This felt more accessible to the general population. Each county was then ranked from worst to best for infection rate and death rate. Those is the worse-off 50th percentile received a score of "1" for that risk factor.

* Infection Risk: A "1" was issued if more than 1 out of every 50 citizens had at some point been infected.
* Death Risk: A "1" was issued if more than 1 out of every 2000 citizens had died of COVID-19.

These numbers were then combined into a target metric known as the Risk Score. Each Risk Score is understood to mean the following:

* Risk Score of 0: These counties have both a slower-than-average infection and death risk. There may be factors in play that are slowing both the rates of transmission and death.
* Risk Score of 1: These counties have a higher-than-average infection OR death risk. This represents the vast majority of counties.
* Risk Score of 2: These cou nties have both a higher-than-average infection and death risk. There may be factors in play that are speeding up both the rates of transmission and death.

Because this is a classification problem that has both an obviously desireable class and an obviously undesireable class, the success metrics for each class are different. I chose to only focus on the Risk Scores of 0 and 2, as those in the 1 category provide fewer insights into potential protective factors or risk factors:

* Risk Score of 0: Because these counties have the most desireable outcome, we want to maximize PRECISION. We want to have a very high threshold for declaring a county as "low-risk", because to erroneously declare a county as low-risk when they are, in-fact, of moderate risk could provide a false sense of security for its citizenry. While this exclude counties that are, in fact, low-risk, in this instance, we would prefer to have a smaller population considered to be "safe."
* Risk Score of 2: Because these counties have the least desireable outcome, we want to maximize RECALL. We want to have a very low threshold for declaring a county as "high-risk", because to erroneously declare a county as NOT high-risk when they in-fact are could minimize the action taken by the citizenry to protect their health. While this may include counties that are medium-risk into the high-risk group, in this instance, we would prefer to have a larger population considered to be "in danger."

**Conclusions**
* **Don’t Underestimate the Impact of Partisanship**
  * Politics may play a larger-than-expected role in COVID-19 risk rates.
  * The analysis fails to catch the current prevalence of the virus in the midwest and plains states.
  * In the 2020 election, many of these states leaned or heavily favored the Republican party.
* **Issue Stay-at-Home Orders**
  * Failure to Issue Stay-at-Home Orders Negate Protective Factors.
  * Stay-at-home orders are amongst the highest used features
  * The average of coefficient is close to zero, meaning these features rely on feature interactions for its impact in the model
  * A negative coefficient means impact on protective factors
  * Stay-at-home orders are binary 0/1 scores
* **Focus on Areas with Extreme Poverty**
  * Many underlying risk factors are positively correlated with poverty
  * Teen Birth Rate: Percent of women aged 15-19 who give birth in a calendar year
  * Percent Smokers: Percent of residents 18 years or older who smoke cigarettes or use tobacco products
  * Severe Housing Cost Burden: Citizens who pay more than 30% of their income for housing
  * Percent Food Insecure: Percent of residents whose food intake is disrupted do to lack of money or resources
  * Percent Uninsured 3: Percent of residents who are uninsured (3 month rolling average)
  
**Potential for Future Research**
* **How do politics impact risk rates?**
    Analysis should be conducted on the impact of political affiliation, given the president’s divisive rhetoric about the pandemic. Does this explain certain regions being impacted more than we would expect?

* **How does climate impact risk rates?**
    Analysis should be conducted to see if certain climate and/or weather patterns either increase or decrease risk rates. While this was originally in scope for this project, due to high quantities of missing data, it was eventually excluded.

* **What are the best interventions for high-risk areas?**
    Analysis should be conducted to determine what might most effectively mitigate identified risk factors: increased access to health resources, increased access to virus/pandemic education, or improved social safety net programs. Answering the question of “where” resources are allocated doesn’t answer “how.”
