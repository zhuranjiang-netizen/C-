**# Convert Sorted List to Binary Search Tree**

**🔗 题目链接：**  
**[convert-sorted-list-to-binary-search-tree](https://leetcode.cn/problems/convert-sorted-list-to-binary-search-tree/description/?envType=problem-list-v2&envId=divide-and-conquer)**

---

## 链表结点定义

```cpp
/**
 * Definition for singly-linked list.
 */
struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};
/**
 * Definition for a binary tree node.
 */
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right)
        : val(x), left(left), right(right) {}
};
class Solution {
public:
    TreeNode* buildBST(vector<int>& temp, int left, int right) {
        if (left > right) {
            return nullptr;
        }

        int mid = (left + right) / 2;
        TreeNode* root = new TreeNode(temp[mid]);
        root->left = buildBST(temp, left, mid - 1);
        root->right = buildBST(temp, mid + 1, right);

        return root;
    }

    TreeNode* sortedListToBST(ListNode* head) {
        ListNode* p = head;
        vector<int> temp;

        while (p != nullptr) {
            temp.push_back(p->val);
            p = p->next;
        }

        TreeNode* root = buildBST(temp, 0, temp.size() - 1);
        return root;
    }
};
## 思路说明

采用分治和递归的思想。
由于链表是已经排好序的，而二叉搜索树具有左子树节点值小于根节点、右子树节点值大于根节点的特点，因此每次选择中间位置 mid 作为当前子树的根节点。

左右子树分别由数组中 mid 左右两部分递归构造，从而保证构造出的二叉搜索树是高度平衡的。
