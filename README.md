# Resolume QR Code Plugin

A dynamic QR code generator plugin for Resolume Arena/Avenue built with the FFGL SDK. This plugin allows real-time generation of QR codes from URL or text input with full visual customization.

## 🚀 Current Status

**✅ DEVELOPMENT COMPLETE** - Ready for Windows compilation and testing

### What's Implemented
- [x] Complete FFGL source plugin architecture
- [x] Integration with Nayuki's QR Code Generator library
- [x] Real-time QR code generation from text/URL input
- [x] OpenGL shader-based rendering pipeline
- [x] Dynamic texture generation and updates
- [x] Full color customization (foreground/background RGBA)
- [x] Size/scale controls
- [x] Error handling and logging
- [x] CMake build system integration

### Next Steps
1. **Windows Compilation** - Build `.dll` plugin using Visual Studio
2. **Resolume Testing** - Test plugin functionality in Resolume Arena/Avenue
3. **Parameter Refinement** - Adjust UI parameters based on testing
4. **Performance Optimization** - If needed based on testing results

## 🎯 Features

### Plugin Parameters
- **URL/Text**: Dynamic text input for QR code content
- **Foreground Color**: RGBA controls for QR code modules (default: black)
- **Background Color**: RGBA controls for background (default: white) 
- **Size**: Scale factor for QR code display

### Technical Features
- Real-time QR code generation using C++ library
- Efficient OpenGL texture-based rendering
- Automatic texture updates when content changes
- Shader-based color mixing and scaling
- Error correction level: Medium (suitable for most use cases)

## 🏗️ Architecture

### Project Structure
```
ffgl/source/plugins/QRCode/
├── FFGLQRCode.h          # Plugin class definition
├── FFGLQRCode.cpp        # Main implementation
├── qrcodegen.hpp         # QR generation library header  
├── qrcodegen.cpp         # QR generation library implementation
└── CMakeLists.txt        # Build configuration
```

### Technical Implementation
- **Base Class**: `CFFGLPlugin` (FFGL source plugin)
- **QR Generation**: Nayuki's QR-Code-generator (C++11, high-quality)
- **Rendering**: OpenGL 4.1 shaders with texture sampling
- **Performance**: Lazy texture generation (only on content change)

## 🔧 Compilation Instructions

### Windows (Primary Target)
1. **Prerequisites**: Visual Studio 2017 or newer
2. **Open Project**: `ffgl/build/windows/FFGLPlugins.sln`
3. **Create Target**:
   - Duplicate an existing plugin project (e.g., Gradients)
   - Rename to "QRCode" 
   - Remove old source files from project
   - Add QRCode source files to project
4. **Build**: Compile to generate `.dll` file
5. **Install**: Copy `.dll` to `%USERPROFILE%/Documents/Resolume/Extra Effects`

### macOS (Secondary)
1. **Prerequisites**: Xcode with recent version
2. **Open Project**: `ffgl/build/osx/FFGLPlugins.xcodeproj`
3. **Create Target**: Similar process to Windows
4. **Build**: Generate universal `.bundle` for ARM/Intel compatibility
5. **Install**: Copy `.bundle` to `~/Documents/Resolume/Extra Effects`

## 🧪 Testing

### Resolume Integration
1. Launch Resolume Arena/Avenue
2. Plugin appears as "QR Code Generator" in Sources
3. Drag to composition layer
4. Configure parameters in plugin panel

### Test Cases
- [ ] Basic URL encoding (e.g., "https://resolume.com")
- [ ] Long URLs and text strings
- [ ] Special characters and Unicode
- [ ] Real-time parameter updates
- [ ] Color customization
- [ ] Size scaling
- [ ] Performance with multiple instances

## 📚 Dependencies

### Included Libraries
- **FFGL SDK**: Resolume's official plugin framework
- **Nayuki QR Generator**: High-quality C++ QR code generation
- **OpenGL**: Graphics rendering (via FFGL)

### System Requirements
- **Resolume**: 7.0.3 or newer (plugin compatibility)
- **OpenGL**: 4.1+ support (for shaders)
- **Platform**: Windows 64-bit (primary), macOS universal (secondary)

## 🔬 Technical Details

### QR Code Generation Pipeline
1. **Input**: User enters URL/text via parameter
2. **Generation**: Nayuki library creates QR matrix
3. **Conversion**: Matrix converted to OpenGL texture (R8 format)
4. **Rendering**: Fragment shader samples texture and applies colors
5. **Display**: Scaled and positioned using uniforms

### Shader Implementation
- **Vertex Shader**: Handles positioning and UV scaling
- **Fragment Shader**: Texture sampling with color mixing
- **Uniforms**: Scale, foreground color, background color

### Performance Considerations
- Texture generation only on content change (`needsUpdate` flag)
- Nearest-neighbor filtering for crisp QR code pixels  
- Efficient memory usage with single-channel textures
- Error handling prevents crashes on invalid input

## 📝 Development Notes

### Key Design Decisions
- **Source Plugin Type**: Generates content rather than processing input
- **Text Parameter**: Enables dynamic URL/content input
- **Shader-Based**: Leverages GPU for efficient rendering
- **Standard FFGL Patterns**: Follows Resolume conventions for consistency

### Known Limitations
- QR complexity increases with text length (inherent to QR codes)
- Maximum text length limited by QR specification
- Requires manual recompilation for code changes

## 🤝 Contributing

### Development Environment
- Clone repository with FFGL SDK and QR generator library
- Modify source files in `ffgl/source/plugins/QRCode/`
- Test compilation before submitting changes

### Future Enhancements
- Error correction level parameter
- QR code style options (dots, rounded corners)
- Batch text processing
- Animation effects
- REST API integration for dynamic content

## 📄 License

This plugin integrates multiple components:
- **FFGL SDK**: Resolume's licensing terms
- **Nayuki QR Generator**: MIT License
- **Plugin Code**: [Specify license for plugin-specific code]

## 🔗 Resources

- [Resolume FFGL Documentation](https://github.com/resolume/ffgl)
- [Nayuki QR Generator](https://github.com/nayuki/QR-Code-generator)
- [Resolume Plugin Development Guide](https://github.com/resolume/ffgl/wiki)
- [OpenGL Reference](https://www.opengl.org/sdk/docs/man/)

---

**Status**: Ready for Windows compilation and Resolume testing  
**Last Updated**: December 2024  
**Compatibility**: Resolume 7.0.3+ (Windows/macOS 64-bit)