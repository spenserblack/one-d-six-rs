# One D Six

:warning: Archiving this since this was just a first project to learn Rust. If you stumble on this and
would like to see more development, you can reach me [here](https://github.com/spenserblack/spenserblack/discussions).
I'll be happy to un-archive the repository.

[![Crates.io](https://img.shields.io/crates/v/one-d-six)](https://crates.io/crates/one-d-six)
[![docs.rs](https://docs.rs/one-d-six/badge.svg)](https://docs.rs/one-d-six/)
[![Build Status](https://travis-ci.com/spenserblack/one-d-six-rs.svg?branch=master)](https://travis-ci.com/spenserblack/one-d-six-rs)
[![Dependabot Status](https://api.dependabot.com/badges/status?host=github&repo=spenserblack/one-d-six-rs)](https://dependabot.com)
![Crates.io downloads](https://img.shields.io/crates/d/one-d-six)
![License](https://img.shields.io/crates/l/one-d-six)

Rolls some dice

## Usage
### From Command Line
```bash
# Install
cargo install one-d-six

# Print help
one-d-six -h

# Print total of each dice
one-d-six 3d4 2d6 1d20

# Print each die cast of each dice roll
one-d-six --complex 2d20 1d12
```

### As Library
*This is not complete usage documentation. This is the expected most common usage.*
```rust
use one_d_six::{
  quickroll,
  Dice,
};

// Quickly generates a set of Dice and rolls them
// quickroll can return any int type (i8 - isize, u8 - usize)
let coinflip: u8 = quickroll("1d2");
if coinflip == 1 {
    println!("Heads!");
} else {
    println!("Tails!");
}

// Creating sets of dice
let set_1 = Dice::new(2, 4); // Creates 2d4 with Dice::new
let set_2 = "1d20".parse().unwrap(); // Creates 1d20 by parsing str

// Combining sets of dice
let mut dice = set_1 + set_2; // Creates 2d4 + 1d20

// Prints 50 rolls of the dice set
for _ in 0..50 {
    // Method 1: Printing Dice struct
    println!("2d4 + 1d20: {}", dice.roll_all());

    // Method 2: Printing value of Dice::total(&self)
    let total = dice.total();
    println!("2d4 + 1d20: {}", total);
}

// Getting value of each die cast
let _results = format!("{:?}", dice);
```
Want to roll for your own custom type? Just implement `one_d_six::Rollable` on `MyCustomType`, and
then you can create a new `Die<MyCustomType>`!
