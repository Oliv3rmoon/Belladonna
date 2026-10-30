<h1 align="center">Belladonna</h1>

<p align="center">
  <strong>Nightshade's PS5 Vulkan driver: an open-source AMD Vulkan driver running on the PS5, with Nightshade's own fixes and diagnostics.</strong>
</p>

<p align="center">
  <a href="https://discord.gg/pSqgRU3YP9"><img src="https://img.shields.io/badge/discord-nightly-0d0d0f?style=for-the-badge&logo=discord&logoColor=e5484d" alt="Discord: nightly"></a>
  <a href="https://github.com/Oliv3rmoon/Belladonna/stargazers"><img src="https://img.shields.io/github/stars/Oliv3rmoon/Belladonna?style=for-the-badge&logo=github&logoColor=e5484d&color=e5484d&labelColor=0d0d0f" alt="GitHub stars"></a>
  <a href="docs/license.rst"><img src="https://img.shields.io/badge/license-MIT-0d0d0f?style=for-the-badge&labelColor=0d0d0f&color=e5484d" alt="MIT license"></a>
</p>

Belladonna, named after *Atropa belladonna*, the deadly nightshade, is the graphics driver behind **[Nightshade](https://github.com/Oliv3rmoon/Nightshade)** on the PS5: an open-source AMD Vulkan driver, forked, with a PS5 port underneath it that connects it to the console's GPU and its VideoOut display output. This branch, `nightshade`, is the default, and it adds what Nightshade needs on top, one commit each. Belladonna has no releases of its own: Nightshade builds it.

## Why Belladonna

What Nightshade adds, one commit each:

- **A display that starts and stops cleanly.** VideoOut follows Nightshade's app lifetime, so the app can close and start again cleanly, and the driver sees host memory.
- **Geometry shaders as compute, without the crash.** A draw the pass drops no longer hands it a null pointer.
- **A shader cache that survives.** The cache on disk stays on when the app's user ids differ after elevation, so compiled shaders survive between starts.
- **Long command streams split where they need to.** They may also be split before a transfer or a barrier.
- **A stall report that says why.** When the GPU stops making progress, `stderr.log` names:
  - the first wait it never got past;
  - the last draws and dispatches before it, with their sizes and, for indirect draws, their arguments;
  - the pipeline each shader belongs to.

## Use it

Nightshade builds Belladonna with the [PS5_Vulkan](https://github.com/mihawk-99/PS5_Vulkan) recipe. Its `PS5_MESA_FORK` points at this repository and `PS5_MESA_REVISION` at a commit on `nightshade`. See Nightshade's `tools/build-radv-dependencies.sh` and `tools/deps.json`.

## Docs

- **[PS5_PORT.md](PS5_PORT.md):** the PS5 port's own description, unchanged.
- **[README.rst](README.rst):** the README of the project this is forked from, and [its documentation](docs/index.rst).

## The Nightshade family

Belladonna is one of seven repositories in the Nightshade family, all by [Oliv3rmoon](https://github.com/Oliv3rmoon): the same black-and-red look, one Discord.

| App | What it is |
| --- | --- |
| [**Nightshade**](https://github.com/Oliv3rmoon/Nightshade) | The Switch emulator for PS5 homebrew |
| [**Physalis**](https://github.com/Oliv3rmoon/Physalis) | Live TV, movies and Plex on the PS5 |
| [**Datura**](https://github.com/Oliv3rmoon/Datura) | Game streaming from your PC to the PS5 |
| [**Mandrake**](https://github.com/Oliv3rmoon/Mandrake) | PS1 emulation, with two emulators |
| [**Dulcamara**](https://github.com/Oliv3rmoon/Dulcamara) | RPG Maker 2000 and 2003 games, and Ren'Py visual novels |
| [**Solanum**](https://github.com/Oliv3rmoon/Solanum) | A store for open-source PS5 homebrew, with its catalog [on the web](https://oliv3rmoon.github.io/Solanum-Catalog/) |
| **Belladonna** (this repo) | Nightshade's PS5 Vulkan driver |

## Built on

[PS5_Mesa](https://github.com/mihawk-99/PS5_Mesa) by Mihawk, a PS5 port of [Mesa](https://www.mesa3d.org)'s RADV. RADV and its ACO shader compiler do almost all of the work, and the port connects them to the PS5's GPU and its VideoOut display output. Belladonna's commits sit on top of Mihawk's `1ba9874` (Mesa 26.2.0).

## Credits and license

- **Mesa and RADV:** the Mesa project (MIT; see `docs/license.rst`).
- **PS5 port** (`src/amd/vulkan/winsys/ps5`, `src/vulkan/wsi/wsi_common_videoout.c`): Mihawk (MIT).
- **Nightshade's changes:** Oliv3rmoon (MIT, like the files they change).

## Help it grow

Like Belladonna? **[Star it](https://github.com/Oliv3rmoon/Belladonna)** and **[join the Discord](https://discord.gg/pSqgRU3YP9)**.
