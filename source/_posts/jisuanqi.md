---
title: 简易计算器
date: 2016-10-16 15:31:59
tags: 数据结构
---

## 数据结构:栈的应用

### 简易计算器

#### 代码

``` cpp
#include <iostream>
#include <stack>
#include <map>
#include <math.h>

using namespace std;

/**
 * 辅助函数: 判断c是不是运算符
 * @param c 待判断的字符
 * @return bool
 */
bool isOP(char c)
{
    char OPs[9] = {'#', '(', ')', '^', '*', '/', '%', '+', '-'};
    for (int i = 0; i < 9 ; ++i)
    {
        if (c == OPs[i])
        {
            return true;
        }
    }
    return false;
}

/**
 * 判断栈顶元素和待入栈元素的优先级
 * @param op1 栈内元素
 * @param op2 待入栈元素
 * @return char '<','>','='
 */
char precede(char op1, char op2)
{
    map<char, int> inner_op;
    map<char, int> outer_op;
    map<char, int>::iterator iter;

    //初始化栈内运算符的优先级
    inner_op['#'] = 0;
    inner_op['('] = 1;
    inner_op['^'] = 7;
    inner_op['*'] = 5;
    inner_op['/'] = 5;
    inner_op['%'] = 5;
    inner_op['+'] = 3;
    inner_op['-'] = 3;
    inner_op[')'] = 8;

    //初始化栈外运算符的优先级
    outer_op['#'] = 0;
    outer_op['('] = 8;
    outer_op['^'] = 6;
    outer_op['*'] = 4;
    outer_op['/'] = 4;
    outer_op['%'] = 4;
    outer_op['+'] = 2;
    outer_op['-'] = 2;
    outer_op[')'] = 1;

    int op1_num = inner_op[op1];
    int op2_num = outer_op[op2];
    if (op1_num < op2_num) {
        return '<';
    } else if (op1_num == op2_num) {
        return '=';
    } else {
        return '>';
    }
}

int operate(int a, int b, char theta)
{
    int result;
    switch (theta)
    {
        case '+':
            result = a + b;
            break;
        case '-':
            result = a - b;
            break;
        case '*':
            result = a * b;
            break;
        case '/':
            result = a / b;
            break;
        case '%':
            result = a % b;
            break;
        case '^':
            result = (int)pow(a,b);
            break;
    }
    return result;
}


//计算中缀表达式的值
int evaluate_expression()
{
    //初始化运算符栈
    stack<char> OPTR;
    OPTR.push('#');

    //初始化操作数栈
    stack<int> OPND;

    char c;
    c = getchar();

    while( c != '#' || OPTR.top() != '#')
    {
        if (!isOP(c)) //如果是操作数，则转化为整形入操作数栈
        {
            int num = c - '0';
            if (num > 9 || num < 0) {
                cout << "请不要乱输入运算符"<< c << endl;
                exit(0);
            }
            OPND.push(num);
            c = getchar();
        }
        else //如果是运算符则判断运算符的优先级
        {
            switch (precede(OPTR.top(), c))
            {
                case '<': //栈顶元素优先权低 
                    OPTR.push(c);
                    c = getchar();
                    break;
                case '=': //优先权相等，脱括号并接收下一个字符
                    OPTR.pop();
                    c = getchar();
                    break;
                case '>': //栈顶元素优先权高，退栈并将运算结果入栈
                    char theta = OPTR.top();
                    OPTR.pop();
                    int b = OPND.top();
                    OPND.pop();
                    int a = OPND.top();
                    OPND.pop();
                    int result = operate(a,b,theta);
                    OPND.push(result);
                    break;
            }
        }
    }
    return OPND.top();
}

int main()
{
    cout << "请输入简易的表达式，以#号结束:" << endl;
    int result = evaluate_expression();
    cout << "result = " << result << endl;
    return 0;
}
```