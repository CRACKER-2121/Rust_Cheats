A professional-grade DLL injection framework for Rust with menu system and cheat features.

## 🚀 Quick Start

1. **Build the Project**
   - Open `RustHack.sln` in Visual Studio 2019+
   - Select x64 Release configuration
   - Press Ctrl+Shift+B to build

2. **Setup**
   - Copy `RustHack.dll` to same folder as `Injector.exe`
   - Both should be in `bin/Release/x64/`

3. **Run**
   ```
   Injector.exe
   ```
   - Choose option 2 to auto-find Rust
   - Or option 1 to manually enter process ID

4. **Use**
   - Press **INSERT** to toggle menu
   - Press **DELETE** to unload
   - Use **1**, **2**, **3** to toggle features

## 📋 What's Included

### Core Features
✅ **DLL Injection** - Inject into Rust process safely  
✅ **Menu System** - Console-based + ImGui-ready structure  
✅ **ESP** - Display player positions  
✅ **Wallhack** - See through walls  
✅ **Speed Hack** - Increase movement speed (1-5x)  

### Supporting Systems
✅ **Memory Utilities** - Pattern scanning, read/write operations  
✅ **Hooking System** - Generic function hooking framework  
✅ **Direct3D Rendering** - Hook into game rendering pipeline  
✅ **Logging System** - Comprehensive file and console logging  
✅ **Configuration** - Easy-to-modify settings and hotkeys  

### Developer Tools
✅ **Clean Architecture** - Modular, easy to extend  
✅ **Complete Documentation** - Multiple guides included  
✅ **Build System** - Pre-configured Visual Studio projects  
✅ **Example Implementations** - Advanced guide with code examples  

## 📂 Project Structure

```
RustHack/
├── RustHack.sln              Main solution file
├── COMPILE.md                Build instructions (READ THIS FIRST!)
├── BUILD_GUIDE.md            Detailed build guide
├── SETUP.md                  Project setup instructions
├── README.md                 This file
│
├── Injector/                 Injector application
│   ├── Injector.cpp          Smart DLL injector
│   └── Injector.vcxproj      Visual Studio project
│
└── DLL/                      Main hack DLL
    ├── include/              Headers
    │   ├── Menu.h            Menu system
    │   ├── Features.h        Cheat features
    │   ├── Hooks.h           Function hooks
    │   ├── Utils.h           Utilities
    │   ├── Memory.h          Memory operations
    │   ├── Render.h          D3D rendering
    │   ├── Config.h          Configuration
    │   └── AdvancedGuide.h   Implementation examples
    ├── src/                  Implementations
    │   ├── dllmain.cpp       DLL entry point
    │   ├── Menu.cpp
    │   ├── Features.cpp
    │   ├── Hooks.cpp
    │   ├── Utils.cpp
    │   ├── Memory.cpp
    │   └── Render.cpp
    └── DLL.vcxproj           VS DLL project
```

## 🎮 In-Game Controls

| Key | Action |
|-----|--------|
| INSERT | Toggle menu on/off |
| DELETE | Unload hack and exit |
| 1 | Toggle ESP |
| 2 | Toggle Wallhack |
| 3 | Toggle Speed Hack |
| W | Increase speed multiplier (when enabled) |
| S | Decrease speed multiplier (when enabled) |

## 🔧 Features

### ESP (Enemy Spotting)
- Shows player positions and information
- Customizable range
- Player name display
- Health status indicator

### Wallhack
- Renders players through walls
- Transparent rendering mode
- Customizable opacity
- Works with ESP combined

### Speed Hack
- Adjustable multiplier (1.0x to 5.0x)
- Smooth speed transitions
- Real-time adjustment with W/S keys
- Three movement directions

## 💻 System Requirements

- **OS**: Windows 10/11 (64-bit)
- **Rust**: 64-bit version (required)
- **RAM**: 4GB minimum
- **Compiler**: Visual Studio 2019+ Community Edition (free)

## 🏗️ Building from Source

### Quick Build
```bash
# Open in Visual Studio
1. Open RustHack.sln
2. Select x64 Release configuration
3. Press Ctrl+Shift+B
4. Copy RustHack.dll next to Injector.exe
5. Run Injector.exe
```

### Command Line Build
```batch
cd RustHack\DLL
cl /LD /O2 /EHsc src\*.cpp /I include /Fe:RustHack.dll ^
    /link d3d9.lib kernel32.lib user32.lib psapi.lib

cd ..\Injector
cl /O2 /EHsc Injector.cpp /link kernel32.lib user32.lib psapi.lib
```

See `COMPILE.md` for detailed instructions.

## ⚙️ Configuration

Edit `DLL\include\Config.h` to customize:

```cpp
#define HOTKEY_MENU_TOGGLE VK_INSERT      // Change menu key
#define DEFAULT_SPEED_MULTIPLIER 1.5f      // Default speed
#define MAX_SPEED_MULTIPLIER 5.0f          // Maximum speed
// ... more settings
```

## 📖 Documentation

- **COMPILE.md** - How to build the project
- **BUILD_GUIDE.md** - Detailed build steps
- **SETUP.md** - Project setup and quick start
- **AdvancedGuide.h** - Code examples and advanced implementation patterns

## 🎓 How It Works

### DLL Injection Process
1. **Injector.exe** finds Rust process
2. Allocates memory in Rust process
3. Writes DLL path to allocated memory
4. Creates remote thread with LoadLibraryA
5. Rust loads `RustHack.dll`

### DLL Initialization
1. DllMain called with DLL_PROCESS_ATTACH
2. Allocate console for logging
3. Create main thread for menu/features
4. Create unload monitor thread
5. Initialize all subsystems (rendering, hooking, features)

### Feature Execution
1. Main thread loops continuously
2. Checks for hotkey presses
3. Updates enabled features
4. Renders menu/overlay
5. Unload thread checks for DELETE key

## 🔍 Finding Memory Offsets

Each Rust update changes memory offsets. To update them:

1. **Download Cheat Engine** from cheatengine.org
2. **Open Rust process** in Cheat Engine
3. **Search for values**:
   - Search for player health (numeric value)
   - Narrow down results by changing value in game
   - Find associated structures
4. **Update Code**:
   - Edit `DLL\include\Config.h`
   - Update offset constants
   - Recompile

See `AdvancedGuide.h` for detailed examples.

## 🚨 Important Notes

- **EasyAntiCheat** may detect this hack
- **Use at your own risk** on official servers
- **For educational purposes only** - understand how game hacking works
- **Don't grief players** - keep it fun for everyone
- **Update offsets regularly** when Rust patches

## 🐛 Troubleshooting

**Build Error: "Cannot open source file"**
- Check all file paths
- Verify `#include` paths are correct
- Make sure all .cpp and .h files are present

**Injection Failed: "Access Denied"**
- Run Injector.exe as Administrator
- Close any antivirus that might block it
- Make sure Rust is running

**DLL Loads but Features Don't Work**
- Memory offsets are outdated
- Use Cheat Engine to find new offsets
- Update Config.h with new values

**Menu Not Showing**
- Check console window (opens automatically)
- Use hotkeys to toggle features
- Check log file at `C:\RustHack.log`

See `COMPILE.md` for more troubleshooting.

## 📦 Distribution

To share the compiled hack:

1. Create folder: `RustHack_Release/`
2. Copy: `RustHack.dll`, `Injector.exe`
3. Add: README with usage instructions
4. Zip and share

## 🔐 Security Practices

- Always scan compiled DLL with antivirus
- Don't trust unknown builds - compile yourself
- Keep memory unsafe code isolated
- Use try-catch blocks around all memory operations
- Log all major operations for debugging

## 🤝 Contributing

To add features:

1. Create new `.h` file in `include/`
2. Create matching `.cpp` in `src/`
3. Include in dllmain initialization
4. Add hotkeys to Config.h
5. Update documentation

## 📚 Learning Resources

- **Game Hacking**: Search "game hooking C++"
- **Memory Hacking**: Cheat Engine tutorials
- **Win32 API**: Microsoft official documentation
- **Reverse Engineering**: IDA Pro, Ghidra
- **IL2CPP**: dnSpy for .NET inspection

## 💬 Support

Check these files for help:
- `COMPILE.md` - Build issues
- `SETUP.md` - Setup questions  
- `AdvancedGuide.h` - Code examples
- Log file at `C:\RustHack.log`

## 📄 License

Educational use only. Modify as needed for learning purposes.

## 🎉 Credits

Built as a complete learning project demonstrating:
- DLL injection techniques
- Game hooking and patching
- Memory manipulation
- Win32 API usage
- Professional C++ architecture

---

**Last Updated**: March 2026  
**Version**: 1.0  
**Status**: Ready to Compile and Run

**Happy Hacking!** 🚀
