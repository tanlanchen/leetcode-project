# leetcode-46-medium

46.全排列

给定一个 没有重复 数字的序列，返回其所有可能的全排列。

示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]

```java
class Solution {
    //递归回溯
    List<List<Integer>> ans = new LinkedList<>();  
    public List<List<Integer>> permute(int[] nums) {
        LinkedList<Integer> path = new LinkedList<>();  // 路径
        backtrack(nums, path);  
        return ans;
    }

    public void backtrack(int[] nums, LinkedList<Integer> path) {
        // 结束条件
        if (path.size() == nums.length) {
            ans.add(new LinkedList(path));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (path.contains(nums[i])) {   
                continue;   // 重复数字跳过
            }
            path.add(nums[i]);  // 当前位做选择
            backtrack(nums, path);  // 继续对下一位选择
            // 下一位无法选择递归返回了且没满足结束条件
            // 说明当前位的选择导致了下一位无论怎么选都不能到达结束条件
            // 所以当前位的选择是错误的，撤销当前位选择
            path.removeLast();  
        }
    }
}


```

