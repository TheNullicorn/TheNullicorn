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

## March

***TODO***

## April

***TODO***

## May

***TODO***

### May 31st

Got some rotatable [monitor arms](https://amzn.com/dp/B07T5SY43L)! I'm liking how portrait-mode feels for IntelliJ, and I've even set up some keybind [scripts](http://noeld.com/programs.asp#display) to rotate each screen. Overall, 10 out of 10, would rotate again.

## June

### June 1st ⇒ June 5th (6 days)

Got my motherboard bricked by enabling a misdocumented feature in BIOS. It's off to MSI for repair, and I'm hoping for the best. In the meantime, I've moved my SSD over to my brother's PC, so I'll have to adjust to the new setup.

### June 6th ⇒ June 7th (2 days)

My bearded dragon's tail got an infection at the tip, so he had to go to the vet to get that part amputated. Besides sleepiness from the anesthesia, he acts like nothing even happened, and he's still a crazy goofball! Getting him to take his medicine is the only tricky part, aside from making sure he goes easy on his tail.

Oh yeah, and everything smells like Canada on fire...

### June 8th ⇒ June 15th (8 days)

Back to ribt! I'm starting a new module (and possibly the last one!) for [kotlinx-serialization](https://github.com/Kotlin/kotlinx.serialization) interop. I'm pretty sure the first iteration of ribt from 2022 started with this same premise, so I guess I've come full circle!

I also just got [Rain World](https://rainworldgame.com), and I love the art style so much!!!!

### June 16th ⇒ June 20th (5 days)

The two Windows installations in my PC right now—mine and my brother's—got into a fight and died spectacularly...

Long story short, my EFI & recovery partitions got borked somehow, and my brother's Windows installation had created a dependency on those partitions in MY SSD for some reason, so his began failing as well. Manually rebuilding those partitions didn't appear to make any difference, so we just grabbed our important files off via a laptop and wiped both drives.

Over the course of many, many Windows re-installations, we kept finding that the disks would become dependent on one another, sometimes even to the installation USB. After a few days we finally got each one properly installed by "tactically" unplugging/replugging devices between reboots to keep installers from detecting and becoming dependent on one another.

...I- I'm not crying, YOU'RE crying!...🥲
