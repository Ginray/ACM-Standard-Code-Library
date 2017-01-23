~~~
//Stoer-Wagner算法

//无向图全局最小割，算法复杂度o（n^3)

include<iostream>

include<cstdlib>

include<cstring>

include<cstdio>

define MAXN 600

using namespace std;

int matMAXN;

int res;

void Mincut (int n)

{

 int node [MAXN];

 int dist [MAXN];

 bool visit[MAXN];

 int i,prev,maxj,j,k;

for(i=0;i<n;i++)

    node[i]=i;

while(n>1)

{

int maxj =1;

for(i=1;i<n;i++)

{

    dist[node[i]]=mat[node[0]][node[i]];

if(dist[node[i]]>dist[node[maxj]])

    maxj=i;

}

prev=0;

memset(visit,false,sizeof(visit));

visit[node[0]]=true;

for(i=1;i<n;i++)

 {

     if(i==n-1)
     {
      res=min(res,dist[node[maxj]]);
     for(k=0;k<n;k++)
        mat[node[k]][node[prev]]=(mat[node[prev]][node[k]]+=mat[node[k]][node[maxj]]);
     node[maxj]=node[--n];
    }

visit[node[maxj]]=true;

prev=maxj;

maxj=-1;

for(j=1;j<n;j++)

    if(!visit[node[j]])

{

dist[node[j]]+=matnode[prev]];

if(maxj==-1||dist[node[maxj]]  <dist[node[j]])

    maxj=j;



}

}

}

return ;

}

int main() {

    int n, m, a, b, v;
    while (scanf("%d%d", &n, &m) != EOF) {
        res = (1 << 29);
        memset(mat, 0, sizeof (mat));
        while (m--) {
            scanf("%d%d%d", &a, &b, &v);
            mat[a][b] += v;
            mat[b][a] += v;
        }
        Mincut(n);
        printf("%d\n", res);
    }

}



~~~

