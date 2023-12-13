---
layout: post
title:  "Templates for plotnine"
tags: python plotting svg
---

Python package [`plotnine`](https://plotnine.readthedocs.io/) presents a ggplot2-based realization of the "Grammar of Graphics" with `matplotlib` background. Actively using LaTeX package [`pgfplots`](https://pgfplots.net/) for plottings, I found `plotnine` useful to do make drawings directly in Python with a reasonable convenience of previewing in Jupyter notebooks and exporting into png/svg (for further assembly in Inkscape).

## Resources
- [https://r-graphics.org/](https://r-graphics.org/)

## Preamble
Typical preamble
```python
import meshio
import pandas as pd
import numpy as np
import plotnine as p9

from glob import glob
from os.path import join as pjoin
from matplotlib import rc
rc('text', usetex=True) # use tex fonts in labels
```

Note that the LaTeX texts are exported as paths to svg. Thus, they are not editable as text and do not require font embedding, which could be as positive aspect as well as a drawback.

## Plotting a few lines in the same axes
Say, we have two datasets saved in files `result_size_24.dat` and `result_size_58.dat` which are different by size of the sample analyzed. The first step is to create a joint dataset, where the column `size` will be used to distinguish the initial datasets:
```python
df1 = pd.read_csv('result_size_24.dat', sep=' ')
df1['size'] = 24.
df2 = pd.read_csv('result_size_58.dat', sep=' ')
df2['size'] = 58.

# $ cat result_size_24.dat 
# time magnetization
# 0.000000000000000000e+00 2.210569005689148714e+00
# 1.212121212121212155e+00 2.247376865418724279e+00
# 2.424242424242424310e+00 2.211233780883315791e+00
# 3.636363636363636687e+00 2.257762135137621584e+00
# ...

df = pd.concat((df1, df2))
```
Other useful options for `read_csv` are `header=None` and `skiprows=1`.

By default, labels for axes and legends are taken from the dataset column captions. While axes labels can be easily changed, this is not true for legends (at least, if you want to keep automatic selection of symbols and colors instead of manual assignment of them). Thus, a reasonable way is to add a few new columns into the dataset `df`, which will be properly labeled. Say, dataset contains columns `time`  and `magnetization` we want to plot:
```python
xaxis = r'\rmfamily Time (min)'
yaxis = r'\rmfamily Magnetization $M$ (emu/g)'
groupby = r'\rmfamily Sample size (nm)'

df[xaxis] = df['time']
df[yaxis] = df['magnetization']
df[groupby] = df['size'].transform(str)
```
Two important points here:

- LaTeX font selection `\rmfamily` is used to override the default `\sffamily` font just because I like it more.
- Since `size` is numerical (for purpose in this example), we need to convert it to the text with `transform` method. Of course, one can use own functions as well as lambda expressions here.

The simplest plot is generated as
```python
fig = p9.ggplot(df, p9.aes(x=xaxis, y=yaxis, shape=groupby, color=groupby)) + \
    p9.geom_point(size=3) + p9.geom_line()
fig.draw()
```
Here, shape of symbols and color of symbols/lines is determined by the `groupby` column.

![](/assets/blg/figs-p9/plt1.png)





















