# Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.
 
Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]
 

Constraints:

2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.
 
Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?


## Solution

class Solution {

public:

    vector<int> twoSum(vector<int>& nums, int target) {
        for(int i=0; i<nums.size(); i++){
            for(int j=i+1; j<nums.size(); j++){
                if((nums[i] + nums[j]) == target){
                    return {i,j};
                }
            }
        }
        return {};
    }
};


**Explanation of the Code**

*Function Definition:*

vector<int> twoSum(vector<int>& nums, int target): This function takes two parameters:
- nums: A reference to a vector of integers where we need to find the two numbers.
- target: The integer value that the two numbers should sum up to.

*Nested Loops:*

The function uses two nested for loops to iterate through each pair of numbers in the array nums.
- The outer loop (for(int i=0; i<nums.size(); i++)) iterates over each element in the array, starting from the first element (i=0) to the second-last element (i<nums.size()).
- The inner loop (for(int j=i+1; j<nums.size(); j++)) iterates over all subsequent elements in the array, starting from the element immediately after the current i index (j=i+1) to the last element of the array (j<nums.size()).

*Checking Sum:*

- Inside the inner loop, it checks if the sum of the current pair of elements (nums[i] and nums[j]) equals the target.
- If (nums[i] + nums[j]) == target, it means we have found the two indices (i and j) where nums[i] and nums[j] sum up to target.
- In this case, it immediately returns a vector containing these two indices: {i, j}.

*Default Return:*

If no such pair is found after examining all pairs in the array, it returns an empty vector {} indicating no solution was found.

**Complexity:**

*Time Complexity*
- The time complexity of this solution is **O(n²)**, where n is the number of elements in the array nums. This is because of the nested loops that examine each pair of elements.

*Space Complexity*
- The space complexity is **O(1)** since it uses only a constant amount of extra space.

**Improvement:**

- While this brute-force solution works, it's not optimal for large inputs. For a more efficient solution with 
*𝑂(𝑛)* time complexity, we can use a hash map (unordered_map in C++) to store each element's index as you iterate through the array. This allows us to check if the complement of the current element (needed to reach the target) has been seen before in constant time.


## Optimized solution:

class Solution {

public:

    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> numMap;
        vector<int> result;
        
        for (int i = 0; i < nums.size(); ++i) {
            int complement = target - nums[i];
            
            if (numMap.find(complement) != numMap.end()) {
                result.push_back(numMap[complement]);
                result.push_back(i);
                return result;
            }
            numMap[nums[i]] = i;
        }
        return result;
    }
};

**Complexity:**

*Time Complexity:* $𝑂(𝑛)$

- We traverse the list containing 'n' elements exactly twice. The hashmap allows for $𝑂(1)$ average time complexity lookups.

*Space Complexity:* $𝑂(𝑛)$

- The extra space required depends on the number of elements stored in the hashmap, which can be up to 'n' in the worst case if no pairs are found.
