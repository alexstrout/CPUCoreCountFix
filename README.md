# CPU Core Count Fix (32 & 64-bit)

x64-compatible fork of [adrian-lebioda/SpaceMarineCoreFix](https://github.com/adrian-lebioda/SpaceMarineCoreFix) - itself inspired by [maximumgame/DOW2CoreFix](https://github.com/maximumgame/DOW2CoreFix) - for games that have issues with high-end multicore processors (e.g. 16 or more cores) and happen to use DirectInput 8.

This DLL uses [Microsoft Detours](https://github.com/microsoft/Detours) to limit the return values of [GetSystemInfo](https://learn.microsoft.com/en-us/windows/win32/api/sysinfoapi/nf-sysinfoapi-getsysteminfo) and [GetLogicalProcessorInformation](https://learn.microsoft.com/en-us/windows/win32/api/sysinfoapi/nf-sysinfoapi-getlogicalprocessorinformation) to a **maximum of 12 CPU cores**. (The true core count is still returned if fewer, in which case you would not need this fix anyway.)

## Installation

1. Download latest version from [releases](https://github.com/alexstrout/CPUCoreCountFix/releases):
   - For 64-bit apps, use **"x64"** version.
   - For 32-bit apps, use **"x86"** version.
2. Download and install **Visual Studio 2022 Redistributable**:
   - https://aka.ms/vs/17/release/vc_redist.x64.exe (64-bit apps)
   - https://aka.ms/vs/17/release/vc_redist.x86.exe (32-bit apps)
3. Copy **DINPUT8.dll** to the game executable directory. (next to game's **.exe** file)
4. Launch game!

## Limitations

- This will work only for standard Windows installation in **C:\Windows**.
- Prevents using other DINPUT8.dll hooks, unless they can specify a custom DLL path to "chain" into.
  - *Future enhancement: Read original DLL path from %SystemRoot% and make configurable?*
- Currently hard-coded to return a maximum of 12 cores to the application.
  - *Future enhancement: Make max core count configurable in case a game still has issues?*
- Tested only on 64-bit Windows, although in theory it should work on 32-bit Windows too.

## Building

Open [SpaceMarineCoreFix.sln](SpaceMarineCoreFix.sln) in Visual Studio 2022 Community and build Release version for your target platform:
- x64 (64-bit apps) - builds to x64/Release folder.
- x86 (32-bit apps) - builds to Release folder.
