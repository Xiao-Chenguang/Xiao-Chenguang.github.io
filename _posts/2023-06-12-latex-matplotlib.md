---
layout: post
title:  Latex compatible matplotlib figures
date:   2023-06-21
categories: skills
author: Chenguang Xiao
---

Inserting awsome figure produced by matplotlib into latex is a bit tricky considering the resolution, font size, and the size of the figure.
Formats as png and jpg are easy to be inserted into latex, but the resolution is not good enough for a paper, especially when you want to zoom in to see the details.

Scalable Vector Graphics (SVG) is a good choice for this purpose. Other formats like pdf, eps, and pgf are also capitable with latex.
However, large SVG files takes a lot of space and time to compile if your are using overleaf.
If you use svg with latex locally, you need to convert it to pdf first, which requires InkScape or other software.

It seems pgf is the best choice for latex. Here is a simple example to show how to use pgf with latex.

```python
import numpy as np
import matplotlib.pyplot as plt

# set commonly used font
plt.rcParams['font.family'] = 'serif'
plt.rcParams['font.serif'] = ['Times New Roman']

# convert Tex pt to matplotlib inch
fig_size_pt = 390, 390*0.6
fig_size_inches = fig_size_pt[0]/72.27, fig_size_pt[1]/72.27

fig, ax = plt.subplots(figsize=fig_size_inches)
# plot figure
fig.set_facecolor("0.8")
x = np.linspace(0, 200, 1000)
y = np.sin(0.6*x)*np.cos(0.01*x)
ax.plot(x, y)
ax.set_title('Figure title with latex: $y=sin(x)\sqrt{x}$')
ax.set_xlabel('x axis: $x_i$')
ax.set_ylabel('y axis: $y_i$')

# set padding to 0
fig.tight_layout(pad=0)

# save figure with pgf backend
plt.savefig('figure.pgf', backend='pgf')
```

You may still confront some problems when using pgf with latex, for example, you are required to upload the tex file to publish your paper and extra package may cause compilation error.
In this case, you can use pdf as the figure format.
Just change the last line of the code above to

```python
plt.savefig('figure.pdf', backend='pgf')
```