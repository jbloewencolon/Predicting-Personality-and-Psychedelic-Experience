# Openness to Psychedelic Experience: Targeting Potential Participants for Studies in Psychedelic Medicine
A Flatiron School Phase 3 Project

![psycedelic_mushroom.png](https://github.com/jbloewencolon/Phase-3---Open-to-Psychedelic-Experience/blob/main/Images/bauhous%20trip.png)
    
By Jordan Loewen-Colón May 26th 2023

# The Business Problem

The (fictional) MindSpectrum Research Institute, is deeply engaged in groundbreaking work involving the clinical trials of psychedelic-assisted therapies. These trials seek to gauge the safety and effectiveness of various psychedelic substances, including psilocybin, MDMA, LSD, Ketamine, and Cannabis. Our data science problem is to develop a predictive model using personality traits and focusing on 'precision' as the key performance indicator, aiming to minimize false positives in identifying potential trial participants. The institute prefers a focused approach, favoring a smaller, more reliable group of participants who are genuinely likely to experiment with psychedelics, rather than a larger group with unpredictable inclinations.

# Recommendations:
The Mind Spectrum Institute should prioritize incorporating Oscore assessment into screening processes which could improve predictions of psychedelic use, as higher scores often indicate an inclination towards such usage. Given the noticeable difference in average Oscores between psychedelic users (0.152) and non-users (-0.593), investigating Oscore's influence on therapeutic effects of psychedelic-assisted therapies could yield valuable insights. And, finally, the study should taget those who've never used legal highs, nicotine, or amyl nitrites as potential participants for psychedelic trials.

# Data Understanding

To make our recommendations, we analyzed the [Drug Consumptions (UCI)](https://www.kaggle.com/datasets/obeykhadija/drug-consumptions-uci) from Kaggle. As stated on the original database:

"The Database contains records for 1885 respondents. For each respondent 12 attributes are known: Personality measurements which include NEO-FFI-R (neuroticism, extraversion, openness to experience, agreeableness, and conscientiousness), BIS-11 (impulsivity), and ImpSS (sensation seeking), level of education, age, gender, country of residence and ethnicity. All input attributes are originally categorical and are quantified. After quantification values of all input features can be considered as real-valued. In addition, participants were questioned concerning their use of 18 legal and illegal drugs (alcohol, amphetamines, amyl nitrite, benzodiazepine, cannabis, chocolate, cocaine, caffeine, crack, ecstasy, heroin, ketamine, legal highs, LSD, methadone, mushrooms, nicotine and volatile substance abuse and one fictitious drug (Semeron) which was introduced to identify over-claimers. For each drug they have to select one of the answers: never used the drug, used it over a decade ago, or in the last decade, year, month, week, or day."

![heatmap](https://github.com/jbloewencolon/Phase-2-Project---The-Garage-Problem/blob/main/Images/heatmap.JPG)

The dataset has 1884 entries and 31 columns with a mix of floats and objects. The personality scores (6:12) is measured on a Likert-based scale ranging from 0 (“Strongly Disagree”) to 4 (“Strongly Agree”) and then rendered as a float. The demographics have various sub categories, and the drug values are measured by recency (if ever) the substance has been consumed; CL0 being never used, and CL6 being used in the last day. Since we were primarily focused on understanding psychedelic use based on personality scores, we used violin plots to get a sense of the connection.

# Step 2: Data Preperation

In preparing the data, we focused on elements we thought would affect our numbers involving renovations broadly, and garage additions more specifically. Since we were dealing with both continuous numbers and integers, experimented with log transformations, but didn't find their adjustments useful and getting a more acurate model. To check the accuracy of our model, we focused primarily on the correlation between price per sqft of house. According to according to the website [www.redfin.com](https://www.redfin.com/county/118/WA/King-County/housing-market) the average price per sqft is $453. So we thought that would be a good target for checking the accuracy of our data prep.

With price as our major target, we set it as our Y and looked for correlations with the other columns as our x's.

![plots](https://github.com/jbloewencolon/Phase-2-Project---The-Garage-Problem/blob/main/Images/multiple%20regression.JPG)

Since scatterplots are more useful at visualizing the relationship with continuous data, we adjusted columns like "grade" and "condition" by turning them from strings to integers which allowed our model to see the relationship between the numbers more clearly and hopefully give us more accuracy. We then dealt with outliers which filtered out 2513 rows from our set of 30155.

We then created new columns checking for which houses had garages, and which ones didn't, in addition to a new column for garages based on size (either 1-car, 2-car, or 3-car).

# Data Modeling

Now with our data prepared and in hand, we created some models. First, we checked to see the accuracy of our data preperation by checking price per sqft.

![Model1](https://github.com/jbloewencolon/Phase-2-Project---The-Garage-Problem/blob/main/Images/Model%201.JPG)

So it looks like the coefficient is within the right range, but the R-squared is very low. However, it seems that transforming the numbe logarithmically actually lowers are R-value. So we kept it as it was and then added our other variables until we achieved the highest R-value given our selected data:

![Model2](https://github.com/jbloewencolon/Phase-2-Project---The-Garage-Problem/blob/main/Images/model%202.JPG)

# Data Understanding

Interpretations:


# Conclusion



# Next Steps

With more time, we could narrow down on personality traits and other drug types that might offer more insights from our model and thus update our recommendations.

# Questions?
For a full analysis please check the Jupyter Notebook or slide presentation.
Further questions? Contact Jordan Loewen-Colón @ jbloewen@syr.edu

## Repository Structure


```
├── data : data used for modeling
├── images : images used in PPT and README
├── Openness to Psychedelics.ipynb : notebook used to pull from API
├── README.md : project information and repository structure
├── presentation.pdf : the powerpoint presentation used to present data analysis
