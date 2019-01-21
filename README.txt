Make sure that you have the Matlab image processing toolbox installed. 

Launch matlab.

cd to where-ever you put my code. I STRONGLY recommend against using spaces in directories or filenames. 

Edit navin_code_setup.m:
      edit the NAVIN_CODE_PATH to where you put my source code directory

Using Windows, copy put_into_C_windows_system32\pdftk.exe to C:\Windows\System32

Run navin_code_setup in matlab each time you want to use my code: 

>> navin_code_setup 

This will temporarily set the program path to the NAVIN_CODE_PATH 
directory and temporarily remove any other non-core matlab paths. This is necessary to avoid conflicts between functionnames, etc. 
These changes are NOT saved; you will need to run navin_code_setup each time unless you manually save the path. 


To track, cd to the directory containing your movies, or the directory just above.

>> TrackerAutomatedScript
Usage: TrackerAutomatedScript(argument1, [stimulusFile], other_arguments)
stimulusFile is optional
argument1 can be:
     a movie filename,
     a directory of movies,
     a cell array of movie filenames,
     a cell array of directory filenames,
     or a text file listing directories of movies
If you have a second movie my_scale_movie.avi with a object of known length, include 'scale','my_scale_movie.avi' in the argument 
If you have drawn a circle on the plate using a holepunch template as a scale marker, include 'holepunch' 
If your framerate is NOT 3, include 'framerate','my_framerate' in the argument 
If number of worms <20 or >30, then you might include 'numworms',#worms in the argument (optional)
If you have a copper ring, AND your animals are on food, include 'food' in the argument (optional)
Please see the example and README in demo_movie/

Ideally your movie (an avi file of some sort ... it works well with XVID mpeg-4) will contain some object whose dimensions are known to set the scale. 

If the argument is a directory of movies, the program will automatically try to detect the ring and worms for all the movies. It will then ask for user
assitance with problematic movies. It will then track all the movies and automatically average them.  

By default, it will look for a 28mm x 28mm frame (the copper ring). 
If it cannot find it, a GUI will pop up. 

If you draw a circle somewhere using a standard 6mm diameter holepunch, it can use that as well (include the 'holepunch' option). 

Instead of drawing on your plate of interest, you can take a short movie (10 frames) of some object whose dimensions are known, and 
include that as the scale argument. 
For example:
>> TrackerAutomatedScript('mymovie.avi','scale','my_scale_movie.avi');
>> TrackerAutomatedScript('mymovie.avi','holepunch','scale','my_scale_holepunch_movie.avi');

The data for each track are stored in rawTracks.mat, Tracks.mat (processed tracks), and linkedTracks.mat (track segments with closed gaps). 
Track files may be loaded with:
	myTrack_variable = load_Tracks('prefix.linkedTracks.mat')
BinData.mat contains the binned and averaged data, and may be loaded with:
	my_binned_data_variable = load_BinData('prefix.BinData.mat')
The relevant txt files contain the data from BinData.mat in a tab-delimited format which can be opened in Excel or with any text editor.

WormPlayer('mymovie.linkedTracks.mat') will launch a viewer. Play around with it. Zoom in and out. 
It may or may not be useful to you. It is admittedly a bit clunky ...

Copper Rings:
	Punch a 28mm x 28mm hole in Whatmann 3MM paper ( http://www.acherryontop.com/shop/cat/punches/184898 ) 
	Trim a frame.
	Briefly soak the frame in 20mM CuCl2 and place on an NGM plate. 
	Add the worms. 
	Position the plate such that the outer edge of the ring is just outside the field of view. 
	See the demo_movie for an example.
	Record at 3Hz with at least 512x512 resolution (at least 20 pixels per animal).

For lawn leaving:
	For experimental details, see Bendesky et al 2011
	See the included movie hw_1.avi for an example. The drawn circle was made using a standard 6mm diameter 
		holepunch hole as a stensil. 
	Movies should be saved as xvid mpeg-4 avi files
	leaving_events_per_min_on_lawn = lawn_leaving_analysis(Moviename, framerate, timerbox_flag);
	Returns the mean lawn leaving events per worm minute on the lawn in leaving_events_per_min_on_lawn 
	If your movie has a timerbox in the corner, set timerbox_flag to 1, else ignore it.
	For example: (no timer, 1 frames/sec)
		>> leaving_events_per_min_on_lawn  = lawn_leaving_analysis('mymovie.avi',1)
	For example: (timer box present, 1 frames/sec)	
		>> leaving_events_per_min_on_lawn  = lawn_leaving_analysis('mymovie.avi',1,'timerbox')
	If the program has a hard time finding the lawn edge or worms, the GUI will ask for your help.

There are lots of other functions and programs hidden in the package .... I need to document them all someday!

If you have any questions or problems at all, please let me know. This version has been tested on R2011b, 
but should work on later versions. Some earlier versions may give interesting errors that can
be easily fixed by changing the names of some functions. 
I have found that anytime someone else uses my software, it fails in a novel manner!! 
npokala@alum.mit.edu



