---
layout: post
title: 3 Ways To Calculate User Retention Rate
category: Common Knowledge
keywords: 留存，Retention Rate, Rolling Retetion, Range Retention
---

## The 3 most popular methods are classic, range, and rolling retention.


**Classic retention**, also known as Day N or Retention by Day, is the percent of new users who come back on a specific day.

![Classic Retention](https://i1.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_1_826x350R.jpeg)

**Range retention** is similar to classic retention with a measurement period that spans multiple days

![Range Retention](https://i2.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_2_826x373R.jpeg)

**Rolling, or return retention** is the percent of new users who return on or after a specific day.

![Rolling Retention](https://i0.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_3_826x138R.jpeg)

##Classic Retention##

Imagine you have 10 users who first use your app on Monday, the first of the month. Three of those users come back the next day on Tuesday, the second of the month, and two come back the following day on Wednesday, the third of the month. Your Day 1 retention rate is 3/10 or 30%. Your Day 2 retention rate is 2/10 or 20%. If five people were to come back 89 days from Monday the 1st (not shown), your Day 90 retention rate would be 5/10 or 50%.

![经典留存率](https://i0.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_4_826x439R.jpg)

Note that the two individuals who came back on Day 2 could be all, some, or none of the three that came back on Day 1. That is to say, each day is calculated independently.  

![经典留存率用户在计量时间内都是独立计算的](https://i0.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_7_826x250R.jpg)

Benefits

 - Daily granularity
 - Easy to explain
 - Easy to calculate

Limitations

 - Sensitive to noise from whatever may be happening on a specific day
 

##Range Retention##
While any interval of time can be used, 7-day weekly ranges or 30-day monthly ranges tend to be the most common and intuitive. Let’s look at an example using a 7-day weekly range.

You have 10 new users every day for five days during the first week. On Saturday, the 6th of the month, six users come back. Some time during the subsequent week, nine unique users come back, five on the 8th and four on the 13th. In the third week, three users come back, all on the 21st. The first period retention is 9/50 or 18%. The second period retention is 3/50 or 6%.

![一定日期范围内的留存率](https://i1.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_5_826x439R.jpg)

The activity from the six visitors on the 6th is not counted because we’re looking at 7-day blocks of time and all activity in the first seven days are lumped together as the initial activity. For the same reason we wouldn’t count multiple interactions on the first day under classic retention methodology, we don’t count multiple interactions in the first week under a weekly range methodology. The concept is identical if we used a 30-day monthly range.

![计算公式](https://i2.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_8_826x250R.jpg)

Benefits

 - Smooths out some of the day-to-day noise
 - Easy to explain
 - Good for looking at trends or patterns over a longer period of time

Limitations

 - Weekly granularity means you don’t know if the activity is occurring
   at the beginning or end of the range
 - Longer lag time since you have to wait multiples of your date range
   for results

##Rolling Or Return Retention##
Sometimes you want just one simple answer. Rather than combing over how many users are coming back today vs. tomorrow, or in two weeks vs. in three weeks, you just want to know how many customers you’ve successfully built a long-term relationship with. Rolling retention gives you that one number. Of course, is has its blind spots, too, which we’ll discuss.

To understand how rolling retention is calculated, let’s go back to our example of 10 new users on the first of the month. On the 7th, user A comes back. On the 10th, user B comes back. On the 15th, user C comes back and again on the 16th. Your Day 7 retention is 3/10 or 30% because users A, B, and C all came back on Day 7 or after. Your Day 14 retention is 1/10 or 10% because only user C came back on or after Day 14.

![单位时间内及以后的留存率](https://i1.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_6_826x439R.jpg)

It doesn’t matter if a user comes back one time or 100 times after the day you’ve selected. At the same time, if you select Day 7 as the day to measure against, it doesn’t matter if the user comes back on Day 7 or Day 700.

![Rolling Retention计算公式](https://i0.wp.com/www.braze.com/wp-content/uploads/2016/10/AB1016_BLOG_USER-RETENTION_9_826x250R.jpg)

Benefits

 - Fast to calculate, requiring only two data points: date of first use
   and last use
 - Reflects the stickiness of your app in one metric

Limitations

 - Open-ended nature of methodology means the numbers can be constantly
   changing
 - Treats a daily active user the same as a user who comes back only
   once after the measurement day


Source: [The Top 3 Ways To Calculate User Retention Rate](https://www.braze.com/blog/calculate-retention-rate/)
