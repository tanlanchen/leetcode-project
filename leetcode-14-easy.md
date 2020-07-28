# leetcode-14-easy

14.最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:

输入: ["flower","flow","flight"]
输出: "fl"

示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。

说明:

所有输入只包含小写字母 a-z 。



```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length <1 ) return "";
        //第一个参数,以其为标准
        String str0 = strs[0];
        if ("".equals(str0)) return "";
        char[] str = str0.toCharArray();
        
        for (int j = 0; j < str.length; j++) {
            for (int i = 1; i < strs.length; i++) {
                //如果后面元素i长度不够执行本次循环，说明元素i完全满足，直接返回
                if (strs[i].length() < j+1) {
                    return strs[i];
                }

                if (str[j] == strs[i].charAt(j)) {
                    //正常情况，匹配到了
                    continue;
                } else {
                    //匹配失败，直接截取返回
                    return str0.substring(0, j);
                }
            }
        }
        //元素0遍历完了，说明第一个元素就是
        return str0;

    }
```

