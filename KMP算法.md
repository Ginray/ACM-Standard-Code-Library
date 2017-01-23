````
#include <cstdio>
#include <cstring>

int next[1005000];
char s[1005000];  char t[1005000];
inline void calnext(char s[],int next[]) {
    int i,j;
    int len = strlen(s);
    next[0]=-1;
    j=-1;
     for(i=1;i<len;i++) {
        while(j>=0&&s[i]!=s[j+1])
            j=next[j];
        if(s[j+1]==s[i])//上一个循环可能因为 j==-1 而不做，此时不能知道s[i]与s[j+1]的关系。故需要此条件
             j++;
        next[i]=j;
    }
}
int KMP(char t[],char s[]) {
    int ans=0;
    int lent=strlen(t);
    int lens=strlen(s);
    if(lent<lens) return 0;
    int i,j;
    j=-1;
    for(i=0;i<lent;i++) {
        while(j>=0&&s[j+1]!=t[i])
            j=next[j];
        if(s[j+1]==t[i])
            j++;
        if(j==lens-1) {
            ans++;
            j=next[j];
        }
    }
    return ans;
}
int main() {
    int n;
    scanf("%d",&n);
    while(n--) {
        scanf("%s%s",s,t); //s代表短串,t代表长串
        int slen=strlen(s);
        int tlen=strlen(t);
        calnext(s,next);
        //slen%(slen-1-next[slen-1])==0
        //slen代表串长，(slen-1-next[slen-1])代表最小重复子串长度
        if(slen%(slen-1-next[slen-1])==0)
            printf("%d\n",slen/(slen-1-next[slen-1]));//求最多重复子串个数
        else
            printf("1\n");
        printf("%d\n",KMP(t,s));//求s在t中的个数
    }
    return 0;
}
````