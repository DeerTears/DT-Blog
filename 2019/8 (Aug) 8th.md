I'm going through a lot with Godot 3.1.1's audio right now. It's been fun, but more importantly it's been incredibly infuriating to figure out.

## My Background (skippable cutscene)

I'm a musician. I learned Scratch and then got stuck for the next 10 years figuring out how code works. With (huge) help from my partner I've come to really understand the way that Godot works and also to properly understand some of the high-level programming tricks. I had claimed to love and know Lua for so long but I didn't even really understand functions with their own arguments, arrays, utilising booleans correctly, and other little optimisations. It's been really fun to go from only knowing how to print("hello world") to now be writing code by hand in an external editor because I know the syntax well enough for basic input-checking scripts.

I worked like crazy on one project where I just tried to stuff everything I could learn into one project. It started with accessing a label node and changing the text to ("pressed " + Times as String + " times.") and eventually wound up becoming a metronome. I was pretty satisfied with how it turned out even if it had its messy quirks. The metronome had barely any control over its speed, the fastest speed I deemed too dangerous for people with photosensitivity, but it seemed consistent and incredibly functional. All I had left to do was add the sound and tweak some other parameters.

The sound part of this project has given me the longest-running headache of my life, but at least it doesn't compare to the time-intensive theory tests I took in university. But it's still kinda close.

## The good stuff:

Godot has 3 versions: 1.X, 2.X and 3.X. I actually know nothing about 1.X but since nobody talks about it anymore I feel it's safe to assume I don't need to know. In 2.1 they polished a lot of features to the code that lets developers make the most of its current audio engine. 2.1 has a lot of really useful global properties like AudioServer.get_time_to_next_mix() as well as a custom audio buffer in each project. BUT, the only article that goes over ANY of this is this document: https://docs.godotengine.org/en/latest/tutorials/audio/sync_with_audio.html#using-the-system-clock-to-sync

These functions are all in 2.1, but nowhere does it say that nearly all of its contents are currently 2.1 exclusive or in the latest branch. My only clue was the fact that going to the official 3.1 docs doesn't show this "sync the gameplay with audio" bar and that the url says latest/ where normally it says 3.1/ or 2.1/. I actually don't know how to find this latest unstable version of Godot since all the releases only show stable versions. So I guess my answer is that all these really helpful code bits are stuck in 2.1 and haven't made the transition to 3.1 or 3.2.

## Other's issues that back-up what I'm saying:

I did some digging around the issues for Godot and found these fantastic issues:

https://github.com/godotengine/godot/issues/27230
"Moreover, when profiling in Godot 3.1, I notice the Audio Thread and Audio Driver take a lot of frame time. They fluctuate, and a lot of the time they're over 50%, sometimes beyond 100%: I noticed a few frames over 300% or even 600%."

Wait, there's an Audio Profiler? And wow, yeah it looks like the Audio Driver and the Audio Thread take a lot of frame time from the engine AND they fluctuate by default with no sounds! The example project that Skaruts linked with a tilemap has no soundfiles used: https://github.com/godotengine/godot/files/2982534/Simple.Cell.Rendering.Test.zip but that doesn't stop it from having wonky Audio chunks. So that explains a lot about my metronome, the one thing that is going to be dependent on these audio chunks.

Now I do recognise that 3.0 actually rehauled audio so in 99% of cases this won't be an issue, the audio buffer is now small enough that basically no human will notice there's a delay between pressing a button and the sound playing. Even for rhythm games, it's possible to use the animation player or getplaybackposition of an audiostream to link in-game events to the music. This metronome is the only case where I'm begging the audio chunks to be consistent, and 3.X doesn't want to provide any of that. It just takes up less frametime overall compared to 2.X. There's demos for Godot that I discovered at this point which includes a BPM_Sync demo: https://github.com/godotengine/godot/issues/28553 and wow! This is super helpful! It can only be opened in 2.X which explains a lot.

I guess what I wanted was some kind of disclaimer that these audio functions were not possible in 3.X at the moment, and downgrading to 2.X is where I could try to narrow down this latency and then account for it in an increased Audio Buffer...or something. I dunno, I really hope I can be forgiven for not figuring this out any sooner because I'm still new to Github and everyone I ask reassures me that the website's design is barely intuitive to people who don't understand git at all.

## Other issues describing problems with Godot's audio latency:

https://github.com/godotengine/godot/issues/30562

"Looking at the WASAPI audio driver, it looks like we have no control on the size of [3.0's] audio buffer/latency, which is likely why the setting isn't exposed." - Akien-mga

https://github.com/godotengine/godot/issues/26566

"Repeatedly playing AudioStreamPlayer2Ds with a WAV file that has loop info either causes weird noises or plays as if it started at the end before actually play from the beginning.
Using AudioStreamPlayer2D.seek before playing makes the sound play from start, quickly stopping and quickly restarting like it was a small audio hickup..."
"...Before playing the audio, seek it to 0.0 and then play it starting from -1.0
`$AudioStreamPlayer2D.seek(0.0) $AudioStreamPlayer2D.play(-1.0)`
Interally as far as I got it by reading the source code, when you play it from a value bellow 0.0, it'll skip some stuff on _mix_audio method, so seeking before playing it at -1 will make sure things are alright internally so it can skip that small code block and play normally. Playing at -1 before seeking won't actually play the audio at all." - wagnerfs

## What I'm going to do to help fix this:

1. Hunt down that latest branch for the docs and add in that this is not present in the stable 3.1.1 build, in case some poor soul ever comes across it again.

2. Link the Performance class in the audio doc for 3.1.1 since this is the closest thing that 3.1.1 currently has.

3. Link the custom audio stream tutorial in the audio section (it's C++ but it's something for those who are still searching and can't find more than 2 pages on audio in 3.1's docs)

4. Make a video detailing my experience with this so I can maybe get even more answers from folks

5. Try other solutions: FMOD for Godot by alexfoneska and its GDNative fork, SDL, SFML, and document my experience using those for future Godot musicians.

## What I'll be doing in the meantime that isn't this

Code anything but a metronome. I'm going through a tutorial series (https://youtu.be/nk0YQGb08IA?list=PLQsiR7DILTczMLsN8qmMym7pYfJXynzK0) to learn more about control nodes and making applications with Godot instead of games, since that seems to interest me the most right now. I'm also considering making games for Godot that use Midi controllers as the controller, since I already have my own code which successfully reads these inputs in Godot, and it's not a metronome.

I'm also working with my partner on a visual novel, they've made some pretty neat code for a groundwork and I'm looking forward to creating something with a focus on telling a variety of stories of the LGBTQ+ community. This would also be in Godot.

I'll be learning more C# and Unity as I've already been making steady progress for a job I'm doing, and I've seen how Unity's default audio engine is much stronger for making audio-based applications like the ones that I plan to make, such as a tool for laying out mixed meters, a tool for building chord progressions, a tool for easily writing western rhythms digitally, and who knows what else. I imagine I'll be switching over at some point but that might not be for a while.

## In Closing:

I hope this has helped anybody else who has the same issues as myself with Godot 3.X's audio, and if at the least this offers sympathy to others who have suffered through it. Feel free to take on the solutions I noted earlier if you see that they haven't already been done and you're feeling like doing something about this. Hopefully my next log won't be as complaint-riddled and I can just talk about breakthroughs or successes, but this is the culmination of many weeks of digging and pain just trying to learn about Godot and how I can combat.

If you're reading this, I hope something unexpectedly positive comes your way. o/
