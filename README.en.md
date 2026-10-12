# L+R 7.1.4 LIVE Panner v2.1

[Chinese manual (PDF)](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_Manual_CN.pdf) · [Chinese manual (Word)](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_Manual_CN.docx)

Make the movement of sound part of your performance.

[中文](README.md) · English

[Download v2.1 (pre-release)](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_0.zip) · [Installation & quick start](docs/v2.1/guide.en.md) · [Versions](docs/versions.md)

L+R 7.1.4 LIVE Panner is a spatial panning tool for Ableton Live / Max for Live, designed by electronic musician L+R, Wang Lu, and currently available at no cost. It distributes a single input channel across twelve outputs in a 7.1.4 layout, putting horizontal position, height and movement directly into your hands.

The heart of v2.1 is a separate **Motion Editor**. Choose a trajectory, reshape it or draw your own, then let sound move at its own pace or with the music. Start with a slow ambient orbit, or build a back-and-forth movement around a musical phrase.

## Motion: shape how sound moves

- **36 trajectories:** circles, figure eights, left/right and front/back lines, polygons, petals, weaves and random movement. Edit nodes, stretch fixed shapes and reposition them.
- **Draw paths and height independently:** create up to 8 XY strokes, with fixed, oscillating, rising/falling, random or hand-drawn height.
- **Free / Sync:** set seconds per cycle, or follow Live using note values, bars, dotted timing and triplets.
- **Perform and observe:** play, pause, reverse and reset the start. The main XYZ / 3D monitor shows position, trajectory and a short trail. Manual XYZ changes take over and stop Motion.

Spread, Focus, LFE, X, Y and Z remain available alongside the test tone, twelve output meters and six routing pairs.

## Get started

The recommended setup is macOS with Ableton Live 12 Suite, or Live with Max for Live. Full 7.1.4 monitoring requires at least twelve available physical outputs and the corresponding speaker system.

1. Download the **device package** above and unzip it. Keep the entire `LR_714_Panner_v2_1_0` folder and its dependencies together. Do not copy only the `.amxd`. GitHub's automatically generated “Source code” ZIP is not the installer.
2. Lower your monitoring level. Load `LR_714_Panner_v2_1_0.amxd` on a regular Audio Track and set the track's **Audio To to Sends Only**.
3. Enable output pairs 1/2 through 11/12 in Live's Output Config. Check each ROUTING TYPE and CH against your actual wiring, even if they were selected automatically.
4. Check outputs at a low level, then turn TEST off. Open **MOTION / EDIT**, choose a shape, and set its cycle time and height. Selecting a shape starts Motion; Sync also requires Live's transport to be playing.
5. Try it in a copy of your set before using it in production or on stage. See the [quick-start guide](docs/v2.1/guide.en.md) for channel order, controls and troubleshooting.

The current device uses the first input channel; it does not automatically preserve or downmix a full stereo input. It provides discrete 7.1.4 speaker outputs, without Dolby Atmos encoding. Real Live audio, save/reopen and cross-interface testing are not yet complete. See the [release notes](docs/releases/v2.1.md).

## Documentation & feedback

- [English quick start](docs/v2.1/guide.en.md) / [完整中文手册](docs/v2.1/guide.zh-CN.md)
- [v2.1 changes and known limitations](docs/releases/v2.1.md)
- [All versions and v1.3.1 Public Beta downloads](docs/versions.md)
- [First-generation v1.3.1 Public Beta guide](docs/v1.3.1/README.md)
- [Report an issue or share a use case](https://github.com/bigwanglu/lr-714-panner/issues)

Please include the device, Live, Max and OS versions, your audio interface and steps to reproduce. Avoid sharing private audio or an entire personal project.

## A note from the author

![L+R, Wang Lu, wearing headphones while performing with tabletop electronic instruments](assets/images/artist-live.jpg)

I'm L+R, Wang Lu, an electronic musician. Many of the ideas in this plugin came from my own needs while mixing spatial audio and performing live over the years.

I spent a few months asking myself: what kind of tool do I actually want? Then I worked with AI to bring those ideas to life. I don't know how to code, but now we can start making tools that fit the way we work, and keep maintaining and developing them over time.

I hope you use it to create the spaces and movements you hear in your mind, and make your music sound better. If you have ideas, come and talk. Let's all get into it and have fun.

[Read the full author's note](docs/author/author-message.en.md)

L+R / Wang Lu · L+R SOUNDSYSTEM
