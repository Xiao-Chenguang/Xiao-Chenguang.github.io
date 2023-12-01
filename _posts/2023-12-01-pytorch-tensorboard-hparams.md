---
layout: post
title: torch version tensorboard hparams
date:   2023-12-01
categories: skills
author: Chenguang Xiao
---

Tensorboard is a great tool for machine leanring process visualization.
The key component of tensorboard is the `SummaryWriter` class.
The writer has methods include add_scalars, add_histogram, add_image, add_embedding, add_pr_curve, add_audio, add_text, add_video, add_mesh, and add_hparams.
![add_hparams](/_posts/figs/tb-hist.png)

The most popular method is `add_scalars`, which can be used to plot loss and accuracy curves. As well as the `add_histogram` shown above.
After that, `add_hparams` is handy for hyperparameter tuning. In this post, I will show how to use tensorboard hparams to tune hyperparameters.

```python
import numpy as np
from torch.utils.tensorboard import SummaryWriter

lod_dir = 'name_of_run'
epoch = 10
metrics = 'acc'

# instantiate summary writer, default directory is runs/
writer = SummaryWriter(log_dir=lod_dir)

# log the hyperparameters with metric to be compared
writer.add_hparams({'lr': 0.1}, {'acc': 0})

# log the metrics during training
for e in range(epoch):
    writer.add_scalar('acc', np.sin(e/3), e)
```
This will results in the following tensorboard hparams.
![add_hparam](/_posts/figs/tb-hparam.png)

However, the torch build-in tensorboard hparams is not very user-friendly for two reasons.
1. The hparams are loged into same file as other scalars in the same run.
2. The hparams only log the metric once rather than during whole training process.

Thus, before running the code, make sure you made some modifications to the `env_path/lib/python3.10/site-packages/torch/utils/tensorboard/writer.py` file by commenting out the following lines. 
```python
        # if not run_name:
        #     run_name = str(time.time())
        # logdir = os.path.join(self._get_file_writer().get_logdir(), run_name)
        # with SummaryWriter(log_dir=logdir) as w_hp:
        #     w_hp.file_writer.add_summary(exp)
        #     w_hp.file_writer.add_summary(ssi)
        #     w_hp.file_writer.add_summary(sei)
        #     for k, v in metric_dict.items():
        #         w_hp.add_scalar(k, v)
```
and add the following lines instead.
```python
        self.file_writer.add_summary(exp)
        self.file_writer.add_summary(ssi)
        self.file_writer.add_summary(sei)
```