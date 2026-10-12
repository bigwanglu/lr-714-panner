# L+R 7.1.4 LIVE Panner v2.1

[Full English manual](guide.en.md) · [Full English PDF](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_Manual_EN.pdf)

[Chinese manual (PDF)](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_Manual_CN.pdf) · [Chinese manual (Word)](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_Manual_CN.docx)

## Installation & quick start

[English overview](../../README.en.md) · [中文完整手册](guide.zh-CN.md) · [Release notes](../releases/v2.1.md)

This guide covers v2.1, distributed as `LR_714_Panner_v2_1_0.zip` under Git tag `v2.1.0`. It is a Max for Live spatial panner for a **single input channel** and twelve discrete outputs. It is not an Atmos encoder, binaural renderer or automatic speaker-calibration system.

This version is provided as a pre-release. Test it at a low monitoring level in a copy of your set before relying on it in production or performance.

## 1. Setup and installation

Recommended setup: macOS, Ableton Live 12 Suite or Live with Max for Live, and an audio interface with at least twelve available physical outputs for full 7.1.4 monitoring. Enable output pairs 1/2–11/12 in Live's **Audio → Output Config** and connect the corresponding speakers.

The development machine had macOS 15.4.1 on Apple Silicon, Live 12 Suite 12.4.6 and bundled Max 9.1.5 installed. These are reference environment details, not a claim that this exact final release has passed full runtime testing. Windows and other DAWs have not been verified.

1. [Download the device package](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_0.zip). Do not use GitHub's automatic “Source code” ZIP as the installer.
2. Unzip it and keep the entire `LR_714_Panner_v2_1_0` folder together. The device loads companion JavaScript and Max patch files; copying only the `.amxd` can leave controls or scripts missing.
3. You can place this folder in your User Library under `Presets/Audio Effects/Max Audio Effect`, or drag `LR_714_Panner_v2_1_0.amxd` directly from the extracted folder onto a regular Audio Track.
4. Set that track's **Audio To to Sends Only**. The device has its own twelve-output path; leaving the normal main output active can produce duplicate output and misleading levels.
5. Start with your hardware monitoring level lowered. Use a single-channel source for the first check. The device currently processes the first input channel only; it does not sum a stereo pair to mono.

Keep v1.3.1 and v2.1 in separate folders. Save a copy of existing sets before upgrading; seamless migration of old sets, presets and automation is unverified.

## 2. Check routing before listening

The six ROUTING rows select pairs of twelve **mono** outputs. PAIR identifies the device's internal pair, TYPE normally selects **Ext. Out**, and CH selects the actual output pair offered by Live and your interface.

| Internal pair | First output | Second output |
|---|---|---|
| 1/2 | L — front left | R — front right |
| 3/4 | C — front center | LFE |
| 5/6 | Ls — side left | Rs — side right |
| 7/8 | Lrs — rear left | Rrs — rear right |
| 9/10 | Ltf — top front left | Rtf — top front right |
| 11/12 | Ltr — top rear left | Rtr — top rear right |

The device attempts to select Ext. Out and sequential pairs during initialization. Check the results against your wiring every time you use a new setup. If selection fails, set TYPE and CH manually. If only 1/2 is available, check the interface connection and Live's Output Config.

For a test tone, pause the source audio, keep monitoring low, enable **TEST**, and raise **VOL** cautiously from a low value. TEST does not mute the source. HZ at its midpoint corresponds to 1 kHz. Move X, Y and Z while checking meters and speakers. Turn TEST off afterwards. The meters show the device signal before hardware; they cannot confirm that a speaker is connected or working.

LFE feeds output 4 independently. It has no built-in low-pass filter or bass-management crossover, so check downstream filtering and routing before increasing the send.

## 3. Manual panning

Keep Motion OFF. Drag inside the XY pad to position the source, or use X and Y. Drag the height strip or use Z for elevation.

| Control | Range | Meaning |
|---|---|---|
| X | −1 to +1 | Left to right |
| Y | −1 to +1 | Rear to front |
| Z | 0 to 1 | Lower layer to height layer |
| Spread | 0–100 | Broadens spatial distribution |
| Focus | 0–100 | Higher values concentrate the image |
| LFE | 0–1 | Independent send to output 4 |

Spread and Focus default to 50; X, Y, Z and LFE default to 0. These six controls expose Live parameters for the existing automation and MIDI-mapping workflow. There is no public Width control.

## 4. Your first moving trajectory

1. Open **MOTION / EDIT**. Its yellow color identifies the window button, not the running state.
2. Choose **Circle**. Selecting a shape starts Motion. The main ON/OFF switch and PLAY / PAUSE control the same running state.
3. Select **FREE** and enter `8` in TIME (SECONDS): one full orbit takes a nominal eight seconds.
4. Choose **Fixed** height and set HEIGHT to 25%. Motion's default height is 25%, although the main device initially loads with Z at 0.
5. Watch the XYZ / 3D monitor, then check the actual outputs at a low level. Reduce SIZE for a smaller orbit, or choose REVERSE for the opposite XY direction.

PAUSE holds the current position and phase while audio continues. RESET sets phase to the start without deleting the trajectory. When paused, press PLAY to send that start position to the audio path. Manually changing XYZ stops Motion; press PLAY or ON to resume it.

## 5. Shape, draw and add height

The top row provides Circle, Figure 8, L/R, Front/Back, Random Lines and Random Points. **More** opens the full set of 36 shapes.

For fixed shapes, drag hollow nodes to edit the contour and white corner handles to change width and height. Drag elsewhere inside the plot to move the shape. Reduce SIZE first if a full-size shape has little room to move. SIZE changes trajectory scale, not speed, Spread or Focus. Edited geometry is retained when you select that shape again; selecting Circle again is not a factory reset.

Choose **Draw 1-8**, drag and release to make one stroke, then add up to eight strokes in total. Each stroke needs some movement; a click alone is not a stroke. A cycle traverses all strokes, with time distributed by their length and direct jumps between them. Random and hand-drawn modes do not expose the fixed-shape node and corner handles.

Height is independent of XY:

- **Fixed:** a constant height.
- **Up/Down:** a smooth oscillation around 50% height; RANGE sets its extent.
- **Rise/Fall:** a smooth rise and return, starting from 10% height.
- **Random:** a smoothly connected random height curve; click it again to generate another.
- **Draw:** edit height across the cycle directly. The horizontal axis is time through the cycle; the vertical axis is height. The HEIGHT / RANGE slider is hidden in this mode.

REVERSE changes XY traversal only; it does not reverse height with it. There are no Undo, delete-stroke, clear-canvas or factory-geometry-reset buttons. RESET does not clear strokes, and changing shapes preserves them.

## 6. Free and synchronized timing

**FREE:** TIME (SECONDS) is the duration of the entire cycle, from 0.01 to 300 seconds. Smaller values mean faster motion. Free does not require Live's transport to play. If mouse dragging stops at 0.1 seconds, enter 0.01 directly.

**SYNC:** choose LENGTH, then RHYTHM. Available lengths are 1/64, 1/32, 1/16, 1/8, 1/4 and 1/2 notes, 1–16 Bars, 64 Bars and Custom Bars. Straight uses the selected duration; Dotted multiplies it by 1.5; Triplet multiplies it by 2/3. Bar durations follow the set's time signature. Custom Bars accepts finite positive values, including fractions; extreme values have not been validated.

Sync needs Live's transport to be playing and the host connection to be ready. If it does not move, check transport, Motion ON and the waiting/reconnecting status. Press RESET to establish a new phase start relative to the current song position. There is no automatic restart-from-zero every time Live's transport starts.

Timing uses Max task scheduling, not sample-accurate audio scheduling. Audio gains retain 80 ms smoothing. A 0.01-second setting does not guarantee precisely audible 100-cycle-per-second movement.

## 7. Saving and automation

Motion has a device-state save/restore mechanism for shape edits, strokes, height and timing. It is designed to restore at phase 0 with Motion OFF. Full Live save/close/reopen testing is still incomplete; confirm recall in your own set before depending on it.

The six main controls expose Live parameters; Motion On is also a public parameter. Do not assume every Motion button, menu or slider can be mapped directly. Motion-generated coordinates have not been verified as automatically recordable or bakeable XYZ automation. XYZ automation may take over position and stop Motion, just as manual adjustments do.

## 8. Troubleshooting and current limits

- **Blank drawing or script errors:** keep the device and all companion files together, then reload.
- **Meters move but speakers do not:** check TYPE/CH, enabled Live outputs, interface routing and wiring.
- **Sound also reaches Main:** verify Audio To = Sends Only.
- **Motion stops after a manual change:** manual XYZ takes priority; resume with PLAY/ON.
- **Sync does not move:** start Live's transport and check host-connection status.
- **A shape is still edited after reselecting it:** stored geometry is retained; there is no public geometry-reset command.
- **No height slider in Draw:** the drawn curve controls Z directly.

Testing remains incomplete for real Live audio and repeated loading, Sync seeking/looping/time-signature changes, multiple instances, save/reopen, automatic routing on other interfaces, window-on-top behavior and trajectory-to-speaker listening checks. Existing model and selected native Max checks do not replace these tests.

See the [release notes](../releases/v2.1.md) for scope. When [reporting a problem](https://github.com/bigwanglu/lr-714-panner/issues), include the device, Live, Max and OS versions, audio interface, relevant routing and exact steps. Do not attach private audio or an entire personal project.
