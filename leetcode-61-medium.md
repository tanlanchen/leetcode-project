# leetcode-61-medium

61.旋转链表

给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
示例 2:

输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL



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
    public ListNode rotateRight(ListNode head, int k) {

        if(head == null || head.next == null || k == 0) {
            return head;
        }
        int length = 0;
        ListNode tempLength = head;
        while(true) {
            length++;
            if(tempLength.next == null) {
                break;
            }
            tempLength = tempLength.next;
        }
        int changSize = k % length;
        int goSize = length - changSize - 1;
        if(changSize == 0) {
            return head;
        }

        ListNode temp = head;
        ListNode cur = head;
        for(int i = 1; i <= goSize; i++) {
            temp = temp.next;
        }
        for(int i = 1; i <= length - 1; i++) {
            cur = cur.next;
        }

        ListNode newHead = temp.next;
        temp.next = null;
        cur.next = head;

        return newHead;
    }
}

```



