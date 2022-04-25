---
title: C 语言链表的饿创建
date: 2021-03-29 23:57:25
categories: C
tags: C
index_img: https://w.wallhaven.cc/full/47/wallhaven-477x9o.jpg
banner_img: https://w.wallhaven.cc/full/42/wallhaven-42yxry.jpg
---

## 单链表的创建

编辑时间：2021-3-29



创建的方法——（有无头结点）头插法、（有无头结点）尾插法。

#### 定义链表结点

```c
struct node{
    int data;
    struct node *next;
};
```

#### 有头结点 

##### 1.头插法

从一个空链表开始，重复读入数据，生成新的结点，将读入的数据存放到新结点的数据域中，然后将新结点插入到当前链表的表头结点之后，直至读入结束标志。

>链表中数据的关系：
>
>先读取的数据离头结点越远。  链表输出数据的顺序与输入顺序相反。

```c
//形参采用二重指针形式
void createNode(struct ListNode **head)
{
    *head = (struct ListNode *)malloc(sizeof(struct ListNode)); //head分配地址
    struct ListNode *temp;                                      //声明指针temp，用于指向新生成的链表结点
    (*head)->next = NULL;                                       //head初始化为空
    temp = *head;                                               //temp指向尾部的结点

    int n; //链表长度
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        printf("input:");
        scanf("%d", &node->data);
        node->next = temp->next; //将node->next指向链表首元结点
                                 //插入第一个结点时，node->next = NULL
        temp->next = node;       // head->next再指向node
                                 //完成将node插入到头结点之后
    }
}

//node->next = temp->next
//temp->next = node
//两句顺序不能交换，交换后会失去head后面的结点
//故而先将head之后的结点链接到node之后
//再将node链接到head->next
```

```c
//返回头结点
struct ListNode *create()
{
    struct ListNode *head;
    head = (struct ListNode *)malloc(sizeof(struct ListNode)); //head分配地址
    head->next = NULL;                                         //head初始化为空
    int n;                                                     //链表长度
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        printf("input:");
        scanf("%d", &node->data);
        node->next = head->next; 
        head->next = node;       
    }
    return head;
}
```

##### 2.尾插法

将新结点 插到当前单链表的表尾上。增加一个尾指针Tial， 使之指向当前单链表的表尾。

保证了输入数据的顺序与链表顺序的相同。

```c
//形参采用二重指针形式
void createNode(struct ListNode **head)
{
    *head = (struct ListNode *)malloc(sizeof(struct ListNode)); //head分配地址
    struct ListNode *Tail;                                     //Tial尾指针
    Tail = *head;
    int n;                                                     //链表长度
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        printf("input:");
        scanf("%d", &node->data);
        Tail->next = node;//新结点接在Tail后面
        Tail = node;      //尾指针指向新结点，新结点作为链表尾部
    }
    Tail->next = NULL;
}
```

```c
//返回头结点
struct ListNode *create()
{
    struct ListNode *head;
    head = (struct ListNode *)malloc(sizeof(struct ListNode)); //head分配地址
    struct ListNode *Tail = head;
    int n;                                                     //链表长度
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        printf("input:");
        scanf("%d", &node->data);
        Tail->next = node;//新结点接在Tail后面
        Tail = node;      //尾指针指向新结点，新结点作为链表尾部
    }
    Tail->next = NULL;
    return head;
}
```

#### 无头结点 

##### 1.头插法

输入顺序与输出顺序相反

```c
void create_noHeadNode_HeadInsert(struct ListNode **head)
{
    //头插法
    (*head) = (struct ListNode *)malloc(sizeof(struct ListNode));
    (*head) = NULL;
    int n; //链表长度
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        scanf("%d", &node->data);
        node->next = (*head);
        (*head) = node;
    }
}
```



##### 2.尾插法

输入顺序与输出顺序相同

```c
void create_noHeadNode_TailInsert(struct ListNode **head)
{
    //尾插法
    (*head) = (struct ListNode *)malloc(sizeof(struct ListNode));
    //(*head)->next = NULL;
    struct ListNode *tail = (*head);//tail为尾结点
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        scanf("%d", &node->data);
        tail->next = node;
        tail = node;
    }
    (*head) = (*head)->next;//head结点没有存储上数据，故直接让其指向储有第一个数据的head->next
    tail->next = NULL;//尾结点下一个为空
}
```

#### 全部代码

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Students
{
    //char name[20];
    int age;
    float marks;
} Student;

struct ListNode
{
    int data;
    struct ListNode *next;
};

//有头结点
struct ListNode *create();               //尾插法
void createNode(struct ListNode **head); //头插法
void printNode(struct ListNode *head);
//无头结点
void createNode_nohead(struct ListNode **head); //头插法
void create_nohead(struct ListNode **head);     //尾插法
void PrintNode_Nohead(struct ListNode *head);
int main()
{
    struct ListNode *HeadI, *TailI;     //有头结点
    struct ListNode *noHeadI, *noTailI; //无头结点
    //创建链表
    createNode(&HeadI);
    printNode(HeadI);

    TailI = create();
    printNode(TailI);

    createNode_nohead(&noHeadI);
    PrintNode_Nohead(noHeadI);

    create_nohead(&noTailI);
    PrintNode_Nohead(noTailI);
    system("pause");
    return 0;
}
void PrintNode_Nohead(struct ListNode *head)
{
    while (head)
    {
        printf("%d ", head->data);
        head = head->next;
    }
    printf("\n");
}
//头插法
void createNode(struct ListNode **head)
{
    *head = (struct ListNode *)malloc(sizeof(struct ListNode)); //head分配地址
    struct ListNode *temp;                                      //声明指针temp，用于指向新生成的链表结点
    (*head)->next = NULL;                                       //head初始化为空
    temp = *head;                                               //temp指向尾部的结点
    int n;                                                      //链表长度
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        printf("input:");
        scanf("%d", &node->data);
        node->next = temp->next; //将node->next指向链表头结点之后的内容
        temp->next = node;       // head->next再指向node
                                 //完成将node插入到头结点之后
    }
}
//尾插法
struct ListNode *create()
{
    struct ListNode *head;
    head = (struct ListNode *)malloc(sizeof(struct ListNode)); //head分配地址
    struct ListNode *Tail = head;
    int n; //链表长度
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        printf("input:");
        scanf("%d", &node->data);
        Tail->next = node;
        Tail = node;
    }
    Tail->next = NULL;
    return head;
}
void printNode(struct ListNode *head)
{
    while (head->next)
    {
        head = head->next;
        printf("%d\n", head->data);
    }
}
void createNode_nohead(struct ListNode **head)
{
    //头插法
    (*head) = (struct ListNode *)malloc(sizeof(struct ListNode));
    (*head) = NULL;
    int n; //链表长度
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        scanf("%d", &node->data);
        node->next = (*head);
        (*head) = node;
    }
    //(*head)->next = NULL;
}
void create_nohead(struct ListNode **head)
{
    //尾插法
    (*head) = (struct ListNode *)malloc(sizeof(struct ListNode));
    //(*head)->next = NULL;
    struct ListNode *tail = (*head);
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        struct ListNode *node = (struct ListNode *)malloc(sizeof(struct ListNode));
        scanf("%d", &node->data);
        tail->next = node;
        tail = node;
    }
    (*head) = (*head)->next;
    tail->next = NULL;
}
```
