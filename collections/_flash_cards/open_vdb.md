---
title: OpenVDB
definition:
  Hierarchical data structure and a large suite of tools for the efficient
  storage and manipulation of sparse volumetric data.
tags: dynamic sparse volumetric data tree tile voxel grid
---

**V**olumetric,  
**D**ynamic grid that shares several characteristics with  
**B**+trees

### Characteristics

- Dynamic
- Memory efficient
- General topology
- Fast random and sequential data access
- Virtually infinite
- Efficient hierarchical algorithms
- Adaptive resolution
- Simplicity
- Configurable
- Out-of-core

## Buildings Blocks

- Direct access bit masks: provide fast and compact direct access to a binary
  representation of the topology
  - hierarchical topology encoding
  - fast sequential iterators
  - lossless compression
  - boolean operations
  - efficient implementations of algorithms
- Leaf nodes
  - keep the size of the LeafNodes relatively small for two reasons:
    - cache performance and
    - memory overhead from partially filled LeafNodes with few active voxels
- Internal nodes
- Root node
  - sparse and can be dynamically resized (via hash-map)
  - bottom-up vs. top-down tree traversals via `Accessors` due to spatially
    coherent grid access
  - `Accessor` are used to amortize the overhead of slow lookup into the
    `mRootTable` (hash-map) by means of reusing cached child nodes.

### When Manipulating data

When manipulating data in OpenVDB, the three essential objects are

1. the `Tree`, a B-tree-like three-dimensional data structure;
2. the `Transform`, which relates voxel indices (i, j, k) to physical locations
   (x, y, z) in World Space "world" space; and
3. the `Grid`, a container that associates a Tree with a Transform and
   additional metadata.

## Access Algorithms

- Random Access
- Sequential Access
- [Stencil Access](https://en.wikipedia.org/wiki/Stencil_code)

## Sources

- [Repo](https://github.com/AcademySoftwareFoundation/openvdb)
- [Overview](https://www.openvdb.org/documentation/doxygen/overview.html)
- [Cookbook](https://www.openvdb.org/documentation/doxygen/codeExamples.html)
- Original Paper:
  [VDB: High-Resolution Sparse Volumes with Dynamic Topology](http://www.museth.org/Ken/Publications_files/Museth_TOG13.pdf)
- Talk explaining VDB:
  [OpenVDB: An Open Source Data Structure and Toolkit for High-Resolution Volumes](https://youtu.be/7hUH92xwODg)
- VDB on GPU:
  [Fast Fluid Simulations with Sparse Volumes on the GPU](https://www.researchgate.net/publication/325488464_Fast_Fluid_Simulations_with_Sparse_Volumes_on_the_GPU)
- [Raytracing Sparse Volumes with NVIDIA® GVDB in DesignWorks](https://developer.nvidia.com/sites/default/files/akamai/designworks/docs/GVDB_TechnicalTalk_Siggraph2016.pdf)

## Compile openVDB to WASM (attempt, not working)

Source:
https://medium.com/@tdeniffel/pragmatic-compiling-from-c-to-webassembly-a-guide-a496cc5954b8

### [Boost](https://stackoverflow.com/a/51924884/3731530)

Check
[recommended version](https://www.openvdb.org/documentation/doxygen/dependencies.html#depDependencyTable).

```bash
# go to home folder
cd
wget http://downloads.sourceforge.net/project/boost/boost/1.61.0/boost_1_54_0.tar.gz
tar -zxvf boost_1_61_0.tar.gz
cd boost_1_61_0

./bootstrap.sh

# get the no of cpucores to make faster
cpuCores=`cat /proc/cpuinfo | grep "cpu cores" | uniq | awk '{print $NF}'`
echo "Available CPU cores: "$cpuCores
sudo ./b2 --with=all -j $cpuCores install
```

```
em++ openvdb.cc -s WASM=1 -o openvdb.js \
  -I $HOME/boost_1_61_0 \
  -I $HOME/openexr-2.2.0 \
  -I $HOME/ilmbase-2.2.0
```

## Build openVDB & run tests

### Install Blosc

- `git clone git@github.com:Blosc/c-blosc.git`
- `git co tags/v1.5.4`
- `cd c-blosc/`
- `mkdir build`
- `cd build/`
- `ccmake ..`
- `sudo cmake --build . --target install`

### Install other [dependencies](https://www.openvdb.org/documentation/doxygen/dependencies.html) via `apt-get`

e.g. `sudo apt-get install libboost-python-dev`

### Build ([standalone](https://www.openvdb.org/documentation/doxygen/build.html#buildBuildStandalone)) openVDP

- `mkdir build` in repo folder
- `cd buld/`
- `cmake ../ -DCMAKE_NO_SYSTEM_FROM_IMPORTED:BOOL=TRUE -DOPENVDB_BUILD_UNITTESTS=ON`

  - It is possible to set the install folder (e.g. `/usr/include` or
    `$HOME/openvdb`) by setting `-DCMAKE_INSTALL_PREFIX=/usr/include`
    - `cmake -DCMAKE_INSTALL_PREFIX=/usr/include ../
      -DCMAKE_NO_SYSTEM_FROM_IMPORTED:BOOL=TRUE -DOPENVDB_BUILD_UNITTESTS=ON```

- `-DCMAKE_NO_SYSTEM_FROM_IMPORTED:BOOL=TRUE` is need due to
  [error](https://github.com/AcademySoftwareFoundation/openvdb/issues/70#issuecomment-508984505):

  - /usr/include/c++/7/cstdlib:75:15: fatal error: stdlib.h: No such file or
    directory #include_next <stdlib.h>

- `make`
- `sudo make install`

#### Run Tests

Dependencies:

- `sudo apt-get install liblog4cplus-dev`
- `sudo apt-get install libcppunit-dev`
- `sudo apt-get install libjemalloc-dev`
- `sudo apt-get install libtbb-dev`

Running tests:

- Python & C++ tests: In `../openvdb/build/` run `make test` to run Python and
  C++ tests
- C++ tests only: Alternatively run tests via `./openvdb/unittest/vdb_test -v`
  for more details on the C++ tests
  - `Segmentation fault` happens and is mentioned in
    `tsc/meetings/2019-09-26.md` explaining it happens
    `during serialization of OpenVDB Point Data Grids into Houdini file formats`
- C++ custom test:
  1. Copy custom test file `TestTalus.cc` to `../unittest/TestTalus.cc`
  2. Add `TestTalus.cc` in `CMakeLists.txt`
  3. Run specific test with
     - `clear && make && ./openvdb/unittest/vdb_test -v -t TestTalus::InternalNode_testCoordToOffset`

Test log files can be found in `openvdb/build/Testing/Temporary`.

## Glossary

- DT-Grid: Dynamic Tubular Grids
- CRS: Compressed-Row-Storage
- H-RLE: Hierarchical Run-Length Encoding
- DB+Grid: DB-Grid with [B+Trees](https://en.wikipedia.org/wiki/B%2B_tree) → VDB
- [Narrow-band](<https://en.wikipedia.org/wiki/Level_set_(data_structures)#Narrow_band>)
  [Level Sets](https://en.wikipedia.org/wiki/Level_set)
- Dilating: Stretching or scaling (change the size but not the shape of an
  object)
- [Stencil Access](https://en.wikipedia.org/wiki/Stencil_code): E.g.
  [Moore neighborhood](https://en.wikipedia.org/wiki/Moore_neighborhood),
  [Pixel connectivity](https://en.wikipedia.org/wiki/Pixel_connectivity)
- VAS: Virtual Address Space
- TLB: Translation Look-aside Buffer
- [Convolution](https://en.wikipedia.org/wiki/Convolution)
- Morphology
  - [Dilation](https://en.wikipedia.org/wiki/Dilation_(morphology\))
  - [Erosion](https://en.wikipedia.org/wiki/Erosion_(morphology\))
