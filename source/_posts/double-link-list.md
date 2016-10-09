---
title: 循环双链表
date: 2016-10-08 23:28:25
tags: 数据结构
---

## 循环双链表

下面使用C++实现循环双链表:

``` cpp
#include <stdio.h>
#include <stdlib.h>
#include <iostream>

using namespace std;

typedef struct double_linklist
{
    int data;
    struct double_linklist *prior;
    struct double_linklist *next;
}double_linklist;

double_linklist *create_link_list_end(); //尾插法创建双链表
void show_link_list(double_linklist *h); //输出链表
int delete_node_by_value(double_linklist *h, int x); //删除制定元素，题目要实现的方法

/**
 * 主函数调用
 * 1.创建链表
 * 2.建立一个1，2，3，4，5的链表，打印
 * 3.删除数值为4的链表，打印
 * @return 0
 */
int main()
{
    int x;
    int result;
    double_linklist *head;
    printf("创建循环双链表，输入-1结束\n");
    head = create_link_list_end();
    show_link_list(head);
    printf("输入要删除的元素值:");
    scanf("%d", &x);
    result = delete_node_by_value(head, x);
    if (result == 1)
    {
        printf("删除成功\n");
    } else 
    {
        printf("删除失败\n");
    }
    show_link_list(head);
    return 0;
}

int delete_node_by_value(double_linklist *h, int x) 
{   
    double_linklist *p;
    p = h->next;
    while(p != h)
    {
        if (p->data == x)
        {
            double_linklist *t = p;
            p->prior->next = p->next;
            p->next->prior = p->prior;
            p = p->next;
            free(t);
            return 1;
        }
        p = p->next;
    }
    return 0;
}

double_linklist *create_link_list_end()
{
    double_linklist *head, *p, *end;
    int data;

    head = (double_linklist*)malloc(sizeof(double_linklist));
    end = head;
    cin>>data;
    while(data != -1)
    {
        p = (double_linklist*)malloc(sizeof(double_linklist));
        p->data = data;
        p->prior = end;
        end->next = p;
        end = p;
        cin>>data;
    }
    end->next = head;
    head->prior = end;

    return head;
}

void show_link_list(double_linklist *h)
{
    printf("链表为:");
    double_linklist *p;
    p = h->next;
    while(p != h)
    {
        printf("%d -> ", p->data);
        p = p->next;
    }
    printf("<head>\n");
}

```
