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


