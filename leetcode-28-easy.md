# leetcode-28-easy

28.实现strStr()

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

示例 1:

输入: haystack = "hello", needle = "ll"
输出: 2

示例 2:

输入: haystack = "aaaaa", needle = "bba"
输出: -1

```java
class Solution {
    //双指针
    public int strStr(String haystack, String needle) {
        for (int i = 0; i <= haystack.length() - needle.length(); i++){ 
            int j = 0;
            for (;j < needle.length(); j++){
                if (haystack.charAt(i + j) != needle.charAt(j)) {
                    break;
                }
            }
            if (j == needle.length()){
                return i;
            }
        }
        return -1;
    }
};

```

