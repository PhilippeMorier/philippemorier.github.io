---
title: OpenVDB
definition:
  Hierarchical data structure and a large suite of tools for the efficient
  storage and manipulation of sparse volumetric data.
tags: dynamic sparse volumetric data tree tile voxel grid
---

*V*olumetric,  
*D*ynamic grid that shares several characteristics with  
_B_+trees

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

## Access Algorithms

- Random Access
- Sequential Access
- [Stencil Access](https://en.wikipedia.org/wiki/Stencil_code)

## Sources

- [OpenVDB overview](https://www.openvdb.org/documentation/doxygen/overview.html)
- Original Paper:
  [VDB: High-Resolution Sparse Volumes with Dynamic Topology](http://www.museth.org/Ken/Publications_files/Museth_TOG13.pdf)
- Talk explaining VDB:
  [OpenVDB: An Open Source Data Structure and Toolkit for High-Resolution Volumes](https://youtu.be/7hUH92xwODg)
- VDB on GPU:
  [Fast Fluid Simulations with Sparse Volumes on the GPU](https://www.researchgate.net/publication/325488464_Fast_Fluid_Simulations_with_Sparse_Volumes_on_the_GPU)

## Compile openVDB to WASM (attempt)

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
