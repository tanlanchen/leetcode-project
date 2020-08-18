# leetcode-59-medium

59.螺旋矩阵 2

给定一个正整数 n，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

示例:

输入: 3
输出:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] ans = new int[n][n];
        int left = 0, right = n - 1, top = 0, bottom = n - 1;
        int num = 1;  //填充的元素 (初始为 1)
        while(num <= n * n){
            for(int i = left; i <= right; i++) ans[top][i] = num++;  //由左往右
            top++;
            for(int i = top; i <= bottom; i++) ans[i][right] = num++;  //从上往下
            right--;
            for(int i = right; i >= left; i--) ans[bottom][i] = num++;  //从右往左
            bottom--;
            for(int i = bottom; i >= top; i--) ans[i][left] = num++;  //从下往上
            left++;
        }
        return ans;
    }
}


```

