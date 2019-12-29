# Create stack without STL
```c++
struct stack {
    int n = 0;
    int ss[maxn];

    void push(int a) {
        n++;
        ss[n] = a;
    }
    void pop() {
        n--;
    }
    int top() {
        return ss[n];
    }
    bool empty() {
        if(n == 0)
            return true;
        else
            return false;
    }
    int size() {
        return n;
    }
};
```
