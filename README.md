## Catkinized CMVS/PMVS2

This is a catkinized version of CMVS and PMVS2, you will need to install ROS, catkin and create a catkin workspace. If you want to embed these packages into an existing workspace, make sure the dependencies listed below are available.

Follow these instructions: **Ubuntu 14.04 and ROS Indigo**

```bash
#Install ROS
sudo add-apt-repository "deb http://packages.ros.org/ros/ubuntu trusty main"
wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -
sudo apt-get update

sudo apt-get install ros-indigo-desktop-full liblapack-dev libblas-dev libboost-all-dev python-setuptools git g++ cppcheck default-jre libgtest-dev liblog4cplus-dev cimg-dev python-wstool python-catkin-tools 

# Update ROS environment
sudo rosdep init
rosdep update
echo ". /opt/ros/indigo/setup.bash" >> ~/.bashrc
source ~/.bashrc

# Create a catkin workspace
export CATKIN_WS=~/catkin_ws
mkdir -p $CATKIN_WS/src
cd $CATKIN_WS
catkin init
catkin config --merge-devel # Necessary for catkin_tools >= 0.4.
catkin config --extend /opt/ros/indigo
catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release
cd src

# Checkout main repository
git clone git@github.com:ethz-asl/cmvs_pmvs_catkin

# Checkout catkin dependencies
git clone git@github.com:ethz-asl/eigen_catkin.git
git clone git@github.com:ethz-asl/nlopt.git
git clone git@github.com:catkin/catkin_simple.git

# Build packages
catkin build cmvs_catkin pmvs_catkin
```

**Run Examples:**

The examples from the [original version](http://www.di.ens.fr/cmvs/documentation.html) work as well with some minor adaptations:
 * Source the catkin workspace to be able to access the executables: `source $CATKIN_WS/devel/setup.bash`
 * Use `rosrun` to execute the programs:
    * `rosrun cmvs_catkin cmvs`
    * `rosrun pmvs_catkin genOption`
    * `rosrun pmvs_catkin pmvs2`
 * The instructions to run the original datasets are still valid for the most part:
   ```bash
   # KERMIT DATASET
   cd kermit-after-bundler
   rosrun cmvs_catkin cmvs pmvs/
   rosrun pmvs_catkin genOption pmvs/
   sh pmvs/pmvs.sh
   
   # HALL DATASET
   cd hall-after-bundler
   rosrun cmvs_catkin cmvs pmvs/ 20
   rosrun pmvs_catkin genOption pmvs/
   sh pmvs/pmvs.sh
   
   # GENERIC
   rosrun cmvs_catkin cmvs $PMVS_FOLDER 20
   rosrun pmvs_catkin genOption $PMVS_FOLDER
   sh pmvs/pmvs.sh
   ```

**Dependencies:**

* Catkinized Eigen (e.g. [ethz-asl/eigen_catkin](https://github.com/ethz-asl/eigen_catkin))

* Catkinized nlopt (e.g. [ethz-asl/nlopt_catkin](https://github.com/ethz-asl/nlopt))

* catkin_simple (e.g. [ethz-asl/catkin_simple](https://github.com/ethz-asl/catkin_simple))

* Lapack (will be removed completely if performance is not an issue)

* JPEG

* Boost

* [Graclus (libmetis, libmultilevel):](http://www.cs.utexas.edu/users/dml/Software/graclus.html) Currently there is no need to add it, because a pared-down version is already included, but it will be replaced with a catkinized version.






**Autors:**

* [Modified CMVS version by Pierre Moulon](https://github.com/pmoulon/CMVS-PMVS)

* [Original CMVS version by Yasutaka Furukawa](http://www.di.ens.fr/cmvs/)
