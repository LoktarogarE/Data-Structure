# Select Sort
```C++
void selectSort(int a[],int N)
{
    int i,j,k;
    for( i=0;i<N;i++)
    {
        k = i;
        for(j=i+1;j<N;j++)
        {
            if(a[j]<a[k])
                k = j;
        }
        int temp = a[i];
        a[i] = a[k];
        a[k] = temp;
    }
}
```
---
# Bubble Sort
```C++
// n numbers sort (n-1) times, in the i(th) round , sort (n-i-1) times.

void BubbleSort (int arr[], int n){
    for (int i = 0; i < n - 1; i++){
        for (int j = 0; j < n - i - 1; j++){
            if (arr[j] > arr[j + 1]){
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```
---
# Topologically Sort
```C++
#include<iostream>
#include<queue>
using namespace std;

const int MAXN=10005;
int vertex,edge;
bool a[MAXN][MAXN];//邻接矩阵建图用
int in_degree[MAXN];//入度数组
queue <int> q;

void input()
{
    cin>>vertex>>edge;
    for(int i=0;i<edge;i++)
    {
        int x,y;
        cin>>x>>y;
        a[x][y]=1;
        in_degree[y]++;//建图，同时统计入度
    }
}

void topo_sort()
{
    for(int i=0;i<vertex;i++)
     if(in_degree[i]==0)
      q.push(i);//将所有入度为0的点入队
    while(!q.empty())//开始搜索
    {
        const int u=q.front();
        cout<<u<<' ';
        q.pop();
        for(int i=0;i<vertex;i++)
         if(a[u][i])//删边的操作转化为入度减1
         {
            in_degree[i]--;
            if(in_degree[i]==0)//如果这个点变成入度为0，入队列
             q.push(i);
         }
    }
}

int main()
{
    input();
    topo_sort();
    return 0;
}
```
>[源网站(判断是否有环)](https://www.luogu.com.cn/blog/hyyyprtf06/kuai-su-ru-shou-ta-pu-pai-xu)
---
