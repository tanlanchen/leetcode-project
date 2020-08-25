# leetcode-73-medium

73.矩阵置零

给定一个 m x n 的矩阵，如果一个元素为 0，则将其所在行和列的所有元素都设为 0。请使用原地算法。

示例 1:

输入: 
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
输出: 
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
示例 2:

输入: 
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
输出: 
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
进阶:

一个直接的解决方案是使用  O(mn) 的额外空间，但这并不是一个好的解决方案。
一个简单的改进方案是使用 O(m + n) 的额外空间，但这仍然不是最好的解决方案。
你能想出一个常数空间的解决方案吗？

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        //时间换空间，空间O(1)
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }
        //单独处理第一行
        boolean firstRow = false; 
        for (int i = 0; i < matrix[0].length; ++i) {
            if (matrix[0][i] == 0) {
                firstRow = true;
            }
        }
        //单独处理第一列
        boolean firstCol = false;
        for (int i = 0; i < matrix.length; i++) {
            if (matrix[i][0] == 0) {
                firstCol = true;
            }
        }
        //遍历数组如果matrix[i][j] == 0，则将matrix[0][j]、matrix[i][0]都置为0。
        for (int i = 1; i < matrix.length; ++i) {
            for (int j = 1; j < matrix[0].length; ++j) {
                if (matrix[i][j] == 0) {
                    matrix[0][j] = 0;
                    matrix[i][0] = 0;
                }
            }
        }
        //再遍历第一行，如果matrix[0][j] == 0，则将该列都置0
        for (int i = 1; i < matrix[0].length; ++i) {
            if (matrix[0][i] == 0) {
                zeroOneCol(matrix, i);
            }
        }
        //再遍历第一列，如果matrix[j][0] == 0，则将该行都置0
        for (int i = 1; i < matrix.length; ++i) {
            if (matrix[i][0] == 0) {
                zeroOneRow(matrix, i);
            }
        }
        //单独处理第一行
        if (firstRow) {
            zeroOneRow(matrix, 0);
        }
        if (firstCol) {
            zeroOneCol(matrix, 0);
        }
    }
    //将一行置0
    private void zeroOneRow(int[][] matrix, int row) {
        for (int i = 0; i < matrix[0].length; ++i) {
            matrix[row][i] = 0;
        }
    }

    //将一列置0
    private void zeroOneCol(int[][] matrix, int col) {
        for (int i = 0; i < matrix.length; ++i) {
            matrix[i][col] = 0;
        }

    }
}


```

