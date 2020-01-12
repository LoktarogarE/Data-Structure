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
# QuickSort
```c++
#include <cstdio>
#include<iostream>
using namespace std;

int a[101],n;//定义全局变量，这两个变量需要在子函数中使用
void quicksort(int left,int right)
{
    int i,j,t,temp;
    if(left > right)
       return;
       
    temp = a[left]; //temp中存的就是基准数
    i = left;
    j = right;
    while(i != j)
    {
        //顺序很重要，要先从右边开始找
        while(a[j] >= temp && i < j)
            j--;
        //再找左边的
        while(a[i] <= temp && i < j)
            i++;
        //交换两个数在数组中的位置
        if(i < j)
        {
            t = a[i];
            a[i] = a[j];
            a[j] = t;
        }
    }
    //最终将基准数归位
    a[left] = a[i];
    a[i] = temp;
    
    quicksort(left,i-1);//继续处理左边的，这里是一个递归的过程
    quicksort(i+1,right);//继续处理右边的 ，这里是一个递归的过程
}
int main(int argc, const char * argv[])
{
    int i;
    //读入数据
    scanf("%d",&n);
    for(i=1;i<=n;i++)
        scanf("%d",&a[i]);
    quicksort(1,n); //快速排序调用
    
    //输出排序后的结果
    for(i=1;i<=n;i++)
        printf("%d ",a[i]);
    cout<<endl;
    return 0;
}

```
