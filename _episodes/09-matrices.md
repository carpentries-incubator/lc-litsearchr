---
title: "Matrices"
teaching: 0
exercises: 0
questions:
- "What are matrices in R?"
objectives:
- "Successfully use matrices in R"
keypoints:
- "Matrices behave as two-dimensional vectors"
---



# Matrices
Matrices behave as two-dimensional vectors. They are faster to access and index than data frames, but less flexible in that every value in a matrix must be of the same data type (integer, numeric, character, etc.). If one is changed, implicit conversion to the next data type that could contain all values is performed.

~~~
rowMeans(mat)

## [1] 46 47 48 49 50 51 52 53 54 55

colMeans(mat)

## [1] 5.5 15.5 25.5 35.5 45.5 55.5 65.5 75.5 85.5 95.5
~~~
{: .language-r}

Matrices are indexed by row, then column. Indexes can include numeric sequences or TRUE/FALSE values.

~~~
mat[1:3, 1:3]

##    [,1] [,2] [,3]
## [1,]   1   11    21
## [2,]   2   12    22
## [3,}   3   13    23
~~~
{: .language-r}
