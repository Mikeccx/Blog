# 二叉树
## 遍历
### 前序
```
    // 伪代码
    traverse function(root) {
        traverse(root.left)
        console.log(root.value)
        traverse(root.right)
    }
```
### 中序
```
    // 伪代码
    traverse function(root) {
        console.log(root.value)
        traverse(root.left)
        traverse(root.right)
    }
```
### 后序
```
    // 伪代码
    traverse function(root) {
        traverse(root.left)
        traverse(root.right)
        console.log(root.value)
    }
```
### 层序
```
    // 伪代码
    /**
    * Definition for a binary tree node.
    * function TreeNode(val) {
    *     this.val = val;
    *     this.left = this.right = null;
    * }
    */

    /** 利用队列实现树的广度遍历
    * @param {TreeNode} root
    * @return {number[][]}
    */
    var levelOrder = function(root) {
        const res = []
        const queue = [root]
        if (!root) {
            return res
        }
        while(queue.length > 0) {
            const len = queue.length
            const tmp = []
            for(let i = 0; i < len; i++) {
                const curNode = queue.shift()
                tmp.push(curNode.val)
                if(curNode.left) {
                    queue.push(curNode.left)
                }
                if(curNode.right) {
                    queue.push(curNode.right)
                }
            }
            res.push(tmp)
        }
        return res
    };
```
### 实战(leetcode)

* 226 翻转二叉树
```
    翻转一棵二叉树。

    示例：

    输入：

         4
       /   \
      2     7
     / \   / \
    1   3 6   9

    输出：
         4
       /   \
      7     2
     / \   / \
    9   6 3   1

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/invert-binary-tree
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
* 思路
* 代码
```
    /**
    * Definition for a binary tree node.
    * function TreeNode(val, left, right) {
    *     this.val = (val===undefined ? 0 : val)
    *     this.left = (left===undefined ? null : left)
    *     this.right = (right===undefined ? null : right)
    * }
    */
    /**
    * @param {TreeNode} root
    * @return {TreeNode}
    */
    var invertTree = function(root) {
        if (!root) {
            return null
        }
        let tmp = root.left
        root.left = root.right
        root.right = tmp
        if (root.left) {
            invertTree(root.left)
        } 
        if (root.right) {
            invertTree(root.right)
        }
        return root
    };
```

* 116 填充每个节点的下一个右侧节点指针
```
    给定一个 完美二叉树 ，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：

    struct Node {
        int val;
        Node *left;
        Node *right;
        Node *next;
    }
    填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

    初始状态下，所有 next 指针都被设置为 NULL。

     

    进阶：

    你只能使用常量级额外空间。
    使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。
     

    示例：



    输入：root = [1,2,3,4,5,6,7]
    输出：[1,#,2,3,#,4,5,6,7,#]
    解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化的输出按层序遍历排列，同一层节点由 next 指针连接，'#' 标志着每一层的结束。
     

    提示：

    树中节点的数量少于 4096
    -1000 <= node.val <= 1000

    来源：力扣（LeetCode）
    链接：https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node
    著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
* 思路
* 代码
```
    /**
    * // Definition for a Node.
    * function Node(val, left, right, next) {
    *    this.val = val === undefined ? null : val;
    *    this.left = left === undefined ? null : left;
    *    this.right = right === undefined ? null : right;
    *    this.next = next === undefined ? null : next;
    * };
    */

    /**
    * @param {Node} root
    * @return {Node}
    */
    // 第二种思路
    var connect = function(root) {
        if (!root) {
            return null
        }
        const queue = [root]
        while(queue.length) {
        const size = queue.length
        for(let i = 0; i < size; i++) {
            if (i !== size - 1 ) {
                queue[i].next = queue[i+1]
            }
            if (queue[i] && queue[i].left) {
                queue.push(queue[i].left)
            }
            if (queue[i] && queue[i].right){
                queue.push(queue[i].right)
            }
        }
        queue.splice(0, size)
    }
        return root
    };

    // 第二种思路
    var connect = function(root) {
        if (!root) {
            return null
        }
        twoConnect(root.left, root.right)
        return root
    };
    var twoConnect = function (left, right) {
        if (!left || !right) {
            return
        }
        left.next = right
        twoConnect(left.left, left.right)
        twoConnect(right.left, right.right)
        twoConnect(left.right, right.left)
    }
```


