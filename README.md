# ReGROUND-img

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/565)

### USAGE

### Creating the overlay image and completing the setup

* Pull the base image
```
singularity pull --name RG.simg shub://ozanarkancan/ReGROUND:np
```

* Create the overlay image
```
singularity image.create --size 2048 overlay.simg
```

* Connect to the container with overlayed image. Don't forget to bind your cuda and cudnn paths
```
singularity shell --bind <your cuda path>:/usr/local/cuda,<your cudnn path>:/opt/cudnn --overlay overlay.img --nv RG.simg
```

* Build Knet
```
julia -e 'Pkg.build("Knet")'
```

* Create catkin workspace
```
source /opt/ros/lunar/setup.bash
cd /workdir/rg/src
catkin_init_workspace
```

* Copy or download the neuralpredicate package to /workdir/rg/src/
* Copy or download the neural components "reground_components.jld" to /workdir/rg/src/neuralpredicate/scripts/models/
* Compile the package
```
cd /workdir/rg
catkin_make
```

* Source package environment variables
```
source /workdir/rg/devel/setup.bash
```

* No you are ready to run the package
* Test it by running the launch file
```
cd /workdir/rg/src/neuralpredicate/scripts
roslaunch np.launch
```
### DEPENDENCIES
* Singularity
* Cuda drivers and libraries
* Cudnn library
