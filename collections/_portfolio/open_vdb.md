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

```
Created with https://asciiflow.com/

                                         openVDB


┌─────────────┐                      ┌─────────────┐                       ┌─────────────┐
│ Grid 1      │                      │ Grid 2      │                       │ Grid 3      │
├─────────────┤                      ├─────────────┤                       ├─────────────┤
│ Transform 1 │12345678901234567890  │ Transform 2 │12345678901234567890   │ Transform 3 │
│             │                      │             │                       │             │
│ TreeRef     │                      │ TreeRef     │                       │ TreeRef     │
└──────┬──────┘                      └──────┬──────┘                       └──────┬──────┘
       │                                    │                                     │
       └────────────────────────────────────┼─────────────────────────────────────┘
                                            │
                                            ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                        │
│                                              ┌──────────┐                              │
│                                              │          │                              │
│                                              │ RootNode │    HashMap                   │   Background Value, empty voxel value
│  Level 3                                     │          │                              │
│                                              └────┬─────┘                              │
│                                                   │                                    │
│                                         ┌─────────┘                                    │
│                                         ▼                                              │
│                               ┌──────────────────┐                                     │
│                               │    InnerNode     │           32x16x8 (4096) Voxels     │
│  Level 2                      │                  │ x Int32                             │   Tile Value, set to single value if
│                               │ 1234567890123456 │           per Dimension/Side        │   child nodes voxels have all the same
│                               │ 1234567890123456 │                                     │   value, i.e. complete tile is filled
│                               └─────────┬────────┘                                     │
│                                         │                                              │
│                                 ┌───────┘                                              │   non-leaf nodes store either a tile value
│                                 ▼                                                      │   or a child node at each grid position
│                        ┌──────────────────┐                                            │
│                        │    InnerNode     │                                            │
│  Level 1               │                  │ x 32             16x8 Voxel per Dimension  │   Tile Value
│                        │ 1234567890123456 │                                            │
│                        └────────┬─────────┘                                            │
│                                 │                                                      │
│                   ┌─────────────┘                                                      │
│                   ▼                                                                    │
│              ┌──────────┐                                                              │
│              │ LeafNode │                                                              │
│  Level 0     │          │ x 16                               8 Voxel per Dimension     │   Voxel Value, single value
│              │ 12345678 │                                                              │
│              └──────────┘                                                              │
│                                                                                        │
└────────────────────────────────────────────────────────────────────────────────────────┘

 Prune: replace full child node with one tile value representing the same volume,
 but more sparselynull(reducing memory footprint).

 Iterators visit (in)active or all voxels

 Value iterators travers entire tree visiting
 eachavalue (tileworavoxel)eexactly once.

 Leaf iterator visits each leaf node exactly
 once (used for narrow-band voxel operations).

 A node iterator traverses a tree in depth-first order,
 starting from its root, and visits each node exactly once.

 Node value iterator visits the values (active, inactive or both) stored in a single
 RootNode, InternalNode or LeafNode, whereas a node child iterator visits the children
 of a single root or internal node.

 Value accessor: caches tree traversal path from last voxel accessor. When accessing
 a neighboring voxel performs a bottom-up traversal lookup (i.e. goes up to first
 common parent node). This increases performance when iterating over voxels.

 narrow-band level set: neighbourhood of level set is interesting, "signed distance field" -> inside/outside level set?
 https://youtu.be/RDUH2412ZU0
```

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
- [CppCast Episode 227: OpenVDB with Ken Museth](https://youtu.be/qCt2el3-x3A)

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
- `cd c-blosc/`
- `git co tags/v1.5.4`
- `mkdir build`
- `cd build/`
- `ccmake ..`
  - install `ccmake` via `sudo apt-get install cmake-curses-gui`
  - use `g` to generate
- `sudo cmake --build . --target install`

### Install other [dependencies](https://www.openvdb.org/documentation/doxygen/dependencies.html) via `apt-get`

Taken from
[Installing Dependencies](https://www.openvdb.org/documentation/doxygen/dependencies.html#depInstallingDependencies):

- `sudo apt-get install libilmbase-dev`
- `sudo apt-get install libtbb-dev`
- `sudo apt-get install libcppunit-dev`
- `sudo apt-get install libboost-system-dev`
- `sudo apt-get install libboost-iostreams-dev`
- `sudo apt-get install libboost-python-dev`
- `sudo apt-get install libboost-numpy-dev`
- `sudo apt-get install libjemalloc-dev`

### Build ([standalone](https://www.openvdb.org/documentation/doxygen/build.html#buildBuildStandalone)) openVDP

- `git clone git@github.com:AcademySoftwareFoundation/openvdb.git`
- `mkdir build` in repo folder
- `cd buld/`
- `cmake ../ -DCMAKE_NO_SYSTEM_FROM_IMPORTED:BOOL=TRUE -DOPENVDB_BUILD_UNITTESTS=ON`

  - Watch out for the message 'Build files have been written to ...'

  - It is possible to set the install folder (e.g. `/usr/include` or
    `$HOME/openvdb`) by setting `-DCMAKE_INSTALL_PREFIX=/usr/include`
    - `cmake -DCMAKE_INSTALL_PREFIX=/usr/include ../
      -DCMAKE_NO_SYSTEM_FROM_IMPORTED:BOOL=TRUE -DOPENVDB_BUILD_UNITTESTS=ON```

- `-DCMAKE_NO_SYSTEM_FROM_IMPORTED:BOOL=TRUE` is need due to
  [error](https://github.com/AcademySoftwareFoundation/openvdb/issues/70#issuecomment-508984505):

  - /usr/include/c++/7/cstdlib:75:15: fatal error: stdlib.h: No such file or
    directory #include_next <stdlib.h>

- `make -j 12` // -j: amount parallel jobs (`lscpu` to check amount of cores)
- `sudo make install`

#### Run Tests

Dependencies:

- `sudo apt-get install liblog4cplus-dev`
- `sudo apt-get install libcppunit-dev`
- `sudo apt-get install libjemalloc-dev`
- `sudo apt-get install libtbb-dev`

Run custom C++ test:

1. Copy custom test file `TestTalus.cc` to
   `../openvdb/openvdb/unittest/TestTalus.cc`
2. Add `TestTalus.cc` in `CMakeLists.txt`
3. Run specific test in `./openvdb/build/` with
   - `clear && make && ./openvdb/unittest/vdb_test -v -t TestTalus::InternalNode_testCoordToOffset`

Test log files can be found in `openvdb/build/Testing/Temporary`.

Running tests:

- Python & C++ tests: In `../openvdb/build/` run `make test` to run Python and
  C++ tests
- C++ tests only: Alternatively run tests via `./openvdb/unittest/vdb_test -v`
  for more details on the C++ tests
  - `Segmentation fault` happens and is mentioned in
    `tsc/meetings/2019-09-26.md` explaining it happens
    `during serialization of OpenVDB Point Data Grids into Houdini file formats`

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
