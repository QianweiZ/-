#include <stdio.h>
#include <stdlib.h>
typedef struct link
{
    int date;
    struct link * next;
}Link;
Link*creatlink(Link*head);
void printnode(Link*head);
void deletenode(Link*head);
Link*addnode(Link*head,int date);
Link*deletion(Link*head,int date);
Link*menu(Link*head);


int main(int argc, const char * argv[])
{
    int i=0,date;
    char ch;
    Link*head=NULL;
    printf("你想增加一个节点吗？y或n");
    scanf("%c",&ch);
    while(ch=='Y'||ch=='y')
    {
        head=creatlink(head);
        printnode(head);
        i++;
        printf("你想再增加一个节点吗？y或n");
        scanf(" %c",&ch);
    }
    head=menu(head);
    printnode(head);
    deletenode(head);
    return 0;
}

Link*menu(Link*head)
{
    int date;
    char ch;
    printf("do you want add a date?(y/n)");
    scanf(" %c",&ch);
    if(ch=='y')
    {
        printf("please input date:");
        scanf("%d",&date);
        head=addnode(head,date);
    }
    printf("do you want delete a date?(y/n)");
    scanf(" %c",&ch);
    if(ch=='y')
    {
        printf("please input date:");
        scanf("%d",&date);
        head=deletion(head,date);
    }
    return head;
}


Link*creatlink(Link*head)
{
    Link *p=NULL,*pr=head;
    int date;
    p=(Link*)malloc(sizeof(Link));
    if(p==NULL)
    {
        printf("没有足够空间分配！");
        exit(0);
    }
    if(head==NULL)
    {
        head=p;
    }
    else
    {
        while (pr->next!=NULL)
        {
            pr=pr->next;
        }
        pr->next=p;
    }
    printf("请输入数据：");
    scanf("%d",&date);
    p->date=date;
    p->next=NULL;
    return head;
}




void printnode(Link*head)
{
    int i=1;
    Link*pr=head;
    while (pr!=NULL)
    {
        printf("%5d%6d\n",i,pr->date);
        pr=pr->next;
        i++;
    }
}


void deletenode(Link*head)
{
    Link*pr=head,*p=head;
    while (p!=NULL)
    {
        pr=p;
        p=p->next;
        free(pr);
    }
    
}

Link*addnode(Link*head,int nodedate)
{
    Link*p=head,*pr=head,*temp=NULL;
    p=(Link*)malloc(sizeof(Link));
    if (p==NULL)
    {
        printf("fail to create!\n");
        exit(0);
    }
    p->date=nodedate;
    p->next=NULL;
    if(head->next==NULL)
    {
        head=p;
    }
    else
    {
        while (nodedate>pr->date&&pr->next!=NULL)
        {
            temp=pr;
            pr=pr->next;
        }
        if(pr->date>=nodedate)
        {
            if(pr==head)
            {
                p->next=head;
                head=p;
            }
            else
            {
                pr=temp;
                p->next=pr->next;
                pr->next=p;
            }
        }
        else
        {
            pr->next=p;
        }
    }
    return head;
}

Link*deletion(Link*head,int date)
{
    Link*p=head,*pr=head;
    if (head==NULL)
    {
        printf("link is null!");
        exit(0);
    }
    while (pr->date!=date&&pr->next!=NULL)
    {
        p=pr;
        pr=pr->next;
    }
    if(pr->date==date)
    {
        if(pr==head)
        {
            head=p->next;
        }
        else
        {
            p->next=pr->next;
        }
        free(pr);
    }
    else
    {
        printf("not find date!\n");
    }
    return head;
}
