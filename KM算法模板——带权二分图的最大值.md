

//黑箱模板   ​:sad:​

````
include<string.h>

include<stdio.h>

include<math.h>

const int maxn = 101;

const int INF = 0x3fffffff;

int wmaxn;//权值

int lx[maxn],ly[maxn]; //顶标

int linky[maxn];

int visx[maxn],visy[maxn];//访问

int slack[maxn];

int nx,ny;//x和y的个数，

int  find(int x)

{

    visx[x] = 1;
    for(int y = 0; y < ny; y++)
    {
        if(visy[y])
            continue;
        int t = lx[x] + ly[y] - w[x][y];
        if(t==0)
        {
            visy[y] = 1;
            if(linky[y]==-1 || find(linky[y]))
            {
                linky[y] = x;
                return 1;        //找到增广轨
            }
        }
        else if(slack[y] > t)
            slack[y] = t;
    }
    return 0;                   //没有找到增广轨（说明顶点x没有对应的匹配，与完备匹配(相等子图的完备匹配)不符）

}

int KM()                //返回最优匹配的值

{

    int i,j;

    memset(linky,-1,sizeof(linky));
    memset(ly,0,sizeof(ly));
    for(i = 0; i < nx; i++)
        for(j = 0,lx[i] = -INF; j < ny; j++)
            if(w[i][j] > lx[i])
                lx[i] = w[i][j];
    for(int x = 0; x < nx; x++)
    {
        for(i = 0; i < ny; i++)
            slack[i] = INF;
        while(1)
        {
            memset(visx,0,sizeof(visx));
            memset(visy,0,sizeof(visy));
            if(find(x))                     //找到增广轨，退出
                break;
            int d = INF;
            for(i = 0; i < ny; i++)          //没找到，对l做调整(这会增加相等子图的边)，重新找
            {
                if(!visy[i] && d > slack[i])
                    d = slack[i];
            }
            for(i = 0; i < nx; i++)
            {
                if(visx[i])
                    lx[i] -= d;
            }
            for(i = 0; i < ny; i++)
            {
                if(visy[i])
                     ly[i] += d;
                else
                     slack[i] -= d;
            }
        }
    }
    int result = 0;
    for(i = 0; i < ny; i++)
    if(linky[i]>-1)
        result += w[linky[i]][i];
    return result;

}

int main()

{

    while(1)
    {
        scanf("%d%d",&nx,&ny);
        int a,b,c;
        while(scanf("%d%d%d",&a,&b,&c),a+b+c)//a到b 的权值为c
        {
            w[a][b]=c;
        }
        printf("%d\n",KM());
        break;
    }
    return 0;

}





````

