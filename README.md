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
1. Descargar los pesos;\
3.1 wget https://pjreddie.com/media/files/yolo.weights. Para los primeros pesos.\
3.2 wgethttps://pjreddie.com/media/files/yolov2-tiny.weights, para los segundos pesos.\
3.3 Si  va  muy  lento  o  no  funciona,  se  puede  acceder  ala  p ́agina  https://pjreddie.com/darknet/yolo/  y  desdeah ́ı descargar los pesos correspondientes a YOLOv2608x608  y  Tiny  YOLO,  y  guardarlos en la carpeta principal.\
1. Preprocesado  de  vídeo;\
4.1 En primer lugar, introduces el vídeo a analizar en la carpeta llamada vídeo. Y te introduces en el directoriode esa carpeta.\
4.2 En  el  scriptvideo2img.pyintroduces  par ́entesis  entodos los print.\
4.3 Instalar opencvpip  install  opencv-python.\
4.4 python  video2img.py  -i  input.mp4para cambiar elvideo a im ́agenes. input.mp4 es el nombre del v ́ıdeo.
4.5 python getpkllist.pypara ejecutar el preprocesado.
1. M ́etodo  de  detecci ́on;\
5.1 Volver al directorio principal. \
5.2 En  el  scriptyoloseqnms.py,  introduces  igual  queantes los par ́entesis en los print. \
5.3 En  la  l ́ınea  6  del  script  anterior,  sustituyesimportcPickle  as  pickleporimportpickle  as  pickle. \
5.4 python  -m  pip  install  -U  matplotlib, para instalarmatplotlib y sus dependencias. \
5.5 python -m pip install –user scipy, para instalar scipy. \
5.6 En el scriptyolodetection.pycambias de nuevo losprint. \
5.7 Despu ́es   introduces   import   os   el   principio   delscript  anterior  y  sustituyes  la  l ́ınea  37  porlib  =CDLL(os.path.join(os.getcwd(),   ”libdarknet.so”),RTLDGLOBAL). \
5.8 Volvemos  a  la  l ́ınea  de  comandos  y  ejecutamos  losiguiente\
5.8.1 exportPATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}\
5.8.2 export  LDLIBRARYPATH=$LDLIBRARYPATH:/usr/local/cuda-10.1/lib64.\
5.8.3 export  LIBRARYPATH=$LIBRARYPATH:/usr/local/cuda-10.1/lib64.\
5.9 conda  install  -y  -c  conda-forge  tensorflowinstalarm ́as librer ́ıas
5.10 pip  install  tensorflow-object-detection-api.
5.11 Volver al script yolodetection.py y sustituir:
5.11.1 La  l ́ınea  139  pornet  =  loadnet(bytes(cfg,’utf-8’),  bytes(weights,’utf-8’),  0)
5.11.2 L ́ınea 140 pormeta  =  load(bytes(data,’utf-8’))
5.11.3 L ́ınea 113 porim  =  loadimage(bytes(image,’utf-8’),  0,  0)
5.12 Enlabelmaputil.pyen   la   l ́ınea   116   sustituirtf.gfile.GFile(path,   ’r’)portf.io.gfile.GFile(path,’r’)
5.13 nstalar pip install imageio
5.14 En yoloseqnms
5.14.1 Al principio del script incluirImport  imageio.
5.14.2 Sustituirlal ́ınea288porima-geio.imwrite(’video/output/frame{}.jpg’.format(i),imageprocess)
5.14.3 En    la    l ́ınea    39    sustituirbox[0]==clsporstr(box[0],’utf-8’)==  cls
5.15 Ejecutar yoloseqnms.py para obtener los resultados


And you will see detection results in `video/output`

## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).
