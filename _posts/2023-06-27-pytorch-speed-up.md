---
layout: post
title:  Configure PyTorch to speed up training
date:   2023-06-21
categories: skills
author: Chenguang Xiao
---

Contents:
- dataloader (num_workers)


## Dataloader (num_workers)

### Number of workers (multiprocessing)

grid search for the best number of workers for the train and test dataloader.
For example, using workers from 0 to 32, measure the time for each number of workers.
```python
import time
for num_workers in [0, 1, 2, 4, 8, 16, 32]:
    start = time.time()
    train_loader = torch.utils.data.DataLoader(
        train_dataset, batch_size=batch_size, shuffle=True, num_workers=num_workers)
    end = time.time()
    print('num_workers: {}, time: {:.4f}'.format(num_workers, end-start))
```