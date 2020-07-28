

# leetcode-15-medium

15.三数之和

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

 

示例：

给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]



```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        //排序+双指针
        Arrays.sort(nums);
 	    int closedNum = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < nums.length - 2; i++) {
            if (i == 0 || (i > 0 && nums[i] != nums[i - 1])) {  // 跳过重复的答案
                int l = i + 1, r = nums.length - 1, sum = target - nums[i];
                while (l < r) {
                    if (Math.abs(nums[l] + nums[r] - sum) < Math.abs(closedNum-target)) {
                        closedNum = nums[l] + nums[r] + nums[i];
                        while (l < r && nums[l] == nums[l + 1]) l++;
                        while (l < r && nums[r] == nums[r - 1]) r--;
                        l++;
                        r--;
                    }
                    if (nums[l] + nums[r] < sum) {
                        while (l < r && nums[l] == nums[l + 1]) l++;  
                        l++;
                    } else if(nums[l] + nums[r] > sum) {
                        while (l < r && nums[r] == nums[r - 1]) r--;
                        r--;
                    }
                    else{
                        return target;//相等直接返回
                    }
                }
            }
        }
        return closedNum;
    }
}
```

