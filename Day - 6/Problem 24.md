# Remove K Digits

Given string num representing a non-negative integer num, and an integer k, return the smallest possible integer after removing k digits from num.

Example 1:

Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
Example 2:

Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
Example 3:

Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.

## Solution

class Solution 
{
public:

    string removeKdigits(string num, int k) {
      stack<char> s;
        for (char digit : num) {
            while (!s.empty() && s.top() > digit && k > 0) {
                s.pop();
                k--;
            }
            if (!s.empty() || digit != '0') { 
                s.push(digit);
            }
        }
        
        while (k > 0 && !s.empty()) {
            s.pop();
            k--;
        }
        
        string result;
        while (!s.empty()) {
            result.push_back(s.top());
            s.pop();
        }
        reverse(result.begin(), result.end());
        
        return result.empty() ? "0" : result;  
    }
};
