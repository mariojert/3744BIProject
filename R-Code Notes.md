SETUP:

Importing both the "prices" and "reviews".csv files into datasets in python:

> phones <- read.csv("GitHub/3744BIProject/20191226-items.csv")

> reviews <- read.csv("GitHub/3744BIProject/20191226-reviews.csv")


Editing records and columns from phones dataset:

(Incorrect prices)

> phones <- phones[phones$price > 1,]

(No brand name)

> phones <- filter(phones, brand != "")

(Original Price, URLs, and title removal because of irrelevance)

> phones <- select(phones, -c(3,4,5,7,10))


Editing records and columns from reviews dataset:

(Name, tilte, and body removal because of irrelevance)

> reviews <- select(reviews, -c(2,6,7))

(Chagning helpful votes from null to 0)

> reviews$helpfulVotes <- ifelse(is.na(reviews$helpfulVotes), 0,reviews$helpfulVotes)


Importing dplyr and ggplot libraries under the megalibrary "tidyverse":

(Installation)
> install.packages("tidyverse")

(Loading and attatching packages)
> library("tidyverse")


Summary of phones:

> str(phones)
> summary(phones)

- Plots of single variables:

Brand:
> phones %>%
+ ggplot(aes(brand, fill = brand))+
+ geom_bar()

Rating:
> phones %>%
+ ggplot(aes(rating))+
+ geom_histogram()

Total Reviews:
> phones %>%
+ ggplot(aes(totalReviews))+
+ geom_histogram()

Price:
> phones %>%
+ ggplot(aes(price))+
+ geom_histogram()


Summary of reviews:

> str(reviews)
> summary(reviews)

-Plots of single variables:

Rating:
> reviews %>%
+ ggplot(aes(rating))+
+ geom_histogram()

Verified:
> reviews %>%
+ ggplot(aes(verified))+
+ geom_bar()

helpfulVotes:
> reviews %>%
+ ggplot(aes(helpfulVotes))+
+ geom_bar()



ANSWERING QUESTIONS (IN README.MD):


Q1: What is the correlation between ratings and total reviews recieved?

-Creating plot to visually analyze data

> phones %>%
+ ggplot(aes(rating, totalReviews))+
+ geom_jitter()


Q2: Are reviews done at later times more helpful or not?

- Converting "date" column from string to a usable column of dates

> reviews$date <- as.Date(reviews$date, "%B %d, %Y")

-Creating plot to visual analyze data

> reviews %>%
+ ggplot(aes(date,helpfulVotes)) +
+ geom_point()+
+ facet_wrap(~verified)


Q3. For each brand, do prices correlate with how many reviews a specific product receives?

-Creating plot to visual analyze data
> phones %>%
+ group_by(brand) %>%
+ ggplot(aes(price,totalReviews, color = brand))+
+ geom_jitter()+
+ facet_wrap(~brand)


Q4. For each brand is there any correlation between average rating, and average price?

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




