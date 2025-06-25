# 🚀 CS2 Bunnyhop Cheat Kernel Driver (Educational)

## 📝 Overview
This project demonstrates a **kernel-mode driver** and a **user-mode application** working together to implement a bunnyhop (auto-jump) cheat for Counter-Strike 2 (CS2). The main goal is to provide an educational resource for understanding Windows kernel development, user-kernel communication, and game memory manipulation. **This project is strictly for educational and research purposes.**

## 🏗️ Architecture
- **Kernel Driver (`km/`)**: A Windows kernel-mode driver that exposes a device interface for reading/writing memory of a target process (the game). It handles IOCTL requests for process attachment, memory read, and memory write.
- **User-Mode Application (`um/`)**: A C++ application that interacts with the driver, locates the CS2 process, resolves module and memory offsets, and implements the bunnyhop logic by reading/writing game memory.
- **Offsets/Headers**: The `um/src/client.dll.hpp` and `um/src/offsets.hpp` files contain up-to-date memory offsets and structure definitions for CS2, generated using external tools.

## ✨ Features
- 🛡️ **Kernel-level memory access**: Bypasses user-mode anti-cheat protections by reading/writing memory from kernel space.
- 🐇 **Bunnyhop automation**: Automatically triggers jumps in CS2 when the spacebar is held and the player is on the ground.
- 📚 **Educational code**: Clean, well-commented code for both kernel and user mode, suitable for learning about Windows internals, driver development, and game hacking basics.
- 🖥️ **Safe testing setup**: Designed for use with WinDbg and VMware for safe, isolated experimentation.

## 📁 Project Structure
```
Kernel_driver_cs2-main/
├── km/                # Kernel-mode driver
│   ├── src/
│   │   └── main.cpp   # Driver source code
│   ├── km.vcxproj     # Visual Studio project file
│   └── km.inf         # Driver installation info
├── um/                # User-mode application
│   ├── src/
│   │   ├── main.cpp           # Main logic for bunnyhop
│   │   ├── client.dll.hpp     # CS2 structure/offsets
│   │   └── offsets.hpp        # CS2 memory offsets
│   └── um.vcxproj     # Visual Studio project file
├── kernel_drivers.sln # Visual Studio solution
├── LICENSE            # MIT License
└── README.md          # This file
```

## ⚙️ How It Works
1. **Driver Loading**: The kernel driver is loaded (e.g., via a mapper or test signing mode) and creates a device interface.
2. **Process Attachment**: The user-mode app locates the CS2 process and attaches to it via the driver.
3. **Memory Manipulation**: The app reads player state and writes jump commands using IOCTLs to the driver, which performs kernel-level memory operations.
4. **Bunnyhop Logic**: When the spacebar is held and the player is on the ground, the app triggers a jump by writing to the appropriate memory address.

## 🛠️ Build & Usage Instructions
### 📋 Prerequisites
- 🪟 Windows 10/11 (x64)
- 🛠️ Visual Studio (with C++ and Windows Driver Kit components)
- 🐞 WinDbg and VMware (recommended for safe testing)
- 🎮 CS2 installed (for testing)

### 🏗️ Building
1. **Open `kernel_drivers.sln` in Visual Studio.**
2. **Build the `km` (kernel driver) project** for `x64` and `Release` mode.
3. **Build the `um` (user-mode) project** for `x64` and `Release` mode.

### ▶️ Running
> ⚠️ **Warning:** Running unsigned drivers on your main system is dangerous and may violate game/OS terms. Use a VM and test signing mode.

1. **Load the driver** (e.g., using a driver mapper or in test mode):
   - Enable test signing: `bcdedit /set testsigning on` (reboot required)
   - Use a driver loader tool (e.g., kdmapper) to load the driver.
2. **Start CS2** and join a game.
3. **Run the user-mode application (`um.exe`) as administrator.**
4. **Hold the spacebar** in-game to activate bunnyhop. Press `END` to exit.

## ⚠️ Safety & Legal Notice
- 🚫 **For educational use only.** Do not use on official servers or for cheating in online games.
- 🧑‍💻 **Running unsigned drivers can compromise system security.** Always use a virtual machine for testing.
- 📝 **You are responsible for any consequences of using this code.**

## 🙏 Credits
- Inspired by Cazz (YouTube) and based on public CS2 reversing resources.
- Offset dumping via [a2x/cs2-dumper](https://github.com/a2x/cs2-dumper).
- Educational driver mapping techniques from the Windows driver development community.

## 📄 License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
