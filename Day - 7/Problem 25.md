# Sum of Subarray Minimums

Given an array of integers arr, find the sum of min(b), where b ranges over every (contiguous) subarray of arr. Since the answer may be large, return the answer modulo 109 + 7.

## Solution

class Solution 
{
public:

    int sumSubarrayMins(vector<int>& arr) {
        int n = arr.size();
        vector<int> prev(n), next(n);
        stack<int> s;
        const int MOD = 1e9 + 7;

        for (int i = 0; i < n; i++) {
            while (!s.empty() && arr[s.top()] >= arr[i]) {
                s.pop();
            }
            prev[i] = s.empty() ? -1 : s.top();
            s.push(i);
        }

        while (!s.empty()) {
            s.pop();
        }

        for (int i = n - 1; i >= 0; --i) {
            while (!s.empty() && arr[s.top()] > arr[i]) {
                s.pop();
            }
            next[i] = s.empty() ? n : s.top();
            s.push(i);
        }

        long long result = 0;
        for (int i = 0; i < n; ++i) {
            long long leftCount = i - prev[i];
            long long rightCount = next[i] - i;
            result = (result + arr[i] * leftCount * rightCount) % MOD;
        }

        return result;
    }
};
