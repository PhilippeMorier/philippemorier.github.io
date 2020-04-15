---
title: IFC
definition: Industry Foundation Classes
tags: BIM buildingSMART
---

## IFC EXPRESS file

- [IFC Specifications Database](https://technical.buildingsmart.org/standards/ifc/ifc-schema-specifications/)

### Example IFC files

- https://standards.buildingsmart.org/IFC/DEV/IFC4_2/FINAL/HTML/link/listing-ifc4x2.htm
- http://www.ifcwiki.org/index.php?title=KIT_IFC_Examples

## STEPcode

- [STEPcode Repo](https://github.com/stepcode/stepcode)
- [STEPCode Wiki](https://stepcode.github.io/)
  - [exp2cxx](https://stepcode.github.io/docs/executables/#exp2cxx)
- https://github.com/wikifactory/stepcode-example

### Build

- Building SC from the command prompt see
  [INSTALL](https://github.com/stepcode/stepcode/blob/master/INSTALL):

  - Download current IFC EXPRESS file
    [here](https://technical.buildingsmart.org/standards/ifc/ifc-schema-specifications/)
    and save it into folder e.g. `../stepcode/data/ifc4x2`
  - `cd stepcode`
  - `mkdir build`
  - `cd build`
  - `cmake .. -DSC_BUILD_SCHEMAS=ifc4x2` //
    [Defaults to special value ALL, which builds all schemas in SC/data](https://stepcode.github.io/docs/cmake_vars/#sc_build_schemas).
  - `make -j12`
  - `make sdai_IFC4x2 generate_cpp_sdai_IFC4x2 lazy_sdai_IFC4x2 sdai_IFC4x2 p21read_sdai_IFC4x2 -j12`

    - these binaries will be saved in `../stepcode/build/bin`
    - use e.g. `p21read_sdai_IFC4x2` like:
      `./bin/p21read_sdai_IFC4x2 ./bin/KIT-Bridge.ifc`

  - `make install` // will put `bin` & `lib` in `sc-install` folder outside
    `stepcode` folder

## WASM

- [Developer’s Guide - WebAssembly](https://webassembly.org/getting-started/developers-guide/)
  - `source ~/Documents/git/emsdk/emsdk_env.sh --build=Release`

## Visual Studio & C++

- Create new C++ project like
  [this](https://code.visualstudio.com/docs/cpp/config-linux)
- Install debugger `sudo apt-get install build-essential gdb`
- STEPcode:
  - `emcmake cmake .. -DSC_BUILD_SCHEMAS=ifc4x2`
  - `emmake make -j12`
  - `emmake make sdai_IFC4x2 -j12`
  - `emmake make install`
  - `emmake make sdai_IFC4x2 generate_cpp_sdai_IFC4x2 lazy_sdai_IFC4x2 sdai_IFC4x2 p21read_sdai_IFC4x2`
- `emmake make`
- `emcc ifc-wasm.so -o ifc-wasm.html`
