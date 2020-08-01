# leetcode-22-medium

22.括号生成

数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

 

示例：

输入：n = 3
输出：[
       "((()))",
       "(()())",
       "(())()",
       "()(())",
       "()()()"
     ]

```java
class Solution {
    //深度优先搜索
    List<String> res = new ArrayList<>();
    public List<String> generateParenthesis(int n) {
        dfs(n, n, "");
        return res;
    }

    private void dfs(int left, int right, String curStr) {
        if (left == 0 && right == 0) { // 递归终止条件
            res.add(curStr);
            return;
        }

        if (left > 0) { 
            dfs(left - 1, right, curStr + "(");
        }
        if (right > left) { 
            dfs(left, right - 1, curStr + ")");
        }
    }


```

