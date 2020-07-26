# UCAS-AOD-benchmark
**A benchmark of UCAS-AOD dataset**. (Only Oriented box is tested)

More results  and PRs are welcomed **if you test with our imagesets** (for fair comparison).

## Introduction

There is no official division of the UCAS-AOD dataset, thus it's  troublesome to compare the performance on different models. This project is provided with a plan for dataset division, and you can directly make comparison with our test results if you adopt **the same division  strategy**.

## Dataset repare

1. Download  UCAS-AOD [dataset](https://hyper.ai/datasets/5419) .

2. Unzip dataset package into your root_dir, and rename the folder to `UCAS_AOD`.

3. Run `data_prepare.py `(modify the dataset dir to your own), and you will obtain directory as follow:
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
└───CAR
└───PLANE
└───Neg
```

4. Put our imageset files `train.txt`, `val.txt` and `test.txt` into `ImageSets` folder.
5. Train, eval and test you model according to `ImageSets`  settings.

**notes**: The integrated dataset contains 1510 images, with train set 755, val set 302, test set 452(following DOTA division 5:2:3). Files are numbered from 1-1510, in which `1-510` are cars, `511-1510` are airplanes. Besides, classname is attached to label file in format of  `classname x1 y1 x2 y2 x3 y3 x4 y4 theta cx cy w h ` ,

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

### Details

* Model are Training on **trainset** , and test on testset, valset is used for parameter optimization. 
* All models were trained with a batch size of 4, and totally 100 epochs, and the trained models are available at  [Baidu Drive](https://pan.baidu.com/s/15xsvYr8AKr7hV62obK3tkg).
* lr is set to 0.0001, we first warm up for 500 iters, and adjust lr with step 70 and 90 epochs. 
* we evaluate via **VOC07 metric** which is different DOTA and COCO. 
### Benchmark
| model | backbone | input_size | car | airplane | mAP |paper link |remarks |
| :---: | :---: |:--------: | :--: | :------: | :--: |:-----: |:-----: |
| Faster RCNN(OBB) | ResNet50 | 800*800 | 86.87 | 89.86 | 88.36 | —— | [code](https://github.com/dingjiansw101/AerialDetection) |
| RoI Transformer | ResNet50 | 800*800 | 87.99 | 89.90 | 88.95 | [CVPR2019](https://openaccess.thecvf.com/content_CVPR_2019/papers/Ding_Learning_RoI_Transformer_for_Oriented_Object_Detection_in_Aerial_Images_CVPR_2019_paper.pdf) | [code](https://github.com/dingjiansw101/RoITransformer_DOTA) |

## Some Results

![car](https://github.com/ming71/UCAS-AOD-benchmark/blob/master/examples/P0003.jpg)

![airplane](https://github.com/ming71/UCAS-AOD-benchmark/blob/master/examples/P1114.jpg)

---

**Notes** : If you have any problem about the benchmark or  the codes, pls contact me via [emal](mq_chaser@126.com) or issue, I will reply as soon as I see the message. 

