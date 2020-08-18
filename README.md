# seabirdNET 

Repo for using Keras Retinanet for seabird detection in drone imagery

### Set up environment

1. Install Docker on Ubuntu (https://docs.docker.com/engine/install/ubuntu/) 

2. Install Git

3. Clone this repo 
```
git clone https://github.com/madelinehayes/seabirdNET.git
```
4. Move into that directory 
```
cd seabirdNET
```
5. Create a Docker Image and Container based on the Dockerfile in this repo
```
docker build -t <img_name> Dockerfile
docker run --name <cont_name> -it -p 8888:8888 -p 6006:6006 -v ~/:/host <img_name> 
```
6. Create a Docker Image and Container for your deep learning environment based on the GPU Dockerfile in this repo
```
docker build -t <img_name> DockerfileGPU
docker run --name <cont_name> -it -p 8888:8889 -p 6006:6006 -v ~/:/host <img_name>
```
Your Docker container is now running. Exit that container
```
exit
```
To restart your container and attach it to the terminal
```
docker start <cont_name>
docker attach <cont_name>
```
Now start jupyter:
```
jupyter notebook --allow-root --ip 0.0.0.0 /host
```
7. Now install Keras Retinanet following the instructions here: https://github.com/fizyr/keras-retinanet

* `uas_img_handler_FINAL.ipynb` is used to split the orthomosaics created from drone imagery into smaller tiles
* The tiles created from `uas_img_handler_FINAL.ipynb` can be imported into VIA http://www.robots.ox.ac.uk/~vgg/software/via/app/via_image_annotator.html
* `via_to_retinanet_FINAL` is used to convert the output of VIA into the format Retinanet requires for training data
* `albatross_detections_FINAL.ipynb` and `penguin_detections_FINAL.ipynb` trains the model, runs validation and testing, and runs inference on the tiles created from `uas_img_handler_FINAL.ipynb`
* `export_detections_FINAL.ipynb` ingests the output from the Retinanet detections and converts into geolocated shapefiles
