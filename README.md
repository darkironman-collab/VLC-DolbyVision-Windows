# VLC Dolby Vision for Windows

Windows x64 VLC build pipeline with Dolby Vision stream detection, profile-aware decoder routing, Media Foundation/P010 handling, FFmpeg fallback, and an Energy Media Player-inspired settings menu.

## Included controls

- Dolby Vision decoding on/off
- Auto, Microsoft Media Foundation, Windows codec extension, FFmpeg/D3D11VA, and software decode modes
- Profile override: Auto, 4, 5, 7, 8.1, 8.2, 8.4, and 9
- Force-play fallback and HDR10/HLG base-layer fallback
- In-player detected-profile popup
- Live video-decoder restart when routing settings change

## Build

The GitHub Actions workflow checks out the VLC source baseline, applies the versioned patch, verifies all Dolby Vision integration points, and builds a Windows x64 artifact in the official VideoLAN CI image.

Before an artifact is uploaded, CI downloads Jellyfin's Creative Commons
1080p Dolby Vision Profile 5 test clip, verifies its published SHA-256 and
`dvh1`/RPU signalling, then plays it with the newly built Windows VLC under
Wine. The artifact is accepted only when VLC logs the exact Profile 5 popup
submission. Both validation logs are included with the Windows packages.

> The VLC popup reports that Dolby Vision metadata was detected. A television or laptop panel's native Dolby Vision indicator still depends on the licensed Windows decoder, GPU driver, certified display, and active output path.
