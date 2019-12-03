### 深度優先搜索(递归)
```C++
#include<stdio.h>
#include<string.h>
#define MAX 100
using namespace std;

bool visited[MAX];//标记顶点是否被遍历过
int map[MAX][MAX];
int n;
void DFS(int v)
{
    visited[v]=true;
    printf("%d ",v);
    for(int i=0;i<n;i++)
        if(!visited[i]&&map[v][i]==1)
            DFS(i);
}
int main()
{
    printf("请输入结点数:");
    scanf("%d",&n);
    memset(map,0,sizeof(map));
    printf("请输入%d*%d的邻接矩阵:\n",n,n);
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%d",&map[i][j]);
    for(int i=0;i<n;i++)
        visited[i]=false;
    printf("遍历的结果为:");
    for(int i=0;i<n;i++)
        if(!visited[i])
            DFS(i);
    printf("\n");
}
```
---
### 深度優先搜索(非递归)
```C++
#include <iostream>
#include <stack>
using namespace std;

#define MaxNode 20
#define MAX 2000
#define StartNode 1

int map[MaxNode+1][MaxNode+1];

void dfs_stack(int start, int n){
    int visited[MaxNode],s_top;
    for(int i = 0;i <= MaxNode; i++){
        visited[i] = 0;
    }
    visited[start] = 1;
    stack <int> s;
    cout<<start<<" ";
    for(int i = 1; i <= n; i++){
        if(map[i][start] == 1 && !visited[i] ){
            visited[i] =  1;
            s.push(i);
        }
    }
    
    while(!s.empty()){
        s_top =  s.top();
        visited[s_top] = 1;
        cout<<s_top<<" ";
        s.pop();
        for(int i = 1; i <= n; i++){
            if(map[i][s_top] == 1 && !visited[i] ){
                visited[i] = 1;
                s.push(i);
            }
        }
    }
    
}

int main(int argc, const char * argv[]) {
    int num_edge,num_node;
    int x,y;
    cout<<"Input number of nodes and edges >"<<endl;
    cin>>num_node>>num_edge;
    for(int i =0;i<num_node;i++){
        for(int j=0;j<num_node;j++){
            map[i][j] = 0;
        }
    }
    for(int i = 1; i <= num_edge; i++){
        cin>>x>>y;
        map[x][y] = map[y][x] = 1;
    }
    
    dfs_stack(StartNode, num_node);

    return 0;
}
```
### 廣度優先搜索
```C++
#include<stdio.h>
#include<string.h>
#include<queue>
#define MAX 100
using namespace std;
bool visited[MAX];//标记顶点是否被遍历过
int map[MAX][MAX];
int n;
void BFS(int v)
{
    printf("%d ",v);
    visited[v]=true;
    queue<int> Q;
    Q.push(v);
    while(!Q.empty())
    {
        int front=Q.front();
        Q.pop();
        for(int i=0;i<n;i++)
            if(!visited[i]&&map[front][i]==1)
            {
                visited[i]=true;
                printf("%d ",i);
                Q.push(i);
            }
    }
}
int main()
{
    printf("请输入结点数:");
    scanf("%d",&n);
    memset(map,0,sizeof(map));
    printf("请输入%d*%d的邻接矩阵:\n",n,n);
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            scanf("%d",&map[i][j]);
    for(int i=0;i<n;i++)
        visited[i]=false;
    printf("遍历的结果为:");
    for(int i=0;i<n;i++)
        if(!visited[i])
            BFS(i);
    printf("\n");
}
```
---
