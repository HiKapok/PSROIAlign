# PsRoIAlign Operation In Tensorflow C++ API
PsRoIAlign involves interpolation techniques for [PsRoiPooling](https://arxiv.org/abs/1605.06409) (position-sensitive RoI pooling operation), the interpolation idea is proposed in [RoIAlign](https://arxiv.org/abs/1703.06870) to avoid any quantization of the RoI boundaries. The first adoption of PsRoIAlign might be in this paper [Light-Head R-CNN: In Defense of Two-Stage Object Detector](https://arxiv.org/abs/1711.07264).

You can find more details about the RoiPooling technique in [Fast R-CNN](https://arxiv.org/abs/1504.08083) and [Spatial Pyramid Pooling in Deep Convolutional Networks for Visual Recognition](https://arxiv.org/abs/1406.4729).

## ##
This repository contains code of the implement of PsRoIAlign operation in Tensorflow C++ API. You can use this operation in many popular two-stage object detector. Both research work using PsRoIAlign and contribution to this repository are welcomed. 

For using this op in your own machine, just following this script:
```sh
mkdir build
cd build && cmake ..
make
```
The code is tested under Tensorflow 1.7 with CUDA 8.0 using Ubuntu 16.04. This PsRoIAlign Op had been used to train Xception based [Light-Head RCNN](https://arxiv.org/abs/1711.07264) successfully with performance at 70%+mAP on PASCAL VOC 2007 Test dataset, you can see codes [here](https://github.com/HiKapok/X-Detector). 

Update:

- Added support for mean pooling (default is max pooling)
- PsRoIAlign now support oriented RoI inputs (for both max and mean pooling).

Future Work:

- Check if there is need to ensure the convex of polygon
- Improve performance

##  ##
The MIT License