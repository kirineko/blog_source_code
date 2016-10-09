---
title: 栈
date: 2016-10-08 22:25:52
tags: 数据结构
---

## 数据结构:栈的实现

下面使用C++实现顺序栈~:

``` cpp
#include <iostream>
using namespace std;

template <class T>
class Stack
{
public:
    Stack(int max_stack_size = 10); //构造函数
    ~Stack(); //析构函数
    bool IsEmpty(); //判空
    bool IsFull(); //判满
    T Top(); //取栈顶元素
    Stack<T>& Add(const T& x); //入栈
    Stack<T>& Del(T& x); //出栈
    void MakeEmpty(); //栈置空
    void Output(); //输出栈元素    
private:
    int top; //栈顶指针
    int MaxTop; //栈容量
    T *stack; //栈数组
};

template<class T>
Stack<T>::Stack(int max_stack_size)
{
    MaxTop = max_stack_size - 1;
    stack = new T[max_stack_size];
    top = -1;
}

template<class T>
Stack<T>::~Stack()
{
    delete [] stack;
}

template<class T>
bool Stack<T>::IsEmpty()
{
    return top == -1;
}

template<class T>
bool Stack<T>::IsFull()
{
    return top == MaxTop;
}

template<class T>
void Stack<T>::MakeEmpty()
{
    top = -1;
}

template<class T>
Stack<T>& Stack<T>::Add(const T& x)
{
    if (IsFull())
    {
        cout<<"塞不下了"<<endl;
        return *this;
    }
    top = top + 1;
    stack[top] = x;
    return *this;
}

template<class T>
Stack<T>& Stack<T>::Del(T& x)
{
    if (IsEmpty())
    {
        cout<<"求塞"<<endl;
        return *this;
    }
    x = stack[top];
    top = top - 1;
    return *this;
}

template<class T>
T Stack<T>::Top()
{
    int x;
    if (IsEmpty())
    {
        cout<<"求塞"<<endl;
        return 0;
    }
    x = stack[top];
    return x;
}

template<class T>
void Stack<T>::Output()
{
    if (IsEmpty())
    {
        cout<<"no element"<<endl;
        return;
    }
    for (int i = top; i > -1; --i)
    {
        cout << stack[i] << "->";
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
    Stack<int> stack1;
    int x; //出栈元素保存在x
    int y; //取栈顶元素保存在y
    stack1.Add(1);
    stack1.Add(2);
    stack1.Add(3);
    stack1.Output();
    stack1.Del(x);
    stack1.Output();
    cout << "x = " << x << endl;
    y = stack1.Top();
    stack1.Output();
    cout << "y = " << y << endl;

    /**
     * stack2: 测试判断栈空、栈满
     * 1) 取栈顶元素，提示栈空
     * 2) 首先判断栈是否为空，为空则给出提示
     * 3) 循环向栈中添加11个元素
     * 4) 判断栈是否满，栈满则给出提示
     */
    Stack<int> stack2;
    stack2.Top();
    if (stack2.IsEmpty())
    {
        cout << "栈 stack2 为空" << endl;
    }
    for (int i = 0; i <= 10; ++i)
    {
        stack2.Add(i);
    }
    if (stack2.IsFull())
    {
        cout << "栈 stack2 为满" << endl;
    }
    cout << "stack2:";
    stack2.Output();
}
```
