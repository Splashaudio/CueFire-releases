# CueFire

CueFire is an app for firing sound effects and audio cues in live productions. Cues sit on a grid of buttons (or in a list), and you fire them by clicking, with hotkeys, from MIDI controllers, or over OSC (including from Bitfocus Companion).

This repository holds the downloadable builds. **Get the latest version from [Releases](https://github.com/Splashaudio/CueFire-releases/releases/latest).**

## Mac

Requires macOS 14 (Sonoma) or later on an Apple silicon Mac (M1 or newer).

1. Download `CueFire-<version>-macOS.zip` from the latest release and double-click it to unzip.
2. Drag **CueFire** into your **Applications** folder.
3. The first time, **right-click CueFire and choose Open**, then click **Open** again.

CueFire isn't notarised by Apple yet, so a plain double-click the first time says it "can't be opened" or "can't be checked for malicious software". If that happens, open **System Settings ▸ Privacy & Security**, scroll down, and click **Open Anyway** next to the CueFire message. You only need to do this once.

## Windows

A Windows build will be added to the releases when it's ready.

## Shows

A show is saved as a `.soundboard` file. Mac and Windows use the same format, so a show can move between them; audio files are found again by path.
