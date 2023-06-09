# state-reader: Touhou Data Analysis

Simple python tool to extract game state data for a given frame: 
* player coords and movement state, 
* resources, 
* list of on-screen enemies, bullets, items and lasers, 
* screenshot (optional, slow)

<br>Meant to help parakeets analyze their games; should be easy to build various analysis tools on top of this (feel free to fork). For instance: over the next 5 seconds, when/where will the biggest bullet cluster of a given radius be?

Doesn't yet work with every game and will definitely need some changes to maximize usability
<br>If you have feature requests or need help making your own custom analysis let me know

Supported games:
* DDC

Goals:
* Minor stuff to add: seija flip data, current RNG value, Grow Bigger & You Grow Bigger
* Save-stating
* Multi-game support (refactoring)
  * Re-examine need for storing values prior to declaring dataclasses
* UM support
* LoLK support
* MoF support 
* Player bullet/bomb data?

To add your analysis code, go to `analysis.py` and implement `__init__`, `step` and `done`; you'll see a few basic examples there to help you. I decided to make this a class to give you better control over the init step, which happens right before the extraction starts (rather than during setup), and to make it easy to swap between different analyses.
<br>If you need screenshots, set the `requiresScreenshots` boolean at the top of the `state-reader.py` to True (RGB and Greyscale available). You can also disable extracting bullets, enemies, items and lasers to make extraction faster with the `requiresBullets`, `requiresEnemies`, `requiresItems` and `requiresLasers` booleans respectively (True for all by default).

Huge credits to ExpHP for helping out with the extraction.

## Setup 
TODO: UPDATE
Let's use a venv to minimize python headaches; you'll need to activate it every time.
<br>(you might be prompted to install virtualenv if you haven't, it'll tell you how)

Windows:
```bash
python -m venv venv #only do this the first time
venv\Scripts\activate
pip install -r requirements.txt #only do this the first time
```

Linux/Mac:
```bash
python -m venv venv #only do this the first time
source venv_name/bin/activate
pip install -r requirements.txt #only do this the first time
```

If you need to exit the venv for whatever reason (script will no longer work), type `deactivate`.

## Running
TODO: UPDATE

To get the state once:
```bash
python state-reader.py
```

To get the states over 500 in-game frames (# must be integer):
```bash
python state-reader.py 500f
```

To get the states over 10.5 in-game seconds (# can be decimal):
```bash
python state-reader.py 10.5s
```

Depending on how fast your machine is and how much stuff is on screen, extracting the game state can take longer than a frame (1/60ths of a second) and as a result, the extracted frames **will not be contiguous and some frames will have been skipped**. For instance, if I run `python state-reader.py 100f`, we'll go from frame #2901 to #3049 after extracting 100 frames (a difference of 148): 48 frames that happened during the extraction were skipped. 

To **prevent this**, add the argument `exact` to your command, i.e.: `python state-reader.py 100f exact`. This will slow the game down to ensure extraction always finishes in time for the next frame (and as a side-effect, it'll help you be more precise if you plan to play while this is going on).

Either way, extraction will most likely take longer than the actual time specified (especially for longer periods).

## Screenshots

Single state extraction:

<img alt="single state extraction" src="https://i.imgur.com/mKAfFJ0.png" width="600px">

Analysis over 50 frames (`exact`):

<img alt="analysis over 50 frames" src="https://i.imgur.com/voSiS0I.png" width="300px">

Various analyses:

![9head bullet count over time](https://i.imgur.com/nLY7TPQ.png)
![FMH close bullets over time](https://i.imgur.com/o11hOLC.png)
![SUR bullet scatter plot](https://i.imgur.com/zXazVcT.png)
![Shimmy laser plot](https://cdn.discordapp.com/attachments/913211531158749227/1105889947241693396/image.png)
![Benben laser plot](https://cdn.discordapp.com/attachments/913211531158749227/1105993194233139351/image.png)
![Modded laser plot](https://cdn.discordapp.com/attachments/205514395566997514/1106354957281665034/image.png)