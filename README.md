# Hydroneer Community Modkit Project

## [Download](https://drive.google.com/file/d/15-ELLy3XoBh45doDdZQqv4b8G5Lvs1Pl/view?usp=sharing)

## [Modkit Creation Process](https://www.twitch.tv/videos/2192292674)

**Current version:** `1.0`

**Based on the game version:** `3.0.8 + Journey to Volcalidus DLC`

**Based on the Hydroneer-Template commit:** [3.0.8](https://github.com/Buckminsterfullerene02/Hydroneer-Template/commit/0ea4be0995076d116fdb51ad73e839d1a09f08ab)

**Full opened project size:** `14GB`

## What is this for?

The modkit is almost an exact mirror of Hydroneer's original Unreal project without any of the code implementations. It is for:
- Blueprint modding, when you are making a mod that needs to get references to various game assets
- Animation modding, when you want to test out your animations on the skeletons/skeletal meshes already there
- Skin/texture/material/model modding, for testing your assets on existing game assets and meshes in the editor
- Map modding, for example editing the game world or making a new map using existing or entirely new assets 

With this modkit, you can make your own content inside of the editor in almost the same way the developers can when developing the game - minus the ability to test blueprint or map mods inside of the editor due to there being no code implementations.

It completely removes the need to recreate any assets by hand which is usually very time consuming.

## Usage

1. Unzip the modkit files to a location of your choice. The content includes the base game and the DLC01 content (which can be found in `Plugins/DLC01/Content`).

2. Then:
    - If you have no interest in looking through the source code, just open the `Mining.uproject`.

    - If you wish to look through the source code, you will need to generate the project files by right clicking the `Mining.uproject` file and selecting `Generate Visual Studio project files`, then open `Mining.sln` in your IDE.

3. Have fun being able to access thousands of references at once!

Note: There is a folder called `Mods` in the base game content; this is *not* content from the game - it is a UE4SS mod for creating the levels maps (such as `Levels/L_GameWorld`).

## Modding

Any C++ changes can be built like normal, just remember that there are now assets in the project that may break.

**Editing an existing game asset is not recommended, unless you know what you are doing!** Usually creating a child actor override of the asset you wish to edit is the best way to do it. This prevents possible mod conflicts.

## FAQ

**Why do blueprints have no code?**

> Blueprints are compiled into kismet bytecode, which currently is not reconstructed back in the editor.
>
> If you wish for an alternate, human-readable way to view the kismet bytecode, you can use [this tool](https://github.com/trumank/kismet-analyzer).

**Why are many of the materials and particles all white/fuzzy/strange looking?**

> It is an unsolved problem to reconstruct the material code automatically. This is because the parameter data is stored in the `globalshadercache.bin` file, rather than in the cooked `.uasset` data. 
>
> By extension, because the particles are using these partially reconstructed materials, they too will look all weird.

**Why can't I open particles or sound waves?**

> These asset types are actually the cooked files copied directly from the unpacked game files, since they work just fine in-editor as references. Cooked files cannot be opened or saved in the editor.

**Why are some assets missing?**

> Some asset types are missing because the code to reconstruct them has not been written yet, or for some other reason. Please see the below section on missing files for more detail.

## Missing files

There are a few files that are in the game content but are not in the modkit content. These are:
- Movies
- Niagara assets
- Media players
- File media sources
- Any assets related to the plugins such as the Voxel Pro plugin (except for the DLC01 plugin assets)

## Known issues

- Animation sequences have no track data, so they won't play any sounds or particles

## Credits

Buckminsterfullerene - Modkit creator

Credits related to [UE4SS UHT Generator](https://docs.ue4ss.com/guides/generating-uht-compatible-headers.html), the UE4SS utility used to generate the dummy C++ headers (FSD-Template):
- Archengius
- Narknon
- Buckminsterfullerene

Credits related to [UEAssetToolkitGenerator](https://github.com/LongerWarrior/UEAssetToolkitGenerator), the program used to generate JSON data about the assets from the unpacked files:
- LongerWarrior
- Buckminsterfullerene
- atenfyr

Credits related to [UEAssetToolkit](https://github.com/Buckminsterfullerene02/UEAssetToolkit-Fixes), the UE plugin used to generate the assets in-editor from the JSON data:
- Archengius
- Mircearoata
- Buckminsterfullerene
- LongerWarrior

Credits related to the [FBX export pipeline](https://github.com/LongerWarrior/UEAssetToolkitGenerator/wiki/Generating-FBX):
- CUE4Parse developers, Zain, Buckminsterfullerene (for the ActorX mass export script)
- Zain, matyalatte, Befzz (for the FBX mass export blender scripts)
