# Social Media Sentiment Analysis with Spark SQL & DataFrames

## Overview
This project leverages PySpark and Spark SQL to analyze social media posts and user data, uncovering insights into hashtag trends, engagement patterns by age group, sentiment impact on engagement, and the top verified influencers.

## Project Structure
```
SocialMediaSentimentAnalysis/
├── input/
│   ├── posts.csv
│   └── users.csv
├── outputs/
│   ├── hashtag_trends.csv
│   ├── engagement_by_age.csv
│   ├── sentiment_engagement.csv
│   └── top_verified_users.csv
├── src/
│   ├── task1_hashtag_trends.py
│   ├── task2_engagement_by_age.py
│   ├── task3_sentiment_vs_engagement.py
│   └── task4_top_verified_users.py
├── docker-compose.yml
└── README.md
```

## Setup & Execution

### ✅ Running the Tasks Locally
```bash
cd SocialMediaSentimentAnalysis/
spark-submit src/task1_hashtag_trends.py
spark-submit src/task2_engagement_by_age.py
spark-submit src/task3_sentiment_vs_engagement.py
spark-submit src/task4_top_verified_users.py
```

### ✅ Docker Execution (Optional)
```bash
docker-compose up -d
docker exec -it spark-master bash
cd /opt/bitnami/spark/
spark-submit src/task1_hashtag_trends.py
spark-submit src/task2_engagement_by_age.py
spark-submit src/task3_sentiment_vs_engagement.py
spark-submit src/task4_top_verified_users.py
exit
docker-compose down
```

## Tasks, Approach, and Results

### 1️⃣ Hashtag Trends
- Objective: Identify the top 10 most frequently used hashtags.
- Approach:
  - Exploded Hashtags column into individual hashtags.
  - Grouped by hashtag and counted occurrences.
  - Ranked by count descending.
- Result:
  | Hashtag  | Count |
  |----------|-------|
  | #design  | 29    |
  | #cleanui | 28    |
  | #ux      | 22    |
  | #tech    | 19    |
- Insight: Design-related hashtags dominate trends. Functional tags like #bug, #fail, and #tech are also prominent.

### 2️⃣ Engagement by Age Group
- Objective: Analyze average likes and retweets by user age group.
- Approach:
  - Joined `posts.csv` and `users.csv` on `UserID`.
  - Grouped by `AgeGroup`.
  - Calculated average likes and retweets.
- Result :
  | AgeGroup | Avg_Likes | Avg_Retweets |
  |----------|----------|-------------|
  | Senior   | 82.97    | 22.75       |
  | Adult    | 71.5     | 23.19       |
- Insight: Seniors receive the highest average likes, while adults have slightly higher retweet engagement.

### 3️⃣ Sentiment vs Engagement
- Objective: Examine how sentiment impacts engagement.
- Approach:
  - Categorized sentiment into Positive (>0.3), Neutral (-0.3 to 0.3), Negative (<-0.3).
  - Calculated average likes and retweets for each sentiment.
- Result:
  | Sentiment | Avg_Likes | Avg_Retweets |
  |----------|----------|-------------|
  | Negative | 79.11    | 20.88       |
  | Neutral  | 74.72    | 25.59       |
- Insight: Surprisingly, negative sentiment posts receive the highest likes, while neutral sentiment generates more retweets.

### 4️⃣ Top Verified Users by Reach
- Objective: Identify the most influential verified users based on total reach.
- Approach:
  - Filtered verified users from `users.csv`.
  - Computed total reach as the sum of likes and retweets.
  - Sorted and extracted the top 5.
- Result :
  | Username | Total Reach |
  |----------|------------|
  | @user1   | 647        |
  | @user45  | 592        |
- Insight: Verified users have a significant reach, with @user1 leading the list.

## Final Observations & Learnings
✅ Data Handling:Utilized advanced Spark SQL techniques such as `explode`, `groupBy`, `agg`, and dataset joins.
✅ Engagement Metrics: Negative sentiment posts attract more likes, while neutral sentiment wins retweets.
✅ Trend Analysis: Design and UI-related hashtags are prevalent.
✅ erified User Influence: Verified users generally have a wider reach and higher engagement.

## 📂 Outputs Location
All outputs can be found in the `outputs/` directory:
```
- hashtag_trends.csv
- engagement_by_age.csv
- sentiment_engagement.csv
- top_verified_users.csv
```

