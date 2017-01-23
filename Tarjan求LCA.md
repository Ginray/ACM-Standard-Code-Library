~~~
include <iostream>

include <cstdio>

include <cstring>

using namespace std;

define N 10010

define M 10010

define Q 1000010

int head[N];

struct edge{

    int u,v,w,next;

}e[2*M];

int __head[N];

struct ask{

    int u,v,lca,next;

}ea[2*Q];

int dir[N],fa[N],vis[N];

inline void add_edge(int u ,int v ,int w ,int &k)

{

    e[k].u = u; e[k].v = v; e[k].w = w;
    e[k].next = head[u]; head[u] = k++;

}

inline void add_ask(int u ,int v ,int &k)

{

    ea[k].u = u; ea[k].v = v; ea[k].lca = -1;
    ea[k].next = __head[u]; __head[u] = k++;

}

int find(int x){

    return  x == fa[x] ? x : fa[x] = find(fa[x]);

}

void Tarjan(int u ,int c)

{

    vis[u] = c; fa[u] = u;
    for(int k=head[u]; k!=-1; k=e[k].next)
        if(!vis[e[k].v])
        {
            int v = e[k].v , w = e[k].w;
            dir[v] = dir[u] + w;
            Tarjan(v,c);
            fa[v] = u;
        }
    for(int k=__head[u]; k!=-1; k=ea[k].next)
        if(vis[ea[k].v] == c)
            ea[k].lca = ea[k^1].lca = find(ea[k].v);

}

int main()

{

    int n,m,q,k;
    while(scanf("%d%d%d",&n,&m,&q)!=EOF)
    {
        memset(head,-1,sizeof(head));
        memset(__head,-1,sizeof(__head));
        memset(vis,0,sizeof(vis));
        k = 0;
        for(int i=0; i<m; i++)
        {
            int u,v,w;
            scanf("%d%d%d",&u,&v,&w);
            add_edge(u,v,w,k);
            add_edge(v,u,w,k);
        }
        k = 0;
        for(int i=0; i<q; i++)
        {
            int u,v;
            scanf("%d%d",&u,&v);
            add_ask(u,v,k);
            add_ask(v,u,k);
        }
        k = 0;
        for(int i=1; i<=n; i++)
            if(!vis[i])
            {
                dir[i] = 0;
                Tarjan(i,++k);
            }
        for(int i=0; i<q; i++)
        {
            int s = i*2 , u = ea[s].u , v = ea[s].v , lca = ea[s].lca;
            if(lca == -1) printf("Not connected\n");
            else          printf("%d\n",dir[u] + dir[v] - 2*dir[lca]);
        }
    }
    return 0;

}

~~~

