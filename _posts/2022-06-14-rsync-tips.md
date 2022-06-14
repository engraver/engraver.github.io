---
layout: post
title:  "rsync tips"
---

## Copy remote folders with content recursively
The following command copies the content of `~/path/to/` in the remote server to the current folder `.`:
```
$ rsync -Pra user@remote-server:~/path/to/* .
```

## Selective sync
Copying files with `*.vtu` extension only:
```
$ rsync -Pra --include="*/" --include="*.vtu" --exclude="*"  user@remote-server:~/path/to/* .
```
