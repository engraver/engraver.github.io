---
layout: post
title:  "Module not found in Fedora"
tags: linux fedora
---

In case if Fedora cannot recognize `ml` or `module load` command
```bash
$ ml av
bash: ml: command not found
```

run

```bash
source /etc/profile.d/modules.sh
```
