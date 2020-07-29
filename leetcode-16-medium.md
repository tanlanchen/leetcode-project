# leetcode-16-medium

16.最接近三数之和

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

 

示例：

输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。

 

提示：

    3 <= nums.length <= 10^3
    -10^3 <= nums[i] <= 10^3
    -10^4 <= target <= 10^4

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

