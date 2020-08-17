# leetcode-56-medium

56.合并区间

给出一个区间的集合，请合并所有重叠的区间。

 

示例 1:

输入: intervals = [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].

示例 2:

输入: intervals = [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。

注意：输入类型已于2019年4月15日更改。 请重置默认代码定义以获取新方法签名。

 

提示：

    intervals[i][0] <= intervals[i][1]

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        if(intervals==null || intervals.length==0) {
            return intervals;
        }
        //先按区间的一个元素排序一遍
        Arrays.sort(intervals, (x,y)->x[0]-y[0] );
        List<int[]> arr = new ArrayList<int[]>();
        arr.add(intervals[0]);
        for(int i=1;i<intervals.length;++i) {
            //[x1,x2]和[y1,y2]比较，如果x2<y1说明这两个区间不想交
            if(arr.get(arr.size()-1)[1] < intervals[i][0]) {
                arr.add(intervals[i]);
            }
            //否则，将这两个区间合并为 [x1,max(x2,y2)]
            else {
                arr.get(arr.size()-1)[1] = Math.max(arr.get(arr.size()-1)[1],intervals[i][1]);
            }
        }
        return arr.toArray(new int[arr.size()][2]);
    }

}
```



