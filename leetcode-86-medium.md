# leetcode-86-medium

86.分隔链表

给定一个链表和一个特定值 x，对链表进行分隔，使得所有小于 x 的节点都在大于或等于 x 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

示例:

输入: head = 1->4->3->2->5->2, x = 3
输出: 1->2->2->4->3->5

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
   //双指针
   public ListNode partition(ListNode head, int x) {

        ListNode one = new ListNode(0);
        ListNode one_prev = one;
        ListNode two = new ListNode(0);
        ListNode two_prev = two;


        while (head != null) {
            if (head.val < x) {
                one_prev.next = head;
                one_prev = one_prev.next;
            } else {
                two_prev.next = head;
                two_prev = two_prev.next;
            }
            head = head.next;
        }
        two_prev.next = null;

        one_prev.next = two.next;
        return one.next;
    }
}


```

