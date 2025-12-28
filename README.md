 Darkest Days (ProjectNow) Advanced Manual Map Injector
 Project Overview
This repository contains a sophisticated C++ Manual Map Injector specifically engineered to interface with ProjectNow-Win64-Shipping.exe (Darkest Days), a title utilizing Unreal Engine 4.27. In modern game security, standard injection techniques—such as LoadLibrary—are easily intercepted by kernel-level anti-cheats (like EAC or XIGNCODE3). These protections often result in "Access Denied" errors or the "kernel32.dll not found" exception seen in standard tools. This project overcomes these limitations by implementing a custom memory mapping logic that bypasses the Windows Loader entirely.

 Technical Problem & Solution
Standard injectors rely on the target process to load the DLL. However, protected games hook system APIs to hide critical modules like kernel32.dll or ntdll.dll from external tools.

This injector utilizes Manual Mapping, which performs the following steps internally:

Privilege Escalation: Obtains SeDebugPrivilege to interact with high-integrity processes.

Memory Allocation: Uses VirtualAllocEx to create a dedicated space in the game's memory.

Section Mapping: Manually writes the DLL's PE headers and sections into the allocated space.

Relocation Handling: Adjusts the image base and relocates absolute addresses to ensure the code runs correctly in the new memory offset.

Import Resolution: Manually resolves the DLL’s dependencies by finding function addresses in the target's loaded modules.

Execution: Fires the DllMain entry point via thread hijacking or specialized shellcode to avoid detection by standard thread monitors.

 Key Features
Animated Terminal UI: A dynamic, wave-style "L o O a A d i N g . . ." animation provides a polished user experience.

Real-time Process Monitoring: The tool continuously scans for the game window and displays the Process ID (PID) once found.

Stealth Injection: By erasing PE headers and hiding the injected module, the detection footprint is significantly minimized compared to public injectors.

Custom Pathing: Users can input direct paths to their compiled DLLs for rapid testing and deployment.

Usage Instructions
Administrative Rights: Must be "Run as Administrator" to bypass Windows security tokens and interact with protected memory.

Environment Setup: Launch the game first. The injector will automatically hook once the process is initialized.

DLL Deployment: Enter the full directory path when prompted.

Verification: Check the console for successful mapping logs and shellcode execution status.
