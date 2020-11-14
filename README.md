# Seq_nms_YOLO

## Introduction

This project combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) to realise **real time video detection**.

## Steps to execute


1. Download `yolo.weights` and `tiny-yolo.weights` by running
    ```
    wget https://pjreddie.com/media/files/yolo.weights
    wget https://pjreddie.com/media/files/yolov2-tiny-voc.weights -O tiny-yolo-voc.weights
    ```
1. While downloading the previous files create a Conda enviroment.
    ```
    conda create -y --name YOLOv2 python=2.7
    conda activate YOLOv2
    conda install -y -c conda-forge opencv
    conda install -y matplotlib Pillow scipy tensorflow
    conda install -y -c conda-forge tf_object_detection
    ```   
1. Make sure that paths are correctly setted.
    ```
    export PATH=/usr/local/cuda-10.1/bin:$PATH
    ```
1. `make` the project.

    If you have a NVIDIA GPU you could set `GPU=1`. Also you might need to change the path of CUDA in lines `49 & 51`. If don't have GPU just write `GPU=0`.

    If you want to use OpenCV set the flag `OpenCV=1`. If you want to use it but don't know how installed https://docs.opencv.org/3.3.1/d7/d9f/tutorial_linux_install.html. If you don't want to use it just set `OpenCV=0`.

1. Copy a video file to the **video folder**. _(We added next videos as examples: `v_HighJump_g03_c04.avi`, `v_MilitaryParade_g09_c03.avi`, `v_SalsaSpin_g03_c02.avi`)_
1. In the **video folder**, run `python video2img.py -i input_file` and then run `python get_pkllist.py`.
1. Return to **root floder** and run `python yolo_seqnms.py` to generate output images in `video/output` folder.
    > From the `label_map_util.py` file in original repository we need to change `tf.gfile.GFil` by `tf.io.gfile.GFile` as the previous function is deprecated.
1. If you want to reconstruct a video from these output images, you can go to the **video folder** and run `python img2video.py -i output`.
    > From the `img2video.py` file in original repository we changed `cv2.cv.CV_FOURCC(*'mp4v')` by `cv2.VideoWriter_fourcc(*'mp4v')` as the previous functions was not able.
    > In the same file we commented `cv2.destroyAllWindows()` function as `libgtk2.0-dev` is not currently installed.
1. At last you will see `output.mp4` file with detection results in `video/` folder.

## Use Yolov2 without Seq-NMS

In order to deactivate Seq-NMS post-processing add to the `python yolo_seqnms.py` execution `--nms 0` flag.

## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).

Videos come from [UCF-101](https://www.crcv.ucf.edu/data/UCF101.php) dataset.
