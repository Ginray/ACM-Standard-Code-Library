~~~
prime算法：

include<stdio.h>

include<string.h>

define INF 0x3fffffff

int lowcost[110];//此数组用来记录第j个节点到其余节点最少花费

int map110;//用来记录第i个节点到其余n-1个节点的距离

int visit[110];//用来记录最小生成树中的节点

int n;

void prime()

{

  int min,i,j,next,mincost=0;

  memset(visit,0,sizeof(visit));//给最小生成树数组清零

  for(i=1;i<=n;i++)

  {

    lowcost[i]=map[1][i];//初始化lowcost数组为第1个节点到剩下所有节点的距离

  }

  visit[1]=1;//选择第一个点为最小生成树的起点

  for(i=1;i<n;i++)

  {

    min=INF;
    for(j=1;j<=n;j++)
    {
      if(!visit[j]&&min>lowcost[j])//如果第j个点不是最小生成树中的点并且其花费小于min
      {
        min=lowcost[j];
        next=j;//记录下此时最小的位置节点
      }
    }
    if(min==INF)
    {
      printf("数据不足以确定\n");                               //当数据不够构成最小生成树的时候
      return ;
    }
    mincost+=min;//将最小生成树中所有权值相加
    visit[next]=1;//next点加入最小生成树
    for(j=1;j<=n;j++)
    {
      if(!visit[j]&&lowcost[j]>map[next][j])//如果第j点不是最小生成树中的点并且此点处权值大于第next点到j点的权值
      {
        lowcost[j]=map[next][j];     //更新lowcost数组
      }
    }

  }

  printf("%d\n",mincost);

}

int main()

{

  int road;

  int j,i,x,y,c;

  while(scanf("%d%d",&road,&n)&&road!=0)

  {

    memset(map,INF,sizeof(map));//初始化数组map为无穷大
    while(road--)
    {
      scanf("%d%d%d",&x,&y,&c);
      map[x][y]=map[y][x]=c;//城市x到y的花费==城市y到想的花费
    }
    prime();

  }

  return 0;

}











kruskal算法：

include<stdio.h>

include<algorithm>

using namespace std; 

int set[110]; 

struct record 

{ 

  int beg; 

  int end; 

  int money; 

}s[11000]; 

int find(int fa) 

{ 

  int ch=fa; 

  int t; 

  while(fa!=set[fa]) 

  fa=set[fa]; 

  while(ch!=fa) 

  { 

    t=set[ch]; 
    set[ch]=fa; 
    ch=t; 

  } 

  return fa; 

} 

void mix(int x,int y) 

{ 

  int fx,fy; 

  fx=find(x); 

  fy=find(y); 

  if(fx!=fy) 

  set[fx]=fy; 

} 

bool cmp(record a,record b) 

{ 

  return a.money<b.money; 

} 

int main() 

{ 

  int city,road,n,m,j,i,sum; 

  while(scanf("%d",&road)&&road!=0) 

  { 

    scanf("%d",&city); 
    for(i=0;i<road;i++) 
    { 
      scanf("%d%d%d",&s[i].beg,&s[i].end,&s[i].money); 
    } 
    for(i=1;i<=city;i++) 
    set[i]=i; 
    sort(s,s+road,cmp); 
    sum=0; 
    for(i=0;i<road;i++) 
    { 
      if(find(s[i].beg)!=find(s[i].end)) 
      { 
        mix(s[i].beg,s[i].end); 
        sum+=s[i].money; 
      } 
    } 
    j=0; 
    for(i=1;i<=city;i++) 
    { 
      if(set[i]==i) 
      j++; 
      if(j>1) 
      break; 
    } 
    if(j>1) 
    printf("数据不足以确定\n");                       //当数据不够构成最小生成树的时候  
    else
    printf("%d\n",sum); 

  } 

  return 0; 

}

~~~

