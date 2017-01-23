~~~
include<stdio.h>

include<string.h>

include<stdlib.h>

int flag;

typedef struct node  

{

    int data;
    struct node *childs[2];
    struct node ()
    {
    data=0;
    for(int i=0;i<2;i++)
    	childs[i]=NULL;
    
    }

}node;

node root,cur,*newn;

void insert (char *x)

{

    int i,m;
    cur=root;
    
     for(i=0;i<strlen(x);i++)  
    {  
        m=x[i]-'0';  
        if(cur->childs[m]!=NULL)  
        {  
            cur=cur->childs[m];  
            if(i==strlen(x)-1||cur->data==1)  
            {  
                flag=0;  
                break;  
            }  
        }  
        else  
        {  
            newn=new node;  
            cur->childs[m]=newn;  
            cur=newn;  
        }  
    }  
    cur->data=1;  

}

// void innnt (node *head)

//{

//	

//	  for(int i=0;i<2;i++)  

//    if(head->childs[i]!=NULL)  

//    innnt(head->childs[i]);  

//    innnt(head);  

//

//

// }

int main()

{

int num=1;

char x[15];

    while(scanf("%s",x)!=EOF)
    {
    flag=1;
    root=new node;
    insert (x);
    while(scanf("%s",x),strcmp(x,"9"))
    {
    if(!flag)
    continue;
    insert (x);
    
    }

if(!flag)  

        printf("Set %d is not immediately decodable\n",num++);  
        else  
        printf("Set %d is immediately decodable\n",num++);  

   // innnt(root);

	

    }

    return 0;

}





~~~

