# Data Generation Image

### USAGE

* Pull the base image
```
singularity pull --name RG-dgen.simg shub://ozanarkancan/ReGROUND:dgen
```

* This image is not complete due to the ros requirements. You should add the created overlay image or create that image and complete the setup.

* You can dowload the created overlay image from [here](http://ai.ku.edu.tr/download/reground/dgen_overlay.simg) .

* Connect to the container with the overlayed image. 
```
singularity shell --overlay overlay.simg RG-dgen.simg
```

### Creating the overlay image and completing the setup

* Create the overlay image
```
singularity image.create --size 2048 overlay.simg
```

* If you need more space, you can expand this image later
```
singularity image.expand overlay.simg
```

* Connect to the container with the overlayed image.
```
singularity shell --overlay overlay.simg RG.simg
```

* Create catkin workspace
```
source /opt/ros/indigo/setup.bash
cd /workdir/rg/src
catkin_init_workspace
```

* Copy or download the datagen package to /workdir/rg/src/
* Compile the package
```
cd /workdir/rg
catkin_make
```

* Source package environment variables
```
source /workdir/rg/devel/setup.bash
```

* Now you are ready to run the package
* Test it by running the core, launch file, and the ros executable
```
roscore & disown
cd /workdir/rg/src/datagen/dg
roslaunch dg.launch & disown
rosrun dg dc_datagen
```

### Usage on the kuacc cluster

* Load necessary modules
```
module load singularity
```

* Set SINGULARITY_CACHEDIR as your scratch
```
export SINGULARITY_CACHEDIR=/scratch/users/username
```

* On a compute node with gpu
```
singularity shell --bind --overlay overlay.img --nv RG-dgen.simg
```

### DEPENDENCIES
* Singularity
