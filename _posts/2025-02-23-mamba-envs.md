---
layout: post
title:  "Setting mamba environments"
tags: linux development
---

== SLaSi, CPU version ==

Prerequisites:
```bash
mamba create --name "slasi-cpu" python=3.9 -y
mamba activate slasi-cpu
mamba install gcc gxx openmpi cmake cunit zlib backports.lzma sphinx -y
```

Preparing SLaSi libraries:
```bash
cd slasi-cpu/libsources
make python nlopt -j4
# optionally, one may remove unnecessary source folders here
cd ..
make -f Makefile.docs -j4
cd ..
```

```bash
mkdir slasi-build-cpu
cd slasi-build-cpu
cmake ../slasi -DPARALLEL=MPI && make -j4
```


== SLaSi, GPU version ==

Prerequisites:
```bash
mamba create --name "slasi-nv" python=3.9 -y
mamba activate slasi-nv
mamba install gcc gxx openmpi cmake cunit zlib backports.lzma sphinx -y
mamba install cuda-toolkit cuda-version=12
mamba install cuda-cudart cuda-version=12
#mamba install cuda-toolkit cuda-version=11 -y
#mamba install cuda-cudart cuda-version=11 -y
```

```bash
mkdir slasi-build-nv
cd slasi-build-nv
cmake ../slasi -DPARALLEL=CUDA && make -j4
ln -s ./slasi ./slasi-nv
```
