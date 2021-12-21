# mo2mp4
This is a hacky solution to convert Wii Mobiclip .mo files to .mp4 until if and when ffmpeg can read them. Despite its name, While ffmpeg can convert DS .mods and 3DS .moflex files to .mp4, it cannot handle Wii .mo files (nor can the predecessor, Gericom's MobiConverter, which can only handle 3DS .moflex files). This tool uses a combination of the Wii Mobiclip SDK and Gericom's MobiclipDecoder in order to convert to .mp4. (And it's not pretty at all...)

The Wii Mobiclip SDK can view Mobiclip files using MoSimulator, however there isn't a way to get great recordings that way. No one wants to record that with OBS.

## Process

This is how the conversion from .mo to .mp4 happens:

1. Open the .mo file with MobiclipDecoder, and dump all frames as PNGs. It reads whatever Mobiclip file is in the directory. This can take a while...
1. Use MoDump from the Wii Mobiclip SDK to dump the audio into wav.
1. Merge all the frames and the audio with ffmpeg, and clean the folder up afterwards.

This does not work with videos with Vorbis audio (Tremor library). Those were only used on the Nintendo Channel and Wii no Ma (they can load other audio formats too, but Nintendo stuck with using Vorbis for some reason, which is not in the Wii Mobiclip SDK).

Also, this script will break if you have more than one .mo in the directory. Since this tool was made in such a hurry, it's pretty flimsy.

Instead, make a script like this.

```
copy C:\Kirby\USA\Anime01.mo . && MobiclipDecoder.exe && del Anime01.mo
copy C:\Kirby\USA\Anime02.mo . && MobiclipDecoder.exe && del Anime02.mo
copy C:\Kirby\USA\Anime03.mo . && MobiclipDecoder.exe && del Anime03.mo
```