# How reviews on Yelp affect mobility

## Abstract
In this creative extension, we aim at studying the effects of yelp reviews, and more specifically reviews of businesses on mobility. We will be using a very extensive dataset provided by Yelp giving information on businesses, users, reviews and user check-ins of certain businesses.<br>
Studying human mobility can be very useful for a number of applications. For instance, with this extension, we try to understand how businesses' online presence affects everyday mobility.  Specifically how friends’ reviews and average reviews for each business can influence mobility. If we are willing to travel further from home to go to a well-rated business.  This is valuable information from a business stand-point: business owners can be motivated to improve their online public image if people are willing to travel more for a well-rated business. <br>
We study the effect of the average rating of a business on the probability of long distance travel for the users. We expect that the better rated business will likely attract more users, but also users that come from further away.<br>
We then study how reviews from friends affect long distance travelling to certain businesses depending whether the review is good or not. The intuition is that if a user’s friend has given a positive or negative review for a certain business, chances are that friend has talked to that user about it, enabling the user to check-out or not the business, regardless if they have seen the friend’s review or not. We also examine how the influence of the user’s friend's review will evolve depending on the day of the week, or the category of business, which once again could be some very valuable information for businesses.<br>
This is another facet of the effects on friendships on short and long distance travelling, studied in the reference paper. We expect to find some similar results, that long distance mobility in particular is strongly linked to friends' presence and opinions on certain businesses.<br>
Finally, we study the distribution of the number of checkins per business depending on the business grade. We monitor two populations: well-graded businesses and poorly-graded businesses to see which one attracts more users. 

## Research Questions
The goal is to study: how do ratings on businesses affect mobility?

- Study the influence of mean rating of businesses on mobility. 
Do good ratings and bad ratings of businesses influence human mobility? If yes, how?

- Study of the word of mouth impact on friends’ recommendations.
How do friends’ recommendations influence our mobility? 
How likely are we to visit a friend's recommended business?

- Study of the word of mouth impact on weekdays.
Depending on the day of the week, are we more likely to travel far?
Does the influence of friend’s recommendations change depending on the day of the week ?

- Study of the word of mouth impact on categories of businesses.
Are there categories of businesses more influenced by friends reviews than others? 

- Study the 'treatment' having a good rating vs not, with methods seen in the course.
Does a good rating have an influence on the number of visits of the business?
Is there a correlation between ratings and the number of visits?


## Proposed dataset
We will be using a dataset downloaded from Yelp. The whole dataset has more than 9GB and consists of several `.json` files: `business.json`, `review.json`, `user.json` etc.
We list some main attributes that are useful for this project. For more information, please refer [here](https://www.yelp.com/dataset/documentation/main?fbclid=IwAR1RgySn5BU9FaD_5TkJ0Rxqs-hIoEQqEC5CSm9kzXka7boJj8YVTRyDvYc).
- `business.json` contains the information of the business places (i.e. restaurants). The key attributes are the id of the restaurant `business_id`, its location `state`, its mean rating `stars` and its categories `categories`.
- `review.json` indicates the writer of the review by `user_id`, the corresponding business place by `business_id`, the rating of the writer by `stars` and the date of the review by `date`.
- `user.json` contains user’s information, including her id `use_id`, and a list of her friends `friends`.

For our study, we need to infer the user's home and friends, so we only keep users who have done at least 3 reviews and have at least 3 friends. Once we load business (i.e. `business_id`) we can find all selected users (i.e. `user_id`) who have rated these places by filtering `business_id` in `review.json`. In this manner, we also obtain the corresponding rating score of the user and the review date. The social network can be obtained using `friends` in `user.json`. `Date` in `reviews.json` will be useful for studying frends' recommendations on our mobility.


## Methods
- Remove useless attributes from datasets.
- Assign each of the 1336 business subcategories a global category (among 17) - done by hand
- Select users that have done at least 3 reviews and have at least 3 friends.
- Prepare masks for each category of business so that we can achieve information conveniently.
- We will infer the user's home with the same technique used by the author of the Friendship and Mobility.
- We will plot the probability of visiting a business positively reviewed (and negatively reviewed) by all reviewers of the business with respect to distance from home.
- We will plot the probability of visiting a business positively reviewed (and negatively reviewed) by at least one friend before with respect to distance from home.
- Depending on the category of business, we will plot the probability of visiting such business positively reviewed (and negatively reviewed) with respect to distance from home.
- Depending on the day of the week, we will plot the probability of visiting a business positively reviewed (and negatively reviewed) with respect to distance from home.
- Using the methods seen in class, we will find similar categories and try to figure out whether the ratings of business will have an impact on mobility (observational studies) 

## Proposed timeline
- 01/12/20 - 06/12/20: massage the dataset and get all the relevant information. Finally, try to have the following datasets:
  - dataframe that contains only selected users (namely, users who have done at least 3 reviews and have at least 3 friends).
  - user_id mapped to its friend list.
  - user_id mapped to coordinates to location visited (this will help to infer home locations).
  - business_id mapped to its categories.
  - review_id mapped to business location.
  - review_id mapped to whether one user’s friend has reviewed the same business before, and if yes, whether the friend has given good rating or bad rating.
  - review_id mapped to the mean rating of the business.
- 07/12/20 - 13/12/20: do analysis of data in hand and discuss the results.
  - Compute probabilities of travelling in different context mentioned in section `Methods` with respect to distance from home.
  - Plot the results and discuss.
- 14/12/20 - 18/12/20: finish the project and prepare for the submission.
  - Modify `README.md` of the repository.
  - Prepare the data story.
  - Clean notebooks.
  - Submit.

## Organization within the team
For the first week, we have divided the work amongst ourselves in the following way:
- Paul
  - Study the datasets.
  - Apply the selection on users.
  - Combined useful attributes: add business location, mean rating of business, list of user’s friends, categories and so on to review dataframe.
- Malo
  - Do data wrangling.
  - Find users’ homes.
  - Compute `reviewed label` for studying impact of friends’ recommendations on mobility.
- Xiaoyan
  - Load all datasets and remove useless attributes.
  - Find travelling distance for the business location and user’s home for each review.
  - Create masks of categories for the business of each review.
- All together
  - Manually label categories of businesses in the dataframe according to `business_category_list.pdf`.

For the second week, we have divided the work amongst ourselves in the following way:
- Paul
  - Group travelling distances, and then compute the probability that we travel when a business is positively reviewed (and negatively reviewed) by **all reviewers** with respect to distance from home. Prepare plots.
  - Find “similar categories” and study the “treatment” and “non-treatment” model. Group travelling distances, computed the probability that we travel to business of such categories that is positively reviewed (and negatively reviewed) by **all reviewers** with respect to distance from home. 
- Malo
  - Group travelling distances, and then compute the probability that we travel depending on the category of business that is positively reviewed (and negatively reviewed) by **our friends** with respect to distance from home. Prepare plots.
  - Group travelling distances, and then compute the probability that we travel depending on the category of business that is positively reviewed (and negatively reviewed) by **all reviewers** with respect to distance from home. Prepare plots.
- Xiaoyan 
  - Group travelling distances, and then compute the probability that we travel to a business positively reviewed (and negatively reviewed) by **our friends** with respect to distance from home. Prepare plots.
  - Group travelling distances, and then compute the probability that we travel depending on the week day to a business positively reviewed (and negatively reviewed) by **our friends** with respect to distance from home. Prepare plots.
- All together
  - Show results to teammates and discuss.
  - annotate the sub-categories 

For the last week, we will finalize the project by collaborating:
- All together
  - Clean notebooks.
  - Correct README.md.
  - Create interactive plots for the data story.
  - Write the data story.


## References:
- [Paper](http://ial.eecs.ucf.edu/Reading/Papers/Friendship%20and%20Mobility%20User%20Movement%20In%20Location-Based%20Social%20Networks.pdf) *Friendship and Mobility: User Movement in Location-Based Social Networks*.
- [Yelp Dataset](https://www.yelp.com/dataset/download).
- [Data story](https://zxyzz.github.io/In-Reviews-We-Trust-/)



