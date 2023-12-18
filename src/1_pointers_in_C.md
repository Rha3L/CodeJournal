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
  printf("%d\n", p+1); // p + 1 is 2006
}
```

## Pointer Types

### call by value

```
#include <stdio.h>
void Increment(int p)
{
  p = p + 1;
}
int main()
{
  int a = 10;
  Increment(a);
  printf("a = %d\n", a);
}
```

- Passed in copy value of a
- p and a have same value but different memonry addresses
- local variable will not be called or used outside the function
- In memory stack, increment function stack will pop out once the function is executed. That's why main function cannot access the local variable in Increment function
- the inrement function will not change the value of a
- printing result is 10

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
  printf("a = %d\n", a);
}
```

- Passed in the address of a
- the inrement function will change the value of a
- printing result is 11
