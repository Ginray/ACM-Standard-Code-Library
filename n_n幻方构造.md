````
/单偶数幻方的构造/

include<stdio.h>

include<string.h>

include<stdlib.h>

define MAXN 500

int aMAXN;

int bMAXN;

int x;

int m;

void swap(int a1,int a2,int b1,int b2)

{

    int flag;
    flag=a[a1][a2];
    a[a1][a2]=a[b1][b2];
    a[b1][b2]=flag;
    return ;

}

void solve1   (int f)  //奇数幻方的构造

{

    int h;
    if(f==1)
     h=x/2;
    else
     h=x;
    
    int i,j;
    int flagi,flagj;
    int flag=2;
    a[1][ h/2+1]=1;
    
    int sum=1;
    i=1;
    j=h/2+1;

   bi=1;

    while(sum!=h*h)
    {
       flagi=i-1;
       flagj=j+1;
        if(flagi<1)
            flagi=h;
        if(flagj>h)
            flagj=1;
    
        if(b[flagi][flagj]==1||(i==1&&j==h))
        {
            a[i+1][j]=flag++;
            b[i+1][j]=1;
            i=i+1;
            if(i<1)
                i=h;
            sum++;
        }
        else
        {
                a[flagi][flagj]=flag++;
                b[flagi][flagj]=1;
                i=flagi;
                j=flagj;
                sum++;
        }
    
    }

   return ;

}

void solve2()//单偶数幻方

{

    solve1(1);
    int i,j;
    int h=x/2;
    int j1,j2;
    m=(x-2)/4;
    
        for(j1=1;j1<=(x/2);j1++)
        {
                for(j2=1;j2<=(x/2);j2++)
                {
                    a[j1+(x/2)][j2+(x/2)]=(4*m*m+4*m+1)+a[j1][j2];
                    a[j1][j2+(x/2)]=2*(4*m*m+4*m+1)+a[j1][j2];
                    a[j1+(x/2)][j2]=3*(4*m*m+4*m+1)+a[j1][j2];
                }
        }

     swap((h/2)+1,(h/2+1),(h/2+1+h),(h/2+1));
      for(i=1;i<=h;i++)
      {
          if(i!=(h/2)+1)
            for(j=1;j<=m;j++)
                swap(i,j,i+h,j);
        else
                for(j=1;j<m;j++)
                swap(i,j,i+h,j);
      }
      for(i=1;i<=h;i++)
      for(j=x+2-m;j<=x;j++)
        swap(i,j,i+h,j);
    
        return ;

}

void solve3()  //双偶数幻方

{

    int flag=1;
    int i,j;
    int nx,ny;

   int fx;

    for(i=1;i<=x;i++)
        for(j=1;j<=x;j++)
           a[i][j]=flag++;

   for(nx=0;nx<(x/4);nx++)

   {

       for(ny=0;ny<=(x/4);ny++)
       {
              for(i=1;i<=4;i++)
                   {
                      a[nx*4+i][ny*4+i]=x*x+1-a[nx*4+i][ny*4+i];
                     a[nx*4+4+1-i][ny*4+i]=x*x+1-a[nx*4+4+1-i][ny*4+i];
                   }
    
       }

   }

     return ;

}

int main()

{

   while( scanf("%d",&x)!=EOF)

   {

       memset(a,0,sizeof(a));
       memset(b,0,sizeof(b));
    int i,j;
    if(x%2==0&&x%4!=0)
    {
        if(x==2)
        {
            printf("None\n");
            continue;
        }
    solve2();
    int sum=0;
    for(i=1;i<=x;i++)
    {
        sum=0;
        for(j=1;j<=x;j++)
        {
            printf("%3d ",a[i][j]);
            sum+=a[i][j];
        }
        printf("           sum=%d\n",sum);
    
    }

  continue;

   }

   else if (x%2!=0)

   {

    solve1(2);
    int sum=0;
    for(i=1;i<=x;i++)
    {
        sum=0;
        for(j=1;j<=x;j++)
        {
            printf("%3d ",a[i][j]);
            sum+=a[i][j];
        }
        printf("           sum=%d\n",sum);
    
    }

   }

       else if(x%4==0)
    {
        solve3();
    int sum=0;
    for(i=1;i<=x;i++)
    {
        sum=0;
        for(j=1;j<=x;j++)
        {
            printf("%3d ",a[i][j]);
            sum+=a[i][j];
        }
        printf("           sum=%d\n",sum);

    }

  continue;

}

   }

    return 0;

}



````

