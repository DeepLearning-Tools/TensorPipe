# TensorPipe
[![Library][tensorflow-shield]][tensorflow-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]


![alt text](logo.png)


High Performance Tensorflow Data Pipeline with State of Art Augmentations and low level optimizations.

## Features

- [x] High Performance tf.data pipline
- [x] Core tensorflow support for high performance
- [x] Classification data support
- [ ] Bbox data support
- [ ] Keypoints data support
- [ ] Segmentation data support
- [x] GridMask in core tf2.x
- [x] Mosiac Augmentation in core tf2.x
- [x] CutOut in core tf2.x
- [x] Flexible and easy configuration
- [x] Gin-config support

## Example Usage 1

```
from pipe import Funnel                                                         
from bunch import Bunch                                                         
"""                                                                             
Create a Funnel for the Pipeline!                                               
"""                                                                             


# Config for Funnel
config = {                                                                      
    "batch_size": 2,                                                            
    "image_size": [512,512],                                                    
    "transformations": {                                                        
        "flip_left_right": None,                                                
        "gridmask": None,                                                       
        "random_rotate":None,                                                   
    },                                                                          
    "categorical_encoding":"labelencoder"                                       
}                                                                               
config = Bunch(config)                                                          
pipeline = Funnel(data_path="testdata", config=config, datatype="categorical")  
pipeline = pipeline.dataset(type="train")                                       
                                                                                
# Pipline ready to use, iter over it to use.                                                      
for data in pipeline:                                                           
    print(data[0].shape, data[1].shape)                                     

```

## Config.
* **image_size** - Output Image Size for the pipeline.
* **batch_size** - Batch size for the pipeline.
* **transformations** - Dictionary of transformations to apply with respective keyword arguments.
* **categorical_encoding** - Encoding for categorical data - ('labelencoder' , 'onehotencoder').

## Augmentations:

### GridMask
Creates a gridmask on input image with rotation defined on range.
* **params**:
    * **ratio** - grid to space ratio
    * **fill** - fill value
    * **rotate** - rotation range in degrees

### MixUp
Mixes two randomly sampled images and their respective labels with given alpha.
* **params**:
    * **alpha** - value for blend function.

### RandomErase
Randomly erases rectangular chunk with is sampled randomly on given image.
* **params**:
    * **prob** - probablity to randomerase on image.

### CutMix
Overlaps a resized randomly sample image on given image with complete overlay on subset portion of image.
* **params**:
    * **prob** - probablity to CutMix on image.

### Mosaic
Creates a gridmask on input image with rotation defined on range.
* **params**:
    * **ratio** - grid to space ratio
    * **fill** - fill value
    * **rotate** - rotation range in degrees



## Release History
* v1.0
    * Bbox, Keypoints, Custom Py Functions Support.(WIP)
* v1.0-beta
    * Classification Support with gridmask and mosaic augmentations.

## Meta

Kartik Sharma – [@linkedIn](https://www.linkedin.com/in/kartik-sharma-aaa021169/) – kartik4949@gmail.com

Distributed under the Apache 2.0 license. See ``LICENSE`` for more information.


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[tensorflow-shield]: https://img.shields.io/badge/Tensorflow-2.x-orange
[tensorflow-url]: https://tensorflow.org
[license-shield]: https://img.shields.io/badge/OpenSource-%E2%9D%A4%EF%B8%8F-blue
[license-url]: LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/kartik-sharma-aaa021169/
