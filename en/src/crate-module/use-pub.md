# Use and pub
1. 🌟 We can bring two types of the same name into the same scope with use, but you need `as` keyword.

```rust,editable
use std::fmt::Result as FmtResult;
use std::io::Result as IoResult;

fn main() {}
```

2. 🌟🌟 If we are using multiple items defined in the same crate or module, then listing each item on its own line will take up too much vertical space.

```rust,editable

// FILL in the blank in two ways
// DON'T add new code line
use std::collections::{HashSet, HashMap, BTreeMap};
// also can do:
// use std::collections::*;

fn main() {
    let _c1:HashMap<&str, i32> = HashMap::new();
    let mut c2 = BTreeMap::new();
    c2.insert(1, "a");
    let _c3: HashSet<i32> = HashSet::new();
}
```

### Re-exporting names with `pub use`
3. 🌟🌟🌟 In our recently created package `hello-package`, add something to make the below code work
```rust,editable
// in here we originally had hello_package::front_of_house::seat_at_table()
// We want to remove the second bit 
// For that we need to move the hosting inside the lib.rs 
// an we can do so with 
// pub use crate::front_of_house::hosing
// the lib.rs is the point of entry for the stuff outside the only library crate inside the package. 
fn main() {
    assert_eq!(hello_package::hosting::seat_at_table(), "sit down please");
     assert_eq!(hello_package::eat_at_restaurant(),"yummy yummy!");
}
```


### Pub(in Crate) 
Sometimes we want an item only be public to a certain crate. For this we can use the `pub(in Crate)` syntax.

#### Example
```rust,editable
pub mod a {
    pub const I: i32 = 3;

    fn semisecret(x: i32) -> i32 {
        use self::b::c::J;
        x + J
    }

    pub fn bar(z: i32) -> i32 {
        semisecret(I) * z
    }
    pub fn foo(y: i32) -> i32 {
        semisecret(I) + y
    }

    mod b {
        pub(in crate::a) mod c {
            pub(in crate::a) const J: i32 = 4;
        }
    }
}
```

### Full Code
The full code of `hello-package` is [here](https://github.com/sunface/rust-by-practice/tree/master/practices/hello-package).


> You can find the solutions [here](https://github.com/sunface/rust-by-practice/blob/master/solutions/crate-module/use-pub.md) (under the solutions path), but only use it when you need it :)
