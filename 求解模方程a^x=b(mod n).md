    //hdu 2815 Mod Tree  
    #include <cstdio>  
    #include <cstring>  
    #include <cmath>  
    #include <map>  
    #include <iostream>  
    #include <algorithm>  
    using namespace std;  
    #define LL __int64  
    LL gcd(LL a,LL b)  
    {  
        return b==0?a:gcd(b,a%b);  
    }  
    //拓展欧几里得定理，求ax+by=gcd(a,b)的一组解(x,y),d=gcd(a,b)  
    void gcd_mod(LL a,LL b,LL &d,LL &x,LL &y)  
    {  
        if(!b){d=a;x=1;y=0;}  
        else{gcd_mod(b,a%b,d,y,x);y-=x*(a/b);}  
    }  
    //求解模方程d*a^(x-c)=b(mod n)。d,a和n互质，无解返回-1  
    LL log_mod (LL a,LL b,LL n,LL c,LL d)  
    {  
        LL m,v,e=1,i,x,y,dd;  
        m=ceil(sqrt(n+0.5));     //x=i*m+j  
        map<LL,LL>f;  
        f[1]=m;  
        for(i=1;i<m;i++)  //建哈希表，保存a^0,a^1,...,a^m-1  
        {  
            e=(e*a)%n;  
            if(!f[e])f[e]=i;  
        }  
        e=(e*a)%n;//e=a^m  
        for(i=0;i<m;i++)//每次增加m次方，遍历所有1<=f<=n  
        {  
            gcd_mod(d,n,dd,x,y);//d*x+n*y=1-->(d*x)%n=1-->d*(x*b)%n==b  
            x=(x*b%n+n)%n;  
            if(f[x])  
            {  
                LL num=f[x];  
                f.clear();//需要清空，不然会爆内存  
                return c+i*m+(num==m?0:num);  
            }  
            d=(d*e)%n;  
        }  
      
        return -1;  
    }  
    int main()  
    {  
        LL a,b,n;  
        while(scanf("%I64d%I64d%I64d",&a,&n,&b)!=EOF)  
        {  
            if(b>=n)  
            {  
                printf("Orz,I can’t find D!\n");  
                continue;  
            }  
            if(b==0)  
            {  
                printf("0\n");  
                continue;  
            }  
            LL ans=0,c=0,d=1,t;  
            while((t=gcd(a,n))!=1)  
            {  
                if(b%t){ans=-1;break;}  
                c++;  
                n=n/t;  
                b=b/t;  
                d=d*a/t%n;  
                if(d==b){ans=c;break;}//特判下是否成立。  
            }  
            if(ans!=0)  
            {  
                if(ans==-1){printf("Orz,I can’t find D!\n");}  
                else printf("%I64d\n",ans);  
            }  
            else  
            {  
                ans=log_mod(a,b,n,c,d);  
                if(ans==-1)printf("Orz,I can’t find D!\n");  
                else printf("%I64d\n",ans);  
            }  
        }  
        return 0;  
    }  
    /* 
        求解模方程a^x=b(mod n)，n不为素数。拓展Baby Step Giant Step 
        模板题。 
         
        方法： 
        初始d=1,c=0,i=0; 
        1.令g=gcd(a,n),若g==1则执行下一步。否则由于a^x=k*n+b;(k为某一整数),则(a/g)*a^k=k*(n/g)+b/g,(b/g为整除，若不成立则无解) 
    令n=n/g，d=d*a/g，b=b/g,c++则d*a^(x-c)=b(mod n),接着重复1步骤。 
        2.通过1步骤后，保证了a和d都与n互质，方程转换为d*a^(x-c)=b(mod n)。由于a和n互质，所以由欧拉定理a^phi(n)==1(mod n),(a,n互质) 
    可知，phi(n)<=n,a^0==1(mod n),所以构成循环，且循环节不大于n。从而推出如果存在解，则必定1<=x<n。(在此基础上我们就可以用 
    Baby Step Giant Step方法了) 
        3.令m=ceil(sqrt(n)),则m*m>=n。用哈希表存储a^0,a^1,..,a^(m-1)，接着判断1~m*m-1中是否存在解。 
        4.为了减少时间，所以用哈希表缩减复杂度。分成m次遍历，每次遍历a^m长度。由于a和d都与n互质，所以gcd(d,n)=1， 
    所以用拓展的欧几里德定理求得d*x+n*y=gcd(d,n)=1,的一组整数解(x,y)。则d*x+n*y=1-->d*x%n=(d*x+n*y)%n=1-->d*(x*b)%n=((d*x)%n*b%n)%n=b。 
    所以若x*b在哈希表中存在，值为k，则a^k*d=b(mod n),答案就是ans=k+c+i*m。如果不存在，则令d=d*a^m,i++后遍历下一个a^m，直到遍历a^0到a^(m-1)还未找到，则说明不解并退出。 
     
    */  