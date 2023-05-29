---
layout: post
title:  "Use python argparse in Jupyter Notebook"
date:   2023-05-29
categories: skills
author: Chenguang Xiao
---

Python built-in module [argparse](https://docs.python.org/3/library/argparse.html) is a very useful tool to parse command line arguments.
In prodcution, we usually run python scripts in command line.
When import a package contain argparse in Jupyter Notebook, it will raise an error.

For example we get a python script `test.py` with argparse:

```python
import argparse

def get_args():
    parser = argparse.ArgumentParser()
    parser.add_argument('--test', type=int, default=0)
    args = parser.parse_args()
    return args

if __name__ == '__main__':
    args = get_args()
    print(args.test)
```

there is no problem to run it in command line:

```bash
python test.py --test 1
```

However, if we import it in Jupyter Notebook, it will raise an error:

```jupyter
from test import get_args
args = get_args()
```
You will get a empty `Namespace` object for args variable rather than args.test=0.

This can be useful when we want to test or debug our code in Jupyter Notebook.
Here is a simple solution to solve this problem.

```jupyter
# add following code before calling argparse
import sys
sys.argv = ['']

# run your code
from test import get_args
args = get_args()
```

Now you can use argparse in Jupyter Notebook normally as in comdline line to get the default value of your configuration.
