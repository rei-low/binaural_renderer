# binaural-render

Places a mono recording at any direction around a listener by convolving it with measured head-related impulse responses (HRIRs), and writes a stereo WAV for headphones. It's the reference pipeline for my research on sound externalization and HRTF individualization.

## What the notebook does

1. Loads a SOFA HRIR set (SimpleFreeFieldHRIR) with sofar and pyfar, and checks that channel 0 is the left ear.
2. Finds the measured direction nearest a requested azimuth and elevation, and reports the match.
3. Plots the left and right HRIRs and their magnitude responses for that direction.
4. Resamples the source to the HRIR sampling rate and convolves it with both ears' HRIRs.
5. Normalizes both ears with one gain (peak at −1 dBFS), so the interaural level difference is preserved.
6. Renders the source front, 25° left, left, back and right.

## Data

- **HRIRs:** Meta Reality Labs SS2 database, listener YNB205 (1,625 directions, 48 kHz, CC-BY-4.0). Download it separately and save it as `data/YNB205081622_1_processed.sofa`.
- **Source:** any WAV saved as `data/trumpet.wav`. Stereo files are mixed to mono.

Neither file is included in this repo.

## Run

```bash
pip install pyfar sofar matplotlib jupyterlab
jupyter lab binaural_render.ipynb
```

Renders are written to `renders/`. Listen on headphones.

## Coordinates

Azimuth runs counterclockwise from straight ahead (90° is the listener's left), and elevation is measured up from the horizontal plane. This matches pyfar and SOFA.
