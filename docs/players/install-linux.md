---
title: Installing on Linux
parent: For players
nav_order: 1.1
---

# Installing the loader on Linux

These steps are for the native Linux x86_64 Steam build. They were tested with Melvor Idle 2 `0.11.6-alpha.1` and Melvor Mod Loader `0.2.0`. Build the loader from source with the .NET 10 SDK.

## Build and install

1. In Steam, right-click **Melvor Idle 2** and choose **Manage → Browse local files**. The folder should contain `MelvorIdle2.x86_64` and `data_GamesByMalcs.Melvor2_linuxbsd_x86_64/`. Close the game before installing.
2. From the root of this repository, set `GAME_DIR` to that folder and build the loader:

   ```bash
   GAME_DIR="/absolute/path/to/Melvor Idle 2"
   dotnet build Loader/MelvorModLoader.csproj -c Release \
     -p:RuntimeIdentifier=linux-x64 \
     -p:GameData="$GAME_DIR/data_GamesByMalcs.Melvor2_linuxbsd_x86_64" \
     -o ./data_MelvorModLoader_linuxbsd_x86_64
   ```

3. Copy the entire `data_MelvorModLoader_linuxbsd_x86_64/` output folder into the game folder. It contains the runtime as well as the loader DLL.
4. Create `override.cfg` next to `MelvorIdle2.x86_64` with the following contents. If an `override.cfg` already exists, back it up and keep its other settings.

   ```ini
   [dotnet]
   project/assembly_name="MelvorModLoader"
   ```

## Check the loader

Launch the game through Steam and check `MelvorModLoader.log` in the game folder for `Game started`. If you have no mods yet, the log may say there is no `mods` folder. Create it when you install your first mod, for example `mods/ExampleMod/ExampleMod.dll`. Use the same capitalization as the mod's DLL and dependency files; Linux paths are case sensitive on most filesystems.

## Remove the loader

Close the game. Remove the `override.cfg` you created, or restore your original file if you had one, then remove `data_MelvorModLoader_linuxbsd_x86_64/`. You can leave `mods/` and `MelvorModLoader.log` in place.
