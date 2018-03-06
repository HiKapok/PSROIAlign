# PSROIAlign Operation In Tensorflow C++ API
PSROIAlign involves interpolation techniques for [PsRoiPooling](https://arxiv.org/abs/1605.06409) (position-sensitive RoI pooling operation), the interpolation idea is proposed in [RoIAlign](https://arxiv.org/abs/1703.06870) to avoid any quantization of the RoI boundaries. The first adoption of PSROIAlign might be in this paper [Light-Head R-CNN: In Defense of Two-Stage Object Detector](https://arxiv.org/abs/1711.07264).

You can find more details about the RoiPooling technique in [Fast R-CNN](https://arxiv.org/abs/1504.08083) and [Spatial Pyramid Pooling in Deep Convolutional Networks for Visual Recognition](https://arxiv.org/abs/1406.4729).

## ##
This repository contains code of the implement of PSROIAlign operation in Tensorflow C++ API. You can use this operation in many popular two-stage object detector. Both research work using PSROIAlign and contribution to this repository are welcomed. 

To using this op in your own machine, just following this script:
```sh
mkdir build
cd build && cmake ..
make
```
The code is tested under Tensorflow 1.5 with CUDA 8.0 using Ubuntu 16.04.

Update:

- Add support for mean pooling (default is max pooling)

Futher Work:

- Improve PSROIAlign to support oriented ROI inputs.

##  ##
The MIT License