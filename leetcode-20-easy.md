# leetcode-20-easy

20.有效的括号

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

    左括号必须用相同类型的右括号闭合。
    左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

示例 1:

输入: "()"
输出: true

示例 2:

输入: "()[]{}"
输出: true

示例 3:

输入: "(]"
输出: false

示例 4:

输入: "([)]"
输出: false

示例 5:

输入: "{[]}"
输出: true



```java
class Solution {
    public boolean isValid(String s) {
        //栈
        Stack<Character> stack = new Stack<Character>();
        int len = s.length();
        if (len==0||s.isEmpty()){
            return true;
        }
        if (len%2==1)
            return false;
        stack.push(s.charAt(0));
        for (int i = 1; i < len; i++) {
            char cur = s.charAt(i);
            if (cur=='('||cur=='['||cur=='{'){
                stack.push(cur);
            }
            if ((cur==')'||cur==']'||cur=='}')&&stack.isEmpty()){
                return false;
            }
            if (cur==')'&&!stack.isEmpty()){
                if (stack.pop()!='(')
                    return false;
            }
            if (cur==']'&&!stack.isEmpty()){
                if (stack.pop()!='[')
                    return false;
            }
            if (cur=='}'&&!stack.isEmpty()){
                if (stack.pop()!='{')
                    return false;
            }
        }
        return stack.isEmpty();
    }
}

```

