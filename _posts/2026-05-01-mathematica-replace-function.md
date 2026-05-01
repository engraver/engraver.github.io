---
layout: post
title:  "Replace function with it's derivatives"
tags: wolfram mathematica
math: true
---

A common “issue” of a theoretician performing symbolic calculations in Wolfram Mathematica is the replacement of the function together with its derivatives in a certain functional. Say we have an energy density of a 1D magnetic texture in a uniaxial ferromagnet

$$
w = \ell^2 \theta'(x)^2 + \sin^2 \theta(x),
$$

where \\\(\ell\\\) is the magnetic length and \\\(\theta(x)\\\) is the polar angle of the magnetization vector. 

To get the energy for the specific magnetic texture like a domain wall \\\(\cos\theta = \tanh (x/\ell)\\\), the most straightforward (and inconvenient!) way is to perform all replacements manually:

```
dw[x_] := 2 ArcTan[Exp[-x/ell]]
w /. {\[Theta][x] -> dw[x], \[Theta]'[x] -> 
    D[dw[x], x]} // FullSimplify
```

Less automatic stuff in coding means more headache and more possibilities to make a mistake. A better way is to make a replacement by a pure function:

```
dw[x_] := 2 ArcTan[Exp[-x/ell]]
w /. \[Theta] -> (dw[#] &) // FullSimplify
```

Both approaches give \\\(w = 2\sech^2 (x/\ell) \\\), but the second one has less room for mistakes.
