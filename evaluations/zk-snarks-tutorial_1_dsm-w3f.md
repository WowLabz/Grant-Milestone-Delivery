

# Evaluation

- **Status:** In Progress.
- **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/ZK-Snarks%20tutorial.md
- **Milestone:** 1
- **Kusama Identity:** Address
- **Previously successfully merged evaluation:** N/A

| Number | Deliverable | Accepted | Link | Evaluation Notes |
| ------ | ----------- | -------- | ---- |----------------- |
| **0a.** | License |<ul><li>[x] </li></ul>| MIT license can be found [here](https://github.com/bright/zk-snarks-with-substrate/tree/main/LICENSE). |  |
| **0b.** | Documentation |<ul><li>[x] </li></ul>| Documentation can be found in the [README](https://github.com/bright/zk-snarks-with-substrate/tree/main/pallets/zk-snarks/README.md) file. ||
| **0c.** | Testing and Testing Guide |<ul><li>[ ] </li></ul>| [Repository](https://github.com/bright/zk-snarks-with-substrate/) | Need a tutorial for functional testing the pallet |
| **0d.** | Docker |<ul><li>[x] </li></ul>| [Repository](https://github.com/bright/zk-snarks-with-substrate/) | 
| 1. | The pallet |<ul><li>[ ] </li></ul>| [Repository](https://github.com/bright/zk-snarks-with-substrate/) and [polkadotjs app](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/extrinsics) | Need a tutorial for using / testing.
| 2. | Blog post |<ul><li>[ ] </li></ul> | Blog post can be found in https//github.com/bright/zk-snarks-with-substrate/tree/main/blog/introduction.md | Changes requested.


### Tutorial text

1. Improve the citations, examples below:

"Zero-knowledge proof is a method where one party...". Who defined this?

Please review all text.


2. For some affirmations there is no explanation at all, please include at least one statement explaining the why of the statements. You can also include a citation/reference for further explanations if the reader wants to know more about the topic. Example below:

"The first ones are the problems that can be run in polynomial time and those are not applicable for the zk-SNARKs.". Why? 

What is a QAP (Quadratic Arithmetic Program)? You mention the term as if the reader already knows what it is. The first time you mention a term you should give at least a brief explanation of it or let a reference for further reading. 


3. R1CS is mentioned before the acronym definition.


### Code in the tutorial

After installing Circom (Rust version, javascript one is deprecated) and trying to run the examples in the tutorial, I got that some options are not valid, you need to change --o to -o and --p to -p as shown below. Furthermore, the --O0 is a parameter and not an option, then should be placed together with the parameters (before the options).

`circom task.circom --r1cs --wasm --sym --c --o build --O0 --p bls12381` change to `circom task.circom --r1cs --wasm --sym --c --O0 -o build -p bls12381` in order to work. 

The next step, generating the witness, is also with some problems in the command. You need to navigate to the folder where generate_witness.js was generated to run the command. There is no explanation of that in the tutorial. Please add more information about what are the outputs of the commands and how to properly execute the commands with all steps required explained. Would be nice to have information on where the files needed are being generated by the commands as well.

### Running the system 

Please add to the tutorial an explanation on how to run the extrinsic in the zk-snarks pallet with examples. Predefined input examples and print screens are welcome in this part of the tutorial.


### Code Quality

- Automated tests are running and passing. The coverage is reasonable: 75 / 87 (86.21%) on the lib.rs of the pallet.

- Some warnings generated by cargo clippy:

```
warning: casting integer literal to `u64` is unnecessary
  --> pallets/zk-snarks/src/weights.rs:45:25
   |
45 |         Weight::from_ref_time(22_000_000 as u64).saturating_mul(len as u64)
   |                               ^^^^^^^^^^^^^^^^^ help: try: `22_000_000_u64`
   |
   = note: `#[warn(clippy::unnecessary_cast)]` on by default
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#unnecessary_cast

warning: casting integer literal to `u64` is unnecessary
  --> pallets/zk-snarks/src/weights.rs:46:46
   |
46 |             .saturating_add(T::DbWeight::get().writes(1 as u64))
   |                                                       ^^^^^^^^ help: try: `1_u64`
   |
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#unnecessary_cast

warning: casting integer literal to `u64` is unnecessary
  --> pallets/zk-snarks/src/weights.rs:52:25
   |
52 |         Weight::from_ref_time(32_000_000 as u64).saturating_mul(len as u64)
   |                               ^^^^^^^^^^^^^^^^^ help: try: `32_000_000_u64`
   |
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#unnecessary_cast

warning: casting integer literal to `u64` is unnecessary
  --> pallets/zk-snarks/src/weights.rs:53:45
   |
53 |             .saturating_add(T::DbWeight::get().reads(1 as u64))
   |                                                      ^^^^^^^^ help: try: `1_u64`
   |
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#unnecessary_cast

warning: casting integer literal to `u64` is unnecessary
  --> pallets/zk-snarks/src/weights.rs:54:46
   |
54 |             .saturating_add(T::DbWeight::get().writes(1 as u64))
   |                                                       ^^^^^^^^ help: try: `1_u64`
   |
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#unnecessary_cast

warning: manual `RangeInclusive::contains` implementation
  --> pallets/zk-snarks/src/deserialization.rs:33:1
   |
33 | / construct_uint! {
34 | |     pub struct U256(6);
35 | | }
   | |_^
   |
   = note: `#[warn(clippy::manual_range_contains)]` on by default
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#manual_range_contains
   = note: this warning originates in the macro `$crate::construct_uint` which comes from the expansion of the macro `construct_uint` (in Nightly builds, run with -Z macro-backtrace for more info)

warning: manual implementation of an assign operation
  --> pallets/zk-snarks/src/deserialization.rs:33:1
   |
33 | / construct_uint! {
34 | |     pub struct U256(6);
35 | | }
   | |_^
   |
   = note: `#[warn(clippy::assign_op_pattern)]` on by default
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#assign_op_pattern
   = note: this warning originates in the macro `$crate::construct_uint` which comes from the expansion of the macro `construct_uint` (in Nightly builds, run with -Z macro-backtrace for more info)

warning: manual implementation of an assign operation
  --> pallets/zk-snarks/src/deserialization.rs:33:1
   |
33 | / construct_uint! {
34 | |     pub struct U256(6);
35 | | }
   | |_^
   |
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#assign_op_pattern
   = note: this warning originates in the macro `$crate::construct_uint` which comes from the expansion of the macro `construct_uint` (in Nightly builds, run with -Z macro-backtrace for more info)

warning: use of `offset` with a `usize` casted to an `isize`
  --> pallets/zk-snarks/src/deserialization.rs:33:1
   |
33 | / construct_uint! {
34 | |     pub struct U256(6);
35 | | }
   | |_^
   |
   = note: `#[warn(clippy::ptr_offset_with_cast)]` on by default
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#ptr_offset_with_cast
   = note: this warning originates in the macro `$crate::uint_overflowing_binop` which comes from the expansion of the macro `construct_uint` (in Nightly builds, run with -Z macro-backtrace for more info)

warning: use of `offset` with a `usize` casted to an `isize`
  --> pallets/zk-snarks/src/deserialization.rs:33:1
   |
33 | / construct_uint! {
34 | |     pub struct U256(6);
35 | | }
   | |_^
   |
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#ptr_offset_with_cast
   = note: this warning originates in the macro `$crate::uint_overflowing_binop` which comes from the expansion of the macro `construct_uint` (in Nightly builds, run with -Z macro-backtrace for more info)

warning: this expression creates a reference which is immediately dereferenced by the compiler
   --> pallets/zk-snarks/src/deserialization.rs:103:22
    |
103 |         U256::from_dec_str(&s[i]).unwrap().to_big_endian(dec_numbers[i].as_mut_slice());
    |                            ^^^^^ help: change this to: `s[i]`
    |
    = note: `#[warn(clippy::needless_borrow)]` on by default
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#needless_borrow

warning: the loop variable `i` is only used to index `inputs`
   --> pallets/zk-snarks/src/deserialization.rs:152:11
    |
152 |     for i in 0..inputs.len() {
    |              ^^^^^^^^^^^^^^^
    |
    = note: `#[warn(clippy::needless_range_loop)]` on by default
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#needless_range_loop
help: consider using an iterator
    |
152 |     for <item> in &inputs {
    |         ~~~~~~    ~~~~~~~

warning: this call to `from_str_radix` can be replaced with a call to `str::parse`
   --> pallets/zk-snarks/src/deserialization.rs:153:9
    |
153 |         match u64::from_str_radix(inputs[i], 10) {
    |               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ help: try: `inputs[i].parse::<u64>()`
    |
    = note: `#[warn(clippy::from_str_radix_10)]` on by default
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#from_str_radix_10

warning: it looks like you're manually copying between slices
  --> pallets/zk-snarks/src/verify.rs:51:3
   |
51 | /         for i in 0..48 {
52 | |             new_bytes[i] = x[i];
53 | |             new_bytes[i + 48] = y[i];
54 | |         }
   | |_________^
   |
   = note: `#[warn(clippy::manual_memcpy)]` on by default
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#manual_memcpy
help: try replacing the loop by
   |
51 ~         new_bytes[..48].copy_from_slice(&x[..48]);
52 +     new_bytes[48..(48 + 48)].copy_from_slice(&y[..48]);
   |

warning: it looks like you're manually copying between slices
  --> pallets/zk-snarks/src/verify.rs:65:3
   |
65 | /         for i in 0..48 {
66 | |             new_bytes[i] = x_c1[i];
67 | |             new_bytes[i + 48] = x_c0[i];
68 | |             new_bytes[i + 96] = y_c1[i];
69 | |             new_bytes[i + 144] = y_c0[i];
70 | |         }
   | |_________^
   |
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#manual_memcpy
help: try replacing the loop by
   |
65 ~         new_bytes[..48].copy_from_slice(&x_c1[..48]);
66 +     new_bytes[48..(48 + 48)].copy_from_slice(&x_c0[..48]);
67 +     new_bytes[96..(48 + 96)].copy_from_slice(&y_c1[..48]);
68 +     new_bytes[144..(48 + 144)].copy_from_slice(&y_c0[..48]);
   |

warning: this returns a `Result<_, ()>`
   --> pallets/zk-snarks/src/verify.rs:112:2
    |
112 | /     pub fn from_uncompressed(
113 | |         alpha: &G1UncompressedBytes,
114 | |         beta: &G2UncompressedBytes,
115 | |         gamma: &G2UncompressedBytes,
116 | |         delta: &G2UncompressedBytes,
117 | |         ic: &Vec<G1UncompressedBytes>,
118 | |     ) -> Result<Self, ()> {
    | |_________________________^
    |
    = note: `#[warn(clippy::result_unit_err)]` on by default
    = help: use a custom `Error` type instead
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#result_unit_err

warning: the loop variable `i` is only used to index `ic`
   --> pallets/zk-snarks/src/verify.rs:125:12
    |
125 |         for i in 0..ic.len() {
    |                  ^^^^^^^^^^^
    |
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#needless_range_loop
help: consider using an iterator
    |
125 |         for <item> in &ic {
    |             ~~~~~~    ~~~

warning: this returns a `Result<_, ()>`
   --> pallets/zk-snarks/src/verify.rs:140:2
    |
140 | /     pub fn from_uncompressed(
141 | |         a: &G1UncompressedBytes,
142 | |         b: &G2UncompressedBytes,
143 | |         c: &G1UncompressedBytes,
144 | |     ) -> Result<Self, ()> {
    | |_________________________^
    |
    = help: use a custom `Error` type instead
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#result_unit_err

warning: you are deriving `PartialEq` and can implement `Eq`
   --> pallets/zk-snarks/src/verify.rs:153:17
    |
153 | #[derive(Debug, PartialEq)]
    |                 ^^^^^^^^^ help: consider deriving `Eq` as well: `PartialEq, Eq`
    |
    = note: `#[warn(clippy::derive_partial_eq_without_eq)]` on by default
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#derive_partial_eq_without_eq

warning: redundant closure
   --> pallets/zk-snarks/src/verify.rs:163:25
    |
163 |     inputs.into_iter().map(|i| Scalar::from(i)).collect()
    |                            ^^^^^^^^^^^^^^^^^^^ help: replace the closure with the function itself: `Scalar::from`
    |
    = note: `#[warn(clippy::redundant_closure)]` on by default
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#redundant_closure

warning: redundant clone
   --> pallets/zk-snarks/src/lib.rs:200:32
    |
200 |             ProofStorage::<T>::put(proof.clone());
    |                                         ^^^^^^^^ help: remove this
    |
    = note: `#[warn(clippy::redundant_clone)]` on by default
note: this value is dropped without further use
   --> pallets/zk-snarks/src/lib.rs:200:27
    |
200 |             ProofStorage::<T>::put(proof.clone());
    |                                    ^^^^^
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#redundant_clone

warning: unneeded `return` statement
   --> pallets/zk-snarks/src/lib.rs:226:4
    |
226 | /             return match verify(vk, proof, prepare_public_inputs(deserialized_public_inputs)) {
227 | |                 Ok(true) => {
228 | |                     Self::deposit_event(Event::<T>::VerificationSuccess);
229 | |                     Ok(())
...   |
235 | |                 Err(_) => Err(Error::<T>::ProofVerificationError.into()),
236 | |             }
    | |_____________^
    |
    = note: `#[warn(clippy::needless_return)]` on by default
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#needless_return
help: remove `return`
    |
226 ~             match verify(vk, proof, prepare_public_inputs(deserialized_public_inputs)) {
227 ~                 Ok(true) => {
228 ~                     Self::deposit_event(Event::<T>::VerificationSuccess);
229 ~                     Ok(())
230 ~                 },
231 ~                 Ok(false) => {
232 ~                     Self::deposit_event(Event::<T>::VerificationFailed);
233 ~                     Ok(())
234 ~                 },
235 ~                 Err(_) => Err(Error::<T>::ProofVerificationError.into()),
236 ~             }
    |

warning: `pallet-zk-snarks` (lib) generated 27 warnings (5 duplicates)
    Checking pallet-grandpa v4.0.0-dev (https://github.com/paritytech/substrate.git?branch=polkadot-v0.9.31#7a4e5163)
    Checking rocksdb v0.19.0
    Checking kvdb-rocksdb v0.16.0
    Checking sc-client-db v0.10.0-dev (https://github.com/paritytech/substrate.git?branch=polkadot-v0.9.31#7a4e5163)
    Checking sc-service v0.10.0-dev (https://github.com/paritytech/substrate.git?branch=polkadot-v0.9.31#7a4e5163)
    Checking sc-cli v0.10.0-dev (https://github.com/paritytech/substrate.git?branch=polkadot-v0.9.31#7a4e5163)
warning: redundant clone
  --> node/src/rpc.rs:48:47
   |
48 |     module.merge(System::new(client.clone(), pool.clone(), deny_unsafe).into_rpc())?;
   |                                                  ^^^^^^^^ help: remove this
   |
   = note: `#[warn(clippy::redundant_clone)]` on by default
note: this value is dropped without further use
  --> node/src/rpc.rs:48:43
   |
48 |     module.merge(System::new(client.clone(), pool.clone(), deny_unsafe).into_rpc())?;
   |                                              ^^^^
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#redundant_clone

warning: very complex type used. Consider factoring parts into `type` definitions
  --> node/src/service.rs:41:6
   |
41 |   ) -> Result<
   |  ______^
42 | |     sc_service::PartialComponents<
43 | |         FullClient,
44 | |         FullBackend,
...  |
59 | |     ServiceError,
60 | | > {
   | |_^
   |
   = note: `#[warn(clippy::type_complexity)]` on by default
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#type_complexity

warning: writing `&String` instead of `&str` involves a new object where a slice will do
   --> node/src/service.rs:149:26
    |
149 | fn remote_keystore(_url: &String) -> Result<Arc<LocalKeystore>, &'static str> {
    |                          ^^^^^^^ help: change this to: `&str`
    |
    = note: `#[warn(clippy::ptr_arg)]` on by default
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#ptr_arg

warning: `node-template` (lib) generated 3 warnings
warning: useless conversion to the same type: `u128`
   --> node/src/benchmarking.rs:105:12
    |
105 |                 value: self.value.into(),
    |                        ^^^^^^^^^^^^^^^^^ help: consider removing `.into()`: `self.value`
    |
    = note: `#[warn(clippy::useless_conversion)]` on by default
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#useless_conversion

warning: redundant clone
   --> node/src/benchmarking.rs:164:7
    |
164 |         call.clone(),
    |             ^^^^^^^^ help: remove this
    |
    = note: `#[warn(clippy::redundant_clone)]` on by default
note: this value is dropped without further use
   --> node/src/benchmarking.rs:164:3
    |
164 |         call.clone(),
    |         ^^^^
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#redundant_clone

warning: redundant clone
   --> node/src/benchmarking.rs:166:40
    |
166 |         runtime::Signature::Sr25519(signature.clone()),
    |                                              ^^^^^^^^ help: remove this
    |
note: this value is dropped without further use
   --> node/src/benchmarking.rs:166:31
    |
166 |         runtime::Signature::Sr25519(signature.clone()),
    |                                     ^^^^^^^^^
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#redundant_clone

warning: redundant clone
   --> node/src/benchmarking.rs:167:8
    |
167 |         extra.clone(),
    |              ^^^^^^^^ help: remove this
    |
note: this value is dropped without further use
   --> node/src/benchmarking.rs:167:3
    |
167 |         extra.clone(),
    |         ^^^^^
    = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#redundant_clone

warning: redundant clone
  --> node/src/rpc.rs:48:47
   |
48 |     module.merge(System::new(client.clone(), pool.clone(), deny_unsafe).into_rpc())?;
   |                                                  ^^^^^^^^ help: remove this
   |
note: this value is dropped without further use
  --> node/src/rpc.rs:48:43
   |
48 |     module.merge(System::new(client.clone(), pool.clone(), deny_unsafe).into_rpc())?;
   |                                              ^^^^
   = help: for further information visit https://rust-lang.github.io/rust-clippy/master/index.html#redundant_clone

warning: `node-template` (bin "node-template") generated 7 warnings (2 duplicates)
```




