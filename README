# ClearCut

This repo allows command-line editing of movies by splicing. The purpose is to provide similar functionality to Clearplay for videos you own. It splices videos from a list of cuts.

## Usage

```
./cut <input_file> <output_file>
```

Both files can be of any format that `ffmpeg` supports. You could go from MKV to MP4, but I've just been using Handbrake for that. Integrating that would be cool in the future. Usually I just edit the MKV because it supports changes much more readily than an MP4.

This will ask for a series of scenes to cut out by timestamp. Timestamps must be entered in the format `[[h:]m:]s` (spaces can also be used as a delimiter). Non-realistic times are supported by accident (i.e. 1:0:183 for 1 hour, 3 minutes, and 3 seconds, or 1:-20:10 for 40 minutes, 10 seconds). Remember, these are scenes you want gone, not what's left.

### Script Differences

There are two scripts, `cut` and `integer-cut`. They have the same syntax and do essentially the same thing. However, `integer-cut` only supports integer seconds, while `cut` supports seconds with decimals. In addition, `integer-cut` runs faster, but may introduce AV sync errors, especially for smaller cuts.

To apply a list of changes, just feed `cut` a file with a newline at the end, for example the file `oppenheimer/visualCuts.cfg`. This is done as follows:

```
cat clearcut/oppenheimer/visualCuts.cfg | ./clearcut/cut oppenheimer_original.mkv oppenheimer_clean.mkv
```

## File Structure

Each movie will have its own folder, names using POSIX-compliant folder names. This isn't the wild west.

Each folder should have at least a `.cfg` file with a list of cuts and a `master.txt` with explanations of each cut, which allows for expansion and customization. If the master is changed, create a completely new `.cfg` file for those changes, leaving the others intact. New config files should only be created for significant changes; we don't want a new one for every permutation of cuts.

> A use case of this would be a user desiring to remove another couple explicatives from a movie. They would add those new cuts to the master in order, then create a new config file with those cuts.

## Creating Filters

Creating filters can be time-consuming, but I have a simple way I like to do it. First, there is some setup to do.

- Open a window with the original MKV movie
- Open the MKV in Audacity (you'll have to select the track)
- Open `master.txt` (and the config file, if desired)
- Open a terminal

When creating a cut, determine the cut boundaries. Run `./cut` or `./integer-cut` (see [script differences](#Script-Differences)) and put in the desired boundaries. We'll output to a test file, and use the `-t` flag so we can create a test output.

```
./cut -t oppenheimer.mkv test1.mkv
```

The "clip begin" and "clip end" prompts refer to the beginning and end of our test file - we're only testing on one scene and don't want to transcribe the entire video. Put the beginning and end at least 20 seconds from the cut boundary.

### Small cuts

Most small cuts are for an explicative. Knowing the exact time of those is difficult. However, we can use Audacity. Audacity shows the waveform and allows removing a section and listening to the resulting waveform. It's fast because you can 'see' the audio and place cuts accordingly. Keep timestamps with max 2 decimal places for best results.
