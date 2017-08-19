# Universe
It just something
#include <iostream>
#include <memory.h>

#define MAXLEN 1000

// High Precision
struct hp
{
    int s[MAXLEN];
    int len;
};

// 1234
// s[0], s[1], s[2], s[3];
// 4      3      2     1

hp Add(hp a, hp b)
{
    hp c;
    memset(c.s, 0, sizeof(c.s));
    
    c.len = (a.len > b.len)?a.len:b.len;
    c.s[0] = a.s[0] + b.s[0];
    for (int i = 1; i < c.len; i++)
    {
        c.s[i] = c.s[i-1] / 10 + a.s[i] + b.s[i];
        c.s[i-1] %= 10;
    }
    
    if (c.s[c.len-1] > 9)
    {
        c.s[c.len] = c.s[c.len-1]/10;
        c.s[c.len-1] %= 10;
        c.len ++;
    }
    
    return c;
}

/* 
hp Minus()
{
}
*/

hp Multi(hp a, hp b)
{
    hp c;
    memset(c.s, 0, sizeof(c.s));//QTB & GZJ
    
    for (int i = 0; i < a.len; i++)
        for (int j = 0; j < b.len; j++)
        {
            c.s[i+j] += a.s[i] * b.s[j];
            c.s[i+j+1] += c.s[i+j] / 10;
            c.s[i+j] %= 10;
        }
        
    c.len = a.len + b.len - 1;
    while (c.len > 1 && c.s[c.len-1] == 0)
        c.len --;
    
    return c;
}

hp MultiSingle(hp a, int b)
{
    hp c;
    memset(c.s, 0, sizeof(c.s));
    
    c.s[0] = a.s[0] * b;
    for (int i = 1; i < a.len; i++)
    {
        c.s[i] = a.s[i] * b + c.s[i-1] / 10;
        c.s[i-1] %= 10;   
    }
    
    c.len = a.len; 
    while (c.s[c.len-1] > 9)
    {
        c.s[c.len] = c.s[c.len-1]/10;
        c.s[c.len-1] %= 10;
        c.len ++;
    }
    
    return c;
}
