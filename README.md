
Singularity recipe to access GPU from host machine. It will spin up a jupyter notebook from singularity. 

CUDA 11.0 and tensorflow 2.2.0 and keras 2.4.0
=================================================================================================

Bootstrap: docker
#From: tensorflow/tensorflow:latest-gpu-py3-jupyter
From: nvcr.io/nvidia/tensorflow:20.08-tf2-py3
%help
This container is made by Shahinur Alam (sajonbuet@gmail.com)

%setup


%files
	
%labels
    Maintainer Shahinur
    Version 1.0

%environment


%post

	#pip install numpy pandas sklearn webcolors plotly matplotlib statsmodels factorial pynrrd pillow
	#pip install torch
	#pip install scikit-image medpy Tables tensorflow_addons nilearn SimpleITK h5py glob3 nibabel tifffile scipy opencv-python
	#pip install --upgrade keras
	pip install tensorflow-gpu==2.2.0	
			

%runscript
echo "Arguments received: $*"
port=$1
root_dir=$2
port=`echo $port| sed 's/ *$//g'`
root_dir=`echo $root_dir| sed 's/ *$//g'`
echo $port
jupyter notebook --no-browser --port $port --notebook-dir $root_dir --ip 0.0.0.0





Works with CUDA 10.1 
=====================================================================================================

Bootstrap: docker
From: tensorflow/tensorflow:latest-gpu-py3-jupyter
%help
This container is made by Shahinur Alam (sajonbuet@gmail.com)

%setup


%files
	
%labels
    Maintainer Shahinur
    Version 1.0

%environment


%post
	#pip install numpy pandas sklearn webcolors plotly matplotlib statsmodels factorial pynrrd pillow
	#pip install torch
	#pip install scikit-image medpy Tables tensorflow_addons nilearn SimpleITK h5py glob3 nibabel tifffile scipy opencv-python
	pip uninstall -y tensorflow tensorflow-addons tensorflow-estimator tensorflow-gpu tensorboard tensorboard-plugin-wit
	pip install --upgrade keras
	pip install --upgrade tensorflow	
	pip install tensorflow-addons==0.11.2
	pip install tensorflow-estimator==2.3.0
	pip install tensorflow-gpu==2.3.0
	pip install tensorboard==2.3.0
	pip install tensorboard-plugin-wit==1.7.0



		

%runscript
echo "Arguments received: $*"
port=$1
root_dir=$2
port=`echo $port| sed 's/ *$//g'`
root_dir=`echo $root_dir| sed 's/ *$//g'`
echo $port
jupyter notebook --no-browser --port $port --notebook-dir $root_dir --ip 0.0.0.0
