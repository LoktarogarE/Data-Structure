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
# 樹的遍歷
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


