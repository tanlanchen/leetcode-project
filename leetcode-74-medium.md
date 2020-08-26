# leetcode-74-medium

74.搜索二维矩阵

编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

每行中的整数从左到右按升序排列。
每行的第一个整数大于前一行的最后一个整数。
示例 1:

输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
输出: true
示例 2:

输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
输出: false

```java
class Solution {
    //两次二分查找
    public boolean searchMatrix(int[][] matrix, int target) {
        //判空
        if(matrix == null || matrix.length == 0 || 
            matrix[0] == null || matrix[0].length == 0) {
            return false;
        }
        //二分查找首列，双指针
        int left = 0;
        int right = matrix.length - 1;
        while(left < right) {
            int mid = (left + right) / 2;
            if(matrix[mid][0] == target) {
                return true;
            } else if(matrix[mid][0] > target) {
                right = mid-1;
            } else {
                left = mid+1;
            }
        }
        if(matrix[left][0] == target) {
            return true;
        } else if(matrix[left][0] > target && left > 0) {   //要查找left的上一行
            return search(matrix[left-1], target);
        } else if(matrix[left][0] < target) {   //查找left所在行
            return search(matrix[left], target);
        }
        return false;
    }
    //在一行中再次二分查找
    private boolean search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left < right) {
            int mid = (left + right) / 2;
            if(nums[mid] == target) {
                return true;
            } else if(nums[mid] > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        if(nums[left] == target) {
            return true;
        }
        return false;
    }
}

```

