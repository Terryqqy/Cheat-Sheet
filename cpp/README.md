
# Pointer, reference 
1. A reference is a name constant for an address. You need to initialize the reference during declaration
2. Once a reference is established to a variable, you cannot change the reference to reference another variable.
`int * p1`: static initialization
`int * p1 = new int(1)` :dynamic 
The main differences between static allocation and dynamic allocations are:

- In static allocation, the compiler allocates and deallocates the storage automatically, and handle memory management. Whereas in dynamic allocation, you, as the programmer, handle the memory allocation and deallocation yourself (via new and delete operators). You have full control on the pointer addresses and their contents, as well as memory management.
- Static allocated entities are manipulated through named variables. Dynamic allocated entities are handled through pointers.

  So if you pass in by pointer and want to modify it( point to other variable), you need a pointer to pointer
  Like:

```cpp
#include <iostream>

using namespace std;
void test(int* p1,int* p2,int** p3,int*& p4){
   // you can modify the value p1 point to, it will modify the outer p1 as well, pass pointer by value, you copy the pointer but the pointer still point to the outer value.
   *p1 = 8; 
   cout<<*p1<<endl;//8
   
   // if you point p2 to another variable, you can't modify outer p2 since you pass in the address stored by p2 and let the "p2" inside point to it.
   //When you point p2 inside (it is a copy) to another var, it will not sycn with outer p2.
   // It is because you pass the point by value!!!
   p2 = p1;
   cout<<*p2<<endl;//8
   
  //instead you can pass in pointer by pointer to manipulate p3 point to p2 so you can manipulate the pass in point directly.
   *p3 = p1;
   cout<<**p3<<endl;//8
   
   //Or pass the pointer by reference
   p4 = p1;
   cout<<*p4<<endl;//8
}
int main()
{
    int * p1 = new int(5);
    int * p2 = new int(10);
    int * p3 = new int(15);
    int * p4 = new int(20);
    test(p1,p2,&p3,p4);
    //here we pass in the address of p3 stored
    cout<<*p1<<endl;//8 the value is changed by passing in the pointer
    cout<<*p2<<endl;//10 the value is not changed 
    cout<<*p3<<endl;//8 the value is changed by pointer to pointer
    cout<<*p4<<endl;//8
    return 0;
}
```
## reference of vector and array
&vector is the address of the std::vector object
but &array is the memory address of the first item.
So if you want to pass in by void* which should be the pointer to the first item,
then you need to pass in &vector.front() or array.

# L-Value R-Value
left and right of the equal sign