# Dockerfiles
This project contains the files, to create docker container which compile and
execute my projects.

## compiler

A container with the last versions of GCC and clang. This container is the base
for all other.

## boost

A container with the develop branch of the C++ boost libraries. This container
is the base for my C++ projects.

Boost is configured to use C++14. If the compiler is clang, libc++ is used,
instead of libstdc++.

## mitrax

A container to checkout and compile my mitrax library and run the test suite.

The default compiler is clang.

## disposer

A container to checkout and compile my disposer library and its module suite.

The default compiler is clang.
