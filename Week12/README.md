## Recursion
```c++
void printf(int iter){
    if(iter < 10){
        cout >> "Hello World";
        iter++;
        printf(iter)
    }
}

int main(){
    int iter = 0;
    printf(iter);

    return 0;
}
```

### Types of recursion
#### Linear
Going form start to bottom
```c++
int sum(int number, int result = 0){ // if result is not passed, default is 0 !!
    if(number <= 0)
        return result;
    sum(number-1, result + number); //f here "return" is not written it will be
    // executable and compilable thanks to some processor registries
}
```

#### Tail recursion
Returning from the bottom to the start
```c++
int sum(int n ){
    if(n == 0)
        return 0;
    return n + sum(n-1);
}
```

#### Tree like recursion
There are many branches in with the recursion is called.  
Good examples the calculation the Fibonacci sequence.  
It is not a good type of recursion because it runs the calculation for the same
values at least 2 times because of the tree structure.
```c++
unsigned int fib(unsigned n){
    if(n < 2)
        return n;
    return fib(n-1) + fib(n - 2);
}
```
So in order to escape this calculation we remember the values
Very fast
```c++
unsigned int fib2_rec(unsigned int first, unsigned sec, unsigned int n){
    if(n == 0)
        return first;
    if(n == 1)
        return second;
    return fib2_rec(sec, first + sec, n - 1);
}
```

**Good practice will be doing binary search first with iterator the with rec**

### Spectre and  meltdown and some low level shit
Semerjiev is explaining about instruction sets and registries.  
He showed us how the "if" operator makes "goto" in the registries memory.  

`TODO`: Check how the "if" tree of the code generates registry address to the
goto jumps when "if" is executed or just how the instruction set is generated
with registry pointer to the memory

So in modern chips not every instruction is taken from the instruction set
which is maybe in L1 cache? So to prevent this the chip loads whole blocks
of instruction from the cache to the registries  

Chips have 2 ways of optimizing:
* Speculation execution - RIGHT/WRONG checking    
* Parallelism  

Mechanism of Meltdown: Takes uncleared cache data which is actually unprotected  

Spectre even could inject code  

Speculation control Script

## How the functions work in the stack by Semerjiev:

Exactly after the stack pointer in the begging, the arguments are written.
After that there is the functions and its local variables.
So in order to go back to the starting pointer after execution of the function,
before the function call the pointer goes back with help of a base pointer or
frame pointer which helps to navigate back before the function call.  

This thing we learned in OS back in ELSYS - base pointer is the start of the
stack in this case the function and navigates with stack pointer  
