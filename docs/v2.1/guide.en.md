# L+R 7.1.4 LIVE Panner v2.1 Full User Guide and Release Notes

[Full English manual (PDF)](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_Manual_EN.pdf) · [Word edition](https://github.com/bigwanglu/lr-714-panner/releases/download/v2.1.0/LR_714_Panner_v2_1_Manual_EN.docx) · [English quick start](quick-start.en.md) · [中文完整手册](guide.zh-CN.md)

Device: LR_714_Panner_v2_1_0.amxd  
Document date: October 12, 2026

L+R 7.1.4 LIVE Panner is a spatial panning tool designed by electronic musician L+R / Wang Lu for 7.1.4 multichannel workflows in Ableton Live and Max for Live. It distributes a single sound source across twelve speaker outputs and brings planar position, height, spread, focus, and motion paths together in one device.

This guide starts with installation and getting sound, then explains the main panel, Motion Editor, preset shapes and freehand drawing, height, Free and Sync timing, saving, and automation. New users should read Sections 1 through 4 in order. Experienced users can go directly to Sections 5 through 11. Version changes, operating limitations, and the scope of verification are covered in Sections 13 and 14. A separate note from the author appears at the end.

## Contents

- [1 Before you begin](#1-before-you-begin)
- [2 Installation and loading](#2-installation-and-loading)
- [3 Signal routing and channel checks](#3-signal-routing-and-channel-checks)
- [4 Your first Motion session](#4-your-first-motion-session)
- [5 Main panel controls](#5-main-panel-controls)
- [6 How Motion Editor works](#6-how-motion-editor-works)
- [7 Planar shapes and geometry editing](#7-planar-shapes-and-geometry-editing)
- [8 Drawing planar paths](#8-drawing-planar-paths)
- [9 Height curves](#9-height-curves)
- [10 Free and Sync timing](#10-free-and-sync-timing)
- [11 Saving presets and automation](#11-saving-presets-and-automation)
- [12 Examples and troubleshooting](#12-examples-and-troubleshooting)
- [13 Release notes](#13-release-notes)
- [14 Limitations and verification scope](#14-limitations-and-verification-scope)
- [A note from the author](#a-note-from-the-author)

## 1 Before you begin

### Software and hardware

The recommended starting environment is macOS with Ableton Live 12 Suite, or another Live edition with Max for Live. The device loads through Max for Live. Regular users do not need to install Node or run Python build scripts.

A complete 7.1.4 speaker monitoring setup requires twelve available physical outputs, with the corresponding speakers and cabling. Select the intended audio interface in Live's Audio settings, then enable the six output pairs 1/2, 3/4, 5/6, 7/8, 9/10, and 11/12 in Output Config. A channel appearing in a menu does not confirm that its speaker is correctly connected.

The recommended setup should not be confused with a minimum compatibility specification. This release does not guarantee compatibility across all operating systems, processor architectures, or historical Live versions. See Section 14 for the recorded software environment and completed checks.

### Prepare a single-source input

The current device audio chain uses the first input channel. It does not have a complete left-plus-right stereo downmix chain, so you should not assume that all content from both sides of an arbitrary stereo track will reach the spatial outputs.

For your first session, prepare a suitable single-source signal upstream of the device and confirm that the first input channel contains audio. If important material exists only in the right channel, check the input arrangement before treating the problem as a routing fault. The device's twelve outputs distribute the sound source among the speakers.

### LFE is an independent send

LFE controls the send level to output 4 and defaults to 0. There is no evidence that the current signal chain automatically extracts low frequencies first or performs complete crossover processing or bass management. Raising LFE should not be understood as raising only the low-frequency content. Confirm the processing and wiring of the downstream low-frequency system before increasing it gradually.

### Lower the monitoring level first

Before testing, lower the hardware monitoring level, stop unnecessary upstream sound sources, and confirm that TEST is off. Routing changes, the test tone, and motion can immediately change the outputs. Verify channel assignments before raising the monitoring level.

Motion PAUSE and the main panel OFF control stop position movement only. They do not mute the twelve audio outputs. To stop the sound, stop the source or use the appropriate volume control.

## 2 Installation and loading

### Keep the complete folder

After extracting the plugin release package, keep the LR_714_Panner_v2_1_0 folder intact. The file you load is LR_714_Panner_v2_1_0.amxd. Do not move only the AMXD file elsewhere: Motion, routing, displays, and other functions depend on companion files in the same folder.

If downloading from GitHub, choose the provided plugin installation package. GitHub's automatically generated Source code ZIP serves a different purpose from the plugin installation package. They are not interchangeable simply because both have a ZIP extension.

Place the complete folder in Presets/Audio Effects/Max Audio Effect inside your Ableton User Library so it is easy to find in Live's browser. Check Live's Library settings for the actual User Library location. Alternatively, leave the folder structure intact and drag the AMXD from Finder into Live.

### Start on a regular audio track

1. Prepare a regular Audio Track in Live and feed it a single-source test signal.
2. Double-click the device or drag LR_714_Panner_v2_1_0.amxd into the track's device area.
3. Set the track's Audio To to Sends Only.
4. Check all six rows of ROUTING on the right.
5. At a low monitoring level, perform the channel-by-channel checks in Section 3.

A regular Audio Track is recommended for the initial setup because it makes the source and signal destination clear. Complete this basic setup before incorporating the device into a more complex performance set.

**Why use Sends Only:** The device sends its twelve internal outputs directly to the selected destinations. If the track also feeds Main, the main output and device direct outputs may overlap, making levels and panning harder to assess.

### Required runtime dependencies

The current device directly references the following twelve files. Keep them with the device. The complete release folder may also contain documentation, a matching maxpat file, and verification records. There is no need to break up the folder to make it smaller.

- LR714RoutingPanel_alpha15r2.maxpat
- LR714RoutingObjects_alpha15r2.maxpat
- lr_714_routing_defaults_alpha15r2.js
- lr_714_gains_comfy.js
- lr_714_pad_avenir_bigger.js
- lr_714_meter_avenir.js
- lr_714_testfreq.js
- lr_logo.js
- lr_714_motion_ui.js
- lr_714_motion_model.js
- lr_714_motion_monitor.js
- lr_714_object_mark.js

If parts of the interface are missing, Motion does not work, or a missing-file message appears after loading, first check that these files remain in the complete folder, then reload the device.

## 3 Signal routing and channel checks

### The signal path

After the source enters the device's first input channel, position, Spread, Focus, LFE, and related controls determine the channel gains before the signal reaches the twelve outputs. The six ROUTING rows on the right assign these outputs in pairs to the actual destinations offered by Live. The audio interface then sends them to the speakers.

The device's twelve meters sit after gain processing and before the hardware outputs. They help confirm that signal is present inside the device. They do not confirm speaker connections, amplifier power, or the sound pressure level in the room.

### Six routing rows carry twelve signals

PAIR identifies a fixed internal output pair. TYPE selects the output type, and CH selects the actual audio-interface output pair. TYPE is normally Ext. Out. The available CH entries depend on the host, audio interface, and Output Config.

| PAIR and default CH | First channel | Second channel | Internal numbers |
|---|---|---|---|
| 1/2 | L front left | R front right | 1, 2 |
| 3/4 | C front center | LFE low-frequency send | 3, 4 |
| 5/6 | Ls side left | Rs side right | 5, 6 |
| 7/8 | Lrs rear left | Rrs rear right | 7, 8 |
| 9/10 | Ltf top front left | Rtf top front right | 9, 10 |
| 11/12 | Ltr top rear left | Rtr top rear right | 11, 12 |

This pairing belongs to the current device and host routing design. The channel names in the table always refer to the device's internal order. Adjust CH to match the actual venue wiring; you do not have to rewire all hardware to match the default numbers.

### Automatic initialization and manual changes

The device has default routing initialization logic that attempts to select Ext. Out and assign the six rows to 1/2 through 11/12 in order. Initialization waits until the device path and output menus are ready. If a target channel is missing, it continues waiting rather than treating an unavailable output as connected.

After automatic initialization completes, it does not keep overwriting your manual choices. For a different wiring arrangement, change TYPE and CH row by row and verify the actual speaker assignments. Recheck all six routing rows after changing the audio interface, driver, or Output Config.

If the defaults are not selected automatically, check the hardware and Output Config first. Then manually set each row's TYPE to Ext. Out and CH to the required output pair. One correct row does not mean the other five are also correct.

### Checking with TEST

TEST provides a built-in sine-wave test tone. VOL controls its level, and HZ controls its frequency. VOL is not the master volume of the whole track.

1. Pause the original source so each output is easier to identify. Enabling TEST does not mute the original source automatically; both may enter the device at the same time.
2. Lower VOL before enabling TEST, then raise it slowly to a safe, clearly audible level.
3. The HZ midpoint of 50 corresponds to 1000 Hz. The frequency control displays a normalized value from 0 to 100, not a direct reading in hertz.
4. Keep Motion OFF. Change X, Y, and Z while observing the device meters and listening to the actual speakers.
5. Check the lower-layer and overhead output pairs in turn. Test LFE separately by raising it slightly from 0, within the safe operating conditions of your low-frequency system.
6. Turn TEST off when finished, then resume the original source.

Position-based distribution may use several speakers at once. Assess the coordinates, Spread, Focus, and meters together rather than assuming that each position activates only one speaker.

## 4 Your first Motion session

Once routing is confirmed, use this short sequence to learn automatic movement. Keep the monitoring level low throughout.

1. Click the yellow MOTION / EDIT area on the main panel to open Motion Editor. The yellow entry point means the window can be opened; it does not indicate that Motion is running.
2. Click Circle. Selecting a shape starts Motion immediately. Click PAUSE if you want to configure it first.
3. Select FREE and enter 8 in TIME (SECONDS), giving one complete cycle a duration of eight seconds.
4. Select Fixed height and set HEIGHT to 0% to keep this check on the lower layer.
5. Click PLAY and observe the main panel XYZ / 3D view and twelve meters.
6. Click FORWARD / REVERSE to change the planar travel direction. Click PAUSE or the main panel OFF control to stop movement.
7. To restart from the beginning of the path, pause, click RESET, then click PLAY.

The main panel Z value starts at 0, while Motion's default Fixed height is 25%. Starting the default Motion setup for the first time may therefore change Z to 0.25. Setting height to 0% in the sequence above makes the first channel check easier to interpret.

## 5 Main panel controls

### Layout and spatial orientation

From left to right, the main panel contains branding and TEST, the Motion entry point, XY/Z positioning, the XYZ / 3D monitor, six SHAPE/SPACE main controls, twelve meters, and ROUTING. The current layout is a low-profile horizontal panel measuring 1226 × 169.

On the plane, X=-1 is left and X=+1 is right; Y=+1 is front and Y=-1 is rear. Z=0 corresponds to the lower layer and Z=1 to the height layer. The top of the planar view means front, not physical Z height.

### The six main controls

| Control | Range | Initial value | Function |
|---|---|---|---|
| Spread | 0–100 | 50 | Changes the spread of spatial distribution; higher values widen distribution around the source |
| Focus | 0–100 | 50 | Changes focus; higher values concentrate the distribution and shrink the yellow coverage circle |
| LFE | 0–1 | 0 | Controls the independent send level to output 4 |
| X | -1–1 | 0 | Left/right position: negative left, positive right |
| Y | -1–1 | 0 | Front/rear position: negative rear, positive front |
| Z | 0–1 | 0 | Height: 0 is the lower layer, 1 is the height layer |

Spread and Focus both affect spatial distribution, but they are different parameters. Hold the source position fixed, change one control at a time, and judge the result through your actual monitoring system. Neither changes the Motion cycle duration, and neither is equivalent to path SIZE.

All six main controls use Live's parameter system and support the existing automation and MIDI-mapping workflow. While Motion is running, manually changing X, Y, or Z takes over position control and stops Motion. X, Y, or Z automation may trigger the same takeover through the parameter chain. Treat Spread, Focus, and LFE according to their own purposes; not every control is a motion start/stop switch.

### Dragging XY and height

Click or drag inside the main XY square to move the panning center. Center snapping is enabled by default, with a threshold of 0.06 to help return to the center when nearby.

Drag vertically in the height area outside the XY square to change Z: higher on screen means greater height, and lower means less height. The X, Y, and Z controls provide numeric control of the same position.

The yellow coverage circle shows the Focus range. The white L+R mark scales with the radius of that circle. The yellow circle's opacity changes with height, while the white mark remains visible. The branding is an interface element; use the coordinates, path, and actual monitoring to assess position and movement.

### Test-tone parameters

| Control | Range | Default | Mapping |
|---|---|---|---|
| TEST | Off / On | Off | Turns the built-in sine-wave test tone off or on |
| VOL | 0–100 | 50 | Linear mapping to 0–1; 0 is silent and 100 is full scale in the test-tone chain |
| HZ | 0–100 | 50 | 0 → 20 Hz; 50 → 1000 Hz; 100 → 20 kHz |

HZ uses a piecewise exponential mapping. Its midpoint is not the arithmetic mean of 20 Hz and 20000 Hz. VOL affects only the test tone; the original source retains its own volume controls.

### Motion switching and read-only monitoring

MOTION / EDIT opens the separate editor window. Loading the device does not open this window automatically. The main panel OFF / ON control runs or stops the existing path. It defaults to OFF and is exposed as the Motion On parameter.

XYZ / 3D shows the current manual or Motion position, the planned path, and a short recent trail. The monitor area measures 188 × 164, retains up to 160 history points, and displays coordinate values to one decimal place. This is read-only feedback: you cannot drag the ball in this view to edit the path, and there is no data-export button.

The twelve meters show the post-gain signals and decaying peak levels, with displayed values limited to 0–1. They do not measure the audio interface's output terminals or room sound pressure.

## 6 How Motion Editor works

### What makes up a cycle

Motion links a planar path, height changes, and timing. The XY path determines horizontal position; the Z curve determines height at each point in the cycle; Free or Sync determines the duration of a complete cycle. Independent height editing means that you can design the Z curve separately. It still uses the same cycle phase.

The window is designed at 760 × 550. Select a shape at the top, edit the planar path in the middle, and design height and set timing and playback at the bottom. There is no additional Speed or Rate slider. Speed is controlled by the cycle duration or synchronized note/bar length.

### Default state of a new instance

| Item | Default |
|---|---|
| Shape | Circle |
| SIZE | 100% |
| Motion | OFF |
| Direction and phase | Forward, phase 0 |
| Translation offset | X=0, Y=0 |
| Free cycle | 4 seconds |
| Sync | Off, with 1 Bar as the stored length setting |
| RHYTHM | Straight |
| Height mode | Fixed |
| HEIGHT | 25%, corresponding to Z=0.25 |

These are the model defaults for a new instance. When loading a saved device or set, some settings come from the saved content. Restoring state leaves Motion stopped by default; see Section 11.

### What happens when you select a shape

The top shortcuts are Circle, Figure 8, L/R, Front/Back, Random Lines, Random Points, More, and Draw 1-8. SHAPES / ALL 36 under More contains the complete set of 36 presets. This total already includes the shortcut shapes.

Selecting a shape adopts its path, resets phase and the overall translation offset to zero, and starts Motion. An unedited preset returns to SIZE=100%; a shape whose geometry has been edited uses its own saved edits. In Sync mode, movement also requires Live to be playing and the synchronization connection to be ready.

Switching the XY shape does not reset the height curve. After changing shapes, also check what Z is doing, so an existing height variation is not mistaken for a property of the new shape.

### Playback and manual takeover

PLAY begins outputting path coordinates, and the button becomes yellow PAUSE. PAUSE stops position updates while retaining the path and current phase. The main panel ON/OFF state stays in sync with this playback state. When paused, audio continues to be distributed at the last position.

Operating the main XY/Z area or changing X, Y, or Z parameters takes over manually and stops Motion. To resume, press PLAY or the main panel ON control. Check the current timing mode first: Free does not depend on Live playback; Sync also requires host playback and a valid connection.

### Reverse and starting-point reset

FORWARD / REVERSE changes the direction in which the XY path is traversed. The button is highlighted when reversed. The current implementation reverses planar path sampling, while height is still calculated from cycle phase. It does not play the complete XYZ movement, including height, backward.

RESET sets the playback phase to 0 while retaining the path, geometry edits, and strokes. In Sync, RESET records the current host beat position as a new phase offset, making it the reference starting point for subsequent movement.

Pressing RESET while paused does not immediately send the starting coordinates to the audio path. Those coordinates are output when you press PLAY again. RESET does not clear drawings or restore factory shapes. Clicking an edited Circle again likewise does not remove its geometry edits.

## 7 Planar shapes and geometry editing

### All shapes

The table lists all 36 actual names in groups for easier reference. These categories are reading aids; the menu displays the names in English.

| Category | Shape names |
|---|---|
| Basic and directional | Circle, Ellipse, Figure 8, Left / Right, Front / Back, Diagonal, Arc, S Curve |
| Polygons | Triangle, Square, Diamond, Pentagon, Hexagon, Heptagon, Octagon |
| Spirals and petals | Spiral, 3 Petals, 4 Petals, 5 Petals, 6 Petals, 7 Petals, 8 Petals |
| Waves and weaves | Double Wave, Triple Wave, 2:3 Weave, 3:4 Weave, 3:5 Weave, 4:5 Weave |
| Stars and other shapes | 5 Point Star, 6 Point Star, Zigzag, Offset Orbit, Butterfly, Heart |
| Random | Random Lines, Random Points |

Circle follows a circular path, Figure 8 follows a figure-eight path, and Left / Right and Front / Back move laterally and front to rear on the plane. Other presets provide starting shapes that can be developed through geometry editing. Front / Back always refers to the horizontal plane, not vertical height.

New presets are scaled proportionally and centered using the actual curve bounds. Circle and Square can reach all four sides. Shapes such as Ellipse retain their proportions, so only the longest dimension is guaranteed to reach the boundary. A setting of 100% does not stretch every shape into a full square.

### Editing fixed shapes

Hollow circular nodes in the XY drawing area allow local shape editing. Drag a node to change that part of the contour. White squares at the four outer corners are width/height deformation handles that let you widen or heighten the shape separately.

Drag inside the drawing area away from handles to translate the whole path. Coordinates are constrained to X/Y=-1–1, so a shape that already fills the area has little room to move. If translation in a direction is difficult, reduce SIZE first, then reposition it.

Geometry edits remain in the edit state of the corresponding shape. Switching to another shape and back does not restore an unedited preset. There is currently no exposed Undo or restore-factory-geometry button. Save a copy of the set or device before important changes.

Random modes and custom drawings do not display fixed-shape nodes or corner handles. The node-editing method for fixed presets does not apply to every mode.

### SIZE controls the path scale

SIZE changes the overall spatial scale of the path. The model range is 0.1%–100%. The displayed percentage is rounded to a whole number, so the minimum may appear as 0%. This does not mean that the actual scale has reached zero.

SIZE does not change the duration of a complete cycle and is not equivalent to Spread or Focus. Reducing the path makes the source travel a shorter spatial distance. If the cycle duration is unchanged, it still completes a cycle in the same amount of time.

Drawn content keeps the user's original coordinates; it is not automatically enlarged to fill the drawing area. Older saved states also retain their original dimensions rather than being expanded to fill the area on loading.

### Random Lines and Random Points

Random Lines generates 12 control points and connects them smoothly into a continuous path. It suits irregular, continuous position changes.

Random Points generates 12 positions and switches discretely between them according to cycle phase, without interpolating a path between points. It suits deliberate point-to-point position changes. The audio gain chain retains its existing smoothing, so a jump in the display does not mean that the speaker signals change instantaneously within one sample.

Random paths are regenerated when the cycle crosses its boundary. Clicking the same random button again also generates a new path or set of points. Reverse changes the XY traversal direction. Height can separately be set to Fixed, a rising/falling mode, or Random.

These modes change the sound's position. They do not generate new sounds, reverb, or timbres.

## 8 Drawing planar paths

### Up to eight strokes

Draw 1-8 allows up to eight path strokes. A stroke is one continuous press-drag-release action. It is not a control point or a user preset slot.

1. Click Draw 1-8 to enter drawing mode.
2. Press and drag in the XY area to draw the first stroke.
3. Release the mouse to finish the stroke.
4. Start another stroke to append it, up to a maximum of eight.
5. Set a Free cycle duration or Sync length for the entire group of strokes, then run it with PLAY.

A click in place without nonzero movement does not form a valid stroke. Attempting to draw beyond the eighth stroke displays “8 strokes reached.”

### How multiple strokes run

The model allocates time within a cycle according to the actual length of each stroke. Longer strokes receive more time and shorter strokes receive less. TIME or Sync LENGTH sets the total duration needed to traverse the entire group once. Each stroke does not receive its own equally long cycle.

The position jumps directly between strokes; connecting lines are not drawn automatically. For a visually continuous path, arrange the end and start points of adjacent strokes accordingly, or draw the required continuous path in one stroke. The Z curve continues to vary independently according to the time fraction of the entire cycle.

### Drawing at the edges

XY and height drawing can begin within 24 pixels outside the drawing area's boundary. Within 6 pixels of the edge, drawing snaps to the exact boundary. If you continue dragging outside the area, coordinates are clamped to the valid boundary; out-of-range positions are not saved.

These behaviors help create edge-following paths. They do not allow the actual panning position to exceed the model ranges of X/Y=-1–1 or Z=0–1.

### Keep a copy before making changes

There is currently no exposed command to undo, delete an individual stroke, or clear the canvas. The Draw toggle only switches drawing mode. Selecting a different shape does not delete stored strokes, and RESET does not clear them.

To design a completely new path from an empty state, use a new device instance and recheck its routing. Do not repeatedly try undocumented “clear” shortcuts in an existing performance set. To preserve several creative variations, use copies of the Live set or device first, then check what was actually saved in each copy.

## 9 Height curves

### Reading the height graph

The horizontal axis represents the time fraction of one cycle, from 0 to 1. The vertical axis represents Z from 0 to 1, or 0%–100%. A white dot and vertical line indicate the current phase.

The height curve can be edited separately, so the same planar Circle can use a fixed height, cyclical movement, random height, or a drawn rise-and-fall pattern. There is no additional independent height clock. Height and XY both run by phase within the same cycle.

Dragging directly in the height graph changes height in a particular time interval while preserving untouched intervals. Selecting another XY shape does not reset height. After switching to another height mode, you can also return to Draw and use the retained hand-drawn curve.

### Five height modes

**Fixed** holds a constant height. HEIGHT from 0% to 100% maps directly to Z=0–1. The default of 25% is Z=0.25.

**Up/Down** creates sinusoidal movement centered at 50% height. HEIGHT / RANGE controls the excursion. At 0%, height remains at 50%; at 100%, the range can reach 0%–100%; at the default 25%, the range is approximately 37.5%–62.5%. It does not move between 0% and the selected percentage.

**Rise/Fall** rises smoothly and falls back, with a fixed minimum height of 10%. HEIGHT / RANGE controls how far it rises. At the default 25%, the range is approximately 10%–32.5%. At 100%, it can rise from 10% to 100% and return.

**Random** smoothly connects eight segments of random height, with matching start and end heights. RANGE at 0% holds height at 50%; at 100%, it allows the full 0%–100% range, but an individual random curve is not guaranteed to reach both extremes. Click Random again to generate a new height curve.

**Draw** determines Z directly from the drawn curve, using 129 height samples with linear interpolation. You can redraw part of the curve without redrawing the whole cycle. Draw does not display the HEIGHT / RANGE slider. The curve itself determines height and cannot be scaled as a whole with that slider.

### Height range reference

| Mode | Control at 0% | Default 25% | Control at 100% |
|---|---|---|---|
| Fixed | Fixed at 0% | Fixed at 25% | Fixed at 100% |
| Up/Down | Fixed at 50% | Approximately 37.5%–62.5% | 0%–100% |
| Rise/Fall | Fixed at 10% | Approximately 10%–32.5% | 10%–100% |
| Random | Fixed at 50% | May vary within 37.5%–62.5% | May vary within 0%–100% |
| Draw | Slider not used | Follows the drawn curve | Follows the drawn curve |

These ranges come from the current model. The permitted range in Random does not mean that every cycle reaches both the upper and lower limits.

## 10 Free and Sync timing

### Free runs in seconds

FREE uses TIME (SECONDS) to set the duration of a complete cycle, independently of whether Live is playing. Direct numeric input accepts 0.01–300 seconds, with a default of 4 seconds. Smaller values mean faster nominal movement.

| Input in seconds | Nominal duration of one cycle |
|---|---|
| 0.01 | One hundredth of a second |
| 0.1 | One tenth of a second |
| 1 | One second |
| 4 | Four seconds |
| 60 | One minute |
| 300 | Five minutes |

For multi-stroke drawings, these values control the total cycle time for all strokes. For slow ambient work, start with a longer cycle and adjust it with the music. At very fast settings, also consider the scheduling and audio-smoothing limitations explained below.

There are native Max check records for direct 0.01-second input, display, and model restoration. Feedback has reported mouse dragging stopping at a minimum of 0.1 seconds; the cause has not been confirmed. To use 0.01 seconds, enter the value directly and check both the input field and the graph label. This release should not be treated as having resolved the dragging limitation.

### Sync follows the host

Selecting SYNC shows LENGTH and RHYTHM and hides the Free seconds field. The custom bar-count field appears only when Custom Bars is selected.

The actual LENGTH options are:

- 1/64, 1/32, 1/16, 1/8, 1/4, 1/2
- 1 Bar through 16 Bars, with a separate option for every whole-number bar count
- 64 Bars
- Custom Bars

Use Custom Bars for 32 bars or other lengths that are not listed separately. An odd number of bars specifies how many bars the path cycle spans. It does not change the time signature of the Live set.

Live must be playing and the synchronization connection must be valid before the position moves. Even when Motion displays RUNNING, it may still be waiting for host playback or a ready connection.

### Rhythm modifiers

| RHYTHM | Cycle multiplier | Meaning |
|---|---|---|
| Straight | 1 | Uses the selected standard duration |
| Dotted | 1.5 | Extends the cycle to one and a half times the standard duration |
| Triplet | 2/3 | Shortens the cycle to two thirds of the standard duration |

The modifier applies to both note and bar options. Triplet modifies duration; it does not change the set to 3/4 time.

In the current model, note options are first converted to quarter-note beats by dividing 4 by the note denominator. Bar options are converted as “bar count × time-signature numerator × 4 ÷ time-signature denominator.” The result is then multiplied by the RHYTHM multiplier.

For example, at 4/4 and 120 BPM, the nominal cycle for 1 Bar is 2 seconds with Straight, 3 seconds with Dotted, and approximately 1.333 seconds with Triplet. These are calculated timing relationships, not a substitute for verification of actual synchronization timing.

### Custom bar counts

Custom Bars accepts finite positive numbers, including fractional values. Zero, negative numbers, and nonnumeric input are rejected, preserving the valid state. The current code does not specify an upper limit that can be advertised as a supported maximum.

Custom values are useful for phrase lengths beyond the listed menu options or for very slow movement. Entering a very large value does not establish that the complete cycle has been verified to run without error. This feature does not guarantee unlimited precision, unlimited duration, or years of continuous operation.

### Playback position and Reset

Sync follows Live's current_song_time by default. Stopping and restarting Live does not guarantee that every playback starts at the beginning of the path. This release has no Retrig function that automatically returns to the start on every playback.

Use RESET to establish a new reference starting point. It stores the current host beat position as an offset, so subsequent path movement runs relative to that position. With Motion paused, RESET followed by PLAY is the explicit sequence for outputting coordinates from a new start.

### Timing settings and actual updates

Free uses a requested task interval that varies with cycle duration: a 0.01-second cycle requests 1-millisecond updates, a 0.1-second cycle requests 10-millisecond updates, and cycles from 0.2 to 300 seconds request 20-millisecond updates. The editor redraws no more often than approximately every 20 milliseconds. Sync position polling remains at 20 milliseconds.

These are requested control-task intervals. Max Task is not an audio-sample-accurate clock, and actual scheduling may be delayed. The twelve audio-channel gains still use the existing 80-millisecond smoothing. A 0.01-second cycle setting therefore does not mean that the audible panning completes exactly one hundred revolutions per second. Screen redraw frequency also does not indicate the audio processing rate.

The Sync connection waits for the host to become ready, retries after failure, and reconnects after disconnection. Playback state, tempo, and time signature are refreshed periodically. Model and simulation checks support these improvements, but stress behavior in complex real-world sets still requires the verification described in Section 14.

## 11 Saving presets and automation

### Shape presets and device state

The 36 built-in shapes provide starting points for path design. They are not complete, user-named device presets. There are currently no separate path Save, Load, Export, named-favorites, cloud-sync, or sharing buttons.

Motion uses device-state storage to record shape, SIZE, translation, geometry edits, strokes, random point sets, height curves, Free/Sync timing values, and reverse state. On restoration, phase returns to zero and playback is OFF. It does not resume from the previous running phase.

Model save-and-restore checks have been recorded. Final verification of saving, closing, and reopening a complete Live set has not been completed. For important work, save a copy of the set or device and reopen it to check before use. Completing a save action alone does not prove that all state will restore correctly.

### Checks before saving and after reopening

Before saving, note the key shape, cycle, height, and six routing rows. Confirm that the drawings and geometry edits are the versions you want to retain. When preparing a performance, keep a known-working copy of the set.

After reopening, keep the monitoring level low. Check that dependencies are intact and output destinations are correct, then check shape, SIZE, strokes, height, and timing mode. Restoring Motion as OFF is the current design. Verify the content before starting movement.

Recheck routing after changing computers or audio interfaces. Motion state storage does not replace hardware-destination checks, nor does it guarantee identical output names and ordering on another computer.

### Automation and MIDI mapping of the six main controls

Spread, Focus, LFE, X, Y, and Z use Live's parameter system and support the existing automation and MIDI-mapping workflow. The basic MIDI-mapping procedure on macOS is:

1. Press Cmd+M to enter Live's MIDI Map Mode.
2. Click the target control, such as X.
3. Move a knob or fader on the hardware controller.
4. Press Cmd+M again to leave mapping mode.

X, Y, or Z automation may trigger manual takeover and stop Motion. If Motion and automation compete for position control, decide which should control the position, then disable the corresponding control from the other source.

The main panel Motion On is an exposed Off/On parameter. Its latest actual mapping and recording behavior still needs to be checked in Live.

### Limits of Motion controls

Do not assume that shape, seconds, LENGTH, RHYTHM, SIZE, and HEIGHT can all be mapped directly like the six main controls. Some controls are JSUI interactions, and the native menus do not have parameter exposure enabled.

Motion updating the displayed X, Y, and Z values does not prove that generated coordinates are automatically recorded as Live automation. This release has no verified one-click automation-baking workflow. Pressing Record should not be presented as a method for converting an entire Motion sequence into automation.

Internal patch message interfaces exist, but they do not constitute a public external SDK. There is currently no available OSC port, standalone MIDI-parsing service, REST service, or documented remote-control protocol.

## 12 Examples and troubleshooting

### A single source at a fixed position

Check all six routing rows first and leave Motion OFF. Position the source in the main XY view, then adjust height with Z. Once the position is fixed, adjust Spread and Focus separately and observe the channel distribution. Start LFE at 0 and increase it gradually according to the downstream low-frequency system.

This procedure suits channel checks and static source placement. Turn TEST off when finished, and confirm that the intended program material enters the first input channel.

### An eight-second horizontal orbit

Open Motion Editor and select Circle. If it has started running, press PAUSE first if needed. Select FREE, enter 8 in TIME, choose Fixed height at 25%, then press PLAY. Each nominal cycle lasts eight seconds, with height held at Z=0.25.

Reduce SIZE for a smaller orbit and switch to REVERSE for the opposite direction. Pause with PAUSE or the main panel OFF control. To return to the start, pause, press RESET, then PLAY. Do not use RESET to try to restore edited circle nodes.

### An eight-bar spatial round trip

Select L/R or Front/Back, choose SYNC, set LENGTH to 8 Bars, and set RHYTHM to Straight. Start Live playback and check that the position advances with the host.

One cycle spans eight bars in the current time signature. To make a particular musical position the new path starting point, use RESET at that position. Dotted makes the cycle one and a half times as long; Triplet makes it two thirds as long.

### Orbiting with height movement

Select Circle or Figure 8, then choose Up/Down. Start with a small RANGE and observe the movement around 50% height. Increase it gradually for a wider excursion. To rise from a lower position and fall back, use Rise/Fall, remembering that its minimum height is 10%.

For local changes, draw directly in the relevant time interval of the height graph. Switching planar shapes does not clear height edits, and Reverse changes only XY traversal direction.

### Multi-stroke and slow-motion experiments

In a new device instance, use Draw 1-8 to draw between one and eight strokes, then edit the height curve. Start with a slower Free cycle and observe the entire sequence. Check that the jumps between strokes are what you want before changing the total duration.

You can also combine Random Lines with a long cycle for continuous, irregular spatial motion, or use Random Points for discrete position changes. Free has a maximum of 300 seconds; use Custom Bars for longer synchronized cycles. Extremely long cycles still require practical verification. A value being accepted does not establish a stable operating duration.

### No sound at all

Check, in order: whether the source is playing, whether the first input channel contains audio, whether the device is enabled, whether the twelve meters are active, whether all six TYPE/CH rows are valid, whether Output Config is enabled, and whether the audio interface, amplifiers, and speakers are working.

If using TEST, lower VOL before turning it on. If internal meters move but there is no actual sound, concentrate on routing and hardware after the device. Pausing Motion alone does not stop audio.

### Only some speakers play or the direction is wrong

Compare each output pair with the channel table in Section 3. Confirm that the audio interface has enough physical outputs and that CH matches the actual cabling. Position, Spread, Focus, and Z also affect which channels receive signal. An instantaneous meter reading at one position is not enough to conclude that other channels have failed.

If the perceived front/rear or left/right direction is opposite to the display, check wiring and output destinations first, then X/Y orientation. Up in the planar view means front; Z is height.

### Overlapping signals or confusing levels

Check whether the track's Audio To still points to Main, allowing both the device direct outputs and the track's main output to sound. Also check whether TEST is still on while the original source is playing. Simplify the signal path before judging panning.

### Motion does not move

Check the main panel OFF/ON or the editor PLAY/PAUSE control. Do not infer playback state from the yellow MOTION / EDIT entry point. If you recently used the main XY/Z area or X, Y, or Z parameters, manual takeover may have stopped Motion.

In SYNC, also confirm that Live is playing and the connection is ready. RUNNING indicates that movement has been requested; it does not rule out waiting for the host. Temporarily switching to FREE can help distinguish a host-sync condition from a path problem. Note the current timing settings before switching.

### A shape will not move or return to a circle

If a full-size path already approaches the coordinate boundaries, it has limited room for translation. Reduce SIZE first. Node editing, corner-handle deformation, and whole-path translation are different operations; check the pointer location before dragging.

RESET resets playback phase only. Selecting Circle again retains that shape's edited geometry. There is currently no exposed restore-factory-geometry, Undo, or clear-canvas operation. For a fresh path, use a new device instance and recheck routing.

### Timing differs from what you expect

First distinguish FREE seconds from SYNC note/bar durations. Then check RHYTHM, the set's BPM, and its time signature. Multi-stroke drawings use one total duration for the whole group; a cycle is not the duration of a single stroke.

You can enter 0.01 seconds directly, but interface redraws, control tasks, and audio-gain smoothing are separate stages. The visual and audible behavior of very fast cycles cannot be inferred from the entered number alone. Actual synchronization and fast cycles still need testing in the target set.

### Height differs from what you expect

Check the height mode. Up/Down at 0% stays at the middle height, and Rise/Fall has a fixed minimum of 10%. Neither simply moves from zero to the selected percentage. Draw follows the height curve directly and is not scaled globally by the HEIGHT / RANGE slider.

Main Z defaults to 0, while Motion defaults to Fixed at 25%. A height change when starting Motion for the first time may result from these different initial values.

### What to include in feedback

Record the device filename; Live, Max, and operating-system versions; audio-interface model and output configuration; the step where the problem begins; and the expected and actual results. For save/restore issues, describe the difference before saving and after reopening. For routing issues, include readable screenshots of all six ROUTING rows and Output Config.

Prefer a minimal reproducible set. Do not indiscriminately include an entire working directory containing private audio, account information, or unrelated files.

## 13 Release notes

### Changes from the earlier version

This comparison uses the traceable v1.3.1 Public Beta as its baseline. Earlier unversioned introductory copy cannot establish which features are new in this release.

| Area | Already present in the earlier version | Changes in v2.1 |
|---|---|---|
| Core panning controls | Position, Spread, Focus, LFE, XYZ, test tone, and meters | Retains the existing main workflow |
| Multichannel output | Twelve outputs, six routing pairs, and fixed channel order | Retains these and adds default output-selection logic |
| Planar motion | No Motion system equivalent to this release | Adds a separate editor, 36 shapes, up to eight drawn strokes, and geometry editing |
| Height motion | Manual Z control | Adds separately designable height modes and curves |
| Timing and playback | No Motion clock or controls equivalent to this release | Adds Free, Sync, play/pause, reverse, and Reset |
| Spatial monitoring | No 3D monitor equivalent to this release | Adds read-only XYZ / 3D position and path monitoring |
| Main panel | 1030 × 169 | Expands to 1226 × 169, adding the monitor and new entry points |
| Branding | Earlier positioning view | Adds the white L+R mark inside the yellow range circle |

The core audio-gain, test-frequency, meter, and original output-object implementations are retained from the earlier version. The new motion features should not be described as a newly implemented Atmos encoding or rendering engine.

### Development revisions included in the release

Sync initialization adds host-readiness waiting, connection-validity checks, failure retries, release of old observers, reconnection, and refreshes of playback state, tempo, and time signature. These changes address startup and connection recovery. Stress verification in complex real-world sets remains to be completed.

New presets now start at SIZE=100%, rather than the 70% used in an earlier candidate, and are fitted proportionally using their actual curve bounds. Older saved states restore their original geometry; drawings are not enlarged automatically.

Default routing now keeps waiting for menus and the device path, with dedicated routing dependencies kept separate. Initialization no longer simply ends because they are not ready within a short interval. Routing checks are still required with the actual audio interface and on another computer.

The Free direct-input minimum changed from 1 second in an earlier candidate to 0.01 seconds. Numeric display and state restoration use the same range, and a dynamic requested task interval was added for fast cycles. Labels for values below 1 second use two decimal places. Existing audio smoothing remains in place. The cause of reported mouse dragging stopping at 0.1 seconds has not been confirmed.

### What the version names mean

The public version name is v2.1, while the technical device filename uses v2_1_0. The final named release retains the functionality and layout of the immediately preceding Free01 candidate. Its changes mainly concern filenames, version displays, and delivery records; they do not represent another round of features or fixes that did not occur.

The traceable v2 development history includes alpha candidates. These must not automatically be treated as a formally published v2.0 release.

## 14 Limitations and verification scope

### Product scope

The device distributes the position and movement of a single source across twelve speaker outputs. There is currently no functional evidence of Atmos bitstream encoding, Dolby object metadata, ADM/BWF export, a Dolby Renderer connection, or Dolby certification. There is also no confirmed workflow for binaural headphone rendering or automatic speaker calibration.

LFE is an independent send and does not currently provide complete crossover processing or bass management. The six exposed main controls are Spread, Focus, LFE, X, Y, and Z. Retained legacy internal fields do not constitute additional public features.

### Recorded installed environment

The development computer's recorded environment is listed below. These details identify software conditions. They do not establish that every combination has passed runtime verification or constitute a minimum-version commitment.

| Item | Recorded value |
|---|---|
| Operating system | macOS 15.4.1, Build 24E263 |
| Computer architecture | arm64 |
| Host | Ableton Live 12 Suite 12.4.6 |
| Max bundled with Live | 9.1.5 |
| Device save metadata | Max 9.1.4, x64 |

The x64 entry in device save metadata does not prove compatibility across all Intel and Apple Silicon combinations. This release has no confirmed support scope for Windows, other DAWs, VST/AU, or a standalone application.

### What the completed checks establish

The delivered device container has been checked against the final project content, and the related files have passed consistency checks. Ten existing Node checks cover the model, structure, simulated synchronization connections, simulated routing menus, shape bounds, state restoration, and related behavior.

Existing native Max records check direct 0.01-second input, display, model restoration, and identifier mapping for the six output menus. The Free check ran in a standalone window without audio. The routing check used synthetic menus to verify identifiers and did not write to actual Live or hardware routing. Earlier development records also document actual button and visual-interaction checks. These results provide evidence for their respective model or native-check scenarios.

### Checks still required before production use

The checks above do not amount to complete audio verification of the final device in a real Ableton set with an audio interface. The following still need checking in the actual target environment:

- Real device loading, repeated reopening, and operation in complex sets
- Sync behavior during looping, pausing, seeking, and time-signature changes
- Actual timing and audible behavior of fast cycles such as 0.01 seconds
- The six default routing pairs on another computer and with the actual audio interface
- State after saving, closing, and reopening a complete Live set
- Isolation and interaction when several device instances run together
- Correspondence between each path, height changes, and the actual twelve outputs
- Whether the first-input-channel arrangement meets expectations for the stereo material in use
- Actual automation, MIDI-mapping, and recording behavior
- Whether the editor remains on top after focus changes in Live

Before performing, check the complete system using the actual computer, audio interface, wiring, and set, and keep a set copy you can return to. Default routing, model tests, and a successful numeric-input check cannot replace verification of the live system.

### Free availability and future maintenance

The software is currently provided free of charge, as stated by the author. Continued maintenance and free updates reflect the author's present intention and are not a guarantee that it will remain free forever. Distribution and usage rights are governed by the license terms actually provided. Free availability alone does not imply an open-source license, commercial redistribution rights, or other unstated permissions.

## A note from the author

Hello, I'm L+R, Wang Lu, an electronic musician.

Many of the ideas behind this plugin came from my own needs while mixing spatial audio and performing live over the years. I wanted sound to move more freely through a 7.1.4 space, and I wanted those ideas to give musicians something they could really play with on stage.

I make ambient music, and I'm especially drawn to slow movement. Some ideas might not come up in everyday use, but there will always be people who enjoy experimenting and want to try them. I wanted to leave some room for those ideas too.

I spent a few months thinking about this update: what features did I actually need? Getting AI to write the code took less than two days. I didn't write a single line of it myself. I'm a developer who doesn't know how to code, using AI to help bring my own ideas to life.

So I still want to say: open up your thinking, start playing with AI, and make the tools you want. Those of us who have been making music for years have plenty of ideas, and we know when a tool doesn't quite fit the way we work. Now we can start shaping it in our own way, making it fit a little better, and keeping it maintained and growing over time.

I feel that this era is opening up more and more possibilities for people who have ideas, want to create, and want to try more interesting things. Give it a try.

I hope you enjoy using this plugin, make your music sound better, and create the spaces and movements you hear in your mind. I also welcome you to come and talk: how is it working for you? What ideas do you have? We can explore them together.

The software is still free, and I'll keep updating it. Thank you for your support.

Let's all get into it and have fun.

L+R / Wang Lu
