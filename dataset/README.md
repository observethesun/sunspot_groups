## Dataset of sunspot groups

File `sunspot_dataset.zip` contains a dataset of sunspot groups observed at the [Kislovodsk Mountain Astronomical Station](http://en.solarstation.ru/). In total there are 8498 sunspot groups in the dataset for the period 2010--2020 observed in the central part of the solar disk (within 60 degrees from the central meridian).

### Filename

Each filename in the dataset has the format YYYYMMDDHHMM_N, where YYYYMMDDHHMM are the date and time of the observation, N is the sunspot group number assigned by the station. The same sunspot group numbers are also shown on the website [https://observethesun.com/](https://observethesun.com/). For example, file 201512180623_299.npz represents sunspot group number 299 observed on 2015/12/18_06:23UT. Select this date on the [https://observethesun.com/](https://observethesun.com/) or use this direct [link](https://observethesun.com/?current=2015-12-18&objects=3f&past=2014-11-25) to see this sunspot group on the map of solar activity.

### File format

Files in the dataset are given in the sparse format `.npz`. Use the Python function [`scipy.sparse.load_npz`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.sparse.load_npz.html) to open the files. In order to represent data in a spatial form, reshape the array to the shape (256, 256, 3). Below is an example of file loading:

```python
from scipy import sparse

data = sparse.load_npz('201512180623_299.npz').toarray().reshape(256, 256, 3)
```

### Data description

Each file in the dataset contains 3 binary masks of size 256x256 pixels that describe the shape of the sunspot group. The first mask describes the position of sunspots, the second mask describes sunspot cores, and the third mask describes pores.

In addition, file [sunspot_group_properties.csv](./sunspot_group_properties.csv) contains physical properties of sunspot groups: 
* fname - filename of the sunspot group in the dataset (also the filename format YYYYMMDDHHMM_N encodes date, time of observation and sunspot group number)
* date - date and time of observation
* group_number - sunspot group number
* lat_max - maximal heliographic latitude of sunspot group pixels
* lat_min - minimal heliographic latitude of sunspot group pixels
* lat_mean - mean heliographic latitude of the sunspot group
* long_max - maximal Carrington longitude of sunspot group pixels
* long_min - minimal Carrington longitude of sunspot group pixels
* long_mean - mean Carrington longitude of the sunspot group
* area - sunspot group area in MSH (millionth of the solar hemisphere)
* nspots - total number of spots and pores in the sunspot group
* ncores - number of cores in the sunspot group
* nspots_with_cores - number of spots with cores
* tilt - inclination (in degrees, positive clockwise) of the regression line fitted to the sunspot group
* complexity - integer number, reflecting complexity of the sunspot group. Defined a the number of principal components, at which the reconstruction error is half the reconstruction error for the first principal component
* B0 - B0 angle for date and time of the observation
* L0 - L0 angle for date and time of the observation