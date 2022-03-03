# Inky wHAT Weather Station 2022 Update

Inky wHAT eInk display from Pimoroni driven by a Raspberry Pi Zero (or any other Raspberry Pi) to display a seven day weather forecast.

<img src="https://dl.dropboxusercontent.com/s/uhkezjmmvqs427n/IMG_6384.jpg?dl=0" width="640" align="center">

Icons and code table are from Erik Flowers:

[Weather Icons](https://github.com/erikflowers/weather-icons)

The weather information is fetched from OpenWeather:

[OpenWeather](https://openweathermap.org)

Here you need to create an account and [an API key](https://openweathermap.org/api). Put the code into the "weather.py" file ("api_key" variable). You also need to set your location ("lat" and "lon" variables).

An easy way to find your latitude and longitude is to go to Google Maps and enter your address. Your latitude and longitude will be in the URL of the resulting map. For example, the Google Maps URL for New York City is: https://www.google.com/maps/place/New+York,+NY/@40.6971494,-74.2598655. The latitude (north/south) is 40.6971494, and the longitude (east/west) is -74.2598655. (West of the Prime Meridian, longitudes are negative all the way to the 180th Meridian in the Pacific Ocean. North of the Equator, latitudes are positive.)

The font is from David Jonathan Ross:

[Bunjee](https://github.com/djrrb/bungee)

## Setup

The Pimoroni Inky wHAT display requires a bunch of software to be installed. My recommendation is to follow the description in a Pimoroni tutorial:

[Getting Started with Inky wHAT](https://learn.pimoroni.com/tutorial/sandyj/getting-started-with-inky-what)

The installation is done by executing a bash script, and it takes a while. Everything is installed for Python 2 and 3 which isn't necessary from my point of view, so you might consider deselecting version 2 in the script before running it.

If you use Raspbian Lite, without a desktop environment, you will need to install Git, Vim, and Imagemagick.

We need to convert Erik's SVG icons to 8 bit PNG, using the Imagemagick "mogrify" command for the bulk convert. With Erik's original SVGs this would deliver PNGs with a 30 x 30 pixel resolution which is too small. Using the mogrify's "resize" option via a "vim" script (see below), we get what we need. The original SVGs are stored in a 7z-file in the "icons" folder. In the setup script "setup.sh" there is a line to remove the modified SVGs after PNG conversion (commented out, security reasons ;-) ).

The main Python file to drive the display is "weather.py". The default display is a "red" one. You may have to change the color in the Python file if you own a different one.

Here is what the setup script "setup.sh" does:

```
cd icons
7za x erik_flowers_weather-icons.7z
find -name "*.svg" -exec vim -s script.vim {} \;
mogrify -background white -format PNG8 *.svg
#rm *.svg # Commented out for security. This will remove all svg files
```
You may set up a crontab job to have the script run daily. (It's not necessary to run it more often than that, but you could if you wanted to.) [Here is a good guide on using crontab job schedules.](https://towardsdatascience.com/how-to-schedule-python-scripts-with-cron-the-only-guide-youll-ever-need-deea2df63b4e)

## Credit

* The icons are provided by Erik Flowers.
* The font is from David Jonathan Ross.
* Adapted from Rbunger's code.

## Licensing

The weather icons and the font are licensed under [SIL OFL 1.1](http://scripts.sil.org/OFL).
