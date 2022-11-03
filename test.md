setup

```ocaml
# #require "ppx_csv_conv";;

# #require "digestif.ocaml";;
# #require "irmin" ;;
# #require "ppx_irmin" ;;
```

then stuff

```ocaml
type csv = { name : string; } [@@deriving fields, csv]
type n = int [@@deriving irmin]
```

