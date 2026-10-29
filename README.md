# Belladonna

**Belladonna is Nightshade's PS5 Vulkan driver**, named after *Atropa belladonna*, the deadly nightshade. It's Mesa's RADV, the open-source Vulkan driver for AMD GPUs, running on the PS5 through [Mihawk's PS5 port](https://github.com/mihawk-99/PS5_Mesa), plus Nightshade's own fixes and diagnostics.

Belladonna is a fork. Mesa's RADV and its ACO shader compiler do almost all of the work, and Mihawk's port connects them to the PS5's GPU and its VideoOut display output. This branch, `nightshade`, adds what Nightshade needs on top. All of it is listed below, one commit each.

## What Nightshade adds

On top of Mihawk's `1ba9874` (Mesa 26.2.0):

- **Display lifetime:** VideoOut follows Nightshade's app lifetime, so the app can close and start again cleanly, and the driver sees host memory.
- **Geometry shaders as compute:** a draw the pass drops no longer hands it a null pointer.
- **Shader cache on disk** stays on when the app's user ids differ after elevation, so compiled shaders survive between starts.
- **Long command streams** may also be split before a transfer or a barrier.
- **Stall report:** when the GPU stops making progress, `stderr.log` names:
  - the first wait it never got past;
  - the last draws and dispatches before it, with their sizes and, for indirect draws, their arguments;
  - the pipeline each shader belongs to.

## Built by

Nightshade builds Belladonna with Mihawk's [PS5_Vulkan](https://github.com/mihawk-99/PS5_Vulkan) recipe. Its `PS5_MESA_FORK` points at this repository and `PS5_MESA_REVISION` at a commit on `nightshade`. See Nightshade's `tools/build-radv-dependencies.sh` and `tools/deps.json`.

## Credits and license

- **Mesa and RADV:** the Mesa project (MIT; see `docs/license.rst`).
- **PS5 port** (`src/amd/vulkan/winsys/ps5`, `src/vulkan/wsi/wsi_common_videoout.c`): Mihawk (MIT).
- **Nightshade's changes:** Oliv3rmoon (MIT, like the files they change).

Mihawk's description of the port, unchanged, is [PS5_PORT.md](PS5_PORT.md), and Mesa's own README is [README.rst](README.rst).
