### Will a Customer Accept the Coupon?

**Context**

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a subsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? How would you determine whether a driver is likely to accept a coupon?

**Overview**

The goal of this project is to use what you know about visualizations and probability distributions to distinguish between customers who accepted a driving coupon versus those that did not.

**Data**

This data comes to us from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’.  There are five different types of coupons -- less expensive restaurants (under \\$20), coffee houses, carry out & take away, bar, and more expensive restaurants (\\$20 - \\$50). 

### Data Description
Keep in mind that these values mentioned below are average values.

The attributes of this data set include:
1. User attributes
    -  Gender: male, female
    -  Age: below 21, 21 to 25, 26 to 30, etc.
    -  Marital Status: single, married partner, unmarried partner, or widowed
    -  Number of children: 0, 1, or more than 1
    -  Education: high school, bachelors degree, associates degree, or graduate degree
    -  Occupation: architecture & engineering, business & financial, etc.
    -  Annual income: less than \\$12500, \\$12500 - \\$24999, \\$25000 - \\$37499, etc.
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she buys takeaway food: 0, less than 1, 1 to 3, 4 to 8 or greater
    than 8
    -  Number of times that he/she goes to a coffee house: 0, less than 1, 1 to 3, 4 to 8 or
    greater than 8
    -  Number of times that he/she eats at a restaurant with average expense less than \\$20 per
    person: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -  Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    

2. Contextual attributes
    - Driving destination: home, work, or no urgent destination
    - Location of user, coupon and destination: we provide a map to show the geographical
    location of the user, destination, and the venue, and we mark the distance between each
    two places with time of driving. The user can see whether the venue is in the same
    direction as the destination.
    - Weather: sunny, rainy, or snowy
    - Temperature: 30F, 55F, or 80F
    - Time: 10AM, 2PM, or 6PM
    - Passenger: alone, partner, kid(s), or friend(s)


3. Coupon attributes
    - time before it expires: 2 hours or one day

### Summary of Findings

Jupyter notebook link => https://github.com/1kit/Berkeley-Practical-Application_5_1/blob/main/prompt.ipynb

### High Level Data Analysis
1. To anyalize the data, the very first step was to clean the data.
   - Eliminated duplicates
   - Dropped the 'car' column as it had 99% data missing.
   - The rest of the columns that had Nan values were converted to 'never'
2. Use a bar plot to visualize the `coupon` column
![newplot](https://github.com/1kit/Berkeley-Practical-Application_5_1/assets/11397575/80383dea-6f49-4c28-ba57-3d38e401cbf2)

3. Use a histogram to visualize the temperature column
![newplot6](https://github.com/1kit/Berkeley-Practical-Application_5_1/assets/11397575/ba77e61e-a64f-4de9-ae50-e55516d8800b)

### Investigating the Bar Coupons
Created a new `DataFrame` that contains just the bar coupons and then queried it based on the following :
1. What proportion of bar coupons were accepted?
2. Compare acceptance rate between those who went to a bar 3 or fewer times a month to those who went more
3. Compare the acceptance rate between drivers who go to a bar more than once a month and are over the age of 25 to the all others. Is there a difference?
4. Use the same process to compare the acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry.
5. Compare the acceptance rates between those drivers who:
   * go to bars more than once a month, had passengers that were not a kid, and were not widowed OR
   * go to bars more than once a month and are under the age of 30 OR
   * go to cheap restaurants more than 4 times a month and income is less than 50K
  

Based on the observations, I hypothesize the following, about drivers who accepted the bar coupons
* 40% of poeple who were offered bar coupons took it.
* Accptance rate among people who went to the bar 3 or fewer times was at 37%, while among people who went to the bar more often only accepted at the rate of 76.8%.
  This seems to indicate that people who go to bar more often like to take deals offered by the coupon.
* For people who go to bars more than 1 per month are more likely to accept the coupon if they are older than 25 years
* Similarly, for people who go to bars more than 1 per month and who are not accompanied by a kid AND if they dont work in farming/fishing/forestry are highly likely to accept the coupon. Perhaps the framing/fishing/forestry folks are out there working or doinig outdoorsy activities, rather than spending their time drinking in a bar.
* The fact that kids are not present or the person is young (<30) does increase chances of accepting coupon.
* Income does appear to make a difference. The fact that the individual is cost conscious and makes less income makes them less likely to accept the coupon.

### Investigating the Coffee House Coupons
Created a new `DataFrame` that contains just the Coffee House coupons and then queried it based on the following:
1. Find out what proportion of Coffee House coupons were accepted
2. Lets try to find out what kind of user is more likely to accept the Coffee House coupon

   Lets examine the bar chart colored by `Y`
   ![newplot-coffee](https://github.com/1kit/Berkeley-Practical-Application_5_1/assets/11397575/2bdf2642-147c-411f-b7ee-bd6dc43bfc96)

   * 49.8% of people who were offered coffee house copuons took it.

3. For <3 Coffee House visits per month

   * People who visit 1-3 months accepted the coupon at the rate of 56.2%
   * People who visit <3 months (including never) accepted the coupon at the rate of 39%
   * People who visit >3 months accepted the coupon at the rate of 45.8%

4. More drill down
   * How does age and destination affect acceptance of the coupon.
   * Lets start with a filtered dataset where we have <3 visits to coffee house (but have visited atleast once)
   Lets see the histogram based on age and color it based on destination

   ![newplot-lt3data](https://github.com/1kit/Berkeley-Practical-Application_5_1/assets/11397575/57132077-9220-4ed2-a68c-5cbbec17cb9f)


   Very clearly, the following patterns emerge. People who fit into all of the following profiles are very likely to accept a coffee house coupon
   * People who have visited a coffee house between 1-3 times in the last month AND
   * People who are <30 years of age AND
   * People who are not headed to an urgent destination (not going to work or returning home)
