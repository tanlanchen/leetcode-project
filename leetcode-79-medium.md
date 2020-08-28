# leetcode-79-medium

79.单词搜索

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

示例:

board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false


提示：

board 和 word 中只包含大写和小写英文字母。
1 <= board.length <= 200
1 <= board[i].length <= 200
1 <= word.length <= 10^3

```java
class Solution {
    //dfs+回溯剪枝
    boolean[][] visted;
    int x, y;
    //四个方向
    int[][] d = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};

    public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0 || word == null) {
            return false;
        }
        x = board.length;
        y = board[0].length;
        visted = new boolean[x][y];
        for (int i = 0; i < x; i++) {
            for (int j = 0; j < y; j++) {
                //尝试从每一个点出发进行搜索，如果搜索到了就表明存在这个单词，直接返回true
                if (process(board, i, j, word, 0)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean process(char[][] board, int row, int col, String word, int index) {
        //终止条件
        if (index == word.length() - 1) {
            return board[row][col] == word.charAt(index);
        }
        if (board[row][col] == word.charAt(index)) {
            visted[row][col] = true;
            //分别从四个方向进行搜索
            for (int i = 0; i < 4; i++) {
                int newRow = row + d[i][0];
                int newCol = col + d[i][1];
                //能够递归需满足位置未越界并且未被访问这样的条件
                if (legal(newRow, newCol) && !visted[newRow][newCol] && process(board, newRow, newCol, word, index + 1)) {
                    return true;
                }
            }
            //回溯
            visted[row][col] = false;
        }
        return false;
    }

    //判断位置是否越界
    private boolean legal(int row, int col) {
        return row >= 0 && row < x && col >= 0 && col < y;
    }

}
```

