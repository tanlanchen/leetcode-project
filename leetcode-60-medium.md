# leetcode-60-medium

60.第k个排列

给出集合 [1,2,3,…,n]，其所有元素共有 n! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：

    "123"
    "132"
    "213"
    "231"
    "312"
    "321"

给定 n 和 k，返回第 k 个排列。

说明：

    给定 n 的范围是 [1, 9]。
    给定 k 的范围是[1,  n!]。

示例 1:

输入: n = 3, k = 3
输出: "213"

示例 2:

输入: n = 4, k = 9
输出: "2314"

```java
import java.util.LinkedList;
import java.util.List;
class Solution {
    //回溯
    public String getPermutation(int n, int k) {
        boolean[] visited = new boolean[n];
        List<Integer> a = backTrace(n, k, visited, new LinkedList<>());
        StringBuilder sb = new StringBuilder();
        for (Integer integer : a) {
            sb.append(integer);
        }
        return sb.toString();
    }


    private volatile int count;

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.getPermutation(5, 2));
    }


    private LinkedList<Integer> backTrace(int n, int k , boolean[] visited, LinkedList<Integer> result) {
        if (result.size() == n) {
            ++count;
            return result;
        }
        for (int i = 1; i <= n; i++) {
            if (!visited[i - 1]) {
                visited[i - 1] = true;
                result.add(i);
                result = backTrace(n, k, visited, result);
                if (count == k) {
                    return result;
                }
                visited[i - 1] = false;
                result.removeLast();
            }
        }
        return result;
    }

}

```

