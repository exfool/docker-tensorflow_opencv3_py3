FROM gcr.io/tensorflow/tensorflow:1.1.0-rc2-gpu
#FROM gcr.io/tensorflow/tensorflow:0.12.1-gpu

# https://github.com/kampta/docker-tensorflow-opencv3.1

MAINTAINER Dmitry Bystritsky <exfool.dev@gmail.com>

RUN apt-get update && \
        apt-get upgrade -y && \
        apt-get install -y \
        build-essential \
        cmake \
        git \
        wget \
        unzip \
        yasm \
        pkg-config \
        libswscale-dev \
        libtbb2 \
        libtbb-dev \
        libjpeg-dev \
        libpng-dev \
        libtiff-dev \
        libjasper-dev \
        libavformat-dev \
        libpq-dev

RUN pip install docopt \
                Pillow \
                tqdm

RUN wget https://github.com/Itseez/opencv/archive/3.2.0.zip -O /opencv.zip\
&& unzip /opencv.zip -d / \
&& mkdir /opencv-3.2.0/cmake_binary \
&& cd /opencv-3.2.0/cmake_binary \
&& cmake -DBUILD_TIFF=ON \
  -DBUILD_opencv_java=OFF \
  -DWITH_CUDA=OFF \
  -DENABLE_AVX=ON \
  -DWITH_OPENGL=ON \
  -DWITH_OPENCL=ON \
  -DWITH_IPP=ON \
  -DWITH_TBB=ON \
  -DWITH_EIGEN=ON \
  -DWITH_V4L=ON \
  -DBUILD_TESTS=OFF \
  -DBUILD_PERF_TESTS=OFF \
  -DCMAKE_BUILD_TYPE=RELEASE \
  -DCMAKE_INSTALL_PREFIX=$(python -c "import sys; print(sys.prefix)") \
  -DPYTHON_EXECUTABLE=$(which python) \
  -DPYTHON_INCLUDE_DIR=$(python -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
  -DPYTHON_PACKAGES_PATH=$(python -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") .. \
&& make install \
&& rm /opencv.zip \
&& rm -r /opencv-3.2.0

RUN git clone https://github.com/aleju/imgaug.git \
&& cd imgaug \
&& python setup.py sdist \
&& pip install dist/imgaug-0.2.5.tar.gz \
&& cd .. \
&& rm -rf /imgaug

RUN mkdir /app
WORKDIR /app

ONBUILD COPY requirements.txt /notebooks/code
ONBUILD RUN pip install --no-cache-dir -r requirements.txt

ONBUILD COPY . /notebooks/code/
