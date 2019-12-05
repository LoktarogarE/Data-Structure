# DFS(深度優先搜索)
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
//Non-recursive DFS
void DFS_nr(int start) {
    visited[start]= true;
    cout<<start<<" "<< endl;
    stack<int> s;
    s.push(start);
    bool is_push;
    while (!s.empty()) {
        is_push= false;
        int top= s.top();
        for (int i= 0; i< N; i++) {
            if (!visited[i]&& mat[top][i]) {
                visited[i]= true;
                cout<< "visit: "<< i<< endl;
                s.push(i);
                is_push= true;
                break;
            }
        }
        if (!is_push) {
            s.pop();
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
            DFS(i);
            //DFS_nr(i);
    printf("\n");
}
```
---
# BFS(廣度優先搜索)
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
# Dijkstra
![Dijkstra](https://github.com/WangleiO/Data-Structure/blob/master/Dijkstra.png)
```C++
void dijkstra()
{
    memset(dis,INT_MAX,sizeof(dis));//初始化
    v[1]=1;
    dis[1]=0;
    for(int i=1;i<=n;++i)
    {
        int k=0;
        for(int j=1;j<=n;++j)//找出距离最近的点
            if(!v[j]&&(k==0||dis[j]<dis[k]))
                k=j;
        v[k]=1;//加入集合
        for(int j=1;j<=n;++j)//松弛
            if(!v[j]&&dis[k]+a[k][j]<dis[j])
                dis[j]=dis[k]+a[k][j];
    }
}
```
>注释(这个也太难啦吧)：
用一个叫 dis 的数组存长度，还有一个叫 v 的数组来储存观察过的结点，一开始第一个结点为0，其余为最大值(∞)，根结点(也就是第一个结点)的 dis 为0，然后在那个大的for循环里面遍历每个结点一次，用 k 作为一个下标来标记 dis 数组中的最小值，已被访问的除外，!v[j]就说明了这样子滴，k 这个结点就被访问了咯，然后再更新每个未被访问的结点的距离，dis[k] + a[k][j]就是与 k 相连的结点的权值的，而dis[j]可能是被其他结点改变过的值，也可能是 ∞ ，反正变小就完事了。
