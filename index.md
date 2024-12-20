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

#### **Figure 4: Histogram of Domestic Ratings**
![Histogram of Domestic Ratings](assets/img/Domestic%20Rating.png)

**Observation**:  
Most domestic beers have fewer than **100 ratings**, with a steep decline and a long tail for popular beers.

**Analysis**:  
- **Bias in Domestic Ratings**: A few highly rated beers dominate the average.  
- **Recommendation**: Normalize data to account for less-rated beers.

---

#### **Figure 5: Histogram of International Ratings**
![Histogram of International Ratings](assets/img/International%20Rating.png)

**Observation**:  
International beers exhibit a broader distribution, with many beers receiving **>1,000 ratings**.

**Analysis**:  
- **Popularity Disparity**: International beers have a wider consumer base.  
- **Recommendation**: Normalize data to enable fair comparisons between domestic and international ratings.

---

### **4. Naming Bias**

#### **Figure 6: Comparison Analysis**
![Comparison Analysis](assets/img/Camparison.png)

**Observation**:  
First ratings are consistently higher than subsequent averages, indicating **optimism bias**.

**Analysis**:  
- **Expectation vs. Reality**: Higher initial ratings reflect enthusiasm or positive impressions from beer names.  
- **Recommendation**: Platforms could anonymize beer names during early reviews to reduce bias.

---

## **Key Insights**

1. **Temporal Trends**:  
   - Both datasets show an upward trend in ratings over time, influenced by industry growth and consumer preferences.  

2. **Anchoring Effect**:  
   - Early ratings bias subsequent reviews, requiring adjusted weightings for objectivity.  

3. **Cultural Bias**:  
   - Domestic beers receive more favorable ratings, reflecting cultural preferences.  

4. **Naming Bias**:  
   - Optimistic early ratings may be driven by beer names, suggesting anonymization as a potential solution.

---

## **Conclusion**

This analysis reveals multiple biases influencing beer ratings, including temporal trends, anchoring effects, cultural preferences, and naming influences. Addressing these biases through normalization, weighting adjustments, and anonymization can lead to more objective and reliable ratings, ultimately benefiting consumers and breweries alike.

---
