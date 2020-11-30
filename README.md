# 3744BIProject
Business Intelligence Project using R, analyzing consumer reviews of Amazon bought cellphones


Link i got the reviews and items csvs from:
https://www.kaggle.com/grikomsn/amazon-cell-phones-reviews?select=20191226-reviews.csv

Note: Some prices seemed to be inaccurate, so I could not include phones that were priced $1 or less.

Using the ggplot and/or dplyr packages I will seek to answer the new few questions 
via data visualization techniques.

Questions w/ Code:

1. What is the correlation between ratings and total reviews recieved?

While there initially seems to be none, the data actually forms a shape similar to normal distribution. Most of the ratings with a score between 3.5 and 4.5 
seems to have a higher than average amount of total reviews as well. More than likely the more popular a phone was, the more polarizing reviews it got and that
ended up with it getting a larger amount of total reviews and a rating that seems average.

-Creating plot to visually analyze data

> phones %>%
+ ggplot(aes(rating, totalReviews))+
+ geom_jitter()


2. Are reviews getting more helpful as time progresses?

Reviews have seemed to be seen as more and more helpful in general as time progresses. It may be because with time there have been: more users on Amazon in general, and
more conscientious shoppers actively researching products within the reviews before purchases.

- Converting "date" column from string to a usable column of dates

> reviews$date <- as.Date(reviews$date, "%B %d, %Y")

-Creating plot to visual analyze data

> reviews %>%
+ ggplot(aes(date,helpfulVotes)) +
+ geom_point()+
+ facet_wrap(~verified)


3. For each brand, do prices correlate with how many reviews a specific product receives?

Less expensive products seems to get more reviews across all of the brands that were within the dataset. Google, Samsung, OnePlus, Apple
 and Asus definitely had more reviews than average for more expensive devices because they either produce more expensive devices in general
(Samsung, Google, Apple, HUAWEI) or they do not produce too many different devices (ASUS, OnePlus).

-Creating plot to visual analyze data
> phones %>%
+ group_by(brand) %>%
+ ggplot(aes(price,totalReviews, color = brand))+
+ geom_jitter()+
+ facet_wrap(~brand)

4. For each brand, is there any correlation between average rating, and average price?

On the left side of the data it is hard to see a correlation between average price and average rating. On the right side, however, brands that had a lower 
average price saw a higher average rating. I suspect this is because there is lower risk when buying these products as far as price is concerned. That risk
mitigation can lead to good press if a consumer is satisfied with their product.

-Creating plot to visual analyze data

> phones %>%
+ group_by(brand) %>%
+ summarize(avg_rating = mean(rating, na.rm = TRUE) , avg_price = mean(price, na.rm = TRUE)) %>%
+ ggplot(aes(avg_rating,avg_price)) +
+ geom_point(aes(color = brand)) +
+ geom_line()

-List of brands, average ratings and average prices

> phones %>%
+ group_by(brand) %>%
+ summarize(avg_rating = mean(rating, na.rm = TRUE) , avg_price = mean(price, na.rm = TRUE)) %>%
+ arrange(desc(avg_price))

5. Do verified reviewers have a preference of brand that they like to review and do they generally review more expensive phones?

Verified reviewers tend to review more Samsung phones than any other in general, however if you go back to phones_plot_brand.png you will see that there are more Samsung phones
on Amazon than any other phone on this list. If you refer to Q5-3 they make up about 40% of all brands, with that being said I can only say that reviews correlate with the
amount of products each brand has on Amazon and not preference of brand.



Q5. Do verified reviewers have a preference of brand that they like to review, and do they generally review more expensive phones?

- Merging the dataframes "phones" and "reviews"

> phones_reviews <- merge(phones,reviews, by = "asin")

- List of brands and the amount reviews they get from verified reviewers arranged by average price

> phones_reviews %>%
+ group_by(brand) %>%
+ filter(verified == TRUE) %>%
+ summarize(count = n(), avg_price = mean(price)) %>%
+ arrange(desc(count))

- Creating plot for visual analysis

> phones_reviews %>%
+ group_by(brand) %>%
+ filter(verified == TRUE) %>%
+ ggplot(aes(price, totalReviews)) +
+ geom_boxplot()+
+ facet_wrap(~brand)
Questions & Analyses:

