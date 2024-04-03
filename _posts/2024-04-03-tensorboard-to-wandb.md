---
layout: post
title: upload tensorboard events to wandb
date:   2024-04-03
categories: skills, ml
author: Chenguang Xiao
---
For some reason you want to transfer from tensorboard to wandb, then you will suffer from this problem where there are already some tensorboard runs with configs to be uploaded to wandb.

There are some official tutorial in wandb related about this

1. [wandb developer guide](https://docs.wandb.ai/guides/integrations/tensorboard#syncing-previous-tensorboard-runs)
2. [wandb api](https://docs.wandb.ai/ref/python/public-api/api#sync_tensorboard)

They corresponding to two ways to sync tensorboard enents to wandb:

* CLI
* Python api

There we use the wandb python api to solve it.

## Demo

```python-repl
from glob import glob

import yaml

import wandb

# root path include multiple runs folders
root = "root/to/runs/"
project = "your-project-name"
entity = "your-wandb-entity"

# all subfolders (runs)
fds = glob(root + "*")

# wandb session
api = wandb.Api()


for fd in fds:
    # define run is same as folder name
    name = fd.split("/")[-1]

    # get tensorboard and config file path
    tb_path = glob(fd + "/events.out.tfevents.*")[0]
    cf_path = glob(fd + "/config.yaml")[0]

    # sync tensorboard to wandb
    run = api.sync_tensorboard(
        root_dir=tb_path,
        run_id=name,
        project=project,
        entity=entity,
    )

    # update config to wandb
    with open(cf_path) as f:
        config = yaml.load(f, Loader=yaml.FullLoader)
    run.config = config
    run.update()

```


The key is use of two Api `api.sync_tensorboard`( ) and `run.update()`.

### Notice

1. use events file path instead of the parent folder in `api.sync_tensorboard`, ensure the wandb group runs correctly.
2. make sure to run `run.update()` after setting the configs of the run.
