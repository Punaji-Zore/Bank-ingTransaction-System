#include<stdio.h>
#include<stdlib.h>

typedef struct node
{
    int data;
    struct node *next;
}node;

typedef struct LL
{
    node *front;
    node *rear;
}LL;

void enqueue(LL *l, int x)
{
    node *newrec;
    newrec=(node*)malloc(sizeof(node));
    newrec->data=x;
    newrec->next=NULL;
    if(l->front==NULL)
    {
        l->front=newrec;
        l->rear=newrec;
    }
    else
    {
        l->rear->next=newrec;
        l->rear=newrec;
    }
    printf("\nTransaction of Rs.%d added successfully!",x);
}

int isempty(LL *l)
{
    if(l->front==NULL)
        return 1;
    else
        return 0;
}

void dequeue(LL *l)
{
    node *p;
    if(isempty(l))
    {
        printf("\nNo transactions to process...");
    }
    else
    {
        p=l->front;
        printf("\nProcessed Transaction of Rs.%d",p->data);
        l->front=l->front->next;
        if(l->front==NULL)
            l->rear=NULL;
        free(p);
    }
}

void display(LL *l)
{
    node *p;
    int c=0;
    if(isempty(l))
    {
        printf("\nNo pending transactions...");
    }
    else
    {
        p=l->front;
        while(p!=NULL)
        {
            printf("\nRs.%d",p->data);
            c++;
            p=p->next;
        }
        printf("\nTotal Pending Transactions=%d",c);
    }
}

int main()
{
    int ch,x;
    LL l;
    l.front=NULL;
    l.rear=NULL;
    while(1)
    {
        printf("\nBanking System ");
        printf("\n1-Add Transaction");
        printf("\n2-Process Transaction");
        printf("\n3-Display Transactions");
        printf("\n4-EXIT");
        printf("\nEnter Choice=");
        scanf("%d",&ch);
        if(ch==4)
            break;
        switch(ch)
        {
            case 1:
            {
                printf("\nEnter Transaction Amount=");
                scanf("%d",&x);
                enqueue(&l,x);
            }
            break;
            case 2:
            {
                dequeue(&l);
            }
            break;
            case 3:
            {
                display(&l);
            }
            break;
            default:
            {
                printf("\nInvalid Choice...");
            }
        }
    }
    return 0;
}
