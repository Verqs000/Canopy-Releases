# Canopy Anti-Cheat

Launcher and client-side anti-cheat for competitive Gorilla Tag leagues on Steam.

Download the latest build from **[Releases](../../releases)**.

## Two downloads

- **Canopy** (Steam / PC VR): the launcher and anti-cheat described below.
- **Canopy Quest** (standalone Quest): a match gate that verifies a headset before and during league matches. See [Canopy Quest](#canopy-quest) at the end.

## Requirements

- Windows 10 or 11, 64-bit
- Gorilla Tag installed through Steam, and SteamVR
- [.NET 8 Desktop Runtime](https://dotnet.microsoft.com/download/dotnet/8.0)

## How to use

1. Unzip the whole folder anywhere and run `Canopy\Canopy.exe`. Keep the `league` folder next to it.
2. Press **Launch Gorilla Tag**. Canopy checks the game files, starts the game through Steam and attaches protection.
3. Closing Canopy closes the game. The game cannot run under Canopy without protection.

For league matches, use **Restart as administrator** so Canopy can also inspect tools that run as administrator.

This is a league-managed build: the protection policy and game baseline are signed by the league and cannot be changed on a player's PC. The `admin` folder contains the league administrator tool; it does nothing without the league's private key.

## What it does

- Refuses to launch a tampered game install, proxy loader DLLs, or BepInEx when league policy prohibits it.
- Locks the game process against outside memory access and closes untrusted programs' handles to it.
- Verifies every library and managed assembly that loads into the game.
- Checks the game's and SteamVR's code for hooks.
- Writes a tamper-evident security log and a session report for league administrators.

## What it does not do

Canopy runs in user mode and has no kernel driver.

- Kernel-level cheats are out of reach.
- Tools run as administrator can only be inspected when Canopy is also run as administrator.
- It does not read in-game movement values.
- A session report shows that nothing was caught. It is not proof that a player is clean.

It has been run against the real game, but not yet through a full headset session. After a Gorilla Tag update, players need a new signed baseline from the league before they can launch.

## Privacy

Canopy inspects the game process, SteamVR, and programs that hold access to the game. It sends nothing over the network. Logs stay on your PC until you share them.

## Canopy Quest

For league matches played on a standalone Meta Quest. Download `CanopyQuest-…-win-x64.zip` from [Releases](../../releases).

Needs Windows 10/11, the .NET 8 Desktop Runtime, [SideQuest](https://sidequestvr.com) installed (it provides ADB), Developer Mode on for the headset, and a USB cable.

1. Unzip and run `CanopyQuest.exe`. Plug the headset in and choose **Allow** inside the headset.
2. Press **Install / Update** once. It puts the small Canopy Quest app on the headset.
3. Enter the match code from your league and press **Start Pre-Check**.
4. On a pass, give the pass code to your referee, press **Start Protection**, unplug and play.

It verifies that Gorilla Tag is the genuine build, that no unapproved apps are installed, that settings follow league policy (60 Hz, chromatic aberration and texture size up to 2560 are allowed) and that the system does not look modified. During the match the headset app keeps checking and logs connection stalls.

It is a gate for league matches, not gameplay protection: it cannot see or protect anything inside Gorilla Tag, and its results are evidence rather than proof. Tested on Quest 2.

The league's signed policy lives in this repository under `quest/` and is downloaded by the launcher automatically.