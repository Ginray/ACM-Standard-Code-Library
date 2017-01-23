~~~
include <iostream>

include<stdlib.h>

include<string.h>

include<stdio.h>

include <queue>

using namespace std;



const long MAXN=10000;

const long lmax=0x7FFFFFFF;



typedef struct

{

    long v;

    long next;

    long cost;

}Edge;





Edge e[MAXN];

long p[MAXN];

long Dis[MAXN];

bool vist[MAXN];



queue<long> q;



long m,n;//点,边

void init()

{

    long i;

    long eid=0;



    memset(vist,0,sizeof(vist));

    memset(p,-1,sizeof(p));

    fill(Dis,Dis+MAXN,lmax);



    while (!q.empty())

    {

        q.pop();

    }



    for (i=0;i<n;++i)

    {

        long from,to,cost;

        scanf("%ld %ld %ld",&from,&to,&cost);



        e[eid].next=p[from];

        e[eid].v=to;

        e[eid].cost=cost;

        p[from]=eid++;



        //以下适用于无向图

        swap(from,to);



        e[eid].next=p[from];

        e[eid].v=to;

        e[eid].cost=cost;

        p[from]=eid++;



    }

}



void print(long End)

{

    //若为lmax 则不可达

    printf("%ld\n",Dis[End]);

}



void SPF()

{



    init();



    long Start,End;

    scanf("%ld %ld",&Start,&End);

    Dis[Start]=0;

    vist[Start]=true;

    q.push(Start);



    while (!q.empty())

    {

        long t=q.front();

        q.pop();

        vist[t]=false;

        long j;

        for (j=p[t];j!=-1;j=e[j].next)

        {

            long w=e[j].cost;

            if (w+Dis[t]<Dis[e[j].v])

            {

                Dis[e[j].v]=w+Dis[t];

                if (!vist[e[j].v])

                {

                    vist[e[j].v]=true;

                    q.push(e[j].v);

                }

            }

        }

    }



    print(End);



}



int main()

{

    while (scanf("%ld %ld",&m,&n)!=EOF)

    {

        SPF();

    }

    return 0;

}

~~~

