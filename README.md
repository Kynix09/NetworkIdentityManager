<div align="center">

# Network Identity Manager

A real Windows network configuration utility. This project replaces the simulated hardware-profile controls with supported Windows networking operations.
**A modern Windows utility for viewing, backing up, and changing supported network settings.**

![Windows](https://img.shields.io/badge/Windows-10%20%7C%2011-0078D4?style=flat-square&logo=windows)
![.NET](https://img.shields.io/badge/.NET-8-512BD4?style=flat-square&logo=dotnet)
![Architecture](https://img.shields.io/badge/Architecture-x64-333333?style=flat-square)

</div>

## Preview

![Network Identity Manager dashboard](docs/images/dashboard.png)

<details>
<summary><strong>Open the configuration panel</strong></summary>

![Network configuration panel](docs/images/configuration.png)

</details>

## Features

## Real changes
- View all Windows network adapters and their current status.
- Apply or remove a driver-supported MAC address override.
- Generate valid locally administered unicast MAC addresses.
- Switch IPv4 between DHCP and static configuration.
- Configure IPv4 address, prefix length, and default gateway.
- Configure custom DNS while using either DHCP or static IPv4.
- Change the interface metric.
- Rename the Windows computer.
- Automatically preserve the original configuration for each adapter.
- Restore saved original settings at any time.
- English, Turkish, Spanish, French, Hindi, German, Portuguese, and Italian UI options.
- Arial, Inter Variable, and Minecraft font options.
- Self-contained single executable—no separate .NET installation or asset files required.

## Requirements

| Requirement | Details |
|---|---|
| Operating system | 64-bit Windows 10 or Windows 11 |
| Permissions | Administrator approval is required |
| Architecture | x64 |
| MAC override | Must be supported by the selected adapter driver |
| Restart | Required after changing the computer name |

> [!WARNING]
> Applying network settings can temporarily disconnect the selected adapter. Verify static IP, gateway, and DNS values before confirming.

## Installation

1. Download `NetworkIdentityManager.exe` from the repository's **Releases** page.
2. Place it anywhere, including the Desktop.
3. Run the executable and approve the Windows administrator prompt.

The release build embeds the .NET runtime, WPF native components, fonts, and startup audio. The executable works by itself without adjacent files.

Windows SmartScreen may display a warning for unsigned community builds. Review the source and build it locally if preferred.

- Enumerates Windows network adapters and current configuration
- Applies or removes a driver-supported `NetworkAddress` MAC override
- Generates locally administered unicast MAC addresses
- Switches IPv4 between DHCP and static configuration
- Changes IPv4 address, prefix length and default gateway
- Changes DNS servers independently of DHCP/static IPv4 mode
- Changes interface metric
- Renames the Windows computer (restart required)
- Creates an immutable first-run original backup per adapter and restores it
## How original settings are protected

The executable requests administrator elevation because Windows requires it for these operations. Applying settings can temporarily disconnect the selected adapter. Some adapter drivers do not support MAC override; the UI detects this and refuses that operation.
The first time an adapter is selected, its current configuration is saved under:

Original backups are stored under `Documents\Network Identity Manager\originals-{interfaceIndex}.networkprofile`.
```text
Documents\Network Identity Manager\originals-{interfaceIndex}.networkprofile
```

## Project layout
The backup includes the MAC override state, IPv4 mode and address, gateway, DNS servers, interface metric, and computer name. Existing original backups are not silently replaced.

- `Models/NetworkAdapterSnapshot.cs` — adapter state and change request contracts
- `Services/NetworkConfigurationService.cs` — validation, backup and Windows network operations
- `Services/PowerShellRunner.cs` — encoded, non-interactive PowerShell execution
- `Themes/` and `App.xaml` — palette and custom controls, including scrollbar/dropdowns
- `UI/` — dragging, fonts, language and credits behavior
## Build from source

## Build
Install the [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0), then run:

```powershell
dotnet publish -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true
dotnet publish -c Release
```
