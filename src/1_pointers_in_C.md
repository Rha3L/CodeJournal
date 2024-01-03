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
  int size = sizeof(A)/sizeof(A[0]); // size is 8
  for (i = 0; i < size; i++)
  {
    sum += A[i];
  }
  return sum;
}
int main()
{
  int A[] = {1,2,3,4,5};
  int size = sizeof(A)/sizeof(A[0]); //size is 20
  int total = SumOfElements(A,size);
  printf("Sum of elements = %d\n",total);
}
```

- Pointer of array A is passed to the SumOfElements function, not the whole array
- Array as function arguments is using call by reference
- The changes made to the array in the function will change the value of the array and be reflected in the main function.
- Size of array has to be calculated in main function and passed to the SumOfElements function
- Both name of array A `SumOfElements(A, size)`and the pointer to the first element `SumOfElements(&A[0], size)` can be passed to SumOfElements function. If the pointer to the first element was used, it can be treated as pointer variable that can perform pointer arithmetic and dereferencing. It cannot be done if array name was passed in.

### Character Arrays (Strings) and Pointers

1. How to store strings

   size of array >= no. of characters in string + 1

   1 is used to store the ending of the string - NULL character ('/0')

2. Character arrays and pointers are different types that are used in similar manner

   Pointers to character arrays can be used to manipulate value of character or traverse through the array

3. Character arrays are always passed to functions by reference

### Pointers & 2D arrays

Pointer to 2D arrays:

```
int A[i][j]; //i number of one dimentional array of size j
int (*p)[j] = A;
A[0] //1-D array of j number of integers (size of 4 bytes * j)
For 2-D arrays:
A[i][j] = *(A[i]+j) //A[i] == int* (integer pointer)
        = *(*(A+i)+j)
```

Examples:

```
int A[2][3];

Pointer to 1-D array of size 3:
print A or &A[0] // address of starting point of first one-dimentional array
print A+1 or &A[1] // move to the next one-dimentional array

Pointer to integer:
print *A or A[0] or &A[0][0] // pointer to the first integer of A[0]
print *(A+1) or A[1] or &A[1][0]
print *(A+1) + 2 or A[1]+2 or &A[1][2]

print *(*A + 1) or A[0][1] // value of A[0][1]
```

The type of pointers matters when dereferencing and performing pointer arithmetic

### Pointers & multidemensional arrays

```
int A[i][j][k]
A collection of i number of j dimentional arrays of size k
int(*p)[j][k] = A;
A[i][j][k] = *(A[i][j]+k) = *(*(A[i]+j)+k)= *(*(*(C+i)+j)+k)
```

Examples:

```
int A[3][2][2]; //A collection of 3 2-dimensional arrays of size 2
int (*P)[2][2] = A;
print A; // int (*)[2][2]
print *A OR A[0] or &A[0][0] // int (*)[2] pointer to one dimensional array of 2 integers
print *(A[0][1] + 1) or A[0][1][1] //int *(integer pointer) + 1 (move one integer size of 4 bytes)
print *(A[1]+1) or A[1][1] or &A[1][1][0] //int *[2](array pointer) + 1 (move to next one dimentional array of 2 integers)
```

Passing multiple arrays as function arguments:

```
void Function(int *A) // 1-D array of integers
{
}
void Function(int *A[j] or A[][j]) // 2-D array of integers, size has to be specified
{
}
void Function(int *A[][j][k]) // 3-D array of integers
{
}
```

Size has to be specified and passed in different size of multidimensional arrays needs to change size j

## Pointers & Dynamic Memory

| Application's Memory | Storage                          | Note |
| -------------------- | -------------------------------- | ---- |
| Heap                 |                                  |      |
| Stack                | Function calls & local variables |      |
| Static/Global        | Global variables                 |      |
| Code(Text)           | Instructions                     |      |
