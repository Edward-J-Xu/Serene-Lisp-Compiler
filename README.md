# Serene-Lisp-Compiler
Design and Implement a lisp compiler using LLVM and MLIR

Credit to https://devheroes.codes/Serene

* Serene lang

** Setup development environment
Setup the githook and install dependencies using the following commands:

 #+BEGIN_SRC bash
 ./builder setup
 #+END_SRC

*** Dependencies
    You would need the following dependencies to start get started with *Serene* development

    - LLVM (LLVM Instructions coming up.)
    - cmake
    - ninja
    - doxygen (If you want to build the docs as well)
    - Valgrind
    - CCache (If you want faster builds specially with the LLVM)

** LLVM Installation
  MLIR is a part of the [[https://llvm.org][LLVM]] project and in order to build it we need to build the LLVM itself as well.
  Here is a quick guide to build the latest version of the LLVM and MLIR.

  #+BEGIN_SRC bash
    ## YES we're using the development version of MLIR
    git clone https://github.com/llvm/llvm-project.git

    mkdir llvm-project/build
    cd llvm-project/build

    cmake -G Ninja ../llvm \
          -DCMAKE_INSTALL_PREFIX=/your/target/path \
          -DLLVM_PARALLEL_COMPILE_JOBS=7 \
          -DLLVM_PARALLEL_LINK_JOBS=1 \
          -DLLVM_BUILD_EXAMPLES=ON \
          -DLLVM_TARGETS_TO_BUILD="X86" \
          -DCMAKE_BUILD_TYPE=Release \
          -DLLVM_ENABLE_ASSERTIONS=ON \
          -DLLVM_CCACHE_BUILD=ON \
          -DCMAKE_EXPORT_COMPILE_COMMANDS=ON \
          -DLLVM_ENABLE_PROJECTS='clang;lldb;lld;mlir;clang-tools-extra;compiler-rt' \
          -DCMAKE_C_COMPILER=clang \       # If you have clang installed already
          -DCMAKE_CXX_COMPILER=clang++ \   # If you have clang installed already
          -DLLVM_ENABLE_LLD=ON

    cmake --build .

    cmake --build . --target check-mlir

    cmake -DCMAKE_INSTALL_PREFIX=/your/target/location -P cmake_install.cmake
  #+END_SRC

  You need to have =clang= and =lld= installed to compile the LLVM with the above command. Also if you
  are not using =ccache= just remove the option related to it from the above command.

*** Emacs
    If you're using Emacs as your development environment just install =clangd= and =lsp=.


* How to build
In order to build for development (Debug mode) just use =./builder build= to setup the build and build
the project once and then you can just use =./builder compile= to build the changed files only.

Check out the =builder= script for more subcommands and details.

* Cheatsheets
  - [[https://github.com/muqsitnawaz/modern-cpp-cheatsheet][Modern C++ Cheatsheet]]
* Get Help
  If you need help or you just want to hangout, you can find us at:

  - *IRC*: *#serene-lang* on the freenode server

  - *Matrix Network*: https://matrix.to/#/#serene:matrix.org?via=matrix.org&via=gitter.im

  - *MailingList*: https://www.freelists.org/list/serene