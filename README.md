
For `.cargo` configuration inside a member package:

```toml
# inner/.cargo/config.toml
[build]
target = "riscv64gc-unknown-none-elf"
```

Enter the package folder to run cargo commands, then we get correct build target:

`target/riscv64gc-unknown-none-elf 👈 /doc/inner/index.html`

```bash
outer/inner $ cargo doc
 Documenting inner v0.1.0 (/rust/tmp/outer/inner)
   Generated /rust/tmp/outer/target/riscv64gc-unknown-none-elf/doc/inner/index.html
```

But if we run cargo commands from workspace root, since there is no `.cargo` configuration,
cargo won't notice the inner configuration even if `-p` or `--manifest-path` is specified:

```bash
outer $ cargo doc -p inner
 Documenting inner v0.1.0 (/rust/tmp/outer/inner)
   Generated /rust/tmp/outer/target/doc/inner/index.html

outer $ cargo doc --manifest-path inner/Cargo.toml 
   Generated /rust/tmp/outer/target/doc/inner/index.html
```
