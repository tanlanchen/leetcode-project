# leetcode-5-medium

#### 5. 最长回文子串

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。

示例 2：

输入: "cbbd"
输出: "bb"

```java
class Solution {
    public String longestPalindrome(String s) {
        //动态规划
        if(s == null || s.equals("")){
            return s;
        }
        boolean[][] dp = new boolean[s.length()][s.length()];
        int[] result = new int[2];
        for(int i = 0; i<s.length(); i++) dp[i][i] = true;
        for(int i = s.length()-1; i>=0; i--){
            for(int j = i+1; j<s.length(); j++){
                if(s.charAt(i) == s.charAt(j)) {
                    if(j-i == 1){
                        dp[i][j] = true;
                    }
                    else{
                        dp[i][j] = dp[i+1][j-1]; 
                    }
                }else{
                    dp[i][j] = false;
                }
                if(dp[i][j]){
                    if(result[1]-result[0] <= j - i){
                        result[0] = i;
                        result[1] = j;
                    }
                }
            }
        }
        return s.substring(result[0],result[1]+1);
        
    }
}
```

