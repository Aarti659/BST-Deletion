//C++ Program to implement BST-Deletion

#include <bits/stdc++.h>

using namespace std;

struct node {
int key;
struct node *Lt, *rgt;
};
struct node* newNode(int item)
{
struct node* temp
= (struct node*)malloc(sizeof(struct node));
temp->key = item;
temp->Lt = temp->rgt = NULL;
return temp;
}
void inorder(struct node* root)
{
if (root != NULL) {
inorder(root->Lt);
cout << root->key << " ";
inorder(root->rgt);
}
}
struct node* insertFunc(struct node* node, int val)
{
if (!node)
{
return newNode(val);
}
if (val > node->key)
{
node->rgt = insertFunc(node->rgt, val);
}
else
{
node->Lt = insertFunc(node->Lt, val);
}
return node;
}
struct node* minValueNode(struct node* node)
{
struct node* current = node;
while (current && current->Lt != NULL)
current = current->Lt;
return current;
}
struct node* deleteFunc(struct node* root, int key)
{
if (root == NULL)
return root;
if (key < root->key)
root->Lt = deleteFunc(root->Lt, key);
else if (key > root->key)
root->rgt = deleteFunc(root->rgt, key);
else {
if (root->Lt==NULL and root->rgt==NULL)
return NULL;
else if (root->Lt == NULL) {
struct node* temp = root->rgt;
free(root);
return temp;
}
else if (root->rgt == NULL) {
struct node* temp = root->Lt;
free(root);
return temp;
}
struct node* temp = minValueNode(root->rgt);
root->key = temp->key;
root->rgt = deleteFunc(root->rgt, temp->key);
}
return root;
}
int main()
{
struct node* root = NULL;
root = insertFunc(root, 27);
root = insertFunc(root, 39);
root = insertFunc(root, 17);
root = insertFunc(root, 19);
root = insertFunc(root, 67);
root = insertFunc(root, 35);
root = insertFunc(root, 12);
root = insertFunc(root, 1);
cout << "Inorder traversal of the given tree \n";
inorder(root);
cout << "\n<Delete> 1\n";
root = deleteFunc(root, 1);
cout << "Traversing the modified tree \n";
inorder(root);
cout << "\n<Delete> 39\n";
root = deleteFunc(root, 39);
cout << " Traversing the modified tree \n";
inorder(root);
cout << "\n<Insert> 19\n";
root = insertFunc(root, 19);
cout << " Traversing the modified tree \n";
inorder(root);
cout << "\n<Delete> 67\n";
root = deleteFunc(root, 67);
cout << " Traversing the modified tree \n";
inorder(root);
return 0;
}




