---
title: 栈的链式存储结构      
date: 2016-10-16 14:35:16
tags: 数据结构
---

## 数据结构:栈的实现

### 实现方式2: 基于链表的实现

``` cpp
#include <iostream>  
using namespace std;  

typedef int dataType;  
  
struct node                   //链栈节点  
{  
    dataType data;            //数据域  
    node *next;               //指针域  
};  
  
class ls  
{  
public:  
    ls();  
    ~ls();  
    void push(dataType var); //压栈  
    int pop();              //出栈. 
    dataType stackTop();     //取栈顶元素,栈顶无变化.
    bool isEmpty();          //判空.空返回true,反之返回false  
    //bool isFull();         //判满.链栈是动态分配内存空间的,无需判满
    void output();           //遍历打印链栈  
  
private:  
    node *top;               //栈顶指针.top=NULL表示为空栈  
};  

ls::ls()  
{  
    top = NULL;            //top=NULL表示链栈为空  
}  
  
ls::~ls()  
{  
    node *ptr = NULL;  
  
    while(top != NULL)     //循环释放栈节点空间  
    {  
        ptr = top->next;  
        delete top;  
        top = ptr;  
    }  
}  
  
void ls::push(dataType var)  
{  
    node *ptr = new node;  
  
    ptr->data = var;        //新栈顶存值  
    ptr->next = top;        //新栈顶指向旧栈顶  
  
    top = ptr;              //top指向新栈顶  
}  
  
int ls::pop()  
{
    if (isEmpty())
    {
        cout<< "栈空，无法出栈" << endl;
        return -1;
    }
    int delete_value = top->data;  
    node *ptr = top->next;  //预存下一节点的指针  
    delete top;             //释放栈顶空间  
    top = ptr;              //栈顶变化
    return delete_value;  
}  
  
dataType ls::stackTop()  
{
    if (isEmpty())
    {
        cout<< "栈空，无法出栈" << endl;
        return -1;
    }  
    return top->data;       
}  
  
bool ls::isEmpty()  
{  
    return top == NULL;     //栈顶为NULL表示栈空  
}

void ls::output()
{
    if (isEmpty())
    {
        cout<< "求塞" << endl;
        return;
    }
    node *p = top;
    while (p)
    {
        cout << p->data << "->";
        p = p->next;
    }
    cout << "bottom" << endl;
}  

int main()  
{
    /**
     * stack1: 测试入栈、出栈、取栈顶元素操作
     * 1) 1，2，3，入栈，打印3->2->1->bottom
     * 2) 出栈1次，打印2->1->bottom, 同时打印x=3
     * 3) 取栈顶元素, 打印2->1->bottom, 同时打印y=2
     */
    ls stack1;
    int x; //出栈元素保存在x
    int y; //取栈顶元素保存在y
    stack1.push(1);
    stack1.push(2);
    stack1.push(3);
    stack1.output();
    x = stack1.pop();
    stack1.output();
    cout << "x = " << x << endl;
    y = stack1.stackTop();
    stack1.output();
    cout << "y = " << y << endl;

    /**
     * stack2: 测试判断栈空、链栈无需判满
     * 1) 取栈顶元素，提示栈空
     * 2) 首先判断栈是否为空，为空则给出提示
     */
    ls stack2;
    stack2.stackTop();
    if (stack2.isEmpty())
    {
        cout << "栈 stack2 为空" << endl;
    }
    return 0;  
}  
```
