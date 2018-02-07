Bootstrap: docker
From: ubuntu:latest

%runscript

    echo "ReGROUND image. This will be the whole pipeline."

%environment
   
   ROS_DISTRO=lunar
   LANG=C.UTF-8
   LC_ALL=C.UTF-8
   export ROS_DISTRO LANG LC_ALL
   export LD_LIBRARY_PATH=/usr/lib:/usr/lib64:$LD_LIBRARY_PATH
   export PATH=/opt/julia-0.6/bin:$PATH
   export JULIA_PKGDIR=/workdir/.julia

%post
 
   echo "Here we are installing software and other dependencies for the container!"
   apt-get update
   apt-get install -y \
    git \
    vim \
    libxml2 \
    wget \
    curl \
    cmake \
    
   apt-get update && apt-get install -y --no-install-recommends \
      dirmngr \
      gnupg2 \
      && rm -rf /var/lib/apt/lists/*
   apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 421C365BD9FF1F717815A3895523BAEEB01FA116
   echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list
   apt-get update && apt-get install --no-install-recommends -y \
    python-rosdep \
    python-rosinstall \
    python-vcstools \
    && rm -rf /var/lib/apt/lists/*
   rosdep init
   rosdep update
   
   apt-get update && apt-get install -y \
    ros-lunar-desktop-full=1.3.1-0* \
    && rm -rf /var/lib/apt/lists/*

    mkdir -p /opt/julia-0.6.2-dev && \
    curl -s -L https://julialang-s3.julialang.org/bin/linux/x64/0.6/julia-0.6.2-linux-x86_64.tar.gz | tar -C /opt/julia-0.6.2-dev -x -z --strip-components=1 -f -
    ln -fs /opt/julia-0.6.2-dev /opt/julia-0.6

    mkdir -p /workdir
    chmod 777 /workdir
    
    /opt/julia-0.6/bin/julia -e 'Pkg.init()'
    /opt/julia-0.6/bin/julia -e 'Pkg.add("Knet")'
    /opt/julia-0.6/bin/julia -e 'Pkg.add("RobotOS")'
    /opt/julia-0.6/bin/julia -e 'Pkg.add("JLD")'
    /opt/julia-0.6/bin/julia -e 'Pkg.add("ArgParse")'
    /opt/julia-0.6/bin/julia -e 'Pkg.add("LightXML")'
