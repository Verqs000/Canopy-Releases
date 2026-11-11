# Canopy Anti-Cheat

Launcher and client-side anti-cheat for competitive Gorilla Tag leagues on Steam.

Download the latest build from **[Releases](../../releases)**.

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
