# audioio
Platform independent interfacing of numpy arrays with audio files and devices.

The modules try to use whatever available audio module to achieve
their tasks. It does not provide own code.

Run the `audiomodules.py` script to see what modules you already have installed on your system,
which ones are recommended to install, and how to install them.

Usage:
------
```
import audioio as aio
```

Load an audio file into a numpy array:
```
data, samplingrate = aio.load_audio('audio/file.wav')
```
	
The data are numpy arrays of floats ranging between -1 and 1.
The arrays are either 1-D arrays for single channel data,
or 2-day arrays with first axis time and second axis channel.

You can also randomly access chunks of data of an audio file, without
loading the entire file into memory. This is really handy for
analysing very long sound recordings:
```
with open_audio_loader('audio/file.wav', 60.0) as data:
     block = 1000
     rate = data.samplerate
     for i in range(len(data)/block):
     	 x = data[i*block:(i+1)*block]
     	 # ... do something with x and rate
```

Write a numpy array into an audio file:
```
write_audio('audio/file.wav', data, samplerate)
```

Play a numpy array as a sound:
```
play(data, samplingrate)
```
or just beep for half a second and 440 Hz:
```
beep(0.5, 440.0)
beep(0.5, 'a4')
```

Documentation:
--------------
See the modules in `audioio/` for further and more detailed docmentation:
- `audioloader.py`: reading audio files
- `audiowriter.py`: writing audio files
- `playaudio.py`: play a sound through your audio board
- `audiomodules.py`: query installed modules
