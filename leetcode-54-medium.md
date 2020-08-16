# leetcode-54-medium

54.螺旋矩阵

给定一个包含 m x n 个元素的矩阵（m 行, n 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

示例 1:

输入:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
输出: [1,2,3,6,9,8,7,4,5]

示例 2:

输入:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
输出: [1,2,3,4,8,12,11,10,9,5,6,7]

```java
class Solution {
    //递归
    List<Integer> ans = new LinkedList<>();
    int[][] matrix;

    public List<Integer> spiralOrder(int[][] matrix) {
        this.matrix = matrix;
        if (matrix.length == 0) return ans;
        export(0, matrix.length - 1, 0, matrix[0].length - 1);
        return ans;
    }

    public void export(int row_start, int row_end, int col_start, int col_end){
        // 递归出口
        if (row_start > row_end || col_start > col_end) return;
        if (row_start==row_end && col_end==col_start){
            ans.add(matrix[row_start][row_end]);
            return;
        }
        if (row_end == row_start){
            for (int i = col_start; i <= col_end; ++i){
                ans.add(matrix[row_start][i]);
            }
            return;
        }
        if (col_end == col_start){
            for (int i = row_start; i <= row_end; ++i){
                ans.add(matrix[i][col_start]);
            }
            return;
        }

        // Obtain the outer elements of the matrix in a clockwise direction
        for (int i = col_start; i < col_end; ++i) {ans.add(matrix[row_start][i]);}
        
        for (int i = row_start; i < row_end; ++i) {ans.add(matrix[i][col_end]);}

        for (int i = col_end; i > col_start; --i) {ans.add(matrix[row_end][i]);}

        for (int i = row_end; i > row_start; --i) {ans.add(matrix[i][col_start]);}

        export(row_start + 1, row_end - 1, col_start + 1, col_end - 1);
    }
}


```

