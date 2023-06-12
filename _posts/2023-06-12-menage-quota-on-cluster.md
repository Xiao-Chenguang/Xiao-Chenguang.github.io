---
layout: post
title:  "Manage your quota on computer cluster"
date:   2023-06-12
categories: skills
author: Chenguang Xiao
---

When you are using a computer cluster, you are usually given a quota of disk space as home directory.
This home directory allows you to store necessary script files that customize your working environment, for example, `.bashrc`, `.vimrc`, `.tmux.conf`, etc.
With this target, the quota of your home directory is usually not large, e.g., 10GB.
This is a fair small space when you put your project data in it or faild to manage your files.

In this post, I will introduce some useful commands to help you manage your quota on computer cluster.
This is done in two steps: 
- set up a soft link from your project storage to your home directory;
- clean up your home directory.

## Set up a soft link from your project storage to your home directory
The first step is to set up a soft link from your project storage to your home directory.
This make you access your project storage from your home directory painlessly while keep your home directory clean.
As the data you put in your project storage can be accessed from your home directory but not take up the space of your home directory.
For example, if you have a project storage `/cluster/project/` and your home directory is `/cluster/user_name/home/`, you can set up a soft link from `/cluster/project/` to `/cluster/user_name/home/project/` by
```bash
ln -s /cluster/project/ /cluster/user_name/home/project/
```
Then you can access your project storage by `cd ~/project/` from your home directory.

## Clean up your home directory if necessary
The second step is to clean up your home directory.
Even you already set up proper soft links to store large files to project storage, you may still run out of your quota gradually.
This is because you may have some temporary files or large files that you do not need any more.
You may find the `.cache` directory in your home directory takes up a 5GB space as lots of applications store their temporary files in it.
By running `ls ~/.cache/`, you can see results like
```bash
total 10K
drwxr-xr-x. 3 user_name users 4.0K Nov 11  2022 matplotlib
drwxr-xr-x. 5 user_name users 4.0K May 24 11:38 pip
drwxr-xr-x. 2 user_name users 4.0K Jan 14 15:45 seaborn
drwxr-xr-x. 3 user_name users 4.0K Aug 10  2022 torch
```
Obvirously, pip, matplotlib, seaborn, torch, typescript, and yarn pleace their temporary files in `.cache`.

Further more, you can use `du -sh *` to see the size of each directory in your home directory, ans sort the results by `sort -h` from samller folder to larger with help of pipleline `|`.
As we want to see the usage of .cache fordler, we can run
```bash
cd ~/.cache
du -sh $(ls -A) | sort -h
```
The results are like
```bash
131K    matplotlib
257K    seaborn
188M    torch
5.2G    pip
```

Obvirously, the pip folder takes up a large space.
You may want to clean up the pip folder with `rm -rf ~/.cache/pip/*` or just use `pip cache purge` to clean up the pip cache.

Similarly, you can use `du -sh $(ls -A) | sort -h` to see the size of all folders in your home directory and clean up the large folders that you do not need any more.

## Technique details:
- `ln -s`: `-s` for soft link, which is a symbolic link to a file or directory.
- `du`: short for **d**isk **u**sage, is a standard Unix/Linux command used to check the information of disk usage of files and directories on a machine.
- `du -sh`: `-s` for summary, which will only show the total size of a directory and all its subdirectories; `-h` for human readable, which will print sizes in human readable format(e.g., 1K 234M 2G).
- `ls -A`: `-A` for all files and directories except `.` and `..`.
- `sort -h`: `-h` for sort by human readable numbers corresponding to the `-h` option of `du`.