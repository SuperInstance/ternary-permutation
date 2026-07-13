# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Fixed
- `order()` no longer panics spuriously on valid permutations whose order exceeds
  `n² + 1`. The previous iterative approach bounded the search at `n² + 1`, which
  first fails at degree 25 (a product of cycles of length 4·5·7·9 has order 1260 >
  25² + 1 = 626). Order is now computed exactly as the least common multiple of the
  cycle lengths (`O(n)`).
- Corrected the README "How It Works" description of the permutation **sign**. The
  old text ("−1 if any cycle has even length") was mathematically wrong: two
  even-length cycles yield an even permutation (+1). The code was already correct.
- `cargo fmt`/`cargo clippy` now pass cleanly. Four pre-existing `rustfmt` violations
  and a `clippy::len_without_is_empty` lint were failing the CI `fmt` and `clippy`
  jobs (run with `-D warnings`). Added `Permutation::is_empty()`.

### Changed
- README "Order" and "Orbit computation" descriptions updated to match the actual
  implementation (LCM of cycle lengths; graph traversal rather than "BFS").

### Tests
- Replaced a fake-green test (`test_stabilizer_generators`) that asserted a tautology
  (`!empty || empty`) with real assertions on the stabilizer.
- Added coverage: orbit-stabilizer theorem spot-check for S₃ (6 = 3·2), sign of
  two/three even-length cycles, `symmetric_group(4)` yields 24 distinct bijections,
  `transpositions(4)` yields C(4,2)=6, generated-group size equals the order, three
  error-path `should_panic` cases, and a regression test for the high-degree order fix.
