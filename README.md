[GGPK Browser](https://www.ggpk.exposed) consists of the following components:

[ggpk-server](https://github.com/ggpk-exposed/ggpk-index-server) - a searchable index of all PoE1 and PoE2 game files. Axum server deployable as a docker image.  
[unoodler](https://github.com/ggpk-exposed/unoodler) - extracts individual blocks of raw data from bundle files. Cloudflare worker written in rust.  
[ggpker](https://github.com/ggpk-exposed/ggpker) - file server that fetches file details from the index server and uses that to identify which raw blocks to fetch, slice and concatenate to produce requested files. Cloudflare worker written in typescript.  
[unddser](https://github.com/ggpk-exposed/unddser) - image conversion service. Cloudflare worker, currently using a fork of image-rs as the pull request (https://github.com/image-rs/image/pull/2258) adding support for required DX10 image formats has not been merged yet.  
[exposer](https://github.com/ggpk-exposed/exposer) - web frontend using [vuefinder file browser](https://github.com/n1crack/vuefinder). SPA that calls apis served by ggpker.  

![visual representation](https://github.com/user-attachments/assets/e0c954fb-8d20-4da9-a604-88b518541968)
