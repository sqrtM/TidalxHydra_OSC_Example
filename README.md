# TidalxHydra_OSC_Example

i had some problems getting OSC set up between hydra and tidal, so I wanted to share my set-up so hopefully it can be a little easier for others to get it put together.

TIDAL BOOT FILE :

the boot file is one that I modified from the original (the changes are from lines 79-102; basically just copied from the official Tidal documentation with minor edits to make it work with haskell's weird syntax). you should be able to just straight up replace the orginal with this, assuming you haven't modified your own. it has all the stuff having to do with OSC-out, so you don't have to copy paste it every time you want to make a hydra/tidal project. the parameters i picked are semi-arbitrary; just stuff I think is useful for audio integration. you can add more (or take some away!) by just following the format I have and following the documentation at http://tidalcycles.org/docs/configuration/MIDIOSC/osc/.

The out port is set to 57101, which is the Hydra default, so you don't have to set that in hydra either. the out address is "/tidal", but you can change it to anything you want very easily by just modifying the boot file and the .js file and restarting your text editor (could be useful to have a shorter address if you're pairing this with something like Orca/Aioi, for example). lines 100 + 102 initialize the OSC stream and create the shortcut "o" (for OSC Out) to make a pattern to be sent over to hydra. you can see an example of how this works in the .tidal file.

THE .TIDAL FILE : 

the .tidal file is just a simple pattern with some oscillators on it to show how this stuff can work with different values being sent out. when you initialize it, it should make no sound (as you're not telling tidal to play any samples). you may get a message which says "Listening for external controls on XXX.X.X.X:XXXX That port isn't available, perhaps another Tidal instance is already listening on that port?". this isn't an error and everything should still work just fine. [PS, since the HUSH command only affects sound, OSC messages will not stop when "hushed". you have to # silence it to stop the flow.]


THE .JS FILE : 

extremely simple, bare minimum example. most other hydra OSC integrated files I've seen have a complex parser which iterates through the OSC message, but i thought that could be a little cumbersome (especially for live coding), so I just have variables set up to read the array values at each "tick". variable names are the same as the tidalcycles ones for the sake of readability. you can open the console with ctrl+shift+I and check the incoming feed of OSC messages for debugging purposes.

if everything is set up properly, then running the .js file and toggling hydra should yield a colorful screen and no errors. 

happy coding. let me know if i can help.
