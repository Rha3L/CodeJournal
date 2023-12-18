## Definition

Pointers are variables that store address of another variable.

```
int a;
int* p;
p = &a; //p stores address of a
*p //value at address pointed by p (which is a) (dereferencing)
```

## Pointer Arithmetic

```
#include <stdio.h>
int main()
{
  int a = 10;//size of integer is 4 bytes
  int *p;
  p = &a;
  printf("%d\n", p); //if p is address 2002
  printf("%d\n", p+1); // p + 1 is address 2006
}
```

## Pointer Types

Pointers are strongly typed.

### Typecasting

Typecasting changes the type of a variable just for that operation.

Void pointer - Generic pointer

```
#include <stdio.h>
int main()
{
  int a = 1025;
  int *p;
  p = &a;
  printf("Address = %d, value = %d\n", p, *p);
  //Void pointer
  void *p0;
  p0 = p;
  printf("Address = %d\n", p0); //*p0 will give error
}
```

- Cannot use \* to dereference a void pointer
- Cannot perform pointer arithmetic

## Pointers to Pointers

```
int x = 5;
int* p;
p = &x;
int** q;
q = &p; //q stores address of pointer p
int*** r;
r = &q; //r stores address of pointer q
printf("%d\n", *p); //5
printf("%d\n", *q); //address of p
printf("%d\n", *(*q)); //5
printf("%d\n", *(*r)); //address of p
printf("%d\n", *(*(*r))); //5
***r = 10; //x changes to 10
**q = *p + 2; //x changes to 12
```

## Pointer as function arguments

### Call By Value

```
#include <stdio.h>
void Increment(int p) //p is formal argument
{
  p = p + 1;
}
int main()
{
  int a = 10;
  Increment(a); //a is actual argument
  printf("a = %d\n", a); //a is 10
}
```

- Passed in copy value of a
- p and a have same value but different memory addresses
- local variable will not be called or used outside the function
- In Stack, Increment function stack frame will pop out once the function is executed. But main function continues executing in Stack. That's why main function cannot access the local variable in Increment function
- the Inrement function will not change the value of a in main function

### call by reference

```
#include <stdio.h>
void Increment(int *p)
{
  *p = (*p) + 1;
}
int main()
{
  int a = 10;
  Increment(&a);
  printf("a = %d\n", a); // a is 11
}
```

- Passed in the address of a
- the Increment function will change the value of a

## Pointers & Arrays

- Data in arrays are conscutive in memory
- Assign an array to a pointer is equivalent to assigning the memory address of the first element of the array to the pointer

```
int A[5];
int* p;
p = A; //A is base address of the array
print A //address of the first element
print A+1 //address of the second element
print &A[i] or (A+i) //address of element at index i
print *A //value of the first element
print *(A+1); //value of the second element
print A[i] or *(A+i) //value of element at index i
```

### Arrays as function arguments

```
#include<stdio.h>
int SumOfElements(int A[], int size)
{
  int i, sum = 0;
  for (i = 0; i < size; i++)
  {
    sum += A[i];
  }
  return sum;
}
int main()
{
  int A[] = {1,2,3,4,5};
  int size = sizeof(A)/sizeof(A[0]);
  int total = SumOfElements(A,size);
  printf("Sum of elements = %d\n",total);
}
```

### Character Arrays and Pointers

### Pointers & 2D arrays

### Pointers & multidemensional arrays

## Pointers & Memory
