# [199. 二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view)

[English Version](/solution/0100-0199/0199.Binary%20Tree%20Right%20Side%20View/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给定一个二叉树的 <strong>根节点</strong> <code>root</code>，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。</p>

<p> </p>

<p><strong>示例 1:</strong></p>

<p><img src="https://cdn.jsdelivr.net/gh/doocs/leetcode@main/solution/0100-0199/0199.Binary%20Tree%20Right%20Side%20View/images/tree.jpg" style="width: 270px; " /></p>

<pre>
<strong>输入:</strong> [1,2,3,null,5,null,4]
<strong>输出:</strong> [1,3,4]
</pre>

<p><strong>示例 2:</strong></p>

<pre>
<strong>输入:</strong> [1,null,3]
<strong>输出:</strong> [1,3]
</pre>

<p><strong>示例 3:</strong></p>

<pre>
<strong>输入:</strong> []
<strong>输出:</strong> []
</pre>

<p> </p>

<p><strong>提示:</strong></p>

<ul>
	<li>二叉树的节点个数的范围是 <code>[0,100]</code></li>
	<li><meta charset="UTF-8" /><code>-100 <= Node.val <= 100</code> </li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

层序遍历，取每层最后一个元素。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        ans = []
        if root is None:
            return ans
        q = deque([root])
        while q:
            ans.append(q[0].val)
            for i in range(len(q), 0, -1):
                node = q.popleft()
                if node.right:
                    q.append(node.right)
                if node.left:
                    q.append(node.left)
        return ans
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if (root == null) {
            return ans;
        }
        Deque<TreeNode> q = new LinkedList<>();
        q.offerLast(root);
        while (!q.isEmpty()) {
            ans.add(q.peekFirst().val);
            for (int i = q.size(); i > 0; --i) {
                TreeNode node = q.pollFirst();
                if (node.right != null) {
                    q.offerLast(node.right);
                }
                if (node.left != null) {
                    q.offerLast(node.left);
                }
            }
        }
        return ans;
    }
}
```

### **C++**

```cpp
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
    vector<int> rightSideView(TreeNode* root) {
        vector<int> ans;
        if (!root) return ans;
        queue<TreeNode*> q{{root}};
        while (!q.empty())
        {
            ans.push_back(q.front()->val);
            for (int i = q.size(); i > 0; --i)
            {
                TreeNode* node = q.front();
                q.pop();
                if (node->right) q.push(node->right);
                if (node->left) q.push(node->left);
            }
        }
        return ans;
    }
};
```

### **Go**

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func rightSideView(root *TreeNode) []int {
	var ans []int
	if root == nil {
		return ans
	}
	q := []*TreeNode{root}
	for len(q) > 0 {
		ans = append(ans, q[0].Val)
		for i := len(q); i > 0; i-- {
			node := q[0]
			q = q[1:]
			if node.Right != nil {
				q = append(q, node.Right)
			}
			if node.Left != nil {
				q = append(q, node.Left)
			}
		}
	}
	return ans
}
```

### **...**

```

```

<!-- tabs:end -->
