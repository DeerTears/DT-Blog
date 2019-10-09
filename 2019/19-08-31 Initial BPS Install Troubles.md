Damn this thing is difficult to install! Like, I'm so close, but the tutorials are on the old version of BPS (not 1.3) but of course it was 1.3 that got me excited to start using it.

I've got most of its useability figured out, I'm really excited to have an open source video editor that's actually really strong and easy to understand, but the proxies (previews) keep rendering really slow and I've been going through the arguous task of figuring that all out.

I have all the steps worked out perfectly but it's just...for...an earlier version...where do I install BPS into Python's scripts to pull from so I can call upon it from the Powershell? I dunno it's heck

My current notes:

Installing BPSProxy individually?
C:\Users\Ember\AppData\Local\Programs\Python\Python37-32\Scripts\BPSProxy ???
:It can be installed as a standalone command line utility [via PiPy](https://pypi.org/project/bpsproxy/): `pip install [--user] bpsproxy`. *Note* that you have to have `$HOME/.local/bin` included in your `$PATH` environment variable (on unix) if you're going to install the utility locally (using `--user` when executing `pip`).:
But I probably don't need to go that deep...right? Idk we're gonna need to ask help from BPS discord

Workflow for when you get it installed:
https://www.youtube.com/watch?v=xZoZaSsuhXw

Older installation of BPS tutorial might have this standalone proxy renderer installation? https://youtu.be/Zcj4onvP06w
