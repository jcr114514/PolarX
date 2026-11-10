# PolarX

PolarX is a personal, non-commercial Minecraft Java launcher for Windows.

It is built for learning, personal use, and experimenting with a clean, custom-drawn WinForms UI. It is not affiliated with Mojang Studios or Microsoft.

> **Project status:** Microsoft OAuth and Xbox Live authentication are implemented. A Minecraft Services API access request has been submitted for the public client ID used by PolarX. Until that request is approved, online Microsoft login may return `Invalid app registration`. Offline accounts continue to work normally.

## Features

- Microsoft account login using OAuth 2.0 Authorization Code + PKCE
- Xbox Live user authentication and XSTS authorization
- Minecraft profile lookup and Java Edition launch
- Offline accounts with deterministic local UUIDs
- Authlib-Injector / Yggdrasil third-party account login
- Vanilla, Fabric, Forge, NeoForge, Quilt, and OptiFine version support
- Modrinth, CurseForge, and MC百科 (mcmod) download sources
- Mod management, resource packs, shader packs, and save management
- Version isolation, memory settings, and custom JVM arguments
- Light and dark themes with a custom rounded UI
- Local account persistence with Windows DPAPI token protection

## Authentication and API usage

PolarX uses the standard Microsoft public-client flow. No client secret is embedded in the application.

```text
Microsoft OAuth 2.0 Authorization Code + PKCE
  → Xbox Live user authentication
  → XSTS authorization
  → Minecraft Services login_with_xbox
  → Minecraft profile
```

Scopes:

```text
XboxLive.signin offline_access
```

Minecraft Services is used only to authenticate the signed-in user, read that user's own profile, and launch Minecraft Java Edition. PolarX does not operate a token relay, does not proxy account tokens, and does not share access tokens with a third-party server.

Third-party accounts use the Yggdrasil API and authlib-injector. Passwords are never stored. Access tokens are encrypted locally with Windows DPAPI.

## Privacy and security

- Account tokens are stored on the local Windows machine using Windows DPAPI.
- Passwords are kept in memory only for the duration of a login request.
- PolarX does not operate a remote account database or token server.
- The launcher writes local logs to help diagnose startup and download failures.
- Opening the Microsoft login page uses the system browser and a local loopback callback on `http://localhost`.

## Build

Requirements:

- Windows 10 or Windows 11
- .NET 8 SDK
- .NET 8 Desktop Runtime for running a framework-dependent build

Build:

```powershell
dotnet build .\src\PolarX.App\PolarX.App.csproj -c Release
```

Publish a Windows x64 single-file build:

```powershell
dotnet publish .\src\PolarX.App\PolarX.App.csproj `
  -c Release -r win-x64 --self-contained false `
  -p:PublishSingleFile=true -p:DebugType=None `
  -o .\artifacts\publish
```

## FAQ

### Why does Microsoft login return `Invalid app registration`?

Minecraft Services currently requires third-party applications to be registered in its API allowlist. A new Entra application cannot call `/authentication/login_with_xbox` until the request is approved, even when OAuth, Xbox Live, and XSTS all succeed.

### Can I use PolarX offline?

Yes. Offline accounts are local and do not require a Microsoft account or Minecraft Services access.

### Does PolarX store my Microsoft password?

No. The password is used only for the browser-based Microsoft login and is not saved by PolarX.

### Does PolarX share my access token?

No. Tokens are stored locally and are sent only to the Microsoft, Xbox, and Minecraft endpoints required for authentication.

## Contact

For questions about PolarX or its API usage, please open an issue in this repository.

