# Custom Darknet for training YOLO on Google Colab


## Setup darknet environment in Colab Notebook

To enable GPU backend for your notebook: __Runtime->Change runtime type->Hardware Accelerator->GPU__

```
# run these command line from notebook cell

!git clone https://github.com/Bhanu-mbvg/darknet_for_colab.git
%cd darknet_for_colab
!make
!chmod +x ./darknet
```

## Tuning parameters from Colab environment
Double click on `yolov4_config.py`to edit model parameters.
More details about the meaning of each parameter can be found [here](https://github.com/AlexeyAB/darknet/wiki/CFG-Parameters-in-the-%5Bnet%5D-section)

<br>
<p align="center"><img src="./data/edit_yolov4_config.png" width=1024></>


## Generate YOLOv4 config and test file
```
!python yolov4_setup.py
```

## Train with YOLOv4
```
!./darknet detector train data/yolov4.data cfg/yolov4_custom_train.cfg {weights_path} -map
```

## Predict with YOLOv4
- Image (predicted image is saved at `predictions.jpg`:
    ```
    %cp data/yolov4.data cfg/coco.data
    !./darknet detect cfg/yolov4_custom_test.cfg {weights_path} {img_path}
    ```

         
- Video:

    ```
    usage: darknet_video.py [-h] -v VIDEO [-c CONFIG] -w WEIGHTS [-l LABEL]
                    [-m META] [-o OUTPUT]

    optional arguments:
      -h, --help            show this help message and exit
      -v VIDEO, --video VIDEO
                            Path to input video
      -c CONFIG, --config CONFIG
                            Path to yolo config file
      -w WEIGHTS, --weights WEIGHTS
                            Path to yolo weight
      -l LABEL, --label LABEL
                            Path to label file
      -m META, --meta META  Path to metaPath
      -o OUTPUT, --output OUTPUT
                            Path to output file  
    ```
         
         
    ```
    !python darknet_video.py -v {video path} -c cfg/yolov4_custom_test.cfg -w {weights_path}  -o output.mp4
    ```
                                                                       
## License
[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

[MIT License](./LICENSE)
