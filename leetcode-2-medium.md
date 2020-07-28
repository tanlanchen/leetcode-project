# leetcode-2-medium

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807



```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //链表
        ListNode node = new ListNode(0);
        ListNode p = l1,q = l2,curr = node;
        int number = 0;
        int data1 = 0;
        int data2 = 0;
        while(p != null || q != null || number != 0){
            if(p == null){
                data1 = 0;
            } else {
                data1 = p.val;
                p = p.next;
            }
            if(q == null){
                data2 = 0;
            } else {
                data2 = q.val;
                q = q.next;
            }
            
            curr.next = new ListNode((data1 + data2 + number) % 10);
            curr = curr.next;
            number = (data1 + data2 + number) / 10;
        }
        return node.next;
    }
}
```

