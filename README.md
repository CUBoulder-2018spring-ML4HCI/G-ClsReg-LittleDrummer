# G-ClsReg-LittleDrummer

Derek Prince, Andrew Lim

## Overview
Video: [Processing]()

For this project we wanted to use the Leap Motion to allow people to play a musical instrument with their hands in the air. In the end we chose to use a piano-like movement to control drum sounds with linear regression.

## Tools and Hardware
We used [Processing](https://processing.org/), [Input Helper](http://www.wekinator.org/kadenze/#Install_the_8220WekiInputHelper8221), [Wekinator](http://www.wekinator.org/downloads/), and the [Leap Motion SDK](https://developer.leapmotion.com/).

We also used a Leap Motion as one might imagine.

## Features

Starting with only the 5 finger tip positions x, y, and z coordinates being sent to Wekinator, we quickly realized that we needed something to detect a depressed finger that was relative to the hand rather than free space (this was to allow your hand to be at whatever height is comfortable without messing up the finger-press detection).
To do this we added an OSC message that tracks the center of your hand in x/y/z and use Input Helper to send 5 new signals:

* ThumbPalmDiff = PalmY[n] - ThumbY[n]
* IndexPalmDiff = PalmY[n] - IndexY[n]
* MiddlePalmDiff = PalmY[n] - MiddleY[n]
* RingDiff = PalmY[n] - RingY[n]
* PinkyPalmDiff = PalmY[n] - PinkyY[n]
(The processing sketch uses `y` as vertical)

Additionally, we chose to ignore the y and z axis because we were 'modeling' a keyboard-like feel where your hands only vary much in x (if we choose that to be side-to-side as the feature extractor does).
It could have been interesting to allow for z and y to have a greater effect on the instrument/output but as we only had 3 outputs at this time, we were already mapping inputs to outputs at something approximating 5-to-1.

#### [Add pictures]

## Training Algorithm

We chose to use a linear regression model for our data set. The reason for this over a NN or polynomial regression because we wanted a very smooth, linear transition over the 'keyboard' without the large feature-space on the extreme ends from a NN sigmoid function, or the non-uniform/linear mapping of a polynomial regression.
One unforeseen bonuses we found from using a linear regression was how the small number of training examples needed made it really easy to re-train the model to try to find a fun combination of input/outputs.

## Further Goals

We originally wanted this to work with AbletonLive but could not get it working in a reasonable amount of time. It would be significantly more powerful and could make better use of a larger feature set though. [Chuck](http://chuck.cs.princeton.edu/) would also have made for a good example with a little experience.

The Processing sketch only sends data on one hand in OSC but tracks two. It would be cool to add another hand (while reconciling sensor issues along the way) to create more complicated interactions. Ableton Live would be almost a requirement though.

## Credits

* Darius Morawiec - [Leap Motion for Processing](https://github.com/nok/leap-motion-processing)
* Andreas Schlegel - [oscP5](http://www.sojamo.de/libraries/oscP5/)
* Rebecca Fiebrink - [Wekinator and Misc](http://www.wekinator.org/examples/)
