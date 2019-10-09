##What is this you're writing?

Well, to help me learn how to get addon and future Python-related Blender scripts working on Windows, I tried making my process into a tutorial format. Things were actually going really well! My only problem has been activating the custom proxy script, and this is as far as I got before giving up after about 2 days of really trying to figure it out. I'll make a note of where the Tutorial is no longer guaranteed to help anything. I don't know what I'll do with this tutorial or where I'll put it, but maybe I'll come back to it once I learn more from documentation or just asking the right questions in the GDQuest Discord.

##Blender Power Sequencer Tutorial:

###Table of Contents:

A. Downloading and Installing BPS
B. Reducing Blender's preview size
C. Enabling Faster Video Previews and Transparent Image Previews
D. Creating Proxies with Python and FFmpeg

**A. Downloading and Installing BPS**

Written by following this video tutorial:  https://youtu.be/TZZ9I-yxEjM?t=94

1. Download Blender: blender.org
2. Download BPS: https://github.com/GDquest/Blender-power-sequencer/releases and place it somewhere safe.
3. In Blender, go to Edit>Preferences>Addons>Install (with the download arrow next to it) and select the BPS .zip file.

**B. Reducing Blender's preview size**

BPS is installed at this point, but this next step is highly reccomended for any new Blender video project.

1. Click the preview window in Blender's Video Editor and hit "N" to open the side panel.
2. Open the "View Settings" dialog.
3. "Proxy Render Size" determines the scale of your video preview. By default it's native, so it's highly reccomended to make it smaller like 25% or 50%.

You should now start to see orange lines appearing next to the horizontal scrollbar. These are places that have proxies rendered. You probably won't see any until you do this since Blender has been trying to render native previews of your edits until just now.

##Note: This is where the tutorial stops being correct and I ran into issues

**C. Enabling Faster Video Previews and Transparent Image Previews**

Blender is currently doing all the work of rendering preview "proxies" on a single core and won't do it while you're idling either. Images in the preview are also proxied as JPEGs instead of PNGs, which turn transparent images opaque until the video is rendered. If you'd like transparent image previews and ready-to-go multicore-rendered proxies, continue following this guide.

1. Download Python 3.X (any version of Python 3) https://www.python.org/downloads/windows/
2. Download FFmpeg https://ffmpeg.zeranoe.com/builds/

While you wait for these two to download, you can prepare yourself for a step further down the road by making a custom folder for the project you plan to create. Place all the videos you plan to use in one subfolder, images in another, and audio in another as well. You can also place the Blender project file in this folder to make file portability easier.

3. Place the FFmpeg download contents somewhere accessable, like an Encoders folder in your C drive.

With that out of the way, let's get into the trickier Windows stuff:

4. Copy the path of the /bin/ folder in your unzipped ffmpeg (the one that contains ffmpeg.exe and other .exe files)
5. Open the Start menu, search for "Environment Variables" and select it
6. In the now-open system properties tab, click "Environment Variables" at the bottom.
7. Click "Path", click "Edit" You'll now see the list of directories that Python scans.
8. Click "add" and paste the copied path of your /bin/ folder.
9. Open command prompt or powershell and type "ffmpeg" to check the installation.

If you see a lot of text with dashes pop up, it's installed! If you get just a little bit of text with any errors, the path with ffmpeg.exe in it was probably incorrect.

**D. Creating Proxies with Python and FFmpeg**

This GDQuest video is unlisted but super useful. This shows the process in-action: https://www.youtube.com/watch?v=4EZOtj1PTik

1. Unpack the parent folder of the BPS .zip file into your AppData/Local/Programs/Python/[Python Version]/Scripts/ folder.

(BPS 1.2 or older: Go to "utils" and copy the path in that "utils" folder. Use the Command Line/Powershell window inside this directory.)

2. Locate your video project parent folder with all the footage you want to process. (Making a custom folder with no excess footage is reccomended!)
3. Moment of truth. Type the following:

"python .build\ffmpeg_proxies.py [YOUR VIDEO PROEJCT PATH]"

Your video project path might look like: "C:\Users\You\Documents\Blender\Video Import\Holiday 2001"

4. Let the image, audio and video proxies build for a few minutes. Check that no substantial errors occured.

You're good to go! You should now be able to scrub through the video without an issue, and any transparent images should preview with their transparency preserved!

BPS 1.3 or newer: Check this file: 

##My notes in trying to figure out what went wrong:

```C:\Users\Me\Documents\Blender\Videos Import\Barcelona Trip

C:\Users\Me\AppData\Local\Programs\Python\Python37-32\Scripts\BPSProxy ???

Installing BPSProxy individually?
:It can be installed as a standalone command line utility [via PiPy](https://pypi.org/project/bpsproxy/): `pip install [--user] bpsproxy`. *Note* that you have to have `$HOME/.local/bin` included in your `$PATH` environment variable (on unix) if you're going to install the utility locally (using `--user` when executing `pip`).:

we're gonna need to ask help from BPS discord

also https://www.gdquest.com/tutorial/video-editing/blender-power-sequencer/blender-video-editing-tutorials/chapter/13_power_sequencer_utils_render_proxies_with_ffmpeg/


workflow:
https://www.youtube.com/watch?v=xZoZaSsuhXw

older installation of BPS? https://youtu.be/Zcj4onvP06w```
