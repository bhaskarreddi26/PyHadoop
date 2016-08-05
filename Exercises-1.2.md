Problems

Problem 1: The following is data of few users. It cotains four columns (userid, date, item1 and item2). Find each user's latest day's records?

Input

val data="""
user date      item1 item2
1    2015-12-01 14  5.6
1    2015-12-01 10  0.6
1    2015-12-02 8   9.4
1    2015-12-02 90  1.3
2    2015-12-01 30  0.3
2    2015-12-01 89  1.2
2    2015-12-30 70  1.9
2    2015-12-31 20  2.5
3    2015-12-01 19  9.3
3    2015-12-01 40  2.3
3    2015-12-02 13  1.4
3    2015-12-02 50  1.0
3    2015-12-02 19  7.8
"""
Expected output

For user 1, the latest date is 2015-12-02 and he has two records for that particular date.
For user 2, the latest date is 2015-12-31 and he has two records for that particular date.
For user 3, the latest date is 2015-12-02 and he has three records for that particular date.
Problem 2: From the tweet data set here, find the following (This is my own solution version of excellent article: Getting started with Spark in practice)

all the tweets by user
how many tweets each user has
all the persons mentioned on tweets
Count how many times each person is mentioned
Find the 10 most mentioned persons
Find all the hashtags mentioned on a tweet
Count how many times each hashtag is mentioned
Find the 10 most popular Hashtags
Input sample

{
   "id":"572692378957430785",
   "user":"Srkian_nishu :)",
   "text":"@always_nidhi @YouTube no i dnt understand bt i loved the music nd their dance awesome all the song of this mve is rocking",
   "place":"Orissa",
   "country":"India"
}
{
   "id":"572575240615796737",
   "user":"TagineDiningGlobal",
   "text":"@OnlyDancers Bellydancing this Friday with live music call 646-373-6265 http://t.co/BxZLdiIVM0",
   "place":"Manhattan",
   "country":"United States"
}
Problem 3: Demonstrate data virtualization capabilities of SparkSQL by joining data across different data stores i.e. rdbms, parquet, avro
