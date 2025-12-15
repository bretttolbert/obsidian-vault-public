# make

###### Simple single C file Makefile
```make
CFLAGS=-O3 -std=c++0x -pg -D_DEBUG -g -Wall
all:
    g++ $(CFLAGS) sbox.cpp -o sbox

```
