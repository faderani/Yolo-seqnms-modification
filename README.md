# Seq_nms_YOLO

#### Membres: Yunyun SUN, Yutong YAN, Sixiang XU, Heng ZHANG

---

## Introduction

![](img/index.jpg) 

This project combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) to realise **real time video detection**.

## Steps

1. Creación del entorno; crear un entorno con python3.7 a tu gusto;
1. Ejecución  del  makefile;\
2.1 Modificar en el makefile, las lineas 2 y 3 y poner susflags a 0 (OPENCV Y CUDNN).;\
2.2 Introducir la variable PATH con el siguiente comando exportPATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}};\
2.3 Instalar libreria cuda con comando sudo apt-getinstall nvidia-cuda-toolkit.;\
2.4 En el makefile linea 49 y 51 cambiar el 8.0 por la versión de cuda que se disponga, en nuestro caso COM-MON+=-DGPU -I/usr/local/cuda-10.1/include/.;\
2.5 Ejecutar el makefile.\;
1. Descargar  los  pesos;\
3.1 wget https://pjreddie.com/media/files/yolo.weights. Para los primeros pesos.\
1. In the video folder, run `python video2img.py -i input.mp4` and then `python get_pkllist.py`;
1. Return to root floder and run `python yolo_seqnms.py` to generate output images in `video/output`;
1. If you want to reconstruct a video from these output images, you can go to the video folder and run `python img2video.py -i output`

And you will see detection results in `video/output`

## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).
