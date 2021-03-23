# UCAS-AOD-benchmark
**A benchmark of UCAS-AOD dataset**. (Only Oriented box is tested)

To be continued...

## Introduction

There is no official division of the UCAS-AOD dataset, thus it's  troublesome to compare the performance on different models. You can directly make comparison with our test results if you adopt **the same division  strategy**.

## Dataset repare

1. Download  UCAS-AOD [dataset](https://hyper.ai/datasets/5419) .
2. Unzip dataset package into your root_dir, and rename the folder to `UCAS_AOD`.
3. Put our imageset files `train.txt`, `val.txt` and `test.txt` into `ImageSets` folder in `UCAS_AOD`.
4. Run `data_prepare.py `(modify the dataset dir to your own), and you will obtain directory as follow:
```
UCAS_AOD
└───AllImages
│   │   P0001.png
│   │   P0002.png
│   │	...
│   └───P1510.png
└───Annotations
│   │   P0001.txt
│   │   P0002.txt
│   │	...
│   └───P1510.txt       
└───ImageSets 
│   │   train.txt
│   │   val.txt
│   └───test.txt  
└───Test
│   │   P0003.png
│   │	...
│   └───P1508.txt 
└───CAR
└───PLANE
└───Neg
```

5. Train, eval and test you model according to `ImageSets`  settings.

**notes**: The integrated dataset contains 1510 images, with train set 755, val set 302, test set 452(following DOTA division 5:2:3). Files are numbered from 1-1510, in which `1-510` are cars, `511-1510` are airplanes. Besides, classname is attached to label file in format of  `classname x1 y1 x2 y2 x3 y3 x4 y4 theta lx ly w h ` ,

for example:

```
car  2.763971e+02	9.125021e+01	2.911375e+02	3.823406e+01	3.308891e+02	4.928647e+01	3.161486e+02	1.023026e+02	1.055379e+02	2.787673e+02	3.876027e+01	4.975157e+01	6.301615e+01	
car  3.002141e+02	1.003123e+02	3.209637e+02	4.665470e+01	3.566901e+02	6.047021e+01	3.359405e+02	1.141279e+02	1.111416e+02	3.055889e+02	4.856245e+01	4.572642e+01	6.365764e+01	
...
```

## Experiment

###  Environment
* NVIDIA 2080 Ti
* pytorch>1.1.0
* CUDA 10.0

### Details

* Models are Trained on **trainset** , and test on **testset**, valset is used for parameter optimization. 
* All models are available at  [Baidu Drive](https://pan.baidu.com/s/1TtJEY7dwvOOQpf61c9ATfg) with passward `sd4f`.
* `na` denotes number of anchors preset at each location of feature maps.
* Data augment is adopted (random flip, hsv augment, translation, rotation).
* All models are evaluated via **VOC07 metric**. 
### Benchmark
| model | backbone | input_size | na | car | airplane | mAP |paper link |remark |
| :---: | :---: |:--------: | :--: | :--: |:-----: |------- |------- |------- |
| R-Yolov3 | Darknet53 | 800*800 | 9 | 74.63 | 89.52 | 82.08 | [arxiv](https://arxiv.org/abs/1804.02767) |[code1](https://github.com/JKBox/YOLOv3-quadrangle), [code2](https://github.com/ming71/rotate-yolov3) |
| R-RetinaNet | ResNet50 | 800*800 | 3 | 84.64 | 90.51 | 87.57 |[ICCV 2017](https://openaccess.thecvf.com/content_iccv_2017/html/Lin_Focal_Loss_for_ICCV_2017_paper.html) |[code](https://github.com/ming71/R-RetinaNet) |
| Faster RCNN | ResNet50 | 800*800 | 3 | 86.87 | 89.86 | 88.36 | [CVPR 2018](https://arxiv.org/abs/1711.10398) | [code](https://github.com/dingjiansw101/AerialDetection) |
| RoI Transformer | ResNet50 | 800*800 | 3 | 88.02 | 90.02 | 89.02 | [CVPR 2019](https://openaccess.thecvf.com/content_CVPR_2019/papers/Ding_Learning_RoI_Transformer_for_Oriented_Object_Detection_in_Aerial_Images_CVPR_2019_paper.pdf) | [code](https://github.com/dingjiansw101/RoITransformer_DOTA) |
| RIDet-Q | ResNet50 | 800*800 | 9 | 88.50 | 89.96 | 89.23 | [arxiv](https://arxiv.org/abs/2103.11636) | [code](https://github.com/ming71/RIDet) |
| CFC-Net | ResNet50 | 800*800 | 1 | 89.29 | 88.69    | 89.49 | [arxiv](https://arxiv.org/abs/2101.06849) | [code](https://github.com/ming71/CFC-Net) |
| RIDet-O | ResNet50 | 800*800 | 9 | 88.88 | 90.35 | 89.62 | [arxiv](https://arxiv.org/abs/2103.11636) | [code](https://github.com/ming71/RIDet) |
| DAL | ResNet50 | 800*800 | 3 | 89.25 | 90.49    | 89.87 | [AAAI 2021](https://arxiv.org/abs/2012.04150) | [code](https://github.com/ming71/DAL) |
| S2ANet | ResNet50 | 800*800 | 1 | 89.56 | 90.42    | 89.99 | [TGRS](https://arxiv.org/pdf/2008.09397) | [code](https://github.com/csuhan/s2anet) |

## Some Results

![car](https://github.com/ming71/UCAS-AOD-benchmark/blob/master/examples/P0003.jpg)

![airplane](https://github.com/ming71/UCAS-AOD-benchmark/blob/master/examples/P1114.jpg)

---

**Notes** : More results  and PRs are welcomed if you test with imagesets division here.

