---
layout: default
title: "The biases behind rating: Uncovering the hidden influences in beer ratings"
---

# **The Biases Behind Rating: Uncovering the Hidden Influences in Beer Ratings**

## **Introduction**

The world of beer reviews is rich with data, offering insights into consumer preferences and biases. The main goal of any rating app is to provide **objective scores**, helping users navigate a world of choices. However, ratings are inherently **subjective**, shaped by the biases and perceptions of reviewers.

In this data story, we explore the various biases that influence beer ratings, ranging from **time-related trends** to **cultural and naming biases**. By identifying these influences, we propose adjustments that enhance the objectivity and accuracy of ratings.

---

## **The Key Questions**

Our analysis focuses on the following critical questions:

1. **Temporal Trends**: How do ratings change over time? Are there seasonal variations or spikes linked to events or holidays?  
2. **Anchoring Effects**: Do early ratings significantly impact subsequent ones? Are reviewers biased by the first few scores?  
3. **Cultural Biases**: Do reviewers rate domestic beers more favorably than international ones? How does beer consumption per capita influence ratings?  
4. **Naming Bias**: Does a beer's name set expectations that influence its rating?

---

## **Datasets and Methodology**

### **Datasets**
1. **BeerAdvocate Dataset**: Comprising ratings, user information, and brewery details.  
2. **Beer Consumption Data**: Total and per capita beer consumption by country (sourced from World Population Review).  

### **Methodology**
- **Temporal Analysis**: Ratings were aggregated by month and year to identify patterns and trends.  
- **Anchoring Effect**: Correlation tests (Pearson and Spearman) were used to evaluate the relationship between early and subsequent ratings.  
- **Cultural Bias**: Domestic and international ratings were compared using t-tests and mean comparisons, and their correlation with beer consumption was assessed.  
- **Naming Bias**: Text analysis and Chi-square tests were used to evaluate the impact of beer names on ratings.

---

## **Findings**

### **1. Temporal Trends**

#### **Figure 1: Ratebeer Dataset**
![Average Rating per Year (Ratebeer Dataset)](assets/img/Average%20Rateing%20per%20Year%20Ratebeer.png)

**Observation**:  
The average rating starts at **3.25** in 2000, dips slightly, and then steadily increases, reaching **3.40** by 2017.

**Analysis**:  
- **Upward Trend**: Consistent increases in ratings suggest improving beer quality or shifting consumer expectations.  
- **Initial Dip**: Early ratings reflect stricter evaluations or limited beer variety.  
- **Industry Growth**: The rise of craft beer in the mid-2000s likely contributed to higher ratings.

---

#### **Figure 2: BeerAdvocate Dataset**
![Average Rating per Year (BeerAdvocate Dataset)](assets/img/Average%20Rating%20per%20Year%20BeerAdvocate%20dataset%20.png)

**Observation**:  
A spike in 2000 (rating > 4.0) is followed by a sharp decline, with steady growth post-2005.

**Analysis**:  
- **Spike in 2000**: Early adopters may have rated generously, or the sample size was small.  
- **Recovery**: Ratings post-2005 reflect better beer quality and consumer preferences.  
- **Comparison**: BeerAdvocate data exhibits more fluctuations than Ratebeer.

---

### **2. Anchoring Effect**

The anchoring effect is a well known cognitive bias that influences people's judgment based on others previous opinions or other information they encountered. This effect appears everywhere in anyone’s life, often without us noticing it. The brain tends to use the first information it sees, which greatly influences the final judgment of everyone. For well-known items, this can lead to significant bias: if everyone’s opinion is biased by the anchoring effect then the item will be perceived as having a biased value by the majority. As it is also difficult for many people to go against the majority opinion, popular objects may have stronger anchoring effects that may cause some items to be highly overrated !

In BeerAdvocate and RateBeer the ratings are given by any one. As some beers might have a really large number of ratings, one can think that Wisdom of the Crowds apply and that the ratings are representative. However, in order to write a review, one has to go on the web site and will necessarily see the current rating of the beer, with the list of more recent ratings with a commentary. So anyone rating a beer will be confronted with the others opinions and this will have a little bias because of the anchoring effect.

The goal is to observe this anchoring effect on both BeerAdvocate and RateBeer datasets.

To analyse the anchoring effect we first want to look at the __data__ !
In this case it would be interesting to see what the distribution of the rating ordered by their corresponding date looks like. 
As the plots appear to be very noisy we perform a moving average in order to smooth them.
Then by looking at the plot of such distribution for individual beer we can see a strange phenomena. When the first ratings are extreme values, either very high or very low, the following rating seems to be more nuanced and closer to the mean (which is 3).

If the initial ratings are very high, they tend to decrease over time, and if they start low, they tend to increase.
Here are two cherry picked examples of such distribution:

__*Distribution of ratings order in time for cherry picked beers*__
<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="assets/img/part2/p2_cherry1.png" alt="Histogram of Domestic Ratings" style="width: 48%;"/>
  <img src="assets/img/part2/p2_cherry2.png" alt="Histogram of Domestic Ratings" style="width: 48%;"/>
</div>
<br>

On these specific plots we can see that the first ratings are highly biased, or at least overly categorical. And this appears on many beers, but to see if the tendency really exists, we now plot the mean distance on every popular beer between a rating and the mean rating of three, and we perform that for bothBeerAdvocate and RateBeer.
We only took the popular beer, because our analysis directly depends on the total number of ratings and we need many of them for it to be significant. As before the graph is noisy so we smooth it using a moving average.
Here are the two plots, respectively for RateBeer and BeerAdvocate.

__*Average distance of ordered ratings from the mean rating of 3*__
<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="assets/img/part2/rb_average_dist.png" alt="Histogram of Domestic Ratings" style="width: 48%;"/>
  <img src="assets/img/part2/ba_average_dist.png" alt="Histogram of Domestic Ratings" style="width: 48%;"/>
</div>
<br>

On these graphs we can see that the first ratings are on average more distantes from the average rating of 3 than the following ones.  We also observe that the rating that comes just after the first rating also tends to be higher than the final rating of the beer. This might 
This might be due to the fact that the most enthusiastic or critical individuals are usually giving their rating first !

By plotting a histogram of the distribution of the first rating, vs the mean rating of every beer, we can see that first beer tends to be greater, which correlates with the hypothesis that more enthusiastic people tend to give their rating first.

__*Distribution of first ratings vs overall final rating*__
![histogram first vs overall](assets/img/part2/first_vs_hist.png)

We can also consider the regression to the mean effect, rating tends to naturally move close to the average, 3 in this case, and this is due to the fact, as said before, that the first rating is often highly biased by special circumstances, emotions or by the novelty of the beer. 

To see if the anchoring effect has an influence on the final rating of the beer, we want to search for a correlation between the first rating and the mean rating one. 
To do that, we perform a Pearson correlation test with null hypothesis telling that there is no correlation between the first rating and the final mean of the rating. The test tells us that there is a significant correlation of 0.683 (p value < 0.05). 
We can illustrate this correlation by making a joint plot of both first rating and the mean of every other rating on every beer. This illustration highlights the correlation between both distributions.

__*Correlation between the first ratings vs overall final rating distributions*__
![correlation joint plot](assets/img/part2/joint_plot_correlation.png)

The absence of any correlation would have proven the absence of any anchoring effect, but this correlation alone doesn’t prove the presence of the anchoring effect as both the first rating and the mean rating concern the same beer, so they should normally be correlated.

To prove the precence of any Anchoring Effect we would need a rating for every beer that is representative and unbiased. 
On the BeerAdvocate website, there is such an objective score named the bros score. 
The idea to observe Anchoring effect would be to split the website rating in two groupe :
- The first groupe have a very high first rating
- The second group has a very low first rating

The anchoring effect would act differently between the two groups, in the first groupe the overall rating would be __above__ the objective rating (or bros score), and in the second groupe, the overall of final rating would be __below__ the bros score.

By doing so we obtained the following results :

__*Differency between overall rating and bros score for both groups*__
![Bros score bar plot](assets/img/part2/bros_bar_plot.png)


We can see on this graph that the rating differs from the bros score as expected according to the Anchoring Effect.
For the groupe with high first rating, the overall rating is slightly above from about `0.04` which is negligible. 
But for the second group the difference it higher, around `0.17` points lower than the bros score.

The observed Anchoring effect it really small, so this differences might be only due to randomness in the rating.
To prove it is not the case, we perform a T-Test with the null hypothesis being that both rating do not differ significantly.
This statistical test result tell us that the difference  between the bros score and the overall final rating is significative, so we conclude that we have observed the Anchoring Effect, but it has a really small impart on the final ratings.


---

### **3. Cultural Bias**

So, we found that there is indeed a small but existing Anchor bias in the beer ratings. But what about cultural biases ?
Indeed, it wouldn't be surprising that beers rated by people from the same country as where they were created are more
generously rated than the others.  

We'll first check whether people who rate beer that come from their country, give more generous notes or not when rating the beer.
We'll call them, respectively, domestic and international raters.  

Let's plot ratings frequencies of both domestic (treatment group) and international (control group) raters!

__*Treatment and control group rating frequencies with KDE curves (BeerAdvocate left and RateBeer right)*__
<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="assets/img/part3/ba_rating_freq.png" alt="" style="width: 48%;"/>
  <img src="assets/img/part3/rb_rating_freq.png" alt="" style="width: 48%;"/>
</div>
<br>

We see that the distributions are pretty similar, but in both of them a slight shift between the domestic and international ratings can be seen.
On the BeerAdvocate data, domestic reviewers seem to have slightly higher ratings, but we notice the inverse for RateBeer.
We can't be sure just by looking at the histograms. Maybe a plot of the means and basic statistics can give us some more insight.

__*Treatment and control group statistics with bootstrapping error bars for the mean (BeerAdvocate left and RateBeer right)*__
<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="assets/img/part3/ba_boxplot.png" alt="" style="width: 24%;"/>
  <img src="assets/img/part3/ba_means.png" alt="" style="width: 25%;"/>
  <img src="assets/img/part3/rb_boxplot.png" alt="" style="width: 24%;"/>
  <img src="assets/img/part3/rb_means.png" alt="" style="width: 25%;"/>
</div>
<br>

The median for BeerAdvocate is slightly higher for the domestic raters and the mean is about 0.1 higher. However, the 
quantiles are more or less the same for RateBeer and the international raters' mean looks higher than the domestic raters.
Although the means' error bars are overlapping so they might just be also very similar.  

It seems like there is a small positive impact on the rating when people come from the sample place as the beer in the
BeerAdvocate data, but the results tend to show that there is no impact in the RateBeer data. Let's try fitting a
linear model to both datasets with the ratting as the dependant variable and see the influence of each feature of the data.

__*Linear regression coefficients (BeerAdvocate left and RateBeer right)*__
<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="assets/img/part3/ba_coeffs.png" alt="" style="width: 48%;"/>
  <img src="assets/img/part3/rb_coeffs.png" alt="" style="width: 48%;"/>
</div>
<br>

We see that the for BeerAdvocate, the domestic ratings, the alcohol by volume, the date when the rating was posted and
"Brothers' score" (the two founders of BeerAdvocate) have a positive impact on the rating, but when people post a review 
with the rating, it's rating tends to be lower. We can see the same behaviour for RateBeer (minus the review and bros_score
which are only on BeerAdvocate). There are quite large error bars for the domestic_rating variable for RateBeer, so again
it's hard to say if domestic ratings influence the ratings for this data.  

This a bit disappointing... Results show that there might not be a real difference between domestic and international ratings
after all.

---

### **4. Naming Bias**

# What's in a Name?

When it comes to the enjoyment of drinking a beer, how much does the label impact us? This is a question that merges psychology, 
branding and consumer behaviour. Beer names can vary wildly from classic descriptions of the beer and its brewery (Speedway IPA), 
to quirky and unique names (Hopportunity). These names were selected for a reason, and as consumers, the name is the first thing that we see. 
Does this cause some sort of priming where certain names raise or lower our expectation of a beer and thus the likelihood that we rated it higher or lower?

First of all, what do typical beer names look like? Below is a wordcloud of the most common terms found in beer names for 
BeerAdvocate and RateBeer respectively:

BeerAdvocate Word cloud					RateBeer word cloud

When analyzing beer names, and as demonstrated by the word clouds above, we first noticed that the most common words refer 
to the beer’s style or its brewery. Specifically, **41.87%** of beer names on BeerAdvocate and **38.13%** on RateBeer ave some 
mention of the beer’s style, while **14.30%** on BeerAdvocate and a striking **89.35%** on RateBeer mention the brewery. 
Given the high prevalence of these references—especially brewery names on RateBeer—we exclude them from our keyword analysis 
moving forward to focus on more unique and meaningful terms that might better capture the impact of naming on ratings.

## Average Rating per Keyword

We begin our analysis by studying the impact of specific words within a beer’s name. By tokenizing beer names and stemming 
words to group similar forms together, we can observe the average rating that beers containing such a word have obtained. 
We initially limit our analysis to the most common words, that have at least 100 beers that use them. For Beer Advocate, 
we find the following ten best and worst rated keywords:

GRAPH

And for Rate Beer:

GRAPH

The biggest takeaway from this analysis is that the choice of keywords in beer names strongly correlates with average ratings, 
and these correlations seem to cluster into thematic groups that reflect consumer expectations and preferences. By grouping these keywords, 
we can better understand the types of associations they evoke and how they might prime a drinker’s experience.

### Keywords Associated with High Ratings

The highest-rated beers often include words that evoke indulgence, craftsmanship, or exclusivity. These can be grouped into several themes:

#### 1. Barrel-Aging and Blending

Terms like “blend”, “brandi”, “cognac” , and “ba” (short for barrel-aged) suggest techniques associated with high-end or 
experimental brewing. These processes are often perceived as elevating a beer’s complexity and depth, potentially leading to higher ratings.

#### 2. Dessert-Like Flavors
    
Words like “cake”, “bean” (linked to vanilla or coffee), and “nib” (cacao nibs) suggest rich flavors. 
These terms align with consumer preferences for dessert-inspired beers.

#### 3. Exotic Hops
    
Terms such as “galaxi”, "dank" and “sauvin”, which reference specific hop varieties, hint at the use of rare or premium ingredients. 
This resonates with craft beer enthusiasts who value innovation and distinctive flavor profiles.

#### 4. Craft and Independent Branding
    
Names like “speedway” and “mikkel” are tied to well-regarded craft breweries. 
These words carry brand-specific associations that can elevate consumer expectations.

### Keywords Associated with Low Ratings

On the other end of the spectrum, the lowest-rated beers often include terms that suggest simplicity, 
mass production, or lower-quality offerings. These terms can be grouped as follows:

#### 1. Mass-Market Appeal
    
Words like “premium”, “light”, “ice”, and “draft” are commonly associated with large-scale commercial beers. 
These beers are often perceived as less complex or distinctive, which may lead to lower ratings.

#### 2. Mixes or Low-Alcohol Styles
    
Terms like “radler,” “shandi,” and “alkoholfrei” refer to lighter, often fruit-infused or alcohol-free beverages. 
While these styles have their niche, they are not typically associated with the depth and richness favored by craft beer enthusiasts.

#### 3. Generic Branding
    
Words such as “cerveza” and “classic” evoke a traditional or straightforward image. This simplicity may not excite consumers looking for novelty or creativity.

The analysis highlights how a beer’s name is tied to certain expectations, and what the average reviewer on the platform tends to prefer. 
Words linked to indulgence, rarity, or craftsmanship tend to prime consumers to expect—and potentially rate—a better experience, 
whereas names tied to mass production or simplicity might lower expectations and ratings. While it is not made evident that the label causes higher/lower ratings, 
it is certain that reviewers are more responsive to complex flavors and techniques than the typical available beers most people enjoy.

## Descriptive Names vs Non-Descriptive Names

As seen before, most beer names are quite descriptive. They clearly present the beer's style and/or brewery. 
But perhaps people prefer more creative names instead? To explore whether including the beer style or brewery name impacts ratings, 
we compared beers with and without these descriptors across all beers and specific styles like lagers (which is a keyword that tends to have lower average ratings). 
While a t-test revealed a statistically significant difference, the effect was minuscule and inconsistent between datasets: one showed a slight positive effect, 
and the other a slight negative. This suggests that including style or brewery names in the beer’s name does not meaningfully influence its rating.

---

## **Conclusion**

This analysis reveals multiple biases influencing beer ratings, including temporal trends, anchoring effects, cultural preferences, and naming influences. 
Addressing these biases through normalization, weighting adjustments, and anonymization can lead to more objective and reliable ratings, ultimately benefiting consumers and breweries alike.

---
