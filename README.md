# PolarX

PolarX is a personal, non-commercial third-party Minecraft Java launcher.

## Purpose

PolarX signs users in with their own Microsoft account and launches Minecraft Java Edition. It is intended for personal use and learning, not for resale or commercial distribution.

## Authentication and API usage

PolarX uses Microsoft OAuth 2.0 Authorization Code + PKCE with the following scopes:

- XboxLive.signin
- offline_access

After Microsoft OAuth, it uses the Xbox Live user authentication and XSTS authorization endpoints. The Minecraft Services API is used only to:

- authenticate the signed-in user with /authentication/login_with_xbox;
- read the user's own Minecraft profile from /minecraft/profile;
- launch Minecraft Java Edition for that user.

PolarX is a public/native desktop client. It does not use a client secret, does not proxy tokens, and does not share access tokens with any third-party server.

## Privacy

Account tokens are stored only on the user's local Windows machine using Windows DPAPI. The launcher does not collect, sell, or upload account data to a developer-operated server.

## Disclaimer

PolarX is not affiliated with Mojang Studios or Microsoft.

## Contact

For questions about this project or its API usage, please open an issue in this repository.
