Not every macro benefits from being linked to a button on a keyboard, whether it be because of the frequency at which you need said macro not being very high, or if you don't need to see `Key Events`. A streamdeck is a tool often used by streamers or just anyone looking to optimise whatever workflow they're in.

In the case of video editing it allows us to have some useful scripts that only pop up every once in a while, still within arms reach.

> **I should note that for me personally, I put less frequently used macros here because I use a secondary keyboard with `QMK.ahk` if you don't have a secondary keyboard, a streamdeck is a good alternative to put any scripts that don't require either seeing `Key {Up/Down}` events or doesn't require the activation key being held.*

> *All scripts show their dependencies at the top of the script, all of which can be found in the `..\lib\` folder.*

## Support Files
Within `..\Support Files\Streamdeck Files\` you will find a `.ini` file where you can set a few directory locations used throughout some streamdeck scripts. This file is placed in this directory to allow the user to more easily replace the entire `Streamdeck AHK` folder without worrying about custom directories being wiped.
***
## Timeline Coords
Some scripts require the coordinates of the `Premiere Pro` timeline. These coordinates are stored within the `Prem {` class, but because these scripts are generally designed to run once and then terminate, that means each new instance of the script will have to relocate those coordinates. Because of this, those scripts will also attempt to ask `My Scripts.ahk` if it has those coordinates already which can result in recieving them much faster (if the `Prem {` class within `My Scripts.ahk` has already retrieved them) than needing to manually retrieve them each time.

***

## convert scripts
These scripts take advantage of `ffmpeg` to quickly convert files from one file format to another. If you do **not** have [`ffmpeg` installed](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) to the system path, these scripts will not work.

Go to any folder that contains the files you wish to convert, then simply run the desired script. It will automatically grab the path of the current explorer window then send the desired command to cmd. It will then send an `ffmpeg` command to convert **all** files of the desired file format to the requested file format.

> *This function may recurse further into folders searching for files to convert.*

- `convert mkv2mp3.ahk`  => converts all `.mkv` files to `.mp3`
- `convert mkv2mp4.ahk`  => converts all `.mkv` files to `.mp4`
- `convert mov2mp4.ahk`  => converts all `.mov` files to `.mp4`
- `convert mp42mp3.ahk`  => converts all `.mp4` files to `.mp3`
- `convert webm2mp3.ahk` => converts all `.webm` files to `.mp3`
***

## download scripts
These scripts take advantage of `yt-dlp` to quickly download (and/or convert) youtube/twitch videos. If you do **not** have [`yt-dlp` installed](https://github.com/Tomshiii/ahk/wiki/Install-yt%E2%80%90dlp) to the system path, these scripts will not work.

These scripts will first check for any highlighted text (or will fall back to checking the clipboard if the user isn't highlighting anything), then check for a youtube/twitch url. If one is found it should automatically download the file to the desired location!

- `sfx.ahk`       => downloads the video and converts it to `.wav` and saves it in the path provided
- `thumbnail.ahk` => downloads the thumbnail and places it in `[ptf.comms]\[ClientName]\口 thumbnails`
- `video.ahk`     => downloads the video and saves it in the path provided. If the passed URL is from youtube, the file will be reencoded to `h264` for compatibility with NLE's
- `vfx.ahk`       => downloads the video and saves it in the path provided. If the passed URL is from youtube, the file will be reencoded to `h264` for compatibility with NLE's
- `projVideo.ahk` => downloads the video and saves it in the path of the currently active project. If the passed URL is from youtube, the file will be reencoded to `h264` for compatibility with NLE's
- `projAudio.ahk` => downloads the audio and saves it in the path of the currently active project.
- `vidSelect.ahk` => downloads the video and saves it in the path selected.
- `audSelect.ahk` => downloads the audio and saves it in the path selected.
***

## hCrop scripts
These scripts take advantage of [`ffmpeg`](https://github.com/Tomshiii/ahk/wiki/Install-ffmpeg) and offer a variaty of functionality centered around the need to split a video in half along the horizontal axis. These scripts extend off the `encodeGUI {` to offer that basic functionality while also offering some additional options if necessary

- `hCrop CamAll.ahk`      => offers the user the ability to select which half of every video in the chosen directory they wish to reencode to a new file
- `hCrop CamSingle.ahk`   => offers the user the ability to select which half of the video selected they wish to reencode to a new file
- `hCrop loop.ahk`        => automatically splits every video in the active directory and reencodes them to two new files
- `hCrop SplitSingle.ahk` => offers the user the ability to split and reencode the selected video to two new files
***

## Lock Scripts
These scripts are designed to trigger `prem.excalibur.lockTracks()`
***

## Preview scripts
These scripts are designed to speed up the process of generating/deleting `Render Previews` on the timeline. All of them will attempt to save the current project before moving on with their action.

> These scripts require the proper shortcuts to be set within `KSA`
***

## openSocials scripts
These scripts use the function `openSocials()` to open the youtube/twitch channel of the current project client. The client name is pulled from the path directory that can be found in the title of either After Effects or Premiere Pro and is then cross referenced against a local class for the appropriate online channel name.
***

## blend scripts
These scripts are designed to adjust the blend mode of a given track for either Adobe Premiere or Adobe After Effects.

Simply run a script for the desired mode in either program! If run in Premiere, the script will adjust the mode for the desired track.

> If script is run in After Effects, it will simply ensure you're in the right mode to be able to adjust blend modes, **it will not attempt to change blend modes for any layers**.
***

## run & activate Scripts
These scripts are designed to run and activate any folder path you set.

> #### **Although you can simply run a filepath from a streamdeck natively, it won't automatically activate it (at least in win11) so this script can help ensure the desired filepath is brought to the foreground whenever pressed**
***

## Update Scripts
These scripts are a collection of scripts to quickly update any `chocolatey` repos using the commandline
***

## Other Scripts
Here I will go through each script and describe its use case.

> *A lot of these are designed for my workflow specifically and will likely **not** be plug and play.*

> #### `adjustment layer.ahk`
A script to quickly add a new adjustment layer in either Adobe Premiere or Adobe After Effects.
***

> #### `close stream.ahk`
Would close all programs I used during a live stream, as well as close a script I used specifically during streams.
***

> #### `disable obs preview.ahk`
A script to quickly activate `OBS` and disable its preview window. This is preferable over just a hotkey as the hotkey will only work while `OBS` is active
***

> #### `enable obs preview.ahk`
A script to quickly activate `OBS` and enable its preview window. This is preferable over just a hotkey as the hotkey will only work while `OBS` is active
***

> #### `focusChat.ahk`
A script to quickly focus my twitch chat window. (Streams get hectic and windows get hidden regularly).
***

> #### `Move project.ahk`
This script will ask you to select a project directory, then it will ask you to select a destination directory, from there it will move project.

It will also;

- Delete the `..\renders\draft` directory if it exists
- Delete the `..\proxies` directory if it exists
- Delete the `..\Adobe Premiere Pro Auto-Save` directory if it exists
- Delete the `..\Adobe After Effects Auto-Save` directory if it exists
- Delete the `..\Adobe Premiere Pro Audio Previews` directory if it exists
- Delete the `..\Adobe Premiere Pro Video Previews` directory if it exists
- Delete any `.pek/.pkf/.cfa` temp files if they exist
- Delete any `.mkv` files if they exist (Premiere can't use them, so they're likely a duplicate of an `.mp4` file within the project)
- Delete any files (that aren't the final render in `..\renders\final`) larger than `2GB`

This script is designed to aid in project storage, making sure to wipe anything unnecessary before storing the final project file
***

> #### `New Premiere.ahk`
This script will automate the process of creating a new `Premiere Pro` project. This script copies a template project file found in `..\Backups\Adobe Backups\Premiere\Template\` to the desired project folder then automates the process of changing the default proxy location.
***

> #### `obs_screenshot.ahk`
A script to quickly focus `OBS` and input the `screenshot` hotkey. (set within `KSA.ini`)
***

> #### `powerpoints.ahk`
As a speedrunner, route documents are a frequent thing to have open - but can be a little tedious as if the document isn't the active window, trying to progress it forward will result in nothing.

This script will activate the desired window before progressing it forward.
***

> #### `push to audition.ahk`
Select the track you wish to open in audition, then open this script. It should take care of the rest.

**note: this script contains mouse coordinates that might not line up for you. I use a 1440p main display with audition's default layout (I think)*
***

> #### `qss.ahk Scripts`
`Quick Sound Settings`. *These scripts were primarily used when I used a `GoXLR`*. When using a goxlr, there are times I would want my browser's audio stream to go to a separate track so `OBS` wouldn't hear it, and then there are other times where I would want to show chat a video, these scripts were designed to automate that process.

- `qss_firefox DEFAULT/STREAM.ahk` => open the `"ms-settings:apps-volume"` settings page, locate the firefox logo, set it to the desired audio channel.
- `quick sound settings.ahk` => open the `"ms-settings:apps-volume"` settings page.
***

> #### `scale.ahk Scripts`
Set the scale of the selected track to a predetermined amount. Works in Premiere & Resolve
***

> #### `speed.ahk Scripts`
Set the speed of the selected track to a predetermined amount. Works in Premiere.
***

> #### `start stream.ahk Scripts`
Two scripts designed to start all programs I need for a livestream, as well as making sure they all get moved into the correct position. They will also make sure OBS is on the correct profile. These scripts are the main culperate for getting me into ahk!
***

> #### `Start new project.ahk`
This script will ask you for a directory, once selected will create all folders needed for a video editing project.
***

> #### `tiktok project.ahk`
This script will (if activated within Premiere Pro) open up the sequence settings and change the aspect ratio to a vertical one.
***

> #### `tiktok voice.ahk`
This script is designed to use the tiktok text to speech tool found [here](https://github.com/oscie57/tiktok-voice). It requires python to be installed.

This script will ask you what you want the tts to say, then it will ask you what you want the file to be called and it will work its magic. The output directory & voice are definied within the script and will need to be changed.
***

> #### `pcTimerShutdown.ahk`
This script provides a quick and easy to use GUI to schedule a PC shutdown for up to a max of `9999 hours`.
***

> #### `trim(Audio/Video).ahk`
These scripts provide the user with a quick and easy to use GUI designed to trim an audio/video file using `ffmpeg`.
***

> #### `render and replace.ahk`
This script will label the current selected clip the colour of your choosing and then send the hotkey (set within `KSA`) to open the `Render and Replace` dialogue box.
***

> #### `(blue/green)Key.ahk`
These scripts are to quickly add a Premiere Pro preset for a blue/green key
***

> #### `make sequence.ahk`
A script designed to quickly make the highlighted clips a sequence within Premiere Pro.

> Will require the appropriate hotkeys to be set within `KSA.ini`
***

> #### `sendtoAE.ahk`
A script designed to send the highlighted clip to an `After Effects` composition.
***

> #### `remapDrive.ahk`
This script is designed to easily adjust `Mapped Network Drives` using a GUI.
***

> #### `resetAEtrans.ahk`
As `autosave.ahk` changes the transparency of `After Effects` this script is a failsafe to allow the user to set it back to normal in the event that something goes wrong.
***