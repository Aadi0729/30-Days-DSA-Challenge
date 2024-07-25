# Binary tree level order traversal

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

Example 1:
![alt text](image.png)

Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
Example 2:

Input: root = [1]
Output: [[1]]
Example 3:

Input: root = []
Output: []
 

## Solution

class Solution 
{
public:

    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if (root == nullptr) return result;
        
        queue<TreeNode*> q;
        q.push(root);
        
        while (!q.empty()) {
            int levelSize = q.size();
            vector<int> currentLevel;
            
            for (int i = 0; i < levelSize; ++i) {
                TreeNode* currentNode = q.front();
                q.pop();
                currentLevel.push_back(currentNode->val);
                
                if (currentNode->left != nullptr) {
                    q.push(currentNode->left);
                }
                
                if (currentNode->right != nullptr) {
                    q.push(currentNode->right);
                }
            }
            
            result.push_back(currentLevel);
        }
        return result;
    }
};
