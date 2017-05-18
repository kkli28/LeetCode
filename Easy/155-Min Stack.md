> Description

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

```
push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
```

```
Example:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

> Idea

使用 `vector<int>` 来模拟栈，可以方便地找到最小值。入栈就是 `push_back`，出栈就是 `pop_back`，
需要注意的是每次入栈需要将入栈的数与最小值比较以更新最小值（如果每次getMin都计算则影响性能，因此
使用一个变量min来保存），每次出栈也需要更新最小值。出栈时，如果最末尾元素（出栈的元素）不是最小值，
则不需要更新min，否则需要更新min。

> Solution

```C++
class MinStack {
public:
    /** initialize your data structure here. */
    vector<int> vec;
    int min=INT_MAX;
    MinStack() {
        
    }
    
    int func(){
        min=INT_MAX;
        int size=vec.size();
        if(size==0) return INT_MAX;
        if(size==1) return vec[0];
        for(int i=0;i<size;++i)
            if(vec[i]<min) min=vec[i];
        return min;
    }
    
    void push(int x) {
        vec.push_back(x);
        if(x<min) min=x;
    }
    
    void pop() {
		int back = vec.back();
		vec.pop_back();
		if (back == min) min = func();
	}
    
    int top() {
        return vec.back();
    }
    
    int getMin() {
        return min;
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```
