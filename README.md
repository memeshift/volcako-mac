# Volcako

Fork of [Luomu/volcako](https://github.com/Luomu/volcako) with a macOS port by [Memeshift](https://memeshift.com). All original work is by Luomu, under the MIT license.

## Note: this project has not been tested with Volca FM 2 (released 2022)! Get in touch if you have one!

This is a realtime editor for the Korg Volca FM. It exposes all of Volca's parameters in one ~~ugly~~ functional screen. In addition it can load and save entire 32 voice banks in .SYX format. If you have a midi input device connected, the keypresses will be routed to Volca, optionally with note velocity!

![Screenshot](docs/screenshot.png)

How to use:
- Select your midi out device from Settings. The Volca listens to the sysex messages regardless of the channel it's set to.
- Selecting a patch or editing the patch parameters sends it to the currently selected slot on the Volca. You still have to Save the patch manually on the device (Edit->Write, hardware limitation)
- File->Load .SYX can be used to load an entire DX7 patch bank.
- File->Send All Patches will send and save all of the 32 patches to the device.

Some nice to know things:
- Right click on an envelope to copy/paste the values
- Control-click on an input field to type in the value
- The last edited present is auto-saved/loaded into lastpreset.txt

Windows release can be found at: https://github.com/Luomu/volcako/releases/download/r1/volcako-r1.zip

## Release notes

```
Unreleased
[New] macOS build (CMake, Apple Silicon tested)
[Fix] Fonts render sharp on HiDPI/Retina displays
[Fix] MIDI backend is auto-detected instead of hard-coded to Windows MM

R2 (May 2022)
[New] Allow copying and pasting patches (right-click patch browser)
[New] Save the entire patch bank on shutdown as lastbank.syx, load on startup
[New] Add Init Patch to the browser right-click menu
[New] EXPERIMENTAL: Add "DX7 compatibility mode" to settings: Sends sysex messages according to the original DX7 spec. Will sound wrong on Volca FM. May work with Volca FM2.
[New] Add "reset envelope" context menu action

R1 (November 2019)
Initial release
```

## Building

Windows and macOS are supported. Linux has not been tried. You have two choices on Windows: [CMake](https://cmake.org/) and [Genie](https://github.com/bkaradzic/genie). On macOS use CMake.

### Windows

Using CMake is simple with Visual Studio 2022 (Community): Just open the folder and it should run the CMake configuration. Then select Build->Build all.

With genie you need to generate the makefile/solution for the IDE of your choice. To create .sln for VS 2019, run this in the root directory:

```genie vs2019```

Precompiled Genie Windows executable: https://github.com/bkaradzic/bx/raw/master/tools/bin/windows/genie.exe

Note: the macOS port changed a few shared source files (C++14 instead of C++11, Unicode escapes in algorithm.cpp, MIDI API auto-detection, font scaling). The Windows build has not been re-tested since.

### macOS

Needs the Xcode Command Line Tools (`xcode-select --install`) and [Homebrew](https://brew.sh/). Tested on one Apple Silicon Mac with a Volca FM connected through a USB-MIDI interface; File -> Send All Patches has not been tested on macOS.

```sh
brew install cmake glfw
cmake -B build
cmake --build build
./volcako
```

The executable is written to the repository root. Run it from there: fonts, presets and the settings/last-patch files are found via relative paths, so launching it from another directory (or double-clicking it in Finder) will not work. There is no `.app` bundle yet.

macOS deprecated OpenGL in 10.14. It still works, but a future macOS release could remove it.

## Libraries used
dear imgui - https://github.com/ocornut/imgui

glfw - www.glfw.org/

inipp - https://github.com/mcmtroffaes/inipp

rtmidi - www.music.mcgill.ca/~gary/rtmidi/

tinyfiledialogs - https://sourceforge.net/projects/tinyfiledialogs/

font awesome + headers - https://github.com/juliettef/IconFontCppHeaders/

## References
Korg Volca FM Midi implementation - www.korg.com/us/support/download/manual/0/558/2963/

## Thanks to
Dexed - https://asb2m10.github.io/dexed/ - DX7 VST and editor, used to verify Sysex compatibility
