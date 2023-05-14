# TGC-VP
The Scale4Edge ecosystem VP using VP-VIBES peripherals.

This VP is based in MINRES TGC series cores and uses CoreDSL to generate the concrete ISS 
of a particular ISA + extensions. The generator approach makes it very flexible and adaptable.
Since the CoreDSL description is used to generate RTL as well as verification artifacts it 
provides a comprehensive and consistent solution to develop processor cores.

# etiss in TGC-VP
This project replaces the default dbt-rise ISS with ETISS. The ETISS core is provided as a 
SystemC wrapper (`cpu_minres.h/cpp`) within the `etiss-sc` lib repo (found at project root).



## Quick start

* you need to have a C++14 capable compiler, make, python, and cmake installed. Known to work with fresh Ubuntu 20.04.

* install conan.io (see also http://docs.conan.io/en/latest/installation.html). Conan2 has not been tried yet so please install v>1.5
  
  ```

  pip3 install --user conan==1.59.0

  ```
  
  It is advised to use conan version 1.36 or newer. In case of an older version please run
  
  ```sh

  pip3 install --user --upgrade conan

  ``` 
  
  Installing conan for the first time you need to create a profile:
  
  ```
  
  conan profile create default --detect
  
  ```
* ETISS needs to be installed as a library. We recommend installing specific commit 36902d32ae760aa3c413ca06189e6515bc28d79c of ETISS project (https://github.com/tum-ei-eda/etiss)  
  
* checkout source for this TGC-VP repo

* start an out-of-source build:
  
  ```

  cd TGC-VP
  git checkout etiss
  cmake -B build -S . -DCMAKE_BUILD_TYPE=Release -DETISS_PREFIX=<path to ETISS installation>
  cd build
  make -j4 tgc-vp

  ```
  
* run the VP with pre-built firmware
  ```
  src/tgc-vp -f ../fw/hello-world/prebuilt/hello.elf 

  ```
  
To rebuild the firmware you need to install a RISC-V toolchain like https://github.com/riscv/riscv-tools.
  
