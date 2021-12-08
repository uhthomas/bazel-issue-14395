# Bazel <REPLACE> reproduction

Bazel 4.2.2 introduced a regression where C fails to link on macOS x86_64. This
builds fine with 4.2.1.

The quickest way to reproduce the issue:

```sh
USE_BAZEL_VERSION=4.2.2 bazel build //:bin
```

## Bazel 4.2.2

```sh
❯ USE_BAZEL_VERSION=4.2.2 bazel build //:bin
INFO: Analyzed target //:bin (46 packages loaded, 8076 targets configured).
INFO: Found 1 target...
ERROR: /private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/raze__memchr__2_4_1/BUILD.bazel:40:19: Compiling Rust bin memchr_build_script_ v2.4.1 (35 files) failed: (Exit 1): process_wrapper failed: error executing command bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/rules_rust/util/process_wrapper/process_wrapper --subst 'pwd=${pwd}' -- external/rust_darwin_x86_64/bin/rustc external/raze__memchr__2_4_1/build.rs ... (remaining 23 argument(s) skipped)

Use --sandbox_debug to see verbose messages from the sandbox
error: linking with `external/local_config_cc/cc_wrapper.sh` failed: exit status: 1
  |
  = note: "external/local_config_cc/cc_wrapper.sh" "-m64" "-arch" "x86_64" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.0.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.1.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.10.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.2.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.3.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.4.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.5.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.6.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.7.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.8.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.memchr_build_script_.ae7338a9-cgu.9.rcgu.o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_.1s71bpdk8li7d4tg.rcgu.o" "-L" "external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib" "-L" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libstd-dd8a82589e0cba34.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libpanic_unwind-8c04c8bd0d1a8900.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libobject-c6a4ae86ed2c40d0.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libmemchr-f9ab4d1b2e38b05e.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libaddr2line-002c7b677ad6c512.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libgimli-a3f3d9f86c37973f.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libstd_detect-8b14bcf2354140fd.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/librustc_demangle-d6f2fd91ec8bbbcc.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libhashbrown-24c80e37fb5b15c5.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/librustc_std_workspace_alloc-edb9b11fa36b4795.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libunwind-769780536fb7ef9b.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libcfg_if-d37c37a3a3ac2b0c.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/liblibc-c1bdc4c1f89760ef.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/liballoc-750380e9c94de9ce.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/librustc_std_workspace_core-1108e622f5a15c3d.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libcore-43af7053e70b1eed.rlib" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib/libcompiler_builtins-3a81ebf6a3abbdee.rlib" "-lSystem" "-lresolv" "-lc" "-lm" "-liconv" "-L" "/private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/rust_darwin_x86_64/lib/rustlib/x86_64-apple-darwin/lib" "-o" "bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/raze__memchr__2_4_1/memchr_build_script_" "-Wl,-dead_strip" "-nodefaultlibs" "-undefined" "dynamic_lookup" "-headerpad_max_install_names" "-lstdc++" "-lm"
  = note: ld: library not found for -lstdc++
          clang: error: linker command failed with exit code 1 (use -v to see invocation)


error: aborting due to previous error

Target //:bin failed to build
Use --verbose_failures to see the command lines of failed build steps.
ERROR: /private/var/tmp/_bazel_thomas/9c861fc6d98a2c5a9cf5eae5dc642b60/external/raze__memchr__2_4_1/BUILD.bazel:65:13 Compiling Rust rlib memchr v2.4.1 (35 files) failed: (Exit 1): process_wrapper failed: error executing command bazel-out/darwin-opt-exec-2B5CBBC6/bin/external/rules_rust/util/process_wrapper/process_wrapper --subst 'pwd=${pwd}' -- external/rust_darwin_x86_64/bin/rustc external/raze__memchr__2_4_1/build.rs ... (remaining 23 argument(s) skipped)

Use --sandbox_debug to see verbose messages from the sandbox
INFO: Elapsed time: 12.594s, Critical Path: 2.18s
INFO: 46 processes: 40 internal, 6 darwin-sandbox.
FAILED: Build did NOT complete successfully
```

## Bazel 4.2.1

```sh
❯ USE_BAZEL_VERSION=4.2.1 bazel build //:bin
Starting local Bazel server and connecting to it...
INFO: Analyzed target //:bin (46 packages loaded, 8076 targets configured).
INFO: Found 1 target...
Target //:bin up-to-date:
  bazel-bin/bin_/bin
INFO: Elapsed time: 9.280s, Critical Path: 4.58s
INFO: 52 processes: 39 internal, 13 darwin-sandbox.
INFO: Build completed successfully, 52 total actions
```
