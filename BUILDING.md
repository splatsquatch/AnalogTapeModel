# Instructions For Building
CHOW Tape is built using [CMake](https://cmake.org), along with the [JUCE](https://github.com/juce-framework/JUCE) framework, and [PluginGUIMagic](https://github.com/ffAudio/PluginGUIMagic)
for the UI. JUCE and PluginGUIMagic are included in the repository, but CMake must be installed before attempting to build. CHOW Tape also uses the CMake build tool To build from scratch, you must first clone the repository
and initialize the submodules using the following commands:

```bash
# Clone the repository
git clone --recursive https://github.com/jatinchowdhury18/AnalogTapeModel.git

# Enter the repository
cd AnalogTapeModel/Plugin

# Initialize submodules
git submodule update --init --recursive
```

Next you can generate the builds with CMake:

```bash
cd Plugin/
cmake -Bbuild
cmake --build build/ --config Release
```

## Linux Dependencies
The Linux build utilises the following dependencies:
- libasound
- libxcursor
- libxinerama
- libxrandr
- freeglut3
- libjack

These can be installed with the following command:
```
sudo apt-get install libasound2-dev libxcursor-dev libxinerama-dev libxrandr-dev freeglut3-dev libjack-jackd2-dev
```
Depending on your Linux distribution, you may also need to install:
- freetype
- libGL
- libXext
- libcurl
- python3 (only if you plan to build LV2)

## Building with the GUI Editor
If you need to make changes to the GUI, you can build the plugin with Foley's Magic Editor attached. In `Plugin/CMakeLists.txt`, set `FOLEYS_SHOW_GUI_EDITOR_PALLETTE` equal to 1.
