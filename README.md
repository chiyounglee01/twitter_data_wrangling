# We Rate Dogs Twitter account (@dog_rates) Data Wrangling and Visual Analysis.

## Introduction

Most people like dog pictures. They are one of the most popular content in social media. But what months are likely to have more dog pictures tweeted? What months are dog picture tweets most likely to be favorited? What does the distribution of the number of tweets by favorite count look like? We try to answer this question by examining tweet data from a popular dog picture sharing account called We Rate Dogs. In this analysis we examined the data from the period between 2015-11-15 and 2017-08-01. Only tweets with unique dog pictures were analyzed. No retweets part of this analysis.

## Data Wrangling

For this project, I had to gather, assess and clean three datasets with tweet information
from the twitter account @dog_rates, also known as We Rate Dogs.

I first directly downloaded the 'twitter-archive-enhanced.csv’ dataset.
I then used the requests library to programmatically download the ‘image_predictions.tsv’
dataset. I tried to use the tweepy library to scrap data through api keys I got from
twitter, but I could not get elevated access via the developer portal. Therefore, I 
got the data I would have gotten scraping from a link Udacity provided. The link provided a 
file called tweet_json.txt and I opened it using the read_json function.

I first started working on tidiness issues. The first task was to join the dataframes made from the 'twitter-archive-enhanced.csv’, ‘image_predictions.tsv’ and ‘tweet_json.txt’ datasets. I joined the dataframes on the columns with tweet id data. I had to left join ‘image_predictions.tsv’ and ‘tweet_json.txt’ into 'twitter-archive-enhanced.csv’. Also, the dog stage information was in 4 different columns. I had to consolidate the 4 different columns into one column called ‘dog_stages’. I had to make a function and a for loop in order to clean the data after consolidating the columns.

I then worked on quality issues with the dataframe. I first converted columns with id data that were either integers or floats into strings. I used the astype function along with lambda functions to do this task.

In the “name” column, there were 55 rows which had the value “a”. I checked one of the urls
and while the tweet was a rating of a dog picture, the dog’s name was not “a”. It seemed that
the dog’s name was mistakenly filled as ‘a’. I replace the ’a’ values with ‘None’ using the
replace function in the “name column.

Since only original ratings (no retweets) that have images were needed in the dataset,  I had to delete rows where "in_reply_to_user_id”, “in_reply_to_status_id”, "retweeted_status_id" and "retweeted_status_user_id”. I also had to delete the row of index 315 as it was a retweet of another twitter account plagiarizing We Rate Dogs. Rows with duplicated jpg urls were deleted as well as we wanted ratings of distinct images. Finally, index 35 was deleted as it did not have a  jpg url and the expanded url was not a tweet from the We Rate Dogs twitter account.

## Visual Analysis

**From the bar plot below, one can see that November and December were the month where We Rate Dogs tweeted the most dog pictures. It is probably because Thanksgiving is in November and Christmas is in December. Note that this data is from the period 2015-11-15 to 2017-08-01. Therefore, August, September and October only had one set of monthly data while all other months had two. However November and December had so many more tweets than those months that we can assume November and December have the most dog picture tweets.**

<img width="726" alt="Screen Shot 2022-04-17 at 5 30 41 PM" src="https://user-images.githubusercontent.com/90280839/163732793-4e8f9bf0-d673-4a81-8d6f-d9d4cad4448f.png">

**If one looks at the boxplot below, one can see tweets of dog pictures sent in October has the highest median favorite count. This is probably because October 31st is Halloween and there are many pictures of dogs in funny costumes.**

<img width="778" alt="Screen Shot 2022-04-17 at 5 33 18 PM" src="https://user-images.githubusercontent.com/90280839/163732836-cf8a032d-9894-4311-9bd6-204ac7a16a9e.png">

**Despite We Rate Dogs having more than 9 million followers, most tweets have less than 30,000 favorite counts. We Rate Dogs founder says he considers a tweet viral if it has 30,000 favorite counts. We can see it is hard to for a dog picture tweet to go viral.**

<img width="764" alt="Screen Shot 2022-04-17 at 5 34 43 PM" src="https://user-images.githubusercontent.com/90280839/163732863-560c4d4e-edca-4c05-98dd-708e2d5a0633.png">

## Conclusion

* **From our data analysis of the We Rate Dogs account, more dog pictures are tweeted in November and December than other months. This is probably because Thanksgiving is in November and Christmas is in December.**
* **October has the highest median favorite count for dog picture tweets. This is probably because there are many pictures of dogs in funny costumes for Halloween.**
* **The distribution of the number of tweets by favorite count is a right skewed graph. Despite the popularity of dog pictures on social media, it is hard for a dog picture to go viral.**

