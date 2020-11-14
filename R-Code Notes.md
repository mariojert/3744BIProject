SETUP:

Importing both the "prices" and "reviews".csv files into datasets in python:

> phones <- read.csv("GitHub/3744BIProject/20191226-items.csv")

> reviews <- read.csv("GitHub/3744BIProject/20191226-reviews.csv")




Removing faulty records from phones dataset:

(Incorrect prices)

> phones <- phones[phones$price > 1,]

(No brand name)

> phones <- filter(phones, brand != "")




Importing dplyr and ggplot libraries under the megalibrary "tidyverse":

(Installation)
> install.packages("tidyverse")

(Loading and attatching packages)
> library("tidyverse")




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

Q3. For each brand is there any correlation between average rating, and average price?

-Creating plot to visual analyze data

> phones %>%
+ group_by(brand) %>%
+ summarize(avg_rating = mean(rating, na.rm = TRUE) , avg_price = mean(price, na.rm = TRUE)) %>%
+ ggplot(aes(avg_rating, avg_price)) +
+ geom_line()

-List of brands, average ratings and average prices

> phones %>%
+ group_by(brand) %>%
+ summarize(avg_rating = mean(rating, na.rm = TRUE) , avg_price = mean(price, na.rm = TRUE)) %>%
+ arrange(desc(avg_price))

Q4. For each brand do prices correlate with how many reviews a specific product receives?
