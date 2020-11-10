# Seq_nms_YOLO

## Introduction

This project combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) to realise **real time video detection**.

## Steps to execute

1. `make` the project
```
If we have NVIDIA GPU:
  GPU=1
  export PATH=/usr/local/cuda-10.1/bin:$PATH
If not: GPU=0

IF we have OpenCV install on the computer: OpenCV=1
IF you don't have it and you want to install it: read more in https://docs.opencv.org/3.3.1/d7/d9f/tutorial_linux_install.html
If you don't want to use it OpenCV=0

```
1. Download `yolo.weights` and `tiny-yolo.weights` by running
    ```
    wget https://pjreddie.com/media/files/yolo.weights
    wget https://pjreddie.com/media/files/yolov2-tiny-voc.weights -O tiny-yolo-voc.weights
    ```
1. While downloading the previous files create a Conda enviroment.
    ```
    conda create --name YOLOv2 python=2.7
    conda activate YOLOv2
    conda install -y -c menpo opencv
    conda install -y matplotlib Pillow scipy tensorflow=1.15
    conda install -y -c conda-forge tf_object_detection
    ```
1. Copy a video file to the video folder. We added some examples videos: `v_HighJump_g03_c04.avi`, `v_MilitaryParade_g09_c03.avi`, `v_SalsaSpin_g03_c02.avi`;
1. In the **video folder**, run `python video2img.py -i input_file` and then `python get_pkllist.py`;
1. Return to **root floder** and run `python yolo_seqnms.py` to generate output images in `video/output`;
1. If you want to reconstruct a video from these output images, you can go to the **video folder** and run `python img2video.py -i output`

And you will see `output.mp4` file with detection results in `video/` folder.

## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).
