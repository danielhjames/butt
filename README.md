butt (0.1.17) Manual
====================
Author: Daniel Nöthen
:email: butt at danielnoethen dot de

This repo is modified by: @melchor629

About
-----
butt (broadcast using this tool) is an easy to use, multi OS streaming tool. It supports ShoutCast and IceCast and runs on Linux, MacOS and Windows. The main purpose of butt is to stream live audio data from your computers Mic or Line input to an Shoutcast or Icecast server. Recording is also possible. It is NOT intended to be a server by itself or automatically stream a set of audio files.


Install
-------
#### OS X:
Download `butt-osx.zip`, extract it and copy the app to Applications.

#### Windows:
Download `butt-win.zip`, extract it inside a folder and it's ready to use.

#### Debian based distros:
Butt depends on the following packages and their dependencies:  
- `portaudio19`
- `libvorbis`
- `libfltk1.3`
- `libmp3lame`
- `libflac`
- `libsamplerate`
- `libopus`
- `gettext`
- `libiconv`

Download `butt-linux64.zip`, extract it inside a folder and it's ready to use.

#### Linux/MinGW:
First of all you need to have the same libraries as Debain based distros installed on your system, but with dev version (headers and libraries). They are quite common and should be included in every linux distribution.
After installing the above libraries you can install butt from source as usual:

- `tar -xzf butt-src.tar.gz`
- `cd butt`
- `./configure`
- `make`
- `sudo make install`


Quick start
-----------
When you start butt the first time, it will create a default configuration file in in your home directory ('~/.buttrc') on Linux and OS X or at 'C:\Users\\[username]\AppData\Roaming\buttrc' on Windows.

In order to connect to a server, you need to add a new server in the config window.  Just open the settings window and click on [ADD]. Now fill in the input fields with the server data and click on the new [ADD].

Adding Stream Infos is not necessary for connecting to a server.


Configuration
-------------
The command line option `-c <path_to_file>` allows you to define a new standard configuration path. This makes it possible to have multiple instances with different configurations running. In case the file does not exists, butt will create a default file.

[Save]: Saves your current settings to the standard configuration file or to the file that was passed to the -c option
[Export]: Saves your current settings to the given file
[Import]: Loads the selected file and applies the settings

CAUTION: If you use the -c command line option and import another configuration file by using the import function, pressing [Save] will overwrite the file that was passed to the -c option.


Main Window
-----------
The dot matrix display shows you the current state of the butt software. +
The states are: idle, streaming, recording. When in streaming and/or recording state you can cycle through the information by clicking on the display. You can choose between online duration, data sent, recording duration and data recorded

The [>] symbol shines yellow if butt is connected to a server.
The [O] symbol shines orange if the +[start rec. when connected] checkbox is activated.
The [O] symbol shines red if butt is currently recording.

The coloured LED lights (vu-meter) indicate the current input volume.  For best listening experience for you listeners I suggest to have the input volume below or within the orange LEDs. Never let the volume go up to the red LEDs, they indicate saturation.

Gain slider:
The slider is only visible when the little __[more/less]__ button below the __[settings]__ button was clicked. With this slider you can attenuate and amplify the input signal between *-24dB* and  *+24dB*, respectively.  Double clicking the slider resets the gain to *0dB*.  Use this slider only to fine tune your input signal. It does not change the operating systems input volume setting. Instead, the input signal is multiplied by the given factor. Thus adding to much gain will also add lots of noise.

Streaming
---------
To start streaming just klick the play symbol. butt will try to connect to the server until you press the stop symbol.

You can stream with 3 different codecs: _mp3_, _ogg/vorbis_ and _ogg/opus_. In case opus is selected the samplerate is always upsampled to 48kHz. Upsampling needs lot of CPU power. You can change the up sampling algorithm in the **[Advanced]** settings on the **[Audio]** tab. Upsampling is deactivated if you select 48kHz as sample rate.

Unfortunately, it is not possible to update Stream Infos while streaming. You need to reconnect for updating the Stream Infos.

However, at least you can update the current song on the fly. You only need to type the song into the **Song Name** input field at the **[Stream]** tab and hit Enter or click **[OK]**.

butt can also update the song automatically from a text file. The first line of the text file must be the name of the song. As soon as butt detects that the file has been changed it updates the name of the song on the server. In addition, if you are in Mac OS X, you can update the song from current iTunes or Spotify song with a simple click.
Don't hesitate to write a plugin for other audio players. Just mail them to me and I'll add them to the butt package.

**Stream infos:**
In the **[stream]** settings window you can add stream infos. This allows you to deliver more details of your stream station. For example the genre of your music, description of your station, web address etc.

Recording
---------
butt is able to record and stream simultaneously in different bit rates. For example you can stream with 96kbit and record with 192kbit. Recording is possible in *mp3*, *ogg/vorbis*, *ogg/opus*, *FLAC* or *wav*.

In case **opus** is selected the samplerate is always upsampled to *48kHz*. Upsampling needs lots of CPU power. You can change the up sampling algorithm in the **[Advanced]** settings on the **[Audio]** tab or disable it by selecting *48kHz* as sample rate. Not all sound interfaces support a samplerate of *48kHz*, though.

To record you first need to select the destination folder and specify a file name in the **[Rec]** tab. butt will replace the tokens *%d*, *%m* and *%y* with the current day, month and year. All this tokens can be seen in the same same tab.
e.g. `rec_(%m_%d_%y).mp3` -> `rec_(03_28_2008).mp3`. Other possible time tokens are *%H* (hours) *%M* (minutes) *%S* (seconds).

With the *%i* token you can add an index number to your file name. +
This means with `rec_%i.mp3`  butt first tries to open `rec_0.mp3`. If that file already exists, butt tries `rec_1.mp3` and so on...

If the **start recording when connected** checkbox is activated butt starts the recording immediately after being connected to a server.

To manually start the recording press the record symbol.
To stop recording simply click on the record symbol again.

You can also tell butt to split your recording into separate files every *n* minutes. Just enter a number higher than 0 into the **Split file every [..] minutes** field.
Let's assume your file name is `rec_(%m_%d_%y)_%i.mp3` Then the first file is expanded to `rec_(03_28_2008)_0-1.mp3`, the second after *n* minutes to `rec_(03_28_2008)_0-2.mp3`, the third to `rec_(03_28_2008)_0-3.mp3`, you got it. If the **sync to full hour** checkbox is activated the automatic file splitting is synchronized to the full hour. That means if the time is *8:55* and file splitting is set to **15 minutes**, the second file starts at *9:00* and the third at *9:15*.


Uninstall
---------
####OS X:
Delete the *butt.app* from your 'Application' folder and remove the configuration file from '/Users/[username]/.buttrc'.

####Windows:
Run the Uninstaller from the butt folder in your windows start menu.

####Linux:
Delete the exectuable and the configuration file from '/home/[username]/.buttrc'.

Contact
-------
melchor9000@gmail.com (maintainer of this fork)
