# leetcode-47-medium

47.全排列 2

给定一个可包含重复数字的序列，返回所有不重复的全排列。

示例:

输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

```java
class Solution {
    //回溯递归剪枝
    List<List<Integer>>list;
    int []nums;
    public List<List<Integer>> permuteUnique(int[] nums) {
        this.nums=nums;
        list=new ArrayList<>();//排序
        Arrays.sort(nums);
        List<Integer>ll=new ArrayList<>();
        boolean []flag=new boolean[nums.length];
        dfs(ll,flag,0);
        return list;
    }
    public void dfs(List<Integer>ll,boolean[]flag,int length){
        if(length==nums.length)
        {
            list.add(new ArrayList<>(ll));
            return ;
        }
        for(int i=0;i<nums.length;i++)
        {
            if(flag[i])//重复使用的数
                continue;
            if(i>0&&nums[i-1]==nums[i]&&flag[i-1]==false)//相同序列剪枝
            {
                continue;
            }
            ll.add(nums[i]);
            flag[i]=true;
            dfs(ll,flag,length+1);
            ll.remove(ll.size()-1);
            flag[i]=false;
        }
    }
}


```

