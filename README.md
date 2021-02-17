# TimeTeleScope

The goal is to realize a time-lapse using a raspberry π and some python code and finally get this:

![](videos/2021-02-17_TimeTeleScope.gif)

(This was done over 10 days, with *almost* each day an *irregular* session the morning and one in the evening)

## data acquisition

This is well documented on the web 

## image processing

Three notebooks to transform a sequence of frames into a movie:

 * utilities to load images : [`A_load-images.ipynb`](A_load-images.ipynb)
 * histogram matching using different techniques (each runs `A_load-images.ipynb` first):
  * `B_equalize-histograms-laggui.ipynb` (my first try)
  * `B_equalize-histograms-sklearn.ipynb` (works best)
  * using a mask : `B_equalize-histograms-mask.ipynb` (not great)
 * putting things together : `C_movies.ipynb`  (runs `B_equalize-histograms-sklearn.ipynb` first)
