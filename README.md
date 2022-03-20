Neptune-Profiler-Proto
===========

Light weight profiler framework core for hypervisor based embedded system 

Prerequisites
-----------------

> * Install golang
> * Install protoc
> * Install protoc-gen-doc
> * Install [protolint](https://github.com/yoheimuta/protolint/releases)
> * git submodule init && git submodule update

How to Build
-----------------

> * mkdir build && cd build
> * cmake -DCMAKE_PREFIX_PATH=={where your grpc installed(build from source)} ../
> * make install

Documentation
-----------------

Read the API Docs [here](neptune-profiler-proto/doc/neptune-profiler-proto-doc.md)

Inspiration
-----------------

The structure for the project is inspired by [Gauge](https://github.com/getgauge/gauge) from ThoughtWorks

License
-------

Neptune-Profiler-Proto is released under the Apache License, Version 2.0. See [LICENSE](LICENSE) for the full license text.

Copyright
---------

Copyright 2022 Coding Nerd

