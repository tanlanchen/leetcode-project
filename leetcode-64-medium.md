# leetcode-64-medium

64.最小路径和

给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。

示例:

输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。

```java
class Solution {
    //动态规划
    public int minPathSum(int[][] grid){
        int row = grid.length; 
        if(row == 0)    return 0;
        int col = grid[0].length, INF = 0x3f3f3f3f;
        int[][] dp = new int[row + 1][col + 1];
        for(int i = 0; i <= row; i++) Arrays.fill(dp[i], INF);
        dp[0][1] = dp[1][0] = 0;
        for(int i = 1; i <= row; i++){
            for(int j = 1; j <= col; j++){
                dp[i][j] = Math.min(dp[i][j - 1], dp[i - 1][j]) + grid[i - 1][j - 1];
            }
        }
        return dp[row][col];
    }
}


```

