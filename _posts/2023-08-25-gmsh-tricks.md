---
layout: post
title:  "Gmsh tricks"
tags: gmsh simulations
---

The following tricks are tested for [Gmsh](http://gmsh.info/) version 4.10.5 and, probably, should work for other versions. Also, simpler ways for some tasks could be available. Also look for examples in the [official repository](https://gitlab.onelab.info/gmsh/gmsh/-/tree/master/examples).

## Work with arrays
The following command creates an array of size `N` and fills it with numbers from 1 to `N` inclusively. 

```
N = 10;
myArray = {1:N};

Printf("Array size %g", #myArray[]);
Printf("The first element: %g", myArray[0]);
Printf("The last element: %g", myArray[N-1]);
```

The syntax `#myArray[]` provides an access to the array size.

## For loop increments
The following `for` loop iterates from 0 to 9 with step 2:
```
For i In {0:9:2}
	Printf("i: %g", i);
EndFor
```
Note that the last value in the loop will be 8! Indication of step also works for definition of arrays.

## Access to the point coordinates
```
Point(10) = {314., 15., 926.};
Printf("%g %g %g", Point{10}); // prints 314 15 926
```
Access to the particular coordinate:
```
Point(10) = {314., 15., 926.};
g = Point{10};
Printf("%g", g[1]); // prints 15
```

## Add background image

```
General.BackgroundImageFileName = 'background.png';
General.BackgroundImagePositionX = 10;
General.BackgroundImagePositionY = 10;
General.BackgroundImageWidth = 1200;
General.BackgroundImageHeight = 900;
```