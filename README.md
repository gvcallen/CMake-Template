# CMake-Template
CMake Template for VS Code


## Overview

The following is a CMake C++ Template for use with VS Code on Windows. It requires very little CMake knowledge (as I have little myself) which makes it great for mimicking an IDE environment such as Visual Studio (which I will use as a "baseline" for the keyboard shortcuts and as a general comparison). In fact, this template is designed specifically for those who are moving from a fully-fledged IDE such as Visual Studio, to VS Code.

If you would like this template to work out of the box, a few steps need to be followed, however it is obviously all relatively configurable. The template uses the MinGW-w64 32-bit and 64-bit compilers.


## Prerequisites

- Install CMake itself from https://cmake.org/, and ensure that its "bin" directory is added to your "Paths" environment variable (see https://docs.alfresco.com/4.2/tasks/fot-addpath.html for how).

- Install the "CMake Tools" and "CPP-Tools" extensions from the VS Code marketplace. An optional extension is also the "Project Templates" extension, available at https://marketplace.visualstudio.com/items?itemName=cantonios.project-templates. This will allow you to easily create new projects from this template.

- Ensure that the MinGW-w64 64-bit and 32-bit toolchains are installed from http://winlibs.com/, and that you haved moved these folders so that their paths align EXACTLY with those in the "cmake-tools-kits.json" file provided. NOTE: Although CMake tools CAN automatically detect your kits, the "launch.json" file picks which debugger to use based on the active kit's name, and is set to use one of the two directories based on the currently active kit's name. This is as the gdb.exe debugger for 32-bit and 64-bit are unfortunately incompatible, so a little hacking needed to be done, hence this "constraint".


## How to setup template for the first time:

1. If you have installed the "Project Templates" extension, move the "solution-dir" folder to that extension's template location (should be "AppData\Roaming\Code\User\ProjectTemplates" by default) and rename it as you like.

2. Open VS Code. You will need to manually edit CMake Tools' "kits" or compilers. The reason behind this is that the template uses the names of these kits for both the project build directories and (as mentioned) to locate the debugger. Open the command palette, type "Edit User-Local CMake Kits", and hit enter. There may already be a few in this file, however I would just remove them for simplicity sake. Copy the contents of "cmake-tools-kits.json" provided with this template to this file. There may be a bug with the initial setup at some point where CMake Tools re-scans and overrides this file, in which case you may just need to follow this step again.


## How to create a "solution" or base project:

1. Create a new folder wherever, and open it in VS Code. If using the template extension, open the command palette, type "Create Project from Template", and hit enter on your template name, otherwise just copy the template contents to this folder.
  
2. Open the command palette, type "CMake: Configure", and hit enter.


## Keyboard Shortcuts

- We are using CMake Tools to build our Makefiles, and VS Code to debug our target (as CMake Tools debugging for me was producing an error). I have therefore removed the CMake Tools shortcuts for both debug and run (CMake: Debug and CMake: Run Without Debugging).

- CMake: Build --> Ctrl + Shift + B (Build the entire project)
- CMake: Build Target --> Ctrl + B (Build the current target)
- Debug: Start Debugging --> F5 (Start debugging with GDB)
- Debug: Stop --> Shift + F5 (Stop debugging)


## Project structure and CMake Basics

- Each CMake project (including the "solution" or base project) is managed by a CMakeLists.txt file. The outer CMakeLists.txt file simply defines the name of the overall "solution", and add's all relevant "sub-directories" or sub-projects to this "solution" or base project.

- Each sub-project folder should contain a "src" and "include" folder, with another CMakeLists.txt file. In this file, you need to manually add the source files and header files to each sub-project as indicated (for those not used to this, its the CMake way). It has also been setup so that you can add definitions, include paths and compiler options, although I recommend vector-of-bool's videos on "How to CMake Good" on YouTube for anything more complicated.

- The relevant build files are produced in a seperate "build tree" which can be considered "parallel" to the source tree. This may be different from IDE setups. The template produces sub folder's for each kit in the "build" folder, a further subfolder for "debug" and "release" and then a general CMake build tree from there (a folder for each sub-project, and a "bin" directory in each sub-project with the relevant executable). I am not sure if this is standard CMake practice or not, but it prevents rebuilding each time you switch configurations, and is what I consider "Visual Studio" standard, so I went for it.

## Conclusion

That's it! I hoped you find this useful in some way. If you have any additions, suggestions, or bug-fixed, feel free to message/email me or submit a pull request. Happy coding!
