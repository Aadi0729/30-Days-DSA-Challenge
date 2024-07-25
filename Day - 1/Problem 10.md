# Convert binary number in a linked list to integer

Given head which is a reference node to a singly-linked list. The value of each node in the linked list is either 0 or 1. The linked list holds the binary representation of a number.

Return the decimal value of the number in the linked list.

The most significant bit is at the head of the linked list.

Example 1:

![graph-1](https://github.com/user-attachments/assets/de86d529-e46e-4e73-99c2-8549635649eb)

Input: head = [1,0,1]

Output: 5

Explanation: (101) in base 2 = (5) in base 10

Example 2:

Input: head = [0]

Output: 0
 

Constraints:

The Linked List is not empty.
Number of nodes will not exceed 30.
Each node's value is either 0 or 1.
 

## Solution

class Solution 
{
public:

    int getDecimalValue(ListNode* head) {
        int decimalValue = 0;
        ListNode* current = head;
        
        while (current != NULL) {
            decimalValue = (decimalValue << 1) | current->val;
            current = current->next;
        }
        
        return decimalValue;
    }
};
