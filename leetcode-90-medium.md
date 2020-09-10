# leetcode-90-medium

90.子集 2

给定一个可能包含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:

输入: [1,2,2]
输出:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]

```java
class Solution {
    //回溯剪枝
    int n;
    List<List<Integer>> result = new LinkedList();
    Stack<Integer> path = new Stack();
    // 加上剪枝操作, 相同层, 如果当前元素与上一个元素相同, 则跳过不遍历以实现剪枝.
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        if(nums.length <= 0) return result;
        n = nums.length;
        // 先排序
        Arrays.sort(nums);
        
        dfs(nums, 0);
        
        return result;
    }
    
    public void dfs(int[] nums, int start){
        result.add(new LinkedList(path));
        
        for(int i = start; i < n; i++){
            if((i-1)>=start && nums[i-1] == nums[i]) continue;
            path.push(nums[i]);
            dfs(nums, i+1);
            path.pop();
        } 
    }
}


```

