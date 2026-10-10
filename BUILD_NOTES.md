# Virtual Mac for iPhone - Xcode Build Guide

## Project Configuration

This Xcode project supports:
- **iPhone & iPad** (device families 1,2)
- **iOS/iPadOS 14.0+** deployment target
- **StickDebug JIT** support enabled by default
- **Jailbreak signing** with ldid (runs in post-build phase)

## Build Requirements

### macOS Environment
- Xcode 15.4 or later
- iOS 14.0+ SDK (included with Xcode)
- `ldid` for jailbreak signing (optional, but required for iOS deployment)

### Install ldid (optional, for jailbreak sideload)

```bash
brew install ldid
```

## Building the App

### Debug Build (Development)

1. Open `VirtualMac.xcodeproj` in Xcode
2. Select **VirtualMac** target
3. Select your connected iPhone or iPad in the device list
4. Press **Build** (Cmd+B) or **Run** (Cmd+R)

### Release Build (Archive for IPA)

1. Select **Product > Archive**
2. In the Organizer window, select the archive
3. Click **Distribute App**
4. Choose **Custom** for sideloading
5. Select signing certificate and export

## Code Signing

### For Jailbreak (StickDebug) Deployment

The project uses `ldid` for signing in the post-build phase:

```bash
ldid -Icom.mac.virtual -S"${SRCROOT}/VirtualMac/vz/host/VirtualMac.entitlements" "${BUILT_PRODUCTS_DIR}/${EXECUTABLE_PATH}"
```

This happens automatically after each build if `ldid` is installed.

### For App Store (Not applicable - jailbreak only)

This app requires jailbreak entitlements and cannot be signed with a standard Apple developer certificate for App Store distribution.

## Build Settings

### JIT & StickDebug Flags

These preprocessor definitions are set in both Debug and Release configurations:

```
ENABLE_JIT_SUPPORT=1
ENABLE_STICKDEBUG=1
MIN_IOS_VERSION=14
```

Use these in code:

```objc
#if ENABLE_JIT_SUPPORT
  // JIT-enabled code path
#endif

#if ENABLE_STICKDEBUG
  // StickDebug-specific debugging hooks
#endif
```

## Entitlements

The app requires extensive jailbreak entitlements (see `VirtualMac/vz/host/VirtualMac.entitlements`):

- `com.apple.security.virtualization` - VM framework access
- `com.apple.private.hypervisor` - Hypervisor kernel access
- `com.apple.private.security.no-sandbox` - Sandbox bypass (jailbreak only)
- `platform-application` - Platform app privileges
- `get-task-allow` - Debug task access
- And many others for device access

## Frameworks Linked

- UIKit - UI framework
- Foundation - Core runtime
- Virtualization - VM/hypervisor framework
- WebKit - Rendering engine
- AVFoundation - Media capture
- QuartzCore - Metal/graphics layers
- CoreImage - Image processing
- Metal - GPU compute

## Deployment Target

**iOS/iPadOS 14.0** - The oldest supported version. The app runs on:

- iPhone 14 Pro, iPhone 14 Pro Max (iOS 16.0+)
- iPad Pro M1/M2 (iPadOS 14.0+)
- iPad Air M1 (iPadOS 14.0+)

## Troubleshooting

### Build fails with missing frameworks

**Solution:** Ensure your iOS SDK includes private frameworks:

```bash
xcode-select --install
```

### ldid not found during post-build

**Solution:** Install ldid with Homebrew:

```bash
brew install ldid
```

Or download from: https://github.com/kabiroberai/ldid

### Code sign error on device

**Solution:** For jailbreak deployment, use Xcode automatic signing with your Apple ID. The actual jailbreak signing is handled by ldid in the post-build phase.

## Exporting IPA for Sideloading

1. **Product > Archive**
2. **Distribute App > Custom**
3. Choose **Development** or **Ad Hoc**
4. Select your certificate
5. Export to `.ipa`
6. Deploy using `AltStore`, `TrollStore`, or similar

## Next Steps

1. Clone the repo and open in Xcode
2. Set your Team ID in signing settings
3. Connect your iPhone/iPad
4. Build and run with Cmd+R
5. For jailbreak deployment, make sure the device is jailbroken with Dopamine/Sileo
6. Archive and export IPA for distribution

## Support

For issues:
- Check the entitlements file permissions
- Verify iOS version matches deployment target
- Ensure ldid is properly installed for jailbreak builds
- Consult the original project: https://github.com/nfzerox/VirtualMacOniPad
