# mo2mp4
This is a hacky solution to convert Wii Mobiclip .mo files to .mp4 until if and when ffmpeg can read them. Despite its name, While ffmpeg can convert DS .mods and 3DS .moflex files to .mp4, it cannot handle Wii .mo files (nor can the predecessor, Gericom's MobiConverter, which can only handle 3DS .moflex files). This tool uses a combination of the Wii Mobiclip SDK and Gericom's MobiclipDecoder in order to convert to .mp4. (And it's not pretty at all...)

The Wii Mobiclip SDK can view Mobiclip files using MoSimulator, however there isn't a way to get great recordings that way. No one wants to record that with OBS.

[https://github.com/RiiConnect24/mobiclip-conversion-tool/releases/latest Mobiclip Conversion Tool] can do the opposite of this tool, and convert .mp4 to .mo.

To use this tool, you need to have the Mobiclip SDK and a license. The SDK can be found on MarioCube, and the license can be obtained [on this page](https://developer.nintendo.com/group/development/getting-started/3ds/middleware/mobiclip-for-3ds) if you have a Nintendo Developer Account. You also have to have MoDump in the same directory as this program, and you launch MobiclipDecoder with one (1) .mo file in the folder.

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

## Compiling

I have no idea why you would want to compile this, but just replace Form1.cs in [https://github.com/Gericom/MobiclipDecoder/tree/newer_stuff Gericom's MobiclipDecoder].

## License

I don't think MobiclipDecoder has a license, so I don't really have a code license for this.