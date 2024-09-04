# mnn_example
## alibaba MNN, mobilenet classifier, centerface detector, pfld landmarker and zqlandmarker, mobilefacenet
## **1.更新日志**
时间|更新内容
--|--
20200621| 1.remove the interface of GetImg;
20200320| 1.fix bug in face aligner;
20200305| 1.add ultraface and blending nms;
20200221| 1.add mobilefacenet;
20200220| 1.use template to reduce the reaptly code in NMS;
20200218| 1.refacter the project;
20200217| 1.add zwnet and face database;
20200216| 1.refacter the project and add zqlandmarker;
20200215| 1.add pfld landmarker and face aligner;
20200214| 1.add centerface detector;
20200205| 1.add object detection;
20200128| 1.add image classification;
## **2.How to use?**

 - (0). install env
```
sudo yum install gtk2-devel pkgconfig
sudo yum install libjpeg-turbo-devel libpng-devel libtiff-devel
yum install eigen3-devel
yum install gstreamer1-devel gstreamer1-plugins-base-devel
sudo yum install gtk3-devel

git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
cd opencv && mkdir build && cd build

cmake -D CMAKE_BUILD_TYPE=Release \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
      ..
make -j$(nproc)  # 使用所有可用的 CPU 核心进行编译
sudo make install
echo "/usr/local/lib" | sudo tee /etc/ld.so.conf.d/opencv.conf
sudo ldconfig
```

 - (1). convert model
 - - classifier model comes from: https://github.com/tensorflow/models/tree/master/research/slim
 - - object detection model comes from: https://github.com/C-Aniruddh/realtime_object_recognition
```
./MNNConvert -f TF --modelFile mobilenet_v1_1.0_224_frozen.pb --MNNModel mobilenet.mnn --bizCode MNN
```
```
./MNNConvert -f CAFFE --modelFile MobileNetSSD_deploy.caffemodel --prototxt MobileNetSSD_deploy.prototxt --MNNModel mobilenetssd.mnn --bizCode MNN
```
 - (2). build
```
mkdir build && cd build && make -j3 &&  cd src && ./classifier && ./object && ./face
```
 - (3). result 
 classifier result:
![图片](https://github.com/MirrorYuChen/MNN_mobilenet/blob/master/data/images/classify_result.jpg)
 object result:
![图片](https://github.com/MirrorYuChen/MNN_mobilenet/blob/master/data/images/object_result.jpg)
face detection result:
![图片](https://github.com/MirrorYuChen/MNN_mobilenet/blob/master/data/images/face_result.jpg)
## **3. TODO:**
 - [x] add pose
## **4. reference:**
### MNN: https://github.com/alibaba/MNN
### ZQCNN: https://github.com/zuoqing1988/ZQCNN
### MNN_APPLICATION: https://github.com/xindongzhang/MNN-APPLICATIONS
### insightface: https://github.com/deepinsight/insightface
### centerface: https://github.com/Star-Clouds/CenterFace
### ultraface: https://github.com/Linzaer/Ultra-Light-Fast-Generic-Face-Detector-1MB
### seetaface2: https://github.com/seetafaceengine/SeetaFace2
### csdn blog: https://blog.csdn.net/abcd740181246/article/details/90143848
