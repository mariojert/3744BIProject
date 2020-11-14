# 3744BIProject
Business Intelligence Project using R, analyzing consumer reviews of Amazon bought cellphones


Link i got the reviews and items csvs from:
https://www.kaggle.com/grikomsn/amazon-cell-phones-reviews?select=20191226-reviews.csv

Note: Some prices seemed to be inaccurate, so I could not include phones that were priced $1 or less.

Using the ggplot and/or dplyr packages I will seek to answer the new few questions 
via data visualization techniques.


Questions:

1. What is the correlation between ratings and total reviews recieved?

While there initially seems to be none, the data actually forms a shape similar to normal distribution. Most of the ratings with a score between 3.5 and 4.5 
seems to have a higher than average amount of total reviews as well. More than likely the more popular a phone was the more polarizing reviews it got and that
ended up with it getting a larger amount of total reviews and a rating that seems average.

2. Are reviews done been more helpful as time progresses?

Reviews have seemed to be seen as more and more helpful in general as time progresses. It may be because with time there have been: more users on Amazon in general, and
more conscientious shoppers actively researching products within the reviews before purchases.

3. For each brand, do prices correlate with how many reviews a specific product receives?
Cheaper = more reviews more often than not

4. For each brand, is there any correlation between average rating, and average price?
yes generally high price = lower avg rating besides 2 outliers

5. Do verified reviewers have a preference of brand that they like to review and do they generally review more expensive phones?
