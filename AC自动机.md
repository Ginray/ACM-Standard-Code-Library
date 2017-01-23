    #include<stdio.h>
    #include<string.h>
    #include<malloc.h>
    #include<queue>

    #define KIND  26
    //为可能的种类，假如是小写英文就是26  int pos=str[k]-'a';
    //不可见字符就是 128  int pos=str[k]-' ';
    //注意更改~!!
    using namespace std;
    char str[1000000+100];

    struct node
    {
        int count;
        struct node *next[KIND];
        struct node *fail;
        void init()
        {
            int i;
            for(i=0;i<KIND;i++)
                next[i]=NULL;      //接下去要跳转的地方
            count=0;               //这里保存的是单词的个数  也可以保存单词的序号什么的
            fail=NULL;
        }
    }*root;
    void insert()
    {
        int len,k;
        node *p=root;
        len=strlen(str);
        for(k=0;k<len;k++)
        {
            int pos=str[k]-'a';    //注意更改
            if(p->next[pos]==NULL)
            {
                p->next[pos]=new node;
                p->next[pos]->init();
                p=p->next[pos];
            }
            else
                p=p->next[pos];
        }
        p->count++;
    }
    void getfail()
    {
        int i;
           node *p=root,*son,*temp;
           queue<struct node *>que;
           que.push(p);
           while(!que.empty())
           {
               temp=que.front();
               que.pop();
               for(i=0;i<KIND;i++)
               {
                   son=temp->next[i];
                   if(son!=NULL)
                   {
                       if(temp==root) {son->fail=root;}
                       else
                       {
                           p=temp->fail;
                           while(p)
                           {
                               if(p->next[i])
                               {
                                   son->fail=p->next[i];
                                   break;
                               }
                               p=p->fail;
                           }
                           if(!p)  son->fail=root;
                       }
                       que.push(son);
                   }
               }
           }
    }
    void query()
    {
        int len,i,cnt=0;

        //int flag[5500];  记录单词是不是被访问过了
        len=strlen(str);
        node *p,*temp;
        p=root;
        for(i=0;i<len;i++)
        {
            int pos=str[i]-'a';  //注意更改
            while(!p->next[pos]&&p!=root)  p=p->fail;
            p=p->next[pos];
            if(!p) p=root;
            temp=p;

            while(temp!=root)
            {
                if(temp->count>=0)        //这时候flag数组在这里判断一下就行了
                {
                    cnt+=temp->count;
                    temp->count=-1;      // 这里把原来的值清空了  假如一个AC自动机要多次被访问，可以用一个flag数组来保存是否被访问过
                    					 //假如可以计算重复的子串 就删除 temp->count=-1;这句。 
                }
              
                temp=temp->fail;
            }
        }
        printf("%d\n",cnt);     //长串中有多少个AC自动机中的子串
    }
    int main()
    {
        int cas,n;
        scanf("%d",&cas);
        while(cas--)
        {
            root=new node;
            root->init();
            root->fail=NULL;
            scanf("%d",&n);
            int i;
            getchar();
            for(i=0;i<n;i++)
            {
                gets(str);
                insert();
            }
            getfail();
            gets(str);  //假如有多个子串，记得添加flag数组
            query();
        }
        return 0;
    }
