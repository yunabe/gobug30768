# gobug30768

How to reproduce https://github.com/golang/go/issues/30768

- `go get -d github.com/yunabe/gobug30768`
- `(cd /tmp && rm pkg -rf && go install -buildmode=shared -linkshared -pkgdir pkg std && go build -linkshared -pkgdir pkg github.com/yunabe/gobug30768 && ldd gobug30768)`

# Expected
`go build` outputs a binary and `ldd` shows information like:

```
...
libstd.so => /tmp/pkg/libstd.so
...
```

# Actual
`go build -linkshared -pkgdir pkg github.com/yunabe/gobug30768` fails with the following error message:

```
# github.com/yunabe/gobug30768
type..Fm7EsLz5: missing section for relocation target type..FEeY9FdU
type..Fm7EsLz5: reloc 8 (R_CALL) to non-elf symbol type..FEeY9FdU (outer=type..FEeY9FdU) 49 (SABIALIAS)
```
