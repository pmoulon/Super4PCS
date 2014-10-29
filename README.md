Super4PCS
=========

Copyright 2014 Nicolas Mellado

Authors: Nicolas Mellado, Dror Aiger


##Related pages
[Paper project page](http://geometry.cs.ucl.ac.uk/projects/2014/super4PCS)
[Github project page](https://github.com/nmellado/Super4PCS)
[Wiki](https://github.com/nmellado/Super4PCS/wiki)

##Overview
An implementation of the Super 4-points Congruent Sets (Super 4PCS) 
algorithm presented in:

>Super 4PCS: Fast Global Pointcloud Registration via Smart Indexing
>Nicolas Mellado, Dror Aiger, Niloy J. Mitra
>Symposium on Geometry Processing 2014.

Data acquisition in large-scale scenes regularly involves accumulating information across multiple scans. A common approach is to locally align scan pairs using Iterative Closest Point (ICP) algorithm (or its variants), but requires static scenes and small motion between scan pairs. This prevents accumulating data across multiple scan sessions and/or different acquisition modalities (e.g., stereo, depth scans). Alternatively, one can use a global registration algorithm allowing scans to be in arbitrary initial poses. The state-of-the-art global registration algorithm, 4PCS, however has a quadratic time complexity in the number of data points. This vastly limits its applicability to acquisition of large environments. We present Super 4PCS for global pointcloud registration that is optimal, i.e., runs in linear time (in 
the number of data points) and is also output sensitive in the complexity of the alignment problem based on the (unknown) overlap across scan pairs. Technically, we map the algorithm as an ‘instance problem’ and solve it efficiently using a smart indexing data organization. The algorithm is simple, memory-efficient, and fast. We demonstrate that Super 4PCS results in significant speedup over alternative approaches and allows unstructured efficient acquisition of scenes at scales previously not possible. Complete source code and datasets are available for research use at http://geometry.cs.ucl.ac.uk/projects/2014/super4PCS/.

##Development state
I am currently working on the source code to clean it and define a stable API. More interesting updates will come soon !

###Test
Tests are currently under active development (see [CDash](http://my.cdash.org/index.php?project=Super4PCS)). More tests will be added soon.

To submit the result of the test from your computer, go into your `build` directory, and run `ctest -D Experimental`. 

Tests currently available:
* pair_extraction: generate random point clouds in 2, 3 and 4D, and query the pair generation structure with various radius.
* matching: test the whole Super4PCS pipeline by registering range maps of the standford repository. You need an internet connection to build this test, since the datasets are downloaded at this time.


##Compilation
###Dependencies:
* [Eigen](http://eigen.tuxfamily.org/)
* [LibANN](http://www.cs.umd.edu/~mount/ANN/)
* [OpenCV](http://opencv.org/)
* [CFITSIO](http://heasarc.gsfc.nasa.gov/fitsio/fitsio.html), a dependency of chealpix. Both ubuntu and debian provide a virtual package 'cfitsio-dev'.

Super4PCS also requires [Chealpix](http://healpix.jpl.nasa.gov/html/csubnode4.htm), but we included it in the source tree to ease the installation procedure.


###Compiling
The simplest solution is to use cmake, from the source directory:
```
mkdir build
cd build
cmake -DANN_DIR=/your/path/to/ann_1.1.2/ ..
```
Note: For now Super4PCS has been tested on Linux plateforms (Ubuntu, Debian).

Chealpix sources are now part of the Super4PCS repository and are compiled automatically.
However, ANN doesn't come with a cmake package, so you need to set its path by hand (this will be fixed later).

###Compilation error
You may encounter compilation issues when compiling with old versions of Eigen and C++11:
```
/somePath/eigen3/Eigen/src/Core/util/Macros.h:252:35: error: unable to find string literal operator ‘operator""X’
 #define EIGEN_ASM_COMMENT(X)  asm("#"X)
                                    ^
/somePath/eigen3/Eigen/src/Core/products/GeneralBlockPanelKernel.h:604:1: note: in expansion of macro ‘EIGEN_ASM_COMMENT’
 EIGEN_ASM_COMMENT("mybegin2");
 ^
```
You can easily fix it by:
* update and use an up-to-date version of [Eigen](http://eigen.tuxfamily.org/). You may need to call
```
cmake -DEIGEN3_INCLUDE_DIR=/your/path/to/eigen/ ..
```
* Not recommended: modify one line in Eigen sources (Instructions [here](https://sourceforge.net/p/pagmo/mailman/message/30074799/)).


##Usage
A good starting point is to call the enclosed script `./run-example.sh`.

More details about parameter setting will be added soon. In the meantime please contact us to get support on parameter tuning (see section below).


##Contact
Please feel free to contact us if you have any question regarding this source code (see the [project page](http://geometry.cs.ucl.ac.uk/projects/2014/super4PCS/) for contact information).
