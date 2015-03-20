##Catkinized CMVS/PMVS2##

**CMVS is currently ```CATKIN_IGNORE```d since it consides a Metis version which collides with out metis_catkin repository.**

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
