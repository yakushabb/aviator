<div align="center">
<h1>Aviator</h1>

A Flatpak-first easy-to-use GUI for encoding with rav1e & libopus.

<img src="assets/aviator_splash2.avif" alt="Splash" width=450/>
<br>
<br>

[![Installs](https://img.shields.io/flathub/downloads/net.natesales.Aviator?style=for-the-badge)](https://flathub.org/apps/details/net.natesales.Aviator)
![Code Size](https://img.shields.io/github/languages/code-size/natesales/aviator?style=for-the-badge)
[![License](https://img.shields.io/github/license/natesales/q?style=for-the-badge)](https://raw.githubusercontent.com/natesales/q/main/LICENSE)

[![Please do not theme this app](https://stopthemingmy.app/badge.svg)](https://stopthemingmy.app)
</div>

## About

Aviator enables simple & easy video encoding for the word's most advanced open video codec, AV1. Encode your favorite media into super efficient files with incredible quality per bit, powered by the fast, memory-safe rav1e encoder with libopus for audio encoding. The sky's the limit for your old home video collection, large 4k smartphone videos, screen recordings, Blu-ray rips, you name it - take off with Aviator!

Aviator is designed to be a no frills, easy to use AV1 encoding GUI that any beginner can pick up and immediately understand how to use. 

## Installation

### Flathub

Aviator is available on Flathub. You can learn how to set up Flatpak on your distro of choice [here](https://flatpak.org/setup/).

<a href="https://flathub.org/apps/details/net.natesales.Aviator"><img width="200" alt="Download on Flathub" src="https://flathub.org/assets/badges/flathub-badge-en.png"/></a>

### Building from Source

Make sure you have all required dependencies before building from source. This includes `flatpak-builder`, `python3` & `gcc`

```bash
git clone https://github.com/natesales/aviator
cd aviator
make
```

Third party packaging formats are not officially supported by Aviator, and if you encounter bugs while using them please do not submit them as issues; we do not officially support third party packaged versions of Aviator.

## Why AV1?

AV1 aims to be more efficient than HEVC & VP9 by around 30%, and more efficient than h.264 by 50%. Traditionally, a lot of AV1 encoder implementations have been pretty slow compared to competing codecs' encoders, but the Rust-based rav1e encoder has seen decent increases in speed recently and is improving more every day. We decided to use rav1e in order to give users a memory-safe AV1 encoder implementation that prioritizes visual quality &amp; "just works," for the most part.

One downside of rav1e is that despite being generally quicker than the libaom AV1 reference encoder, it is quite a bit slower than the SVT-AV1 production encoder. To combat this while maintaining high visual quality, Aviator utilizes a tool called [Av1an](https://github.com/master-of-zen/Av1an) that is capable of detecting scene changes in a video & splitting the video into multiple shorter videos (chunks) based on those scene changes, then encoding these chunks in parallel. This works especially well with longer videos. Aviator will determine the number of chunks to use based on Av1an's internal chunk allocator, which calculates the number of chunks your system can handle based on your logical CPU cores & the amount of RAM you have available. Encoding speed scales with the number of chunks you have, so more chunks is faster but harder on your CPU & memory.

Aviator comes bundled with its own version of ffmpeg that is capable decoding videos to detect source information, upscaling & downscaling videos with a sharp scaling algorithm called lanczos, & encoding audio using the Opus audio codec via libopus.

## Aviator's Defaults

Hovering over most user configurable options in Aviator will produce a helpful tooltip that you can look at to make things more clear.

<img src="assets/aviator_vid.avif" alt="Aviator Video Settings" width=480/>

When you load a video file into Aviator, resolution & audio bitrate are set to match the source as closely as possible. Aviator's rav1e speed preset is set to 6 by default, with a Quantizer level of 80. You can set the Quantizer level from 1 to 255 using the slider, with larger numerical values indicating smaller filesize at the expense of visual quality. Speed 6 offers a good balance between speed & compression efficiency at any Quantizer level; higher values will encode faster at the expense of visual quality, while lower values will encode more efficiently but more slowly.

<img src="assets/aviator_audio.avif" alt="Aviator Audio Settings" width=480/>

Audio is reencoded even if the bitrate is set to be the same as the source audio. Audio is encoded to Opus, which is a highly efficient free audio codec that is often more efficient than competitors like AAC & MP3 audio. Because of Opus's incredible efficiency, audio tracks will be encoded at 48kbps if no source bitrate is detected. Opus reaches audio transparency at around 128kbps.

## Roadmap & Limitations

Currently, Aviator cannot handle:
- Video streams with subtitles encoded to .webm

These are considered bugs, and we are working on fixing them ASAP. In the meantime, we'd prefer you choose the .mkv container if you are having trouble with subtitles.

In the future, we would like to:
- Add a progress bar
- Add maximize & minimize buttons in the header bar
- Add a "Stop Encode," button
- Add a queue, potentially
- Revamp outputting a file
- Revamp the About page

Let us know if you have any issues in our Issues section. Thank you for using Aviator!

<img src="assets/aviator_output.avif" alt="Aviator Output UI" width=480/>

## Credits

Actively developed by [Nate Sales](https://github.com/natesales/) & [Gianni Rosato](https://github.com/gianni-rosato/)
