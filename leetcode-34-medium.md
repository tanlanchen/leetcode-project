# leetcode-34-medium

34.在排序数组中查找元素的第一个和最后一个位置

​	

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

示例 1:

输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]

示例 2:

输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]

```java
class Solution {
    //二分查找
	public int[] searchRange(int[] nums, int target) {
		if(nums==null) {
			return new int[]{-1,-1};
		}
		int firstIndex = find(true,nums,target);
		int lastIndex = find(false,nums,target);
		return new int[]{firstIndex,lastIndex};
	}
	
	//查找第一个和最后一个元素
	private int find(boolean isFindFirst,int[] nums,int target) {
		int begin = 0;
		int end = nums.length-1;
		while(begin<=end) {
			int mid = begin+(end-begin)/2;
			if(nums[mid]>target) {
				end = mid-1;
			}
			else if(nums[mid]<target) {
				begin = mid+1;
			}
			//找到目标值了，开始定位到第一个和最后一个位置
			else {
				//是查找第一个还是查找最后一个
				if(isFindFirst) {
					//如果不满足条件，缩小右边界，继续往左边查找
					if(mid>0 && nums[mid]==nums[mid-1]) {
						end = mid-1;
					} else {
						return mid;
					}
				}
				else {
					//如果不满足条件，增大左边界，继续往右边查找
					if(mid<nums.length-1 && nums[mid]==nums[mid+1]) {
						begin = mid+1;
					} else {
						return mid;
					}
				}
			}
		}
		return -1;
	}
}


```

