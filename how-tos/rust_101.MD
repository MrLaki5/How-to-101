

## Rustup
* Command line tool for managing Rust versions and associated tools (compiler, docs)

* Installation
``` bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

* Update to latest version
``` bash
rustup update
```

* Docs
``` bash
rustup doc
```

* Formating tool
``` bash
rustfmt
```

## Rustc
* Rust compiler
``` bash
rustc file.rs
```

## Cargo
* Build system and package manager

* Create new project with cargo
``` bash
cargo new <project name>
# It creates project repo with git files, main.rs inside src and Cargo.toml file
```

* Crate: package of code placed in cargo dependency
``` bash
https://crates.io/
```

* Build project with cargo
``` bash
cargo build
# Cargo.lock: created after first build, trackes versions of crates
# --release: add this for release build, additional code otpimizations done with it
```

* To update dependencies written in cargo.lock, use
``` bash
cargo update
```

* Build project and run it in one command with cargo
``` bash
cargo run
```

* Compile program without producing binaries with cargo
``` bash
cargo check
```

* See docs of all project dependencies
``` bash
cargo doc --open
```


## Syntax

### Variables

* let: statement for creating variable

* mut: statement for mutable variables (by default variables are immutable)

* shadowing can be done in same block, where new definition of variable with same name shadows the prev one

* Expression with semicolon on end is statement

### Functions

* Associated function => static method

### Results

* Results of most std functions are enums where each result enum has two variants (Ok, Err), with this we have error propagation.

### Patern matching

* There are multiple enum types with variants that can be used with patern matching

* match: statement for patern match

### Owenership

* Memory allocated on heap has its variable owner, when this variable gets out of scope memory gets freed.

* Doing copy of variable that has heap part makes variable that is beeing copied not valid anymore (there is no shallow copy, just move)

* For deep copy use .clone() on copy statement

* Function arguments and results also have same effect as copy of variables

* Borrowing (references) is way to pass argument to function without copy of variables

* There can only be one mutable or multiple imutable references in one sequence of access to those references (if we have imutable reference, last referenced before creation of mutable, this code is OK). This exists due to data race conditions

* Slices are references but to part of heap memory

### Project structure

* Package is one or more crates that provide set of functionallity. It has Cargo.toml file that describes how to build those crates. It must contain zero or one library crate and zaro or many binary crates, but it has to have one crate minimum.

* Crate is binary (src/main.rs) or library (src/lib.rs), it has root module.

* Module are parts of crate that give us ability to organize crate. They have privacy options for internal (private) or external (public) possibility to use.

* Path is referencing some funcrion or variable that is in modules structure. It can be relative or absolute. Its syntax is like: module::sub_module::function

