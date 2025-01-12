## Oh Hi ##

[![Current Release](https://img.shields.io/github/v/release/mattpannella/pocket-updater-utility?label=Current%20Release)](https://github.com/mattpannella/pocket-updater-utility/releases/latest) ![Downloads](https://img.shields.io/github/downloads/mattpannella/pocket-updater-utility/latest/total?label=Downloads) [![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate/?business=YEERX89E75HQ8&no_recurring=1&currency_code=USD)

  

A free utility for updating the openFPGA cores, and firmware, on your Analogue Pocket.

The update process will check for pocket firmware updates, openfpga core updates, and install any required BIOS files and arcade ROMS. You're on your own when it comes to console ROMs.

  
  

A complete list of available cores can also be found here: [https://openfpga-cores-inventory.github.io/analogue-pocket/](https://openfpga-cores-inventory.github.io/analogue-pocket/)

  

I can't (and don't want to) support old versions, so please make sure you download the latest release before submitting any issues.

  

## Instructions ##

If you just want to use this utility, do not clone the source repository. Just

download the [latest release](https://github.com/mattpannella/pocket-updater-utility/releases/latest/). Unzip it, put the executable file for your platform (windows, mac os, or linux) in the root of your sd card, and run the program.

  

At the main menu run `Settings` to have it walk through the available settings for you.

[Advanced](#advanced-usage) |
[Settings](#settings) |
[Image Packs](#download-image-packs) |
[Core Selector](#core-selector) |
[PC Engine CD](#generating-instance-json-files) |
[Jotego Cores](#jotego-beta-cores) |
[Game n Watch](#how-to-build-game-and-watch-roms-that-are-compatible-with-the-pocket)

  

### Advanced Usage

CLI Parameters

```

  menu                 (Default Verb) Interactive Main Menu
    -p, --path    	     Absolute path to install location

  fund                 List sponsor links. Lists all if no core is provided
    -c, --core               The core to check funding links for
    
  update               Run update all. (Can be configured via the settings menu)
    -p, --path               Absolute path to install location
    -c, --core               The core you want to update. Runs for all otherwise
    -f, --platformsfolder    Preserve the Platforms folder, so customizations aren't overwritten by updates.

  assets               Run the asset downloader
    -p, --path               Absolute path to install location
    -c, --core               The core you want to download assets for.

  firmware             Check for Pocket firmware updates
    -p, --path               Absolute path to install location

  images               Download image packs
    -p, --path               Absolute path to install location
    -o, --owner              Image pack repo username
    -i, --imagepack          Github repo name for image pack
    -v, --variant            The optional variant

  instancegenerator    Run the instance JSON generator
    -p, --path               Absolute path to install location

  help                 Display more information on a specific command.

  version              Display version information.

```

examples:

  

`/path/to/pocket_updater -p /path/to/sdcard/`

  

`/path/to/pocket_updater update -c boogermann.bankpanic`

  

`/path/to/pocket_updater assets -c jotego.jtcontra`

  

`/path/to/pocket_updater images -i pocket-platform-images -o dyreschlock -v home`

  
### Settings

 All settings can be modified in your `pocket_updater_settings.json` file

  

|                                          |                                  |                                                                                                                                                                                                      |
|------------------------------------------|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|                                                                                                                      
| Disable Firmware Downloading             | config.download_firmware         | Set to `false` if you don't want Update All to check for firmware updates                                                                                                                              |
| Disable Asset Downloading                | config.download_assets           | Set to `false` if you'd like to supply your own BIOS and arcade rom files, and don't want Update All to handle this.                                                                                   |
| Preserve Platforms Folder Customizations | config.preserve_platforms_folder | If you have any customizations to the Platforms folder, you can use this option to preserve them during the update process. Set to `true` in your settings file, or use `-f` as a command line parameter |
| Github Personal Access Token             | config.github_token              | If you're running up against the rate limit on the github api, you can provide your personal access token to the updater via the settings.                                                           |
| Disable Instance JSON Builder            | config.build_instance_jsons      | Set this to `false` if you don't want Update All to build instance JSON files.
| Delete Untracked Cores           | config.delete_skipped_cores      | `true` by default. Set to `false` if you don't want the updater to remove cores you don't select to track  
| CRC Check Assets          | config.crc_check      | `true` by default. Set to `false` if you don't want the updater check the CRC hash on your asset files
| Skip Alternative Assets         | config.skip_alternative_assets      | `true` by default. If a core developer puts any of their rom asset files in a directory named `_alternatives` they won't be downloaded automatically (unless you set this to `false`)
| Use Custom Archive         | config.use_custom_archive      | `false` by default. Instead of checking the archive site defined in your settings to look for required assets, use a custom site that you can define. (by default this will be a site hosted by RetroDriven)
| Custom Archive URL         | config.custom_archive.url      | The full url to your custom site
| Custom Archive Index         | config.custom_archive.index      | Relative path to the index of your custom site's files. This is not required, but it's needed for CRC checking. If you have CRC checking enabled, the setting will be ignored unless this provides the necessary format. It must match the output of archive.org's json endpoint. https://archive.org/developers/md-read.html
| Per Core Settings                | coreSettings.{corename}.download_assets and coreSettings.{corename}.platform_rename                   | Set to `false` for any core you don't want assets downloaded for, or automatic platform renaming (currently this only applies to jotego cores)
  

### Download Image Packs

This will present you with a list of available image packs and automatically download and extract it to the Platforms/_images directory for you

  

### Core Selector

On your first run it will prompt you to select the cores you want tracked. After that initial run, you can run it again any time via the main menu.
  

### Generating Instance JSON Files

- Only supported by PC Engine CD, currently

- Put your games in /Assets/{platform}/common

- Each game needs to be in its own directory (and be sure to name the directory the full title of the game)

- Example: /Assets/pcecd/common/Rondo of Blood

- /Assets/pcecd/common/Bonk

- etc

- All games (for PC Engine CD) must be in cue/bin format. The generated json file will be saved using the same filename as the cue file, so be sure to also name that with the full title of the game

- When you run the `Generate Instance JSON Files` or `Update All` menu items, it will search through every directory in common and create a json file that can be launched by the core

- You can disable this process in Update All by setting `build_instance_jsons` to `false` in your settings file, if you don't want it to run every time you update.


### Jotego Beta Cores

Now that Jotego is releasing his beta cores publicly (and requiring a beta key to play them), you can just drop the `jtbeta.zip` file from patreon onto the root of your sd card and run Update All, and it will automatically copy the beta key to the correct folders for the cores that need it. Make sure you don't rename the file, it's going to look for exactly `jtbeta.zip`

  

### How to build game and watch roms that are compatible with the pocket

Create 2 new folders.

`/Assets/gameandwatch/agg23.GameAndWatch/artwork` and `/Assets/gameandwatch/agg23.GameAndWatch/roms`

  

Place your `[artwork].zip` files into the artwork folder and your `[rom]`.zip files into the roms folder

  

Should look like this:

  

```

/Assets/gameandwatch/agg23.GameAndWatch/artwork/gnw_dkong.zip

/Assets/gameandwatch/agg23.GameAndWatch/roms/gnw_dkong.zip

```

  

Now just run the menu option in the updater and it will build your games

  

## Troubleshooting

Slow asset downloads? Try toggling `use_custom_archive` to true, in your settings.

  

If you run the update process and get a message like `Error in framework RS: bridge not responding` when running a core, try to run the updater in a local folder on your pc, and then copy the files over to the sd card afterwards. I'm not entirely sure what the issue is, but I've seen it reported a bunch of times now and running the updater locally seems to help.

  

## Submitting new cores ##

You can submit new cores here [https://github.com/openfpga-cores-inventory/analogue-pocket](https://github.com/openfpga-cores-inventory/analogue-pocket)

  

## Credits ##

  

Thanks to [neil-morrison44](https://github.com/neil-morrison44). This is a port built on top of the work originally done by him here [https://gist.github.com/neil-morrison44/34fbb18de90cd9a32ca5bdafb2a812b8](https://gist.github.com/neil-morrison44/34fbb18de90cd9a32ca5bdafb2a812b8)

  

Special thanks to [RetroDriven](https://github.com/RetroDriven/) for maintaining the arcade rom archive.

  

And [dyreschlock](https://github.com/dyreschlock/pocket-platform-images/tree/main/arcade/Platforms) for hosting the updated platform files for Jotego's cores

  

And if you're looking for something with a few more features and a user interface, check out this updater. [https://github.com/RetroDriven/Pocket_Updater](https://github.com/RetroDriven/Pocket_Updater)

  

Or if you want something cross platform that will run on a mac or linux: [https://github.com/neil-morrison44/pocket-sync](https://github.com/neil-morrison44/pocket-sync)
