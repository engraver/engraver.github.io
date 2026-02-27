---
layout: post
title:  "Adjusting inline tikz macro to baseline"
tags: latex, tikz
---

Here, we use `\raisebox` to shift tikz node a bit down:
```latex
my equation: \raisebox{-12pt}{\tikz \node [draw=red, fill=orange!20!white, ultra thick] {$\dfrac{\partial\vec{M}}{\partial t} = -\gamma \vec{M}\times \vec{H}$};}
```

![](/assets/blg/figs-latex/20260227-001.png)