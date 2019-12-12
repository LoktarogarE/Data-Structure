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
>Question describe
给出顶点数(n)、边数(m)、起点(s)、终点(t)，求 s 到 t 的最短路径
```C++
#include <iostream>
#include <cstring>
#define INF 0x3f3f3f3f;
using namespace std;

int map[2550][2550],dis[2550];
bool visited[2550];
int n,m,s,t;

void init() {
    memset(visited, false, sizeof(visited));
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++)
            if (i == j)
                map[i][j] = 0;
            else
                map[i][j] = INF;
    }
}

void dijkstra(){
    for (int i = 1; i <= n; i++) {
        dis[i] = map[s][i];
    }
    visited[s] = true;
    for (int i=1; i<=n; i++) {
        int v = 0;
        int min = INF;
        for (int j=1; j<=n; j++) {
            if (!visited[j] && dis[j] < min) {
                min = dis[j];
                v = j;
            }
        }
        visited[v] = true;
        for (int k=1; k<=n; k++) {
            if (!visited[k] && dis[v] + map[v][k] < dis[k]) {
                dis[k] = dis[v] + map[v][k];
            }
        }
    }
    cout<<dis[t]<<endl;
}

int main(){

    cin>>n>>m>>s>>t;
    init();
    int si,ti,wi;
    for (int i=0; i<m; i++) {
        cin>>si>>ti>>wi;
        if (wi < map[si][ti]) {
            map[si][ti] = map[ti][si] = wi;
        }
    }
    dijkstra();
    return 0;
}
/*
 input:
 7 11 5 4
 2 4 2
 1 4 3
 7 2 2
 3 4 3
 5 7 5
 7 3 3
 6 1 1
 6 3 4
 2 4 3
 5 6 3
 7 2 1
 
 output:
 7
 */
```
>注释(这个也太难啦吧)：
用一个叫 dis 的数组存长度，还有一个叫 visited 的数组来储存观察过的结点，然后就拿map矩阵来初始化dis数组吧，然后在那个大的for循环里面遍历每个结点一次，用 v 作为一个下标来标记 dis 数组中的最小值，已被访问的除外，!visited[j]就说明了这样子滴，k 这个结点就被访问了咯，然后再更新每个未被访问的结点的距离，dis[u] + map[v][j]就是与 v 相连的结点的权值的，而dis[j]可能是被其他结点改变过的值，也可能是 ∞ ，反正变小就完事了。
