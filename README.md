# LtRt Matrix Decoder with Logic Steering

## Overview

The **LtRt Matrix Decoder with Logic Steering** is an experimental JSFX plugin designed for decoding 2.0 LtRt (Left Total, Right Total) matrix-encoded audio, such as Dolby Stereo, into 4.0 LCRS (Left, Center,  Right, Surround), packaged within a 5.1 container. This plugin aims to emulate the logic-based steering techniques found in cinema sound processors, drawing inspiration from Dolby's white papers and the pioneering matrix decoding work by Jim Fosgate.

## Background

Film industry guidelines advise against the use of matrix-encoded audio in distributed DCPs (see https://registry-page.isdcf.com/audioconfigs/). In addition, distributing DCPs with only 2.0 audio is generally considered poor practice: for example, the Academy Awards submission specifications explicitly require a minimum of three audio channels (Left, Right, Center) for non-mono.

To support exhibition workflows where the only available source masters for DCP creation are 2.0 LtRt tracks, this project was initiated to provide an accessible and efficient method for deriving LCRS channels.

## Features

- Decodes 2.0 LtRt into 4.0 LCRS, mapped to 5.1 SMPTE channel order (L, R, C, LFE, LS, RS). The LFE channel is left empty, and the mono Surround signal is sent to both LS and RS.
- Includes an LCR-only mode for decoding without surround output, ideal for 3.0 playback scenarios.
- Implements logic-based steering for dynamic signal separation.
- Adaptive release times for steering, balancing quick transient response and ambient stability.
- Applies a soft clipper to prevent distortion by smoothly limiting output signals.
- Does not use FFTs, thereby avoiding the artifacts typically associated with that type of audio processing.
- Provides adjustable parameters via sliders for fine-tuning the decoding process.
- Includes a graphical user interface (GUI) with real-time visualization of output levels and steering direction.

## Slider Controls

The plugin offers the following sliders for customization:

- **Surround Delay (ms)** (0–50 ms, default: 20 ms): Adjusts the delay applied to the surround channel, with a default of 20 ms per Dolby’s guidelines.
- **Bass Crossover (Hz)** (0–200 Hz, default: 80 Hz): Sets the crossover frequency for the low-pass filter applied to bass content. Frequencies below this threshold are passively decoded to avoid steering artifacts.
- **Control Low Cut (Hz)** (100–500 Hz, default: 200 Hz): Defines the high-pass filter cutoff frequency for the control signal, used in the steering logic to focus on mid-range frequencies.
- **Control High Cut (Hz)** (5000–15000 Hz, default: 10000 Hz): Sets the low-pass filter cutoff frequency for the control signal, limiting high-frequency content in the steering logic.
- **Surround Low Pass Filter (Hz)** (5000–10000 Hz, default: 7000 Hz): Applies a low-pass filter to the surround channel, with a default of 7000 Hz per Dolby’s guidelines.
- **Mode** (Full Logic LRCS (5.1) or LRC only, default: Full Logic LRCS): Toggles between 4.0 LRCS decoding (5.1 output) or LRC decoding (no surround output). Both modes output in SMPTE channel order.
- **Steering Strength** (0–2, default: 1): Controls the intensity of the logic-based steering.
- **Output Gain (dB)** (-20–0 dB, default: -3 dB): Adjusts the overall output gain for all channels.
- **Surround Level (dB)** (-20–0 dB, default: -3 dB): Applies additional gain to the mono surround channel (in LS and RS), on top of the Output Gain. The default value of -3 dB aligns with Dolby’s 5.1-Channel Production Guidelines.
- **Show/Hide GUI** (Off/On, default: On): Toggles the graphical interface, which displays output level meters for FL, FR, C, and S, and a plot of the steering direction.

## Installation and Usage

- Copy the JSFX script file to your DAW's JSFX plugin directory (e.g., REAPER's Effects folder).
- Make sure your project is set to 5.1 output to enable Full Logic decoding. In REAPER, configure both the Master Track and the LtRt track for 6 channels.
- Load the plugin in your DAW as a JSFX effect on the track containing LtRt audio.
- Adjust sliders to fine-tune the decoding process based on the source material and listening environment.
- If your preferred DAW does not support JSFX, you can still use it through the AU, CLAP, or VST3 plugin hosts available here: https://github.com/JoepVanlier/ysfx.

## Notes

- The soft clipper ensures clean output by preventing hard clipping, especially during dynamic signal peaks.
- The steering strength slider allows balancing between subtle and aggressive channel separation, depending on the desired effect.
- In the plugin, the channel ID corresponds to the SMPTE channel order it outputs (e.g. LRCS).
- Use the GUI (when enabled) to monitor output levels and the logic steering direction in real time, plotted on an X-Y axis: X for left/right movement and Y for front/back movement.
- As this plugin aims to emulate the logic steering found in some cinema sound processors, you may notice certain audio artifacts that are an inherent characteristic of this type of matrix decoding, especially when using higher Steering Strength settings.
- Although this plugin was primarily developed to decode 2.0 LtRt, it can also be used with standard stereo audio. However, results may vary, so please monitor the output carefully. When working with audio that is not matrix-encoded, it is advisable to use the LRC mode to generate a center channel for 3.0 playback.

## Disclaimer

- This plugin is experimental and provided as-is. It is designed to decode LtRt matrix-encoded surround audio, but its performance and accuracy cannot be guaranteed.
- By using this plugin, you acknowledge that it is a work-in-progress and may contain bugs or limitations. Feedback and testing are welcome to help improve future versions.
  
## Acknowledgments

This plugin is inspired by technical white papers published by Dolby and the innovative matrix coefficients developed by Jim Fosgate.

## License

See the `LICENSE` file for details.
