# Future Integration: ternary-permutation

## Current State
Implements permutation groups acting on ternary vectors: `Permutation` with composition, inverse, order, cycle decomposition, orbit computation, stabilizer groups, symmetric group generators, and action on ternary tuples (mod 3 arithmetic).

## Integration Opportunities

### With ternary-cell / room-as-codespace
Strategy exploration via permutations. An ensign agent has a sequence of rooms to visit; `Permutation` generates alternative orderings. `orbit()` explores all reachable orderings under allowed swaps. `stabilizer()` identifies which room positions are invariant under a strategy change — rooms that must be visited first regardless of strategy. The cycle decomposition reveals cyclic dependencies (A must precede B must precede C must precede A = cycle → deadlock).

### With ternary-matrix
Permutation matrices: each `Permutation` corresponds to a `TernaryMatrix` with exactly one +1 per row/column. `Permutation::compose()` is matrix multiplication. `Permutation::inverse()` is matrix transpose. This connection enables using `ternary-matrix`'s efficient storage for permutation matrices and vice versa.

### With ternary-ring
Permutations act on `Z3` vectors via `act_on_ternary()`. Combined with `ternary-ring`'s `PolyZ3`, permutations define symmetry groups of polynomials. The stabilizer of a polynomial under the action of S_n gives its symmetry — useful for understanding invariant structures in room configurations.

## Potential in Mature Systems
In PLATO, permutations manage task assignment. `Permutation` encodes which ensign is assigned to which room. `compose()` combines assignment changes. `orbit()` under the constraint group (permutations that respect skill requirements) generates all valid assignments. The fleet scheduler selects the optimal permutation from this orbit. `cycle_decomposition()` identifies rotating assignments (ensign A → room 1 → ensign B → room 2 → ensign A) for shift scheduling.

## Cross-Pollination Ideas
**Music × Permutation:** Tone rows (Schoenberg's 12-tone technique) are permutations. In ternary, voice permutations create chord voicings. `compose()` combines voicing transformations. `order()` tells how many times to apply a voicing before returning to the original. `orbit()` under the PLR group from `flux-algebra-rs` generates all related voicings. This is deep music theory via group actions.

**Game theory × Permutation:** Strategy permutations in symmetric games. `stabilizer()` identifies the symmetry group of a game. `orbit()` generates all equivalent strategies. A game with full S_n symmetry has n! equivalent strategies — only need to analyze one representative.

**Cryptography × Permutation:** Block cipher S-boxes are permutations. `compose()` chains substitution layers. `inverse()` provides decryption. `cycle_decomposition()` analyzes diffusion properties. Ternary permutations on GF(3)^n build ternary block ciphers.

## Dependencies for Next Steps
- Large-degree permutations (current implementation stores full images — sparse for n >> 100)
- Integration with `ternary-matrix` for permutation matrix representation
- Constraint permutations: generate only permutations that satisfy room assignment constraints
