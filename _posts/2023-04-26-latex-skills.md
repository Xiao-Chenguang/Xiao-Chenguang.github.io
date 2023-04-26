---
layout: post
title:  "Change the fonts in matplotlib figures"
date:   2023-04-26
categories: skills
author: Chenguang Xiao
---

It's common to use Times New Roman font in academic papers, but the default font in matplotlib is not Times New Roman.
Here I will show you how to change the font in matplotlib figures.

## Set font family in matplotlib

If you have installed Times New Roman font in your system, you can set the font family in matplotlib by the following code temperately before plotting your figures:

```python
plt.rcParams['font.family'] = 'Times New Roman'
```

## Use Times New Roman similar font family "Serif"
There are cases that you can't install Times New Roman font in your system or just don't want to install it.
In such case, how to use Times New Roman similar font family "Serif" in matplotlib?

There are simply two ways to do it.

### Method 1: Use font family "Serif" directly

```python
plt.rcParams['font.family'] = 'serif'
```

Whatever font family you set, matplotlib will use the default its serif font family, which is Times New Roman similar font family "Serif".
There are indead some differences between Times New Roman and "Serif", only when you look at them carefully.

### Method 2: Use Times New Roman without installing it

It is possible to use Times New Roman without installing it in your system.
matplotlib provides a font manager to load fonts from files.

First, download the Times New Roman font file from [here](https://freefontsfamily.com/times-new-roman-font-free/).
Then, put the font file in the same directory as your python script.
Finally, use the following code to load the font file:

```python
import matplotlib.font_manager as font_manager
from matplotlib import rcParams

font_path = 'path_to_your_font_folder'
for font in font_manager.findSystemFonts(fontpaths=font_path):
    font_manager.fontManager.addfont(font)
```

Now, you can use Times New Roman font family in matplotlib by the following code:

```python
plt.rcParams['font.family'] = 'Times New Roman'
```
