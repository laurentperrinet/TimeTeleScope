# TimeTeleScope

The goal is to realize a time-lapse using a raspberry π and some python code and finally get this:

![](videos/2021-02-17_TimeTeleScope.gif)

(This was done over 10 days, with *almost* each day an *irregular* session the morning and one in the evening)

## data acquisition

This is well documented on the web and consisted in simply:

* setting up the raspberry π to use the camera
* create a startup script [`startup.sh`](startup.sh) (or clone this repo in `/home/pi` using `git clone https://github.com/laurentperrinet/TimeTeleScope)` consisting of the commands which take 2 successive frames at different exposures :
```
raspistill -rot 270 -ev -10 --metering spot -o /home/pi/Desktop/orchid/`date +%Y-%m-%d.%H:%M:%S`.jpg
raspistill -rot 270 -ev -8 --metering spot -o /home/pi/Desktop/orchid/`date +%Y-%m-%d.%H:%M:%S`.jpg
```
* run that script regularly (every ten minute) by adding the following line to the cron table (using `sudo crontab -e`):
```
*/10 * * * * /home/pi/TimeTelescope/startup.sh
```

## image processing

Three notebooks to transform a sequence of frames into a movie:

 * utilities to load images : [`A_load-images.ipynb`](A_load-images.ipynb)
 * histogram matching using different techniques (each runs `A_load-images.ipynb` first):
  * [`B_equalize-histograms-laggui.ipynb`](B_equalize-histograms-laggui.ipynb) (my first try)
  * [`B_equalize-histograms-sklearn.ipynb`](B_equalize-histograms-sklearn.ipynb) (works best)
  * using a mask : [`B_equalize-histograms-mask.ipynb`](B_equalize-histograms-mask.ipynb`) (not great)
 * putting things together : [`C_movies.ipynb`](C_movies.ipynb)  (runs `B_equalize-histograms-sklearn.ipynb` first)
