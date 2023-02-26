# Activity Log 🖍

Hi! I'm keeping a little log here of what I've been up to throughout 2023, mostly just for my own curiosity.

## January

### January 1st ⇒ January 8th (8 days)

Implemented `NbtDeflaterSink` for my (kinda?) new NBT library, "ribt". The class is responsible for compressing encoded NBT data in either gzip or zlib, but also needs to be implemented for JVM, JavaScript, and native platforms.

Most interesting was implementing it on native platforms, where I got to use Kotlin's C interop features for the first time to interface with zlib.
I also got a bit familiar with C-style pointers and memory management, namely having to allocate & deallocate space for a `z_stream`.

Implementing the class's behaviour uniformly across all platforms was also a fun challenge, especially since the underlying tools are so different:
- bare zlib for Native
- pako for JavaScript
- `java.util.zip.Deflater` for JVM

### January 9th ⇒ February 1st (22 days)

Wrapped up the encoder/sink part of ribt. Most of the time was spent writing tests and documentations, but I also did a bit of iterating on the API for it until it was something I'd be comfortable using. Finally, I made it official by [merging](https://github.com/TheNullicorn/ribt/pull/22) `feature/outputs` into `dev`. I'll still be making little tweaks to it now on `dev`, along with future additions, but for now I'm happy with where it's at!

## February

### February 2nd ⇒ February 8th (6 days)

Began drafting & fleshing out the decoder/source part of ribt. The goal is for it to intuitively mirror the encoder/sink API, though there are some slight differences because decoding needs to account for ambiguities and issues in the data it's reading.

So far I've got the `NbtDecoder` interface and `NbtByteArraySource` class, but now I've got to delve back into zlib/pako to work on the `NbtDecompressionSource`...

### February 9th ⇒ February 17th (8 days)

Planning, drafting, & iterating on `NbtDecompressionSource`'s API & implementation(s). The tricky part is trying to create an abstraction that can neatly and performantly be implemented using zlib, `java.util.Deflater` and pako, all separately:
- Pako's API is callback-based, meaning you `push` data to its `Inflater` and whenever it feels like it, it'll send more decompressed bytes through the `onData` callback.
- On the other hand, `zlib`/`Deflater` are much more hands-on, making the caller provide input & output buffers and decompress progressively through them until the whole input is consumed *and* a full output is produced.

I don't mind either, but trying to fit them both under an `expect`/`actual` class is a bit tough.

### February 18th ⇒ February 21st (3 days)

Went to a family wedding! I did manage to sneak in a little work on the decompressor while we were at a hotel though.

### February 22nd ⇒ February 26th (4 days)

Got distracted on a mini web-app project, a 3D banner editor for Minecraft:
- SvelteKit for the UI and server-side rendering
- TypeScript for the app logic
- [Babylon.js](https://babylonjs.com) for rendering & scene-building
- [Enigma](https://github.com/FabricMC/Enigma) to decompile Minecraft's banner rendering code (for visual accuracy)

I got into it when I noticed that [Miners Need Cool Shoes](https://minersneedcoolshoes.com) seems to have been discontinued, and I noticed *that* because I was thinking about how on [hypixel.net](https://hypixel.net), you used to be able to customize your guild's banner, either through their own editor (which no longer exists) or by importing one from MNCS.

I also just haven't worked on anything web-related in (what feels like) ages, and I've been meaning to play around with Svelte. It might go nowhere since I really want to focus on ribt anyway, but maybe it's one of those things I'll come back to someday and give it some love 💖.
