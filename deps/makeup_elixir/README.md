# MakeupElixir
[![Build Status](https://travis-ci.org/tmbb/makeup_elixir.svg?branch=master)](https://travis-ci.org/tmbb/makeup_elixir)

A [Makeup](https://github.com/tmbb/makeup/) lexer for the Elixir language.

## Installation

Add `makeup_elixir` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:makeup_elixir, "~> 0.14.0"}
  ]
end
```

The lexer will be automatically registered in Makeup for
the languages "elixir" and "iex" as well as the extensions
".ex" and ".exs".

## Benchmarks

### Schism: "inline vs no inline"

Should we inline parsec or not?
Currently this can be done using a config option.
By default, parsers are not inlined because inlining doubles compilation time.

* Lexing speed:
  [comparison](assets/benchmarks/inline_vs_no_inline-lexing-speed_comparison.html);
  [with inlined parsecs](assets/benchmarks/inline_vs_no_inline-lexing-speed_with_inline.html);
  [without inlined parsecs](assets/benchmarks/inline_vs_no_inline-lexing-speed_without_inline.html).
  Very weird performance characteristics.
  Faster on average but extremely high latency in the worst case.

* Compilation speed:
  [comparison](assets/benchmarks/inline_vs_no_inline-compilation-speed_comparison.html);
  [with inlined parsecs](assets/benchmarks/inline_vs_no_inline-compilation-speed_with_inline.html);
  [without inlined parsecs](assets/benchmarks/inline_vs_no_inline-compilation-speed_without_inline.html).
  As expected, compiling the inlined parsecs is much slower (about 2x slower)

### Schism: "map lookup vs pattern matching"

Postprocessing the token lists using map lookup VS pattern matching

* Lexing speed:
  [comparison](assets/benchmarks/map_lookup_vs_pattern_matching-lexing-speed_comparison.html);
  [map lookup](assets/benchmarks/map_lookup_vs_pattern_matching-lexing-speed_map_lookup.html);
  [pattern matching](assets/benchmarks/map_lookup_vs_pattern_matching-lexing-speed_pattern_matching.html).
  Very weird performance characteristics.
  Faster on average but extremely high latency in the worst case.

* Compilation speed:
  [comparison](assets/benchmarks/map_lookup_vs_pattern_matching-compilation-speed_comparison.html);
  [map lookup](assets/benchmarks/map_lookup_vs_pattern_matching-compilation-speed_map_lookup.html);
  [pattern matching](assets/benchmarks/map_lookup_vs_pattern_matching-compilation-speed_pattern_matching.html).

### Schism: "parse delimiter pairs"

This lexer used to use a very expensive operation to match some delimiters,
which seemed to have supralinear complexity.
Now, only a couple delimiters are parsed like this.

* [Benchmark](assets/benchmarks/delimited_pairs-complexity.html)
