Making Quake maps has been interesting. I've been doing it so I can use the Qodot plugin to turn the geometry from Quake into level geometry for Godot, my favourite (and best-known) engine so far. I'm currently experimenting with turning my old maps for TF2 and CSGO into geometry that Godot can run, and that involves a loaded process.
1. Download BSPSource https://tf2maps.net/threads/tutorial-decompiling-maps-with-bspsource.22131/
2. Download the map of your choosing https://steamcommunity.com/sharedfiles/filedetails/?id=575371559 , https://steamcommunity.com/sharedfiles/filedetails/?id=1368986210, https://steamcommunity.com/sharedfiles/filedetails/?id=1542876527
3. Decompile it, and load it into J.A.C.K. as a .vmf http://jack.hlfx.ru/en/
4. Save it in J.A.C.K. as a .map file
5. Import that .map file to Trenchbroom to do any final edits before sending it to Qodot, since Qodot is parsing Trenchboom's method of storing .map files
And then I've got my old Valve maps in Godot!

The only problem is that J.A.C.K.'s method of a .map file is too different from Trenchbroom so there's errors in TB when it tries to load the file. It's stuff I could debug line-by-line if I wanted to for each piece of miswritten geometry...
The weird part is that apparently it works TB to JACK? Just not JACK to TB?
Eh well, my brushwork has never been that great up until the beginning of this year, so maybe it's best I just re-create these things from the ground up with a better idea of what they'll be used for.

Also, I seriously need to work more on my 3D game system so I have a purpose for putting these maps in Godot. I have a third person pill-thing with a completely static camera. Ah well, eventually.
