[GGPK Browser](https://www.ggpk.exposed) consists of the following components:

[ggpk-server](https://github.com/ggpk-exposed/ggpk-index-server) (ggpk-index.onrender.com) - a searchable index of all PoE1 and PoE2 game files. Axum server deployable as a docker image.  
[unoodler](https://github.com/ggpk-exposed/unoodler) (unoodler.lvlvlvllvlvlvl.workers.dev) - extracts individual blocks of raw data from bundle files. Cloudflare worker written in rust.  
[ggpker](https://github.com/ggpk-exposed/ggpker) (ggpk.exposed) - file server that fetches file details from the index server and uses that to identify which raw blocks to fetch, slice and concatenate to produce requested files. Cloudflare worker written in typescript.  
[unddser](https://github.com/ggpk-exposed/unddser) (image.ggpk.exposed) - image conversion service. Cloudflare worker, currently using a fork of image-rs as the pull request (https://github.com/image-rs/image/pull/2258) adding support for required DX10 image formats has not been merged yet.  
[exposer](https://github.com/ggpk-exposed/exposer) (www.ggpk.exposed) - web frontend using [vuefinder file browser](https://github.com/n1crack/vuefinder). SPA that calls apis served by ggpker.  

![visual representation](https://github.com/user-attachments/assets/e0c954fb-8d20-4da9-a604-88b518541968)

The bundle scheme is detailed [here](https://github.com/poe-tool-dev/ggpk.discussion/wiki/Bundle-scheme), but a high-level overview is that individual game files are contained within bundles, which contain blocks of data compressed with [oodle](https://www.radgametools.com/oodle.htm). Bundles do not contain information about their own contents, instead all file entries are listed in a single bundle named `_.index.bin`, which also lists the names of all other bundle files, and the location of each file within a bundle as a byte offset and size.

PoE1 has about 1 million files, with an _.index.bin of around 20Mb, while PoE2 has closer to 4 million files indexed a file of almost 100Mb.

Note that the 'ggpk' in GGPK Browser is metonymy - ggpk refers to the 'Content.ggpk' game file distributed with the client, while this project sources data from Grinding Gear Games' CDN, which serves bundles individually rather than as a monolithic ggpk.
