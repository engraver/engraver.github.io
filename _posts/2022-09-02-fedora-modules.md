---
layout: post
title:  "Module not found in Fedora"
---

In case if Fedora cannot recognize `ml` or `module load` command
```
$ ml av
bash: ml: command not found
```

run

```
source /etc/profile.d/modules.sh
```
