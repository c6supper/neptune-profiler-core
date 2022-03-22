Neptune-Profiler-Core
===========

Light weight profiler framework core for hypervisor based embedded system 

Prerequisites
-----------------

> * I highly recommended to use docker as building host, you could follow [Jupiter](https://github.com/c6supper/Jupiter.git)
> * gRPC
>> * gRPC isn't aim to automotive system , many problems have been met when cross compiling to aarch64 QNX from X86_64 linux host. I have forked [gRPC](https://github.com/c6supper/grpc/tree/v1.33.2_qnx) and  [abseil-cpp](https://github.com/c6supper/abseil-cpp/tree/lts_2020_02_25_qnx)(it's submodule for gRPC) which have fixed the building issues, please refer to the branch labeled as "qnx"

>> * [gRPC X86 Compiling Configuration Example] 
  ```bash
  cmake -DgRPC_BUILD_CODEGEN=ON -DgRPC_BUILD_GRPC_CPP_PLUGIN=ON \
	-DgRPC_BUILD_GRPC_CSHARP_PLUGIN=OFF -DgRPC_BUILD_GRPC_NODE_PLUGIN=OFF \
	-DgRPC_BUILD_GRPC_OBJECTIVE_C_PLUGIN=OFF -DgRPC_BUILD_GRPC_PHP_PLUGIN=OFF \
	-DgRPC_BUILD_GRPC_PYTHON_PLUGIN=OFF -DBENCHMARK_ENABLE_TESTING=off -DgRPC_BUILD_GRPC_RUBY_PLUGIN=OFF \
	-DgRPC_BUILD_CSHARP_EXT=OFF  -DgRPC_BUILD_TESTS=OFF ../.. && make -j64
  ```

>> * [gRPC Cross Compiling Configuration Example] 
  ```bash
  cmake -D_gRPC_PLATFORM_QNX=1 -DCMAKE_CROSSCOMPILING=1 -DgRPC_BUILD_CODEGEN=ON -DgRPC_BUILD_GRPC_CPP_PLUGIN=ON \
	-DgRPC_BUILD_GRPC_CSHARP_PLUGIN=OFF -DgRPC_BUILD_GRPC_NODE_PLUGIN=OFF \
	-DgRPC_BUILD_GRPC_OBJECTIVE_C_PLUGIN=OFF -DgRPC_BUILD_GRPC_PHP_PLUGIN=OFF \
	-DgRPC_BUILD_GRPC_PYTHON_PLUGIN=OFF -DgRPC_BUILD_GRPC_RUBY_PLUGIN=OFF \
	-DgRPC_BUILD_CSHARP_EXT=OFF  -DgRPC_BUILD_TESTS=ON -DgRPC_PROTOBUF_PROVIDER=module \
	-DgRPC_SSL_PROVIDER=package -DBENCHMARK_ENABLE_TESTING=off -DgRPC_ZLIB_PROVIDER=package \
	-DZLIB_LIBRARY=$QNX_TARGET/aarch64le/usr/lib/libz.a \
	-DOPENSSL_CRYPTO_LIBRARY=$QNX_TARGET/aarch64le/usr/lib/libcrypto.a \
	-DOPENSSL_SSL_LIBRARY=$QNX_TARGET/aarch64le/usr/lib/libssl.a -DCMAKE_BUILD_TYPE=Release \
	-DZLIB_INCLUDE_DIR=$QNX_TARGET/usr/include \
	-DOPENSSL_INCLUDE_DIR=$QNX_TARGET/usr/include/openssl \
	-DCMAKE_TOOLCHAIN_FILE=$QNX_ROOT/cmake/QNXToolchain.cmake -DCMAKE_INSTALL_PREFIX=$QNX_TARGET/aarch64le/usr/ ../.. && \
find . -name "link.txt" -exec sed -i "s/-lrt//g" {} +;find . -name "link.txt" -exec sed -i "s/-lpthread//g" {} + && make -j64 && make install
  ```
>> * [gRPC example Cross Compiling Configuration Example] 
  ```bash
  cmake -DCMAKE_TOOLCHAIN_FILE=$QNX_ROOT/cmake/QNXToolchain.cmake \
	-DProtobuf_DIR=$QNX_TARGET/aarch64le/usr/lib/cmake/protobuf \
	-DgRPC_DIR=$QNX_TARGET/aarch64le/usr/lib/cmake/grpc \
	-DZLIB_LIBRARY=$QNX_TARGET/aarch64le/usr/lib/libz.a \
	-DOPENSSL_CRYPTO_LIBRARY=$QNX_TARGET/aarch64le/usr/lib/libcrypto.a \
	-DOPENSSL_SSL_LIBRARY=$QNX_TARGET/aarch64le/usr/lib/libssl.a \
	../;find . -name "link.txt" -exec sed -i "s/-lrt//g" {} +;find . -name "link.txt" -exec sed -i "s/-lpthread//g" {} + && make -j64
  ```
> * Installation
>> * Install golang , protoc-gen-doc
>> * Install protoc, grpc_cpp_plugin, build and install from source(version should be align with cross compiled one)
>> * Install [protolint](https://github.com/yoheimuta/protolint/releases)
> * git submodule update --init 

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

