# Integration of rosbag-extractor with rosdiscover as a node provider

## Steps 
### 1. Prepare the rosdiscover-extract-cxx volume

Rosdiscover uses a static analyzer program to extract information from the source code of your ROS nodes. It might seem like the rosdisover script is giving you correct output. But it will not be able to extract the correct information without this crucial part. This program will be built inside a docker container and then the binaries will be made available trough a docker volume. Then it will be mounted and run from inside the docker container of the robot solution. 

#### 1.1 Build docker-llvm
Build the [docker-llvm image](https://github.com/ChrisTimperley/docker-llvm) image. This will build the llvm compiler used to build `rosdicover-extract-cxx`. This might take a while. 

#### 1.2 Build rosdiscover-extract-cxx
1. Clone [the repo](https://github.com/cmu-rss-lab/rosdiscover-cxx-recover)
2. Add submodules with their correct versions 
   -  `cd extern`
   - `git clone https://github.com/fmtlib/fmt`
   - `cd fmt`
   - `git checkout d141cdbeb0fb422a3fb7173b285fd38e0d1772dc`
   - `cd ..`
   - `git clone https://github.com/nlohmann/json nlohmann_json`
   - `cd nlohmann_json`
   - `git checkout db78ac1d7716f56fc9f1b030b715f872f93964e4`
   - `cd ..`
   - `git clone https://github.com/mapbox/variant/`
   - `cd variant`
   - `git checkout a5a79a594f39d705a7ef969f54a0743516f0bc6d`
   - `cd ../../`
3.  Build the image
  - `cd docker`
  - `sudo make install`

After following these steps you will have a docker volume called `rosdiscover-cxx-extract-opt` ready to be mounted and used by `rosdiscover`. 
You can check if it was properly installed by running `sudo docker volume ls`.


