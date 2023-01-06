
二叉树的遍历，非递归写法：

题目 94 144 145

思路:二叉树的遍历的递归写法其实是利用函数的调用原理隐式地维护了一个栈，所以非递归的写法需要显式地维护栈。

前序遍历： root left right
```c++
vector<int> preorderTraversal(TreeNode * root){
    vector<int> res;
    if(root == nullptr) return res;
    stack<TreeNode *> stk;
    while(!stk.empty() || root != nullptr){
        while(root != nullptr){
            res.push_back(root->val)
            stk.push(root);
            root = root -> left;
        }
        root = stk.top();
        stk.pop();
        root = root -> right;
    }
    return res;
}
```
中序遍历： left root right
```c++
vector<int> inorderTraversal(TreeNode * root){
    vector<int> res;
    if(root == nullptr) return res;
    stack<TreeNode *> stk;
    while(!stk.empty() || root != nullptr){
        while(root != nullptr){
            stk.push(root);
            root = root -> left;
        }
        root = stk.top();
        res.push_back(root->val);
        stk.pop();
        root = root -> right;
    }
    return res;
}
```
后序遍历： left right root

修改前序遍历的代码，使其按照root right left的顺序便利，然后反转一下结果
```c++
vector<int> postorderTraversal(TreeNode * root){
    vector<int> res;
    if(root == nullptr) return res;
    stack<TreeNode *> stk;
    while(!stk.empty() || root != nullptr){
        while(root != nullptr){
            res.push_back(root -> val);
            stk.push(root);
            root = root -> right;
        }
        root = stk.top();
        stk.pop();
        root = root -> left;
    }
    reverse(res.begin(),res.end());
    return res;
}
```