# leetcode-93-medium

93.复原IP地址

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

有效的 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 有效的 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效的 IP 地址。

 

示例 1：

```
输入：s = "25525511135"
输出：["255.255.11.135","255.255.111.35"]
```

示例 2：

```
输入：s = "0000"
输出：["0.0.0.0"]
```

示例 3：

```
输入：s = "1111"
输出：["1.1.1.1"]
```

示例 4：

```
输入：s = "010010"
输出：["0.10.0.10","0.100.1.0"]
```

示例 5：

```
输入：s = "101023"
输出：["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```



```Java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
//回溯剪枝
public class Solution {
    //结果集
    List<String> res = new ArrayList<>();

    public List<String> restoreIpAddresses(String s) {
        //边界特判：ip地址长度4~12位
        if(s.length() < 4 || s.length() > 12) return res;

        //记录选择的路径
        List<String> track = new ArrayList<>();
        //调用回溯函数（需记录剩余待匹配的长度和ip片段数）
        backtrack(s, 0, s.length(), 4 ,track);
        return res;
    }

    /**
     * @param s         目标字符串
     * @param index     当前索引位置
     * @param len       剩余待匹配的字符串长度0~ s.length()
     * @param segments  剩余待匹配的IP片段数0~4
     * @param track     记录当前的路径
     */
    //回溯函数
    //已选路径：track记录已选的字符串 → 最后使用String.join()对集合元素进行拼接
    //选择列表：当前可选的字符串长度为1、2 、3
    //结束条件：剩余待匹配的长度和ip片段数均为 0
    public void backtrack(String s, int index, int len, int segments , List<String> track){
        //触发结束条件：深度已到达第4层，且剩余待匹配字符为0
        if(segments == 0 && len == 0){
            res.add(String.join(".", new ArrayList<String>(track)));   //将track中的字符串使用"."拼接
            return;
        }

        //边界条件：剩余待匹配的字符串
        if(len < segments || len > segments * 3){
            return;
        }

        //选择列表：当前可选的字符串长度为1、2 、3
        for(int i = 1 ; i <= 3; i++){
            //判断当前索引是否越界
            if(index + i - 1 >= s.length()) continue;
            //截取当前选择的字符串片段【包左不包右】
            String sub = s.substring(index, index + i);
            //无效ip数字串
            if(!isValidIpNum(sub)) continue;

            //作出选择
            track.add(sub);
            //System.out.println("回溯前→" + track);
            //递归调用回溯函数 → 进入决策树下一层
            backtrack(s, index + i, len - i, segments - 1, track);
            //撤销选择
            track.remove(track.size() - 1);
        }
    }

    //判断是否为有效的ip数字
    public boolean isValidIpNum(String str){
        int subLen = str.length();
        //长度在1~3之间
        if(subLen > 3 || subLen < 0){
            return false;
        }

        //长度大于1时，首字母不能为0
        if(subLen > 1 && str.charAt(0) == '0'){
            return false;
        }

        //不能超过255
        if(Integer.parseInt(str) > 255){
            return false;
        }
        return true;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        Scanner sc = new Scanner(System.in);
        String ip = sc.nextLine();

        List<String> res = sol.restoreIpAddresses(ip);
        System.out.println(res);
    }
}


```

