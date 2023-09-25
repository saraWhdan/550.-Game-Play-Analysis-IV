# 550. Game Play Analysis IV
### Problem Link:[ Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/description/?envType=study-plan-v2&envId=top-sql-50)
## Solution 
```sql
/* Write your T-SQL query statement below */

WITH FirstLogins AS (
    SELECT
        player_id,
        MIN(event_date) AS first_login_date
    FROM
        activity
    GROUP BY
        player_id
)

SELECT
    ROUND(
        SUM(
            CASE WHEN DATEDIFF(day, fl.first_login_date, a.event_date) = 1 THEN 1.0 ELSE 0 END
        ) / COUNT(DISTINCT fl.player_id), 2
    ) AS fraction
FROM
    activity a
INNER JOIN
    FirstLogins fl ON a.player_id = fl.player_id;
