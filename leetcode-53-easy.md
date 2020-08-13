# leetcode-53-easy

53.最大子序和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。

进阶:

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

```java
class Solution {
    //动态规划
    public int maxSubArray(int[] nums) {
        int n = nums.length;	// 由于数组nums长度不为0，所以没有考虑n为零的情况。
        int[] dp = new int[n];	// 定义状态数组
        int ans = nums[0];		// 初始化最大值
        dp[0] = nums[0];		// 初始化状态
        for(int i = 1; i < n; i++){
            dp[i] = Math.max(nums[i], dp[i-1] + nums[i]);	// 根据状态转移方程更新数组
            ans = Math.max(ans, dp[i]); 
        }
        return ans;
    }
}


```

