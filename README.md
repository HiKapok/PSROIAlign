# PsRoIAlign Operation In Tensorflow C++ API
PsRoIAlign involves interpolation techniques for [PsRoiPooling](https://arxiv.org/abs/1605.06409) (position-sensitive RoI pooling operation), the interpolation idea is proposed in [RoIAlign](https://arxiv.org/abs/1703.06870) to avoid any quantization of the RoI boundaries. The first adoption of PsRoIAlign might be in this paper [Light-Head R-CNN: In Defense of Two-Stage Object Detector](https://arxiv.org/abs/1711.07264).

You can find more details about the RoiPooling technique in [Fast R-CNN](https://arxiv.org/abs/1504.08083) and [Spatial Pyramid Pooling in Deep Convolutional Networks for Visual Recognition](https://arxiv.org/abs/1406.4729).

## ##
This repository contains code of the implement of PsRoIAlign operation in Tensorflow C++ API. You can use this operation in many popular two-stage object detector. Both research work using PsRoIAlign and contribution to this repository are welcomed. 

For using this op in your own machine, just following these steps:

- copy the header file "cuda\_config.h" from "your\_python\_path/site-packages/external/local\_config\_cuda/cuda/cuda/cuda\_config.h" to "your\_python\_path/site-packages/tensorflow/include/tensorflow/stream\_executor/cuda/cuda\_config.h".

- run the following script:


```sh
mkdir build
cd build && cmake ..
make
```

- run "test\_op.py" and check the numeric errors to test your install

- follow the below codes snippet to integrate this Op into your own code:

	```python
	op_module = tf.load_op_library(so_lib_path)
	ps_roi_align = op_module.ps_roi_align

	@ops.RegisterGradient("PsRoiAlign")
	def _ps_roi_align_grad(op, grad, _):
	  '''The gradients for `PsRoiAlign`.
	  '''
	  inputs_features = op.inputs[0]
	  rois = op.inputs[1]
	  pooled_features_grad = op.outputs[0]
	  pooled_index = op.outputs[1]
	  grid_dim_width = op.get_attr('grid_dim_width')
	  grid_dim_height = op.get_attr('grid_dim_height')
	
	  return [op_module.ps_roi_align_grad(inputs_features, rois, grad, pooled_index, grid_dim_width, grid_dim_height, pool_method), None]

	pool_method = 'max' # or 'mean'
	pool_result = ps_roi_align(features, rois, 2, 2, pool_method)
	```

The code is tested under TensorFlow 1.6 with CUDA 8.0 using Ubuntu 16.04. This PsRoIAlign Op had been used to train Xception based [Light-Head RCNN](https://arxiv.org/abs/1711.07264) successfully with performance at ~75%mAP on PASCAL VOC 2007 Test dataset, you can see codes [here](https://github.com/HiKapok/X-Detector). 

Update:

- Added support for mean pooling (default is max pooling)
- PsRoIAlign now support oriented RoI inputs (for both max and mean pooling).

Future Work:

- Check if there is need to ensure the convex of polygon
- Improve performance

If you encountered some linkage problem when generating or loading *.so, you are highly recommended to read this section in the [official tourial](https://www.tensorflow.org/extend/adding_an_op#compile_the_op_using_your_system_compiler_tensorflow_binary_installation) to make sure you were using the same C++ ABI version.

##  ##
The MIT License