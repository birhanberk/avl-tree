#include <stdio.h>
struct node{
    int key;
    struct node *left;
    struct node *right;
    int height; // derinlik
};

int max(int a, int b){
    return a>b ? a:b;
}

int height(struct node *node){
    if(node==NULL) return 0;
    return node->height;
}

struct node *rightRotate(struct node **y){
    struct node *x=(*y)->left, *T=x->right;
    x->right=*y;
    (*y)->left = T;
    
    (*y)->height=max(height((*y)->left),height((*y)->right))+1;
    x->height=max(height(x->left),height(x->right))+1; 
    
    return x;
} // sol sol

struct node *leftRotate(struct node **x){
    struct node *y=(*x)->right, *T=y->left;
    y->left=*x;
    (*x)->right = T;
    
    (*x)->height=max(height((*x)->left),height((*x)->right))+1;
    y->height=max(height(y->left),height(y->right))+1;
    
    return y;
} // sag sag

int getBalance(struct node *node){
    if(node==NULL) return 0;
    return height(node->left) - height(node->right);
}

struct node *newNode(int key){
    struct node *node=(struct node*)malloc(sizeof(struct node));
    node->key=key;
    node->left=node->right=NULL;
    node->height=1;
    return node;
}

void insert(struct node **node, int key){
    int balance;
    if(*node==NULL){ 
        *node = newNode(key);
        return;
    }
    if(key<(*node)->key) insert(&(*node)->left,key);
    else insert(&(*node)->right,key);
    
    (*node)->height = max(height((*node)->left),height((*node)->right)) +1;
    
    balance=getBalance(*node);
    
    if(balance>1 && key < (*node)->left->key){ // sol sol
        *node = rightRotate(node);
        return;
    }
    if(balance<-1 && key > (*node)->right->key){ // sag sag
        *node = leftRotate(node);
        return;
    }
    if(balance>1 && key>(*node)->left->key){  // sol sag
        (*node)->left=leftRotate(&(*node)->left);
        *node = rightRotate(node);
        return;
    }
    if(balance<-1 && key<(*node)->right->key){  // sag sol
        (*node)->right=rightRotate(&(*node)->right);
        *node = leftRotate(node);
        return;
    }
}

void preOrder_yardimci(struct node *node) {
    if(node!=NULL){
        printf("%d (%2d) ",node->key,node->height);
        preOrder_yardimci(node->left);
        preOrder_yardimci(node->right);
    }
    
}

void preOrder(struct node *node) {
    preOrder_yardimci(node);
    printf("\n");
}

struct node *minValueNode(struct node *root){
    struct node *current = root;
    if(current == NULL) return NULL;
    while(current->left) current=current->left;
    return current;
}

void deleteNode(struct node **root, int key){
    if(*root==NULL) return;
    if(key<(*root)->key) deleteNode(&(*root)->left,key);
    else if(key>(*root)->key) deleteNode(&(*root)->right,key);
    else {
        if((*root)->left == NULL || (*root)->right == NULL){
            struct node *temp=(*root)->left ?(*root)->left:(*root)->right;
            if(temp==NULL){
                temp=(*root);
                (*root)=NULL;
            }
            else **root=*temp; // root->key=temp->key; root->rigt = temp->rigt; root->left= 
            free(temp);
        }
        else {
            struct node *temp=minValueNode((*root)->right);
            (*root)->key=temp->key;
            deleteNode(&(*root)->right,temp->key);
        }
    }
    
    if(*root==NULL) return;
    (*root)->height = max(height((*root)->left),height((*root)->right)) +1;

    int balance=getBalance(*root);

    if(balance>1 && getBalance((*root)->left) >=0)
        *root=rightRotate(root);
        return;
    if(balance>1 && getBalance((*root)->left) < 0){
        (*root)->left=leftRotate(&(*root)->left);
        *root=rightRotate(root);
        return;
    }
    if(balance <-1 && getBalance((*root)->right)<=0)
        *root=leftRotate(root);
        return;
    if(balance <-1 && getBalance((*root)->right)>0){
        (*root)->right = rightRotate(&(*root)->right);
        *root=leftRotate(root);
        return;
    }
}
int main()
{
    struct node *root=NULL;
    
    insert(&root,40);
    insert(&root,52);
    insert(&root,68);
    insert(&root,30);
    insert(&root,35);
    insert(&root,50);
    insert(&root,20);
    insert(&root,25);
    insert(&root,22);
    
    preOrder(root);
    deleteNode(&root,35);
    deleteNode(&root,30);
    
    preOrder(root);
    return 0;
}
