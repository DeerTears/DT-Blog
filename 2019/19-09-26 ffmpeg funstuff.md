Oh wow so I don't even need Blender to make videos to upload my music to Youtube, I can just pump these things out using ffmpeg!

Example on ffmpeg's website:
``ffmpeg -loop 1 -i img.jpg -i audio.wav -c:v libx264 -c:a aac -b:a 192k -shortest out.mp4``

JM's description of said example: ffmpeg, loop 1 image, -i image, -i audio, -c:v video codec, -c:a audio codec, -b:a audio bitrate, make the video as long as the audio, out.mp4 = filename output

I can also use "" and forward slashes to denote the location of the input/output files so I don't just create random files in unknown locations on Windows

Here's a working example:
ffmpeg -framerate 24 -loop 1 -i "C:/Users/Ember/Videos/ffmpeg/images/14days.png" -i "C:/Users/Ember/Videos/ffmpeg/audio/02.wav" -c:v libx264 -c:a aac -b:a 192k -pix_fmt yuv420p -shortest "C:/Users/Ember/Videos/ffmpeg/02.mp4"

The `-pix_fmt yuv420p` part is just for compatability. It works perfectly fine on Youtube with or without this parameter, it just impacts if a thumbnail is shown on the windows explorer and if the built-in Films And TV app can play the video portion of the video. The audio is still in-tact.

Cool fax
