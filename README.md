minimal test case to demonstrate `ppx_irmin` + `mdx` breaking on OCaml 5

to reproduce issue:

1. install OCaml 5 switch: `opam switch create 5.0.0~beta1`
1. install deps: `opam install -y irmin ppx_irmin ppx_csv_conv mdx`
1. `dune test` to run mdx on `test.md` to see issue of `Error: Cannot locate
   deriver irmin`

doing the same with OCaml 4.14 will not result in an error.

the `ppx_csv_conv` deriver is in `test.md` as well to demonstrate that it is
functioning correctly with OCaml 5.
