# AtCoder Modern C++26 Template

A modern, highly optimized competitive programming template designed specifically for **AtCoder** using bleeding-edge **C++26** standard features and the **AtCoder Library (ACL)**. 

This design completely bypasses legacy GCC headers (`<bits/stdc++.h>`) by leveraging **C++26 Modules (`import std;`)**, natively uses type-safe formatting with `std::println`, and includes a clean macro-less approach to optional local debug streams.

## Core Features

* **Modules Over Headers:** Uses `import std;` for modular standard library features, delivering drastically cleaner compile environments and stripping away platform-dependent headers.
* **Modern I/O Standard:** Employs global standard `std::println` wrappers for fast, native string formatting without relying on old stream insertion operators.
* **No Platform-Specific Dependencies:** Avoids legacy GNU headers, ensuring the core layout is portable and fully standard-compliant while supporting advanced types.
* **Seamless ACL Integration:** Features a global `using namespace atcoder;` integration so you can use types like `dsu`, `segtree`, and `modint` natively without prefix constraints.
* **Local Debug Engine:** Includes a smart `debug(...)` print routine utilizing `std::tuple` unpacking that automatically turns into a no-op when submitted to the online judge.

---

## Template Reference & Architecture

### 🔢 Modern Type Shortcuts
* **Shorthand Scalars:** `ll` (`long long`), `ull` (`unsigned long long`), and `ld` (`long double`).
* **Wide-Integer Support:** Native aliases for `i128` (`__int128`) and `ui128` (`unsigned __int128`) to handle large numbers up to 2¹²⁷-1 without overflow.
* **Vector Containers:** Quick typing for standard arrays (`vi`, `vll`, `vc`, `vb`, `vs`) and nested multi-dimensional structures (`vvi`, `vvll`).
* **Pairs:** `pii` and `pll` wrappers for standard coordinate and weight pairs.

### 🔄 Loops & Ranges
* `rep(i, N)`: Forward loop running from `0` up to `N - 1` safely evaluated using signed 64-bit integer tracking (`ll`).
* `rep3(i, M, N)`: Range loop moving forward from `M` up to `N - 1`.
* `rrep(i, N)`: Reverse loop stepping from `N - 1` down to `0`.
* `all(x)` / `rall(x)`: Shortens standard iterator endpoints for range operations (e.g., `sort(all(v));`).

### 📦 Utilities & Mathematical Constants
* `yn(condition)`: Clean conditional shorthand that outputs a capitalized `"Yes"` or `"No"` followed by a newline.
* `inf`: Set to a safe 10¹⁸ ceiling (`1000000000000000000LL`) to prevent signed overflow on additions.
* `mod998` / `mod107`: Pre-configured standard competitive programming modulo definitions (`998244353` and `1000000007`) guarded with `[[maybe_unused]]`.

---

## Environment & Compilation Guide

### Recommended Toolchain
For modern C++26 module compliance and efficient static linking, **Clang 23** combined with `libc++` and LLVM tooling is highly recommended.

### Local Compilation & Execution
To build your source locally while mapping your pre-compiled standard modules (`std.pcm`/`std.o`), enabling strict compiler warnings, and activating your custom `debug(...)` stream, use the following command:

```bash
cd "/home/smizuno/workspace/" && \
clang++-23 -std=c++26 -stdlib=libc++ -fuse-ld=lld -rtlib=compiler-rt --unwindlib=libunwind -static -O3 \
-DLOCAL -Wall -Wextra -Wpedantic \
-fmodule-file=std=/home/smizuno/workspace/std.pcm main.cpp /home/smizuno/workspace/std.o \
-o /tmp/main && /tmp/main
```

### AtCoder Production Submission
When submitted, the online judge processes your template natively under its standard C++26 pipeline (`import std;` executes through modern module mapping) and automatically turns off the `debug(...)` block seamlessly.
