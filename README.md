# Openness to Psychedelic Experience: Targeting Potential Participants for Studies in Psychedelic Medicine
A Flatiron School Phase 3 Project

![psycedelic_mushroom.png](https://github.com/jbloewencolon/Phase-3---Open-to-Psychedelic-Experience/blob/main/Images/bauhous%20trip.png)
    
By Jordan Loewen-Colón May 26th 2023

# The Business Problem

The (fictional) MindSpectrum Research Institute, is deeply engaged in groundbreaking work involving the clinical trials of psychedelic-assisted therapies. These trials seek to gauge the safety and effectiveness of various psychedelic substances, including psilocybin, MDMA, LSD, Ketamine, and Cannabis. These substances, when used in conjunction with psychotherapy, are being tested as potential treatments for various mental health disorders, such as depression, anxiety, post-traumatic stress disorder (PTSD), and addiction.

Our task is to assist the institute with its patient recruitment campaign, aiming to attract individuals who are not only afflicted by the targeted conditions, but are also open to the concept of psychedelic usage. The goal is to identify individuals who are naturally inclined towards trying psychedelics, without the need for excessive persuasion or influence.

In this relatively nascent field of psychedelic science, it's critical for the institute to maintain a positive public image, hence there's an inherent need to ensure that trial participants are optimally suited. The ideal participant would display an inherent willingness to try psychedelics, indicating a certain level of curiosity and a potentially positive mindset, which in turn may contribute to improved trial outcomes.

Our data science problem is to develop a predictive model focusing on 'precision' as the key performance indicator, aiming to minimize false positives in identifying potential trial participants. The institute prefers a focused approach, favoring a smaller, more reliable group of participants who are genuinely likely to experiment with psychedelics, rather than a larger group with unpredictable inclinations.

# Recommendations:
Recruitment should prioritize individuals who've never used legal highs, nicotine, or amyl nitrites as potential participants for psychedelic trials. Secondly, with an Oscore coefficient of 0.5, incorporating Oscore assessment into screening processes could improve predictions of psychedelic use, as higher scores often indicate an inclination towards such usage. Finally, given the noticeable difference in average Oscores between psychedelic users (0.152) and non-users (-0.593), investigating Oscore's influence on therapeutic effects of psychedelic-assisted therapies could yield valuable insights.

# Step 1: Data Understanding

To make our recommendations, we analyzed the 2022 data from King's County.

The dataset has 30155 entries and 25 columns with a mix of string values, floats, and integers. Bathrooms as float makes sense, but "floors" as float seems odd. It was also not clear what elements were contained in some of the object categories like "grade" or "nuisance." There were also some missing entries for "sewer_system" and "heat_source." Some odd things we noticed initially is that there were houses without bedrooms or bathrooms. There were also outliers on the larger end as well, with houses containing 13 bedrooms and 10.5 bathrooms. There was even a house listed with only 3sqft of living space. It also became clear that we were going to need to seperate out the houses that already have garages from those that do not.

![heatmap](https://github.com/jbloewencolon/Phase-2-Project---The-Garage-Problem/blob/main/Images/heatmap.JPG)

Given that are focus is on garages, it's important to note that there are both houses with no garages or which have never been renovated. In narrowing down, we noticed that columns like "waterfront" and "greenbelt" had a small number of entries, so they probably would not add much to our analysis. Additionally, given time constraints, we wouldn't be able to spend time on categories like "date, view, sqft_above, sqft_basement." And for the sake of this excercise (and its time constraints), we are pretending "address, lat, and long" were not included in the dataset. So we ended up focusing primarily on "yr_renovated," "condition," "grade," and, especially, "sqft_living" as categories in order to build the most accurate model.

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
