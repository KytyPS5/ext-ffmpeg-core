## FFmpeg builtins

This repository builds static FFmpeg libraries for KytyPS5. It is based on
[shadPS4's FFmpeg core](https://github.com/shadps4-emu/ext-ffmpeg-core), originally
from [Vita3K](https://github.com/Vita3K/ffmpeg-core).

The Windows version is built using clang-cl, this is done so that inline assembly optimisations (which are not supported by MSVC) can be enabled.

VP8, VP9, Opus and Vorbis decoding and the Matroska/WebM demuxer are enabled.
No external codec libraries or GPL/nonfree components are enabled. Linux CI checks
decoder availability and decodes generated VP9/Opus and VP8/Vorbis test videos.

Each release includes libraries, their matching public headers, the LGPL notice,
build logs, and a corresponding source archive for every platform. The source
archives contain the patched FFmpeg sources, vcpkg port, build configuration and
the build recipe. The workflow pins vcpkg at
`df8bfe519564ae001903e5cdd32af0999531ef71` (FFmpeg 7.1.1).

To reproduce a build, check out the release commit and the pinned vcpkg revision
in `_vcpkg`, apply `ffmpeg.patch` there, bootstrap vcpkg, and install
`ffmpeg[core,avcodec,avfilter,avdevice,avformat,swresample,swscale]:<triplet>`
with `--overlay-triplets=./triplets`. See `.github/workflows/build.yml` for the
platform tools and triplets. `scripts/package.py` creates the release archives.
On Windows, set `KYTY_MSYS_ROOT` to an MSYS2 installation with automake, make,
diffutils and pkgconf, and include it in `VCPKG_KEEP_ENV_VARS`.

Applications distributing these static libraries must preserve the notices and
provide the corresponding source and build materials needed to rebuild and relink
with a modified FFmpeg. See `copyright` for the LGPL 2.1 terms.
