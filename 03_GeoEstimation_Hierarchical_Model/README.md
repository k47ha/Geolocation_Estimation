# How to use the repository GeoEstimation

The following instructions will guide you through the process of downloading the models of the repository [GeoEstimation](https://github.com/TIBHannover/GeoEstimation), downloading the [test data set of IM2GPS](http://graphics.cs.cmu.edu/projects/im2gps/) and making a prediction/inference for an image from the test data set.

1. Navigate into the folder `GeoEstimation/`


## Downloading the models

In the [repository](https://github.com/TIBHannover/GeoEstimation) you will find a script `downloader.py` which should download all necessary models, weights and the scene hierarchy. But as there are problems with automatically extracting the following 3 models, they have to be extracted manually:

1. Download and extract the following files manually and put them into a new folder called */resources*:
- 'base_M.tar.gz'
  - [https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/base_M.tar.gz](https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/base_M.tar.gz)
- 'ISN_M_indoor.tar.gz'
  - [https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/ISN_M_indoor.tar.gz](https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/ISN_M_indoor.tar.gz)
- 'ISN_M_natural.tar.gz'
  - [https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/ISN_M_natural.tar.gz](https://github.com/TIBHannover/GeoEstimation/releases/download/v1.0/ISN_M_natural.tar.gz)

```
mv base_M.tar base_M.tar.gz
```
gunzip base_M.tar.gz
tar xvf base_M.tar
```

1. Rename the old files to .tar.gz
```
mv base_M.tar base_M.tar.gz
```

1. Run the script `downloader.py ` (skip the 3 manually downloaded models).

2. Make sure the ResNet 152 model for scene classification trained on Places365 as well as the hierarchy file for scene-classification are saved in a folder called */resources*. Make sure the TensorFlow geolocation model files are saved in a new folder called */models*.


## Downloading the test data set

We will use the small IM2GPS test set which only consists of 237 images (39 MB).

5. Download the *im2gps test set, 237 images, 39MB* from the [IM2GPS website](http://graphics.cs.cmu.edu/projects/im2gps/).



## How to use Docker

The repository provides a Docker image that takes care of meeting all requirements and therefore makes it easy to run the code.

6. Install Docker (the easy (a little bit unsafe) way)
   
   Run `curl -fsSL https://get.docker.com -o get-docker.sh` in your Terminal.

7. Build the Docker image
    
```shell script
    docker build GeoEst -t geoloc
```


8. Start an interactive Terminal session in your Docker Container
   
   Run `sudo docker run --volume $(pwd):/GeoEst -w /GeoEst -u $(id -u):$(id -g) -it geoloc bash` in your Terminal.

Here is what it means:

`run` : start container

`--volume`: mount left path on host system to right path in container (leftpath:rightpath)
to be able to work with local files (read and write)

`-w /GeoEst` : set GeoEst as working directory

`-u`: set user and group id to allow access to mounted files

`-it`: interactive terminal

`geoloc`: docker image name

`bash`: command to start terminal/shell



## How to make an inference?

We want to predict the longitude and latitude of all the images in the IM2GPS test data set that we downloaded earlier (`gps_query_imgs`) using the Individual Scene Networks.

9. Make sure you startet a Terminal Session in your Docker Container as described in step 8.

10. Execute the script `inference.py` and provided the command line arguments (-i: input images; -m: chosen model)

    Run `python inference.py -i gps_query_imgs/*.jpg -m ISN` in your Terminal.

    Of course you can replace `gps_query_imgs/*.jpg` by a path to the image of your choice.



## Or look at this Google Colab Notebook

Link to the [Colab Notebook](https://colab.research.google.com/drive/1RblmA1350CfQBW8MtcS8T9ZOCcct9jf4?usp=sharing).



## Credits

Partly taken and inspired by the ReadMe from (TIB Hannover GeoEstimation)[https://github.com/TIBHannover/GeoEstimation/blob/ba8a79492fe664be029145aab96774ca4a474b04/README.md].