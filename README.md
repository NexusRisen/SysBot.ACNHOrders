# Animal Crossing: New Horizons SysBot

[![.NET](https://img.shields.io/badge/.NET-9.0-blue.svg)](https://dotnet.microsoft.com/download)
[![Discord.Net](https://img.shields.io/badge/Discord.Net-3.17.1-7289da.svg)](https://github.com/discord-net/Discord.Net)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen.svg)]()

An **Animal Crossing: New Horizons** automation bot that uses **sys-botbase** to remotely control your Nintendo Switch console. This SysBot enables automated item drops, villager management, map editing, and visitor coordination through Discord, Twitch, and web interfaces.

## 🌟 What is ACNH SysBot?

This is a **Nintendo Switch automation bot** specifically designed for **Animal Crossing: New Horizons**. It uses the **sys-botbase** homebrew plugin to remotely control your Switch console, allowing for:

### 🎮 Switch Console Automation
- **Direct Memory Access**: Reads and writes ACNH save data in real-time
- **Input Automation**: Simulates button presses and joystick movements
- **Inventory Management**: Automatically drops items from bot's inventory to visitors
- **Game State Monitoring**: Tracks visitors, dodo codes, and island status
- **Session Management**: Handles visitor arrivals/departures automatically

### 🏝️ Animal Crossing: New Horizons Features
- **Item Drop Service**: Automatically drops requested items for visitors
- **Villager Spawning**: Places specific villagers in empty house plots
- **Map Terrain Editing**: Modifies island terrain, paths, and decorations
- **DIY Recipe Distribution**: Shares rare and seasonal crafting recipes
- **Turnip Price Automation**: Updates and shares turnip prices
- **Museum Donation Tracking**: Tracks donated items across multiple users

### 🔌 Integration Platforms
- **Discord Bot**: Queue orders and manage island through Discord server
- **Twitch Integration**: Accept orders from Twitch chat during streams  
- **Web Dashboard**: Real-time monitoring and manual controls
- **Socket API**: Custom integrations for advanced users

## 📋 Requirements

### 🎮 Nintendo Switch Setup
- **Nintendo Switch** (Original, Lite, or OLED model)
- **Animal Crossing: New Horizons** (any version/region)
- **Custom Firmware (CFW)** - Atmosphere recommended
- **sys-botbase** homebrew plugin installed and configured
- **Stable network connection** between Switch and PC

### 💻 PC/Server Requirements  
- **.NET 9.0 Runtime** ([Download](https://dotnet.microsoft.com/download/dotnet/9.0))
- **Windows 10/11, macOS, or Linux** (cross-platform compatible)
- **4GB+ RAM** recommended for optimal performance
- **Network access** to Nintendo Switch on same local network

### ⚠️ Important Prerequisites
- **Homebrew knowledge required** - This tool requires a modded Switch
- **sys-botbase setup** - Must be properly configured and running
- **ACNH save backup** - Always backup your save before using automation
- **Understanding of risks** - Using homebrew may void warranty

## 🚀 Setup Guide

### Step 1: Prepare Your Nintendo Switch

#### Install Custom Firmware
1. **Check compatibility** - Ensure your Switch can run homebrew
2. **Install Atmosphere CFW** - Follow [NH Switch Guide](https://nh-server.github.io/switch-guide/)
3. **Backup your NAND** - Create a full system backup before proceeding

#### Install sys-botbase
1. Download **sys-botbase** from [GitHub releases](https://github.com/olliz0r/sys-botbase/releases)
2. Copy `sys-botbase.nro` to `/switch/` folder on SD card
3. Copy `430000000000000B` folder to `/atmosphere/contents/`
4. Reboot Switch and launch sys-botbase from homebrew menu

#### Configure Network Settings
1. Note your **Switch IP address** (System Settings > Internet)
2. Ensure Switch and PC are on **same network**
3. Test sys-botbase connection using **sys-botbase-client**

### Step 2: Setup the ACNH SysBot

#### Download and Build
```bash
git clone https://github.com/your-username/SysBot.ACNHOrders.git
cd SysBot.ACNHOrders
dotnet restore
dotnet build --configuration Release
```

#### Initial Configuration
Run the bot once to generate configuration files:
```bash
dotnet run
```

This creates:
- `config.json` - Switch connection and Discord settings
- `twitch.json` - Twitch bot configuration  
- `server.json` - Web API and Socket server settings

### Step 3: Configure Switch Connection

#### Main Configuration (`config.json`)
```json
{
  "IP": "192.168.1.XXX",           // Your Switch IP address from Step 1
  "Port": 6000,                     // sys-botbase port (default: 6000)
  "Token": "YOUR_DISCORD_BOT_TOKEN" // Discord bot token (see next step)
}
```

#### Test Switch Connection
1. Start **Animal Crossing: New Horizons** on your Switch
2. Launch **sys-botbase** from homebrew menu
3. Run the bot: `dotnet run`
4. Look for "Connected to Switch" message in console

#### Discord Bot Setup
1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Create a new application and bot
3. Copy the bot token to `config.json`
4. Invite bot to your server with required permissions

#### Twitch Integration (`twitch.json`)
```json
{
  "Token": "YOUR_TWITCH_OAUTH_TOKEN",
  "Username": "your_bot_username",
  "Channel": "your_channel_name"
}
```

### 4. Run the Bot
```bash
dotnet run --configuration Release
```

## 📖 Usage Guide

## 🎮 How the ACNH SysBot Works

### The Automation Process

1. **Memory Reading**: Bot reads ACNH game memory through sys-botbase
2. **Input Simulation**: Sends button presses to navigate menus and drop items  
3. **Inventory Management**: Automatically spawns requested items in bot's inventory
4. **Visitor Coordination**: Manages dodo codes and tracks visitor arrivals/departures
5. **Session Control**: Handles multiple orders in queue with timing coordination

### Typical Order Flow

```
User Request → Queue System → Switch Automation → Item Drop → Visitor Pickup
     ↓              ↓               ↓               ↓            ↓
Discord/Twitch → Bot Memory → sys-botbase → ACNH Game → User Success
```

## 📱 Using the Bot

### Discord Commands

#### For Users
- `/order [items]` - Request up to 40 items to be dropped on island
- `/villager [name]` - Request a specific villager (requires empty plot)
- `/diy [recipe]` - Request DIY recipe cards
- `/queue` - Check your position in the order queue
- `/catalog [item]` - Search the bot's available item catalog

#### For Island Management
- `/dodo` - Get current dodo code for visiting
- `/visitors` - See who's currently on the island
- `/turnips` - Check current turnip buy/sell prices
- `/map` - View island map and current terraform state

#### Admin Commands (Bot Owner Only)
- `/ban [user]` - Prevent user from placing orders
- `/restart` - Restart the Switch connection
- `/clean` - Clear dropped items from island
- `/config` - Modify bot settings in real-time

### Twitch Integration
- `!order [items]` - Request items during stream
- `!queue` - Check queue position
- `!dodo` - Get dodo code (if streamer enables public access)
- `!catalog [search]` - Search available items

### Order Examples
```
/order 10 nook mile ticket, 5 star fragment, 1 royal crown
/villager Raymond
/diy ironwood dresser, ironwood kitchenette
```

## 🔧 Advanced Configuration

### Item Validation
Configure which items can be ordered:
```json
{
  "AllowedItems": ["*"],          // "*" for all items or specific item list
  "MaxItemsPerOrder": 40,         // Maximum items per order
  "MaxOrdersPerUser": 1           // Orders per user in queue
}
```

### Security Settings
```json
{
  "RequireValidation": true,      // Require order validation
  "GlobalBanList": true,          // Use community ban list
  "RateLimitOrders": 300,         // Seconds between orders per user
  "MaxVisitors": 7                // Maximum concurrent visitors
}
```

### Performance Tuning
```json
{
  "ConnectionTimeoutMs": 30000,   // Switch connection timeout
  "OrderTimeoutMs": 300000,       // Order completion timeout
  "CleanupIntervalMs": 60000,     // Cleanup check interval
  "MaxQueueSize": 100             // Maximum queue size
}
```

## 🛠️ Development

### Building from Source
```bash
# Clone repository
git clone https://github.com/your-username/SysBot.ACNHOrders.git
cd SysBot.ACNHOrders

# Restore dependencies
dotnet restore

# Build project
dotnet build

# Run tests
dotnet test

# Create release build
dotnet publish -c Release -o ./publish
```

### Project Structure
```
SysBot.ACNHOrders/
├── Bot/                    # Core bot logic
│   ├── CrossBot.cs        # Main bot controller
│   ├── Config/            # Configuration classes
│   └── Helpers/           # Utility classes
├── Discord/               # Discord integration
│   ├── SysCord.cs        # Discord client handler
│   └── Modules/          # Discord command modules
├── Twitch/               # Twitch integration
├── SocketAPI/            # Web API endpoints
├── Util/                 # Shared utilities
└── Tests/                # Unit tests
```

### Contributing
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 🆘 Troubleshooting

### Common ACNH SysBot Issues

#### sys-botbase Connection Problems
- ✅ **Check homebrew setup** - Ensure sys-botbase is properly installed
- ✅ **Verify Switch IP** - IP address may change after reboot
- ✅ **Network connectivity** - Switch and PC must be on same subnet
- ✅ **sys-botbase status** - Must be running and showing "Waiting for connection"
- ✅ **Firewall settings** - Ensure port 6000 is not blocked

#### Animal Crossing Game State Issues
- ✅ **Game must be running** - ACNH should be loaded and at the main island
- ✅ **No menus open** - Bot can't work when in NookPhone, inventory, or dialogs
- ✅ **Airport closed** - Gates must be closed when bot starts (it will open them)
- ✅ **Player position** - Character should be in open area, not inside buildings
- ✅ **Save corruption** - Always backup saves before using memory modification

#### Order Processing Problems  
- ✅ **Inventory space** - Bot's inventory must have room for requested items
- ✅ **Item availability** - Some items may not be spawnable or have restrictions
- ✅ **Visitor limits** - Too many visitors can cause connection issues
- ✅ **Order format** - Check item names match internal ACNH database

#### Performance and Timing Issues
- ✅ **Network latency** - Slow connections may cause timeouts
- ✅ **Switch performance** - Overheating or low battery can cause issues  
- ✅ **Memory usage** - Monitor bot memory usage for memory leaks
- ✅ **Queue overload** - Limit concurrent orders to prevent bottlenecks

### Debug Mode
Enable detailed logging by setting environment variable:
```bash
export SYSBOT_DEBUG=true
dotnet run
```

### Getting Help
- 📚 Check the [Wiki](../../wiki) for detailed guides
- 🐛 Report bugs in [Issues](../../issues)
- 💬 Join our [Discord Community](https://discord.gg/your-invite)
- 📧 Contact maintainers for urgent issues

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **SysBot.Base** - Core Nintendo Switch automation framework
- **NHSE** - Animal Crossing save editing libraries
- **Discord.Net** - Discord API wrapper for .NET
- **TwitchLib** - Twitch API integration
- **Community Contributors** - Thanks to everyone who helped improve this project

## ⚠️ Important Disclaimers

### Legal and Safety Warnings

**This is homebrew software that modifies Nintendo Switch firmware and Animal Crossing: New Horizons save data.**

- 🚨 **Warranty Void**: Using custom firmware **voids your Nintendo Switch warranty**
- 🚨 **Ban Risk**: Nintendo may **ban your console** from online services if detected
- 🚨 **Save Corruption**: Memory editing can **corrupt your ACNH save file**
- 🚨 **Educational Use**: This software is for **educational and research purposes only**

### Prerequisites and Responsibilities

- ✅ **Backup Everything**: Always backup NAND and save files before use
- ✅ **Understand Risks**: You accept full responsibility for any consequences
- ✅ **Technical Knowledge**: Requires understanding of Switch homebrew
- ✅ **Legal Compliance**: Follow all applicable laws and terms of service

### Nintendo Terms of Service

This software may violate Nintendo's Terms of Service. Users are responsible for:
- Understanding legal implications in their jurisdiction
- Accepting risks of console bans or legal action
- Using the software responsibly and ethically

**The developers provide no warranty and accept no liability for any damages, bans, or legal issues resulting from use of this software.**

---

**Made with ❤️ by the ACNH Bot Community**

*Star ⭐ this repository if it helped you!*