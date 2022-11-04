minimal test case to demonstrate `ppx_irmin` + `mdx` breaking on OCaml 5, as
seen [in this CI run](https://ci.ocamllabs.io/github/mirage/irmin/commit/26bc5002367deb6f2a2c887a586085e8d1cd675f/variant/debian-11-5.0_opam-2.1).

to reproduce issue:

1. install OCaml 5 switch: `opam switch create 5.0.0~beta1`
1. install deps: `opam install -y irmin ppx_irmin ppx_csv_conv mdx`
1. `dune test` to run mdx on `test.md` to see issue of `Error: Cannot locate
   deriver irmin`

doing the same with OCaml 4.14 will not result in an error.

the `ppx_csv_conv` deriver is in `test.md` as well to demonstrate that it is
functioning correctly with OCaml 5.


if you try loading `ppx_irmin` in `utop` when starting with `utop -dsource`
(thanks @patricoferris for the tip!), it appears the root issue _may_ be related
to loading of a library (`fmt`).

<!-- $MDX skip -->
```ocaml
utop # #require "ppx_irmin";;

[%%ocaml.error
  "Cannot load ppx_irmin: error loading shared library: Dynlink.Error (Dynlink.Cannot_open_dll \"Failure(\\\"/home/metanivek/.opam/5.0.0~beta1/lib/fmt/fmt.cmxs: cannot open shared object file: No such file or directory\\\")\")"];;
```



