# leetcode-62-medium

62.不同的路径

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)

例如，上图是一个7 x 3 的网格。有多少可能的路径？

```java
class Solution {
    public int uniquePaths(int m, int n) {
        //动态规划
        int[][] dp = new int[m + 1][n + 1];
        for(int i = 1;i <= m;i ++){
            for(int j = 1;j <= n;j ++){
                if(i == 1 && j == 1){
                    dp[i][j] = 1;
                }
                else dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m][n];
    }
}


```

