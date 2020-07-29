# leetcode-17-medium

17.电话号码的字母组合

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/original_images/17_telephone_keypad.png)

示例:

输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

说明:
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。



```java
class Solution {
    //dfs递归
	String[] letter_map = {" ","*","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    List<String> res = new ArrayList<>();
	public List<String> letterCombinations(String digits) {
		//边界条件
		if(digits==null || digits.length()==0) {
			return new ArrayList<>();
		}
		dfs(digits, "", 0);
		return res;
	}
	
	//递归函数
	void dfs(String str, String letter, int index) {
		if(index == str.length()) {
			res.add(letter);
			return;
		}
		char c = str.charAt(index);
		int pos = c - '0';
		String map_string = letter_map[pos];
		for(int i=0;i<map_string.length();i++) {
			//递归调用
			dfs(str, letter + map_string.charAt(i), index+1);
		}
	}
}

```

