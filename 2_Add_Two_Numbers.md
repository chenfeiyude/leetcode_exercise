# Problem
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

# Solution 1
1. convert two linkedlist to array
2. for loop two array and add up and put into a linked list 
3. performance is too slow

```
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
        
        List<Integer> num1 = new ArrayList<>();
        num1.add(l1.val);
        while(l1.next != null) {
            l1 = l1.next;
            num1.add(l1.val);
        }
            
        List<Integer> num2 = new ArrayList<>();
        num2.add(l2.val);
        while(l2.next != null) {
            l2 = l2.next;
            num2.add(l2.val);
        }
            
        int num1Size = num1.size();
        int num2Size = num2.size();
        int maxSize = num1Size > num2Size ? num1Size : num2Size;
        
        ListNode r = null;
        ListNode curr = null;
        int n = 0;
        for(int i = 0; i < maxSize; i++) {
            int n1 = i >= num1Size?0:num1.get(i);
            int n2 = i >= num2Size?0:num2.get(i);
            int sum = n1 + n2 + n;
            
            if(curr == null)
                curr = new ListNode(sum % 10 + n);
            else
                curr.next = new ListNode(sum % 10);

            System.out.println(curr.val);
            n = sum / 10;
            if(r == null)
                r = curr;
            else {
                curr = curr.next;
            }
                
        }
        if(n > 0)
            curr.next = new ListNode(n);
        
        return r;
    }
}
```
