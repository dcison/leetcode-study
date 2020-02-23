# 树

1. 94题：[二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
```golang
// 核心算法
// 1. 递归
    if !root {
         return nil
     }
    recInorderTraversal(root.left)
    rtn.push(root.val)
    recInorderTraversal(root.right)

// 2.循环 使用一个栈记录路径 
//以便可以在访问完子树后,可以利用栈中的信息,回退到当前节点的双亲节点,进行下一步操作
// 延伸：
// 后序遍历的非递归算法是三种顺序中最复杂的，原因在于，后序遍历是先访问左、右子树,再访问根节点。
// 而在非递归算法中，利用栈回退到时，并不知道是从左子树回退到根节点，还是从右子树回退到根节点。
// 如果从左子树回退到根节点，此时就应该去访问右子树，而如果从右子树回退到根节点，此时就应该访问根节点。
// 所以相比前序和后序，必须得在压栈时添加信息，以便在退栈时可以知道是从左子树返回，
// 还是从右子树返回进而决定下一步的操作。
    var stack = make([]*TreeNode, 0);
    copyRoot := root;
    for {
        if copyRoot == nil && len(stack) == 0  {
            break;
        }
        if copyRoot != nil {
            stack = append(stack,copyRoot);
            copyRoot = copyRoot.Left
        }else{
            copyRoot = stack[len(stack) - 1];
            stack = stack[:len(stack)-1]
            rtn = append(rtn,copyRoot.Val)
            copyRoot = copyRoot.Right;
        }
    }
    r

```

2. 98. [验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)
```golang
    if root == nil {
        return true
    }
    if !(root.Val > min && root.Val < max) {
        // 如果当前值 不在限定范围内 则为false
        return false
    }
    // 巧妙的利用 min ， max 分别设置为根节点的值 以及当前子树的父节点的值，分别做比较
    return checkBST(root.Left,min,root.Val) && checkBST(root.Right,root.Val,max)
    // 如果比较难懂的话，可以直接递归子树做，外加两个辅助函数，取左子树的最大值，以及右子树的最小值
    // 且要满足 left_max < root < right_min
    // 中序遍历做，拿到数组后，两两比较，如果没有数组没有升序 不是BST
    // 优化的中序遍历 ，直接比较当前节点与上一个节点
    
```