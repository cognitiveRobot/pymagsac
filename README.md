# pymagsac

This repository contains an Python wrapper of [MAGSAC](https://arxiv.org/abs/1803.07469.pdf). 
Daniel Barath, Jana Noskova and Jiri Matas; MAGSAC: Marginalizing sample consensus, CVPR 2019

https://github.com/danini/magsac -- main repo. 

If you use the algorithm, please cite

```
@inproceedings{barath2019magsac,
	author = {Barath, Daniel and Matas, Jiri and Noskova, Jana},
	title = {MAGSAC: marginalizing sample consensus},
	booktitle = {Conference on Computer Vision and Pattern Recognition},
	year = {2019},
}

@inproceedings{barath2019magsacplusplus,
	author = {Barath, Daniel and Noskova, Jana and Ivashechkin, Maksym and Matas, Jiri},
	title = {MAGSAC++, a fast, reliable and accurate robust estimator},
	booktitle = {arXiv preprint:1912.05909},
	year = {2019},
}
```

If you use it for fundamental matrix estimation with DEGENSAC turned on, please cite

```
@inproceedings{Chum2005,
  author = {Chum, Ondrej and Werner, Tomas and Matas, Jiri},
  title = {Two-View Geometry Estimation Unaffected by a Dominant Plane},
  booktitle = {CVPR},
  year = {2005},
}
```



# Performance

Magsac is the state of the art according to the recent study Yin et.al."[Image Matching across Wide Baselines: From Paper to Practice](https://arxiv.org/abs/2003.01587.pdf)", 2020.

![IMW-benchmark](img/ransacs.png)


![IMW-Challenge](img/ransacs2.png)

# Requirements

- Python 3
- CMake 2.8.12 or higher
- Eigen3
- libgcc-ng
- OpenCV 3.4
- A modern compiler with C++17 support

# Preparation for conda env.
Activate conda env
```
conda activate torch
```
Install cmake
```
conda install -c conda-forge cmake
```
Install eigen3
```
conda install -c omnia eigen3
```
Install libgcc
```
conda install -c conda-forge libgcc-ng
```

# Installation

To build and install `python_cpp_example`, clone or download this repository, copy `estimators.h` from the `magsac` repo, update `cmake` file, and run `setpu.py install` as follows:

```bash
git clone https://github.com/cognitiveRobot/magsac.git
git clone https://github.com/cognitiverobot/pymagsac
cp magsac/include/estimators.h pymagsac/src/pymagsac/include/
sed -i 's@set(CMAKE_CXX_STANDARD 14)@set(CMAKE_CXX_STANDARD 17)@' pymagsac/CMakeLists.txt
cd pymagsac
python setup.py install
```

or

```bash (not tested.)
pip3 install .
```

# Example of usage

```python
import pymagsac
H, mask = pymagsac.findHomography(src_pts, dst_pts, 3.0)

#  findFundamentalMatrix arguments:
	# (x1y1: numpy.ndarray[float64], 
	# x2y2: numpy.ndarray[float64], 
	# use_magsac_plus_plus: bool=True, 
	# sigma_th: float=1.0, 
	# conf: float=0.99, 
	# max_iters: int=10000, 
	# partition_num: int=5)
F, mask = pymagsac.findFundamentalMatrix(src_pts, dst_pts, 3.0)

```

See also this [notebook](examples/example.ipynb)


# Acknowledgements

This wrapper part is based on great [Benjamin Jack `python_cpp_example`](https://github.com/benjaminjack/python_cpp_example).
