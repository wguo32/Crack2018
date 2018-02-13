The demons had captured the princess \(**P**\) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight \(**K**\) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health \(negativeintegers\) upon entering these rooms; other rooms are either empty \(0's\) or contain magic orbs that increase the knight's health \(positiveintegers\).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

**Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.**

For example, given the dungeon below, the initial health of the knight must be at least**7**if he follows the optimal path`RIGHT-> RIGHT -> DOWN -> DOWN`.

|  |
| :--- |


| -2 \(K\) | -3 | 3 |
| :--- | :--- | :--- |
| -5 | -10 | 1 |
| 10 | 30 | -5 \(P\) |

  
Idea:

```
倒过来DP
```

Solution: 

```cpp
int calculateMinimumHP(vector<vector<int>>& dungeon) {
    if (dungeon.size() == 0 || dungeon[0].size() == 0) return 0;
    int m = dungeon.size(), n = dungeon[0].size();
    vector<vector<int>> dp(m, vector<int>(n, 0));
    for (int i = m - 1; i >= 0; i--) {
        for (int j = n - 1; j >= 0; j--) {
            dp[i][j] = dungeon[i][j];
            if (i < m - 1 && j < n - 1) dp[i][j] += max(dp[i+1][j], dp[i][j+1]);
            else if (i < m - 1) dp[i][j] += dp[i+1][j];
            else if (j < n - 1) dp[i][j] += dp[i][j+1];
            dp[i][j] = dp[i][j] > 0 ? 0 : dp[i][j];
        }
    }
    return dp[0][0] >= 0 ? 1 : 1 - dp[0][0];
}
```


