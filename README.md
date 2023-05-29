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

![violinplot.png](https://github.com/jbloewencolon/Phase-3---Open-to-Psychedelic-Experience/blob/main/Images/violen%20plot%201.png)

The dataset has 1884 entries and 31 columns with a mix of floats and objects. The personality scores (6:12) is measured on a Likert-based scale ranging from 0 (“Strongly Disagree”) to 4 (“Strongly Agree”) and then rendered as a float. The demographics have various sub categories, and the drug values are measured by recency (if ever) the substance has been consumed; CL0 being never used, and CL6 being used in the last day. Since we were primarily focused on understanding psychedelic use based on personality scores, we used violin plots to get a sense of the connection.

# Step 2: Data Preperation

Since the data contained no null values or duplicate we were able to focus on creating a target column of just psychedelic drugs: cannabis, ecstasy, ketamine, LSD, and mushrooms. We then dropped any rows that indicated used of the fictious drug "Semer" that the original data collectors had included to weed out "overclaimers." Finally, we created a pipeline to streamline our model production going forward and split the data into training and test sets.

# Data Modeling

Our first model was a simple logistic regression. Starting with a logistic regression model offers interpretability and simplicity, serving as an efficient method to establish baseline performance for binary classification, such as distinguishing participants willing to try psychedelics. Its probabilistic output and capability to highlight feature importance provides crucial insights into factors influencing willingness to participate in the trial, while setting a comparative standard for future, more complex models. The model resulted in a **precision score of 94%** which implies a lower rate of false positives, as precision is the ratio of true positives to the sum of true positives and false positives.

![confusionmatrix.png](https://github.com/jbloewencolon/Phase-3---Open-to-Psychedelic-Experience/blob/main/Images/log%20reg%20confusion%20matrix.png)

The model had a total of 23 false positives which isn't bad. We then looked to see what the coefficients with the highest magnitude were: 

![log reg featureimport.png](https://github.com/jbloewencolon/Phase-3---Open-to-Psychedelic-Experience/blob/main/Images/log%20reg%20feature%20importances.png)

The Oscore had the largest coefficient magnitude of all our personality traits. The coefficient value of 0.5 for "Oscore" means that for every one-unit increase, the log odds of the outcome "Psychedelics" being 'yes' (versus 'no') increase by 0.5, assuming all other variables in the model are held constant. To better understand this in terms of odds (rather than log odds), we can calculate the odds by taking the exponent of the coefficient: exp(0.5) ≈ 1.65. This means that for every one-unit increase in "Oscore", the odds of the outcome "Psychedelics" being 'yes' (versus 'no') increase by about 65%, assuming all other variables in the model are held constant. And since, as we saw above, people who have taken psychedelics have a higher Oscore, we can assume that a higher Oscore means a higher likelihood that a person has consumed a psychedelic (or perhaps will).

We continued with our modeling by using both a Random Tree Classifier (RFC) and a Gradient Boost classifier (GBC) which produced **precision ratings of 91 and 92** respectively. Neither seems as good as our logistic regression model. Looking at the feature importances of both revealed an agreement across all three models that Oscore seems to have the most importance in predicting psychedelic use.

RFC Feature Importances:
![RFC featureimport.png](https://github.com/jbloewencolon/Phase-3---Open-to-Psychedelic-Experience/blob/main/Images/RFC%20feature%20importance.png)

GBC Feature Importances
![GBC featureimport.png](https://github.com/jbloewencolon/Phase-3---Open-to-Psychedelic-Experience/blob/main/Images/GBC%20feature%20importance.png)

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
