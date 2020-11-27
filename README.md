# How friends’ reviews on Yelp affect mobility 

## Abstract
In this creative extension, we aim at studying the effects of yelp reviews, and more specifically reviews from friends on mobility. We will be using a very extensive dataset provided by Yelp giving us information on businesses, users, reviews and user check-ins into certain businesses.<br>
Given that the dataset is huge, we will cut it down by focusing on businesses in California, which has a very high concentration of various businesses and many active users, as well as being a big state surface-wise with a relatively high population density.<br>
We will try to clean the data and perform various statistical analysis and plottings  in order to draw conclusions on the effect of friend’s yelp reviews on one's mobility. The intuition is that if a user’s friend has given a positive or negative review for a certain business, chances are that that friend has talked to that user about it, enabling the user to check-out or not the business, regardless if they have seen the friend’s review or not.<br>
This is another facet of the effects on friendships on short and long distance travelling, studied in the reference paper. We expect to find some similar results, that long distance mobility in particular is strongly linked to friends' presence and opinions on certain businesses.<br>

## Research Questions
A list of research questions you would like to address during the project.
- Does a positive review on a location made by a friend increases our probability to visit this place in the future. This probability will be conditioned on the distance between the location and our home
- Same question for negative reviews. 
- How likely are we to move to a friend’s home (or near a friend’s home)?

## Proposed dataset
We will be using a dataset downloaded from Yelp. The whole dataset has more than 9GB and consists of several `.json` files: `business.json`, `review.json`, `user.json` etc.
We list some main attributes that are useful for this project. For more information, please refer [here](https://www.yelp.com/dataset/documentation/main?fbclid=IwAR1RgySn5BU9FaD_5TkJ0Rxqs-hIoEQqEC5CSm9kzXka7boJj8YVTRyDvYc).
- `business.json` contains the information of the business places (i.e. restaurants). The key attributes are the id of the restaurant `business_id` and its location `state`.
- `review.json` indicates the writer of the review by `user_id`, the corresponding business place by `business_id`, the rating of the writer by `stars` and the date of the review by `date`.
- `user.json` contains user’s information, including her id `use_id`, and a list of her friends `friends`.

Since the dataset is huge and contains businesses all over the world, we will restrict the business places to California. Once we have the desired business places (i.e. `business_id`) we can find all users (i.e. `user_id`) who have rated these places by filtering `business_id` in `review.json`. In this manner, we also obtain the corresponding rating score of the user and the review date. The social network can be obtained using `friends` in `user.json`.


## Methods
- Select businesses that are located in California, US. 
Select users that gave at least one review in one of these businesses. 
Users with more than 4 reviews will be considered as living in California. 
- We will infer user’s home with the same technique used by the author of the Friendship and Mobility 
- We will try to reproduce Figure 3(a) that shows the probability that a user will travel to a friend's home as a function of distance traveled. 
This will help us answer the question: how likely are we to move to a friend’s home (or near a friend’s home)?
- We will plot the probability of visiting a place positively reviewed by a friend with respect to distance 
Same plot but for negative reviews. 
- We will perform a t-test on these distributions to see if the treatment (i.e. a positive review or negative review) has an effect compared to the control distribution (i.e. the distribution of all checkins). 

## Proposed timeline
- 01/12/20 - 06/12/20: massage the dataset and get all the relevant information. Finally, try to have the following datasets:
  - user_id mapped to its friend list 
  - user_id mapped to location rated by friends and the rating on that place 
  - user_id mapped to coordinates to location visited (this will help to infer home locations)
- 07/12/20 - 13/12/20: plot the figures
- 14/12/20 - 18/12/20: perform the t-tests and draw the conclusions

## Organization within the team
For the first week, we have divided the work amongst ourselves in the following way: 
- Paul: filter the dataset and perform some first analysis (number of users, number of check-ins, average number of check-ins per user, size of the friend’s list …)
- Malo: create the data frame user_id mapped to location rated by friends and the rating on that place 
- Xiaoyan: create the dataframe user_id mapped to coordinates to location visited (this will help to infer home locations) 
We expect during this week to spend a lot of time shaping the dataset into the correct desired way.

For the second week, we have divided the work amongst ourselves in the following way: 
- Paul & Xiaoyan : creation and analysis of figure about the distribution of visiting a place positively reviewed by a friend with respect to distance 
- Malo: reproduction of Figure 3(a) on our dataset

For the last week, we will work collectively on: 
- Perform the t-test analysis 
- Writing of the report 

## References: 
- Paper: *Friendship and Mobility: User Movement in
Location-Based Social Networks* [Source](http://ial.eecs.ucf.edu/Reading/Papers/Friendship%20and%20Mobility%20User%20Movement%20In%20Location-Based%20Social%20Networks.pdf).
- Yelp Dataset [Source](https://www.yelp.com/dataset/download).

