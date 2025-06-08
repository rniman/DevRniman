# DevRniman Engine

A personal portfolio project showcasing a modern DirectX 12 game engine built with C++17, designed for high-performance graphics programming and real-time rendering applications.

> **⚠️ Development Status**: This project is currently in **early development phase**. The features and architecture described below represent the planned roadmap and target implementation.

## 🎯 Project Overview

This is a **personal portfolio project** demonstrating expertise in:
- **Modern Graphics Programming**: DirectX 12 API mastery
- **Engine Architecture**: Clean, modular design patterns
- **C++ Best Practices**: Modern C++17 features and conventions
- **Real-time Rendering**: Performance-optimized graphics pipeline
- **Software Engineering**: Professional development workflows

The engine serves as a practical showcase of advanced graphics programming concepts and software architecture skills.

### 🚧 Current Development Status
- **Phase**: Initial architecture and foundation setup
- **Progress**: Core project structure and conventions established
- **Next Steps**: DirectX 12 device initialization and basic rendering pipeline
- **Target**: Fully functional engine with sample applications

## 🚀 Planned Technical Features
- **DirectX 12 Core**: Full DirectX 12 API integration with modern rendering pipeline
- **Cross-Platform Foundation**: Platform abstraction layer ready for future expansion
- **Modern C++**: Built with C++17 standards, smart pointers, and RAII principles
- **Sample Projects**: Ready-to-run examples demonstrating engine capabilities
- **Development Tools**: Integrated shader compiler, asset converter, and resource packer

## 📁 Planned Project Structure

```
DevRniman/
├── Engine/                          # Core engine modules
│   ├── Core/                        # Basic systems, memory management
│   ├── Graphics/                    # DirectX 12 rendering core
│   └── Math/                        # Mathematics library
├── Platform/                        # Platform abstraction & Windows implementation
├── Samples/                         # Example projects
│   ├── HelloTriangle/
│   ├── BasicLighting/
│   └── TextureMapping/
├── Tools/                          # Development utilities
├── Assets/                         # Shared resources
└── external/                       # Third-party libraries
```

## 🛠️ Prerequisites

### System Requirements
- **OS**: Windows 10/11 (64-bit)
- **GPU**: DirectX 12 compatible graphics card
- **RAM**: 8GB minimum, 16GB recommended

### Development Environment
- **Visual Studio 2022** (Community, Professional, or Enterprise)
- **Windows SDK 10.0.19041.0** or later
- **DirectX 12 Agility SDK** (included in external/)
- **Git** for version control

### Required Components
- MSVC v143 compiler toolset
- Windows 10/11 SDK
- CMake 3.20+ (optional, for future build system)

## 🚀 Getting Started (Development Phase)

> **Note**: As this project is in early development, some features may not be fully implemented yet.

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/DevRniman.git
cd DevRniman
```

### 2. Open in Visual Studio
1. Open `DevRniman.sln` in Visual Studio 2022
2. Set build configuration to `Debug` or `Release`
3. Set platform to `x64`
4. Build the solution (`Ctrl+Shift+B`)

### 3. Current Implementation Status
- ✅ **Project Structure**: Solution and project files configured
- ✅ **Coding Conventions**: Established and documented (continuously updated)
- 🚧 **Core Systems**: Basic framework in development
- 🚧 **DirectX 12 Integration**: Device initialization in progress
- ⏳ **Sample Projects**: Planned for future implementation

## 🏗️ Development Roadmap

### Phase 1: Foundation (Current)
- [x] Project structure and build system
- [x] Coding conventions and documentation (ongoing updates)
- [ ] Core logging and assertion systems
- [ ] Basic memory management framework

### Phase 2: Graphics Core
- [ ] DirectX 12 device initialization
- [ ] Command queue and allocator setup
- [ ] Basic resource management (buffers, textures)
- [ ] Descriptor heap management

### Phase 3: Rendering Pipeline
- [ ] Shader compilation and management
- [ ] Basic mesh rendering
- [ ] Constant buffer implementation
- [ ] Multi-frame resource handling

### Phase 4: Sample Applications
- [ ] HelloTriangle: Basic triangle rendering
- [ ] BasicLighting: Phong lighting model
- [ ] TextureMapping: Texture sampling and UV coordinates

### Phase 5: Advanced Features
- [ ] Asset loading pipeline
- [ ] Material system
- [ ] Scene management
- [ ] Performance optimization

## 📚 Planned Engine Architecture

> **Note**: The architecture described below represents the target design. Implementation is ongoing.

### Core Modules (In Development)

#### Engine/Core
- **Logger**: Centralized logging system
- **Assert**: Debug assertion macros
- **Memory**: Custom allocators and memory management
- **Timer**: High-precision timing utilities

#### Engine/Graphics
- **DirectX 12 Wrapper**: Modern D3D12 API abstraction
- **Command Queue Management**: Multi-threaded command recording
- **Resource Management**: Buffers, textures, and descriptor heaps
- **Render Pipeline**: PSO caching and state management

#### Engine/Math
- **Vector Classes**: Vector2, Vector3, Vector4
- **Matrix Operations**: Matrix3x3, Matrix4x4
- **Quaternions**: Rotation and orientation
- **Utility Functions**: Common mathematical operations

#### Platform Layer
- **Window Management**: Cross-platform window creation
- **Input Handling**: Keyboard, mouse, and gamepad input
- **Application Framework**: Main loop and event handling

### Namespace Organization
```cpp
namespace rniman {
    namespace core { /* Core systems */ }
    namespace graphics {
        namespace dx12 { /* DirectX 12 specific */ }
    }
    namespace math { /* Mathematics */ }
    namespace platform {
        namespace windows { /* Windows specific */ }
    }
}
```

## 🎮 Planned Sample Projects

> **Status**: These samples are part of the development roadmap and will be implemented in future phases.

### HelloTriangle (Phase 4)
**Target features**:
- Device initialization
- Command queue setup
- Basic vertex buffer creation
- Simple shader pipeline

### BasicLighting (Phase 4)
**Target features**:
- Constant buffer usage
- Basic Phong lighting model
- Texture sampling
- Multiple render targets

### TextureMapping (Phase 4)
**Target features**:
- Texture loading and binding
- UV coordinate mapping
- Multiple texture units
- Basic material system

## 🔧 Development Guidelines

### Code Style
- **Naming**: PascalCase for classes, camelCase for variables
- **Member Variables**: `m` prefix (e.g., `mDevice`)
- **Static Variables**: `s` prefix (e.g., `sInstanceCount`)
- **Global Variables**: `g` prefix (e.g., `gRenderer`)

### Memory Management
- Use smart pointers (`std::unique_ptr`, `std::shared_ptr`)
- DirectX COM objects with `Microsoft::WRL::ComPtr`
- RAII principles throughout

### Git Workflow
Follow our [Git Convention](Git_Commit_Convention_Eng.md):
```bash
[Add] Implement command queue and swap chain
[Fix] Prevent crash on window resize
[Refactor] Separate frame resource logic into class
```

### Documentation
- **Detailed Coding Standards**: 
  - [Code_Convention_Kor.md](Code_Convention_Kor.md) (Korean)
  - ⏳ Code_Convention_Eng.md (English - planned)
- **Git Commit Guidelines**: 
  - [Git_Commit_Convention_Eng.md](Git_Commit_Convention_Eng.md) (English)
  - [Git_Commit_Convention_Kor.md](Git_Commit_Convention_Kor.md) (Korean)

## 🛠️ Tools

### Shader Compiler
Compiles HLSL shaders to bytecode:
```bash
Tools/ShaderCompiler/ShaderCompiler.exe -vs VertexShader.hlsl -ps PixelShader.hlsl
```

### Asset Converter
Converts 3D models to engine format:
```bash
Tools/AssetConverter/AssetConverter.exe model.fbx -o model.asset
```

### Resource Packer
Packages assets for distribution:
```bash
Tools/ResourcePacker/ResourcePacker.exe Assets/ -o GameAssets.pak
```

## 📖 Documentation

### API Reference
- [Graphics API Documentation](docs/Graphics.md)
- [Math Library Reference](docs/Math.md)
- [Platform Layer Guide](docs/Platform.md)

### Tutorials
- [Getting Started with DevRniman](docs/tutorials/GettingStarted.md)
- [Creating Your First Scene](docs/tutorials/FirstScene.md)
- [Advanced Rendering Techniques](docs/tutorials/AdvancedRendering.md)

## 🤝 About This Project

This DirectX 12 engine represents a **personal learning journey** and **portfolio showcase** in advanced graphics programming. The project demonstrates:

- **Technical Planning**: Comprehensive architecture design and development roadmap
- **Professional Standards**: Industry-standard coding conventions and project structure
- **Progressive Development**: Methodical implementation approach with clear milestones
- **Continuous Learning**: Exploration of cutting-edge real-time graphics techniques

**Current Focus**: Establishing solid foundation and core systems before advancing to complex rendering features.

Feel free to follow the development progress, explore the planned architecture, and reach out with questions or feedback!

## 🐛 Current Limitations

> **Note**: As this project is in early development phase, the following limitations are expected and will be addressed as development progresses.

- **Core Systems**: Basic engine systems are not yet implemented
- **Rendering**: DirectX 12 rendering pipeline is in development
- **Samples**: No runnable sample applications yet available
- **Tools**: Development tools are planned for future implementation
- **Documentation**: API documentation will be created alongside implementation

### Next Milestones
1. **Core System Implementation**: Logger, Assert, and Memory management
2. **DirectX 12 Foundation**: Device, command queue, and basic resource setup
3. **First Render**: Simple triangle rendering implementation

## 📊 Performance

### Rendering Performance
- **Target**: 60 FPS at 1080p on GTX 1060 or better
- **Optimization**: Multi-threaded command recording
- **Memory**: Optimized descriptor heap management

### Build Times
- **Clean Build**: ~2-3 minutes on modern hardware
- **Incremental**: ~10-30 seconds depending on changes

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Microsoft**: DirectX 12 API and documentation
- **DirectX Tool Kit**: Inspiration for math library design
- **Dear ImGui**: Integrated for development UI (planned)
- **Community**: All contributors and testers

## 📞 Contact & Feedback

- **Issues**: [GitHub Issues](https://github.com/rniman/DevRniman/issues)
- **Portfolio**: [Rniman Blog](https://rniman.github.io/)
- **Email**: shinmg00.email@gmail.com

I welcome feedback, questions, and discussions about graphics programming and engine development!

---

**DevRniman Engine** - A personal portfolio project showcasing modern DirectX 12 graphics programming planning and progressive development approach.