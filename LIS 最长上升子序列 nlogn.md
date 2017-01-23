````
/*

iterator lower_bound( const key_type &key ): 返回一个迭代器，指向键值>= key的第一个元素。

iterator upper_bound( const key_type &key ): 返回一个迭代器，指向键值 第一个>key的元素。

*/

//这个算法也是nlongn的，只是用了upper_bound  效率可能会低一点

define MAXN 100005

include <iostream>

include<stdio.h>

include<algorithm>

using namespace std;

int a[MAXN];

int n;

int solve(int b[],int l)

{

    int f[MAXN];//f[i]表示子序列长度为i+1的序列中，末尾元素最小的元素的值
    int k=0;
    f[k++]=b[0];
    for(int i=1;i<l;i++)
    {
        if(b[i]>=f[k-1]) f[k++]=b[i];//上升子序列可以相等的情况  若不相等则改成=号
        else
        {
            int pos=upper_bound(f,f+k,a[i])-f;
            f[pos]=a[i];
        }
    }
    return k;

}

int main()

{

    int l=0;
    int num;
    scanf("%d",&num);
    while(num--)
    {
        int n;
        scanf("%d",&n);
        for(int i = 0; i < n;i++)
               scanf("%d",&a[i]);
    
        printf("Case #%d:\n%d\n",++l,n-(solve(a,n)));
    }

}







````












    /*
    //
    /** 
    最长递增子序列O(nlogn)算法： 
    状态转移方程：f[i] = max{f[i],f[j]+1},1<=j<i,a[j]<a[i]. 
    分析：加入x<y,f[x]>=f[y],则x相对于y更有潜力。 
    首先根据f[]值分类，记录满足f[t]=k的最小的值a[t],记d[k]=min{a[t]},f[t]=k. 
        1.发现d[k]在计算过程中单调不上升 
        2.d[1]<d[2]<...<d[k] (反证) 1 2 3 8 4 7 
    解法： 
    1. 设当前最长递增子序列为len,考虑元素a[i]; 
    2. 若d[len]<a[i],则len++，并将d[len]=a[i]; 
       否则,在d[0-len]中二分查找,找到第一个比它小的元素d[k],并d[k+1]=a[i].() 
    
    #include <iostream>  
    #include <cstdio>  
    #include <cstring>  
    using namespace std;  
    const int N = 41000;  
    int a[N];       //a[i] 原始数据  
    int d[N];       //d[i] 长度为i的递增子序列的最小值  
      
    int BinSearch(int key, int* d, int low, int high)  
    {  
        while(low<=high)  
        {  
            int mid = (low+high)>>1;  
            if(key>d[mid] && key<=d[mid+1])  
                return mid;  
            else if(key>d[mid])  
                low = mid+1;  
            else  
                high = mid-1;  
        }  
        return 0;  
    }  
      
    int LIS(int* a, int n, int* d)  
    {  
        int i,j;  
        d[1] = a[1];  
        int len = 1;        //递增子序列长度  
        for(i = 2; i <= n; i++)  
        {  
            if(d[len]<a[i])  
                j = ++len;  
            else  
                j = BinSearch(a[i],d,1,len) + 1;  
            d[j] = a[i];  
        }  
        return len;  
    }  
      
    int main()  
    {  
        int t;  
        int p;  
        scanf("%d",&t);  
        while(t--)  
        {  
            scanf("%d",&p);  
            for(int i = 1; i <= p; i++)  
                scanf("%d",&a[i]);  
            printf("%d\n",LIS(a,p,d));  
        }  
        return 0;  
    }  
    */
