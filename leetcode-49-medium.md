# leetcode-49-medium

49.字母异位词分组

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

示例:

输入: ["eat", "tea", "tan", "ate", "nat", "bat"]
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]

说明：

    所有输入均为小写字母。
    不考虑答案输出的顺序。

```java
class Solution {
    //HashMap比较字母出现次数
    public List<List<String>> groupAnagrams(String[] strs) {
		if (strs == null || strs.length == 0){
            return new ArrayList<>();
        }
        Map<String,List<String>> map = new HashMap<>();
         for (String str : strs) {
            int[] table = new int[26];
            for (int i = 0; i < str.length(); i++) {
                table[str.charAt(i) - 'a']++;
            }
            StringBuffer keySb = new StringBuffer();
            for (int i = 0; i < 26; i++) {
                if(table[i] == 0){
                    continue;
                }
                keySb.append((char)('a'+i)).append(table[i]);
            }
            String key = keySb.toString();
            if (map.containsKey(key)) {
                map.get(key).add(str);
            } else {
                List<String> list = new ArrayList<>();
                list.add(str);
                map.put(key, list);
            }
        }

        return new ArrayList<>(map.values());
    }
}
```

