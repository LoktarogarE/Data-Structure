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