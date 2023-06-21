# Installation of nvidia-docker

Install the nvidia-container-runtime by following these instructions.
- https://github.com/NVIDIA/nvidia-container-runtime#installation

# Prepare the data folder

By default docker will try to mount a folder called 'media' located in the root folder of this repository. This 'media' folder can be a symlink to your data.

# Build and start the container

Build the container :
```
docker-compose -f docker-compose-gui-nvidia.yml build
```

Run the container :
```
docker-compose -f docker-compose-gui-nvidia.yml up
```

Attach a terminal to the container after running it :
```
docker exec -it digiforest_docker bash
```

Run director inside the docker container : 
```
roslaunch director_digiforest digiforest.launch
```

# Known issues

- Inside docker, the buttons that are clicked are not highlighted, which gives the wrong impression that you cannot click on them. 
- Without nvidia-container-runtime the gui is very slow