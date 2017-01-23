```

//POJ 2774
//最长公共子序列

#include <cstdlib>
#include <cstring>
#include <cstdio>
#include <algorithm>
using namespace std;
const int N = 200010;

int seq [N],sa[N];
int n;
char str[N];



int wa[N], wb[N], ws[N], wv[N];
int rank[N], height[N];

bool cmp(int r[], int a, int b, int l) {
    return r[a] == r[b] && r[a+l] == r[b+l];
}

void da(int r[], int sa[], int n, int m) {
    int i, j, p, *x = wa, *y = wb;
    for (i = 0; i < m; ++i) ws[i] = 0;
    for (i = 0; i < n; ++i) ws[x[i]=r[i]]++;
    for (i = 1; i < m; ++i) ws[i] += ws[i-1];
    for (i = n-1; i >= 0; --i) sa[--ws[x[i]]] = i;
    for (j = 1, p = 1; p < n; j *= 2, m = p) {
        for (p = 0, i = n - j; i < n; ++i) y[p++] = i;
        for (i = 0; i < n; ++i) if (sa[i] >= j) y[p++] = sa[i] - j;
        for (i = 0; i < n; ++i) wv[i] = x[y[i]];
        for (i = 0; i < m; ++i) ws[i] = 0;
        for (i = 0; i < n; ++i) ws[wv[i]]++;
        for (i = 1; i < m; ++i) ws[i] += ws[i-1];
        for (i = n-1; i >= 0; --i) sa[--ws[wv[i]]] = y[i];
        for (swap(x, y), p = 1, x[sa[0]] = 0, i = 1; i < n; ++i)
            x[sa[i]] = cmp(y, sa[i-1], sa[i], j) ? p-1 : p++;
    }
}

void calheight(int r[], int sa[], int n) {
    int i, j, k = 0;
    for (i = 1; i <= n; ++i) rank[sa[i]] = i;
    for (i = 0; i < n; height[rank[i++]] = k)
        for (k?k--:0, j = sa[rank[i]-1]; r[i+k] == r[j+k]; k++);
}


int main ()
{
    char s1[N],s2[N];

    while(scanf("%s%s",s1,s2)!=EOF)
    {
        int len1=strlen(s1);
        int len2=strlen(s2);
        for(int i=0;i<len1;i++)
        seq[i]=s1[i]-'a'+2;
    
        seq[len1]=1;
        for(int i=0;i<len2;i++)
            seq[len1+i+1]=s2[i]-'a'+2;
    
        seq[len1+len2+1]=0;
        int len=len1+len2+1;
    
        da(seq,sa,len+1,30);
        calheight(seq,sa,len);
    
        int maxn=0;
        for(int i=2;i<=len;i++)
        {
            if(height[i]>maxn)
            {
                if(0<=sa[i-1]&&sa[i-1]<len1&&sa[i]>len1)
                    maxn=height[i];
                if(0<=sa[i]&&sa[i]<len1&&sa[i-1]>len1)
                    maxn=height[i];
            }
        }
        printf("%d\n",maxn);
    }
    
    return 0;
}

```