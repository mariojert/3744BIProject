SETUP:

Importing both the "prices" and "reviews".csv files into datasets in python:

> phones <- read.csv("GitHub/3744BIProject/20191226-items.csv")

> reviews <- read.csv("GitHub/3744BIProject/20191226-reviews.csv")

Removing faulty records from phones dataset:

> phones <- phones[phones$price > 1,]

Importing dplyr and ggplot libraries under the megalibrary "tidyverse":

(Installation)
> install.packages("tidyverse")

(Loading and attatching packages)
> library("tidyverse")


ANSWERING QUESTIONS (IN README.MD):

Q1: 