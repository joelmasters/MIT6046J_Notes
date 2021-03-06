# Convex Hull
The minimum area or volume that encloses all points of a shape

Given n points in a plane
  S = {(xi, yi) | i = 1, 2, ... n}
assume no two have the same x-coord, no two have the same y-coord, no three in a line,
Convex Hull is the smallest convex polygon containing all points in S, referred to as CH(S)

CH(s) is the sequence of points on the boundary in clockwise order as doubly-linked list

!['Convex Hull'](convexHull.PNG)

==> p <==> q <==> r <==> s <==> t <==> u <==
^==========================================^

## Brute Force
Draw a line between any two points. If all points line on only one side of the line, that edge is part of the convex hull.

Complexity: O(n^3)

## Divide and Conquer
Sort the points by x-coord (only needed once)
For input set S, divide into left half "A" and right half "B" by x-coordinates
Compute CH(A) and CH(B)
Combine

!['Convex Hull Split'](convexHull2.PNG)

Complexity: O(n^2), but we can do better

Start at point closest to middle boundary on left (a, largest x-coord) and on right (b, smallest x-coord) and comput y(i,j) (middle-line intercept point). Go clockwise on b and compute new y(i,j). If it is higher, move clockwise again on b until it gets lower. If it is lower, go counter-clockwise on a until a max and then another min is reached.

Complexity: O(nlogn)

Pseudocode:
```
i = 1;
j = 1;
while (y(i,j+1) > y(i,j) or (y(i+1,j) > (y,i,j)):
  if (y(i,j+1) > y(i,j):
    j = j+1 # move b clockwise
  else:
    i = i - 1 # move a counter-clockwise
 return (ai, bj) as upper tangent
```

To determine then the overall convex hull:
First link: ai -> bj (upper tangent), go around b until you see bm (lower tanget on b) and connect to ak (lower tangent on a) and continue around a until you reach ai.

