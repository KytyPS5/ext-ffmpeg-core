## FFmpeg builtins

This repository builds static FFmpeg libraries for KytyPS5. It is based on
[shadPS4's FFmpeg core](https://github.com/shadps4-emu/ext-ffmpeg-core), originally
from [Vita3K](https://github.com/Vita3K/ffmpeg-core).

The Windows version is built using clang-cl, this is done so that inline assembly optimisations (which are not supported by MSVC) can be enabled.

VP8, VP9, Opus and Vorbis decoding and the Matroska/WebM demuxer are enabled.
No external codec libraries or GPL/nonfree components are enabled. Linux CI checks
decoder availability and decodes generated VP9/Opus and VP8/Vorbis test videos.
