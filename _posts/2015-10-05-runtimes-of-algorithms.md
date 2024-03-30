---
category: Technical
date: 2015-10-05
layout: post
title: Runtimes Of Algorithms
updated: 2024-02-03
---

I was trying to compare different algorithms based on input size. I have implemented all these algorithms in C. Following table gives you how the order of growth is affecting practical implementation.
{: style="text-align: justify;"}

| N | Bubble Sort | Insertion Sort | Merge Sort | Selection Sort |
|--------|-------------|----------------|------------|----------------|
| 100 | 0 ms | 0 ms | 0 ms | 0 ms |
| 1000 | 0 ms | 0 ms | 0 ms | 0 ms |
| 10000 | 252 ms | 62 ms | 0 ms | 94 ms |
| 50000 | 6546 ms | 1563 ms | 16 ms | 2328 ms |
| 100000 | 26687 ms | 6266 ms | 47 ms | 9291 ms |

0 means it has taken very less or negligible time.
So it looks like Merge sort is clear winner. Followed by insertion sort, selection sort and finally Bubble sort.
Same thing I applied for Matrix Multiplication.
{: style="text-align: justify;"}

| N | Brute Force (n^3) | Strassen |
|-------|-------------------|------------------------------------------------------------------------------------|
| 128 | 16 ms | 1391 ms |
| 512 | 656 ms | 68078 ms |
| 1024 | 7297 ms | 474781 ms |
| 10000 | 3.64 hours | Did not stop even after 24 hours |
| | | (Actually even if it had stopped answer would be wrong as 10000 is not power of 2) |

As you can see it looks like Strassen is not yet all beating brute force in any way. Then I came across following points in [Wikipedia](https://en.wikipedia.org/wiki/Strassen_algorithm)
{: style="text-align: justify;"}

```
Practical implementations of Strassen’s algorithm switch to standard methods of matrix multiplication for small enough submatrices, for which those algorithms are more efficient. The particular crossover point for which Strassen’s algorithm is more efficient depends on the specific implementation and hardware. Earlier authors had estimated that Strassen’s algorithm is faster for matrices with widths from 32 to 128 for optimized implementations. However, it has been observed that this crossover point has been increasing in recent years, and a 2010 study found that even a single step of Strassen’s algorithm is often not beneficial on current architectures, compared to a highly optimized traditional multiplication, until matrix sizes exceed 1000 or more, and even for matrix sizes of several thousand the benefit is typically marginal at best (around 10% or less)
```

Similar things are discussed in some of the coding forums -> [Stackoverflow](http://stackoverflow.com/questions/13559928/why-is-my-strassens-matrix-multiplication-slow?rq=1)

So based on above comments, I changed implementation. I kept Crossover value as 32. That is if sub matrix size is 32×32 than Strassen’s algorithm instead of calling its own algorithm with smaller size, it will call Brute force algorithm to do the lower size matrix multiplication.
{: style="text-align: justify;"}

| N | Brute Force (n^3) | Strassen |
|------|-------------------|----------|
| 64 | 0 ms | 16 ms |
| 128 | 16 ms | 16 ms |
| 256 | 125 ms | 110 ms |
| 512 | 1078 ms | 937 ms |
| 1024 | 14468 ms | 6282 ms |  

Clearly Strassen is overtaking brute force. Now I tried with crossover value as 16. Again Strassen was very close to Brute force but could not beat it. For value 128, Strassen was able to beat Brute force only after N size of 512.
{: style="text-align: justify;"}

In my case Strassen algorithm takes 2-3 times more memory than Brute Force like for n = 1024 i.e. 1024*1024 matrix brute force took 21 MB where as Strassens algorithm took 48 MB.*
{: style="text-align: justify;"}