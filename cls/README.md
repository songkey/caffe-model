## CLS (Classification)

Please install [py-RFCN-priv](https://github.com/soeaver/py-RFCN-priv) for evaluating and finetuning.

### Disclaimer

Most of the models are converted from other projects, the main contribution belongs to the original authors.

Project links:

[mxnet-model-gallery](https://github.com/dmlc/mxnet-model-gallery)、 [tensorflow slim](https://github.com/tensorflow/models/tree/master/slim)、 [craftGBD](https://github.com/craftGBD/craftGBD)、 [ResNeXt](https://github.com/facebookresearch/ResNeXt)、 [DenseNet](https://github.com/liuzhuang13/DenseNet)、 [wide-residual-networks](https://github.com/szagoruyko/wide-residual-networks)、 [keras deep-learning-models](https://github.com/fchollet/deep-learning-models)、 [ademxapp](https://github.com/itijyou/ademxapp)


### Performance on imagenet validation.
**1. Top-1/5 error of pre-train models in this repository.**

 Network|224/299<br/>(single-crop)|224/299<br/>(12-crop)|320/395<br/>(single-crop)|320/395<br/>(12-crop)
 :---:|:---:|:---:|:---:|:---:
 resnet18-priv| 29.11/10.07 | ../.. | ../.. | ../..
 resnext26-32x4d-priv| 24.93/7.75 | ../.. | ../.. | ../..
 resnet101-v2| 21.95/6.12 | 19.99/5.04 | 20.37/5.16 | 19.29/4.57
 resnet152-v2| 20.85/5.42 | 19.24/4.68 | 19.66/4.73 | 18.84/4.32
 resnet269-v2| **19.71**/5.00 | **18.25**/4.20 | 18.70/4.33 | **17.87**/3.85
 resnet38a| 20.66/5.27 | ../.. | 19.25/4.66 | ../..
 inception-v3| 21.67/5.75 | 19.60/4.73 | 20.10/4.82 | 19.25/4.24 
 xception| 20.90/5.49 | ../.. | 19.58/4.77 | ../.. 
 inception-v4| 20.03/5.09 | 18.60/4.30 | **18.68**/4.32 |18.12/3.92 
 inception-resnet-v2| 19.86/**4.83** | 18.46/**4.08** | 18.75/**4.02** | 18.15/**3.71**
 resnext50-32x4d| 22.37/6.31 | 20.53/5.35 | 21.10/5.53 | 20.37/5.03
 resnext101-32x4d| 21.30/5.79 | 19.47/4.89 | 19.91/4.97 | 19.19/4.59
 resnext101-64x4d| 20.60/5.41 | 18.88/4.59 | 19.26/4.63 | 18.48/4.31
 wrn50-2<br/>(resnet50-1x128d)| 22.13/6.13 | 20.09/5.06 | 20.68/5.28 | 19.83/4.87

 - The resnet18-priv, resnext26-32x4d-priv are trained under [pytorch](https://github.com/soeaver/pytorch-classification) by bupt-priv.
 - The pre-train models are tested on original [caffe](https://github.com/BVLC/caffe) by [evaluation_cls.py](https://github.com/soeaver/caffe-model/blob/master/cls/evaluation_cls.py), **but ceil_mode:false（pooling_layer） is used for the models converted from torch, the detail in https://github.com/BVLC/caffe/pull/3057/files**. If you remove ceil_mode:false, the performance will decline about 1% top1.
 - 224x224(base_size=256) and 320x320(base_size=320) crop size for resnet-v2/resnext/wrn, 299x299(base_size=320) and 395x395(base_size=395) crop size for inception.

**2. Top-1/5 accuracy with different crop sizes.**
![teaser](https://github.com/soeaver/caffe-model/blob/master/cls/accuracy.png)
 - Figure: Accuracy curves of inception_v3(left) and resnet101_v2(right) with different crop sizes.

**3. Download url and forward/backward time cost for each model.**

 Forward/Backward time cost is evaluated with one image/mini-batch using cuDNN 5.1 on a Pascal Titan X GPU.
 
 We use
  ```
    ~/caffe/build/tools/caffe -model deploy.prototxt time -gpu -iterations 1000
  ```
 to test the forward/backward time cost, the result is really different with time cost of [evaluation_cls.py](https://github.com/soeaver/caffe-model/blob/master/cls/evaluation_cls.py)

 Network|F/B(224/299)|F/B(320/395)|Download|Source
 :---:|:---:|:---:|:---:|:---:
 resnet101-v2| 22.31/22.75ms | 26.02/29.50ms | [170.3MB](https://pan.baidu.com/s/1kVQDHFx)|[craftGBD](https://github.com/craftGBD/craftGBD)
 resnet152-v2| 32.11/32.54ms | 37.46/41.84ms | [230.2MB](https://pan.baidu.com/s/1dFIc4vB)|[craftGBD](https://github.com/craftGBD/craftGBD)
 resnet269-v2| 58.20/59.15ms | 69.43/77.26ms | [390.4MB](https://pan.baidu.com/s/1qYbICs0)|[craftGBD](https://github.com/craftGBD/craftGBD)
 inception-v3| 21.79/19.82ms | 22.14/24.88ms | [91.1MB](https://pan.baidu.com/s/1boC0HEf)|[mxnet](https://github.com/dmlc/mxnet-model-gallery/blob/master/imagenet-1k-inception-v3.md)
 inception-v4| 32.96/32.19ms | 36.04/41.91ms | [163.1MB](https://pan.baidu.com/s/1c6D150)|[tensorflow_slim](https://github.com/tensorflow/models/tree/master/slim)
 inception-resnet-v2| 49.06/54.83ms | 54.06/66.38ms | [213.4MB](https://pan.baidu.com/s/1jHPJCX4)|[tensorflow_slim](https://github.com/tensorflow/models/tree/master/slim)
 resnext50_32x4d| 17.29/20.08ms | 19.02/23.81ms | [95.8MB](https://pan.baidu.com/s/1kVqgfJL)|[facebookresearch](https://github.com/facebookresearch/ResNeXt)
 resnext101_32x4d| 30.73/35.75ms | 34.33/41.02ms | [169.1MB](https://pan.baidu.com/s/1hswrNUG)|[facebookresearch](https://github.com/facebookresearch/ResNeXt)
 resnext101_64x4d| 42.07/64.58ms | 51.99/77.71ms | [319.2MB](https://pan.baidu.com/s/1pLhk0Zp)|[facebookresearch](https://github.com/facebookresearch/ResNeXt)
 wrn50_2<br/>(resnet50_1x128d)| 16.48/25.28ms | 20.99/35.04ms | [263.1MB](https://pan.baidu.com/s/1nvhoCsh)|[szagoruyko](https://github.com/szagoruyko/wide-residual-networks)

### Check the performance
**1. Download the ILSVRC 2012 classification val set [6.3GB](http://www.image-net.org/challenges/LSVRC/2012/nnoupb/ILSVRC2012_img_val.tar), and put the extracted images into the directory:**

      ~/Database/ILSVRC2012

**2. Modify the parameter settings**

 Network|val_file|mean_value|std
 :---:|:---:|:---:|:---:
 resnet_v2(101/152/269)| ILSVRC2012_val | [102.98, 115.947, 122.772] | [1.0, 1.0, 1.0]
 resnet18-priv, resnext26-32x4d-priv<br/>resnet38a, resnext50-32x4d<br/>resnext101-32x4d, resnext101-64x4d<br/>wrn50-2 | ILSVRC2012_val | [103.52, 116.28, 123.675] | [57.375, 57.12, 58.395]
 inception-v3| **ILSVRC2015_val** | [128.0, 128.0, 128.0] | [128.0, 128.0, 128.0] 
 inception-v2, xception<br/>inception-v4, inception-resnet-v2 | ILSVRC2012_val | [128.0, 128.0, 128.0] | [128.0, 128.0, 128.0] 


**3. then run evaluation_cls.py**

    python evaluation_cls.py
