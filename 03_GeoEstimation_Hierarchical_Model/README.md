# How to use the repository GeoEstimation


## How to manage all dependencies




## Downloading the models

There are problems with extracting the following 3 models: 
'base_M.tar.gz':
    'https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/base_M.tar.gz',
'ISN_M_indoor.tar.gz':
    'https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/ISN_M_indoor.tar.gz',
'ISN_M_natural.tar.gz':
    'https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/ISN_M_natural.tar.gz',

Please download and extract them manually.
(`commands`) and rename the old files to .tar.gz

After that run `downloader.py `
(and skip the 3 manually downloaded models)



## Downloading the test data set

- 




## How to use Docker

1. Install it

2. Build docker image

3. `sudo docker run --volume $(pwd):/GeoEst -w /GeoEst -u $(id -u):$(id -g) -it geoloc bash`

`run` : start container

`--volume`: mount left path on host system to right path in container (leftpath:rightpath)
to be able to work with local files (read and write)

`-w /GeoEst` : set GeoEst as working directory

`-u`: set user and group id to allow access to mounted files

`-it`: interactive terminal

`geoloc`: docker image name

`bash`: command to start terminal/shell





## How to make an inference?

start bash in docker container:
`sudo docker run --volume $(pwd):/GeoEst -w /GeoEst -u $(id -u):$(id -g) -it geoloc bash`


`python inference.py -i gps_query_imgs/*.jpg -m base_M`

