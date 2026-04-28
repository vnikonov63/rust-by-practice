# Ownership

1. 🌟🌟 
```rust,editable

fn main() {
    // Use as many approaches as you can to make it work
    let x = String::from("Hello world");
    let y = x.as_str();
    println!("{}, {}",x, y);
}
```

2. 🌟🌟
```rust,editable
// Don't modify code in main!
fn main() {
    let s1 = String::from("Hello world");
    let s2 = take_ownership(s1);

    println!("{}", s2);
}

// Only modify the code below!
fn take_ownership(s: String) -> String {
    s
    // println!("{}", s);
}
```


3. 🌟🌟
```rust,editable

fn main() {
    let s = give_ownership();
    println!("{}", s);
}

// Only modify the code below!
fn give_ownership() -> String {
    let s = String::from("Hello World");
    // convert String to Vec
    // important that .into_bytes() consumes the String and the .as_bytes() provides a slice, so there is no consumption.
    let _s = s.as_bytes();
    s
}
```

4. 🌟🌟
```rust,editable
// Fix the error without removing any code
fn main() {
    let s = String::from("Hello World");

    print_str(&s);

    println!("{}", s);
}

fn print_str(s: &String)  {
    println!("{}",s)
}
```

5. 🌟🌟 
```rust,editable
// Don't use clone, use copy instead

// Remember, it is important to remember that String does not implement the copy trait. 
fn main() {
    let x = (1, 2, (), "hello");
    let y = x;
    println!("{:?}, {:?}", x, y);
}
```

#### Mutability
Mutability can be changed when ownership is transferred.

6. 🌟
```rust,editable

// make the necessary variable mutable
fn main() {
    let s = String::from("Hello ");
    
    let mut s1 = s;

    s1.push_str("World!");

    println!("Success!");
}
```

7. 🌟🌟🌟
```rust,editable

fn main() {
    let x = Box::new(5);
    
    let mut y = Box::new(9);      // update this line, don't change other lines!
    
    *y = 4;
    
    assert_eq!(*x, 5);

    println!("Success!");
}
```

### Partial move
Within the destructuring of a single variable, both by-move and by-reference pattern bindings can be used at the same time. Doing this will result in a partial move of the variable, which means that parts of the variable will be moved while other parts stay. In such a case, the parent variable cannot be used afterwards as a whole, however the parts that are only referenced (and not moved) can still be used.

#### Example
```rust,editable

fn main() {
    #[derive(Debug)]
    struct Person {
        name: String,
        age: Box<u8>,
    }

    let person = Person {
        name: String::from("Alice"),
        age: Box::new(20),
    };

    // `name` is moved out of person, but `age` is referenced
    let Person { name, ref age } = person;

    println!("The person's age is {}", age);

    println!("The person's name is {}", name);

    // Error! borrow of partially moved value: `person` partial move occurs
    //println!("The person struct is {:?}", person);

    // `person` cannot be used but `person.age` can be used as it is not moved
    println!("The person's age from person struct is {}", person.age);
}
```

#### Exercises

8. 🌟
```rust,editable

fn main() {
   let t = (String::from("hello"), String::from("world"));

   let (ref _s1, ref _s2) = t; 

   // Modify this line only, don't use `_s`
   println!("{:?}", t);
}
```

9. 🌟🌟
```rust,editable

fn main() {
   let t = (String::from("hello"), String::from("world"));

    // Fill the blanks
    let (ref s1, ref s2) = t;

    println!("{:?}, {:?}, {:?}", s1, s2, t); // -> "hello", "world", ("hello", "world")
}
```


> You can find the solutions [here](https://github.com/sunface/rust-by-practice/blob/master/solutions/ownership/ownership.md)(under the solutions path), but only use it when you need it
