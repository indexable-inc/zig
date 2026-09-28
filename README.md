# zig 0.15.2+ix.1

Zig 0.15.2 rebuilt from the official [zig-bootstrap 0.15.2](https://codeberg.org/ziglang/zig-bootstrap/src/tag/0.15.2) with one upstream fix backported and debug symbols kept. Prebuilt archives are on the [releases page](https://github.com/indexable-inc/zig/releases/tag/0.15.2-ix.1).

## What differs from the upstream 0.15.2 tarballs

- `patches/0001-llvm-synchronize-target-initialization.patch` backports [ziglang/zig 75044cb04cc6](https://codeberg.org/ziglang/zig/commit/75044cb04cc67454db98ed7c054081806c3830c6) (fixes [#36490](https://codeberg.org/ziglang/zig/issues/36490)). LLVM's target registry has no lock, and parallel sub-compilations (compiler_rt, libzigc, ubsan_rt) could look a target up while another thread was still registering it, failing with `No available targets are compatible with triple`. No zig release contains the fix yet: 0.16.0 predates it and there is no 0.15.3. The upstream commit is kept verbatim in `docs/upstream/zig/`.
- Built with `-Dstrip=false`, so crashes symbolize. The Linux binary also carries a GNU build ID and line info.
- Built with `-Dno-langref`, so `doc/langref.html` is absent.
- `zig version` prints `0.15.2+ix.1`.

## Archives

| File | sha256 |
| --- | --- |
| `zig-x86_64-linux-0.15.2-ix.1.tar.xz` | `5e6bdc0266a70e4fa1fbee0026929c30bafd9edbaec21657ab42a6e650483cd8` |
| `zig-aarch64-macos-0.15.2-ix.1.tar.xz` | `811731ea2f5b9e86c75bbefd7519723a2023607e38fd9786a213f9660ada780a` |

Both come from one x86_64-linux build (the macOS archive is cross-compiled). The Linux archive was run and compiled a musl hello world. The macOS archive was run on an aarch64 Mac, printed its version and cross-compiled to x86_64-linux-musl.

## Licence

Zig is MIT licensed; see `LICENSE` (copied from the archive). The patch is a derivative of upstream zig and carries the same licence.
