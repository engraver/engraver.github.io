---
layout: post
title:  "rsync tips"
tags:   linux
---

## Copy remote folders with content recursively
The following command copies the content of `~/path/to/` in the remote server to the current folder `.`:
```bash
$ rsync -Pra user@remote-server:~/path/to/* .
```

## Selective sync
Copying files with `*.vtu` extension only:
```bash
$ rsync -Pra --include="*/" --include="*.vtu" --exclude="*"  user@remote-server:~/path/to/* .
```
