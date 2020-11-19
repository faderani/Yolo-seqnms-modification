# Seq_nms_YOLO

#### Membres: Yunyun SUN, Yutong YAN, Sixiang XU, Heng ZHANG

---

## Introduction

![](img/index.jpg) 

This project combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) to realise **real time video detection**.

## Steps

1. Creación del entorno; crear un entorno con python3.7 a tu gusto
1. Ejecución  del  makefile\
2.1 Modificar en el makefile, las lineas 2 y 3 y poner sus flags a 0 (OPENCV Y CUDNN).\
2.2 Introducir la variable PATH con el siguiente comando export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}\
2.3 Instalar libreria cuda con comando sudo apt-getinstall nvidia-cuda-toolkit.\
2.4 En el makefile linea 49 y 51 cambiar el 8.0 por la versión de cuda que se disponga, en nuestro caso COMMON+=-DGPU -I/usr/local/cuda-10.1/include/.\
2.5 Ejecutar el makefile.
1. Descargar los pesos\
3.1 wget https://pjreddie.com/media/files/yolo.weights. Para los primeros pesos. \
3.2 wget https://pjreddie.com/media/files/yolov2-tiny.weights, para los segundos pesos.\
3.3 Si va muy lento o no funciona, se puede  acceder  a la  pagina  https://pjreddie.com/darknet/yolo/  y  desde ahí descargar los pesos correspondientes a YOLOv2608x608  y  Tiny  YOLO,  y  guardarlos en la carpeta principal.
1. Preprocesado  de  vídeo\
4.1 En primer lugar, se introduce el vídeo a analizar en la carpeta llamada "video". Y se accede al directorio de esa carpeta.\
4.2 En  el  script video2img.py introducir  parentesis  en todos los print.\
4.3 Instalar opencv: pip  install  opencv-python.\
4.4 python  video2img.py  -i  input.mp4 para cambiar elvideo a imágenes. input.mp4 es el nombre del vídeo.\
4.5 python getpkllist.py para obtener la lista con el nombre de los frames.
1. Método  de  detección\
5.1 Volver al directorio principal.\
5.2 En  el  script yoloseqnms.py,  introducir  igual  que antes los paréntesis en los print. \
5.3 En  la  línea  6  del  script  anterior,  sustituir importcPickle  as  pickle por importpickle  as  pickle. \
5.4 python  -m  pip  install  -U  matplotlib, para instalar matplotlib y sus dependencias. \
5.5 python -m pip install –user scipy, para instalar scipy. \
5.6 En el script yolodetection.py cambiar de nuevo los print. \
5.7 Después   introducir   import   os   al   principio   del script  anterior  y  sustituir  la  línea  37  por lib=CDLL(os.path.join(os.getcwd(),   ”libdarknet.so”),RTLDGLOBAL). \
5.8 Volver  a  la  línea  de  comandos  y  ejectuar  lo siguiente.\
5.8.1 export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}.\
5.8.2 export  LDLIBRARYPATH=$LDLIBRARYPATH:/usr/local/cuda-10.1/lib64.\
5.8.3 export  LIBRARYPATH=$LIBRARYPATH:/usr/local/cuda-10.1/lib64.\
5.9 instalar más librerías : conda  install  -y  -c  conda-forge  tensorflow. \
5.10 pip  install  tensorflow-object-detection-api.\
5.11 Volver al script yolodetection.py y sustituir:\
5.11.1 La  línea  139  por net  =  loadnet(bytes(cfg,’utf-8’),  bytes(weights,’utf-8’),  0).\
5.11.2 Línea 140 por meta  =  load(bytes(data,’utf-8’)).\
5.11.3 Línea 113 por im  =  loadimage(bytes(image,’utf-8’),  0,  0).\
5.12 En labelmaputil.py en   la   línea   116   sustituir tf.gfile.GFile(path,’r’) por tf.io.gfile.GFile(path,’r’).\
5.13 Instalar pip install imageio.\
5.14 En yolo_seqnms:\
5.14.1 Al principio del script incluir Import  imageio.\
5.14.2 Sustituir la línea 288 por imageio.imwrite(’video/output/frame{}.jpg’.format(i),imageprocess).\
5.14.3 En    la    l ́ınea    39    sustituirbox[0]==clsporstr(box[0],’utf-8’)==  cls.\
5.15 Ejecutar yoloseqnms.py para obtener los resultados.
1. Opcionalmente se puede ejecutar python img2video.py -i output para convertir las imágenes en un vídeo.


Verás los resultados finales en `video/output`


## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).
