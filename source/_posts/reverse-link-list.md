---
title: 反转单链表
date: 2016-10-08 23:25:52
tags: 数据结构
---

## 反转单链表

下面使用C++实现反转单链表:

``` cpp
#include <stdio.h>
#include <stdlib.h>
#include <iostream>

using namespace std;

typedef struct linklist
{
    int data;
    struct linklist *next;
}linklist;

linklist *create_link_list_end(); //尾插法创建单链表
void show_link_list(linklist *h); //输出链表
linklist *reverse_link_list(linklist *h); //反转单链表，题目要实现的方法

/**
 * 主函数调用
 * 1.创建链表
 * 2.建立一个1，2，3，4，5的链表，打印
 * 3.反转单链表，打印
 * @return 0
 */
int main()
{
    int x;
    int result;
    linklist *head;
    printf("创建单链表，输入-1结束\n");
    head = create_link_list_end();
    show_link_list(head);
    printf("反转单链表:\n");
    linklist *new_head = reverse_link_list(head);
    show_link_list(new_head);
    return 0;
}

linklist *reverse_link_list(linklist *h)
{
    linklist *p = NULL;
    linklist *prior;
    linklist *next;
    if (h == NULL)
    {
        return h;
    }

    p = h;
    next = p->next;
    p->next = NULL;
    prior = p;
    p = next;
    while(p)
    {
        next = p->next;
        p->next = prior;
        prior = p;
        p = next;
    }
    h = prior;
    return h;
}

linklist *create_link_list_end()
{
    linklist *head, *p, *end;
    int data;

    head = NULL;
    end = head;
    cin>>data;
    while(data != -1)
    {
        p = (linklist*)malloc(sizeof(linklist));
        p->data = data;
        if (head == NULL)
        {
            head = p;
        } else 
        {
            end->next = p;   
        }
        end = p;
        cin>>data;
    }
    if (end)
    {
        end->next = NULL;
    }
    return head;
}

void show_link_list(linklist *h)
{
    printf("链表为:");
    linklist *p;
    p = h;
    while(p != NULL)
    {
        printf("%d -> ", p->data);
        p = p->next;
    }
    printf("<NULL>\n");
}
```