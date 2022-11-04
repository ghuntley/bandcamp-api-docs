## Preface

This section covers available encoding types, how they're represented programmatically.

Just to note, while I am a small audiophile, I have no experience as a musician and have never uploaded files to Bandcamp. I do not know the process, therefore I do not know how files are sampled.

## Encoding Types

There are (as of the time of publishing) 8 available encoding formats from Bandcamp's download menu.

In ascending order of relative size:

| Encoding |           Full Name           | Open Source | Lossless | API Representation |
|:--------:|:-----------------------------:|:-----------:|:--------:|:------------------:|
|    AAC   |     Advanced Audio Coding     |      ❌      |     ✅    |      `aac-hi`      |
|    OGG   |           Ogg Vorbis          |      ✅      |     ❌    |      `vorbis`      |
|  MP3-V0  |                               |      ✅      |     ❌    |      `mp3-v0`      |
|  MP3 320 |                               |      ✅      |     ❌    |      `mp3-320`     |
|   FLAC   |   Free Lossless Audio Codec   |      ✅      |     ✅    |       `flac`       |
|   ALAC   |   Apple Lossless Audio Codec  |      ✅      |     ✅    |       `alac`       |
|    WAV   |   Waveform Audio File Format  |      ❌      |     ✅    |        `wav`       |
|   AIFF   | Audio Interchange File Format |      ❌      |     ✅    |   `aiff-lossless`  |

## Usage

"Consumer" use is a misnomer. It depends entirely on the preference of who's downloading the files.

A sane default setting would be MP3-V0, presuming it's encoded losslessly from the master file. Factoring in MP3's [Bit Reservoir](https://wiki.hydrogenaud.io/index.php?title=Bit_reservoir) quirks, you _**COULD**_ have a higher quality track than with MP3 320.