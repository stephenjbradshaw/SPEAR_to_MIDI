# SPEAR to MIDI

A simple utility that interprets spectral analysis data created by SPEAR (http://www.klingbeil.com/spear/) and creates MIDI files based on this information. It is hoped that this will be of use for musicians who want a quick way to access notation of a spectral analysis of a sound.

The program reads text files in SPEAR's 'text - partials' format. These files contain time, frequency and amplitude data generated by SPEAR's sinusoidal partials analysis. The data are processed and formatted as events which are written to file as MIDI using `mido` https://mido.readthedocs.io

## Installation
Steps for Mac/OSX (will be similar for other platforms):
* Requires Python 3. If this is not installed, download and install: www.python.org.
* Download the code in this repository: 'Clone or download' -> 'Download Zip'
* Extract the .zip  file (anywhere on your computer).
* Open Terminal and navigate to the SPEAR_to_MIDI folder, e.g. by typing `cd` followed by space, dragging the folder from the finder into the Terminal window and then pressing enter.
* Type the command `pip3 install -r requirements.txt` and press enter to install dependencies (in this case the `mido` library).

## Usage
* Create a spectral analysis using SPEAR. Use a relatively high 'Minimum amplitude threshold' value (e.g. -20dB) for best results.
* In SPEAR, under 'File' -> 'Export Format' select 'Text - Partials', then 'File' -> 'Export As...'
* Save the file inside the SPEAR_to_MIDI folder with the exact filename `SPEAR.txt`
* Open Terminal and navigate to the SPEAR_to_MIDI folder.
* Type the command `python3 main.py` to run the program.
* A MIDI file called `output.mid` will have been created inside the SPEAR_to_MIDI folder. This can be opened and edited in a score editing program like Sibelius or MuseScore.

## Limitations

* The program works best for relatively simple spectral analyses that don't have large numbers of simultaneous partials. If the program fails, try setting a higher value for 'Minimum amplitude threshold' when analysing the audio in SPEAR.
* `output.mid` is overwritten every time the program is run. To avoid accidentally losing data, save the file elsewhere on your computer after running the program.

## Data interpretation details

* Pitch: MIDI note numbers are calculated based on the *average* frequency of each partial.
* Loudness: MIDI velocity is calculated based on the average amplitude of each partial. Currently, this is scaled linearly.
* Time: Timestamps are converted from seconds to delta (relative) values in ticks once MIDI-like events have been created and sorted.

## Future development
* Add exponential scaling for amplitude to velocity conversions (currently linear).
* Write unit tests. (Currently using `doctest`).
* Identify and fix issues that prevent the program from processing analyses with high numbers of simultaneous partials.
* Experiment with higher beat resolution (PPQN) for improved timing accuracy.
* Improve data parsing efficiency.
* Add a CLI / GUI and user-configurable parameters.
* Create compiled applications for Mac and Windows.

## Author
Stephen Bradshaw (stephen.j.bradshaw@gmail.com)
