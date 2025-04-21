---
title: Build and Run
layout: default
has_children: false
nav_order: 2
---

# Usage

## Build

```bash
mkdir build
cd build
export CC=clang
export CXX=clang++
cmake -DCMAKE_BUILD_TYPE=Release ..
make
```

You can also use multi-core compilation for better performance:

```bash
make -j$(nproc)
```

## Run

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable fluxsand.service
sudo systemctl start fluxsand.service
```

You can check the service status or view logs using:

```bash
systemctl status fluxsand.service
journalctl -u fluxsand.service -f
```

## Union Test

```bash
mkdir build
cd build
export CC=clang
export CXX=clang++
cmake -DCMAKE_BUILD_TYPE=Release -DTEST=True ..
make
```
