   //并查集+深搜


    #include<stdio.h>
    #include<vector>
    #include<string.h>
    using namespace std;
    #define Size 11111  //节点个数
    
    vector<int> node[Size],que[Size];
    int n,pare[Size],anse[Size],in[Size],rank[Size];
    
    int vis[Size];
    void init()
    {
        int i;
        for(i=1;i<=n;i++)
        {
            node[i].clear();
            que[i].clear();
            rank[i]=1;
            pare[i]=i;///
        }
        memset(vis,0,sizeof(vis));
        memset(in,0,sizeof(in));
        memset(anse,0,sizeof(anse));
    
    }
    
    int find(int nd)//并查集操作  不解释
    {
        return pare[nd]==nd?nd:pare[nd]=find(pare[nd]);
    }
    int Union(int nd1,int nd2)//并查集操作  不解释
    {
        int a=find(nd1);
        int b=find(nd2);
        if(a==b) return 0;
        else if(rank[a]<=rank[b])
        {
            pare[a]=b;
            rank[b]+=rank[a];
        }
        else
        {
            pare[b]=a;
            rank[a]+=rank[b];
        }
        return 1;
    
    }
    
    void LCA(int root)
    {
        int i,sz;
        anse[root]=root;//首先自成一个集合
        sz=node[root].size();
        for(i=0;i<sz;i++)
        {
               LCA(node[root][i]);//递归子树
               Union(root,node[root][i]);//将子树和root并到一块
             anse[find(node[root][i])]=root;//修改子树的祖先也指向root
        }
        vis[root]=1;
        sz=que[root].size();
        for(i=0;i<sz;i++)
        {
                if(vis[que[root][i]])
                {
                    printf("LCA is %d\n",anse[find(que[root][i])]);///root和que[root][i]所表示的值的最近公共祖先
                    return ;
                }
        }
         return ;
    }
    
    int main()
    {
        int cas,i;
        scanf("%d",&cas);
        while(cas--)
        {
            int s,e;
            scanf("%d",&n);
            init();
            for(i=0;i<n-1;i++)
            {
                scanf("%d %d",&s,&e);
                if(s!=e)
                {
                    node[s].push_back(e);
                   // node[e].push_back(s);
                    in[e]++;
                }
            }
            scanf("%d %d",&s,&e);
            que[s].push_back(e);
            que[e].push_back(s);
            for(i=1;i<=n;i++)  if(in[i]==0) break;//寻找根节点
            //printf("root=%d\n",i);
            LCA(i);
        }
        return 0;
    }







//Tarjan算法   带权值
//只能离线处理 降低复杂度



````


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



````

