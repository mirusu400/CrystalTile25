# Build Guide

## Overview

This repository builds as a native Windows MFC application with Visual Studio/MSBuild.
It is not a CMake project.

The main application is `CrystalTile2`.
The most reliable contributor setup is:

- Visual Studio 2022 Build Tools or Visual Studio 2022
- MSVC `v143`
- MFC for `v143`
- Windows 10/11 SDK

Recommended default target:

- `Debug|x86`

This target was verified to build and run successfully on a current Windows machine.
`Debug|x64` was also verified to build and launch successfully after the 64-bit compatibility fixes in this repository.

## Required Components

Install either Visual Studio 2022 or Visual Studio 2022 Build Tools, then add:

- `Desktop development with C++`
- `MSVC v143 - VS 2022 C++ x64/x86 build tools`
- `C++ MFC for v143 build tools (x86 & x64)`
- A Windows SDK

## Open In Visual Studio

Open:

- `CrystalTile2.sln`

Use this configuration first:

- Configuration: `Debug`
- Platform: `x86`

The solution maps `x86` to the project's `Win32` target.

## Command Line Build

Build from a Visual Studio Developer Command Prompt, or initialize one with `VsDevCmd.bat`.

Example:

```powershell
cmd.exe /d /s /c '"C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\Common7\Tools\VsDevCmd.bat" -arch=x86 && msbuild CrystalTile2.sln /t:Build /p:Configuration=Debug /p:Platform=x86 /m'
```

## Build Output

Successful `Debug|x86` output:

- `Debug\CrystalTile2.exe`

Successful `Debug|x64` output:

- `x64\Debug\CrystalTile2.exe`

## Notes

- The project uses MFC dynamically.
- `CrystalTree` exists as a separate project under `CrystalTree\`, but the top-level solution currently builds `CrystalTile2`.
- This repository contains older source and resource files, so some compiler warnings are expected on modern toolchains.

## Known Warnings

Current successful builds may still show warnings such as:

- deprecated `Gm` usage
- pointer truncation warnings such as `LPWSTR` to `WORD`
- formatting mismatches involving `CString`
- source encoding warnings on older files

These warnings do not currently block a successful `Debug|x86` build.
