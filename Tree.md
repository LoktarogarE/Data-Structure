## 建立一棵二叉搜索樹
```c++
tree* Insert(tree* root,int key){
    if (!root) {
        //root = (tree *)malloc(sizeof(tree));
        root = new tree();
        root->data = key;
    }
    else{
        if (key < root->data) {
            root->left = Insert(root->left, key);
        }
        else
            if (key > root->data) {
                root->right = Insert(root->right, key);
            }
    }
    return root;
}
```
---
## 是否完全二叉樹
```C++
bool isCompleteBST(tree* root){
    if (!root) {
        return true;
    }
    if ((root->left && !root->right) || (!root->left && root->right)) {
        return false;
    }
    if (!isCompleteBST(root->left) || !isCompleteBST(root->right)) {
        return false;
    }
    return true;
}
```
---
## 樹的遍歷
### 層次遍歷
```C++
void Hierarchical_traversal(tree* root){
    tree* temp = NULL;
    queue<tree *> Q;
    if (!root) {
        return;
    }
    Q.push(root);
    while (!Q.empty()) {
        temp = Q.front();
        Q.pop();
        cout<<temp->data<<" ";
         if (temp->left) {
            Q.push(temp->left);
        }
        if (temp->right) {
            Q.push(temp->right);
        }
    }
}
```
### 先序遍歷
```C++
void Preorder_traversal(AVLTree* root){
    if (root) {
        cout<<root->data<<" ";
        Preorder_traversal(root->left);
        Preorder_traversal(root->right);
    }
}
```
### 中序遍歷
```C++
void In_order_traversal(AVLTree* root){
    if (root) {
        Preorder_traversal(root->left);
        cout<<root->data<<" ";
        Preorder_traversal(root->right);
    }
}
```
### 後序遍歷
```C++
void Postorder_traversal(AVLTree* root){
    if (root) {
        Postorder_traversal(root->left);
        Postorder_traversal(root->right);
        cout<<root->data<<" ";
    }
}
```
---
## 求一棵完全二叉樹的左子樹結點個數
```C++
//求解最容易錯的就是最底層可能有右子樹的結點，所以需要求得最底層左子樹結點的最大值進行對比

int left_child_number(int total){
    int n = log(total) / log(2);    //除了最底層以外的層數（從0開始編號）
    int bottom = total - (pow(2, n) - 1);   //最底層的結點數，其中(pow(2, n) - 1)是除了底層以外的結點數
    int left_bottom_max = pow(2, n - 1);    //左子樹最底層的最大結點數（第0層除外）
    int left_branch_number = pow(2, n - 1) - 1;     //左子樹除了最底層的結點個數
    if (bottom >= left_bottom_max) {
        return left_bottom_max + left_branch_number;
    }
    else
        return bottom + left_branch_number;
}
```
---


