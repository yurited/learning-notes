### WebAssembly

WebAssembly is not much faster than modern Javascript (no 100x performance increase!). A reasonable expectation is it runtime perf 20-30% faster than JS.

#### Web Assembly future (as of Aug 2018)
Garbage Collector,
Multithreading
Hostbindings (DOM manipulations)

#### Language Support
- C/C++
    Emscripten
    Based on LLVM
    Originally use to create asm.js

examples:
PDFKit
https://pspdfkit.com/blog/2017/webassembly-a-new-hope

JS VM compiled into webassembly
https://mbbill.github.io/JSC.js/

- Java / C#
    More challenging, these langs require a CG
    Blazor, experimental project using Mono


- Javascript
    Needs a GC and isn't statically typed
    Walt is a js-like syntax for webassembly test format https://github.com/ballercat/walt

    AssemblyScript - a typescript to WA compiler
        awaiting GC before it can really become powerful
    example: https://blog.scottlogic.com/2017/10/30/migrating-d3-force-layout-to-webassembly.html

- Rust
    A modern and popular language
    doesn't requrie a GC
    Originally used Emscripten, but moved to a simpler toolchain

    example
    CHIP-8
    https://blog.scottlogic.com/2017/12/13/chip8-emulator-webassembly-rust.html

    source maps
    https://hacks.mozilla.org/2018/01/oxidizing-source-maps-with-rust-and-webassembly/



Things to look at
Swift, Go + WebAssembly
Webpack4 supports WA Rust
WebAssembly starts to sneak into our daily workflow
Native node modules
Dedicated WASM UI Frameworks!
Rust, go, swift will start gaining web market share




https://blog.scottlogic.com/ceberhardt/
https://www.youtube.com/watch?v=3LWgbjVWLug
