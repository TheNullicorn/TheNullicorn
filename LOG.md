# Activity Log 🖍

Hi! I'm keeping a little log here of what I've been up to throughout 2023, mostly just for my own curiosity.

## January

### 1 - 8

Implemented `NbtDeflaterSink` for my (kinda?) new NBT library, "ribt". The class is responsible for compressing encoded NBT data in either gzip or zlib, but also needs to be implemented for JVM, JavaScript, and native platforms.

Most interesting was implementing it on native platforms, where I got to use Kotlin's C interop features for the first time to interface with zlib.
I also got a bit familiar with C-style pointers and memory management, namely having to allocate & deallocate space for a `z_stream`.

Implementing the class's behaviour uniformly across all platforms was also a fun challenge, especially since the underlying tools are so different:
- bare zlib for Native
- pako for JavaScript
- `java.util.zip.Deflater` for JVM
