# Convert sorted array to binary search tree

Given an integer array `nums` where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

## Solution

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {

public:

    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return func(nums, 0, nums.size() - 1);
    }
    TreeNode* func(vector<int>& nums, int left, int right) {
        if (left > right) {
            return nullptr;
        }
        int mid = left + (right - left) / 2;
        TreeNode* root = new TreeNode(nums[mid]);
        root->left = func(nums, left, mid - 1);
        root->right = func(nums, mid + 1, right);
        return root;
    }
};
