# Remove Nth node from end of the list

Given the head of a linked list, remove the nth node from the end of the list and return its head.

Example 1:
 
![remove_ex1](https://github.com/user-attachments/assets/c01e676c-61c5-4754-a893-4460880f35f6)

Input: head = [1,2,3,4,5], n = 2

Output: [1,2,3,5]

Example 2:

Input: head = [1], n = 1

Output: []

Example 3:

Input: head = [1,2], n = 1

Output: [1]
 

Constraints:

The number of nodes in the list is sz.
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz
 

Follow up: Could you do this in one pass?


## Solution

class Solution 
{
public:

    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0); 
        dummy->next = head;
        ListNode* first = dummy;
        ListNode* second = dummy;

        for (int i = 0; i <= n; ++i) {
            second = second->next;
        }

        while (second != nullptr) {
            first = first->next;
            second = second->next;
        }

        ListNode* nodeToDelete = first->next;
        first->next = first->next->next;

        delete nodeToDelete; 

        ListNode* newHead = dummy->next;
        delete dummy; 
        return newHead;
    }
};
