# rust-concurrency
Stuff from the rust concurrency book

## naive hashmap
Start

```
cargo new naive_hashmap --lib
```

## Testing as you go
Test as you go by leaving the added-deps.txt out of Cargo.toml, otherwise it won't compile

## the afl part
The book isn't clear on this, we need to install afl. 

[rust-fuzz and afl page](https://rust-fuzz.github.io/book/afl/setup.html)

```
cargo install afl
cargo install --force afl
```
Once it's installed, we only need the following file to build an afl bin for this project
- src/bin/naive_interpreter.rs

```
cargo afl build --release
```

Be sure you have the relevant files in resources/in/ then we can run with 

```
cargo afl fuzz -i resources/in/ -o resources/out/ target/release/naive_interpreter
```

You're likely to get errors at first which can be fixed.
*Be sure to backup each file it says to edit*

This way you can roll back your changes
- Make sure to backup the values of scaling_governer for each cpu prior to changing
- Note one of the instructinos tells you to scaling_factor to "performance" for cpus which allows the fuzzer to start, and the suggested rollback is "ondemand", however, on ubuntu 18, i got errors that this was an invalid value; on ubuntu 18 the default is "powersave"
