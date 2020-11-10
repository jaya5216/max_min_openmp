# max_min_openmp
#include<stdio.h>
#include<omp.h>
#include<iostream>
//int a,b,c;
int min(int a,int b,int c)
{
if (a > b)
{
if (c > b) return b;
else return c;
}
else
{
if (c > a) return a;
else return c;
}
}
int max(int a,int b,int c)
{
if (a > b)
{
if (a > c) return a;
else return c;
}
else
{
if (b > c) return b;
else return c;
}
}
int main()
{
int a = 6, b = 10, c = 3;
#pragma omp parallel num_threads(2) default(none) shared(a,b,c)
{
int threadId = omp_get_thread_num();
if(threadId==0)
{
printf("The maximum value of %d, %d, %d is %d\n", a, b, c, max(a, b, c));
}
 else if(threadId==1)
{
printf("The maximum value of %d, %d, %d is %d\n", a, b, c, min(a, b, c));
}
}
return 0;
}
