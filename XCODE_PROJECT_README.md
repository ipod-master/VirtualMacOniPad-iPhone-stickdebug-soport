# Virtual Mac - Xcode Project

This is a complete Xcode project for building Virtual Mac for iPhone and iPad with StickDebug JIT support.

## Quick Start

```bash
# Clone the repo
git clone https://github.com/ipod-master/VirtualMacOniPad-iPhone-stickdebug-soport.git
cd VirtualMacOniPad-iPhone-stickdebug-soport

# Open in Xcode
open VirtualMac.xcodeproj
```

## What's Included

✅ **Full Xcode Project** (`VirtualMac.xcodeproj/`)
- `project.pbxproj` - Complete build configuration
- `xcshareddata/xcschemes/VirtualMac.xcscheme` - Build scheme
- `project.xcworkspace/` - Workspace metadata

✅ **iOS/iPadOS 14.0+ Support**
- iPhone (14 Pro / 14 Pro Max)
- iPad (Pro M1/M2, Air M1)
- Minimum deployment target: **iOS 14.0**

✅ **StickDebug JIT Enabled**
- Preprocessor flag: `ENABLE_JIT_SUPPORT=1`
- Preprocessor flag: `ENABLE_STICKDEBUG=1`
- Runtime JIT detection ready

✅ **Jailbreak Signing**
- Automatic ldid post-build signing
- Full entitlements for Hypervisor/Virtualization
- Platform application privileges

✅ **All Frameworks Linked**
- UIKit, Foundation, Virtualization
- WebKit, AVFoundation, QuartzCore
- CoreImage, Metal

## Building

### Debug (for development)

1. Select **VirtualMac** scheme
2. Connect iPhone/iPad
3. Press **Build & Run** (Cmd+R)

### Release (for IPA export)

1. Select **Product > Archive**
2. Follow Xcode's export dialog
3. Choose **Custom** for sideloading
4. Export as `.ipa`

## Project Structure

```
VirtualMac.xcodeproj/
├── project.pbxproj                    # Build configuration
├── xcshareddata/
│   └── xcschemes/
│       └── VirtualMac.xcscheme       # Build scheme
└── project.xcworkspace/
    └── contents.xcworkspacedata      # Workspace config

VirtualMac/                           # Source root
└── vz/
    └── host/
        ├── VirtualMacApp.m           # Main app
        ├── VZAppSettings.m
        ├── VZDiagnostics.m
        ├── VZSupport.m
        ├── VZGuestRuntimePolicy.m
        ├── VirtualMac-Info.plist     # App config
        ├── VirtualMac.entitlements   # Jailbreak entitlements
        └── VirtualMacLaunchScreen.storyboard
```

## Key Build Settings

| Setting | Value |
|---------|-------|
| **Deployment Target** | iOS 14.0 |
| **Device Family** | iPhone, iPad |
| **Code Sign Identity** | iPhone Developer |
| **JIT Support** | Enabled |
| **StickDebug** | Enabled |
| **Entitlements** | `VirtualMac.entitlements` |
| **Signing Script** | ldid post-build phase |

## Preprocessor Flags

```
DEBUG=1                  (Debug config only)
ENABLE_JIT_SUPPORT=1     (All configs)
ENABLE_STICKDEBUG=1      (All configs)
MIN_IOS_VERSION=14       (All configs)
```

## Requirements

- **Xcode 15.4+** with iOS SDK
- **macOS 12.0+** for building
- **ldid** (optional but recommended for jailbreak signing)
  ```bash
  brew install ldid
  ```

## Signing & Deployment

### For Jailbreak Devices (StickDebug)

1. Jailbreak your device (Dopamine/Sileo recommended)
2. Build and run with Xcode
3. ldid automatically signs the app bundle with jailbreak entitlements
4. App launches directly on jailbroken device

### For Sideloading (TrollStore/AltStore)

1. **Product > Archive**
2. Click **Distribute App**
3. Select **Custom** or **Ad Hoc**
4. Choose your signing certificate
5. Export `.ipa`
6. Deploy with TrollStore or AltStore

## Troubleshooting

**Error: ldid not found**
```bash
brew install ldid
```

**Error: Invalid entitlements**
- Verify `VirtualMac.entitlements` exists and is readable
- Check file path in Xcode build settings

**Build fails on framework linking**
- Update Xcode: `xcode-select --install`
- Verify iOS SDK: Check Xcode Preferences > Locations

**Device not showing in build target**
- Unlock device and tap "Trust" when prompted
- Restart Xcode and disconnect/reconnect device

## Next Steps

1. ✅ Open `VirtualMac.xcodeproj` in Xcode
2. ✅ Set your Team ID (or disable signing)
3. ✅ Connect iPhone/iPad running iOS 14+
4. ✅ Build and run with Cmd+R
5. ✅ Archive for IPA export with Cmd+B then Product > Archive

## Additional Resources

- [Xcode Building Guide](https://developer.apple.com/documentation/xcode)
- [iOS Entitlements Reference](https://developer.apple.com/documentation/bundleresources/entitlements)
- [Virtual Mac Original Project](https://github.com/nfzerox/VirtualMacOniPad)
- [ldid on GitHub](https://github.com/kabiroberai/ldid)

## License

MIT - See LICENSE file
