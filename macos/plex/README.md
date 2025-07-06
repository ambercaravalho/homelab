# Plex Media Server

My choice video and audio library server. Installed on the host to gain access to Metal GPU drivers (for faster transcoding!). For more: [Plex](https://www.plex.tv/your-media/)

_I know [Jellyfin](https://github.com/jellyfin/jellyfin)'s open source and all, but I have one of those lifetime Plex passes, so migration can wait another day._

### 1. Install Cask

Install Plex Media Server using Brew **first**: [brew](/macos/brew/README.md)

### 2. Restore Backup

1. Hook up the [Pegasus2 DAS](/macos/pegasus/README.md) and the [Time Machine](/macos/system_settings/README.md). 

2. Copy the `~/Library/Application Support/Plex Media Server/` -> `Preferences.xml` file from Time Machine to the current machine.

3. If that's gone or broken or whatever, then I'm kinda screwed and gotta reconfigure it all. _oh well 🤷‍♀️_