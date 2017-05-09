Sample Exam: Solutions
----------------------

## Problem 1: MCQs

1)  b, d
2)  b
3)  b
4)  a
5)  d
6)  c
7)  a
8)  a
9)  b
10) b

## Problem 2

| Address (Before)  | Value (Before)  | Address (After) | Value (After) |
| -----------------:|:---------------:|:---------------:|:-------------:|
| 0x400b028         | 0x00000022      | 0x400b028       | **0x00000032**|
| 0x400b024         | 0x400b611c      | 0x400b024       | 0x400b611c    |
| 0x400b020         | 0x400b512c      | 0x400b020       | 0x400b512c    |
| 0x400b01c         | 0x00000d12      | 0x400b01c       | 0x00000d12    |
| 0x400b018         | 0x00000014      | 0x400b018       | 0x00000014    |
| 0x400b014         | 0x400b511c      | 0x400b014       | 0x400b511c    |
| 0x400b010         | 0x400b601c      | 0x400b010       | 0x400b601c    |
| 0x400b00c         | 0x00000022      | 0x400b00c       |  Anything     |
| 0x400b008         | 0x00000013      | 0x400b008       |  Anything     |
| 0x400b004         | 0x400b601c      | 0x400b004       | 0x400b601c    |
| 0x400b000         | 0x400b511c      | 0x400b000       | 0x400b511c    |
| 0x400affc         | 0x00000013      | 0x400affc       | **0x00000032**|
| 0x400aff8         | 0x0000001B      | 0x400aff8       | 0x0000001B    |
| 0x400aff4         | 0x400b601c      | 0x400aff4       | 0x400b601c    |
| 0x400aff0         | 0x00000014      | 0x400aff0       | 0x00000014    |
| 0x400afec         | 0x0a0bc11d      | 0x400afec       | 0x0a0bc11d    |
| 0x400afe8         | 0x400b511d      | 0x400afe8       | 0x400b511d    |
| 0x400afe4         | 0x0000001B      | 0x400afe4       | 0x0000001B    |

## Problem 3

A) The linker will generate an error because the strong symbol `main` is defined twice.

B) Output: x = 10

## Problem 4

A) The code is not cache friendly. Because i is incremented in the inner loop, every successive access into the array is stride-n. We can make it cache-friendly by switching the loops:

```
int fun_1()
{
  int B[N][N];

  int i, j;

  for (i = 0 ; i < N ; i++)
    for (j = 0 ; j < N ; j++)
      B[i][j] = 2 * (B[i][j] + 2);
}
```

B) Going over the same array twice is not cache-friendly as we make no advantage of temporal locality. We can rewrite the function by using a single loop:

```
grade compute_average(grade* g, int n)
{
  float exam1_average = 0;
  float exam2_average = 0;
  int i;

  for (int i = 0 ; i < n ; i++)
  {
    exam1_average += g[i].exam1;
    exam2_average += g[i].exam2; 
  }

  grade average = { exam1_average / n, exam2_average / n};
  return average;
}
```

## Problem 5

A) The actual struct in memory will look like:

```
struct node {
  char c;              /* 1 byte  */
  char pad1[7];        /* 7 bytes */
  long value;          /* 8 bytes */
  struct node* next;   /* 8 bytes */
  int flag;            /* 4 bytes */
  char pad2[4];        /* 4 bytes */
  struct node* left;   /* 8 bytes */
  struct node* right;  /* 8 bytes */
} node;
```

B) The blanks are:
* test1() --> `movl 0x18(%rax), %eax`
* test2() --> 
```
	movq 0x10(%rax), %rax
	movq 0x8(%rax), %rax
```

## Problem 6

This problem was discussed in recitation10 so you can refer to the solutions for that.

## Problem 7

A) The output is the numbers: 0 1 2 1 2 2 2 (each on a separate line). A different ordering is also possible due to non-deterministic scheduling.

B) A total of 7 processes are created by fork(). This does not count `main` itself.

C) This is because `main` does not wait for the threads to finish. We can fix this by adding a join:

```
void main() { 
  pthread_t th[3];
  int i;
  for (i = 0; i < 3; i++) {
    pthread_create(&th[i], NULL, print_number, &i);
  }

  for (i = 0; i < 3; i++) {
    pthread_join(th[i], NULL);
  }

  exit(0); 
}
```

The output appears but is non-deterministic (i.e. changes every time) since we do not use synchronization. We are not required to do that.

D) There is only 1 process here since we create none.

E) `main` creates 3 threads.
 
