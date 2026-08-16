# OHMidiPlayer

**A MIDI player for Once Human's in-game Piano and Guitar.**

OHMidiPlayer reads standard `.mid` / `.midi` files and plays them into Once
Human by sending keyboard input — exactly the way you'd press the keys
yourself. Just load a song, click into the game, and press play.

Made by Perpy08.

---

## What it does

- **Plays MIDI files into Once Human** using the in-game Piano and Guitar
  key layouts.
- **Piano mode** maps one octave to the base keys
  (`q 2 w 3 e r 5 t 6 y 7 u`) and uses **hold-Shift = +1 octave** and
  **hold-Ctrl = −1 octave** to reach notes outside the default range.
  Notes more than one octave away are transposed to the nearest playable
  octave rather than dropped.
- **Guitar mode** uses three fixed keyboard rows (one per octave, low /
  mid / high), diatonic scale only — no sharps or flats. Out-of-range and
  sharp/flat notes snap to the nearest playable pitch.
- **Playback controls**: play / pause / stop, loop, a speed slider
  (0.25×–3×, applied live), elapsed/total time, and a progress bar.
- **Skip Drums (MIDI channel 10)** is on by default so percussion tracks
  don't spam random keys.
- **Global hotkeys** for play/pause and stop work even while Once Human is
  focused, so you don't have to alt-tab to stop a song.
- **Live visualizer** lights up each key as it plays.
- **3-second count-in** gives you time to click back into the game after
  pressing play.
- **Persistent settings** — keybinds, speed, last-used folder, loop, and
  instrument choice are remembered between sessions.

## How to use

1. Launch Once Human and sit at an in-game **Piano** or **Guitar** [<u>**Download Here**</u>].
2. Run `OHMidiPlayer.exe` and approve the Windows administrator prompt
   (see below).
3. Pick the matching mode (**Piano Mode** / **Guitar Mode**).
4. Click **Browse MIDI File** and select a `.mid` / `.midi`.
5. Click **Play**. You have 3 seconds to click into the Once Human window
   so the key presses land in the game.
6. (Optional) Open the ⌨ menu in the top-right to assign a global
   Play/Pause or Stop hotkey.

## System requirements

- Windows 10 or 11.
- Administrator rights (required for the global hotkey hook).
- Once Human, with an in-game Piano or Guitar placed and interactable.

---

## Heads-up: Windows may flag the app on first run

When you first run `OHMidiPlayer.exe`, Windows Defender SmartScreen (or
your antivirus) may show a warning such as **"Windows protected your PC"**
or flag the file as **potentially unwanted / unknown**. This is **normal**
for small, independent apps like this one and does **not** mean the file
is dangerous.

### Why it happens

- The app is **not code-signed with a paid certificate**. Code-signing
  certificates cost hundreds of dollars a year, so most hobby/indie tools
  are distributed unsigned. Windows SmartScreen is cautious about any
  unsigned `.exe` it hasn't seen before — it builds "reputation" for an
  app over time as more people run it, and the warning gradually goes away
  on its own.
- This app **sends keyboard input to other programs** (it literally types
  into Once Human to play notes) and **registers a global key hook** for
  the play/stop hotkeys. Those are the *same techniques* some automation
  and macro tools use, so heuristic antivirus scans sometimes flag them —
  even though here they're only used to play music.
- The binary is built with **PyInstaller**, which packs the Python
  interpreter and the app's libraries into a single `.exe`. Some
  antivirus products are extra suspicious of PyInstaller-packed files
  because malware authors occasionally use the same packer.

### The app is safe

- It only does three things: **reads** the MIDI file you pick, **sends
  key presses** for the notes, and **listens** for your two custom
  hotkeys. It does not read your files, passwords, or personal data; it
  does not connect to the internet; it does not install anything; it does
  not modify anything outside its own settings file (stored in
  `%APPDATA%\OHMidiPlayer\`).
- You can Check the Apps Scan Results on [Virustotal.com](https://www.virustotal.com/gui/home/search)

  With this Hash: 991e034636495c092c2e002117a59b4368feb50c03ce3d6f13889279a8fef597


### How to run it anyway

If SmartScreen blocks it:

1. Click **More info** in the SmartScreen dialog.
2. Click **Run anyway**.

If your antivirus quarantines it, open your antivirus history and choose
**Restore / Allow** for `OHMidiPlayer.exe`. You can also run a
right-click → **Scan with Microsoft Defender** to confirm it's clean.

If you'd rather not trust a prebuilt binary at all, clone the repo and
build the `.exe` yourself — every dependency is pinned to a specific
version and the build command is documented in the repository.

---

## Settings file

The first time you change a setting, the app creates
`%APPDATA%\OHMidiPlayer\oh_midi_player_config.json`. Delete it to reset
all keybinds and preferences.

## Troubleshooting

- **Notes don't reach the game** — click the Once Human window during the
  3-second count-in so it has keyboard focus.
- **Hotkeys don't work** — make sure you approved the administrator
  prompt; the global key hook requires admin rights.
- **Shift/Ctrl feel "stuck" after playback** — the app always releases
  held modifiers when a song stops, even on error; if the game still feels
  pitch-shifted, tap Shift or Ctrl once manually to clear it.
- **The taskbar shows a generic icon** — make sure you're running a
  recent build; if you pinned an older version, unpin it and re-pin.

## Credits

Player made by Perpy08. Built with Python, Tkinter, mido, pyautogui, and
keyboard.
