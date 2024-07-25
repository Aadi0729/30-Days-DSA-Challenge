# Maximum Subarray

Given an integer array nums, find the subarray with the largest sum, and return its sum.

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
Example 2:

Input: nums = [1]
Output: 1
Explanation: The subarray [1] has the largest sum 1.
Example 3:

Input: nums = [5,4,-1,7,8]
Output: 23
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
 

Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.


## Solution

class Solution 
{
public:

    int maxSubArray(vector<int>& nums) {
        return maxSubArrayDivideAndConquer(nums, 0, nums.size() - 1);
    }
private:

    int maxCrossingSum(const vector<int>& nums, int left, int mid, int right) {
        int leftSum = INT_MIN;
        int sum = 0;
        for (int i = mid; i >= left; --i) {
            sum += nums[i];
            if (sum > leftSum) {
                leftSum = sum;
            }
        }
        
        int rightSum = INT_MIN;
        sum = 0;
        for (int i = mid + 1; i <= right; ++i) {
            sum += nums[i];
            if (sum > rightSum) {
                rightSum = sum;
            }
        }

        return leftSum + rightSum;
    }

    int maxSubArrayDivideAndConquer(const vector<int>& nums, int left, int right) {
        if (left == right) {
            return nums[left];
        }

        int mid = left + (right - left) / 2;

        int leftSum = maxSubArrayDivideAndConquer(nums, left, mid);
        int rightSum = maxSubArrayDivideAndConquer(nums, mid + 1, right);
        int crossSum = maxCrossingSum(nums, left, mid, right);
        return max(max(leftSum, rightSum), crossSum);
    }
};
