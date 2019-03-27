# Problem
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4


# Solution 1. 1ms
for loop l2 each node and insert into l1

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null)
            return l2;
        else if(l2 == null)
            return l1;
        
        ListNode r = l1;
        // both not null
        while(l2 != null) {
            ListNode temp = new ListNode(l2.val);
            while(l1.next != null && l1.next.val <= temp.val) {
                l1 = l1.next;
            }
            
            if(l1.val <= temp.val) {
                if (l1.next != null && l1.next.val > temp.val){
                    temp.next = l1.next;   
                }  
                l1.next = temp;
            }
            else {
                temp.next = l1;
                l1 = temp;
                r = l1;
            }
            
            l2 = l2.next;
        }
        
        return r;
    }
}
```
