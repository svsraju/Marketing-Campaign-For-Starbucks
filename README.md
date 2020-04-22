# Marketing Campaign for Starbucks
## Motivation

The name **Starbucks** needs no introduction. It is well known american coffee comapany chain. Personally I am a constant customer at Starbucks, one of the reasons which made this project interesting. Also, the data and the problem we will dealing with is a real-life like situation or use-case. This project gave me an opportunity to explore my data science skills to solve any given problem.

## I. Understanding the Business

**Starbucks Corporation** is an American multinational chain of coffeehouses and roastery reserves headquartered in Seattle, Washington. As the largest coffeehouse in the world, Starbucks is seen to be the main representation of the United States' second wave of coffee culture.ell pre-packaged food items, hot and cold sandwiches, and drinkware including mugs and tumblers; select "Starbucks Evenings" locations offer beer, wine, and appetizers. Starbucks-brand coffee, ice cream, and bottled cold coffee drinks are also sold at grocery stores. Source - [Wikipedia](https://en.wikipedia.org/wiki/Starbucks).

### - Introduction 

Once every few days, Starbucks sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). Some users might not receive any offer during certain weeks.Not all users receive the same offer.

- Given data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks actually sells dozens of products. It contains simulated data that mimics customer behavior on the Starbucks rewards mobile app.
- The **goal** is to combine transaction, demographic and offer data to determine which demographic groups respond best to which offer type.
- Every offer has a validity period before the offer expires. As an example, a BOGO offer might be valid for only 5 days. It is obeserved that in the data set that informational offers have a validity period even though these ads are merely providing information about a product
- for example, if an informational offer has 7 days of validity, one can assume the customer is feeling the influence of the offer for 7 days after receiving the advertisement.

The given transactional data shows user purchases made on the app including the timestamp of purchase and the amount of money spent on a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user actually views the offer. There are also records for when a user completes an offer. 

- **what questions do we have?**
Can we predict the amount that customers will be spending based on demographics and offer type?
Can we design a personalized offer_type for each customer, which can help in sending the personalized offer?

## II. Data Understanding

The data is contained in three files:

* `portfolio.json` - containing offer ids and meta data about each offer (duration, type, etc.)
* `profile.json` - demographic data for each customer
* `transcript.json` - records for transactions, offers received, offers viewed, and offers completed

Here is the schema and explanation of each variable in the files:

**Dataset 1: `portfolio.json`**
* id (string) - offer id
* offer_type (string) - type of offer ie BOGO, discount, informational
* difficulty (int) - minimum required spend to complete an offer
* reward (int) - reward given for completing an offer
* duration (int) - time for offer to be open, in days
* channels (list of strings)

**Dataset 2: `profile.json`**
* age (int) - age of the customer 
* became_member_on (int) - date when customer created an app account
* gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
* id (str) - customer id
* income (float) - customer's income

**Dataset 3: `transcript.json`**
* event (str) - record description (ie transaction, offer received, offer viewed, etc.)
* person (str) - customer id
* time (int) - time in hours since start of test. The data begins at time t=0
* value - (dict of strings) - either an offer id or transaction amount depending on the record


## III. Cleaning the Data

After performing necessary exploratory data analysis and other cleaning tasks(check the notebook for looking into details of cleaning)I have merged the three dataset into one. Further, I have split this dataset into two parts. 
1. Dataframe consisting of all the data related to Offers (`offers`)
2. Dataframe consisting of all the data related to Transactions (`transactions`)
I have used Label Encoding to label the categorical variables accordingly.

- Offers data shows all the offers that were sent to the customer along with the type of offer.
- The given transactional data shows user purchases made on the app including the timestamp of purchase and the amount of money spent on    a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user           actually views the offer. There are also records for when a user completes an offer.

## IV Answering the Questions
### Supervised Learning:
**Predicting the amount that will be spent by Customer**
#### Regression:
Using `transactions`,a supervised learning model is built to predict the amount a customer will spend in future on various offers.
I have used Linear Regression and Decision Tree regressor to fit the model.
Both the models performed well on the data, and I got rmse of 6.6 for Linear regressor and 6.4 for Decision Tree.

**Designing a personalized offer_type for each customer, which can help in sending the personalized offer**
#### classification:
I have designed this into a classification problem where we will be classifying the offer_type column based on other features.
I have built Logistic Regression Using GridSearch CV and KNN Classifier to check their performance on our data.
Logistic Regression was overfitting on the data, as we have a perfect accuracy score of 1.0


K Nearest Neighbours Classification is chosen after training the data on various classifiers because KNN Classifier does not overfit and gives good testing accuracy around `73%`

## Acknowledgments
Thank you to Udacity for such amazing opportunity and lessons. Thank you the Starbucks for sharing this use case and the simulated data.

**Check out [my blog](https://medium.com/@sagisv/marketing-campaign-for-starbucks-c29ae8324db6) on Medium!**

