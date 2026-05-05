# Package and Crate
A package is a project which you create with Cargo (in most cases), so it contains a `Cargo.toml` file in it.

1. 🌟 Create a package  with below layout:
`cargo new hello-package`
```shell
.
├── Cargo.toml
└── src
    └── main.rs

1 directory, 2 files
```

```toml
# in Cargo.toml
[package]
name = "hello-package"
version = "0.1.0"
edition = "2021"
```

> Note! We will use this package across the whole chapter as a practice project.

2. 🌟 Create a package with below layout:
`cargo new --lib hello-package1`
```shell
.
├── Cargo.toml
└── src
    └── lib.rs

1 directory, 2 files
```

```toml
# in Cargo.toml
[package]
name = "hello-package1"
version = "0.1.0"
edition = "2021"
```

> Note! This package could be safely removed due to the first one's existence.

3. 🌟 
```rust,editable
/* FILL in the blank with your ANSWER */

// Q: What's the difference between package number 1 and number 2?
// A: One is a library and the other one is a binary.
```


## Crate
A crate is a binary or library. The crate root is a source file that the Rust compiler starts from and makes up the root module of the crate.

In package `hello-package`, there is binary crate with the same name as the package : `hello-package`, and `src/main.rs` is the crate root of this binary crate.

Similar to `hello-package`, `hello-package1` also has a crate in it, however, this package doesn't contain a binary crate but a library crate, and `src/lib.rs` is the crate root.

4. 🌟
```rust,editable
/* FILL in the blank with your ANSWER */

// Q: What's the name of the library crate in package `hello-package1`?
// A: hello-package1 
```


5. 🌟🌟 Add a library crate for `hello-package` and describe it's files tree below:
```shell,editable
# FILL in the blanks
.
├── Cargo.lock
├── Cargo.toml
├── src
│   ├── main.rs
│   └── lib.rs 
```

After this step, there should be two crates in package `hello-package`: **a binary crate and a library crate, both with the same name as the package**.

6. 🌟🌟🌟 A package can contain at most one library crate, but it can contain as many binary crates as you would like by placing files in `src/bin` directory: **each file will be a separate binary crate with the same name as the file**.

```shell,editable
# Create a package which contains 
# 1. three binary crates: `hello-package`, `main1` and `main2`
# 2. one library crate
# describe the directory tree below
.
├── Cargo.toml
├── Cargo.lock
├── src
│   ├── main.rs
│   ├── lib.rs  
│   └── bin
│       └── main1.rs 
│       └── main2.rs 
├── tests # directory for integrated tests files
│   └── some_integration_tests.rs
├── benches # dir for benchmark files
│   └── simple_bench.rs
└── examples # dir for example files
    └── simple_example.rs
```

Yep, as you can see, the above package structure is very standard and is widely used in many Rust projects.


> You can find the solutions [here](https://github.com/sunface/rust-by-practice/blob/master/solutions/crate-module/crate.md) (under the solutions path), but only use it when you need it :)
