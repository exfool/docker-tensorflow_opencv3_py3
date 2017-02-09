# Docker image

Setting up OpenCV on [tensorflow image](gcr.io/tensorflow/tensorflow:0.12.1) using docker.


### Install
Build it (after copying the docker file),
```
docker build -t tensorflow_opencv3_py2 .
```
or pull from the docker
```
docker pull exfool/tensorflow_opencv3_py2
```

### Current versions
- [OpenCV: 3.2.0](https://github.com/Itseez/opencv/archive/3.2.0.zip)
- [TensorFlow: 0.12.1](gcr.io/tensorflow/tensorflow:0.12.1)
- Python: 2.7.6

### Related links
- [Nvidia Docker Hub ](https://hub.docker.com/r/tensorflow/tensorflow/tags/)
- (Image docker with OpenCV)[https://github.com/kampta/docker-tensorflow-opencv3.1]
