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

Requires 64-bit Windows 10 or 11. Nothing else needs installing.

1. Download `CueFire-<version>-Windows.zip` from the latest release and unzip it.
2. Move **CueFire.exe** wherever you like (for example a `CueFire` folder in Documents) and double-click it.

CueFire isn't code-signed yet, so the first time Windows SmartScreen may say it "protected your PC" because the app is from an unknown publisher. Click **More info ▸ Run anyway**. You only need to do this once.

## OSC control

CueFire listens for OSC over UDP on port **53100**. You can change the port, or turn OSC off, in **Preferences ▸ OSC**. Any OSC sender works: Bitfocus Companion, QLab, TouchOSC, a lighting desk, or a script.

Cue numbers in addresses start at 1 and follow the cues' order on screen: left to right, top to bottom in the button view, or top to bottom in the list. Moving a cue changes its number. Addresses aren't case-sensitive.

| Address | Argument | Action |
|---|---|---|
| `/cue/{n}/go` | none | Fire cue *n*. Restarts it if it's already playing |
| `/cue/{n}/stop` | none | Fade out and stop cue *n* |
| `/cue/{n}/level` | dB (number) | Set cue *n*'s level, −60 to +12 dB |
| `/cue/{n}/loop` | 0 or 1 | Turn looping off or on for cue *n* |
| `/stop` | none | Stop all cues with a fade. Send it again during the fade to stop instantly |
| `/master/level` | dB (number) | Set the master level, −60 to +6 dB |
| `/cue/{n}/state` | none | Ask for cue *n*'s state |
| `/state` | none | Ask for the state of every cue and the master |
| `/subscribe` | none | Send every change back to the sender for 20 seconds. Repeat it to keep the updates coming |
| `/unsubscribe` | none | Stop sending changes |

**Buttons that send 1 on press and 0 on release:** go, stop, `/stop` and `/state` ignore an argument of `0`, so each press fires once. `/subscribe` with `0` unsubscribes.

### Replies

About 50 ms after each command, CueFire replies with the state of whatever it changed. Replies go to the computer the command came from, on the port it came from. To send them to a fixed port, or to turn them off, use **Preferences ▸ OSC**. `/state` and `/cue/{n}/state` are always answered.

| Reply | Arguments, in order |
|---|---|
| `/cue/{n}/state` | state (`playing`, `fading`, `stopped`, `empty` or `missing`), name, level in dB, loop (0 or 1), elapsed seconds, remaining seconds, colour as `#RRGGBB` |
| `/master/state` | master level in dB, number of cues playing, number of cues, grid rows, grid columns |

`/stop`, `/state`, and firing a cue set to stop other cues reply with every cue's state plus the master.

### Bitfocus Companion

Companion's built-in **Generic: OSC** connection can send any of the commands above. Point it at the CueFire computer's IP address and port 53100.

## MIDI

CueFire listens to every connected MIDI device, including ones plugged in later. To give a cue a trigger, open the cue's editor (or **Preferences ▸ MIDI**), click **Learn**, then press a note, pad or button.

- Notes and program changes fire straight away.
- A control change fires when its value rises past 64, so a button fires once per press and a fader once each time it passes halfway.
- **Stop All** and **Go Selected Cue** can have MIDI triggers too, in **Preferences ▸ MIDI**.

## Hotkeys

Each cue can have a hotkey, set in its editor or in **Preferences ▸ Hotkeys**. **Stop All** is ⌘Esc by default (Esc on Windows). You can also set a **Go Selected Cue** hotkey, which fires the highlighted cue. Hotkeys without ⌘ or ⌃ are ignored while you're typing in a text field, except Stop All.

## Shows

A show is saved as a `.soundboard` file. Mac and Windows use the same format, so a show can move between them; audio files are found again by path.
